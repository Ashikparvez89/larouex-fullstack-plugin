# Troubleshooting Guide

Common issues and solutions for the Full-Stack Website Builder plugin.

## Installation Issues

### Plugin Not Found

**Symptoms:**
- Commands don't appear when typing `/`
- Claude doesn't recognize commands

**Solutions:**

1. **Verify file location:**
```bash
ls ~/.claude/plugins/larouex-fullstack-plugin
```

2. **Check file permissions:**
```bash
chmod -R 755 ~/.claude/plugins/larouex-fullstack-plugin
```

3. **Restart Claude Code:**
```bash
exit
claude
```

4. **Reinstall:**
```bash
rm -rf ~/.claude/plugins/larouex-fullstack-plugin
# Then reinstall using Method 1 or 2 from Installation guide
```

### Commands Not Working

**Symptoms:**
- Commands appear but fail to execute
- Error messages when running commands

**Solutions:**

1. **Update Claude Code:**
```bash
claude --version
# Ensure version is 2.0.13+
```

2. **Check command files exist:**
```bash
ls ~/.claude/plugins/larouex-fullstack-plugin/.claude/commands/
```

3. **Verify Node.js version:**
```bash
node --version
# Should be v20.0.0 or higher
```

## Azure Issues

### Azure CLI Not Working

**Symptoms:**
- `az: command not found`
- Authentication errors

**Solutions:**

1. **Install Azure CLI:**
```bash
npm install -g azure-cli
```

2. **Login to Azure:**
```bash
az login
```

3. **Set subscription:**
```bash
az account list
az account set --subscription "YOUR_SUBSCRIPTION_ID"
```

4. **Verify credentials:**
```bash
az account show
```

### Azure Deployment Fails

**Common errors and solutions:**

**Error: "Deployment failed with status 400"**
- Check `staticwebapp.config.json` is valid JSON
- Verify routes are correctly configured
- Check environment variables in Azure Portal

**Error: "Function app not found"**
- Verify resource group exists
- Check function app name is correct
- Ensure region is supported

**Error: "CORS errors"**
- Configure CORS in `function.json`
- Add allowed origins in Azure Portal
- Check `staticwebapp.config.json` settings

### Cold Starts (Azure Functions)

**Problem:** First request takes 10+ seconds

**Solutions:**

1. **Enable Always On (Premium plan):**
- In Azure Portal → Function App → Configuration
- Set "Always On" to true

2. **Use Premium plan:**
- Eliminates cold starts
- Costs more but better performance

3. **Optimize function:**
- Minimize dependencies
- Use connection pooling
- Implement warming triggers

## Railway Issues

### Railway CLI Not Working

**Symptoms:**
- `railway: command not found`
- Authentication errors

**Solutions:**

1. **Install Railway CLI:**
```bash
npm install -g @railway/cli
```

2. **Login to Railway:**
```bash
railway login
```

3. **Link project:**
```bash
railway link
```

4. **Verify login:**
```bash
railway whoami
```

### Railway Deployment Fails

**Common errors:**

**Error: "Build failed"**
- Check `railway.toml` configuration
- Verify build command is correct
- Review build logs: `railway logs --build`

**Error: "Database connection timeout"**
- Verify `DATABASE_URL` environment variable
- Check connection string format
- Ensure services are in same project

**Error: "Port binding failed"**
- Use `process.env.PORT` or `0.0.0.0`
- Don't hardcode port numbers

### Environment Variable Issues

**Problem:** Variables not found in Railway

**Solutions:**

1. **Check current environment:**
```bash
railway environment
```

2. **List variables:**
```bash
railway variables
```

3. **Add missing variables:**
```bash
railway variables set KEY=value
```

4. **Switch environment:**
```bash
railway environment staging
```

## TypeScript Issues

### TypeScript Errors After Scaffolding

**Symptoms:**
- Red squiggly lines everywhere
- "Cannot find module" errors

**Solutions:**

1. **Install dependencies:**
```bash
npm install
```

2. **Regenerate types:**
```bash
npm run build
```

3. **Restart TypeScript server (VS Code):**
- Cmd+Shift+P (Mac) or Ctrl+Shift+P (Windows)
- Type "TypeScript: Restart TS Server"
- Press Enter

4. **Clear cache:**
```bash
rm -rf node_modules .next
npm install
```

### Import Errors

**Problem:** Can't import modules

**Solutions:**

1. **Check tsconfig.json paths:**
```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

2. **Verify file exists:**
```bash
ls src/components/ComponentName.tsx
```

3. **Check import statement:**
```typescript
// Correct
import { Component } from '@/components/Component';

// Incorrect
import { Component } from 'src/components/Component';
```

## Bootstrap Issues

### Styles Not Loading

**Symptoms:**
- Components look unstyled
- Bootstrap classes don't work

**Solutions:**

1. **Verify Bootstrap is installed:**
```bash
npm list bootstrap
```

2. **Check import in layout:**
```typescript
// app/layout.tsx
import 'bootstrap/dist/css/bootstrap.min.css';
```

3. **Clear Next.js cache:**
```bash
rm -rf .next
npm run dev
```

4. **Check for CSS conflicts:**
- Review custom CSS files
- Check CSS module naming
- Look for !important overrides

### Responsive Grid Not Working

**Problem:** Grid doesn't respond to breakpoints

**Solutions:**

1. **Use correct Bootstrap classes:**
```jsx
<Col xs={12} sm={6} md={4} lg={3}>
```

2. **Import Container/Row/Col:**
```typescript
import { Container, Row, Col } from 'react-bootstrap';
```

3. **Check viewport meta tag:**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

## Next.js Issues

### Page Not Found (404)

**Problem:** New page returns 404

**Solutions:**

1. **Verify file location:**
```bash
# Should be in app/ directory
ls app/your-page/page.tsx
```

2. **Check file naming:**
- Must be named `page.tsx` (not `Page.tsx` or `your-page.tsx`)
- Dynamic routes: `[id]/page.tsx`

3. **Restart dev server:**
```bash
# Stop with Ctrl+C
npm run dev
```

### Hydration Errors

**Problem:** "Hydration failed" errors in console

**Solutions:**

1. **Use dynamic imports for client-only components:**
```typescript
import dynamic from 'next/dynamic';

const ClientComponent = dynamic(
  () => import('./ClientComponent'),
  { ssr: false }
);
```

2. **Check for mismatched HTML:**
- Don't use `<div>` inside `<p>`
- Ensure consistent server/client render

3. **Use useEffect for browser-only code:**
```typescript
useEffect(() => {
  // Browser-only code here
}, []);
```

## Testing Issues

### Tests Failing

**Common causes:**

**Error: "Cannot find module"**
```bash
npm install @testing-library/react @testing-library/jest-dom
```

**Error: "Unexpected token"**
```bash
# Add to jest.config.js
transform: {
  '^.+\\.(ts|tsx)$': 'ts-jest',
}
```

**Error: "window is not defined"**
```javascript
// Mock browser APIs
global.window = {};
```

### E2E Tests Timeout

**Solutions:**

1. **Increase timeout:**
```javascript
test.setTimeout(60000); // 60 seconds
```

2. **Wait for elements:**
```javascript
await page.waitForSelector('#element');
```

3. **Check server is running:**
```bash
npm run dev
# In another terminal:
npm run test:e2e
```

## Performance Issues

### Slow Build Times

**Solutions:**

1. **Enable SWC (Next.js built-in):**
```javascript
// next.config.js
module.exports = {
  swcMinify: true,
}
```

2. **Check bundle size:**
```bash
npm run build
npm run analyze
```

3. **Use dynamic imports:**
```typescript
const HeavyComponent = dynamic(() => import('./Heavy'));
```

### Slow Page Loads

**Solutions:**

1. **Optimize images:**
```typescript
import Image from 'next/image';

<Image
  src="/image.jpg"
  width={500}
  height={300}
  alt="Description"
/>
```

2. **Enable caching:**
```typescript
export const revalidate = 3600; // 1 hour
```

3. **Use Server Components:**
```typescript
// Default in app/ directory, no 'use client' needed
```

## Database Issues

### Azure Table Storage Errors

**Error: "TableNotFound"**
- Verify table name is correct
- Check connection string
- Ensure table exists in Azure Portal

**Error: "Authentication failed"**
- Check connection string in `.env`
- Verify account key is correct
- Use Managed Identity in production

### PostgreSQL Connection Errors (Railway)

**Error: "Connection timeout"**
- Check `DATABASE_URL` format
- Verify database is running in Railway dashboard
- Check connection limits

**Error: "SSL required"**
```javascript
// prisma/schema.prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
  sslmode  = "require"
}
```

## Command-Specific Issues

### /scaffold-* Commands Fail

**Solutions:**

1. **Check directory is empty:**
```bash
ls
# Should be empty or only contain .git
```

2. **Verify Node.js version:**
```bash
node --version  # Should be 20+
```

3. **Check disk space:**
```bash
df -h
```

### /deploy-* Commands Fail

**Solutions:**

1. **Run review first:**
```bash
/review-before-deploy
```

2. **Check environment variables:**
- Azure: In Azure Portal
- Railway: `railway variables`

3. **Verify credentials:**
- Azure: `az account show`
- Railway: `railway whoami`

4. **Check build passes locally:**
```bash
npm run build
```

## Getting More Help

### Documentation
- [Home](Home) - Wiki home
- [Installation](Installation) - Setup guide
- [Quick Start](Quick-Start) - Tutorials
- [FAQ](FAQ) - Common questions

### Community
- [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues) - Report bugs
- [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions) - Ask questions

### Platform Documentation
- [Next.js Docs](https://nextjs.org/docs)
- [Azure Docs](https://docs.microsoft.com/azure)
- [Railway Docs](https://docs.railway.app)
- [Bootstrap Docs](https://getbootstrap.com/docs)

## Still Having Issues?

If your issue isn't covered here:

1. **Search existing issues:** [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
2. **Ask in discussions:** [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)
3. **Create new issue:** Provide:
   - Description of problem
   - Steps to reproduce
   - Error messages
   - Environment details (OS, Node version, Claude Code version)
   - Platform (Azure/Railway)

We're here to help!
