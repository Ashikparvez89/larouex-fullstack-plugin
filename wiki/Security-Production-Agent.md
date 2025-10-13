# Security & Production Agent

## Overview

The Security & Production Agent specializes in security best practices, production issue resolution, emergency recovery procedures, and maintaining platform stability. It handles security configuration, incident response, deployment safety, and emergency rollback procedures.

**Primary Focus:**
- Environment variable protection
- API key and secret management
- Authentication and authorization
- Input validation and sanitization
- CORS and CSP configuration
- Production incident response
- Emergency rollback procedures

## Core Capabilities

### 1. Security Management
- Environment variable protection
- API key and secret management
- Authentication and authorization
- Input validation and sanitization
- CORS and CSP configuration
- Security headers implementation
- XSS and CSRF prevention

### 2. Production Incident Response
- Emergency rollback procedures
- 403/404/500 error resolution
- Performance degradation fixes
- CDN and caching issues
- SSL certificate management
- Service outage recovery

### 3. Deployment Safety
- Pre-deployment checklists
- Staging validation procedures
- Rollback procedures
- Environment configuration verification
- Health check validation

## Common Commands

Commands that frequently use this agent:

- `/audit-security` - Security audit
- `/setup-environment` - Environment configuration
- `/deploy-azure-production` - Production deployment
- `/deploy-railway-production` - Production deployment
- `/review-security` - Security review
- `/review-before-deploy` - Pre-deployment gate

## Critical Security Rules

### Environment Files

**NEVER commit .env files to Git!**

```gitignore
# Correct gitignore entries
.env*
*.env
.env.local
.env.production
```

### API Keys and Secrets

- Always use environment variables
- Never hardcode credentials
- Use Azure Key Vault for production
- Rotate keys regularly
- Use different keys per environment

### Current Environment Variables

```env
# Application Insights (Public keys - OK to expose)
NEXT_PUBLIC_APPINSIGHTS_INSTRUMENTATION_KEY=xxx
NEXT_PUBLIC_APPINSIGHTS_CONNECTION_STRING=xxx

# Azure Storage (Secret - NEVER expose)
AZURE_STORAGE_CONNECTION_STRING=xxx

# API Configuration
NEXT_PUBLIC_API_URL=https://your-api.azurewebsites.net
```

## Recent Production Issues & Resolutions

### Issue: Site Returns 403 Forbidden

**Cause:** Complex middleware with domain routing broke Azure Static Web Apps

**Solution:**
1. Remove middleware domain routing
2. Disable static export conflicts
3. Simplify staticwebapp.config.json
4. Clear CDN cache

### Issue: Deployment Fails - "No matching Static Web App"

**Cause:** Workflow token mismatch or missing swa-db-connections

**Solution:**
1. Verify workflow file matches Azure instance
2. Add placeholder swa-db-connections directory
3. Check deployment token in GitHub secrets

### Issue: Application Insights Missing Data

**Cause:** Numeric values in customDimensions are dropped

**Solution:** Convert all values to strings before tracking

## Emergency Recovery Procedures

### Quick Rollback (30 seconds)

```bash
# Revert last commit
git revert HEAD
git push origin main

# Or reset to known good commit
git reset --hard <good-commit-hash>
git push --force-with-lease origin main
```

### Production Site Down

1. **Check Azure Portal** - Service health, recent deployments
2. **Verify DNS** - Ensure domain points to correct Azure instance
3. **Check Workflows** - GitHub Actions for failed deployments
4. **Review Logs** - Application Insights for errors
5. **Rollback** - Use emergency procedures above

### Fixing Broken Deployments

```bash
# Check current workflows
ls -la .github/workflows/

# Remove conflicting workflows
git rm .github/workflows/azure-static-web-apps-<wrong-id>.yml

# Commit and push
git commit -m "Fix deployment workflow"
git push origin main
```

## Security Checklist

### Before Each Deployment

- [ ] No .env files in git status
- [ ] No hardcoded API keys or secrets
- [ ] All environment variables documented
- [ ] Security headers configured correctly
- [ ] CORS settings appropriate
- [ ] Input validation on all forms
- [ ] API rate limiting enabled

### Production Configuration

- [ ] HTTPS enforced
- [ ] CSP headers configured
- [ ] X-Frame-Options: DENY
- [ ] X-Content-Type-Options: nosniff
- [ ] Referrer-Policy configured
- [ ] API authentication required

## Azure Static Web Apps Security

### Static Web App Configuration

```json
{
  "routes": [
    {
      "route": "/api/*",
      "allowedRoles": ["anonymous"]
    },
    {
      "route": "/admin/*",
      "allowedRoles": ["authenticated", "administrator"]
    }
  ],
  "responseOverrides": {
    "401": {
      "statusCode": 401,
      "redirect": "/login"
    },
    "403": {
      "statusCode": 403,
      "redirect": "/unauthorized"
    }
  },
  "globalHeaders": {
    "X-Frame-Options": "DENY",
    "X-Content-Type-Options": "nosniff",
    "Referrer-Policy": "origin-when-cross-origin",
    "X-XSS-Protection": "1; mode=block"
  }
}
```

### Input Validation

```typescript
import Joi from 'joi';

const schema = Joi.object({
    email: Joi.string().email().required(),
    name: Joi.string().min(2).max(100).required(),
    age: Joi.number().integer().min(0).max(150).optional()
});

export function validateInput(data: any) {
    const { error, value } = schema.validate(data, {
        abortEarly: false,
        stripUnknown: true
    });

    if (error) {
        throw new APIError(400, 'Validation failed', error.details);
    }

    return value;
}
```

### CORS Configuration

```typescript
// Azure Functions
export async function handler(
    request: HttpRequest,
    context: InvocationContext
): Promise<HttpResponseInit> {
    return {
        status: 200,
        headers: {
            'Access-Control-Allow-Origin': 'https://yourdomain.com',
            'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE',
            'Access-Control-Allow-Headers': 'Content-Type, Authorization',
            'Access-Control-Max-Age': '86400'
        },
        jsonBody: { data: 'response' }
    };
}
```

### CSRF Protection

```typescript
// Generate CSRF token
export function generateCSRFToken(): string {
    return crypto.randomBytes(32).toString('hex');
}

// Validate CSRF token
export function validateCSRFToken(token: string, expectedToken: string): boolean {
    return crypto.timingSafeEqual(
        Buffer.from(token),
        Buffer.from(expectedToken)
    );
}
```

## Monitoring & Alerts

### Key Metrics to Watch

- Error rate > 1%
- Response time > 2s
- Failed deployments
- 4xx/5xx status codes
- Authentication failures

### Application Insights Alerts

```kql
// High error rate alert
requests
| where timestamp > ago(5m)
| summarize errorRate = countif(success == false) * 100.0 / count()
| where errorRate > 1
```

## Common Vulnerabilities & Mitigations

### XSS Prevention

- Sanitize all user input
- Use React's built-in escaping
- Configure CSP headers
- Validate on server side

**Example:**
```typescript
import DOMPurify from 'dompurify';

export function sanitizeHTML(dirty: string): string {
    return DOMPurify.sanitize(dirty, {
        ALLOWED_TAGS: ['b', 'i', 'em', 'strong', 'a'],
        ALLOWED_ATTR: ['href']
    });
}
```

### CSRF Protection

- Use SameSite cookies
- Implement CSRF tokens for mutations
- Verify referrer headers

```typescript
// Set secure cookie
response.setHeader('Set-Cookie', [
    `token=${token}; HttpOnly; Secure; SameSite=Strict; Path=/`
]);
```

### SQL Injection

- Use parameterized queries
- Validate input patterns
- Use ORM/query builders

**Note:** Not applicable when using NoSQL Table Storage, but still validate input patterns.

## Testing Security

### Local Testing

```bash
# Check for exposed secrets
grep -r "DefaultEndpointsProtocol" --exclude-dir=node_modules .
grep -r "InstrumentationKey" --exclude-dir=node_modules .

# Verify .env not tracked
git ls-files | grep -E "\.env"
```

### Production Validation

```bash
# Test security headers
curl -I https://yoursite.com

# Check SSL certificate
openssl s_client -connect yoursite.com:443

# Test CORS configuration
curl -H "Origin: https://malicious.com" \
     -H "Access-Control-Request-Method: POST" \
     -X OPTIONS https://yoursite.com/api/endpoint
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

## Incident Response Plan

### Severity Levels

- **P0**: Site completely down (rollback within 5 minutes)
- **P1**: Major functionality broken (within 1 hour)
- **P2**: Performance degradation (within 4 hours)
- **P3**: Minor issues (next business day)

### Communication

1. Update status page
2. Notify stakeholders
3. Document in incident log
4. Post-mortem after resolution

## Environment Management

### Local Development (.env.local)

```env
NEXT_PUBLIC_API_URL=http://localhost:7071
AZURE_STORAGE_CONNECTION_STRING=UseDevelopmentStorage=true
```

### Production (Azure Configuration)

- Set in Azure Portal → Configuration
- Never commit production values
- Use Azure Key Vault for secrets
- Rotate keys quarterly

## Platform-Specific Details

### File Locations

**Security Configuration:**
- `/staticwebapp.config.json` - Azure security settings
- `/.gitignore` - Ensure .env files excluded
- `/next.config.ts` - Security headers

**Deployment Files:**
- `/.github/workflows/` - CI/CD pipelines
- `/api/host.json` - Azure Functions security

## Related Agents

- **Azure-Serverless-Agent**: Azure security configuration
- **DevOps-Azure-Agent**: Deployment security
- **DevOps-Railway-Agent**: Railway security
- **Monitoring-Observability-Agent**: Security monitoring

## Best Practices

1. **Never trust client input**
2. **Always use HTTPS**
3. **Keep dependencies updated**
4. **Monitor security advisories**
5. **Regular security audits**
6. **Incident response plan**
7. **Backup and recovery procedures**

## Recent Lessons Learned

### What Broke Production

- Complex middleware with static export
- Untested Azure-specific behaviors
- Environment variable conflicts
- Security header duplication

### What Prevented Issues

- Staging environment testing
- Quick rollback procedures
- Version control discipline
- Monitoring and alerts

## Reference Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Azure Security Best Practices](https://docs.microsoft.com/azure/security/fundamentals/best-practices-and-patterns)
- [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
- [CORS Documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
