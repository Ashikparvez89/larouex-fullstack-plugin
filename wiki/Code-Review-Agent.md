# Code Review Agent

## Overview

The Code Review Agent is an automated code review specialist that ensures quality, security, performance, and best practices in Next.js full-stack applications. It provides comprehensive analysis across 10 review categories with severity-based issue classification.

## Core Expertise

### Technology Stack
- Next.js 15 App Router patterns
- React 18+ component patterns and hooks
- TypeScript strict mode compliance
- Bootstrap 5 responsive design
- Azure Functions and Railway deployments
- Database optimization (Prisma, Azure Table Storage)

### Review Capabilities
- Code quality and maintainability
- Security vulnerability detection (OWASP Top 10)
- Performance optimization
- Accessibility compliance (WCAG 2.1 AA)
- TypeScript type safety
- API security and validation
- Database query optimization
- Error handling patterns
- Test coverage assessment
- Documentation completeness

## Review Categories

### 1. Code Quality (Weight: 15%)
- Clean code principles
- DRY (Don't Repeat Yourself)
- SOLID principles
- Naming conventions
- Code complexity
- Readability

### 2. Security (Weight: 20%)
- Input validation
- SQL injection prevention
- XSS protection
- Authentication checks
- Authorization verification
- Sensitive data handling
- CORS configuration
- Rate limiting

### 3. Performance (Weight: 15%)
- Bundle size optimization
- Lazy loading
- Caching strategies
- Database query optimization
- API response times
- Core Web Vitals
- Memory leaks

### 4. TypeScript (Weight: 10%)
- Type safety
- Any usage
- Type inference
- Interface definitions
- Generic usage
- Strict mode compliance

### 5. React Best Practices (Weight: 10%)
- Component structure
- Hook usage
- State management
- Props validation
- Memoization
- Effect dependencies

### 6. Accessibility (Weight: 10%)
- WCAG 2.1 AA compliance
- ARIA attributes
- Keyboard navigation
- Screen reader support
- Focus management
- Color contrast

### 7. Testing (Weight: 10%)
- Test coverage
- Test quality
- Edge cases
- Mock usage
- Integration tests
- E2E tests

### 8. Documentation (Weight: 5%)
- Code comments
- JSDoc/TSDoc
- README files
- API documentation
- Complex logic explanation

### 9. Error Handling (Weight: 5%)
- Try-catch blocks
- Error boundaries
- Logging
- User feedback
- Graceful degradation

### 10. Platform-Specific (Weight: Variable)
- Azure best practices
- Railway optimizations
- Deployment configurations
- Environment variables
- CI/CD setup

## Severity Levels

### Critical 🔴
- Security vulnerabilities
- Data loss risks
- Authentication bypasses
- Production blockers
- Compliance violations

### High 🟠
- Performance issues
- Memory leaks
- Missing error handling
- Type safety violations
- Accessibility barriers

### Medium 🟡
- Code smells
- Suboptimal patterns
- Missing tests
- Documentation gaps
- Minor security issues

### Low 🟢
- Style inconsistencies
- Minor optimizations
- Nice-to-have features
- Code formatting

### Info ℹ️
- Best practice suggestions
- Alternative approaches
- Learning opportunities
- Future improvements

## Common Commands

The Code Review Agent works with these commands:

- `/review-code` - Review uncommitted changes
- `/review-component` - Deep component analysis
- `/review-api` - API endpoint review
- `/review-security` - Security-focused audit
- `/review-performance` - Performance analysis
- `/review-before-deploy` - Pre-deployment gate

## Review Process

### 1. Automated Analysis
```typescript
interface ReviewProcess {
  stages: [
    'Parse code changes',
    'Run static analysis',
    'Check patterns',
    'Identify issues',
    'Calculate severity',
    'Generate report'
  ]
}
```

### 2. Issue Detection
```typescript
interface Issue {
  category: ReviewCategory
  severity: 'critical' | 'high' | 'medium' | 'low' | 'info'
  file: string
  line: number
  message: string
  suggestion?: string
  autofix?: boolean
}
```

### 3. Report Generation
```typescript
interface ReviewReport {
  summary: {
    score: number // 0-100
    passed: boolean
    criticalIssues: number
    totalIssues: number
  }
  issues: Issue[]
  recommendations: string[]
  blockers: Issue[] // Must fix before deployment
}
```

## Platform-Specific Validation

### Azure Validation
- Function app configuration
- Connection string security
- App settings validation
- CORS settings
- Authentication setup
- Deployment slots

### Railway Validation
- Environment variables
- Database connections
- Build configuration
- Health checks
- Scaling settings
- Domain configuration

## Quality Gates

### Pre-Deployment Requirements
```typescript
interface QualityGate {
  mandatory: {
    noCriticalIssues: boolean
    securityPassed: boolean
    testsPass: boolean
    buildSucceeds: boolean
  }
  recommended: {
    highIssuesResolved: boolean
    testCoverage: number // >= 80%
    performanceScore: number // >= 90
    accessibilityScore: number // >= 90
  }
}
```

## Best Practices Enforcement

### React Components
```tsx
// ✅ Good: Memoized expensive computation
const ExpensiveComponent = memo(({ data }) => {
  const processedData = useMemo(
    () => expensiveProcess(data),
    [data]
  )
  return <div>{processedData}</div>
})

// ❌ Bad: Computation on every render
const ExpensiveComponent = ({ data }) => {
  const processedData = expensiveProcess(data)
  return <div>{processedData}</div>
}
```

### TypeScript Types
```typescript
// ✅ Good: Strict types
interface UserData {
  id: string
  name: string
  email: string
}

// ❌ Bad: Any usage
const userData: any = { ... }
```

### Security Patterns
```typescript
// ✅ Good: Input validation
const sanitizedInput = validator.escape(userInput)

// ❌ Bad: Direct user input
const query = `SELECT * FROM users WHERE name = '${userInput}'`
```

## Integration with CI/CD

### GitHub Actions Integration
```yaml
- name: Run Code Review
  run: |
    npm run review:code
    npm run review:security
    npm run review:before-deploy
```

### Quality Gate Enforcement
```typescript
if (review.criticalIssues > 0) {
  throw new Error('Critical issues must be resolved before deployment')
}
```

## Common Issues Detected

### Security Issues
- Exposed API keys
- Missing authentication
- SQL injection vulnerabilities
- XSS vulnerabilities
- Insecure dependencies

### Performance Issues
- Large bundle sizes
- Unoptimized images
- N+1 queries
- Missing indexes
- Memory leaks

### Code Quality Issues
- Duplicate code
- Complex functions
- Deep nesting
- Unused variables
- Missing error handling

## Related Agents

- [Security & Production Agent](Security-Production-Agent) - Security focus
- [Testing & Quality Agent](Testing-Quality-Agent) - Test coverage
- [Performance Agent](Monitoring-Observability-Agent) - Performance monitoring

## Review Metrics

### Code Quality Score
```typescript
interface QualityMetrics {
  maintainability: number // 0-100
  reliability: number // 0-100
  security: number // 0-100
  performance: number // 0-100
  overall: number // Weighted average
}
```

## Continuous Improvement

- Learn from false positives
- Update patterns regularly
- Incorporate team standards
- Track issue trends
- Measure fix rates

---

For more information, see:
- [Commands Overview](Commands-Overview)
- [Testing Strategies](Testing-Quality-Agent)
- [Security Best Practices](Security-Production-Agent)