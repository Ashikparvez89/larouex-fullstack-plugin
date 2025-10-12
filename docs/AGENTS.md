# Agent Reference

## Overview

The Full-Stack Website Builder Plugin uses a specialized agent architecture where 11 AI agents work independently or collaboratively to handle different aspects of modern web development. Each agent is an expert in its domain, with deep knowledge of specific technologies, patterns, and best practices.

### How Agents Work

**Single-Agent Tasks**: Simple, focused tasks are handled by one agent:
- Creating a React component → `frontend-development-agent`
- Setting up Azure Functions → `azure-serverless-agent`
- Running accessibility audit → `accessibility-compliance-agent`

**Multi-Agent Collaboration**: Complex features often require multiple agents working together:
- Building a complete admin dashboard → `frontend-development-agent` + `authentication-agent` + `azure-serverless-agent` + `security-production-agent`
- Implementing e-commerce checkout → `forms-workflow-agent` + `frontend-development-agent` + `azure-serverless-agent` + `security-production-agent` + `testing-quality-agent`

Agents communicate and collaborate seamlessly, handing off tasks to the most appropriate specialist when needed.

---

## Agent List

### 1. frontend-development-agent

#### Purpose
Expert in building modern, responsive React applications using Next.js 15, TypeScript, and Bootstrap 5. This agent handles all frontend UI development, component architecture, and client-side functionality.

#### Capabilities
- Create React functional components with TypeScript
- Implement responsive layouts using Bootstrap 5.3 grid system and utilities
- Build reusable UI components following atomic design principles
- Configure Next.js 15 App Router with proper file-based routing
- Implement client and server components appropriately
- Handle client-side state management (useState, useContext, custom hooks)
- Create loading states, error boundaries, and skeleton screens
- Optimize component performance with React.memo and useMemo
- Implement code splitting and lazy loading
- Build accessible UI with semantic HTML and ARIA attributes
- Style components with Bootstrap classes and custom CSS modules
- Create responsive navigation, headers, footers, and layouts
- Implement mobile-first design patterns

#### Technologies
- **React**: 18+ with functional components and hooks
- **Next.js**: 15.x with App Router
- **TypeScript**: 5.x with strict mode enabled
- **Bootstrap**: 5.3+ for responsive design
- **CSS Modules**: Scoped styling alongside Bootstrap
- **React Hook Form**: Form state management
- **Zod**: Client-side validation schemas

#### When to Use
- Creating new pages or components
- Building responsive layouts
- Implementing UI interactions
- Setting up navigation systems
- Optimizing frontend performance
- Creating reusable component libraries
- Converting designs to working React code
- Refactoring component architecture

#### Example Commands
- `/add-page` - Creates a new Next.js page with routing
- `/add-component` - Generates reusable React component
- `/add-navigation` - Sets up site navigation system
- `/add-section` - Creates page sections with Bootstrap grid
- `/scaffold-nextjs` - Initializes basic Next.js project

#### Common Patterns

**Pattern 1: Page Creation**
```typescript
// Server Component for data fetching
export default async function ProductsPage() {
  const products = await fetchProducts();
  return <ProductGrid products={products} />;
}

// Client Component for interactivity
'use client';
export function ProductGrid({ products }) {
  const [filter, setFilter] = useState('all');
  // Interactive logic here
}
```

**Pattern 2: Responsive Layout**
```typescript
<div className="container">
  <div className="row g-4">
    <div className="col-12 col-md-6 col-lg-4">
      <Card />
    </div>
  </div>
</div>
```

**Pattern 3: Loading States**
```typescript
// loading.tsx
export default function Loading() {
  return <Skeleton />;
}
```

#### Best Practices
- **Use Server Components by default**, only add `'use client'` when needed for interactivity
- **Implement proper TypeScript types** for all props and state
- **Follow Bootstrap utilities** before writing custom CSS
- **Create small, focused components** that do one thing well
- **Optimize images** using Next.js Image component
- **Implement proper error boundaries** for resilience
- **Use semantic HTML** (header, nav, main, section, article)
- **Test responsive behavior** at all Bootstrap breakpoints (sm, md, lg, xl, xxl)
- **Leverage Next.js App Router features** like parallel routes and intercepting routes
- **Keep components pure** and side-effect free when possible

---

### 2. forms-workflow-agent

#### Purpose
Specialist in creating complex forms with validation, multi-step workflows, file uploads, and comprehensive user feedback. Handles all aspects of form state management and user input processing.

#### Capabilities
- Build single and multi-step forms with React Hook Form
- Implement client-side validation using Zod schemas
- Create custom form field components with error handling
- Handle file uploads with progress indicators and previews
- Build dynamic forms with conditional fields
- Implement form autosave and draft functionality
- Create accessible forms with proper labels and ARIA attributes
- Handle form submission with loading states and feedback
- Implement form wizards with navigation and progress tracking
- Build filter interfaces with search and faceted filtering
- Create data entry forms with inline validation
- Implement form arrays for repeatable field groups
- Handle complex form state (dirty, touched, errors)

#### Technologies
- **React Hook Form**: Form state management and validation
- **Zod**: Schema validation and type inference
- **Bootstrap Forms**: Form styling and layout
- **TypeScript**: Type-safe form data
- **React**: Controlled and uncontrolled components
- **Next.js**: Form submission with Server Actions

#### When to Use
- Creating contact forms, signup forms, or data entry forms
- Building multi-step registration or checkout flows
- Implementing file upload functionality
- Creating filter and search interfaces
- Building form-heavy admin interfaces
- Implementing complex validation logic
- Creating wizard-style user flows
- Building dynamic forms based on user input

#### Example Commands
- `/add-form` - Creates form with validation
- `/add-multistep-form` - Builds multi-step form workflow
- `/add-filters` - Implements search and filter interface

#### Common Patterns

**Pattern 1: Simple Form with Validation**
```typescript
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const schema = z.object({
  email: z.string().email(),
  name: z.string().min(2),
});

type FormData = z.infer<typeof schema>;

export function ContactForm() {
  const { register, handleSubmit, formState: { errors } } = useForm<FormData>({
    resolver: zodResolver(schema),
  });

  const onSubmit = async (data: FormData) => {
    // Submit logic
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div className="mb-3">
        <label htmlFor="email" className="form-label">Email</label>
        <input
          {...register('email')}
          type="email"
          className={`form-control ${errors.email ? 'is-invalid' : ''}`}
          id="email"
        />
        {errors.email && (
          <div className="invalid-feedback">{errors.email.message}</div>
        )}
      </div>
      <button type="submit" className="btn btn-primary">Submit</button>
    </form>
  );
}
```

**Pattern 2: Multi-Step Form**
```typescript
const [step, setStep] = useState(1);
const totalSteps = 3;

const nextStep = () => setStep(s => Math.min(s + 1, totalSteps));
const prevStep = () => setStep(s => Math.max(s - 1, 1));

return (
  <>
    <ProgressBar current={step} total={totalSteps} />
    {step === 1 && <PersonalInfoStep />}
    {step === 2 && <AddressStep />}
    {step === 3 && <ReviewStep />}
  </>
);
```

#### Best Practices
- **Use Zod for validation** to get TypeScript types automatically
- **Show inline errors** immediately after field blur
- **Implement field-level validation** before form submission
- **Provide clear error messages** that explain how to fix issues
- **Disable submit button** during submission to prevent duplicates
- **Show loading indicators** during async operations
- **Provide success feedback** after successful submission
- **Implement form persistence** for multi-step forms
- **Use proper input types** (email, tel, number) for mobile keyboards
- **Make forms keyboard accessible** with proper tab order
- **Test with screen readers** to ensure accessibility
- **Handle network errors gracefully** with retry options

---

### 3. content-seo-agent

#### Purpose
Expert in search engine optimization, content structure, and metadata management. Ensures content is discoverable, shareable, and optimized for search engines and social media.

#### Capabilities
- Implement Next.js 15 Metadata API for SEO
- Configure Open Graph tags for social sharing
- Set up Twitter Card metadata
- Generate JSON-LD structured data (Schema.org)
- Create and manage sitemaps (sitemap.xml)
- Configure robots.txt for crawler control
- Implement canonical URLs to prevent duplicate content
- Optimize meta descriptions and titles
- Set up dynamic metadata for parameterized routes
- Implement international SEO with hreflang tags
- Configure social media preview images
- Create rich snippets for search results
- Optimize content hierarchy and heading structure

#### Technologies
- **Next.js Metadata API**: Static and dynamic metadata
- **Schema.org**: Structured data standards
- **Open Graph Protocol**: Social media optimization
- **Twitter Cards**: Twitter-specific metadata
- **XML Sitemaps**: Search engine discovery
- **TypeScript**: Type-safe metadata configuration

#### When to Use
- Adding SEO to new or existing pages
- Optimizing content for search engines
- Implementing social media sharing
- Creating rich search results
- Setting up site-wide SEO configuration
- Optimizing for international audiences
- Improving content discoverability
- Implementing breadcrumb navigation

#### Example Commands
- `/add-seo` - Adds comprehensive SEO metadata
- `/add-content-json` - Sets up JSON content management
- `/add-search-client` - Implements client-side search
- `/add-search-azure` - Sets up Azure Cognitive Search

#### Common Patterns

**Pattern 1: Static Metadata**
```typescript
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'About Us | Company Name',
  description: 'Learn about our mission, values, and team.',
  keywords: ['about', 'company', 'mission'],
  openGraph: {
    title: 'About Us',
    description: 'Learn about our mission and team.',
    images: ['/images/about-og.jpg'],
    type: 'website',
  },
  twitter: {
    card: 'summary_large_image',
    title: 'About Us',
    description: 'Learn about our mission and team.',
    images: ['/images/about-twitter.jpg'],
  },
};
```

**Pattern 2: Dynamic Metadata**
```typescript
export async function generateMetadata({ params }): Promise<Metadata> {
  const product = await fetchProduct(params.id);

  return {
    title: `${product.name} | Store`,
    description: product.description,
    openGraph: {
      title: product.name,
      description: product.description,
      images: [product.image],
      type: 'product',
    },
  };
}
```

**Pattern 3: JSON-LD Structured Data**
```typescript
const jsonLd = {
  '@context': 'https://schema.org',
  '@type': 'Product',
  name: product.name,
  description: product.description,
  image: product.image,
  offers: {
    '@type': 'Offer',
    price: product.price,
    priceCurrency: 'USD',
  },
};

<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
/>
```

#### Best Practices
- **Write unique titles and descriptions** for each page
- **Keep titles under 60 characters** for full display in search results
- **Keep descriptions under 160 characters** for optimal display
- **Use descriptive, keyword-rich URLs** with proper slugs
- **Implement proper heading hierarchy** (h1, h2, h3)
- **Add alt text to all images** for accessibility and SEO
- **Use canonical URLs** to prevent duplicate content issues
- **Generate sitemaps automatically** as content changes
- **Test social previews** using Facebook Debugger and Twitter Card Validator
- **Implement breadcrumbs** for better site structure
- **Use semantic HTML** to help search engines understand content
- **Keep structured data up-to-date** with actual page content

---

### 4. azure-serverless-agent

#### Purpose
Expert in building serverless backend APIs using Azure Functions, managing Azure Table Storage, and integrating Azure services. Handles all Azure-specific backend development and serverless architecture.

#### Capabilities
- Create Azure Functions v4 with TypeScript
- Implement HTTP triggers with REST API patterns
- Design Azure Table Storage schemas with optimal PartitionKey/RowKey strategies
- Build CRUD operations for Table Storage
- Configure Application Insights for monitoring
- Implement input validation and error handling
- Set up CORS and security headers
- Create timer triggers for scheduled jobs
- Implement blob storage operations
- Configure function bindings and triggers
- Set up connection strings and app settings
- Implement retry policies and error recovery
- Build API integration layers for frontend
- Optimize cold start performance

#### Technologies
- **Azure Functions**: v4 with Node.js 20+ runtime
- **TypeScript**: Strongly typed function code
- **Azure Table Storage**: NoSQL data persistence
- **Application Insights**: Logging and monitoring
- **Azure Blob Storage**: File storage
- **Azure SDK**: JavaScript/TypeScript SDKs

#### When to Use
- Creating backend API endpoints on Azure
- Setting up data persistence with Table Storage
- Implementing serverless scheduled jobs
- Building file upload/download functionality
- Creating webhooks and event handlers
- Integrating with Azure services
- Setting up monitoring and logging
- Implementing serverless architecture patterns

#### Example Commands
- `/add-api-azure` - Creates Azure Function endpoint
- `/add-database-azure` - Sets up Table Storage
- `/scaffold-azure-functions` - Initializes Azure Functions project
- `/scaffold-azure-full` - Complete Azure stack
- `/add-cron-azure` - Creates scheduled Azure Function

#### Common Patterns

**Pattern 1: HTTP Trigger Function**
```typescript
import { app, HttpRequest, HttpResponseInit, InvocationContext } from '@azure/functions';

export async function getProducts(
  request: HttpRequest,
  context: InvocationContext
): Promise<HttpResponseInit> {
  context.log('Processing getProducts request');

  try {
    // Input validation
    const category = request.query.get('category');

    // Business logic
    const products = await fetchProductsFromStorage(category);

    return {
      status: 200,
      jsonBody: { data: products },
      headers: {
        'Content-Type': 'application/json',
      },
    };
  } catch (error) {
    context.error('Error fetching products:', error);
    return {
      status: 500,
      jsonBody: { error: 'Internal server error' },
    };
  }
}

app.http('getProducts', {
  methods: ['GET'],
  authLevel: 'anonymous',
  route: 'products',
  handler: getProducts,
});
```

**Pattern 2: Table Storage Operations**
```typescript
import { TableClient } from '@azure/data-tables';

const tableClient = TableClient.fromConnectionString(
  process.env.AZURE_STORAGE_CONNECTION_STRING,
  'Products'
);

// Create entity
async function createProduct(product: Product) {
  const entity = {
    partitionKey: product.category,
    rowKey: product.id,
    name: product.name,
    price: product.price,
  };
  await tableClient.createEntity(entity);
}

// Query entities
async function getProductsByCategory(category: string) {
  const products = tableClient.listEntities({
    queryOptions: { filter: `PartitionKey eq '${category}'` },
  });
  return products;
}
```

**Pattern 3: Timer Trigger**
```typescript
import { app, InvocationContext, Timer } from '@azure/functions';

export async function cleanupOldData(
  myTimer: Timer,
  context: InvocationContext
): Promise<void> {
  context.log('Running cleanup job');

  const cutoffDate = new Date();
  cutoffDate.setDate(cutoffDate.getDate() - 30);

  // Cleanup logic
  await deleteOldRecords(cutoffDate);
}

app.timer('cleanupJob', {
  schedule: '0 0 2 * * *', // 2 AM daily
  handler: cleanupOldData,
});
```

#### Best Practices
- **Minimize dependencies** to reduce cold start times
- **Use connection pooling** for database connections
- **Implement proper error handling** with try/catch blocks
- **Log all operations** for debugging and monitoring
- **Validate all inputs** before processing
- **Use environment variables** for configuration
- **Implement retry logic** for transient failures
- **Set appropriate timeouts** for long-running operations
- **Design PartitionKey strategically** for optimal Table Storage performance
- **Use batch operations** when updating multiple entities
- **Enable Application Insights** for production monitoring
- **Configure CORS properly** for frontend integration
- **Use managed identities** instead of connection strings when possible
- **Implement health check endpoints** for monitoring

---

### 5. devops-azure-agent

#### Purpose
Expert in Azure deployment workflows, CI/CD pipelines with GitHub Actions, and Azure infrastructure management. Handles all Azure DevOps operations and deployment automation.

#### Capabilities
- Create GitHub Actions workflows for Azure deployment
- Configure Azure Static Web Apps deployment
- Set up multi-environment deployment (dev, staging, production)
- Implement automated testing in CI/CD pipelines
- Configure environment variables and secrets
- Set up deployment slots and blue-green deployments
- Implement rollback strategies
- Configure custom domains and SSL certificates
- Set up monitoring and alerting
- Automate infrastructure provisioning
- Implement deployment gates and approvals
- Configure deployment health checks
- Set up deployment notifications

#### Technologies
- **GitHub Actions**: CI/CD automation
- **Azure CLI**: Command-line deployment
- **Azure Static Web Apps**: Frontend hosting
- **Azure Functions**: Backend hosting
- **Azure DevOps**: Alternative CI/CD platform
- **Azure Resource Manager**: Infrastructure as code
- **PowerShell/Bash**: Deployment scripts

#### When to Use
- Setting up automated deployments
- Creating CI/CD pipelines
- Managing multiple environments
- Implementing deployment strategies
- Configuring infrastructure
- Setting up monitoring and alerts
- Managing secrets and configuration
- Troubleshooting deployment issues

#### Example Commands
- `/deploy-azure-staging` - Deploys to Azure staging
- `/deploy-azure-production` - Deploys to Azure production
- `/setup-monitoring-azure` - Configures monitoring
- `/scaffold-azure-full` - Sets up complete Azure infrastructure

#### Common Patterns

**Pattern 1: GitHub Actions Workflow**
```yaml
name: Deploy to Azure
on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies
        run: npm ci

      - name: Build
        run: npm run build

      - name: Run tests
        run: npm test

      - name: Deploy to Azure
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: 'upload'
          app_location: '/'
          api_location: 'api'
          output_location: '.next'
```

**Pattern 2: Environment Configuration**
```yaml
# Production environment
production:
  environment:
    name: production
    url: https://myapp.azurestaticapps.net
  steps:
    - name: Deploy
      with:
        deployment_environment: 'Production'
```

**Pattern 3: Azure CLI Deployment**
```bash
# Deploy Azure Function
az functionapp deployment source config-zip \
  --resource-group myResourceGroup \
  --name myFunctionApp \
  --src api.zip

# Configure app settings
az functionapp config appsettings set \
  --resource-group myResourceGroup \
  --name myFunctionApp \
  --settings DATABASE_URL=$DATABASE_URL
```

#### Best Practices
- **Use separate environments** for dev, staging, and production
- **Implement automated testing** before deployment
- **Store secrets in GitHub Secrets** or Azure Key Vault
- **Use deployment slots** for zero-downtime deployments
- **Implement health checks** after deployment
- **Set up automatic rollback** on failed deployments
- **Monitor deployment metrics** with Application Insights
- **Use consistent naming conventions** for resources
- **Document deployment procedures** in README
- **Implement deployment approvals** for production
- **Tag releases** with semantic versioning
- **Set up deployment notifications** to team channels

---

### 6. devops-railway-agent

#### Purpose
Expert in Railway platform deployment, PostgreSQL database management, and Railway-specific infrastructure. Handles all Railway deployment workflows and platform operations.

#### Capabilities
- Configure Railway project and services
- Set up PostgreSQL databases with Prisma ORM
- Create multi-environment deployments (staging/production)
- Configure environment variables per environment
- Set up custom domains and SSL
- Implement health checks and monitoring
- Configure build and start commands
- Set up Redis caching layer
- Implement database migrations
- Configure service networking
- Set up volume mounts for persistent storage
- Implement Railway CLI automation
- Configure webhook deployments

#### Technologies
- **Railway Platform**: Unified hosting platform
- **Railway CLI**: Command-line interface
- **PostgreSQL**: Relational database
- **Prisma**: TypeScript ORM
- **Redis**: In-memory caching
- **Express.js**: Backend framework
- **Docker**: Container deployment
- **Git**: Deployment triggers

#### When to Use
- Setting up Railway projects
- Configuring database and caching
- Creating staging and production environments
- Managing Railway deployments
- Setting up environment variables
- Configuring custom domains
- Troubleshooting Railway issues
- Implementing database migrations

#### Example Commands
- `/deploy-railway-staging` - Deploys to Railway staging
- `/deploy-railway-production` - Deploys to Railway production
- `/add-database-railway` - Sets up PostgreSQL with Prisma
- `/scaffold-railway-full` - Complete Railway stack
- `/add-cron-railway` - Creates scheduled job

#### Common Patterns

**Pattern 1: Railway Configuration (railway.toml)**
```toml
[build]
builder = "nixpacks"
buildCommand = "npm run build"

[deploy]
startCommand = "npm start"
restartPolicyType = "on-failure"
restartPolicyMaxRetries = 10

[[services]]
name = "web"
type = "web"

[[services]]
name = "api"
type = "worker"
```

**Pattern 2: Database Setup with Prisma**
```typescript
// schema.prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id        String   @id @default(uuid())
  email     String   @unique
  name      String
  createdAt DateTime @default(now())
}
```

**Pattern 3: Environment Variables**
```bash
# Set environment variables
railway variables set DATABASE_URL="postgresql://..."
railway variables set API_KEY="secret-key"

# Link to specific environment
railway environment staging
railway variables set NODE_ENV="staging"
```

#### Best Practices
- **Use separate Railway projects** for staging and production
- **Configure health checks** for automatic restarts
- **Use Prisma migrations** for database schema changes
- **Store connection strings** as environment variables
- **Enable connection pooling** for database connections
- **Use Redis** for caching and session storage
- **Set up monitoring** with Railway logs
- **Implement graceful shutdown** in applications
- **Use volume mounts** for persistent file storage
- **Configure proper resource limits** for services
- **Use Railway CLI** for automation
- **Set up webhook deployments** for Git pushes

---

### 7. monitoring-observability-agent

#### Purpose
Expert in application monitoring, logging, performance tracking, and observability. Ensures applications are properly instrumented and monitored in production.

#### Capabilities
- Set up Application Insights for Azure
- Configure structured logging with Winston or Pino
- Implement custom metrics and events
- Create performance monitoring dashboards
- Set up error tracking and alerting
- Implement distributed tracing
- Configure log aggregation
- Set up health check endpoints
- Implement availability monitoring
- Create custom alerting rules
- Configure log retention policies
- Implement real-time monitoring
- Set up SLA tracking

#### Technologies
- **Application Insights**: Azure monitoring
- **Winston/Pino**: Structured logging
- **Prometheus**: Metrics collection
- **Grafana**: Visualization dashboards
- **Sentry**: Error tracking
- **Datadog**: Full-stack observability
- **New Relic**: Application performance monitoring
- **Railway Logs**: Railway platform logging

#### When to Use
- Setting up production monitoring
- Implementing logging strategies
- Creating performance dashboards
- Configuring alerts and notifications
- Troubleshooting production issues
- Tracking application performance
- Implementing error tracking
- Setting up observability best practices

#### Example Commands
- `/setup-monitoring-azure` - Configures Azure monitoring
- `/setup-monitoring-railway` - Configures Railway monitoring
- `/add-error-tracking` - Sets up error tracking service

#### Common Patterns

**Pattern 1: Structured Logging**
```typescript
import winston from 'winston';

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  defaultMeta: { service: 'api' },
  transports: [
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' }),
  ],
});

// Usage
logger.info('User login', { userId: user.id, email: user.email });
logger.error('Database error', { error: error.message, query });
```

**Pattern 2: Application Insights**
```typescript
import { ApplicationInsights } from '@azure/monitor-opentelemetry';

const appInsights = new ApplicationInsights({
  connectionString: process.env.APPLICATIONINSIGHTS_CONNECTION_STRING,
});
appInsights.start();

// Track custom events
appInsights.defaultClient.trackEvent({
  name: 'UserRegistration',
  properties: { plan: 'premium', source: 'web' },
});

// Track metrics
appInsights.defaultClient.trackMetric({
  name: 'CheckoutDuration',
  value: duration,
});
```

**Pattern 3: Health Check Endpoint**
```typescript
export async function health(req: HttpRequest): Promise<HttpResponseInit> {
  const checks = {
    database: await checkDatabase(),
    cache: await checkCache(),
    storage: await checkStorage(),
  };

  const healthy = Object.values(checks).every(check => check.status === 'ok');

  return {
    status: healthy ? 200 : 503,
    jsonBody: {
      status: healthy ? 'healthy' : 'unhealthy',
      checks,
      timestamp: new Date().toISOString(),
    },
  };
}
```

#### Best Practices
- **Use structured logging** with JSON format for easy parsing
- **Log at appropriate levels** (error, warn, info, debug)
- **Include context** in log messages (user ID, request ID, etc.)
- **Set up alerts** for critical errors and performance degradation
- **Monitor key metrics** like response time, error rate, throughput
- **Implement distributed tracing** for microservices
- **Use correlation IDs** to track requests across services
- **Set up dashboards** for real-time monitoring
- **Configure log retention** based on compliance requirements
- **Monitor database performance** with query analysis
- **Track business metrics** alongside technical metrics
- **Set up synthetic monitoring** to catch issues proactively

---

### 8. testing-quality-agent

#### Purpose
Expert in comprehensive testing strategies including unit tests, integration tests, and end-to-end testing. Ensures code quality through automated testing and quality assurance practices.

#### Capabilities
- Create unit tests with Jest and React Testing Library
- Build integration tests for API endpoints
- Implement E2E tests with Playwright
- Set up test coverage reporting
- Configure CI/CD test automation
- Create visual regression tests
- Implement accessibility testing
- Build performance testing suites
- Create test fixtures and mocks
- Set up test databases and environments
- Implement snapshot testing
- Create API contract tests
- Configure test parallelization

#### Technologies
- **Jest**: JavaScript testing framework
- **React Testing Library**: React component testing
- **Playwright**: End-to-end testing
- **MSW**: API mocking for tests
- **Testing Library**: DOM testing utilities
- **Vitest**: Fast unit testing (alternative)
- **Cypress**: E2E testing (alternative)
- **Istanbul**: Code coverage

#### When to Use
- Adding tests to new features
- Setting up testing infrastructure
- Improving test coverage
- Creating E2E test suites
- Implementing TDD workflows
- Testing complex user flows
- Setting up CI/CD testing
- Debugging test failures

#### Example Commands
- `/add-tests` - Creates unit and integration tests
- `/add-e2e-test` - Sets up E2E testing with Playwright

#### Common Patterns

**Pattern 1: Component Unit Test**
```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import { ContactForm } from './ContactForm';

describe('ContactForm', () => {
  it('shows validation error for invalid email', async () => {
    render(<ContactForm />);

    const emailInput = screen.getByLabelText(/email/i);
    fireEvent.change(emailInput, { target: { value: 'invalid' } });
    fireEvent.blur(emailInput);

    expect(await screen.findByText(/invalid email/i)).toBeInTheDocument();
  });

  it('submits form with valid data', async () => {
    const onSubmit = jest.fn();
    render(<ContactForm onSubmit={onSubmit} />);

    fireEvent.change(screen.getByLabelText(/email/i), {
      target: { value: 'user@example.com' },
    });
    fireEvent.change(screen.getByLabelText(/message/i), {
      target: { value: 'Hello' },
    });

    fireEvent.click(screen.getByRole('button', { name: /submit/i }));

    await waitFor(() => expect(onSubmit).toHaveBeenCalled());
  });
});
```

**Pattern 2: API Integration Test**
```typescript
import { app } from './app';
import request from 'supertest';

describe('Products API', () => {
  it('GET /api/products returns products', async () => {
    const response = await request(app)
      .get('/api/products')
      .expect(200);

    expect(response.body).toHaveProperty('data');
    expect(Array.isArray(response.body.data)).toBe(true);
  });

  it('POST /api/products creates product', async () => {
    const product = { name: 'Test Product', price: 19.99 };

    const response = await request(app)
      .post('/api/products')
      .send(product)
      .expect(201);

    expect(response.body).toMatchObject(product);
  });
});
```

**Pattern 3: E2E Test with Playwright**
```typescript
import { test, expect } from '@playwright/test';

test('user can complete checkout', async ({ page }) => {
  await page.goto('/products');

  // Add product to cart
  await page.click('[data-testid="add-to-cart"]');
  await expect(page.locator('[data-testid="cart-count"]')).toHaveText('1');

  // Go to checkout
  await page.click('[data-testid="checkout-button"]');

  // Fill checkout form
  await page.fill('#email', 'user@example.com');
  await page.fill('#cardNumber', '4242424242424242');

  // Submit order
  await page.click('button[type="submit"]');

  // Verify success
  await expect(page.locator('h1')).toContainText('Order Confirmed');
});
```

#### Best Practices
- **Follow testing pyramid** (many unit tests, fewer integration tests, few E2E tests)
- **Write tests alongside code** using TDD when possible
- **Test user behavior** not implementation details
- **Use meaningful test names** that describe what's being tested
- **Keep tests isolated** and independent
- **Mock external dependencies** in unit tests
- **Use real implementations** in integration tests
- **Test edge cases** and error conditions
- **Maintain test coverage** above 80% for critical code
- **Run tests in CI/CD** before deployment
- **Use data-testid** attributes for reliable selectors
- **Test accessibility** with screen reader simulators

---

### 9. security-production-agent

#### Purpose
Expert in application security, secure coding practices, and production-ready security implementations. Ensures applications follow security best practices and are protected against common vulnerabilities.

#### Capabilities
- Conduct security audits and vulnerability assessments
- Implement input validation and sanitization
- Configure CORS and security headers
- Set up CSRF protection
- Implement rate limiting and DDoS protection
- Secure API endpoints with authentication
- Configure Content Security Policy (CSP)
- Implement SQL injection prevention
- Set up XSS protection
- Configure secure session management
- Implement secret management
- Set up security monitoring and alerts
- Conduct dependency vulnerability scanning

#### Technologies
- **Helmet.js**: Security headers
- **Express Rate Limit**: Rate limiting
- **Joi/Zod**: Input validation
- **bcrypt**: Password hashing
- **jsonwebtoken**: JWT handling
- **OWASP**: Security guidelines
- **npm audit**: Dependency scanning
- **Azure Key Vault**: Secret management

#### When to Use
- Conducting security audits
- Implementing authentication and authorization
- Securing API endpoints
- Protecting against common vulnerabilities
- Implementing data encryption
- Setting up security headers
- Reviewing code for security issues
- Preparing for production deployment

#### Example Commands
- `/audit-security` - Comprehensive security audit
- `/add-auth` - Implements authentication system
- `/add-protected-route` - Creates protected routes

#### Common Patterns

**Pattern 1: Security Headers**
```typescript
import helmet from 'helmet';

app.use(helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      scriptSrc: ["'self'"],
      imgSrc: ["'self'", "data:", "https:"],
    },
  },
  hsts: {
    maxAge: 31536000,
    includeSubDomains: true,
    preload: true,
  },
}));
```

**Pattern 2: Input Validation**
```typescript
import { z } from 'zod';

const userSchema = z.object({
  email: z.string().email().max(255),
  name: z.string().min(2).max(100),
  age: z.number().int().min(18).max(120),
});

export async function createUser(req: Request) {
  try {
    const validatedData = userSchema.parse(req.body);
    // Process validated data
  } catch (error) {
    if (error instanceof z.ZodError) {
      return { status: 400, error: 'Validation failed', details: error.errors };
    }
  }
}
```

**Pattern 3: Rate Limiting**
```typescript
import rateLimit from 'express-rate-limit';

const apiLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // Limit each IP to 100 requests per window
  message: 'Too many requests, please try again later.',
  standardHeaders: true,
  legacyHeaders: false,
});

app.use('/api/', apiLimiter);
```

#### Best Practices
- **Never trust user input** - always validate and sanitize
- **Use parameterized queries** to prevent SQL injection
- **Store passwords hashed** with bcrypt or similar
- **Use HTTPS everywhere** in production
- **Implement CSRF protection** for state-changing operations
- **Set secure, httpOnly cookies** for session tokens
- **Use environment variables** for secrets, never commit them
- **Implement rate limiting** on all public endpoints
- **Set restrictive CORS policies** based on actual needs
- **Keep dependencies updated** and scan for vulnerabilities
- **Implement proper error handling** without exposing sensitive info
- **Use Content Security Policy** to prevent XSS attacks
- **Implement audit logging** for security-critical operations

---

### 10. accessibility-compliance-agent

#### Purpose
Expert in web accessibility standards (WCAG 2.1 AA), semantic HTML, ARIA attributes, and inclusive design. Ensures applications are usable by everyone, including people with disabilities.

#### Capabilities
- Audit sites for WCAG 2.1 AA compliance
- Implement semantic HTML structure
- Add appropriate ARIA attributes
- Ensure keyboard navigation
- Implement screen reader support
- Test with assistive technologies
- Fix color contrast issues
- Add skip links and landmarks
- Implement focus management
- Create accessible forms
- Test with accessibility tools (axe, WAVE)
- Document accessibility features
- Implement accessible data tables

#### Technologies
- **ARIA**: Accessible Rich Internet Applications
- **axe-core**: Accessibility testing
- **WAVE**: Web accessibility evaluation
- **Lighthouse**: Accessibility auditing
- **Screen Readers**: NVDA, JAWS, VoiceOver
- **Semantic HTML**: HTML5 elements
- **React**: Accessible component patterns

#### When to Use
- Conducting accessibility audits
- Ensuring WCAG compliance
- Testing with assistive technologies
- Fixing accessibility issues
- Creating accessible components
- Implementing keyboard navigation
- Testing forms for accessibility
- Preparing for accessibility certification

#### Example Commands
- `/audit-accessibility` - Comprehensive accessibility audit

#### Common Patterns

**Pattern 1: Semantic HTML Structure**
```jsx
<header>
  <nav aria-label="Main navigation">
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
  </nav>
</header>

<main>
  <article>
    <h1>Page Title</h1>
    <section aria-labelledby="intro-heading">
      <h2 id="intro-heading">Introduction</h2>
      <p>Content here...</p>
    </section>
  </article>
</main>

<footer>
  <p>&copy; 2025 Company Name</p>
</footer>
```

**Pattern 2: Accessible Form**
```jsx
<form onSubmit={handleSubmit} aria-labelledby="form-title">
  <h2 id="form-title">Contact Us</h2>

  <div className="mb-3">
    <label htmlFor="email" className="form-label">
      Email address
      <span className="required" aria-label="required">*</span>
    </label>
    <input
      type="email"
      id="email"
      className="form-control"
      required
      aria-required="true"
      aria-describedby="email-help"
      aria-invalid={errors.email ? 'true' : 'false'}
    />
    {errors.email && (
      <div id="email-error" className="invalid-feedback" role="alert">
        {errors.email}
      </div>
    )}
    <small id="email-help" className="form-text">
      We'll never share your email.
    </small>
  </div>

  <button
    type="submit"
    className="btn btn-primary"
    disabled={isSubmitting}
    aria-busy={isSubmitting ? 'true' : 'false'}
  >
    {isSubmitting ? 'Submitting...' : 'Submit'}
  </button>
</form>
```

**Pattern 3: Keyboard Navigation**
```jsx
function Modal({ isOpen, onClose, children }) {
  const modalRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    if (isOpen) {
      // Focus first focusable element
      const firstFocusable = modalRef.current?.querySelector(
        'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
      );
      (firstFocusable as HTMLElement)?.focus();

      // Trap focus within modal
      const handleTab = (e: KeyboardEvent) => {
        const focusableElements = modalRef.current?.querySelectorAll(
          'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
        );
        const firstElement = focusableElements?.[0] as HTMLElement;
        const lastElement = focusableElements?.[focusableElements.length - 1] as HTMLElement;

        if (e.key === 'Tab') {
          if (e.shiftKey && document.activeElement === firstElement) {
            lastElement?.focus();
            e.preventDefault();
          } else if (!e.shiftKey && document.activeElement === lastElement) {
            firstElement?.focus();
            e.preventDefault();
          }
        }
      };

      document.addEventListener('keydown', handleTab);
      return () => document.removeEventListener('keydown', handleTab);
    }
  }, [isOpen]);

  if (!isOpen) return null;

  return (
    <div
      ref={modalRef}
      role="dialog"
      aria-modal="true"
      aria-labelledby="modal-title"
    >
      <button onClick={onClose} aria-label="Close modal">×</button>
      {children}
    </div>
  );
}
```

#### Best Practices
- **Use semantic HTML** (header, nav, main, article, section, footer)
- **Provide text alternatives** for all non-text content (alt text)
- **Ensure sufficient color contrast** (4.5:1 for normal text, 3:1 for large text)
- **Make all functionality keyboard accessible** without requiring a mouse
- **Use ARIA attributes appropriately** (don't overuse)
- **Provide skip links** to main content
- **Use descriptive link text** (avoid "click here")
- **Mark up forms properly** with labels and error messages
- **Ensure focus indicators** are visible
- **Test with keyboard only** before shipping
- **Test with screen readers** (NVDA, JAWS, VoiceOver)
- **Use heading hierarchy** properly (h1, h2, h3)
- **Provide captions and transcripts** for media content

---

### 11. authentication-agent

#### Purpose
Expert in user authentication systems, authorization patterns, session management, and identity providers. Handles all aspects of user identity and access control.

#### Capabilities
- Implement email/password authentication
- Set up OAuth providers (Google, GitHub, Microsoft)
- Create JWT token generation and validation
- Implement session management strategies
- Build role-based access control (RBAC)
- Create password reset workflows
- Implement two-factor authentication
- Set up protected routes and middleware
- Build user profile management
- Implement refresh token patterns
- Create authentication context providers
- Set up SSO (Single Sign-On)
- Implement account verification flows

#### Technologies
- **NextAuth.js**: Next.js authentication
- **JWT**: JSON Web Tokens
- **bcrypt**: Password hashing
- **OAuth 2.0**: Third-party authentication
- **Express Session**: Session management
- **Passport.js**: Authentication middleware
- **Azure AD**: Enterprise authentication
- **Auth0**: Authentication platform

#### When to Use
- Implementing user registration and login
- Setting up OAuth providers
- Creating protected routes
- Implementing authorization logic
- Building user profile pages
- Setting up password reset
- Implementing SSO
- Creating multi-factor authentication

#### Example Commands
- `/add-auth` - Complete authentication system
- `/add-protected-route` - Creates protected pages
- `/add-social-login` - Adds OAuth providers

#### Common Patterns

**Pattern 1: NextAuth.js Configuration**
```typescript
import NextAuth from 'next-auth';
import GoogleProvider from 'next-auth/providers/google';
import CredentialsProvider from 'next-auth/providers/credentials';

export const authOptions = {
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
    CredentialsProvider({
      name: 'Credentials',
      credentials: {
        email: { label: 'Email', type: 'email' },
        password: { label: 'Password', type: 'password' },
      },
      async authorize(credentials) {
        const user = await validateUser(credentials.email, credentials.password);
        if (user) return user;
        return null;
      },
    }),
  ],
  callbacks: {
    async jwt({ token, user }) {
      if (user) {
        token.id = user.id;
        token.role = user.role;
      }
      return token;
    },
    async session({ session, token }) {
      session.user.id = token.id;
      session.user.role = token.role;
      return session;
    },
  },
  pages: {
    signIn: '/auth/signin',
    error: '/auth/error',
  },
};

export default NextAuth(authOptions);
```

**Pattern 2: Protected Route Middleware**
```typescript
import { NextRequest, NextResponse } from 'next/server';
import { getToken } from 'next-auth/jwt';

export async function middleware(req: NextRequest) {
  const token = await getToken({ req, secret: process.env.NEXTAUTH_SECRET });

  // Require authentication for /dashboard routes
  if (req.nextUrl.pathname.startsWith('/dashboard')) {
    if (!token) {
      return NextResponse.redirect(new URL('/auth/signin', req.url));
    }
  }

  // Require admin role for /admin routes
  if (req.nextUrl.pathname.startsWith('/admin')) {
    if (!token || token.role !== 'admin') {
      return NextResponse.redirect(new URL('/unauthorized', req.url));
    }
  }

  return NextResponse.next();
}

export const config = {
  matcher: ['/dashboard/:path*', '/admin/:path*'],
};
```

**Pattern 3: Authentication Context**
```typescript
'use client';
import { createContext, useContext, ReactNode } from 'react';
import { useSession } from 'next-auth/react';

interface AuthContextType {
  user: User | null;
  isAuthenticated: boolean;
  isLoading: boolean;
}

const AuthContext = createContext<AuthContextType | undefined>(undefined);

export function AuthProvider({ children }: { children: ReactNode }) {
  const { data: session, status } = useSession();

  const value = {
    user: session?.user ?? null,
    isAuthenticated: !!session,
    isLoading: status === 'loading',
  };

  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}

export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within AuthProvider');
  }
  return context;
}
```

#### Best Practices
- **Never store passwords in plain text** - always hash with bcrypt
- **Use HTTPS everywhere** for authentication
- **Implement secure session management** with httpOnly cookies
- **Use CSRF tokens** for authentication forms
- **Implement rate limiting** on login endpoints
- **Set session timeouts** appropriately
- **Implement refresh tokens** for long-lived sessions
- **Use OAuth for social login** when possible
- **Implement account lockout** after failed login attempts
- **Provide password strength requirements** and validation
- **Implement email verification** for new accounts
- **Use secure password reset** flows with time-limited tokens
- **Log authentication events** for security monitoring
- **Implement multi-factor authentication** for sensitive operations

---

## Agent Interaction Patterns

### Collaborative Workflows

#### Scenario 1: Building a Complete Feature (E-commerce Product Page)

```
1. content-seo-agent
   - Sets up metadata and structured data
   - Implements Open Graph tags
   - Creates sitemap entry

2. frontend-development-agent
   - Builds product detail component
   - Creates image gallery
   - Implements responsive layout

3. azure-serverless-agent OR devops-railway-agent
   - Creates product API endpoints
   - Implements database queries
   - Sets up caching

4. accessibility-compliance-agent
   - Audits component for WCAG compliance
   - Fixes keyboard navigation
   - Tests with screen readers

5. testing-quality-agent
   - Creates unit tests for components
   - Implements E2E test for purchase flow
   - Sets up visual regression tests
```

#### Scenario 2: Deploying to Production

```
1. testing-quality-agent
   - Runs full test suite
   - Verifies test coverage
   - Checks for failing tests

2. security-production-agent
   - Conducts security audit
   - Scans dependencies
   - Validates security headers

3. accessibility-compliance-agent
   - Runs accessibility audit
   - Verifies WCAG compliance
   - Tests with assistive tech

4. devops-azure-agent OR devops-railway-agent
   - Deploys to staging
   - Runs smoke tests
   - Deploys to production

5. monitoring-observability-agent
   - Verifies monitoring active
   - Sets up production alerts
   - Monitors deployment health
```

### Multi-Agent Decision Tree

```
User Request → Analyze Requirements
              ↓
    Is it primarily frontend?
              ↓
         Yes → frontend-development-agent (primary)
              + accessibility-compliance-agent (review)
              + testing-quality-agent (testing)
              ↓
    Is it primarily backend?
              ↓
         Yes → Platform check:
              Azure → azure-serverless-agent
              Railway → (use devops-railway-agent patterns)
              + security-production-agent (review)
              + testing-quality-agent (testing)
              ↓
    Is it deployment/infrastructure?
              ↓
         Yes → Platform check:
              Azure → devops-azure-agent
              Railway → devops-railway-agent
              + monitoring-observability-agent (post-deploy)
              ↓
    Is it authentication/authorization?
              ↓
         Yes → authentication-agent (primary)
              + security-production-agent (review)
              + testing-quality-agent (testing)
```

---

## Troubleshooting

### When Agents Disagree

**Problem**: Multiple agents suggest different approaches

**Solution**:
1. Identify the primary agent based on domain expertise
2. Use other agents as reviewers/validators
3. Consider platform-specific requirements (Azure vs Railway)
4. Follow the agent hierarchy: security > accessibility > functionality

### Agent Not Responding as Expected

**Problem**: Agent produces unexpected output or doesn't understand context

**Solutions**:
1. Provide more specific context about the project
2. Reference exact command that should be executed
3. Specify platform (Azure or Railway) explicitly
4. Break complex requests into smaller, focused tasks
5. Check if the agent has necessary project context

### Cross-Agent Dependencies

**Problem**: One agent needs output from another

**Solution**: Execute agents sequentially:
```
1. First agent completes its task
2. Verify output is correct
3. Provide output as context to second agent
4. Second agent uses previous output for its work
```

**Example**:
```
1. azure-serverless-agent creates API endpoint
2. frontend-development-agent uses API endpoint URL
3. testing-quality-agent tests integration
```

---

## Quick Reference

### Agent Selection Cheat Sheet

| Task Type | Primary Agent | Supporting Agents |
|-----------|--------------|-------------------|
| React component | frontend-development-agent | accessibility-compliance-agent |
| Form with validation | forms-workflow-agent | frontend-development-agent |
| SEO optimization | content-seo-agent | frontend-development-agent |
| Azure Function API | azure-serverless-agent | security-production-agent |
| Railway API | devops-railway-agent | security-production-agent |
| Authentication | authentication-agent | security-production-agent |
| Deploy to Azure | devops-azure-agent | monitoring-observability-agent |
| Deploy to Railway | devops-railway-agent | monitoring-observability-agent |
| Unit/Integration tests | testing-quality-agent | - |
| E2E tests | testing-quality-agent | - |
| Security audit | security-production-agent | - |
| Accessibility audit | accessibility-compliance-agent | - |
| Monitoring setup | monitoring-observability-agent | - |

### Common Multi-Agent Workflows

**1. New Page Development**
```
frontend-development-agent → content-seo-agent → accessibility-compliance-agent → testing-quality-agent
```

**2. API Development**
```
azure-serverless-agent/devops-railway-agent → security-production-agent → testing-quality-agent
```

**3. Feature Launch**
```
[feature agents] → testing-quality-agent → security-production-agent → accessibility-compliance-agent → devops-*-agent → monitoring-observability-agent
```

**4. Security Hardening**
```
security-production-agent → authentication-agent → devops-*-agent (redeploy)
```

---

## Best Practices

### General Agent Usage

1. **Start with the most specialized agent** for your task
2. **Provide clear, specific instructions** with exact requirements
3. **Include platform information** (Azure or Railway) when relevant
4. **Break complex tasks into smaller steps** handled by appropriate agents
5. **Verify each agent's output** before moving to the next step
6. **Use supporting agents for review** (security, accessibility, testing)
7. **Document agent decisions** and rationales for future reference

### Platform-Specific Considerations

**Azure Development**:
- Use `azure-serverless-agent` for all backend API work
- Use `devops-azure-agent` for deployment and infrastructure
- Remember cold start considerations for Azure Functions
- Leverage Application Insights for monitoring

**Railway Development**:
- Use `devops-railway-agent` for backend and deployment
- Leverage PostgreSQL with Prisma for data
- Use Railway's built-in monitoring
- Take advantage of no cold starts

### Quality Assurance Flow

Always involve these agents before production:
1. `testing-quality-agent` - Ensure tests pass
2. `security-production-agent` - Security audit
3. `accessibility-compliance-agent` - Accessibility check
4. `monitoring-observability-agent` - Monitoring setup

---

## Conclusion

The 11-agent architecture provides specialized expertise for every aspect of modern full-stack development. By understanding each agent's strengths and using them collaboratively, you can build production-ready applications efficiently while maintaining high quality standards.

**Key Takeaways**:
- Each agent is a domain expert with specific capabilities
- Agents work independently or collaboratively as needed
- Platform-specific agents handle Azure and Railway differences
- Always involve quality agents (testing, security, accessibility) before production
- Break complex tasks into agent-specific subtasks for best results
