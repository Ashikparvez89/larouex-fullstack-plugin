# Quick Start Guide

Get up and running with the Full-Stack Website Builder plugin in just 5 minutes!

## Your First Command

After [installing the plugin](Installation), let's verify everything works:

```bash
# Start Claude Code
claude

# Type a slash to see available commands
/
```

You should see a list of commands. Try a simple one:

```
/add-component
```

Claude will ask you about the component you want to create. This confirms the plugin is working!

---

## 5-Minute Azure Project

Build a complete Azure-hosted website in 5 minutes.

### Prerequisites
- Plugin installed ([Installation Guide](Installation))
- Azure account ([free signup](https://azure.microsoft.com/free/))
- Azure CLI logged in: `az login`

### Step 1: Scaffold the Project (1 minute)

```bash
# Start Claude Code in your projects directory
cd ~/projects
claude

# Create a new Azure full-stack project
/scaffold-azure-full
```

**Claude will ask for:**
- Project name (e.g., "my-azure-website")
- Azure subscription
- Resource group
- Region (e.g., "eastus")

**This creates:**
- Next.js 15 project with App Router
- Azure Functions API folder
- GitHub Actions workflow for CI/CD
- TypeScript and Bootstrap setup
- Environment configuration
- Complete README with deployment instructions

### Step 2: Add a Homepage (1 minute)

```bash
/add-page
```

**Provide details:**
- Page name: `home`
- Route path: `/`
- Layout type: `default` (with hero section)

**This creates:**
- Homepage at `app/page.tsx`
- Hero section component
- Responsive layout with Bootstrap
- SEO-optimized metadata

### Step 3: Add a Contact Form (1 minute)

```bash
/add-form
```

**Provide details:**
- Form name: `contact`
- Fields: `name, email, message`
- API endpoint: `/api/contact`

**This creates:**
- Contact form component with validation
- Azure Function API endpoint at `/api/contact`
- Form submission handling
- Success/error states
- Email notification setup

### Step 4: Deploy to Staging (1 minute)

```bash
/deploy-azure-staging
```

**This automatically:**
- Builds the Next.js application
- Deploys to Azure Static Web Apps (staging)
- Runs tests
- Provides staging URL

**Wait for deployment** (usually 2-3 minutes)

### Step 5: Deploy to Production (1 minute)

First, run the pre-deployment review:

```bash
/review-before-deploy
```

If all checks pass, deploy:

```bash
/deploy-azure-production
```

**Your site is now live!**

The deployment provides your production URL. Visit it to see your website.

---

## 5-Minute Railway Project

Build a complete full-stack application with Railway in 5 minutes.

### Prerequisites
- Plugin installed ([Installation Guide](Installation))
- Railway account ([free signup](https://railway.app/))
- Railway CLI logged in: `railway login`

### Step 1: Scaffold the Project (1 minute)

```bash
# Start Claude Code in your projects directory
cd ~/projects
claude

# Create a new Railway full-stack project
/scaffold-railway-full
```

**Claude will ask for:**
- Project name (e.g., "my-railway-app")
- Database type: `PostgreSQL`
- Include Redis: `yes/no`

**This creates:**
- Next.js 15 project with App Router
- Express.js API server
- Prisma ORM setup for PostgreSQL
- TypeScript configuration
- Railway deployment configuration
- Environment templates

### Step 2: Add Authentication (1 minute)

```bash
/add-auth
```

**Provide details:**
- Auth providers: `Email, Google, GitHub`
- Session strategy: `database`
- Protected routes: `yes`

**This creates:**
- NextAuth.js configuration
- Login/signup pages
- Protected route middleware
- Database session storage
- OAuth provider setup

### Step 3: Add Admin Panel (1 minute)

```bash
/add-admin-panel
```

**This creates:**
- Admin dashboard layout
- User management interface
- Authentication guards
- Responsive admin UI with Bootstrap
- API endpoints for admin operations

### Step 4: Deploy to Staging (1 minute)

```bash
/deploy-railway-staging
```

**This automatically:**
- Builds the application
- Deploys to Railway staging environment
- Runs database migrations
- Provides staging URL

### Step 5: Deploy to Production (1 minute)

First, run the pre-deployment review:

```bash
/review-before-deploy
```

If all checks pass, deploy:

```bash
/deploy-railway-production
```

**Your app is now live!**

---

## Common Workflows

### Workflow 1: Landing Page with Contact Form

**Goal:** Create a simple landing page with contact form (15 minutes)

```bash
# 1. Scaffold project
/scaffold-azure-full
# or
/scaffold-railway-full

# 2. Create homepage
/add-page
# Name: home, Route: /, Layout: hero

# 3. Add sections
/add-section
# Type: features, Position: below hero

/add-section
# Type: testimonials

# 4. Add navigation
/add-navigation
# Style: transparent header with logo

# 5. Add contact form
/add-form
# Name: contact, Fields: name, email, message

# 6. Setup email notifications
/add-email-azure
# or
/add-email-railway

# 7. Add SEO optimization
/add-seo
# Configure metadata, sitemap, robots.txt

# 8. Deploy
/deploy-azure-staging
# Test in staging
/deploy-azure-production
```

---

### Workflow 2: E-commerce Product Catalog

**Goal:** Build product catalog with checkout (30 minutes)

```bash
# 1. Scaffold project with database
/scaffold-azure-full
# or
/scaffold-railway-full

# 2. Add database
/add-database-azure
# or
/add-database-railway
# Schema: Products (id, name, price, image, description)

# 3. Create product listing page
/add-page
# Name: products, Route: /products, Layout: grid

# 4. Create product detail page
/add-page
# Name: product-detail, Route: /products/[id], Layout: detail

# 5. Add shopping cart
/add-component
# Name: ShoppingCart, Type: client component

# 6. Add checkout flow
/add-checkout
# Multi-step: cart → shipping → payment

# 7. Add payment processing
/add-stripe
# Setup Stripe integration

# 8. Add order management API
/add-api-azure
# or
/add-api-railway
# Endpoints: create order, get orders, update order status

# 9. Add admin panel
/add-admin-panel
# Manage products and orders

# 10. Add email notifications
/add-email-azure
# or
/add-email-railway
# Order confirmation, shipping updates

# 11. Test and deploy
/add-e2e-test
/deploy-railway-staging
/review-before-deploy
/deploy-railway-production
```

---

### Workflow 3: SaaS Application with Authentication

**Goal:** Build SaaS app with user dashboard (45 minutes)

```bash
# 1. Scaffold Railway project
/scaffold-railway-full
# Includes PostgreSQL

# 2. Add authentication
/add-auth
# Providers: Email, Google, GitHub

# 3. Add protected routes
/add-protected-route
# Protect /dashboard, /settings, /admin

# 4. Create user dashboard
/add-dashboard
# User stats, recent activity

# 5. Add user settings page
/add-page
# Name: settings, Route: /settings, Protected: true

# 6. Add subscription management
/add-subscription
# Stripe subscription integration

# 7. Create admin panel
/add-admin-panel
# User management, analytics

# 8. Add API endpoints
/add-api-railway
# Create multiple endpoints for app features

# 9. Setup monitoring
/setup-monitoring-railway
# Error tracking, performance monitoring

# 10. Add analytics
/add-analytics-plausible
# Privacy-friendly analytics

# 11. Test thoroughly
/add-unit-test
/add-e2e-test

# 12. Security audit
/audit-security
/audit-accessibility

# 13. Deploy
/deploy-railway-staging
/review-before-deploy
/deploy-railway-production
```

---

## Next Steps

### Learn the Agents

Understand the 12 specialized agents:
- [Agents Overview](Agents-Overview)
- [Frontend Development Agent](Frontend-Development-Agent)
- [Code Review Agent](Code-Review-Agent)

### Explore All Commands

Browse the complete command library:
- [Commands Overview](Commands-Overview)
- [Scaffolding Commands](Scaffolding-Commands)
- [Development Commands](Development-Commands)

### Platform-Specific Guides

Deep dive into your chosen platform:
- [Azure Platform Guide](Azure-Platform-Guide)
- [Railway Platform Guide](Railway-Platform-Guide)

### Real-World Examples

Check out detailed tutorials:
- [Examples](Examples) - Real-world projects and patterns

### Join the Community

- [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)
- [Report Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)

---

## Quick Reference

### Most Used Commands

```bash
# Project Setup
/scaffold-azure-full          # Complete Azure stack
/scaffold-railway-full        # Complete Railway stack
/scaffold-nextjs              # Standalone Next.js

# Pages & Components
/add-page                     # New page with routing
/add-component                # React component
/add-section                  # Page section (hero, features)
/add-navigation              # Navigation system

# Forms & Data
/add-form                     # Form with validation
/add-multistep-form          # Multi-step wizard
/add-table                    # Data table

# APIs & Backend
/add-api-azure               # Azure Function endpoint
/add-api-railway             # Express.js endpoint
/add-database-azure          # Azure Table Storage
/add-database-railway        # PostgreSQL + Prisma

# Authentication & Features
/add-auth                     # Authentication system
/add-protected-route         # Protected pages
/add-admin-panel             # Admin dashboard
/add-checkout                # E-commerce checkout

# Testing & Quality
/add-tests                    # Unit tests
/add-e2e-test                # End-to-end tests
/audit-security              # Security audit
/audit-accessibility         # Accessibility audit

# Code Review
/review-code                  # Review uncommitted changes
/review-before-deploy        # Pre-deployment gate

# Deployment
/deploy-azure-staging        # Deploy to Azure staging
/deploy-azure-production     # Deploy to Azure production
/deploy-railway-staging      # Deploy to Railway staging
/deploy-railway-production   # Deploy to Railway production
```

### Platform Comparison

| Feature | Azure | Railway |
|---------|-------|---------|
| **Deployment Speed** | 3-5 min | 2-3 min |
| **Setup Complexity** | Medium | Low |
| **Database** | Table Storage | PostgreSQL |
| **Functions** | Serverless | Express.js |
| **Best For** | Enterprise | Startups |
| **Pricing** | Pay-per-use | Fixed tier |

### Common Patterns

**Pattern 1: Simple Website**
```
scaffold → add pages → add navigation → add contact form → deploy
```

**Pattern 2: Web Application**
```
scaffold → add auth → add database → add APIs → add admin panel → deploy
```

**Pattern 3: E-commerce**
```
scaffold → add products → add cart → add checkout → add payment → deploy
```

---

## Getting Help

- **Documentation**: [Home](Home) - Full wiki
- **Troubleshooting**: [Troubleshooting](Troubleshooting) - Common issues
- **FAQ**: [FAQ](FAQ) - Frequently asked questions
- **Issues**: [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)

---

**Ready to dive deeper?** Check out the [Agents Overview](Agents-Overview) to understand the specialized AI agents that power these commands.
