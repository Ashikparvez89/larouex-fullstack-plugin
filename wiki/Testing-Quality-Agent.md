# Testing & Quality Agent

## Overview

The Testing & Quality Agent specializes in implementing comprehensive testing strategies, code quality assurance, and maintaining high standards across web applications. It handles unit tests, integration tests, E2E tests, performance testing, accessibility testing, and quality metrics.

**Primary Technologies:**
- Jest for unit testing
- React Testing Library for component tests
- Playwright for E2E testing
- Lighthouse CI for performance
- axe-core for accessibility
- ESLint and Prettier for code quality

## Core Capabilities

### 1. Testing Strategy Implementation
- Unit testing for components and utilities
- Integration testing for API endpoints
- End-to-end testing for user flows
- Performance testing with Lighthouse
- Accessibility testing with axe-core
- Visual regression testing

### 2. Code Quality Assurance
- TypeScript type safety enforcement
- ESLint configuration and rules
- Code formatting with Prettier
- Code complexity analysis
- Security vulnerability scanning
- Pre-commit hooks

### 3. Test Coverage Management
- Coverage reports and metrics
- Critical path identification
- Test gap analysis
- Coverage improvement strategies
- CI/CD integration

### 4. Quality Metrics & Reporting
- Code quality dashboards
- Test execution reports
- Performance benchmarks
- Accessibility scores
- Security audit reports

## Common Commands

Commands that frequently use this agent:

- `/add-unit-test` - Unit tests
- `/add-integration-test` - Integration tests
- `/add-e2e-test` - E2E test suite
- `/audit-accessibility` - Accessibility testing
- `/optimize-performance` - Performance testing
- `/audit-security` - Security testing

## Key Implementation Patterns

### Component Testing

```typescript
// tests/unit/components/Hero.test.tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import Hero from '@/components/sections/Hero';

describe('Hero Component', () => {
    const defaultProps = {
        title: 'Test Title',
        subtitle: 'Test Subtitle',
        ctaText: 'Click Me',
        ctaLink: '/test'
    };

    it('renders title and subtitle', () => {
        render(<Hero {...defaultProps} />);

        expect(screen.getByText('Test Title')).toBeInTheDocument();
        expect(screen.getByText('Test Subtitle')).toBeInTheDocument();
    });

    it('renders CTA button with correct link', () => {
        render(<Hero {...defaultProps} />);

        const button = screen.getByRole('link', { name: 'Click Me' });
        expect(button).toHaveAttribute('href', '/test');
    });

    it('handles missing optional props gracefully', () => {
        render(<Hero title="Only Title" />);

        expect(screen.getByText('Only Title')).toBeInTheDocument();
        expect(screen.queryByRole('link')).not.toBeInTheDocument();
    });
});
```

### Hook Testing

```typescript
// tests/unit/hooks/useTracking.test.ts
import { renderHook, act } from '@testing-library/react';
import { useTracking } from '@/lib/monitoring/hooks/useTracking';

jest.mock('@/lib/monitoring/appInsights.client', () => ({
    appInsights: {
        trackEvent: jest.fn(),
        trackMetric: jest.fn()
    }
}));

describe('useTracking Hook', () => {
    beforeEach(() => {
        jest.clearAllMocks();
    });

    it('tracks events with properties', () => {
        const { result } = renderHook(() => useTracking());

        act(() => {
            result.current.trackEvent('TestEvent', {
                property1: 'value1'
            });
        });

        expect(appInsights.trackEvent).toHaveBeenCalledWith({
            name: 'TestEvent',
            properties: expect.objectContaining({
                property1: 'value1',
                timestamp: expect.any(String)
            })
        });
    });
});
```

### API Integration Testing

```typescript
// tests/integration/api/emailclaim.test.ts
import { createMocks } from 'node-mocks-http';
import handler from '@/api/src/functions/emailclaim';
import { TableClient } from '@azure/data-tables';

jest.mock('@azure/data-tables');

describe('Email Claim API', () => {
    let mockTableClient: jest.Mocked<TableClient>;

    beforeEach(() => {
        mockTableClient = {
            createEntity: jest.fn(),
            getEntity: jest.fn(),
            listEntities: jest.fn()
        } as any;

        (TableClient.fromConnectionString as jest.Mock).mockReturnValue(
            mockTableClient
        );
    });

    describe('POST /api/emailclaim/create', () => {
        it('creates new claim successfully', async () => {
            const { req, res } = createMocks({
                method: 'POST',
                body: { email: 'test@example.com' }
            });

            mockTableClient.listEntities.mockResolvedValue([]);
            mockTableClient.createEntity.mockResolvedValue({});

            await handler(req, res);

            expect(res._getStatusCode()).toBe(201);
            expect(JSON.parse(res._getData())).toEqual({
                success: true,
                claimCode: expect.any(String),
                claimUrl: expect.stringContaining('/redeem?code=')
            });
        });

        it('prevents duplicate claims', async () => {
            const { req, res } = createMocks({
                method: 'POST',
                body: { email: 'existing@example.com' }
            });

            mockTableClient.listEntities.mockResolvedValue([
                { email: 'existing@example.com' }
            ] as any);

            await handler(req, res);

            expect(res._getStatusCode()).toBe(409);
        });
    });
});
```

### End-to-End Testing with Playwright

```typescript
// playwright.config.ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
    testDir: './tests/e2e',
    timeout: 30000,
    fullyParallel: true,
    retries: process.env.CI ? 2 : 0,
    reporter: [
        ['html'],
        ['junit', { outputFile: 'test-results/junit.xml' }]
    ],
    use: {
        baseURL: process.env.BASE_URL || 'http://localhost:3000',
        trace: 'on-first-retry',
        screenshot: 'only-on-failure',
        video: 'retain-on-failure'
    },
    projects: [
        {
            name: 'chromium',
            use: { ...devices['Desktop Chrome'] }
        },
        {
            name: 'Mobile Chrome',
            use: { ...devices['Pixel 5'] }
        }
    ],
    webServer: {
        command: 'npm run dev',
        port: 3000,
        reuseExistingServer: !process.env.CI
    }
});
```

```typescript
// tests/e2e/flows/redemption.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Email Redemption Flow', () => {
    test('complete redemption process', async ({ page }) => {
        await page.goto('/redeem?code=TEST_CODE');

        // Wait for validation
        await expect(page.getByText('Validating your claim')).toBeVisible();

        // Fill form
        await page.fill('[name="firstName"]', 'John');
        await page.fill('[name="lastName"]', 'Doe');
        await page.selectOption('[name="country"]', 'US');

        // Submit
        await page.click('button[type="submit"]');

        // Verify success
        await expect(page.getByText('Thank you!')).toBeVisible();
    });

    test('handles invalid claim code', async ({ page }) => {
        await page.goto('/redeem?code=INVALID');

        await expect(page.getByText('Invalid or expired claim')).toBeVisible();
    });
});
```

### Accessibility Testing

```typescript
// tests/e2e/accessibility.spec.ts
import { test, expect } from '@playwright/test';
import AxeBuilder from '@axe-core/playwright';

test.describe('Accessibility', () => {
    const pages = ['/', '/about', '/contact'];

    pages.forEach(path => {
        test(`should not have violations on ${path}`, async ({ page }) => {
            await page.goto(path);

            const accessibilityScanResults = await new AxeBuilder({ page })
                .withTags(['wcag2a', 'wcag2aa'])
                .analyze();

            expect(accessibilityScanResults.violations).toEqual([]);
        });
    });

    test('keyboard navigation works', async ({ page }) => {
        await page.goto('/');

        // Tab through navigation
        await page.keyboard.press('Tab');
        await expect(page.getByRole('link', { name: 'Home' })).toBeFocused();

        await page.keyboard.press('Tab');
        await expect(page.getByRole('link', { name: 'About' })).toBeFocused();
    });
});
```

### Performance Testing with Lighthouse

```javascript
// lighthouserc.js
module.exports = {
    ci: {
        collect: {
            url: [
                'http://localhost:3000/',
                'http://localhost:3000/about'
            ],
            numberOfRuns: 3
        },
        assert: {
            assertions: {
                'categories:performance': ['error', { minScore: 0.85 }],
                'categories:accessibility': ['error', { minScore: 0.9 }],
                'first-contentful-paint': ['error', { maxNumericValue: 2000 }],
                'largest-contentful-paint': ['error', { maxNumericValue: 3000 }],
                'cumulative-layout-shift': ['error', { maxNumericValue: 0.1 }]
            }
        }
    }
};
```

## Code Quality Tools

### ESLint Configuration

```javascript
// .eslintrc.js
module.exports = {
    extends: [
        'next/core-web-vitals',
        'plugin:@typescript-eslint/recommended',
        'plugin:jest/recommended',
        'plugin:testing-library/react',
        'prettier'
    ],
    plugins: ['@typescript-eslint', 'jest', 'testing-library'],
    rules: {
        '@typescript-eslint/explicit-module-boundary-types': 'error',
        '@typescript-eslint/no-explicit-any': 'error',
        '@typescript-eslint/no-unused-vars': [
            'error',
            { argsIgnorePattern: '^_' }
        ],
        'no-console': ['warn', { allow: ['warn', 'error'] }],
        'react-hooks/exhaustive-deps': 'error'
    }
};
```

### Pre-commit Hooks

```json
// package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.{ts,tsx}": [
      "eslint --fix",
      "prettier --write",
      "jest --bail --findRelatedTests"
    ],
    "*.{json,md,css}": [
      "prettier --write"
    ]
  }
}
```

## CI/CD Testing Pipeline

### GitHub Actions Test Workflow

```yaml
name: Tests

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Use Node.js 20.x
        uses: actions/setup-node@v3
        with:
          node-version: '20.x'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run linters
        run: |
          npm run lint
          npm run typecheck

      - name: Run unit tests
        run: npm run test:unit -- --coverage

      - name: Run integration tests
        run: npm run test:integration

      - name: Setup Playwright
        run: npx playwright install --with-deps

      - name: Run E2E tests
        run: npm run test:e2e

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info
```

## Test Coverage Requirements

### Coverage Thresholds

```json
// jest.config.js
module.exports = {
    coverageThreshold: {
        global: {
            branches: 80,
            functions: 80,
            lines: 80,
            statements: 80
        },
        './src/components/': {
            branches: 90,
            functions: 90
        },
        './src/lib/utils/': {
            branches: 95,
            functions: 95
        }
    }
};
```

## Platform-Specific Details

### Test Structure
```
tests/
├── unit/              # Unit tests
│   ├── components/
│   ├── utils/
│   └── hooks/
├── integration/      # Integration tests
│   └── api/
├── e2e/             # End-to-end tests
│   ├── flows/
│   └── pages/
├── fixtures/        # Test data
└── mocks/          # Mock implementations
```

## Related Agents

- **Frontend-Development-Agent**: Component implementation
- **Security-Production-Agent**: Security testing
- **Accessibility-Compliance-Agent**: Accessibility standards
- **Monitoring-Observability-Agent**: Performance metrics

## Best Practices Checklist

- [ ] Write tests before implementation (TDD)
- [ ] Aim for 80%+ code coverage
- [ ] Test edge cases and error conditions
- [ ] Mock external dependencies
- [ ] Use descriptive test names
- [ ] Keep tests isolated and independent
- [ ] Run tests in CI/CD pipeline
- [ ] Test accessibility with axe-core
- [ ] Monitor test execution time
- [ ] Review test coverage reports

## Common Pitfalls

1. **Testing Implementation Details**: Test behavior, not implementation
2. **Slow Tests**: Mock heavy operations, use test databases
3. **Flaky Tests**: Avoid time-dependent tests, use proper waits
4. **Low Coverage**: Focus on critical paths first
5. **No E2E Tests**: Always test complete user flows

## Reference Resources

- [Jest Documentation](https://jestjs.io/docs)
- [React Testing Library](https://testing-library.com/docs/react-testing-library)
- [Playwright Documentation](https://playwright.dev/docs)
- [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)
- [axe-core](https://github.com/dequelabs/axe-core)
