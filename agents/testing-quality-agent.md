# Testing & Quality Agent

## Purpose
Specialized agent for implementing comprehensive testing strategies, code quality assurance, and maintaining high standards across the H2All Web CMS project, including unit tests, integration tests, E2E tests, and quality metrics.

## Core Responsibilities

### 1. Testing Strategy Implementation
- Unit testing for components and utilities
- Integration testing for API endpoints
- End-to-end testing for user flows
- Performance testing
- Accessibility testing

### 2. Code Quality Assurance
- TypeScript type safety enforcement
- ESLint configuration and rules
- Code formatting with Prettier
- Code complexity analysis
- Security vulnerability scanning

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

## Technical Context

### Testing Stack
- **Unit Testing**: Jest, React Testing Library
- **Integration Testing**: Supertest
- **E2E Testing**: Playwright or Cypress
- **Performance**: Lighthouse CI
- **Accessibility**: axe-core
- **Security**: npm audit, OWASP

### Test Structure
```
tests/
├── unit/                    # Unit tests
│   ├── components/
│   ├── utils/
│   └── hooks/
├── integration/            # Integration tests
│   ├── api/
│   └── services/
├── e2e/                   # End-to-end tests
│   ├── flows/
│   └── pages/
├── fixtures/              # Test data
├── mocks/                # Mock implementations
└── utils/                # Test utilities
```

## Unit Testing

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

    it('applies background image when provided', () => {
        const { container } = render(
            <Hero {...defaultProps} backgroundImage="/test-bg.jpg" />
        );

        const image = container.querySelector('img[src*="test-bg.jpg"]');
        expect(image).toBeInTheDocument();
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

// Mock Application Insights
jest.mock('@/lib/monitoring/appInsights.client', () => ({
    appInsights: {
        trackEvent: jest.fn(),
        trackMetric: jest.fn(),
        trackException: jest.fn()
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

    it('tracks metrics correctly', () => {
        const { result } = renderHook(() => useTracking());

        act(() => {
            result.current.trackMetric('TestMetric', 42);
        });

        expect(appInsights.trackMetric).toHaveBeenCalledWith({
            name: 'TestMetric',
            average: 42
        });
    });
});
```

### Utility Function Testing
```typescript
// tests/unit/utils/emailClaimUtils.test.ts
import {
    normalizeEmail,
    validateEmail,
    generateClaimCode,
    isExpired
} from '@/lib/utils/emailClaimUtils';

describe('Email Claim Utilities', () => {
    describe('normalizeEmail', () => {
        it('converts to lowercase', () => {
            expect(normalizeEmail('USER@EXAMPLE.COM')).toBe('user@example.com');
        });

        it('removes leading/trailing whitespace', () => {
            expect(normalizeEmail('  user@example.com  ')).toBe('user@example.com');
        });

        it('handles Gmail plus addressing', () => {
            expect(normalizeEmail('user+tag@gmail.com')).toBe('user@gmail.com');
        });
    });

    describe('validateEmail', () => {
        it('accepts valid emails', () => {
            const validEmails = [
                'user@example.com',
                'user.name@example.co.uk',
                'user+tag@example.com'
            ];

            validEmails.forEach(email => {
                expect(validateEmail(email)).toBe(true);
            });
        });

        it('rejects invalid emails', () => {
            const invalidEmails = [
                'notanemail',
                '@example.com',
                'user@',
                'user @example.com'
            ];

            invalidEmails.forEach(email => {
                expect(validateEmail(email)).toBe(false);
            });
        });
    });

    describe('generateClaimCode', () => {
        it('generates code of correct length', () => {
            const code = generateClaimCode();
            expect(code).toHaveLength(12);
        });

        it('generates unique codes', () => {
            const codes = new Set();
            for (let i = 0; i < 100; i++) {
                codes.add(generateClaimCode());
            }
            expect(codes.size).toBe(100);
        });
    });
});
```

## Integration Testing

### API Endpoint Testing
```typescript
// tests/integration/api/emailclaim.test.ts
import { createMocks } from 'node-mocks-http';
import handler from '@/api/src/functions/emailclaim';
import { TableClient } from '@azure/data-tables';

// Mock Azure Table Storage
jest.mock('@azure/data-tables');

describe('Email Claim API', () => {
    let mockTableClient: jest.Mocked<TableClient>;

    beforeEach(() => {
        mockTableClient = {
            createEntity: jest.fn(),
            getEntity: jest.fn(),
            updateEntity: jest.fn(),
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
                body: {
                    email: 'test@example.com'
                }
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
                body: {
                    email: 'existing@example.com'
                }
            });

            mockTableClient.listEntities.mockResolvedValue([
                { email: 'existing@example.com' }
            ] as any);

            await handler(req, res);

            expect(res._getStatusCode()).toBe(409);
            expect(JSON.parse(res._getData())).toEqual({
                error: 'Claim already exists for this email'
            });
        });

        it('validates email format', async () => {
            const { req, res } = createMocks({
                method: 'POST',
                body: {
                    email: 'invalid-email'
                }
            });

            await handler(req, res);

            expect(res._getStatusCode()).toBe(400);
            expect(JSON.parse(res._getData())).toEqual({
                error: 'Invalid email format'
            });
        });
    });

    describe('GET /api/emailclaim/validate', () => {
        it('validates existing claim', async () => {
            const { req, res } = createMocks({
                method: 'GET',
                query: {
                    code: 'VALID_CODE'
                }
            });

            mockTableClient.getEntity.mockResolvedValue({
                partitionKey: 'EMAIL_CLAIM',
                rowKey: 'VALID_CODE',
                email: 'test@example.com',
                status: 'pending',
                expiresAt: new Date(Date.now() + 86400000).toISOString()
            } as any);

            await handler(req, res);

            expect(res._getStatusCode()).toBe(200);
            expect(JSON.parse(res._getData())).toEqual({
                valid: true,
                email: 'test@example.com',
                status: 'pending'
            });
        });

        it('rejects expired claims', async () => {
            const { req, res } = createMocks({
                method: 'GET',
                query: {
                    code: 'EXPIRED_CODE'
                }
            });

            mockTableClient.getEntity.mockResolvedValue({
                partitionKey: 'EMAIL_CLAIM',
                rowKey: 'EXPIRED_CODE',
                expiresAt: new Date(Date.now() - 86400000).toISOString()
            } as any);

            await handler(req, res);

            expect(res._getStatusCode()).toBe(410);
            expect(JSON.parse(res._getData())).toEqual({
                error: 'Claim has expired'
            });
        });
    });
});
```

## End-to-End Testing

### Playwright Configuration
```typescript
// playwright.config.ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
    testDir: './tests/e2e',
    timeout: 30000,
    expect: {
        timeout: 5000
    },
    fullyParallel: true,
    forbidOnly: !!process.env.CI,
    retries: process.env.CI ? 2 : 0,
    workers: process.env.CI ? 1 : undefined,
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
        },
        {
            name: 'Mobile Safari',
            use: { ...devices['iPhone 12'] }
        }
    ],

    webServer: {
        command: 'npm run dev',
        port: 3000,
        reuseExistingServer: !process.env.CI
    }
});
```

### E2E Test Examples
```typescript
// tests/e2e/flows/redemption.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Email Redemption Flow', () => {
    test('complete redemption process', async ({ page }) => {
        // Navigate to redemption page
        await page.goto('/redeem?code=TEST_CODE');

        // Wait for validation
        await expect(page.getByText('Validating your claim')).toBeVisible();

        // Fill form
        await page.fill('[name="firstName"]', 'John');
        await page.fill('[name="lastName"]', 'Doe');
        await page.selectOption('[name="country"]', 'US');

        // Submit
        await page.click('button[type="submit"]');

        // Wait for success
        await expect(page.getByText('Thank you!')).toBeVisible();
        await expect(page.getByText(/gallons of water/)).toBeVisible();

        // Check impact display
        const impactValue = await page.getByTestId('impact-gallons').textContent();
        expect(parseInt(impactValue || '0')).toBeGreaterThan(0);
    });

    test('handles invalid claim code', async ({ page }) => {
        await page.goto('/redeem?code=INVALID');

        await expect(page.getByText('Invalid or expired claim')).toBeVisible();
        await expect(page.getByRole('link', { name: 'Contact Support' })).toBeVisible();
    });

    test('validates form inputs', async ({ page }) => {
        await page.goto('/redeem?code=TEST_CODE');

        // Try submitting empty form
        await page.click('button[type="submit"]');

        // Check validation messages
        await expect(page.getByText('First name is required')).toBeVisible();
        await expect(page.getByText('Last name is required')).toBeVisible();
    });
});
```

### Accessibility Testing
```typescript
// tests/e2e/accessibility.spec.ts
import { test, expect } from '@playwright/test';
import AxeBuilder from '@axe-core/playwright';

test.describe('Accessibility', () => {
    const pages = [
        '/',
        '/about',
        '/impact',
        '/shop',
        '/contact'
    ];

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
        await expect(page.getByRole('link', { name: 'About Us' })).toBeFocused();

        // Activate dropdown with Enter
        await page.keyboard.press('Tab');
        await page.keyboard.press('Enter');
        await expect(page.getByRole('link', { name: 'Water Projects' })).toBeVisible();
    });
});
```

## Performance Testing

### Lighthouse CI Configuration
```javascript
// lighthouserc.js
module.exports = {
    ci: {
        collect: {
            url: [
                'http://localhost:3000/',
                'http://localhost:3000/about',
                'http://localhost:3000/impact',
                'http://localhost:3000/shop'
            ],
            numberOfRuns: 3
        },
        assert: {
            assertions: {
                'categories:performance': ['error', { minScore: 0.85 }],
                'categories:accessibility': ['error', { minScore: 0.9 }],
                'categories:best-practices': ['error', { minScore: 0.9 }],
                'categories:seo': ['error', { minScore: 0.9 }],
                'first-contentful-paint': ['error', { maxNumericValue: 2000 }],
                'largest-contentful-paint': ['error', { maxNumericValue: 3000 }],
                'cumulative-layout-shift': ['error', { maxNumericValue: 0.1 }],
                'total-blocking-time': ['error', { maxNumericValue: 300 }]
            }
        },
        upload: {
            target: 'temporary-public-storage'
        }
    }
};
```

### Load Testing
```typescript
// tests/load/api-load.test.ts
import { check } from 'k6';
import http from 'k6/http';
import { Rate } from 'k6/metrics';

export const errorRate = new Rate('errors');

export const options = {
    stages: [
        { duration: '2m', target: 100 }, // Ramp up
        { duration: '5m', target: 100 }, // Stay at 100 users
        { duration: '2m', target: 0 }    // Ramp down
    ],
    thresholds: {
        http_req_duration: ['p(95)<500'], // 95% of requests under 500ms
        errors: ['rate<0.05']              // Error rate under 5%
    }
};

export default function () {
    // Test email claim creation
    const payload = JSON.stringify({
        email: `test${__VU}${__ITER}@example.com`
    });

    const params = {
        headers: { 'Content-Type': 'application/json' }
    };

    const response = http.post(
        'http://localhost:7071/api/emailclaim/create',
        payload,
        params
    );

    check(response, {
        'status is 201': (r) => r.status === 201,
        'response has claim code': (r) => {
            const body = JSON.parse(r.body);
            return body.claimCode !== undefined;
        }
    });

    errorRate.add(response.status !== 201);
}
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
        'react/jsx-no-target-blank': 'error',
        'react-hooks/exhaustive-deps': 'error'
    },
    overrides: [
        {
            files: ['*.test.ts', '*.test.tsx'],
            env: {
                jest: true
            }
        }
    ]
};
```

### Prettier Configuration
```json
// .prettierrc
{
  "semi": true,
  "trailingComma": "none",
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 4,
  "useTabs": false,
  "bracketSpacing": true,
  "arrowParens": "always",
  "endOfLine": "lf"
}
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

    strategy:
      matrix:
        node-version: [18.x, 20.x]

    steps:
      - uses: actions/checkout@v3

      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
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

      - name: Run Lighthouse CI
        run: npm run lhci:autorun

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info

      - name: Upload test results
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: test-results
          path: |
            coverage/
            playwright-report/
            .lighthouseci/
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

### Coverage Reports
```bash
# Generate coverage report
npm run test:coverage

# View HTML report
open coverage/lcov-report/index.html

# Check coverage thresholds
npm run test:coverage -- --watchAll=false
```

## Security Testing

### Dependency Scanning
```bash
# Regular npm audit
npm audit

# Fix vulnerabilities
npm audit fix

# Check for outdated packages
npm outdated

# OWASP dependency check
npm run security:check
```

### Security Headers Test
```typescript
// tests/security/headers.test.ts
import { test, expect } from '@playwright/test';

test('security headers are present', async ({ page }) => {
    const response = await page.goto('/');

    expect(response?.headers()['x-frame-options']).toBe('DENY');
    expect(response?.headers()['x-content-type-options']).toBe('nosniff');
    expect(response?.headers()['referrer-policy']).toBe('strict-origin-when-cross-origin');
    expect(response?.headers()['content-security-policy']).toBeTruthy();
});
```

## Reference Resources
- [Jest Documentation](https://jestjs.io/docs)
- [React Testing Library](https://testing-library.com/docs/react-testing-library)
- [Playwright Documentation](https://playwright.dev/docs)
- [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)