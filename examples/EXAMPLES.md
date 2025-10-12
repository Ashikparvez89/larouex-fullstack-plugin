# Plugin Usage Examples

Complete workflows and real-world examples showing how to use the plugin commands to build production-ready applications.

## Table of Contents

1. [Complete Workflows](#complete-workflows)
2. [Common Command Combinations](#common-command-combinations)
3. [Platform-Specific Examples](#platform-specific-examples)
4. [Tips and Best Practices](#tips-and-best-practices)

---

## Complete Workflows

### Example 1: Building an Azure Static Web App

**Goal:** Create a marketing website with a blog and contact form

**Timeline:** 2-3 hours

**Steps:**

1. **Initialize project:**
   ```bash
   /scaffold-azure-nextjs
   ```
   Creates base Next.js project configured for Azure Static Web Apps.

2. **Create core pages:**
   ```bash
   /add-page about
   /add-page blog
   /add-page contact
   ```
   Generates page components with routing.

3. **Build reusable components:**
   ```bash
   /add-component Hero --type functional --props title,subtitle,ctaText
   /add-component BlogCard --type functional --props title,excerpt,date,image
   /add-component ContactForm --type functional
   ```
   Creates UI components with TypeScript props.

4. **Add navigation:**
   ```bash
   /add-navigation
   ```
   Generates responsive navbar with mobile menu.

5. **Set up blog content:**
   ```bash
   /add-content-json blog-posts
   ```
   Creates JSON file structure for blog posts with TypeScript types.

6. **Optimize for SEO:**
   ```bash
   /add-seo
   ```
   Adds metadata, Open Graph tags, sitemap generation.

7. **Add testing:**
   ```bash
   /add-tests
   ```
   Sets up Jest and React Testing Library with sample tests.

8. **Set up monitoring:**
   ```bash
   /setup-monitoring-azure
   ```
   Integrates Application Insights for analytics and error tracking.

9. **Deploy to staging:**
   ```bash
   /deploy-azure-staging
   ```
   Creates staging environment for testing.

10. **Deploy to production:**
    ```bash
    /deploy-azure-production
    ```
    Deploys to production with custom domain support.

**Technologies Used:**
- Next.js 15 with App Router
- Azure Static Web Apps
- TypeScript
- Tailwind CSS or Bootstrap 5
- Application Insights
- GitHub Actions

**Result:** A fully functional, SEO-optimized marketing website with blog, deployed to Azure with CI/CD pipeline.

---

### Example 2: Building a Railway E-commerce App

**Goal:** Create an online store with product catalog, shopping cart, and payment processing

**Timeline:** 1-2 weeks

**Steps:**

1. **Initialize full-stack project:**
   ```bash
   /scaffold-railway-full
   ```
   Creates Next.js frontend with Express.js backend and PostgreSQL database.

2. **Set up database schema:**
   ```bash
   /add-database-railway
   ```
   Configures PostgreSQL with Prisma ORM. Add models:
   - User
   - Product
   - Order
   - OrderItem
   - Cart

3. **Add authentication:**
   ```bash
   /add-auth
   ```
   Implements JWT-based authentication with login/register/logout.

4. **Create product pages:**
   ```bash
   /add-page products
   /add-page products/[id]
   ```
   Product listing page and dynamic product detail pages.

5. **Build product components:**
   ```bash
   /add-component ProductCard --type functional
   /add-component ProductGrid --type functional
   /add-component ProductDetails --type functional
   ```
   Reusable product display components.

6. **Create API endpoints:**
   ```bash
   /add-api-railway products --method GET
   /add-api-railway products/:id --method GET
   /add-api-railway products --method POST
   /add-api-railway products/:id --method PUT
   /add-api-railway products/:id --method DELETE
   ```
   RESTful API for product management.

7. **Implement shopping cart:**
   ```bash
   /add-checkout
   ```
   Adds cart state management, cart UI, and checkout flow.

8. **Integrate payments:**
   ```bash
   /add-stripe
   ```
   Sets up Stripe payment processing with webhooks.

9. **Create admin panel:**
   ```bash
   /add-admin-panel
   ```
   Dashboard for managing products, orders, and users.

10. **Add image upload:**
    ```bash
    /add-file-upload
    ```
    Allows product image uploads with optimization.

11. **Add email notifications:**
    ```bash
    /add-email
    ```
    Sends order confirmations and shipping updates.

12. **Add testing:**
    ```bash
    /add-tests
    ```
    Unit tests, integration tests, and E2E tests.

13. **Deploy to staging:**
    ```bash
    /deploy-railway-staging
    ```
    Test all features in staging environment.

14. **Deploy to production:**
    ```bash
    /deploy-railway-production
    ```
    Go live with production database and environment.

**Technologies Used:**
- Next.js 15
- Railway platform
- PostgreSQL + Prisma
- Express.js API
- Stripe payments
- JWT authentication
- SendGrid for emails

**Result:** A full-featured e-commerce platform with secure payments, user accounts, and admin management.

---

### Example 3: Adding Real-time Chat Features

**Goal:** Add live chat functionality to an existing application

**Timeline:** 4-6 hours

#### Azure Version

**Steps:**

1. **Set up Azure SignalR:**
   ```bash
   /add-websockets-azure
   ```
   Configures Azure SignalR Service for real-time communication.

2. **Create chat UI component:**
   ```bash
   /add-component ChatWindow --type functional
   /add-component ChatMessage --type functional
   /add-component ChatInput --type functional
   ```
   Build chat interface components.

3. **Create chat API handlers:**
   ```bash
   /add-api-azure sendMessage --method POST
   /add-api-azure getMessages --method GET
   /add-api-azure joinRoom --method POST
   ```
   API endpoints for message handling.

4. **Add database storage:**
   ```bash
   /add-database-azure --type cosmosdb
   ```
   Store chat messages in Cosmos DB.

5. **Add tests:**
   ```bash
   /add-tests
   ```
   Test WebSocket connections and message delivery.

6. **Deploy to staging:**
   ```bash
   /deploy-azure-staging
   ```
   Test real-time features in staging.

**Technologies:**
- Azure SignalR Service
- Azure Cosmos DB
- Azure Functions
- WebSocket protocol

#### Railway Version

**Steps:**

1. **Set up Socket.io:**
   ```bash
   /add-websockets-railway
   ```
   Configures Socket.io server for real-time communication.

2. **Create chat UI component:**
   ```bash
   /add-component ChatWindow --type functional
   /add-component ChatMessage --type functional
   /add-component ChatInput --type functional
   ```
   Build chat interface components.

3. **Create Socket.io server:**
   ```bash
   /add-api-railway chat --method SOCKET
   ```
   Set up Socket.io event handlers in Express server.

4. **Add database storage:**
   ```bash
   /add-database-railway
   ```
   Add Message model to Prisma schema for message persistence.

5. **Add tests:**
   ```bash
   /add-tests
   ```
   Test WebSocket connections and message delivery.

6. **Deploy to staging:**
   ```bash
   /deploy-railway-staging
   ```
   Test real-time features in staging.

**Technologies:**
- Socket.io
- PostgreSQL + Prisma
- Express.js
- WebSocket protocol

**Result:** Real-time chat with message persistence, typing indicators, and online presence.

---

### Example 4: Performance Optimization

**Goal:** Improve Core Web Vitals scores from 60s to 90+

**Timeline:** 1-2 days

**Steps:**

1. **Run Lighthouse audit:**
   ```bash
   /optimize-lighthouse
   ```
   Analyzes current performance and provides recommendations.

2. **Optimize images:**
   ```bash
   /optimize-images
   ```
   Converts images to WebP, generates responsive sizes, adds lazy loading.

3. **Reduce bundle size:**
   ```bash
   /optimize-bundle
   ```
   Analyzes bundle, implements code splitting, removes unused dependencies.

4. **Implement caching:**
   ```bash
   /add-caching
   ```
   Adds service worker, implements cache strategies, sets up CDN caching.

5. **Optimize fonts:**
   ```bash
   /optimize-fonts
   ```
   Implements font subsetting, preloading, and display swap.

6. **Add performance monitoring:**
   ```bash
   /add-performance-monitoring
   ```
   Tracks Core Web Vitals in production.

7. **Add performance tests:**
   ```bash
   /add-tests --type performance
   ```
   Automated performance regression tests.

8. **Deploy and verify:**
   ```bash
   /deploy-azure-staging
   # or
   /deploy-railway-staging
   ```
   Test improvements in staging environment.

**Optimizations Applied:**
- Image optimization (WebP conversion, lazy loading)
- Code splitting and tree shaking
- Font optimization
- Service worker caching
- CDN configuration
- Critical CSS inlining
- Preloading key resources

**Result:** Lighthouse scores improved from 60s to 90+ across all metrics (Performance, Accessibility, Best Practices, SEO).

---

### Example 5: Adding Multi-language Support

**Goal:** Support English, Spanish, and French for international audience

**Timeline:** 1-2 days

**Steps:**

1. **Set up internationalization:**
   ```bash
   /add-i18n
   ```
   Installs and configures next-intl with routing for locales.

2. **Create translation files:**
   Create JSON files for each language:
   - `/locales/en/common.json`
   - `/locales/es/common.json`
   - `/locales/fr/common.json`

   Example structure:
   ```json
   {
     "nav": {
       "home": "Home",
       "about": "About",
       "contact": "Contact"
     },
     "hero": {
       "title": "Welcome to our site",
       "subtitle": "Building amazing things"
     }
   }
   ```

3. **Add locale formatting:**
   ```bash
   /add-localization
   ```
   Adds date, number, and currency formatting for each locale.

4. **Create language switcher:**
   ```bash
   /add-component LanguageSwitcher --type functional
   ```
   Dropdown or toggle for switching languages.

5. **Update all pages:**
   Replace hardcoded strings with translation keys:
   ```typescript
   import { useTranslations } from 'next-intl'

   export default function Home() {
     const t = useTranslations('hero')
     return <h1>{t('title')}</h1>
   }
   ```

6. **Add locale-specific pages:**
   ```bash
   /add-page about --locale es
   /add-page about --locale fr
   ```

7. **Test translations:**
   ```bash
   /add-tests --type i18n
   ```
   Verify all translations load correctly.

8. **Add SEO for locales:**
   Update sitemap and hreflang tags for each language.

9. **Deploy:**
   ```bash
   /deploy-azure-production
   # or
   /deploy-railway-production
   ```

**Technologies:**
- next-intl for translations
- Locale-based routing
- Translation management system (optional)

**Result:** Fully internationalized application with automatic locale detection and seamless language switching.

---

### Example 6: Platform Migration

**Goal:** Migrate existing Azure Static Web App to Railway

**Timeline:** 4-8 hours

**Steps:**

1. **Run automated migration:**
   ```bash
   /migrate-azure-to-railway
   ```
   Analyzes Azure configuration and generates Railway equivalents.

2. **Review generated files:**
   - Check `railway.toml` configuration
   - Review `Dockerfile` if generated
   - Verify environment variable mappings
   - Check API route conversions

3. **Update database connections:**
   - Migrate from Cosmos DB to PostgreSQL (if applicable)
   - Update connection strings
   - Convert database queries to Prisma

4. **Set up Railway project:**
   ```bash
   railway init
   railway add postgresql
   ```

5. **Configure environment variables:**
   ```bash
   railway variables set NODE_ENV=production
   railway variables set DATABASE_URL=${{ POSTGRESQL_URL }}
   # Add all other environment variables
   ```

6. **Test locally with Railway:**
   ```bash
   railway run npm run dev
   ```

7. **Run database migrations:**
   ```bash
   railway run npx prisma migrate deploy
   ```

8. **Deploy to Railway staging:**
   ```bash
   /deploy-railway-staging
   ```

9. **Validate all features:**
   - Test all pages and routes
   - Verify API endpoints
   - Check database operations
   - Test authentication
   - Validate file uploads
   - Review monitoring/logging

10. **Update DNS and go live:**
    ```bash
    /deploy-railway-production
    ```
    Update DNS records to point to Railway.

**Migration Considerations:**
- Azure Functions → Express.js API routes
- Cosmos DB → PostgreSQL + Prisma
- Azure Blob Storage → Railway volumes or S3
- Application Insights → Railway metrics + custom logging
- Azure AD auth → JWT or OAuth

**Result:** Successfully migrated application running on Railway with improved developer experience and potentially lower costs.

---

## Common Command Combinations

### Quick Website Setup

Build a simple informational website in under 30 minutes:

```bash
# 1. Initialize project
/scaffold-nextjs

# 2. Add navigation
/add-navigation

# 3. Create pages
/add-page home
/add-page about
/add-page services
/add-page contact

# 4. Add contact form
/add-form contact --fields name,email,message

# 5. Optimize for search engines
/add-seo

# 6. Deploy
/deploy-azure-production
```

### API Development

Create a RESTful API backend:

```bash
# 1. Choose platform and initialize
/scaffold-azure-functions
# or
/scaffold-railway-full

# 2. Add API endpoints
/add-api-azure users --method GET
/add-api-azure users --method POST
/add-api-azure users/:id --method PUT
/add-api-azure users/:id --method DELETE

# 3. Add database
/add-database-azure --type cosmosdb
# or
/add-database-railway

# 4. Add tests
/add-tests

# 5. Deploy to staging
/deploy-azure-staging
# or
/deploy-railway-staging
```

### User Authentication Flow

Add complete authentication system:

```bash
# 1. Add authentication
/add-auth

# 2. Create protected routes
/add-protected-route dashboard
/add-protected-route profile
/add-protected-route settings

# 3. Add user management (admin)
/add-user-management

# 4. Add password reset
/add-password-reset

# 5. Add email verification
/add-email-verification

# 6. Add tests
/add-tests --type auth

# 7. Security audit
/audit-security

# 8. Deploy
/deploy-azure-staging
```

### Analytics and Monitoring Setup

Comprehensive analytics implementation:

```bash
# 1. Add Google Analytics
/add-analytics-google

# 2. Add platform monitoring
/setup-monitoring-azure
# or
/setup-monitoring-railway

# 3. Add heatmaps
/add-heatmaps

# 4. Create metrics dashboard
/add-dashboard metrics

# 5. Set up error tracking
/add-error-tracking

# 6. Add custom events
/add-analytics-events

# 7. Deploy
/deploy-azure-production
```

### E-commerce Quick Start

Basic online store setup:

```bash
# 1. Full-stack initialization
/scaffold-railway-full

# 2. Database with products
/add-database-railway

# 3. Product pages
/add-page products
/add-page products/[id]

# 4. Shopping cart
/add-checkout

# 5. Payment processing
/add-stripe

# 6. Order management
/add-order-management

# 7. Deploy
/deploy-railway-staging
```

### Blog Setup

Create a blog with CMS:

```bash
# 1. Initialize
/scaffold-nextjs

# 2. Add blog structure
/add-blog

# 3. Create blog pages
/add-page blog
/add-page blog/[slug]

# 4. Add CMS
/add-cms --type contentful
# or
/add-content-json blog-posts

# 5. Add comments
/add-comments

# 6. Add search
/add-search

# 7. SEO optimization
/add-seo

# 8. Deploy
/deploy-azure-production
```

### Progressive Web App (PWA)

Convert website to PWA:

```bash
# 1. Add PWA support
/add-pwa

# 2. Configure service worker
/add-service-worker

# 3. Add offline support
/add-offline-mode

# 4. Add push notifications
/add-push-notifications

# 5. Add install prompt
/add-install-prompt

# 6. Test PWA
/test-pwa

# 7. Deploy
/deploy-azure-production
```

---

## Platform-Specific Examples

### Azure-Specific Features

#### Using Azure Functions

```bash
# Create serverless functions
/add-api-azure processPayment --method POST
/add-api-azure sendEmail --method POST
/add-api-azure generateReport --method GET

# Add triggers
/add-function-trigger timer --schedule "0 0 * * *"
/add-function-trigger queue --name "orders"

# Add bindings
/add-function-binding cosmosdb --type in
/add-function-binding blob --type out
```

#### Using Azure Services

```bash
# Add Cosmos DB
/add-database-azure --type cosmosdb

# Add Blob Storage
/add-storage-azure --type blob

# Add Service Bus
/add-servicebus-azure

# Add Key Vault
/add-keyvault-azure

# Add Application Insights
/setup-monitoring-azure
```

### Railway-Specific Features

#### Using Railway Services

```bash
# Add PostgreSQL
railway add postgresql

# Add Redis
railway add redis

# Add MongoDB
railway add mongodb

# View all services
railway services
```

#### Railway Environments

```bash
# Create staging environment
railway env create staging

# Set variables per environment
railway env set ENVIRONMENT=staging

# Deploy to specific environment
railway up --environment staging
```

#### Railway CLI Workflows

```bash
# Link to existing project
railway link

# Run command with Railway environment
railway run npm run dev

# View logs
railway logs --follow

# Open dashboard
railway open

# Connect to database
railway connect postgres
```

---

## Tips and Best Practices

### When to Use Azure vs Railway

#### Use Azure when:

- **Enterprise requirements:** Need compliance certifications (SOC 2, HIPAA, etc.)
- **Microsoft ecosystem:** Already using Microsoft services (Azure AD, Office 365)
- **Serverless-first:** Want auto-scaling serverless functions
- **Global scale:** Need Azure's extensive global CDN
- **Hybrid cloud:** Need integration with on-premises infrastructure

#### Use Railway when:

- **Rapid development:** Want fastest time to deployment
- **Full-stack with databases:** Need PostgreSQL, MongoDB, Redis out-of-the-box
- **Indie/startup projects:** Cost-effective for smaller scale
- **Developer experience:** Priority on simplicity and ease of use
- **Modern stack:** Building with Next.js, Prisma, Express, etc.

### Command Sequencing

Always follow this order for best results:

1. **Foundation:** Scaffold project, set up repository
2. **Structure:** Add pages, components, routing
3. **Features:** Add functionality (auth, APIs, database)
4. **Enhancements:** Add nice-to-haves (analytics, monitoring)
5. **Quality:** Add tests, accessibility, security audits
6. **Optimization:** Optimize performance, images, bundles
7. **Staging:** Deploy to staging environment
8. **Validation:** Test thoroughly in staging
9. **Production:** Deploy to production
10. **Monitoring:** Set up alerts and monitoring

### Testing Strategy

Always test before deploying to production:

```bash
# 1. Deploy to staging
/deploy-azure-staging
# or
/deploy-railway-staging

# 2. Run automated tests
npm run test
npm run test:e2e

# 3. Manual testing
# - Test all user flows
# - Test on multiple devices
# - Test with different browsers
# - Test error scenarios

# 4. Performance testing
/optimize-lighthouse

# 5. Security audit
/audit-security

# 6. If all tests pass, deploy to production
/deploy-azure-production
# or
/deploy-railway-production
```

### Environment Variables Management

Best practices for managing secrets:

**Azure:**
```bash
# Never commit .env files
echo ".env" >> .gitignore
echo ".env.local" >> .gitignore

# Set in Azure Portal
# Configuration > Application settings

# For local development
cp .env.example .env.local
# Edit .env.local with real values
```

**Railway:**
```bash
# Use Railway CLI
railway variables set API_KEY=abc123

# Or use Railway dashboard
# Project > Variables

# Pull variables locally
railway variables
```

### Database Best Practices

**Azure (Cosmos DB):**
```bash
# Use connection string from Azure Portal
COSMOS_DB_CONNECTION_STRING=AccountEndpoint=...

# Enable local emulator for development
# https://docs.microsoft.com/azure/cosmos-db/local-emulator
```

**Railway (PostgreSQL):**
```bash
# Use Railway-provided DATABASE_URL
# Automatically injected by Railway

# For local development with Prisma
npx prisma migrate dev
npx prisma studio

# Backup before migrations
railway run pg_dump $DATABASE_URL > backup.sql
```

### Deployment Strategies

#### Blue-Green Deployment

```bash
# Deploy to staging (green)
/deploy-azure-staging

# Test thoroughly
npm run test:e2e

# If successful, promote to production (blue)
/deploy-azure-production

# Keep staging as rollback option
```

#### Canary Deployment

```bash
# Deploy to small percentage of users
/deploy-azure-production --canary 10%

# Monitor metrics
/view-metrics

# If successful, increase rollout
/deploy-azure-production --canary 50%
/deploy-azure-production --canary 100%
```

### Monitoring and Alerts

Set up comprehensive monitoring:

```bash
# 1. Add monitoring
/setup-monitoring-azure
# or
/setup-monitoring-railway

# 2. Configure alerts
/add-alert --metric "error_rate" --threshold 5%
/add-alert --metric "response_time" --threshold 2s
/add-alert --metric "uptime" --threshold 99%

# 3. View dashboards
/view-dashboard
```

### Cost Optimization

**Azure:**
- Use free tier for development
- Enable auto-scaling only when needed
- Use Azure Cost Management for tracking
- Set spending limits and alerts

**Railway:**
- Use free tier for development ($5 credit)
- Monitor resource usage in dashboard
- Optimize Docker images to reduce build time
- Use connection pooling for databases

### Documentation

Always document your project:

```bash
# Generate project documentation
/generate-docs

# This creates:
# - README.md with setup instructions
# - CONTRIBUTING.md with development guidelines
# - API.md with API documentation
# - DEPLOYMENT.md with deployment instructions
```

### Continuous Integration

Set up CI/CD pipeline:

**Azure (GitHub Actions):**
```yaml
# .github/workflows/azure-static-web-apps.yml
# Automatically generated by /scaffold-azure-full
```

**Railway (GitHub Integration):**
```bash
# Connect in Railway dashboard
# Settings > GitHub > Connect Repository

# Auto-deploys on push to main
# Creates preview environments for PRs
```

### Error Handling

Implement robust error handling:

```bash
# Add error boundaries
/add-error-boundary

# Add error tracking
/add-error-tracking

# Add logging
/add-logging

# Add health checks
/add-health-check
```

### Accessibility

Ensure your app is accessible:

```bash
# Add accessibility features
/add-accessibility

# Run accessibility audit
/audit-accessibility

# Add ARIA labels
/add-aria-labels

# Test with screen readers
# Test keyboard navigation
```

### Performance Monitoring

Track performance over time:

```bash
# Add performance monitoring
/add-performance-monitoring

# Set performance budgets
/set-performance-budget --fcp 1.8s --lcp 2.5s

# Add CI performance checks
/add-performance-ci

# View performance dashboard
/view-performance-dashboard
```

---

## Example Project Timeline

### Week 1: MVP (Minimum Viable Product)

**Day 1-2: Setup and Foundation**
- Scaffold project
- Set up repository
- Create basic pages
- Add navigation

**Day 3-4: Core Features**
- Add database
- Create API endpoints
- Implement authentication
- Add forms

**Day 5: Polish and Deploy**
- Add basic styling
- Write tests
- Deploy to staging
- Fix bugs

### Week 2: Enhancement

**Day 1-2: User Experience**
- Improve UI/UX
- Add animations
- Optimize performance
- Improve accessibility

**Day 3-4: Additional Features**
- Add analytics
- Implement payments (if needed)
- Add email notifications
- Create admin panel

**Day 5: Production Ready**
- Security audit
- Final testing
- Deploy to production
- Set up monitoring

### Week 3+: Iteration

- Monitor user feedback
- Fix bugs
- Add requested features
- Optimize based on metrics

---

## Support and Resources

### Getting Help

1. **Plugin Documentation:** Check command-specific documentation
2. **Community:** Join Discord or Slack community
3. **GitHub Issues:** Report bugs or request features
4. **Stack Overflow:** Search for solutions

### Learning Resources

**Next.js:**
- [Next.js Documentation](https://nextjs.org/docs)
- [Next.js Learn](https://nextjs.org/learn)

**Azure:**
- [Azure Static Web Apps Docs](https://docs.microsoft.com/azure/static-web-apps/)
- [Azure Functions Docs](https://docs.microsoft.com/azure/azure-functions/)

**Railway:**
- [Railway Documentation](https://docs.railway.app/)
- [Railway Blog](https://blog.railway.app/)

**TypeScript:**
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)

**Prisma:**
- [Prisma Documentation](https://www.prisma.io/docs)

### Community Examples

Browse real-world projects built with this plugin:
- [GitHub Topic: larouex-plugin](https://github.com/topics/larouex-plugin)
- [Example Projects Repository](https://github.com/larouex/examples)

---

## Conclusion

These examples demonstrate the power and flexibility of the plugin commands. By combining commands strategically, you can build production-ready applications quickly and efficiently.

**Key Takeaways:**

1. **Start with scaffolding** commands to set up your foundation
2. **Build incrementally** add features one at a time
3. **Test thoroughly** always deploy to staging first
4. **Monitor and optimize** use analytics and monitoring from day one
5. **Follow best practices** security, accessibility, performance

Happy building!
