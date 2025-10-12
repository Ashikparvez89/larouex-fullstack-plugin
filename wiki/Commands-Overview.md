# Commands Overview

The Full-Stack Website Builder plugin provides **81 slash commands** organized into 10 major categories. Each command is designed to perform a specific task in your development workflow.

## Command Structure

All commands follow this pattern:
```
/{verb}-{feature}-{platform}
```

**Examples:**
- `/scaffold-azure-full` - Scaffold a full Azure project
- `/add-page` - Add a new page (platform-agnostic)
- `/deploy-railway-staging` - Deploy to Railway staging

## Quick Reference by Category

| Category | Commands | Description |
|----------|----------|-------------|
| [Scaffolding](Scaffolding-Commands) | 6 | Create new projects |
| [Azure](Azure-Commands) | 8 | Azure cloud operations |
| [Railway](Railway-Commands) | 7 | Railway platform operations |
| [Development](Development-Commands) | 20+ | Pages, components, forms |
| [Testing](Testing-Commands) | 8 | Testing and quality |
| [Review](Review-Commands) | 6 | Code review and gates |
| [Deployment](Deployment-Commands) | 4 | Deploy to staging/production |
| [Performance](Performance-Commands) | 6 | Optimization commands |
| [Integration](Integration-Commands) | 10+ | Email, analytics, social |
| [Advanced](Advanced-Commands) | 12+ | i18n, payments, admin |

## All 81 Commands

### Scaffolding Commands (6)
- `/scaffold-azure-nextjs` - Next.js project for Azure Static Web Apps
- `/scaffold-azure-functions` - Azure Functions API project
- `/scaffold-azure-full` - Complete Azure stack (Static Web Apps + Functions)
- `/scaffold-railway-nextjs` - Next.js project for Railway
- `/scaffold-railway-full` - Full-stack Railway project
- `/scaffold-nextjs` - Standalone Next.js 15 project

[View detailed documentation](Scaffolding-Commands)

### Azure Commands (8)
- `/add-api-azure` - Create Azure Function endpoint
- `/add-database-azure` - Configure Azure Table Storage
- `/deploy-azure-staging` - Deploy to Azure staging
- `/deploy-azure-production` - Deploy to Azure production
- `/setup-monitoring-azure` - Configure Application Insights
- `/add-email-azure` - Setup Azure Communication Services
- `/add-upload-azure` - Configure Azure Blob Storage
- `/add-cron-azure` - Create Azure Function timer trigger

[View detailed documentation](Azure-Commands)

### Railway Commands (7)
- `/add-api-railway` - Create Express.js endpoint
- `/add-database-railway` - Configure Railway PostgreSQL
- `/deploy-railway-staging` - Deploy to Railway staging
- `/deploy-railway-production` - Deploy to Railway production
- `/setup-monitoring-railway` - Setup Railway observability
- `/add-email-railway` - Configure email service
- `/add-cron-railway` - Create scheduled jobs

[View detailed documentation](Railway-Commands)

### Development Commands (20+)
**Pages & Components:**
- `/add-page` - Create new page with routing
- `/add-component` - Generate React component
- `/add-section` - Add page section (hero, features, etc.)
- `/add-navigation` - Create navigation system
- `/add-image-gallery` - Build image gallery

**Forms:**
- `/add-form` - Create form with validation
- `/add-multistep-form` - Build multi-step wizard
- `/add-table` - Generate data table

**Content:**
- `/add-content-json` - Setup JSON content management
- `/add-seo` - Add SEO optimization
- `/add-onboarding` - Create onboarding flow

[View detailed documentation](Development-Commands)

### Testing Commands (8)
- `/add-tests` - Generate unit tests
- `/add-e2e-test` - Create E2E tests with Playwright
- `/add-integration-test` - Integration tests
- `/audit-accessibility` - Run WCAG audit
- `/audit-security` - Security vulnerability scan
- `/add-error-tracking` - Setup error monitoring
- `/optimize-lighthouse` - Run Lighthouse audit
- `/add-error-boundary` - Add React error boundaries

[View detailed documentation](Testing-Commands)

### Code Review Commands (6)
- `/review-code` - Review uncommitted changes
- `/review-component` - Deep review of React component
- `/review-api` - Review API endpoint
- `/review-security` - Security-focused audit
- `/review-performance` - Performance analysis
- `/review-before-deploy` - Pre-deployment quality gate

[View detailed documentation](Review-Commands)

### Deployment Commands (4)
- `/deploy-azure-staging` - Deploy to Azure staging
- `/deploy-azure-production` - Deploy to Azure production
- `/deploy-railway-staging` - Deploy to Railway staging
- `/deploy-railway-production` - Deploy to Railway production

[View detailed documentation](Deployment-Commands)

### Performance Commands (6)
- `/optimize-images` - Optimize images with next/image
- `/optimize-bundle` - Analyze and reduce bundle size
- `/optimize-lighthouse` - Run Lighthouse audit
- `/add-caching` - Implement caching strategies
- `/optimize-performance` - General performance optimization
- `/optimize-seo` - SEO optimization

[View detailed documentation](Performance-Commands)

### Integration Commands (10+)
**Email & Notifications:**
- `/add-email-azure` - Azure Communication Services
- `/add-email-railway` - Railway email service
- `/add-notifications` - Push notifications

**Analytics:**
- `/add-analytics-google` - Google Analytics 4
- `/add-analytics-plausible` - Plausible Analytics
- `/add-heatmaps` - User interaction heatmaps

**File Upload:**
- `/add-upload-azure` - Azure Blob Storage
- `/add-upload-railway` - Railway file storage

**Search:**
- `/add-search-client` - Client-side search
- `/add-search-azure` - Azure Cognitive Search
- `/add-filters` - Advanced filtering

**Social:**
- `/add-social-share` - Social media sharing
- `/add-social-login` - OAuth social auth
- `/add-social-feed` - Social media feeds

[View detailed documentation](Integration-Commands)

### Advanced Commands (12+)
**Authentication:**
- `/add-auth` - NextAuth.js authentication
- `/add-protected-route` - Protected pages
- `/add-social-login` - Social OAuth providers
- `/add-user-management` - User admin panel

**Admin & CMS:**
- `/add-admin-panel` - Admin dashboard
- `/add-cms-ui` - Content management UI
- `/add-dashboard` - User dashboard

**Internationalization:**
- `/add-i18n` - Next.js i18n setup
- `/add-localization` - Language translations

**Real-time:**
- `/add-websockets-azure` - Azure Web PubSub
- `/add-websockets-railway` - Railway WebSockets
- `/add-live-updates` - Real-time data sync

**Payments:**
- `/add-stripe` - Stripe integration
- `/add-checkout` - E-commerce checkout

**Data Visualization:**
- `/add-charts` - Interactive charts
- `/add-table` - Data tables

**Background Jobs:**
- `/add-background-job` - Background processing
- `/add-cron-azure` - Azure timer triggers
- `/add-cron-railway` - Railway cron jobs

**Migration:**
- `/migrate-to-nextjs15` - Upgrade to Next.js 15
- `/migrate-azure-to-railway` - Migrate platforms
- `/migrate-railway-to-azure` - Migrate platforms
- `/upgrade-dependencies` - Update dependencies

**Documentation:**
- `/generate-readme` - Generate README
- `/generate-api-docs` - API documentation

[View detailed documentation](Advanced-Commands)

## Command Usage Patterns

### Pattern 1: New Project
```bash
/scaffold-azure-full  # or /scaffold-railway-full
/add-page
/add-navigation
/add-form
/deploy-azure-staging
```

### Pattern 2: Add Feature
```bash
/add-component
/add-tests
/review-code
# commit changes
```

### Pattern 3: Production Deployment
```bash
/review-before-deploy
/audit-security
/audit-accessibility
/deploy-azure-production
```

## Platform-Specific Commands

### Azure-Only Commands
Commands that work specifically with Azure services:
- All `/add-*-azure` commands
- `/deploy-azure-*` commands
- `/scaffold-azure-*` commands

### Railway-Only Commands
Commands that work specifically with Railway:
- All `/add-*-railway` commands
- `/deploy-railway-*` commands
- `/scaffold-railway-*` commands

### Platform-Agnostic Commands
Commands that work on any platform:
- `/add-page`
- `/add-component`
- `/add-form`
- `/add-auth`
- `/audit-*` commands
- `/review-*` commands

## Command Cheat Sheet

### Most Common Commands

```bash
# Project Setup
/scaffold-azure-full        # Azure project
/scaffold-railway-full      # Railway project

# Development
/add-page                   # New page
/add-component              # Component
/add-form                   # Form

# APIs
/add-api-azure             # Azure Function
/add-api-railway           # Express endpoint

# Testing
/add-tests                  # Unit tests
/add-e2e-test              # E2E tests

# Review
/review-code                # Review changes
/review-before-deploy      # Pre-deployment gate

# Deploy
/deploy-azure-staging      # Azure staging
/deploy-azure-production   # Azure production
/deploy-railway-staging    # Railway staging
/deploy-railway-production # Railway production
```

## Next Steps

- **Browse by category**: Click on category links above
- **Learn workflows**: See [Workflows](Workflows) for complete patterns
- **Platform guides**: [Azure](Azure-Platform-Guide) or [Railway](Railway-Platform-Guide)
- **Try examples**: [Examples](Examples) for real-world usage

## Getting Help

- **Command not working?** Check [Troubleshooting](Troubleshooting)
- **Need examples?** See [Examples](Examples)
- **Have questions?** Visit [FAQ](FAQ)
- **Report issues**: [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
