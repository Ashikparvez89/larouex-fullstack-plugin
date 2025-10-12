# Security & Production Issues Agent

## Vision
Protect the platform that delivers clean water to those in need. Every security measure ensures donor trust and recipient impact.

## Purpose
Specialized in security best practices, production issue resolution, emergency recovery procedures, and maintaining platform stability for the H2All Web Platform.

## Core Responsibilities

### 1. Security Management
- Environment variable protection
- API key and secret management
- Authentication and authorization
- Input validation and sanitization
- CORS and CSP configuration

### 2. Production Incident Response
- Emergency rollback procedures
- 403/404/500 error resolution
- Performance degradation fixes
- CDN and caching issues
- SSL certificate management

### 3. Deployment Safety
- Pre-deployment checklists
- Staging validation
- Rollback procedures
- Environment configuration

## Critical Security Rules

### Environment Files
**NEVER commit .env files to Git!**
```gitignore
# Correct gitignore entries
.env*
*.env
```

### API Keys and Secrets
- Always use environment variables
- Never hardcode credentials
- Use Azure Key Vault for production
- Rotate keys regularly

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

### Issue: Site Returns 403 Forbidden (September 2025)
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

# Ensure correct production workflow (icy-sky)
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

### Current Configuration (staticwebapp.config.json)
```json
{
  "routes": [
    {
      "route": "/api/*",
      "allowedRoles": ["anonymous"]  // Consider restricting
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
  }
}
```

### Security Headers
Configure in staticwebapp.config.json, not next.config.ts:
```json
{
  "globalHeaders": {
    "X-Frame-Options": "DENY",
    "X-Content-Type-Options": "nosniff",
    "Referrer-Policy": "origin-when-cross-origin",
    "X-XSS-Protection": "1; mode=block"
  }
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

### SQL Injection
- Not applicable (using NoSQL Table Storage)
- Still validate input patterns

### CSRF Protection
- Use SameSite cookies
- Implement CSRF tokens for mutations
- Verify referrer headers

## Best Practices

1. **Never trust client input**
2. **Always use HTTPS**
3. **Keep dependencies updated**
4. **Monitor security advisories**
5. **Regular security audits**
6. **Incident response plan**
7. **Backup and recovery procedures**

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
1. Run security headers test
2. Check SSL certificate
3. Verify CORS configuration
4. Test authentication flows
5. Monitor for unusual activity

## Incident Response Plan

### Severity Levels
- **P0**: Site completely down
- **P1**: Major functionality broken
- **P2**: Performance degradation
- **P3**: Minor issues

### Response Times
- P0: Immediate (rollback within 5 minutes)
- P1: Within 1 hour
- P2: Within 4 hours
- P3: Next business day

### Communication
1. Update status page
2. Notify stakeholders
3. Document in incident log
4. Post-mortem after resolution

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

## File Locations

### Security Configuration
- `/staticwebapp.config.json` - Azure security settings
- `/.gitignore` - Ensure .env files excluded
- `/next.config.ts` - Next.js security headers (if not using static export)

### Deployment Files
- `/.github/workflows/azure-static-web-apps-*.yml` - CI/CD pipelines
- `/api/host.json` - Azure Functions security

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

Last Updated: September 23, 2025