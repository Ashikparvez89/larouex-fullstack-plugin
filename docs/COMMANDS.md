# Command Reference

## Overview

The Full-Stack Website Builder Plugin provides 75 slash commands organized into 23 categories. Each command is a specialized prompt that invokes one or more agents to accomplish specific development tasks.

### How Commands Work

Commands use the Claude Code slash command system:
- Type `/` to see all available commands
- Commands are stored in `.claude/commands/` as markdown files
- Each command invokes specific agents with detailed instructions
- Commands can be chained together for complex workflows

### Command Naming Convention

Commands follow a consistent pattern:
```
/{verb}-{feature}-{platform}
```

**Examples**:
- `/scaffold-azure-nextjs` - Creates Azure-optimized Next.js project
- `/add-form` - Adds a form component (platform-agnostic)
- `/deploy-railway-production` - Deploys to Railway production

**Platform Suffixes**:
- `-azure` - Azure-specific implementation
- `-railway` - Railway-specific implementation
- No suffix - Platform-agnostic or applicable to both

---

## Quick Reference

### Most Commonly Used Commands

```bash
# Getting Started
/scaffold-azure-full          # Complete Azure stack
/scaffold-railway-full        # Complete Railway stack
/scaffold-nextjs             # Basic Next.js project

# Feature Development
/add-page                    # New page with routing
/add-component               # React component
/add-form                    # Form with validation
/add-api-azure              # Azure Function endpoint
/add-api-railway            # Express.js endpoint

# Deployment
/deploy-azure-staging        # Deploy to Azure staging
/deploy-azure-production     # Deploy to Azure production
/deploy-railway-staging      # Deploy to Railway staging
/deploy-railway-production   # Deploy to Railway production

# Quality Assurance
/add-tests                  # Unit and integration tests
/add-e2e-test              # End-to-end tests
/audit-security            # Security audit
/audit-accessibility       # Accessibility audit
```

---

## Command Categories

### 1. Scaffolding Commands (6)

Commands that create new projects or major infrastructure.

#### `/scaffold-nextjs`

**Description**: Creates a basic Next.js 15 project with TypeScript and Bootstrap 5.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/scaffold-nextjs
```

**Prerequisites**:
- Node.js 20+
- npm or pnpm

**What It Creates**:
- Next.js 15 with App Router
- TypeScript configuration
- Bootstrap 5.3 integration
- Basic folder structure (/app, /components, /lib, /public)
- ESLint and Prettier configuration
- package.json with development scripts
- README.md with setup instructions

**Expected Output**:
Complete Next.js project ready for local development with `npm run dev`.

**Pro Tip**: Use this for platform-agnostic projects. Add platform-specific features later with `/add-api-azure` or `/add-api-railway`.

---

#### `/scaffold-azure-nextjs`

**Description**: Creates Next.js 15 project optimized for Azure Static Web Apps.

**Agent**: `frontend-development-agent` + `devops-azure-agent`

**Usage**:
```bash
/scaffold-azure-nextjs
```

**Prerequisites**:
- Node.js 20+
- Azure account
- GitHub repository

**What It Creates**:
- Everything from `/scaffold-nextjs` plus:
- Azure Functions API folder (/api)
- staticwebapp.config.json with routing rules
- GitHub Actions workflow for Azure deployment
- next.config.js configured for Azure
- Azure-specific environment configuration

**Expected Output**:
Next.js project with Azure deployment pipeline ready. Push to GitHub to trigger automatic deployment.

**Pro Tip**: Run this first when building for Azure. It sets up the entire deployment pipeline automatically.

---

#### `/scaffold-azure-functions`

**Description**: Creates standalone Azure Functions API project with TypeScript.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/scaffold-azure-functions
```

**Prerequisites**:
- Node.js 20+
- Azure Functions Core Tools
- Azure account

**What It Creates**:
- Azure Functions v4 project structure
- TypeScript configuration
- HTTP trigger template functions
- function.json configurations
- local.settings.json template
- host.json with runtime settings
- package.json with Azure Functions scripts
- .funcignore file

**Expected Output**:
Standalone API project. Run locally with `npm start` or `func start`.

**Pro Tip**: Use this for microservices or API-only projects. For full-stack apps, use `/scaffold-azure-full` instead.

---

#### `/scaffold-azure-full`

**Description**: Creates complete full-stack project with Next.js, Azure Functions, and Table Storage.

**Agent**: `frontend-development-agent` + `azure-serverless-agent` + `devops-azure-agent`

**Usage**:
```bash
/scaffold-azure-full
```

**Prerequisites**:
- Node.js 20+
- Azure account with active subscription
- Azure CLI installed
- GitHub repository

**What It Creates**:
- Next.js 15 frontend
- Azure Functions API (/api)
- Azure Table Storage configuration
- staticwebapp.config.json
- GitHub Actions workflow
- Application Insights integration
- Environment configuration for all environments
- Complete folder structure
- README with deployment instructions

**Expected Output**:
Production-ready full-stack project. Push to GitHub to deploy to Azure automatically.

**Pro Tip**: This is the recommended starting point for Azure projects. Includes everything you need for a complete application.

---

#### `/scaffold-railway-nextjs`

**Description**: Creates Next.js 15 project optimized for Railway deployment.

**Agent**: `frontend-development-agent` + `devops-railway-agent`

**Usage**:
```bash
/scaffold-railway-nextjs
```

**Prerequisites**:
- Node.js 20+
- Railway account
- Railway CLI installed

**What It Creates**:
- Next.js 15 with App Router
- TypeScript and Bootstrap 5
- railway.toml configuration
- Express.js server for API routes
- Railway-specific build configuration
- Environment variable templates
- Deployment scripts

**Expected Output**:
Next.js project ready for Railway. Deploy with `railway up`.

**Pro Tip**: Railway handles both frontend and backend in one service, simplifying deployment.

---

#### `/scaffold-railway-full`

**Description**: Creates complete full-stack project with Next.js, Express.js, PostgreSQL, and Prisma.

**Agent**: `frontend-development-agent` + `devops-railway-agent`

**Usage**:
```bash
/scaffold-railway-full
```

**Prerequisites**:
- Node.js 20+
- Railway account
- Railway CLI installed

**What It Creates**:
- Next.js 15 frontend
- Express.js API server
- PostgreSQL database configuration
- Prisma ORM setup
- railway.toml with services
- Database migration scripts
- Environment configuration
- Redis caching setup (optional)
- Complete project structure

**Expected Output**:
Production-ready full-stack project. Deploy all services with `railway up`.

**Pro Tip**: Railway automatically provisions PostgreSQL and Redis. No manual database setup needed.

---

### 2. Azure Platform Commands (8)

Commands specific to Azure infrastructure and services.

#### `/add-api-azure`

**Description**: Creates Azure Function HTTP endpoint with full integration.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-api-azure
```
*Follow prompts to specify endpoint name and functionality.*

**Prerequisites**:
- Azure Functions project initialized
- Azure Functions Core Tools

**What It Creates**:
- Azure Function with HTTP trigger
- TypeScript handler with proper types
- Input validation with Zod
- Error handling with proper HTTP status codes
- CORS configuration in function.json
- API client code in /lib/api for frontend
- Environment variable configuration
- JSDoc documentation
- Example usage component

**Expected Output**:
Working API endpoint. Test locally with `func start`, call from frontend with generated client.

**Pro Tip**: Always validate inputs and handle errors properly. The generated template includes best practices.

**Common Issues**:
- **CORS errors**: Check function.json has correct allowed origins
- **Cold starts**: Consider Premium plan for production

---

#### `/add-database-azure`

**Description**: Sets up Azure Table Storage with complete data layer.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-database-azure
```

**Prerequisites**:
- Azure Storage account
- Connection string in environment variables

**What It Creates**:
- Table Storage entity schema with TypeScript interfaces
- Table Storage client utility
- CRUD operations (Create, Read, Update, Delete, List with pagination)
- Query helpers for complex queries
- Error handling for all operations
- Entity validation
- Connection string configuration
- Application Insights logging
- README documentation for data model

**Expected Output**:
Complete data layer. Use generated functions in Azure Functions.

**Pro Tip**: Design PartitionKey carefully for optimal performance. Use categories, user IDs, or time periods.

**Common Issues**:
- **Slow queries**: Improve PartitionKey design
- **Connection errors**: Verify connection string in environment

---

#### `/deploy-azure-staging`

**Description**: Deploys current project to Azure staging environment.

**Agent**: `devops-azure-agent`

**Usage**:
```bash
/deploy-azure-staging
```

**Prerequisites**:
- Azure Static Web Apps resource created
- GitHub repository connected
- Azure CLI authenticated

**What It Executes**:
1. Checks staging slot exists (creates if missing)
2. Configures staging-specific environment variables
3. Builds Next.js with production optimization
4. Deploys frontend to staging slot
5. Deploys Azure Functions to staging
6. Runs smoke tests on staging endpoints
7. Verifies deployment health
8. Generates deployment summary with staging URL

**Expected Output**:
Deployed application accessible at staging URL (e.g., `https://myapp-staging.azurestaticapps.net`).

**Pro Tip**: Always deploy to staging first, test thoroughly, then deploy to production.

**Common Issues**:
- **Build failures**: Check build logs in GitHub Actions
- **Function deployment fails**: Verify Azure Functions Core Tools version

---

#### `/deploy-azure-production`

**Description**: Deploys current project to Azure production environment.

**Agent**: `devops-azure-agent`

**Usage**:
```bash
/deploy-azure-production
```

**Prerequisites**:
- Successful staging deployment
- All tests passing
- Security and accessibility audits complete

**What It Executes**:
1. Verifies staging deployment health
2. Runs final test suite
3. Builds production bundle
4. Deploys to production slot
5. Runs health checks
6. Configures production environment variables
7. Verifies deployment success
8. Sets up monitoring alerts

**Expected Output**:
Production deployment at main domain (e.g., `https://myapp.azurestaticapps.net`).

**Pro Tip**: Run `/audit-security` and `/audit-accessibility` before production deployment.

**Common Issues**:
- **Environment variables missing**: Set in Azure Portal > Configuration
- **Deployment rollback needed**: Use Azure Portal to swap slots

---

#### `/setup-monitoring-azure`

**Description**: Configures Application Insights monitoring for Azure project.

**Agent**: `monitoring-observability-agent` + `devops-azure-agent`

**Usage**:
```bash
/setup-monitoring-azure
```

**Prerequisites**:
- Azure Application Insights resource
- Instrumentation key or connection string

**What It Creates**:
- Application Insights SDK integration
- Custom metrics tracking
- Error tracking configuration
- Performance monitoring
- Log aggregation setup
- Monitoring dashboard
- Alert rules for critical metrics
- Health check endpoints
- Availability tests

**Expected Output**:
Complete monitoring solution. View metrics in Azure Portal > Application Insights.

**Pro Tip**: Set up alerts for error rate, response time, and availability immediately.

---

#### `/add-email-azure`

**Description**: Implements email sending using Azure Communication Services.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-email-azure
```

**Prerequisites**:
- Azure Communication Services resource
- Email domain configured and verified

**What It Creates**:
- Azure Communication Services client
- Email sending function
- Email templates with HTML/text versions
- Queue-based email sending (optional)
- Email tracking and logging
- Retry logic for failures
- API endpoint for email sending
- Frontend integration

**Expected Output**:
Working email functionality. Send emails from Azure Functions.

**Pro Tip**: Use queues for high-volume email sending to prevent timeouts.

---

#### `/add-upload-azure`

**Description**: Implements file upload with Azure Blob Storage.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-upload-azure
```

**Prerequisites**:
- Azure Storage account
- Blob container created

**What It Creates**:
- Blob Storage upload function
- File validation (size, type)
- Progress tracking
- Presigned URL generation
- Frontend upload component with drag-drop
- Image optimization (for images)
- Thumbnail generation
- File metadata storage

**Expected Output**:
Complete file upload system. Users can upload files through UI.

**Pro Tip**: Generate presigned URLs for direct client uploads to improve performance.

---

#### `/add-cron-azure`

**Description**: Creates scheduled job using Azure Functions timer trigger.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-cron-azure
```

**Prerequisites**:
- Azure Functions project

**What It Creates**:
- Timer trigger function
- Cron expression configuration
- Job execution logging
- Error handling and retry logic
- Job status tracking
- Manual trigger endpoint (for testing)
- Monitoring and alerting

**Expected Output**:
Scheduled job running on specified schedule (e.g., daily at 2 AM).

**Pro Tip**: Use NCRONTAB format for schedule (same as cron but with 6 fields including seconds).

**Common Issues**:
- **Job not running**: Check timer trigger is enabled in Azure Portal
- **Job runs multiple times**: Ensure singleton lock is configured

---

### 3. Railway Platform Commands (7)

Commands specific to Railway infrastructure and services.

#### `/add-api-railway`

**Description**: Creates Express.js API endpoint with TypeScript.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-api-railway
```

**Prerequisites**:
- Express.js server initialized
- TypeScript configured

**What It Creates**:
- Express.js route handler
- TypeScript types for request/response
- Input validation with Zod
- Error handling middleware
- CORS configuration
- API documentation
- Frontend API client
- Environment variable usage

**Expected Output**:
Working API endpoint. Test with `npm run dev`, access at `http://localhost:3000/api/...`.

**Pro Tip**: Railway has no cold starts, so no need to optimize for cold start performance.

---

#### `/add-database-railway`

**Description**: Sets up PostgreSQL database with Prisma ORM.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-database-railway
```

**Prerequisites**:
- Railway project
- PostgreSQL service provisioned

**What It Creates**:
- Prisma schema definition
- Database migrations
- Prisma client configuration
- CRUD operation helpers
- Connection pooling setup
- Seed data scripts
- Query utilities
- TypeScript types from schema
- Migration instructions

**Expected Output**:
Working database with Prisma ORM. Run migrations with `npx prisma migrate dev`.

**Pro Tip**: Railway automatically provides DATABASE_URL. Just run migrations and start coding.

**Common Issues**:
- **Connection timeouts**: Check DATABASE_URL is set correctly
- **Migration fails**: Ensure database is accessible from local machine

---

#### `/deploy-railway-staging`

**Description**: Deploys project to Railway staging environment.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/deploy-railway-staging
```

**Prerequisites**:
- Railway project created
- Railway CLI authenticated

**What It Executes**:
1. Switches to staging environment
2. Builds application
3. Runs database migrations
4. Deploys services
5. Runs smoke tests
6. Verifies health checks
7. Generates deployment URL

**Expected Output**:
Staged deployment accessible at Railway-generated URL.

**Pro Tip**: Railway automatically runs build and start commands from railway.toml.

---

#### `/deploy-railway-production`

**Description**: Deploys project to Railway production environment.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/deploy-railway-production
```

**Prerequisites**:
- Successful staging deployment
- Tests passing

**What It Executes**:
1. Verifies staging health
2. Switches to production environment
3. Runs production build
4. Executes database migrations
5. Deploys all services
6. Verifies deployment
7. Runs health checks

**Expected Output**:
Production deployment at custom domain or Railway URL.

**Pro Tip**: Set up custom domain in Railway dashboard before production deployment.

---

#### `/setup-monitoring-railway`

**Description**: Configures monitoring and logging for Railway project.

**Agent**: `monitoring-observability-agent` + `devops-railway-agent`

**Usage**:
```bash
/setup-monitoring-railway
```

**Prerequisites**:
- Railway project deployed

**What It Creates**:
- Winston logging configuration
- Structured logging format
- Log levels configuration
- Error tracking integration
- Performance metrics
- Health check endpoints
- Railway log analysis guide

**Expected Output**:
Structured logging viewable in Railway dashboard.

**Pro Tip**: Railway has built-in log aggregation. Use structured logs (JSON) for easy parsing.

---

#### `/add-email-railway`

**Description**: Implements email sending with SendGrid or similar service.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-email-railway
```

**Prerequisites**:
- SendGrid account (or alternative email service)
- API key

**What It Creates**:
- Email sending utility
- Email templates
- API endpoint for sending emails
- Queue-based processing (optional)
- Email tracking
- Retry logic
- Frontend integration

**Expected Output**:
Working email functionality accessible via API.

**Pro Tip**: Use Railway environment variables for API keys. Never commit secrets.

---

#### `/add-upload-railway`

**Description**: Implements file upload with Railway volume storage or S3.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-upload-railway
```

**Prerequisites**:
- Railway volume (or S3 bucket)

**What It Creates**:
- File upload API endpoint
- File validation
- Multer middleware configuration
- Progress tracking
- Frontend upload component
- File serving endpoint
- Image optimization
- Storage cleanup scripts

**Expected Output**:
File upload system with persistent storage.

**Pro Tip**: Use Railway volumes for small files, S3 for large files or high volume.

---

#### `/add-cron-railway`

**Description**: Creates scheduled job for Railway using node-cron.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-cron-railway
```

**Prerequisites**:
- Express.js server running

**What It Creates**:
- node-cron job configuration
- Job execution logic
- Logging and monitoring
- Manual trigger endpoint
- Error handling
- Job status tracking

**Expected Output**:
Scheduled job running in background on specified schedule.

**Pro Tip**: Railway keeps workers running, so cron jobs work reliably without cold starts.

---

### 4. Page & Component Development (5)

Commands for creating UI pages and components.

#### `/add-page`

**Description**: Creates new Next.js page with proper structure.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-page
```
*Specify page name and route when prompted.*

**Prerequisites**:
- Next.js project initialized

**What It Creates**:
- Page file in /app with Next.js routing
- Layout wrapper
- TypeScript types for props and params
- SEO metadata using Metadata API
- Responsive Bootstrap grid structure
- Server Component for data fetching
- Client Component patterns (if needed)
- Loading state (loading.tsx)
- Error boundary (error.tsx)
- Page-specific styles

**Expected Output**:
Accessible page at specified route (e.g., `/about` for `app/about/page.tsx`).

**Pro Tip**: Use Server Components by default. Only add 'use client' when needed for interactivity.

**Common Patterns**:
```typescript
// app/products/page.tsx
export const metadata = {
  title: 'Products | Store',
  description: 'Browse our product catalog',
};

export default async function ProductsPage() {
  const products = await fetchProducts();
  return <ProductGrid products={products} />;
}
```

---

#### `/add-component`

**Description**: Creates reusable React component with TypeScript.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-component
```

**Prerequisites**:
- Next.js or React project

**What It Creates**:
- Component file in /components
- TypeScript interface for props
- Component story (if Storybook configured)
- Unit tests
- CSS module or styled component
- JSDoc comments
- Usage examples

**Expected Output**:
Reusable component importable throughout application.

**Pro Tip**: Keep components small and focused. One component should do one thing well.

---

#### `/add-navigation`

**Description**: Creates site navigation system with responsive menu.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-navigation
```

**Prerequisites**:
- Next.js project with layout

**What It Creates**:
- Navigation component with links
- Mobile hamburger menu
- Active link styling
- Dropdown menus (if needed)
- Accessible keyboard navigation
- Bootstrap navbar styling
- Responsive behavior
- TypeScript types

**Expected Output**:
Navigation system in layout. Automatically shows active page.

**Pro Tip**: Use Next.js Link component for client-side navigation without page reloads.

---

#### `/add-section`

**Description**: Creates page section with Bootstrap grid layout.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-section
```

**Prerequisites**:
- Next.js project

**What It Creates**:
- Section component with container
- Bootstrap grid structure
- Responsive column layout
- Section variants (hero, features, testimonials)
- TypeScript props
- Accessible markup

**Expected Output**:
Reusable section component for building page layouts.

**Pro Tip**: Use Bootstrap's grid system (col-12 col-md-6 col-lg-4) for responsive layouts.

---

#### `/add-content-json`

**Description**: Sets up JSON-based content management system.

**Agent**: `content-seo-agent` + `frontend-development-agent`

**Usage**:
```bash
/add-content-json
```

**Prerequisites**:
- Next.js project

**What It Creates**:
- Content JSON structure in /content
- TypeScript types for content
- Content loader utilities
- Dynamic page generation from JSON
- Content validation
- Example content files
- CMS-like editing instructions

**Expected Output**:
JSON-based content system. Edit JSON files to update content.

**Pro Tip**: Great for marketing sites where non-technical users need to edit content.

---

### 5. Forms & Validation (3)

Commands for creating forms with validation.

#### `/add-form`

**Description**: Creates form component with validation and error handling.

**Agent**: `forms-workflow-agent`

**Usage**:
```bash
/add-form
```

**Prerequisites**:
- React project

**What It Creates**:
- Form component with React Hook Form
- TypeScript types for form data
- Zod validation schema
- Bootstrap-styled form fields
- Error display for each field
- Loading states during submission
- Success feedback
- Submit handler with API integration
- Reset functionality
- Accessibility features (ARIA attributes)

**Expected Output**:
Working form with validation. Submits data to API endpoint.

**Pro Tip**: Zod schemas automatically generate TypeScript types. Define validation once, get types free.

**Common Patterns**:
```typescript
const schema = z.object({
  email: z.string().email('Invalid email'),
  name: z.string().min(2, 'Name too short'),
  age: z.number().min(18, 'Must be 18+'),
});

type FormData = z.infer<typeof schema>;
```

---

#### `/add-multistep-form`

**Description**: Creates multi-step form wizard with progress tracking.

**Agent**: `forms-workflow-agent`

**Usage**:
```bash
/add-multistep-form
```

**Prerequisites**:
- React project

**What It Creates**:
- Multi-step form container
- Step components
- Progress indicator
- Navigation (previous/next buttons)
- Form state persistence
- Per-step validation
- Summary/review step
- Submit functionality
- Save as draft feature
- Accessibility for step navigation

**Expected Output**:
Multi-step form wizard. Users can navigate between steps, see progress.

**Pro Tip**: Validate each step before allowing progression. Save state to localStorage for form recovery.

**Common Use Cases**:
- User registration with profile setup
- Checkout process
- Loan applications
- Survey forms

---

#### `/add-filters`

**Description**: Creates filter and search interface for data.

**Agent**: `forms-workflow-agent` + `frontend-development-agent`

**Usage**:
```bash
/add-filters
```

**Prerequisites**:
- React project with data to filter

**What It Creates**:
- Filter component with multiple filter types
- Search input with debouncing
- Checkbox filters
- Range filters (price, date)
- Sort controls
- Active filter display
- Clear filters button
- URL parameter sync
- Responsive filter panel
- Filter count badges

**Expected Output**:
Filter interface. Users can search, filter, and sort data.

**Pro Tip**: Sync filters with URL parameters so users can share filtered views.

---

### 6. Content & SEO (4)

Commands for content management and SEO optimization.

#### `/add-seo`

**Description**: Adds comprehensive SEO metadata to pages.

**Agent**: `content-seo-agent`

**Usage**:
```bash
/add-seo
```

**Prerequisites**:
- Next.js page to optimize

**What It Creates**:
- Metadata object with title and description
- Open Graph tags for social sharing
- Twitter Card tags
- Canonical URL configuration
- Robots meta tags
- JSON-LD structured data (Schema.org)
- Dynamic metadata function for dynamic routes
- Image optimization for OG images
- Sitemap.xml generation
- Robots.txt configuration

**Expected Output**:
Page with complete SEO metadata. Test with Facebook Debugger and Twitter Card Validator.

**Pro Tip**: Keep titles under 60 characters, descriptions under 160 characters for optimal display.

**Common Patterns**:
```typescript
export const metadata: Metadata = {
  title: 'Product Name | Store',
  description: 'Product description for SEO',
  openGraph: {
    title: 'Product Name',
    description: 'Product description',
    images: ['/product-image.jpg'],
  },
};
```

---

#### `/add-search-client`

**Description**: Implements client-side search functionality.

**Agent**: `content-seo-agent` + `frontend-development-agent`

**Usage**:
```bash
/add-search-client
```

**Prerequisites**:
- React project with searchable content

**What It Creates**:
- Search component with input
- Client-side search algorithm (fuzzy search)
- Search result highlighting
- Search suggestions/autocomplete
- Recent searches tracking
- Keyboard shortcuts (/ to focus)
- Search analytics
- Mobile-friendly search

**Expected Output**:
Working search functionality. Users can search content instantly.

**Pro Tip**: Use libraries like Fuse.js for fuzzy search. Works great for small to medium datasets.

---

#### `/add-search-azure`

**Description**: Sets up Azure Cognitive Search integration.

**Agent**: `content-seo-agent` + `azure-serverless-agent`

**Usage**:
```bash
/add-search-azure
```

**Prerequisites**:
- Azure Cognitive Search resource
- Content to index

**What It Creates**:
- Azure Search client configuration
- Index definition
- Search API endpoint
- Content indexing function
- Search UI component
- Faceted search support
- Search suggestions
- Highlighting and snippets
- Search analytics

**Expected Output**:
Enterprise-grade search. Users can search with autocomplete, filters, and relevance ranking.

**Pro Tip**: Use Azure Cognitive Search for large datasets or when you need advanced features like synonyms and ML ranking.

---

#### `/generate-readme`

**Description**: Generates comprehensive README.md for project.

**Agent**: All relevant agents

**Usage**:
```bash
/generate-readme
```

**Prerequisites**:
- Project with code to document

**What It Creates**:
- README.md with project overview
- Installation instructions
- Development setup
- Deployment instructions
- Environment variables documentation
- API documentation links
- Project structure
- Contributing guidelines
- License information
- Badges and shields

**Expected Output**:
Professional README.md in root directory.

**Pro Tip**: Keep README updated as project evolves. Include screenshots and examples.

---

### 7. Authentication & Security (4)

Commands for user authentication and security.

#### `/add-auth`

**Description**: Implements complete authentication system.

**Agent**: `authentication-agent` + `security-production-agent`

**Usage**:
```bash
/add-auth
```

**Prerequisites**:
- Next.js project
- Database configured

**What It Creates**:
- Auth provider component with context
- Registration page with validation
- Login page with email/password
- Logout functionality
- Session management (JWT or sessions)
- Protected route wrapper
- Middleware for auth checking
- User profile page
- Password reset flow
- TypeScript types for User/Session
- API routes for auth operations
- Secure token storage

**Expected Output**:
Complete authentication system. Users can register, login, logout.

**Pro Tip**: Use NextAuth.js for production. Handles most edge cases and security concerns.

**Common Issues**:
- **Session not persisting**: Check cookie settings (httpOnly, secure, sameSite)
- **CSRF errors**: Ensure CSRF tokens are included in forms

---

#### `/add-protected-route`

**Description**: Creates protected pages that require authentication.

**Agent**: `authentication-agent`

**Usage**:
```bash
/add-protected-route
```

**Prerequisites**:
- Authentication system implemented

**What It Creates**:
- Middleware for route protection
- Redirect logic to login page
- Role-based access control
- Loading state during auth check
- Unauthorized page
- Protected layout component

**Expected Output**:
Protected routes. Unauthenticated users redirected to login.

**Pro Tip**: Use middleware.ts for server-side protection. Never rely on client-side only.

---

#### `/add-social-login`

**Description**: Adds OAuth providers (Google, GitHub, etc.).

**Agent**: `authentication-agent`

**Usage**:
```bash
/add-social-login
```

**Prerequisites**:
- Authentication system implemented
- OAuth app credentials from providers

**What It Creates**:
- OAuth provider configuration
- Social login buttons
- User profile merging
- OAuth callback handling
- Error handling
- Account linking flow

**Expected Output**:
Social login buttons. Users can sign in with Google, GitHub, etc.

**Pro Tip**: Always allow account linking so users can connect multiple providers.

---

#### `/audit-security`

**Description**: Performs comprehensive security audit.

**Agent**: `security-production-agent`

**Usage**:
```bash
/audit-security
```

**Prerequisites**:
- Project to audit

**What It Analyzes**:
- XSS, CSRF, SQL injection vulnerabilities
- Environment variable exposure
- CORS configuration
- Authentication and authorization
- Input validation and sanitization
- API endpoint security
- Dependency vulnerabilities (npm audit)
- Security headers
- Session management
- SQL/database query security
- File upload security
- HTTPS enforcement
- Error message information disclosure

**Expected Output**:
Detailed security report with severity ratings and remediation steps.

**Pro Tip**: Run before every production deployment. Fix Critical and High severity issues immediately.

**Common Findings**:
- Missing security headers → Add Helmet.js
- Dependency vulnerabilities → Run npm audit fix
- Exposed secrets → Move to environment variables

---

### 8. Testing & Quality (4)

Commands for testing and quality assurance.

#### `/add-tests`

**Description**: Creates unit and integration tests for components and APIs.

**Agent**: `testing-quality-agent`

**Usage**:
```bash
/add-tests
```

**Prerequisites**:
- Code to test

**What It Creates**:
- Jest configuration
- React Testing Library setup
- Unit tests for components
- Integration tests for APIs
- Test utilities and helpers
- Mock data and fixtures
- Test coverage configuration
- GitHub Actions test workflow

**Expected Output**:
Comprehensive test suite. Run with `npm test`.

**Pro Tip**: Aim for 80%+ coverage on critical business logic. Don't obsess over 100%.

**Testing Best Practices**:
- Test behavior, not implementation
- Use data-testid for stable selectors
- Mock external dependencies
- Keep tests independent

---

#### `/add-e2e-test`

**Description**: Sets up end-to-end testing with Playwright.

**Agent**: `testing-quality-agent`

**Usage**:
```bash
/add-e2e-test
```

**Prerequisites**:
- Running application

**What It Creates**:
- Playwright configuration
- E2E test examples
- Page object models
- Test fixtures
- CI/CD integration
- Visual regression tests (optional)
- Cross-browser test configuration
- Test reports

**Expected Output**:
E2E test suite. Run with `npx playwright test`.

**Pro Tip**: Focus E2E tests on critical user journeys (signup, checkout, etc.). They're slower than unit tests.

**Common Test Scenarios**:
- User registration and login
- Product purchase flow
- Form submissions
- Navigation flows

---

#### `/audit-accessibility`

**Description**: Performs WCAG 2.1 AA accessibility audit.

**Agent**: `accessibility-compliance-agent`

**Usage**:
```bash
/audit-accessibility
```

**Prerequisites**:
- Running application

**What It Analyzes**:
- Semantic HTML usage
- ARIA attributes
- Keyboard navigation
- Focus management
- Color contrast
- Screen reader compatibility
- Form labels and errors
- Heading hierarchy
- Alt text for images
- Skip links
- Focus indicators
- Text alternatives

**Expected Output**:
Accessibility report with WCAG violations and remediation steps.

**Pro Tip**: Run regularly during development, not just before launch. Accessibility is easier to build in than retrofit.

**Common Violations**:
- Missing alt text → Add to all images
- Low color contrast → Adjust colors to meet 4.5:1 ratio
- Missing form labels → Add label elements
- Keyboard navigation broken → Test with Tab key

---

#### `/optimize-lighthouse`

**Description**: Optimizes application based on Lighthouse audit.

**Agent**: `frontend-development-agent` + `testing-quality-agent`

**Usage**:
```bash
/optimize-lighthouse
```

**Prerequisites**:
- Deployed application

**What It Analyzes**:
- Performance metrics
- Accessibility
- Best practices
- SEO
- Progressive Web App features

**What It Optimizes**:
- Image optimization
- Code splitting
- Resource loading
- Caching strategies
- Critical CSS
- Font loading
- JavaScript execution

**Expected Output**:
Improved Lighthouse scores across all categories.

**Pro Tip**: Focus on Performance and Accessibility first. Aim for 90+ scores in both.

---

### 9. Performance Optimization (4)

Commands for improving application performance.

#### `/optimize-images`

**Description**: Optimizes all images for web performance.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/optimize-images
```

**Prerequisites**:
- Project with images

**What It Does**:
- Converts images to WebP/AVIF with fallbacks
- Replaces img tags with Next.js Image component
- Adds proper width/height to prevent layout shift
- Implements lazy loading for below-fold images
- Compresses images with sharp or imagemin
- Creates responsive image sets with srcset
- Adds priority loading for hero images
- Configures next.config for image optimization

**Expected Output**:
Optimized images with faster load times and better Core Web Vitals.

**Pro Tip**: Use Next.js Image component for automatic optimization. It handles everything automatically.

**Performance Gains**:
- 50-80% reduction in image file sizes
- Improved Largest Contentful Paint (LCP)
- Better mobile performance

---

#### `/optimize-bundle`

**Description**: Reduces JavaScript bundle size.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/optimize-bundle
```

**Prerequisites**:
- Built Next.js application

**What It Analyzes**:
- Bundle size analysis
- Unused dependencies
- Large dependencies
- Code splitting opportunities
- Dynamic imports needed

**What It Optimizes**:
- Implements code splitting
- Adds dynamic imports for large components
- Removes unused dependencies
- Configures tree shaking
- Optimizes third-party libraries
- Implements route-based code splitting

**Expected Output**:
Smaller bundle sizes and faster initial page loads.

**Pro Tip**: Use `@next/bundle-analyzer` to visualize bundle composition. Target large dependencies first.

**Common Optimizations**:
- Dynamic import heavy components
- Split vendor bundles
- Remove unused dependencies
- Use lighter alternatives (e.g., date-fns instead of moment)

---

#### `/add-caching`

**Description**: Implements caching strategies for performance.

**Agent**: `azure-serverless-agent` OR `devops-railway-agent`

**Usage**:
```bash
/add-caching
```

**Prerequisites**:
- Backend API
- Redis (for Railway) or Azure Cache for Redis

**What It Creates**:
- Cache client configuration
- Cache key generation utilities
- Cache invalidation strategies
- Cache warming scripts
- Cache monitoring
- TTL (Time To Live) configuration
- Cache-aside pattern implementation

**Expected Output**:
Caching layer reducing database queries and improving response times.

**Pro Tip**: Cache expensive database queries and external API calls. Use appropriate TTLs (5-60 minutes typically).

**Common Cache Strategies**:
- Cache-aside (most common)
- Write-through
- Write-behind

---

#### `/optimize-performance`

**Description**: Comprehensive performance optimization audit and implementation.

**Agent**: `frontend-development-agent` + `azure-serverless-agent` + `testing-quality-agent`

**Usage**:
```bash
/optimize-performance
```

**Prerequisites**:
- Running application

**What It Analyzes**:
- Core Web Vitals (LCP, FID, CLS)
- Time to First Byte (TTFB)
- First Contentful Paint (FCP)
- Bundle sizes
- Database query performance
- API response times
- Network waterfall

**What It Optimizes**:
- Image optimization
- Code splitting
- Database query optimization
- API response caching
- CDN configuration
- Resource prefetching
- Critical CSS extraction
- Font loading strategy

**Expected Output**:
Significantly improved performance metrics and user experience.

**Pro Tip**: Focus on Core Web Vitals. They directly impact SEO and user experience.

---

### 10. Email & Notifications (3)

Commands for email and notification systems.

#### `/add-email-azure`

**Description**: Implements email sending using Azure Communication Services.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-email-azure
```

See [Azure Platform Commands](#add-email-azure) for full details.

---

#### `/add-email-railway`

**Description**: Implements email sending with SendGrid or similar.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-email-railway
```

See [Railway Platform Commands](#add-email-railway) for full details.

---

#### `/add-notifications`

**Description**: Implements push notification system.

**Agent**: `frontend-development-agent` + `azure-serverless-agent` OR `devops-railway-agent`

**Usage**:
```bash
/add-notifications
```

**Prerequisites**:
- Backend API
- Push notification service (Firebase, OneSignal, or Web Push)

**What It Creates**:
- Service worker for Web Push
- Notification permission request UI
- Push subscription management
- Backend notification sending API
- Notification templates
- Notification preferences UI
- Test notification functionality

**Expected Output**:
Push notification system. Users can opt-in and receive notifications.

**Pro Tip**: Always request permission at appropriate times, not immediately on page load.

---

### 11. File Upload & Storage (3)

Commands for file handling and storage.

#### `/add-upload-azure`

**Description**: Implements file upload with Azure Blob Storage.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-upload-azure
```

See [Azure Platform Commands](#add-upload-azure) for full details.

---

#### `/add-upload-railway`

**Description**: Implements file upload with Railway volumes or S3.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-upload-railway
```

See [Railway Platform Commands](#add-upload-railway) for full details.

---

#### `/add-image-gallery`

**Description**: Creates image gallery with lightbox.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-image-gallery
```

**Prerequisites**:
- Images to display

**What It Creates**:
- Gallery grid component
- Lightbox/modal for full-size viewing
- Image navigation (prev/next)
- Touch gestures for mobile
- Lazy loading
- Image captions
- Zoom functionality
- Keyboard navigation
- Responsive layout

**Expected Output**:
Professional image gallery with lightbox.

**Pro Tip**: Use Next.js Image component for automatic optimization and responsive images.

---

### 12. Search & Filtering (3)

Commands for search and filter functionality.

#### `/add-search-client`

**Description**: Client-side search functionality.

**Agent**: `content-seo-agent` + `frontend-development-agent`

**Usage**:
```bash
/add-search-client
```

See [Content & SEO](#add-search-client) for full details.

---

#### `/add-search-azure`

**Description**: Azure Cognitive Search integration.

**Agent**: `content-seo-agent` + `azure-serverless-agent`

**Usage**:
```bash
/add-search-azure
```

See [Content & SEO](#add-search-azure) for full details.

---

#### `/add-filters`

**Description**: Filter and faceted search interface.

**Agent**: `forms-workflow-agent`

**Usage**:
```bash
/add-filters
```

See [Forms & Validation](#add-filters) for full details.

---

### 13. Analytics & Tracking (3)

Commands for analytics and user tracking.

#### `/add-analytics-google`

**Description**: Integrates Google Analytics 4.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-analytics-google
```

**Prerequisites**:
- Google Analytics property created
- Measurement ID

**What It Creates**:
- Google Analytics script integration
- GA4 configuration
- Custom event tracking
- E-commerce tracking (if applicable)
- User ID tracking
- Cookie consent integration
- Development environment filtering

**Expected Output**:
Google Analytics tracking. View data in GA4 dashboard.

**Pro Tip**: Wait 24-48 hours for data to appear in GA4. Use DebugView for immediate verification.

---

#### `/add-analytics-plausible`

**Description**: Integrates privacy-friendly Plausible Analytics.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-analytics-plausible
```

**Prerequisites**:
- Plausible account
- Site added to Plausible

**What It Creates**:
- Plausible script integration
- Custom event tracking
- Goal configuration
- Revenue tracking
- Outbound link tracking

**Expected Output**:
Privacy-friendly analytics. View in Plausible dashboard.

**Pro Tip**: Plausible is GDPR-compliant by default. No cookie consent needed.

---

#### `/add-heatmaps`

**Description**: Adds heatmap and session recording.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-heatmaps
```

**Prerequisites**:
- Hotjar, Microsoft Clarity, or similar account

**What It Creates**:
- Heatmap tracking script
- Session recording configuration
- Funnel analysis setup
- Privacy configuration

**Expected Output**:
Heatmaps and session recordings showing user behavior.

**Pro Tip**: Use heatmaps to identify usability issues and optimize conversions.

---

### 14. Internationalization (2)

Commands for multi-language support.

#### `/add-i18n`

**Description**: Implements internationalization (i18n) support.

**Agent**: `frontend-development-agent` + `content-seo-agent`

**Usage**:
```bash
/add-i18n
```

**Prerequisites**:
- Next.js project

**What It Creates**:
- next-intl or react-i18next setup
- Translation files (JSON) per language
- Language switcher component
- Locale detection
- Date/number formatting
- RTL support (if needed)
- URL structure for locales (/en/, /es/)
- SEO hreflang tags

**Expected Output**:
Multi-language application. Users can switch languages.

**Pro Tip**: Use Next.js internationalized routing for SEO benefits.

---

#### `/add-localization`

**Description**: Adds localized content and formatting.

**Agent**: `content-seo-agent`

**Usage**:
```bash
/add-localization
```

**Prerequisites**:
- i18n system configured

**What It Creates**:
- Translation management workflow
- Content localization for existing pages
- Currency formatting
- Date/time formatting
- Number formatting
- Pluralization rules
- Translation keys

**Expected Output**:
Fully localized content in multiple languages.

**Pro Tip**: Keep translation keys organized by page or feature for maintainability.

---

### 15. Data Visualization (3)

Commands for charts and data visualization.

#### `/add-charts`

**Description**: Adds chart components with Chart.js or Recharts.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-charts
```

**Prerequisites**:
- Data to visualize

**What It Creates**:
- Chart component library setup
- Example charts (line, bar, pie, area)
- Responsive chart configuration
- Chart customization utilities
- Data transformation helpers
- Interactive tooltips
- Export chart functionality
- Accessible chart alternatives (data tables)

**Expected Output**:
Interactive charts displaying data.

**Pro Tip**: Always provide accessible alternatives like data tables for screen readers.

---

#### `/add-dashboard`

**Description**: Creates admin or analytics dashboard.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-dashboard
```

**Prerequisites**:
- Authentication system
- Data to display

**What It Creates**:
- Dashboard layout
- Stat cards with key metrics
- Charts and graphs
- Data tables
- Real-time updates (optional)
- Filter and date range controls
- Export functionality
- Responsive mobile layout

**Expected Output**:
Complete dashboard with metrics and visualizations.

**Pro Tip**: Use skeleton screens for better perceived performance while loading data.

---

#### `/add-table`

**Description**: Creates data table with sorting, filtering, and pagination.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-table
```

**Prerequisites**:
- Data to display in table

**What It Creates**:
- Data table component
- Column configuration
- Sorting functionality
- Filtering per column
- Pagination
- Row selection
- Bulk actions
- Export to CSV
- Responsive table layout
- Accessible table markup

**Expected Output**:
Feature-rich data table with sorting, filtering, pagination.

**Pro Tip**: Use libraries like TanStack Table (formerly React Table) for complex tables.

---

### 16. Real-time Features (3)

Commands for real-time functionality.

#### `/add-websockets-azure`

**Description**: Implements WebSocket support with Azure Web PubSub.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-websockets-azure
```

**Prerequisites**:
- Azure Web PubSub Service

**What It Creates**:
- Web PubSub client setup
- Connection management
- Event handlers
- Reconnection logic
- Broadcasting utilities
- Room/group management
- Authentication for connections

**Expected Output**:
Real-time WebSocket connection. Perfect for chat, live updates, collaborative editing.

**Pro Tip**: Use groups for targeted broadcasts (e.g., notifications to specific users).

---

#### `/add-websockets-railway`

**Description**: Implements WebSocket support with Socket.io.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-websockets-railway
```

**Prerequisites**:
- Express.js server

**What It Creates**:
- Socket.io server setup
- Socket.io client integration
- Event handlers
- Room management
- Authentication middleware
- Reconnection handling
- Broadcasting utilities

**Expected Output**:
Real-time WebSocket connection using Socket.io.

**Pro Tip**: Socket.io handles reconnection automatically. Fallbacks to long-polling if WebSocket unavailable.

---

#### `/add-live-updates`

**Description**: Implements real-time data updates with Server-Sent Events or polling.

**Agent**: `frontend-development-agent` + `azure-serverless-agent` OR `devops-railway-agent`

**Usage**:
```bash
/add-live-updates
```

**Prerequisites**:
- API endpoint

**What It Creates**:
- SSE endpoint (Server-Sent Events)
- Client-side SSE connection
- Polling fallback
- Update notification UI
- Data refresh on updates
- Connection status indicator

**Expected Output**:
Real-time updates without WebSockets. Great for notifications, live feeds.

**Pro Tip**: SSE is simpler than WebSockets for one-way server-to-client updates.

---

### 17. Documentation (3)

Commands for generating documentation.

#### `/generate-readme`

**Description**: Generates comprehensive README.md.

**Agent**: All relevant agents

**Usage**:
```bash
/generate-readme
```

See [Content & SEO](#generate-readme) for full details.

---

#### `/generate-api-docs`

**Description**: Generates API documentation.

**Agent**: `azure-serverless-agent` OR `devops-railway-agent`

**Usage**:
```bash
/generate-api-docs
```

**Prerequisites**:
- API endpoints implemented

**What It Creates**:
- OpenAPI/Swagger specification
- API documentation site
- Endpoint descriptions
- Request/response examples
- Authentication documentation
- Error code reference
- Rate limiting documentation
- Interactive API explorer

**Expected Output**:
Professional API documentation accessible at /api/docs.

**Pro Tip**: Keep API docs in sync with code. Use JSDoc comments to generate docs automatically.

---

#### `/add-onboarding`

**Description**: Creates user onboarding flow with guided tour.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-onboarding
```

**Prerequisites**:
- Application features to showcase

**What It Creates**:
- Onboarding modal/overlay
- Step-by-step tour
- Feature highlights
- Skip option
- Progress indicator
- Completion tracking
- Personalized onboarding paths
- Tooltips for key features

**Expected Output**:
Guided onboarding tour for new users.

**Pro Tip**: Keep onboarding short (3-5 steps max). Let users explore after basics.

---

### 18. Error Handling (3)

Commands for error handling and recovery.

#### `/add-error-boundary`

**Description**: Implements React error boundaries.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-error-boundary
```

**Prerequisites**:
- React application

**What It Creates**:
- Error boundary component
- Error fallback UI
- Error logging
- Reset functionality
- Development vs production error display
- Error reporting to monitoring service

**Expected Output**:
Graceful error handling. App doesn't crash on component errors.

**Pro Tip**: Wrap different sections of your app with separate error boundaries for better isolation.

---

#### `/add-error-pages`

**Description**: Creates custom error pages (404, 500, etc.).

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-error-pages
```

**Prerequisites**:
- Next.js project

**What It Creates**:
- 404 not found page
- 500 server error page
- Custom error page styling
- Helpful error messages
- Navigation back to safety
- Search functionality
- Error code reference

**Expected Output**:
Branded error pages improving user experience during errors.

**Pro Tip**: Make 404 pages helpful with search, popular links, or humor.

---

#### `/add-error-tracking`

**Description**: Sets up error tracking with Sentry or similar.

**Agent**: `monitoring-observability-agent`

**Usage**:
```bash
/add-error-tracking
```

**Prerequisites**:
- Sentry account (or alternative)

**What It Creates**:
- Sentry SDK integration
- Error capture configuration
- Source map upload for debugging
- User context tracking
- Breadcrumb tracking
- Performance monitoring
- Release tracking

**Expected Output**:
Comprehensive error tracking. View errors in Sentry dashboard.

**Pro Tip**: Set up alerting for new or frequent errors. Fix critical issues immediately.

---

### 19. Scheduled Jobs (3)

Commands for background and scheduled tasks.

#### `/add-cron-azure`

**Description**: Creates scheduled Azure Function.

**Agent**: `azure-serverless-agent`

**Usage**:
```bash
/add-cron-azure
```

See [Azure Platform Commands](#add-cron-azure) for full details.

---

#### `/add-cron-railway`

**Description**: Creates scheduled job on Railway.

**Agent**: `devops-railway-agent`

**Usage**:
```bash
/add-cron-railway
```

See [Railway Platform Commands](#add-cron-railway) for full details.

---

#### `/add-background-job`

**Description**: Implements background job processing with queue.

**Agent**: `azure-serverless-agent` OR `devops-railway-agent`

**Usage**:
```bash
/add-background-job
```

**Prerequisites**:
- Backend API
- Queue service (Azure Queue Storage or BullMQ)

**What It Creates**:
- Job queue setup
- Job processor
- Job scheduling
- Retry logic
- Job status tracking
- Job dashboard
- Error handling
- Priority queues

**Expected Output**:
Background job processing. Long-running tasks don't block API responses.

**Pro Tip**: Use queues for email sending, image processing, report generation, etc.

**Common Use Cases**:
- Email sending
- Image/video processing
- Report generation
- Data imports/exports

---

### 20. Social Integration (3)

Commands for social media integration.

#### `/add-social-share`

**Description**: Adds social media sharing buttons.

**Agent**: `frontend-development-agent` + `content-seo-agent`

**Usage**:
```bash
/add-social-share
```

**Prerequisites**:
- Content to share

**What It Creates**:
- Share button component
- Platform-specific share URLs (Facebook, Twitter, LinkedIn, WhatsApp)
- Native share API integration
- Share counts (if available)
- Copy link functionality
- Email share
- Social metadata optimization

**Expected Output**:
Share buttons allowing users to share content on social media.

**Pro Tip**: Use Web Share API for mobile for better UX. Fallback to custom buttons on desktop.

---

#### `/add-social-login`

**Description**: Adds OAuth social login providers.

**Agent**: `authentication-agent`

**Usage**:
```bash
/add-social-login
```

See [Authentication & Security](#add-social-login) for full details.

---

#### `/add-social-feed`

**Description**: Embeds social media feeds on site.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/add-social-feed
```

**Prerequisites**:
- Social media accounts
- API credentials (if needed)

**What It Creates**:
- Social feed component
- Twitter/X timeline embed
- Instagram feed embed
- Facebook page plugin
- LinkedIn company feed
- Feed caching
- Responsive layout
- Loading states

**Expected Output**:
Social media feed displaying latest posts.

**Pro Tip**: Cache social feeds to avoid rate limits and improve performance.

---

### 21. Payment Processing (2)

Commands for payment and checkout.

#### `/add-stripe`

**Description**: Integrates Stripe payment processing.

**Agent**: `frontend-development-agent` + `azure-serverless-agent` OR `devops-railway-agent`

**Usage**:
```bash
/add-stripe
```

**Prerequisites**:
- Stripe account
- Stripe API keys

**What It Creates**:
- Stripe SDK integration
- Payment element/form
- Payment intent API endpoint
- Webhook handling
- Payment success page
- Payment failure handling
- Receipt email
- Subscription management (if applicable)
- Customer portal

**Expected Output**:
Complete payment processing with Stripe.

**Pro Tip**: Always use Stripe Elements for PCI compliance. Never handle raw card numbers.

**Testing**: Use test cards like 4242 4242 4242 4242 for testing.

---

#### `/add-checkout`

**Description**: Creates complete checkout flow for e-commerce.

**Agent**: `forms-workflow-agent` + `frontend-development-agent`

**Usage**:
```bash
/add-checkout
```

**Prerequisites**:
- Shopping cart implemented
- Payment integration

**What It Creates**:
- Multi-step checkout flow
- Cart review page
- Shipping information form
- Payment information form
- Order confirmation page
- Order summary
- Coupon/discount code support
- Shipping calculation
- Tax calculation
- Order email confirmations

**Expected Output**:
Complete checkout experience from cart to confirmation.

**Pro Tip**: Keep checkout to 3 steps max. Offer guest checkout option.

---

### 22. Admin Panel (3)

Commands for admin and CMS interfaces.

#### `/add-admin-panel`

**Description**: Creates admin dashboard with CRUD operations.

**Agent**: `frontend-development-agent` + `authentication-agent`

**Usage**:
```bash
/add-admin-panel
```

**Prerequisites**:
- Authentication with roles
- Database

**What It Creates**:
- Admin layout with sidebar
- User management interface
- CRUD interfaces for data models
- Role-based access control
- Audit logs
- Admin dashboard with metrics
- Search and filtering
- Bulk operations

**Expected Output**:
Complete admin panel for managing application.

**Pro Tip**: Always implement role-based access. Never expose admin functions to regular users.

---

#### `/add-cms-ui`

**Description**: Creates content management system interface.

**Agent**: `frontend-development-agent` + `forms-workflow-agent`

**Usage**:
```bash
/add-cms-ui
```

**Prerequisites**:
- Database for content storage

**What It Creates**:
- Content editor with rich text
- Media library
- Page management
- Category/tag management
- Content preview
- Publishing workflow
- Version history
- Content scheduling

**Expected Output**:
CMS interface for managing website content.

**Pro Tip**: Use TipTap or similar for rich text editing with good UX.

---

#### `/add-user-management`

**Description**: Creates user management interface for admins.

**Agent**: `frontend-development-agent` + `authentication-agent`

**Usage**:
```bash
/add-user-management
```

**Prerequisites**:
- Authentication system
- Admin authentication

**What It Creates**:
- User list with search and filters
- User detail pages
- Edit user functionality
- Role assignment
- Ban/suspend users
- Password reset for users
- Activity logs
- User statistics

**Expected Output**:
Admin interface for managing users.

**Pro Tip**: Include audit logs for all admin actions on user accounts.

---

### 23. Migration & Upgrade (4)

Commands for migrations and upgrades.

#### `/migrate-to-nextjs15`

**Description**: Migrates existing Next.js project to version 15.

**Agent**: `frontend-development-agent`

**Usage**:
```bash
/migrate-to-nextjs15
```

**Prerequisites**:
- Existing Next.js project (v13 or v14)

**What It Does**:
- Updates dependencies to Next.js 15
- Converts pages to app router (if needed)
- Updates metadata API usage
- Updates image optimization
- Fixes breaking changes
- Updates TypeScript types
- Tests for runtime issues
- Updates documentation

**Expected Output**:
Project running on Next.js 15 with all features working.

**Pro Tip**: Read Next.js 15 migration guide first. Test thoroughly after migration.

---

#### `/migrate-azure-to-railway`

**Description**: Migrates project from Azure to Railway.

**Agent**: `devops-azure-agent` + `devops-railway-agent`

**Usage**:
```bash
/migrate-azure-to-railway
```

**Prerequisites**:
- Existing Azure project
- Railway account

**What It Does**:
- Creates Railway project
- Converts Azure Functions to Express.js
- Migrates Table Storage to PostgreSQL with Prisma
- Updates environment variables
- Configures Railway services
- Migrates data
- Updates deployment configuration
- Tests migration

**Expected Output**:
Project running on Railway with all features working.

**Pro Tip**: Run both platforms in parallel during migration for zero-downtime migration.

---

#### `/migrate-railway-to-azure`

**Description**: Migrates project from Railway to Azure.

**Agent**: `devops-railway-agent` + `devops-azure-agent`

**Usage**:
```bash
/migrate-railway-to-azure
```

**Prerequisites**:
- Existing Railway project
- Azure account

**What It Does**:
- Creates Azure resources
- Converts Express.js to Azure Functions
- Migrates PostgreSQL to Table Storage (or Azure SQL)
- Sets up Azure Static Web Apps
- Configures environment variables
- Migrates data
- Sets up CI/CD with GitHub Actions
- Tests migration

**Expected Output**:
Project running on Azure with all features working.

**Pro Tip**: Consider Azure SQL instead of Table Storage if you have complex relational data.

---

#### `/upgrade-dependencies`

**Description**: Upgrades all project dependencies safely.

**Agent**: `frontend-development-agent` + `azure-serverless-agent` OR `devops-railway-agent`

**Usage**:
```bash
/upgrade-dependencies
```

**Prerequisites**:
- Project with dependencies

**What It Does**:
- Checks for outdated dependencies
- Analyzes breaking changes
- Updates dependencies incrementally
- Runs tests after each upgrade
- Fixes breaking changes
- Updates TypeScript types
- Updates documentation
- Creates upgrade report

**Expected Output**:
All dependencies upgraded to latest compatible versions.

**Pro Tip**: Upgrade incrementally, not all at once. Test after each major version bump.

**Common Issues**:
- Breaking changes → Read migration guides
- TypeScript errors → Update type definitions
- Tests failing → Fix code for new API

---

## Common Workflows

### Workflow 1: New Project Setup (Azure)

```bash
# 1. Scaffold complete Azure project
/scaffold-azure-full

# 2. Set up monitoring
/setup-monitoring-azure

# 3. Add authentication
/add-auth

# 4. Create main pages
/add-page  # Homepage
/add-page  # About
/add-page  # Contact

# 5. Add SEO to all pages
/add-seo

# 6. Create contact form
/add-form

# 7. Add API for form submission
/add-api-azure

# 8. Add tests
/add-tests
/add-e2e-test

# 9. Deploy to staging
/deploy-azure-staging

# 10. Run audits
/audit-security
/audit-accessibility

# 11. Deploy to production
/deploy-azure-production
```

---

### Workflow 2: New Project Setup (Railway)

```bash
# 1. Scaffold complete Railway project
/scaffold-railway-full

# 2. Set up monitoring
/setup-monitoring-railway

# 3. Add authentication
/add-auth

# 4. Create main pages
/add-page  # Homepage
/add-page  # Products
/add-page  # Dashboard

# 5. Add SEO
/add-seo

# 6. Set up database with Prisma
/add-database-railway

# 7. Create API endpoints
/add-api-railway

# 8. Add tests
/add-tests
/add-e2e-test

# 9. Deploy to staging
/deploy-railway-staging

# 10. Run audits
/audit-security
/audit-accessibility

# 11. Deploy to production
/deploy-railway-production
```

---

### Workflow 3: Adding E-commerce Features

```bash
# 1. Product pages
/add-page  # Product listing
/add-page  # Product detail

# 2. Shopping cart
/add-component  # Cart component

# 3. Checkout flow
/add-checkout

# 4. Payment processing
/add-stripe

# 5. Order management
/add-api-azure  # or /add-api-railway

# 6. Admin panel for products
/add-admin-panel

# 7. Email confirmations
/add-email-azure  # or /add-email-railway

# 8. Add analytics
/add-analytics-google

# 9. Test everything
/add-e2e-test

# 10. Optimize performance
/optimize-images
/optimize-performance
```

---

### Workflow 4: Improving Existing Project

```bash
# 1. Run audits to identify issues
/audit-security
/audit-accessibility
/optimize-lighthouse

# 2. Fix security issues
# (Address findings from security audit)

# 3. Fix accessibility issues
# (Address findings from accessibility audit)

# 4. Optimize performance
/optimize-images
/optimize-bundle
/add-caching

# 5. Add comprehensive tests
/add-tests
/add-e2e-test

# 6. Set up monitoring
/setup-monitoring-azure  # or /setup-monitoring-railway

# 7. Add error tracking
/add-error-tracking

# 8. Deploy improvements
/deploy-azure-staging  # or /deploy-railway-staging
# Test thoroughly
/deploy-azure-production  # or /deploy-railway-production
```

---

## Troubleshooting

### Command Not Found

**Problem**: Command doesn't appear when typing `/`

**Solutions**:
1. Check spelling - commands are case-sensitive
2. Verify plugin is installed correctly
3. Check `.claude/commands/` directory exists
4. Restart Claude Code

---

### Command Produces Unexpected Output

**Problem**: Command doesn't do what you expected

**Solutions**:
1. Read command description carefully - it might not match your expectation
2. Check prerequisites are met
3. Provide more context about your project structure
4. Try breaking complex requests into smaller commands
5. Specify platform (Azure or Railway) explicitly

---

### Platform-Specific Issues

#### Azure Issues

**Cold Start Delays**:
- Solution: Consider Premium plan with Always On
- Use connection pooling
- Minimize dependencies

**CORS Errors**:
- Check function.json configuration
- Verify staticwebapp.config.json
- Check allowed origins

**Environment Variables Not Found**:
- Set in Azure Portal > Configuration
- Add to GitHub Secrets for CI/CD
- Check spelling and casing

#### Railway Issues

**Build Failures**:
- Check railway.toml buildCommand
- Verify Node.js version compatibility
- Review build logs: `railway logs --build`

**Database Connection Issues**:
- Verify DATABASE_URL environment variable
- Check connection string format
- Use connection pooling
- Ensure database service is running

**Deployment Hangs**:
- Check start command in railway.toml
- Verify application starts successfully
- Review startup logs

---

## Pro Tips Collection

### General Development
- Start with scaffold commands to avoid missing pieces
- Use platform-specific commands for optimal implementation
- Always run audits before production deployment
- Deploy to staging first, always
- Keep commands focused - one feature at a time

### Performance
- Use Next.js Image component for all images
- Implement code splitting for large apps
- Cache expensive operations
- Optimize third-party scripts
- Monitor Core Web Vitals

### Security
- Never commit secrets to repository
- Use environment variables for configuration
- Implement rate limiting on public APIs
- Validate all user inputs
- Keep dependencies updated

### Testing
- Follow testing pyramid (many unit, fewer integration, few E2E)
- Write tests alongside code
- Test user behavior, not implementation
- Run tests in CI/CD
- Aim for 80%+ coverage on critical code

### Accessibility
- Use semantic HTML first
- Test with keyboard navigation
- Check color contrast
- Test with screen readers
- Implement ARIA attributes appropriately

### SEO
- Write unique titles and descriptions
- Use proper heading hierarchy
- Implement structured data
- Optimize images with alt text
- Generate sitemaps automatically

---

## Command Index (Alphabetical)

| Command | Category | Agent |
|---------|----------|-------|
| /add-admin-panel | Admin Panel | frontend-development-agent |
| /add-analytics-google | Analytics | frontend-development-agent |
| /add-analytics-plausible | Analytics | frontend-development-agent |
| /add-api-azure | Azure Platform | azure-serverless-agent |
| /add-api-railway | Railway Platform | devops-railway-agent |
| /add-auth | Authentication | authentication-agent |
| /add-background-job | Scheduled Jobs | azure/railway agents |
| /add-caching | Performance | azure/railway agents |
| /add-charts | Data Visualization | frontend-development-agent |
| /add-checkout | Payment | forms-workflow-agent |
| /add-cms-ui | Admin Panel | frontend-development-agent |
| /add-component | Page Development | frontend-development-agent |
| /add-content-json | Content & SEO | content-seo-agent |
| /add-cron-azure | Scheduled Jobs | azure-serverless-agent |
| /add-cron-railway | Scheduled Jobs | devops-railway-agent |
| /add-dashboard | Data Visualization | frontend-development-agent |
| /add-database-azure | Azure Platform | azure-serverless-agent |
| /add-database-railway | Railway Platform | devops-railway-agent |
| /add-e2e-test | Testing | testing-quality-agent |
| /add-email-azure | Email | azure-serverless-agent |
| /add-email-railway | Email | devops-railway-agent |
| /add-error-boundary | Error Handling | frontend-development-agent |
| /add-error-pages | Error Handling | frontend-development-agent |
| /add-error-tracking | Error Handling | monitoring-observability-agent |
| /add-filters | Forms | forms-workflow-agent |
| /add-form | Forms | forms-workflow-agent |
| /add-heatmaps | Analytics | frontend-development-agent |
| /add-i18n | Internationalization | frontend-development-agent |
| /add-image-gallery | File Upload | frontend-development-agent |
| /add-live-updates | Real-time | frontend-development-agent |
| /add-localization | Internationalization | content-seo-agent |
| /add-multistep-form | Forms | forms-workflow-agent |
| /add-navigation | Page Development | frontend-development-agent |
| /add-notifications | Email & Notifications | azure/railway agents |
| /add-onboarding | Documentation | frontend-development-agent |
| /add-page | Page Development | frontend-development-agent |
| /add-protected-route | Authentication | authentication-agent |
| /add-search-azure | Search | content-seo-agent |
| /add-search-client | Search | content-seo-agent |
| /add-section | Page Development | frontend-development-agent |
| /add-seo | Content & SEO | content-seo-agent |
| /add-social-feed | Social Integration | frontend-development-agent |
| /add-social-login | Social Integration | authentication-agent |
| /add-social-share | Social Integration | frontend-development-agent |
| /add-stripe | Payment | azure/railway agents |
| /add-table | Data Visualization | frontend-development-agent |
| /add-tests | Testing | testing-quality-agent |
| /add-upload-azure | File Upload | azure-serverless-agent |
| /add-upload-railway | File Upload | devops-railway-agent |
| /add-user-management | Admin Panel | frontend-development-agent |
| /add-websockets-azure | Real-time | azure-serverless-agent |
| /add-websockets-railway | Real-time | devops-railway-agent |
| /audit-accessibility | Testing | accessibility-compliance-agent |
| /audit-security | Security | security-production-agent |
| /deploy-azure-production | Azure Platform | devops-azure-agent |
| /deploy-azure-staging | Azure Platform | devops-azure-agent |
| /deploy-railway-production | Railway Platform | devops-railway-agent |
| /deploy-railway-staging | Railway Platform | devops-railway-agent |
| /generate-api-docs | Documentation | azure/railway agents |
| /generate-readme | Documentation | All agents |
| /migrate-azure-to-railway | Migration | devops-azure/railway-agent |
| /migrate-railway-to-azure | Migration | devops-railway/azure-agent |
| /migrate-to-nextjs15 | Migration | frontend-development-agent |
| /optimize-bundle | Performance | frontend-development-agent |
| /optimize-images | Performance | frontend-development-agent |
| /optimize-lighthouse | Performance | frontend-development-agent |
| /optimize-performance | Performance | Multiple agents |
| /scaffold-azure-full | Scaffolding | Multiple agents |
| /scaffold-azure-functions | Scaffolding | azure-serverless-agent |
| /scaffold-azure-nextjs | Scaffolding | frontend + azure agents |
| /scaffold-nextjs | Scaffolding | frontend-development-agent |
| /scaffold-railway-full | Scaffolding | Multiple agents |
| /scaffold-railway-nextjs | Scaffolding | frontend + railway agents |
| /setup-monitoring-azure | Azure Platform | monitoring-observability-agent |
| /setup-monitoring-railway | Railway Platform | monitoring-observability-agent |
| /upgrade-dependencies | Migration | Multiple agents |

---

## Conclusion

This command reference covers all 75 commands in the Full-Stack Website Builder Plugin. Each command is designed to accelerate specific development tasks while maintaining production-ready code quality.

**Key Principles**:
- Use scaffold commands to start new projects
- Add features incrementally with add-* commands
- Deploy to staging before production
- Run audits regularly
- Optimize before launch

**Getting Help**:
- Type `/` in Claude Code to see all commands
- Read command descriptions for details
- Check prerequisites before running commands
- Follow recommended workflows for best results

**Next Steps**:
1. Choose your platform (Azure or Railway)
2. Run appropriate scaffold command
3. Build features with add-* commands
4. Test with testing commands
5. Audit with security/accessibility commands
6. Deploy with deployment commands

For detailed agent information, see [AGENTS.md](./AGENTS.md).
