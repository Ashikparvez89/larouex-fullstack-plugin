[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-blue)](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin)
[![Version](https://img.shields.io/badge/version-1.0.0-green)](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/releases)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Next.js](https://img.shields.io/badge/Next.js-15-black)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue)](https://www.typescriptlang.org/)

# Full-Stack Website Builder - Claude Code Plugin

> A comprehensive Claude Code plugin with 81 commands and 12 specialized AI agents for building modern, full-stack web applications with Next.js 15, Azure, Railway, Bootstrap, and TypeScript.

---

## Overview

The **Full-Stack Website Builder** is a production-ready Claude Code plugin designed to accelerate the development of modern web applications. With an extensive collection of 81 slash commands and 12 specialized AI agents, this plugin provides end-to-end support for building, deploying, and maintaining sophisticated web applications.

### Key Features

- **81 Slash Commands** - Comprehensive command library covering scaffolding, development, deployment, testing, optimization, code review, and maintenance
- **12 Specialized AI Agents** - Expert agents for frontend, forms, content/SEO, Azure serverless, DevOps (Azure & Railway), monitoring, testing, security, accessibility, authentication, and code review
- **Multi-Platform Support** - Native support for Azure Static Web Apps, Azure Functions, and Railway deployments
- **Next.js 15 Optimized** - Built specifically for Next.js 15 with App Router, Server Components, and TypeScript
- **Bootstrap 5 Integration** - Responsive, mobile-first design with Bootstrap 5 components and utilities
- **TypeScript First** - Full TypeScript support with strict type checking and IntelliSense
- **Complete Lifecycle** - From scaffolding to production deployment and monitoring

### Technologies Supported

- **Frontend**: Next.js 15 (App Router), React 18, TypeScript 5, Bootstrap 5
- **Backend**: Azure Functions, Railway Services, REST APIs, GraphQL
- **Cloud Platforms**: Azure Static Web Apps, Azure Functions, Railway
- **Databases**: Azure Cosmos DB, PostgreSQL, MongoDB, Railway PostgreSQL
- **Authentication**: NextAuth.js, Azure AD, Social providers
- **Testing**: Jest, React Testing Library, Playwright, Cypress
- **Analytics**: Google Analytics, Plausible, Application Insights
- **Monitoring**: Azure Application Insights, Railway Observability

---

## Features

### Complete Development Lifecycle

- **Scaffolding** - Generate production-ready projects for Azure, Railway, or standalone Next.js apps
- **Development** - Commands for pages, components, forms, navigation, content, and features
- **Testing** - Unit tests, integration tests, E2E tests, and accessibility audits
- **Optimization** - Image optimization, bundle analysis, Lighthouse audits, caching strategies
- **Deployment** - Staging and production deployments for Azure and Railway
- **Monitoring** - Performance tracking, error logging, and observability

### Platform-Specific Commands

- **Azure Integration** - Static Web Apps, Functions, Cosmos DB, Blob Storage, Application Insights
- **Railway Integration** - Services, PostgreSQL, Redis, Environment variables, Deployments
- **Universal Commands** - Work across both platforms for maximum flexibility

### Specialized AI Agents

12 expert agents that provide context-aware assistance:

1. **Frontend Development Agent** - React, TypeScript, Bootstrap, responsive design
2. **Forms Workflow Agent** - Form creation, validation, multi-step forms
3. **Content & SEO Agent** - Content management, SEO optimization, metadata
4. **Azure Serverless Agent** - Functions, Static Web Apps, Cosmos DB
5. **DevOps Azure Agent** - CI/CD, GitHub Actions, Azure deployments
6. **DevOps Railway Agent** - Railway deployments, environment management
7. **Monitoring & Observability Agent** - Performance tracking, error monitoring
8. **Testing & Quality Agent** - Test strategy, coverage, quality assurance
9. **Security & Production Agent** - Security audits, production best practices
10. **Accessibility & Compliance Agent** - WCAG compliance, a11y auditing
11. **Authentication Agent** - Auth flows, session management, security
12. **Code Review Agent** - Automated code review, quality gates, best practices

---

## Prerequisites

Before using this plugin, ensure you have the following installed and configured:

### Required

- **Node.js 20+** - [Download Node.js](https://nodejs.org/)
- **Claude Code 2.0.13+** - [Get Claude Code](https://claude.ai)
- **Git** - For version control and deployments

### Platform-Specific (if using)

- **Azure Account** - Required for Azure features
  - [Azure Free Account](https://azure.microsoft.com/free/)
  - Azure CLI installed: `npm install -g azure-cli`

- **Railway Account** - Required for Railway features
  - [Railway Sign Up](https://railway.app/)
  - Railway CLI installed: `npm install -g @railway/cli`

### Optional but Recommended

- **VS Code** - For the best development experience
- **GitHub Account** - For CI/CD workflows
- **Docker** - For local containerized development

---

## Installation

### Option 1: Install from GitHub (Recommended)

1. Open Claude Code
2. Run the install plugin command
3. Enter plugin URL: `https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin`
4. Plugin will be downloaded and activated automatically

### Option 2: Manual Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
   ```

2. Copy to Claude Code plugins directory:
   ```bash
   cp -r larouex-fullstack-plugin ~/.claude/plugins/
   ```

3. Restart Claude Code

### Option 3: Install via Git

If you have Claude Code configured to use Git:
```bash
cd ~/.claude/plugins
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

---

## Quick Start

### Example 1: Scaffold a New Azure Project

```bash
# Start Claude Code
claude

# Use the scaffold command
/scaffold-azure-full

# Follow the prompts to configure:
# - Project name
# - Azure subscription
# - Resource group
# - Region
```

This creates a complete Next.js 15 project with:
- Azure Static Web Apps configuration
- Azure Functions API folder
- GitHub Actions workflow for CI/CD
- TypeScript and Bootstrap setup
- Environment configuration
- README with deployment instructions

### Example 2: Add a New Page

```bash
# Add a new page with routing
/add-page

# Specify:
# - Page name (e.g., "about")
# - Route path (e.g., "/about")
# - Layout type (default, full-width, sidebar)
```

Creates:
- New page in `app/[route]/page.tsx`
- Metadata configuration
- Responsive layout with Bootstrap
- SEO-optimized structure

### Example 3: Deploy to Staging

```bash
# For Azure
/deploy-azure-staging

# For Railway
/deploy-railway-staging
```

Deploys your application to staging environment with:
- Build optimization
- Environment variable configuration
- Health check validation
- Deployment URL output

---

## Commands Reference

### Scaffolding Commands (6 commands)

Create new projects with platform-specific configurations:

- `/scaffold-azure-nextjs` - Next.js 15 project for Azure Static Web Apps
- `/scaffold-azure-functions` - Azure Functions API project with TypeScript
- `/scaffold-azure-full` - Complete Azure project (Static Web Apps + Functions)
- `/scaffold-railway-nextjs` - Next.js 15 project optimized for Railway
- `/scaffold-railway-full` - Full-stack Railway project with PostgreSQL
- `/scaffold-nextjs` - Standalone Next.js 15 project (platform-agnostic)

### Azure Commands (8 commands)

Azure-specific cloud operations:

- `/add-api-azure` - Add Azure Function API endpoint
- `/add-database-azure` - Configure Azure Cosmos DB connection
- `/deploy-azure-staging` - Deploy to Azure staging environment
- `/deploy-azure-production` - Deploy to Azure production
- `/setup-monitoring-azure` - Configure Application Insights
- `/add-email-azure` - Setup email with Azure Communication Services
- `/add-upload-azure` - Configure Azure Blob Storage for file uploads
- `/add-search-azure` - Integrate Azure Cognitive Search
- `/add-websockets-azure` - Setup Azure Web PubSub for real-time features
- `/add-cron-azure` - Create Azure Function with timer trigger

### Railway Commands (7 commands)

Railway-specific deployment operations:

- `/add-api-railway` - Add REST API endpoint for Railway
- `/add-database-railway` - Configure Railway PostgreSQL database
- `/deploy-railway-staging` - Deploy to Railway staging
- `/deploy-railway-production` - Deploy to Railway production
- `/setup-monitoring-railway` - Setup Railway observability
- `/add-email-railway` - Configure email service for Railway
- `/add-upload-railway` - Setup file uploads with Railway storage
- `/add-websockets-railway` - Add WebSocket support for Railway
- `/add-cron-railway` - Create scheduled jobs on Railway

### Pages & Components (5 commands)

Build your application structure:

- `/add-page` - Create new page with routing and metadata
- `/add-component` - Generate reusable React component
- `/add-section` - Add page section component (Hero, Features, etc.)
- `/add-navigation` - Create responsive navigation system
- `/add-image-gallery` - Build image gallery with lightbox

### Forms & Validation (3 commands)

Form creation and handling:

- `/add-form` - Create form with validation and submission
- `/add-multistep-form` - Build multi-step form wizard
- `/add-table` - Generate data table with sorting and filtering

### Content & SEO (3 commands)

Content management and optimization:

- `/add-content-json` - Setup JSON-based content management
- `/add-seo` - Add SEO metadata and optimization
- `/add-onboarding` - Create user onboarding flow

### Authentication & Security (4 commands)

User authentication and security:

- `/add-auth` - Setup NextAuth.js authentication
- `/add-protected-route` - Create protected pages with auth guards
- `/audit-security` - Run security audit and vulnerability scan
- `/add-social-login` - Add social authentication providers

### Testing & Quality (4 commands)

Testing and quality assurance:

- `/add-tests` - Generate unit tests for components
- `/add-e2e-test` - Create end-to-end tests with Playwright
- `/audit-accessibility` - Run WCAG accessibility audit
- `/add-error-tracking` - Setup error monitoring (Sentry, etc.)

### Code Review & Quality Gates (6 commands)

Automated code review and quality checks:

- `/review-code` - Review uncommitted changes for issues and best practices
- `/review-component` - Deep review of React component architecture
- `/review-api` - Review API endpoint implementation
- `/review-security` - Security-focused code audit
- `/review-performance` - Performance analysis and optimization suggestions
- `/review-before-deploy` - Pre-deployment quality gate check

### Performance & Optimization (4 commands)

Optimize your application:

- `/optimize-images` - Optimize images with Next.js Image
- `/optimize-bundle` - Analyze and reduce bundle size
- `/optimize-lighthouse` - Run Lighthouse audit and fix issues
- `/add-caching` - Implement caching strategies

### Email & Notifications (3 commands)

Communication features:

- `/add-email-azure` - Azure Communication Services email
- `/add-email-railway` - Railway email service integration
- `/add-notifications` - Push notifications and alerts

### File Upload & Storage (3 commands)

File handling features:

- `/add-upload-azure` - Azure Blob Storage uploads
- `/add-upload-railway` - Railway file storage
- `/add-image-gallery` - Image gallery with uploads

### Search & Filtering (4 commands)

Search and data filtering:

- `/add-search-client` - Client-side search functionality
- `/add-search-azure` - Azure Cognitive Search integration
- `/add-filters` - Advanced filtering UI components
- `/add-analytics-google` - Google Analytics integration

### Analytics & Tracking (3 commands)

Analytics and user tracking:

- `/add-analytics-google` - Google Analytics 4 setup
- `/add-analytics-plausible` - Privacy-focused Plausible analytics
- `/add-heatmaps` - User interaction heatmaps

### Internationalization (2 commands)

Multi-language support:

- `/add-i18n` - Setup Next.js internationalization
- `/add-localization` - Add language translations

### Data Visualization (3 commands)

Charts and dashboards:

- `/add-charts` - Interactive charts (Chart.js, Recharts)
- `/add-dashboard` - Admin dashboard with widgets
- `/add-table` - Data tables with sorting/filtering

### Real-time Features (3 commands)

WebSocket and live updates:

- `/add-websockets-azure` - Azure Web PubSub
- `/add-websockets-railway` - Railway WebSocket support
- `/add-live-updates` - Real-time data synchronization

### Documentation (3 commands)

Project documentation:

- `/generate-readme` - Generate project README
- `/generate-api-docs` - Create API documentation
- `/add-onboarding` - Developer onboarding guide

### Error Handling (3 commands)

Error management:

- `/add-error-boundary` - React error boundaries
- `/add-error-pages` - Custom 404, 500 error pages
- `/add-error-tracking` - Error monitoring integration

### Scheduled Jobs (3 commands)

Background tasks and cron jobs:

- `/add-cron-azure` - Azure Function timer triggers
- `/add-cron-railway` - Railway cron jobs
- `/add-background-job` - Background task processing

### Social Integration (3 commands)

Social media features:

- `/add-social-share` - Social media sharing buttons
- `/add-social-login` - OAuth social authentication
- `/add-social-feed` - Social media feed integration

### Payment Processing (2 commands)

E-commerce features:

- `/add-stripe` - Stripe payment integration
- `/add-checkout` - Complete checkout flow

### Admin Panel (3 commands)

Administrative features:

- `/add-admin-panel` - Admin dashboard interface
- `/add-cms-ui` - Content management system UI
- `/add-user-management` - User administration panel

### Migration & Upgrade (4 commands)

Platform migration and updates:

- `/migrate-to-nextjs15` - Upgrade to Next.js 15
- `/migrate-azure-to-railway` - Migrate from Azure to Railway
- `/migrate-railway-to-azure` - Migrate from Railway to Azure
- `/upgrade-dependencies` - Update all dependencies safely

---

## Agents Reference

### 1. Frontend Development Agent

**Purpose**: Specialized in creating modern web applications with React, TypeScript, and Bootstrap.

**Capabilities**:
- Component development with TypeScript interfaces
- Responsive design (mobile, tablet, desktop)
- Bootstrap 5 grid system and components
- Navigation systems (mega menus, mobile overlays)
- Page architecture and templates
- WCAG 2.1 AA accessibility compliance
- Performance optimization with code splitting and memoization

**When to use**: Building UI components, pages, layouts, and responsive interfaces.

### 2. Forms Workflow Agent

**Purpose**: Expert in form creation, validation, and submission workflows.

**Capabilities**:
- Single and multi-step form creation
- Client and server-side validation
- Form state management
- File upload handling
- Error handling and user feedback
- Accessibility for form controls
- Form analytics and conversion tracking

**When to use**: Creating contact forms, registration forms, surveys, and complex data entry.

### 3. Content & SEO Agent

**Purpose**: Content management and search engine optimization specialist.

**Capabilities**:
- SEO metadata configuration
- JSON-based content management
- Schema.org structured data
- Open Graph and Twitter Cards
- Sitemap generation
- robots.txt configuration
- Content accessibility
- Performance optimization for content

**When to use**: Optimizing pages for search engines and managing content.

### 4. Azure Serverless Agent

**Purpose**: Expert in Azure Static Web Apps, Functions, and serverless architecture.

**Capabilities**:
- Azure Functions development (HTTP, Timer, Queue triggers)
- Cosmos DB integration
- Blob Storage operations
- Azure Communication Services
- Authentication with Azure AD
- API Management integration
- Cost optimization strategies

**When to use**: Building serverless APIs and integrating Azure services.

### 5. DevOps Azure Agent

**Purpose**: Azure deployment, CI/CD, and infrastructure specialist.

**Capabilities**:
- GitHub Actions workflows for Azure
- Static Web Apps deployment
- Azure Functions deployment
- Environment variable management
- Infrastructure as Code (Bicep, ARM)
- Staging and production environments
- Blue-green deployments

**When to use**: Setting up CI/CD pipelines and deploying to Azure.

### 6. DevOps Railway Agent

**Purpose**: Railway deployment and infrastructure management expert.

**Capabilities**:
- Railway service configuration
- PostgreSQL database setup
- Redis integration
- Environment variable management
- Railway CLI automation
- Deployment strategies
- Health checks and monitoring

**When to use**: Deploying and managing applications on Railway.

### 7. Monitoring & Observability Agent

**Purpose**: Application monitoring, logging, and performance tracking specialist.

**Capabilities**:
- Application Insights integration
- Custom metrics and events
- Performance monitoring
- Log aggregation and analysis
- Alert configuration
- Dashboard creation
- Distributed tracing

**When to use**: Setting up monitoring and tracking application health.

### 8. Testing & Quality Agent

**Purpose**: Testing strategy, test creation, and quality assurance expert.

**Capabilities**:
- Unit testing with Jest
- Component testing with React Testing Library
- E2E testing with Playwright/Cypress
- Integration testing
- Test coverage analysis
- Performance testing
- Accessibility testing

**When to use**: Creating tests and ensuring code quality.

### 9. Security & Production Agent

**Purpose**: Security auditing, best practices, and production readiness specialist.

**Capabilities**:
- Security vulnerability scanning
- Authentication and authorization
- Data validation and sanitization
- HTTPS and CORS configuration
- Environment variable security
- Rate limiting and DDoS protection
- Production deployment checklists

**When to use**: Security audits and production deployment preparation.

### 10. Accessibility & Compliance Agent

**Purpose**: WCAG compliance and accessibility expert.

**Capabilities**:
- WCAG 2.1 AA/AAA auditing
- ARIA attributes and roles
- Keyboard navigation
- Screen reader optimization
- Color contrast checking
- Focus management
- Accessibility testing automation

**When to use**: Ensuring your application is accessible to all users.

### 11. Authentication Agent

**Purpose**: User authentication, authorization, and session management expert.

**Capabilities**:
- NextAuth.js configuration
- OAuth provider integration (Google, GitHub, etc.)
- JWT token management
- Session handling
- Protected routes and middleware
- Role-based access control (RBAC)
- Multi-factor authentication

**When to use**: Implementing user authentication and authorization.

### 12. Code Review Agent

**Purpose**: Automated code review specialist ensuring quality and best practices.

**Capabilities**:
- Comprehensive code analysis (10 review categories)
- Security vulnerability detection
- Performance bottleneck identification
- Best practices enforcement
- Platform-specific validations (Azure/Railway)
- Severity-based issue classification (Critical, High, Medium, Low, Info)
- Actionable remediation suggestions
- Pre-deployment quality gates

**When to use**: Reviewing code changes, enforcing quality standards, pre-deployment checks.

---

## Examples

### Example 1: Building an Azure Static Web App

Step-by-step workflow for creating a complete Azure-hosted website:

```bash
# Step 1: Scaffold the project
/scaffold-azure-full

# This creates:
# - Next.js 15 project with App Router
# - Azure Functions API folder
# - GitHub Actions workflow
# - staticwebapp.config.json
# - Environment configuration

# Step 2: Add a homepage
/add-page
# Page name: home
# Route: /
# Layout: default with hero section

# Step 3: Add a contact form
/add-form
# Form name: contact
# Fields: name, email, message
# API endpoint: /api/contact

# Step 4: Setup email for form submissions
/add-email-azure
# Configure Azure Communication Services
# Connect to contact form

# Step 5: Add SEO optimization
/add-seo
# Configure metadata
# Add sitemap and robots.txt

# Step 6: Run accessibility audit
/audit-accessibility
# Fix any WCAG issues

# Step 7: Deploy to staging
/deploy-azure-staging
# Test the staging deployment

# Step 8: Deploy to production
/deploy-azure-production
# Your site is live!

# Step 9: Setup monitoring
/setup-monitoring-azure
# Configure Application Insights
```

### Example 2: Creating a Railway Full-Stack App

Building a full-stack application with database on Railway:

```bash
# Step 1: Scaffold Railway project
/scaffold-railway-full
# Creates Next.js app with PostgreSQL

# Step 2: Add authentication
/add-auth
# Setup NextAuth.js with database sessions

# Step 3: Create protected admin panel
/add-admin-panel
# Build admin dashboard

# Step 4: Add protected routes
/add-protected-route
# Protect admin pages

# Step 5: Add user management
/add-user-management
# CRUD operations for users

# Step 6: Setup database
/add-database-railway
# Configure PostgreSQL connection

# Step 7: Add API endpoints
/add-api-railway
# Create REST API for admin operations

# Step 8: Add monitoring
/setup-monitoring-railway
# Configure observability

# Step 9: Deploy to staging
/deploy-railway-staging

# Step 10: Deploy to production
/deploy-railway-production
```

### Example 3: Adding Authentication to Existing Project

Adding complete authentication flow:

```bash
# Step 1: Add authentication system
/add-auth
# Configure NextAuth.js
# Choose providers (Email, Google, GitHub)

# Step 2: Add social login
/add-social-login
# Configure OAuth providers
# Add provider buttons

# Step 3: Create protected routes
/add-protected-route
# Add middleware
# Protect specific pages

# Step 4: Add user management
/add-user-management
# User profile pages
# Account settings

# Step 5: Run security audit
/audit-security
# Check for vulnerabilities
# Fix security issues

# Step 6: Add tests for auth flows
/add-e2e-test
# Test login/logout
# Test protected routes
```

---

## Troubleshooting

### Common Issues and Solutions

#### Command not found

**Problem**: When typing `/command`, Claude Code doesn't recognize it.

**Solution**:
1. Verify the `.claude` folder is in your project root
2. Restart Claude Code: `exit` then `claude`
3. Check file permissions: `ls -la .claude/commands/`
4. Ensure command files end with `.md` extension

#### Azure deployment fails

**Problem**: Azure deployment fails with authentication error.

**Solution**:
1. Login to Azure CLI: `az login`
2. Set correct subscription: `az account set --subscription "YOUR_SUBSCRIPTION"`
3. Verify resource group exists: `az group list`
4. Check GitHub Actions secrets are configured

#### Railway deployment fails

**Problem**: Railway deployment fails or times out.

**Solution**:
1. Login to Railway: `railway login`
2. Link to correct project: `railway link`
3. Verify environment variables: `railway variables`
4. Check Railway dashboard for build logs

#### TypeScript errors after scaffolding

**Problem**: TypeScript shows errors in generated code.

**Solution**:
1. Install dependencies: `npm install`
2. Regenerate types: `npm run build`
3. Restart VS Code TypeScript server: Cmd+Shift+P > "TypeScript: Restart TS Server"

#### Bootstrap styles not loading

**Problem**: Bootstrap components don't have proper styling.

**Solution**:
1. Verify Bootstrap is installed: `npm list bootstrap`
2. Check import in layout: `import 'bootstrap/dist/css/bootstrap.min.css'`
3. Clear Next.js cache: `rm -rf .next`
4. Restart dev server: `npm run dev`

### Getting Help

- **Documentation**: Check command-specific README files in `.claude/commands/`
- **Agent Help**: Invoke the relevant agent for context-specific assistance
- **GitHub Issues**: [Report bugs or request features](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
- **Community**: Join discussions in GitHub Discussions
- **Claude Code Docs**: [Official Claude Code documentation](https://docs.anthropic.com/claude-code)

---

## Contributing

Contributions are welcome! Here's how you can help:

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Make your changes**
4. **Test thoroughly**
5. **Commit your changes**: `git commit -m 'Add amazing feature'`
6. **Push to the branch**: `git push origin feature/amazing-feature`
7. **Open a Pull Request**

### Adding New Commands

To add a new command to the plugin:

1. Create a new file in `.claude/commands/` with a descriptive name:
   ```bash
   touch .claude/commands/your-command-name.md
   ```

2. Add the command prompt following this template:
   ```markdown
   Brief description of what this command does.

   Detailed explanation including:
   - What it creates/modifies
   - Technologies used
   - Configuration options
   - Expected output

   Include specific instructions for implementation.
   ```

3. Test the command thoroughly
4. Update this README with the new command
5. Submit a pull request

### Improving Agents

To enhance an existing agent:

1. Locate the agent file in `.claude/agents/`
2. Add new capabilities or improve existing ones
3. Update examples and best practices
4. Test with real-world scenarios
5. Submit a pull request

### Code Style Guidelines

- Use TypeScript for all code examples
- Follow Next.js 15 best practices
- Include accessibility considerations
- Add comments for complex logic
- Provide error handling examples

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Larry W Jordan Jr

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Author

**Larry W Jordan Jr**

- GitHub: [@larouex](https://github.com/larouex)
- LinkedIn: [Larry W Jordan Jr](https://www.linkedin.com/in/larrywjordanjr/)
- Website: [larouex.com](https://larouex.com)

---

## Links

- **GitHub Repository**: [https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin)
- **Documentation**: [https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/tree/main/docs](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/tree/main/docs)
- **Issues**: [https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
- **Releases**: [https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/releases](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/releases)
- **Changelog**: [CHANGELOG.md](CHANGELOG.md)
- **Claude Code**: [https://claude.ai](https://claude.ai)
- **Next.js Documentation**: [https://nextjs.org/docs](https://nextjs.org/docs)
- **Azure Documentation**: [https://docs.microsoft.com/azure](https://docs.microsoft.com/azure)
- **Railway Documentation**: [https://docs.railway.app](https://docs.railway.app)

---

## Acknowledgments

Special thanks to:

- **Anthropic** - For Claude Code and AI assistance
- **Vercel** - For Next.js framework
- **Microsoft** - For Azure cloud platform
- **Railway** - For simple cloud deployments
- **Bootstrap Team** - For responsive CSS framework
- **Open Source Community** - For countless tools and libraries

---

## Roadmap

### Coming Soon

- [ ] Plugin Marketplace listing
- [ ] Video tutorials for common workflows
- [ ] Additional cloud platform support (AWS, GCP)
- [ ] GraphQL API scaffolding
- [ ] Database migration tools
- [ ] Component library generator
- [ ] Design system integration
- [ ] Mobile app scaffolding (React Native)
- [ ] WordPress migration tools
- [ ] E-commerce templates

### Under Consideration

- Integration with popular headless CMS platforms
- AI-powered content generation
- Automated testing dashboard
- Performance benchmarking tools
- Multi-tenant architecture templates
- Microservices scaffolding

---

## Statistics

- **Commands**: 81
- **Agents**: 12
- **Supported Platforms**: Azure, Railway, Standalone
- **Technologies**: 20+
- **Lines of Documentation**: 5000+
- **Active Development**: Yes
- **Community Contributors**: Open

---

<div align="center">

**Built with Claude Code**

If this plugin helped you build something amazing, consider giving it a star!

[Report Bug](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues) | [Request Feature](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues) | [View Documentation](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/tree/main/docs)

</div>
