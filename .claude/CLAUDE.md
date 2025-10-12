# Full-Stack Website Builder Plugin - Architecture

## Plugin Overview

### Purpose and Goals
This plugin provides a comprehensive toolkit for building, deploying, and maintaining production-ready Next.js websites with integrated backend infrastructure. It streamlines the entire development lifecycle from initial scaffolding to production deployment.

**Key Goals:**
- Accelerate full-stack web development with pre-configured patterns
- Provide platform-specific guidance for Azure and Railway deployments
- Ensure production-ready code with built-in best practices
- Reduce decision fatigue through opinionated architecture
- Maintain consistency across frontend, backend, and infrastructure

### Target Audience
Professional developers and teams building modern web applications who need:
- Next.js 15 + TypeScript + Bootstrap projects
- Backend API integration (Azure Functions or Express.js)
- Database persistence (Azure Table Storage or PostgreSQL)
- Production deployment automation
- Testing and quality assurance workflows

### Key Differentiator
**Platform-Specific Guidance**: Unlike generic web development tools, this plugin provides tailored implementations for both Azure and Railway platforms, allowing developers to choose the best fit for their needs:

- **Azure Path**: Enterprise-grade serverless architecture with Azure Static Web Apps, Azure Functions, and Azure Table Storage
- **Railway Path**: Rapid full-stack development with Express.js, PostgreSQL, and simplified deployment

Each path includes platform-specific commands, deployment workflows, and best practices.

## Directory Structure

```
.claude-plugin/          - Plugin manifests and metadata
  ├── plugin.json        - Core plugin configuration
  └── marketplace.json   - Marketplace listing information

.claude/
  ├── agents/           - 11 specialized AI agents
  │   ├── frontend-development-agent.md
  │   ├── azure-serverless-agent.md
  │   ├── devops-azure-agent.md
  │   ├── devops-railway-agent.md
  │   ├── forms-workflow-agent.md
  │   ├── content-seo-agent.md
  │   ├── authentication-agent.md
  │   ├── monitoring-observability-agent.md
  │   ├── testing-quality-agent.md
  │   ├── security-production-agent.md
  │   └── accessibility-compliance-agent.md
  │
  └── commands/         - 75 slash commands organized by function
      ├── scaffold-*.md
      ├── add-*.md
      ├── deploy-*.md
      └── [other commands]

docs/                   - Plugin documentation
examples/               - Example projects and templates
```

## Agent Architecture

### Agent Categories

#### 1. Frontend Development
**frontend-development-agent**
- React component development with TypeScript
- Bootstrap 5 responsive design implementation
- Component architecture and reusable patterns
- Accessibility and WCAG compliance
- Performance optimization and code splitting
- Mobile-first development approach

**forms-workflow-agent**
- Complex form creation and validation
- Multi-step form workflows
- File upload handling
- Form state management
- Error handling and user feedback

**content-seo-agent**
- SEO optimization and metadata management
- Content structure and hierarchy
- Schema.org markup implementation
- Social media meta tags
- Sitemap and robots.txt generation

#### 2. Backend & Infrastructure

**azure-serverless-agent**
- Azure Functions v4 development (TypeScript/Node.js)
- Azure Table Storage operations and schema design
- Azure Static Web Apps configuration
- Application Insights integration
- Serverless best practices and cold start optimization

**devops-azure-agent**
- GitHub Actions CI/CD pipelines for Azure
- Azure deployment automation
- Environment management (dev, staging, production)
- Azure CLI operations
- Infrastructure as code patterns

**devops-railway-agent**
- Railway platform deployment workflows
- Multi-environment setup (staging/production)
- PostgreSQL and Redis provisioning
- Railway CLI operations
- Custom domain and SSL configuration

#### 3. Quality & Operations

**authentication-agent**
- User authentication flows
- JWT token management
- OAuth provider integration
- Role-based access control
- Session management

**monitoring-observability-agent**
- Application monitoring setup
- Log aggregation and analysis
- Performance metrics tracking
- Error tracking and alerting
- Health check implementations

**testing-quality-agent**
- Unit testing with Jest
- Integration testing patterns
- E2E testing with Playwright
- Test coverage analysis
- CI/CD test integration

**security-production-agent**
- Security best practices implementation
- Input validation and sanitization
- CORS and CSP configuration
- Secret management
- Security header configuration

**accessibility-compliance-agent**
- WCAG 2.1 AA compliance
- ARIA attributes and semantic HTML
- Keyboard navigation
- Screen reader optimization
- Accessibility testing automation

**code-review-agent** (NEW)
- Automated code review and quality analysis
- 10 comprehensive review categories
- Security vulnerability detection
- Performance bottleneck identification
- Platform-specific validations (Azure/Railway)
- Severity-based issue classification
- Pre-deployment quality gates

### Agent Interaction Patterns

#### Single Agent Workflows
Use a single agent when the task is clearly within one domain:
- Adding a new React component → frontend-development-agent
- Creating an Azure Function → azure-serverless-agent
- Setting up CI/CD → devops-azure-agent or devops-railway-agent

#### Multi-Agent Collaboration
Complex features often require multiple agents working together:

**Example: E-commerce Checkout Flow**
1. forms-workflow-agent → Creates multi-step checkout form
2. frontend-development-agent → Builds responsive UI components
3. azure-serverless-agent → Implements payment processing API
4. security-production-agent → Adds input validation and security
5. testing-quality-agent → Creates comprehensive test suite

**Example: Protected Admin Dashboard**
1. authentication-agent → Implements login and auth flow
2. frontend-development-agent → Builds dashboard components
3. azure-serverless-agent → Creates admin API endpoints
4. accessibility-compliance-agent → Ensures WCAG compliance
5. monitoring-observability-agent → Adds logging and metrics
6. code-review-agent → Reviews complete implementation before deployment

### When to Use Each Agent

| Task | Primary Agent | Supporting Agents |
|------|--------------|-------------------|
| New page/component | frontend-development-agent | accessibility-compliance-agent |
| API endpoint | azure-serverless-agent OR devops-railway-agent | security-production-agent |
| Form with validation | forms-workflow-agent | frontend-development-agent |
| Authentication | authentication-agent | security-production-agent |
| Deployment setup | devops-azure-agent OR devops-railway-agent | monitoring-observability-agent |
| Performance issues | frontend-development-agent | monitoring-observability-agent |
| SEO optimization | content-seo-agent | frontend-development-agent |
| Test coverage | testing-quality-agent | All relevant agents |

## Command Architecture

### Command Categories (10 primary categories, 81 total commands)

#### Scaffolding (6 commands)
- `/scaffold-nextjs` - Basic Next.js project
- `/scaffold-azure-nextjs` - Next.js optimized for Azure
- `/scaffold-azure-functions` - Azure Functions API
- `/scaffold-azure-full` - Complete Azure stack
- `/scaffold-railway-nextjs` - Next.js optimized for Railway
- `/scaffold-railway-full` - Complete Railway stack

#### Add Features (52 commands)
**Components & UI**
- `/add-component` - React component
- `/add-page` - New page with routing
- `/add-layout` - Layout component
- `/add-modal` - Modal dialog
- `/add-navigation` - Navigation system

**APIs & Backend**
- `/add-api-azure` - Azure Function endpoint
- `/add-api-railway` - Express.js endpoint
- `/add-database-azure` - Azure Table Storage
- `/add-database-railway` - PostgreSQL with Prisma
- `/add-caching` - Redis caching layer

**Forms & Data**
- `/add-form` - Form with validation
- `/add-form-multi-step` - Multi-step form
- `/add-file-upload` - File upload handling
- `/add-search` - Search functionality

**Integration & Services**
- `/add-auth` - Authentication system
- `/add-email-azure` - Email service (Azure)
- `/add-email-railway` - Email service (Railway)
- `/add-payment` - Payment processing
- `/add-analytics-google` - Google Analytics
- `/add-analytics-plausible` - Plausible Analytics

**Content & Media**
- `/add-cms-ui` - CMS interface
- `/add-content-json` - JSON content management
- `/add-image-optimization` - Image optimization
- `/add-markdown-support` - Markdown rendering

**Features**
- `/add-admin-panel` - Admin dashboard
- `/add-dashboard` - User dashboard
- `/add-checkout` - E-commerce checkout
- `/add-subscription` - Subscription management
- `/add-notifications` - Push notifications
- `/add-chat` - Real-time chat
- `/add-calendar` - Calendar component
- `/add-maps` - Map integration
- `/add-charts` - Data visualization
- `/add-pdf-generator` - PDF generation

**Jobs & Automation**
- `/add-background-job` - Background processing
- `/add-cron-azure` - Scheduled jobs (Azure)
- `/add-cron-railway` - Scheduled jobs (Railway)
- `/add-queue` - Job queue system

#### Deployment (4 commands)
- `/deploy-azure-staging` - Deploy to Azure staging
- `/deploy-azure-production` - Deploy to Azure production
- `/deploy-railway-staging` - Deploy to Railway staging
- `/deploy-railway-production` - Deploy to Railway production

#### Testing (3 commands via add-*)
- `/add-e2e-test` - E2E test suite
- `/add-integration-test` - Integration tests
- `/add-unit-test` - Unit tests

#### Configuration (2 commands)
- `/setup-environment` - Environment configuration
- `/setup-monitoring` - Monitoring setup

#### Optimization (3 commands)
- `/optimize-performance` - Performance optimization
- `/optimize-seo` - SEO optimization
- `/optimize-bundle` - Bundle size optimization

#### Auditing (2 commands)
- `/audit-security` - Security audit
- `/audit-accessibility` - Accessibility audit

#### Migration (3 commands)
- `/migrate-to-azure` - Migrate project to Azure
- `/migrate-to-railway` - Migrate project to Railway
- `/migrate-database` - Database migration

#### Generation (2 commands)
- `/generate-types` - TypeScript types
- `/generate-docs` - Documentation

#### Code Review (6 commands)
- `/review-code` - Review uncommitted changes
- `/review-component` - Review React component
- `/review-api` - Review API endpoint
- `/review-security` - Security audit
- `/review-performance` - Performance analysis
- `/review-before-deploy` - Pre-deployment gate

### Command Naming Convention

**Pattern Structure:**
```
/{verb}-{feature}-{platform}
```

**Platform-Specific Commands:**
- Always include platform suffix when behavior differs: `-azure` or `-railway`
- Example: `/add-api-azure` vs `/add-api-railway`

**Generic Commands:**
- No platform suffix when implementation is platform-agnostic
- Example: `/add-component`, `/add-form`

**Verb Categories:**
- `scaffold-*`: Create new projects or major structures
- `add-*`: Add features, components, or functionality
- `deploy-*`: Deployment operations
- `setup-*`: Configuration and initialization
- `optimize-*`: Performance and optimization
- `audit-*`: Analysis and reporting
- `migrate-*`: Migration operations
- `generate-*`: Code generation

### Command Design Principles

Each command follows these principles:

1. **Concise Prompts**: Under 150 words, focused on deliverables
2. **Agent References**: Commands work with appropriate agents
3. **Technology Specificity**: Exact versions and technologies specified
4. **Clear Deliverables**: Explicit list of what will be created
5. **Best Practices**: Built-in security, performance, and quality patterns
6. **Platform Awareness**: Azure or Railway specific when needed

**Example Command Structure:**
```markdown
Create a new Azure Function HTTP endpoint with full integration.

Generate:
- Azure Function in /api with TypeScript (HTTP trigger)
- Input validation using Zod or similar validation library
- Comprehensive error handling with proper HTTP status codes
- CORS configuration in function.json
- Azure Table Storage integration for data persistence
- Request/response TypeScript interfaces
- API client code in Next.js (/lib/api) for calling the endpoint
- Environment variable configuration
- Example usage in a Next.js component
- JSDoc comments and inline documentation

Include proper logging, security headers, and follow Azure Functions best practices.
```

## Technology Stack

### Core Technologies
- **Next.js**: 15.x with App Router
- **React**: 18+ with functional components
- **TypeScript**: 5.x with strict mode
- **Bootstrap**: 5.3+ for responsive UI
- **Node.js**: 20+ LTS runtime

### Azure Stack
**Frontend Hosting:**
- Azure Static Web Apps (Next.js deployment)

**Backend & APIs:**
- Azure Functions v4 (TypeScript/Node.js)
- HTTP triggers with custom routing

**Data Storage:**
- Azure Table Storage (NoSQL)
- PartitionKey/RowKey schema design

**Monitoring:**
- Application Insights
- Structured logging

**CI/CD:**
- GitHub Actions
- Azure CLI automation

### Railway Stack
**Full-Stack Hosting:**
- Railway platform (unified deployment)

**Backend APIs:**
- Express.js with TypeScript
- RESTful API design

**Data Storage:**
- PostgreSQL with Prisma ORM
- Redis for caching

**Monitoring:**
- Railway logs
- Winston logging

**Deployment:**
- Railway CLI
- Git-based deployments

## Workflow Patterns

### Pattern 1: Scaffolding New Project

#### Azure Path
```
1. /scaffold-azure-full
   → Creates Next.js + Azure Functions + Table Storage project
   → Generates GitHub Actions workflow
   → Sets up Application Insights

2. /setup-environment
   → Configures dev, staging, production environments
   → Sets up environment variables
   → Creates staticwebapp.config.json

3. /add-component (for needed UI components)
   → Builds responsive components with Bootstrap

4. /add-api-azure (for each API endpoint)
   → Creates Azure Functions with proper structure

5. /deploy-azure-staging
   → Deploys to staging environment
   → Runs tests automatically
   → Verifies deployment

6. /deploy-azure-production
   → Deploys to production after staging validation
```

#### Railway Path
```
1. /scaffold-railway-full
   → Creates Next.js + Express.js + PostgreSQL project
   → Generates Railway configuration
   → Sets up Prisma ORM

2. /setup-environment
   → Configures staging/production on Railway
   → Sets up environment variables per environment

3. /add-component (for needed UI components)
   → Builds responsive components

4. /add-api-railway (for each API endpoint)
   → Creates Express.js routes with validation

5. /deploy-railway-staging
   → Deploys to Railway staging environment

6. /deploy-railway-production
   → Promotes staging to production
```

### Pattern 2: Adding Features

**Simple Feature (Contact Form):**
```
1. /add-form
   → Creates form component with validation
   → Implements error handling
   → Adds loading states

2. /add-api-azure OR /add-api-railway
   → Creates API endpoint for form submission
   → Adds email sending or data persistence

3. /add-unit-test
   → Tests form validation
   → Tests API endpoint
```

**Complex Feature (E-commerce Checkout):**
```
1. /add-checkout
   → Multi-step checkout flow
   → Cart management
   → Order summary

2. /add-payment
   → Payment provider integration
   → Secure payment handling

3. /add-database-azure OR /add-database-railway
   → Order storage schema
   → CRUD operations

4. /add-email-azure OR /add-email-railway
   → Order confirmation emails
   → Receipt generation

5. /add-e2e-test
   → Complete checkout flow testing

6. /audit-security
   → Security review of payment flow
```

### Pattern 3: Deploying to Staging/Production

**Staging Deployment:**
```
1. Commit all changes to feature branch

2. /deploy-azure-staging OR /deploy-railway-staging
   → Automated deployment to staging
   → Runs test suite
   → Verifies health checks

3. Manual validation in staging environment
   → Test all features
   → Verify integrations
   → Check performance

4. Monitor staging logs for issues
```

**Production Deployment:**
```
1. Merge to main branch

2. /review-before-deploy (MANDATORY)
   → Comprehensive pre-deployment review
   → All critical and high severity issues must be addressed

3. /audit-security (optional but recommended)
   → Security scan before production

4. /audit-accessibility (optional but recommended)
   → Accessibility check

5. /deploy-azure-production OR /deploy-railway-production
   → Automated production deployment
   → Blue-green or canary deployment
   → Automatic rollback on failure
   → Includes automated quality gate check

6. Post-deployment verification
   → Health check validation
   → Smoke tests
   → Monitor metrics

7. /setup-monitoring (if not already configured)
   → Production monitoring alerts
```

### Pattern 4: Testing and Quality

**Test-Driven Development:**
```
1. /add-unit-test
   → Create tests first
   → Test business logic

2. Implement feature with tests passing

3. /add-integration-test
   → Test API integration
   → Test database operations

4. /add-e2e-test
   → Test complete user flows
   → Test across browsers

5. /audit-accessibility
   → Ensure WCAG compliance

6. /optimize-performance
   → Performance benchmarks
```

## Best Practices

### When to Use Azure vs Railway

#### Choose Azure When:
- Building enterprise applications with Microsoft ecosystem
- Need serverless architecture with automatic scaling
- Require Azure-specific services (Active Directory, Cosmos DB, etc.)
- Compliance requirements favor Microsoft Azure
- Team has Azure expertise
- Budget allows for consumption-based pricing

**Azure Advantages:**
- Enterprise-grade SLAs
- Global CDN with Azure Static Web Apps
- Tight integration with Microsoft services
- Powerful monitoring with Application Insights
- Serverless auto-scaling

**Azure Considerations:**
- More complex setup and configuration
- Cold starts with Azure Functions
- Learning curve for Azure-specific services

#### Choose Railway When:
- Rapid development and iteration needed
- Prefer traditional server architecture over serverless
- Want simpler deployment workflow
- Need PostgreSQL with full ORM support
- Budget-conscious (predictable pricing)
- Smaller team or solo developer

**Railway Advantages:**
- Extremely simple deployment
- Unified platform (web + API + DB)
- No cold starts
- Excellent developer experience
- Built-in staging environments

**Railway Considerations:**
- Smaller scale than Azure
- Fewer regions available
- Less enterprise features

### Command Sequencing

**Recommended Order for New Projects:**

1. **Foundation** (Day 1)
   - `/scaffold-azure-full` OR `/scaffold-railway-full`
   - `/setup-environment`
   - `/add-navigation`

2. **Core Pages** (Day 1-2)
   - `/add-page` (for each main page)
   - `/add-component` (shared components)
   - `/add-layout` (page layouts)

3. **Data & APIs** (Day 2-3)
   - `/add-database-azure` OR `/add-database-railway`
   - `/add-api-azure` OR `/add-api-railway` (for each endpoint)
   - `/add-caching` (if needed)

4. **Features** (Day 3-5)
   - `/add-form` (contact, signup, etc.)
   - `/add-auth` (if needed)
   - Feature-specific commands as needed

5. **Integration** (Day 5-6)
   - `/add-email-azure` OR `/add-email-railway`
   - `/add-analytics-google` OR `/add-analytics-plausible`
   - `/add-monitoring`

6. **Quality** (Day 6-7)
   - `/add-unit-test`
   - `/add-e2e-test`
   - `/audit-accessibility`
   - `/audit-security`

7. **Optimization** (Day 7)
   - `/optimize-performance`
   - `/optimize-seo`
   - `/optimize-bundle`

8. **Deployment** (Day 7-8)
   - `/deploy-azure-staging` OR `/deploy-railway-staging`
   - Validate staging
   - `/deploy-azure-production` OR `/deploy-railway-production`

### Agent Selection

**Decision Tree:**

```
Is it frontend-related?
├─ Yes → Is it a form?
│  ├─ Yes → forms-workflow-agent
│  └─ No → Is it about SEO/content?
│     ├─ Yes → content-seo-agent
│     └─ No → frontend-development-agent
│
└─ No → Is it backend/API?
   ├─ Yes → Which platform?
   │  ├─ Azure → azure-serverless-agent
   │  └─ Railway → devops-railway-agent
   │
   └─ No → Is it about deployment?
      ├─ Yes → Which platform?
      │  ├─ Azure → devops-azure-agent
      │  └─ Railway → devops-railway-agent
      │
      └─ No → Is it about quality/testing?
         ├─ Testing → testing-quality-agent
         ├─ Security → security-production-agent
         ├─ Accessibility → accessibility-compliance-agent
         ├─ Auth → authentication-agent
         └─ Monitoring → monitoring-observability-agent
```

### Platform Consistency

**Maintaining Consistency Across Platforms:**

1. **Shared Frontend Code**
   - Use identical Next.js setup for both platforms
   - Same component library and patterns
   - Platform-agnostic API client layer

2. **Environment Variables**
   - Use `.env.example` for documentation
   - Platform-specific variables named consistently
   - Never commit secrets to repository

3. **API Contracts**
   - Identical request/response shapes
   - Same validation rules
   - Consistent error formats

4. **Testing**
   - Same test suites for frontend
   - Platform-specific integration tests
   - Shared E2E test scenarios

## Common Patterns

### Multi-step Workflows

#### Scaffold → Develop → Test → Deploy
```
1. Scaffold: /scaffold-azure-full
   Creates complete project structure

2. Develop: /add-page, /add-api-azure, /add-form
   Build features incrementally

3. Test: /add-unit-test, /add-e2e-test
   Ensure quality

4. Deploy: /deploy-azure-staging → validate → /deploy-azure-production
   Ship to production
```

#### Add Feature → Add Tests → Deploy to Staging → Deploy to Production
```
1. Feature: /add-dashboard
   Build new dashboard feature

2. Tests: /add-integration-test
   Test the dashboard

3. Staging: /deploy-azure-staging
   Deploy to staging environment

4. Validation: Manual testing in staging

5. Production: /deploy-azure-production
   Deploy to production after validation
```

### Cross-agent Collaboration

#### Example: Building an Admin Panel

**Agents Involved:**
1. frontend-development-agent
2. authentication-agent
3. azure-serverless-agent
4. security-production-agent
5. accessibility-compliance-agent

**Workflow:**
```
1. /add-admin-panel
   → Invokes: frontend-development-agent
   → Creates: Admin UI components with Bootstrap

2. /add-auth
   → Invokes: authentication-agent
   → Creates: Login flow, JWT handling, protected routes

3. /add-api-azure (for admin endpoints)
   → Invokes: azure-serverless-agent
   → Creates: Admin API endpoints with authorization

4. Security Review
   → Invokes: security-production-agent
   → Reviews: Input validation, CORS, auth flow

5. Accessibility Check
   → Invokes: accessibility-compliance-agent
   → Ensures: WCAG compliance, keyboard navigation
```

#### Example: E-commerce Product Catalog

**Agents Involved:**
1. frontend-development-agent
2. content-seo-agent
3. azure-serverless-agent
4. monitoring-observability-agent

**Workflow:**
```
1. /add-page (product listing)
   → Invokes: frontend-development-agent
   → Creates: Product grid, filters, sorting

2. /add-page (product detail)
   → Invokes: frontend-development-agent + content-seo-agent
   → Creates: Product detail page with rich SEO metadata

3. /add-api-azure (product endpoints)
   → Invokes: azure-serverless-agent
   → Creates: Product CRUD APIs

4. /add-database-azure
   → Invokes: azure-serverless-agent
   → Creates: Product schema in Table Storage

5. /setup-monitoring
   → Invokes: monitoring-observability-agent
   → Creates: Performance tracking, error logging
```

### Error Handling

#### When Agents Encounter Errors

**Pattern 1: Missing Dependencies**
```
Error: Cannot find module 'zod'

Recovery:
1. Agent reports missing dependency
2. Agent suggests: npm install zod
3. Agent provides fallback validation approach
4. User installs dependency
5. Agent retries operation
```

**Pattern 2: Platform Mismatch**
```
Error: Trying to use /add-api-azure on Railway project

Recovery:
1. Agent detects platform from project structure
2. Agent suggests: /add-api-railway instead
3. Agent explains difference
4. User confirms or cancels
```

**Pattern 3: Configuration Missing**
```
Error: Azure credentials not configured

Recovery:
1. Agent detects missing configuration
2. Agent provides setup instructions
3. Agent suggests: /setup-environment
4. User completes setup
5. Agent retries deployment
```

## Extension Points

### Adding New Commands

**To add a new command:**

1. Create file in `.claude/commands/` with pattern: `{verb}-{feature}-{platform}.md`

2. Follow command template:
```markdown
# Command Title (under 10 words)

Brief description of what this command does (1-2 sentences).

Generate:
- Bulleted list of deliverables
- Specific files that will be created
- Technologies used with versions
- Integration points

Include best practices for [security/performance/accessibility].
Reference {agent-name} for detailed implementation.
```

3. Register in plugin.json (if using registry)

4. Test command with various project types

**Example New Command:**
```markdown
# Add WebSocket Real-time Chat

Create a real-time chat feature with WebSocket support.

Generate:
- Chat component in /src/components/Chat
- WebSocket server endpoint (Azure Functions or Express.js)
- Message persistence in database
- Typing indicators and presence
- Message history loading
- File/image sharing support
- Responsive mobile and desktop layouts
- E2E tests for chat functionality

Use Socket.io for WebSocket implementation. Reference frontend-development-agent
for UI and azure-serverless-agent or devops-railway-agent for backend.
```

### Creating New Agents

**Guidelines for new agent creation:**

1. **Identify Clear Domain**: Agent should have specific expertise area

2. **Define Core Capabilities**: List 5-8 main capabilities

3. **Provide Technical Specifications**: Include:
   - Technology stack
   - File structure patterns
   - Code templates
   - Configuration examples

4. **Document Best Practices**: Include:
   - Common patterns
   - Anti-patterns to avoid
   - Performance considerations
   - Security guidelines

5. **Create Agent File**: Place in `.claude/agents/{agent-name}.md`

**Example New Agent Structure:**
```markdown
# Agent Name

## Purpose
Clear statement of agent's role and expertise.

## Core Capabilities
### 1. Capability Name
- Bullet points of what agent can do
- Specific tasks and responsibilities

### 2. Another Capability
- More specific capabilities

## Technical Specifications
### Technology Stack
- List exact technologies with versions

### File Structure Pattern
```
project/
├── structure/
└── examples/
```

## Best Practices
### Pattern Templates
```code
// Example implementation
```

### Common Pitfalls
- Things to avoid
- Known issues

## Reference Resources
- Links to documentation
```

### Platform Support

**To add support for new platforms (Vercel, AWS, GCP):**

1. **Create Platform Agent**:
   - File: `.claude/agents/devops-{platform}-agent.md`
   - Document platform-specific deployment patterns
   - Include CLI commands and workflows

2. **Add Scaffold Commands**:
   - `/scaffold-{platform}-nextjs`
   - `/scaffold-{platform}-full`

3. **Add Platform-Specific Commands**:
   - `/add-api-{platform}`
   - `/add-database-{platform}`
   - `/add-cron-{platform}`
   - `/add-email-{platform}`

4. **Create Deployment Commands**:
   - `/deploy-{platform}-staging`
   - `/deploy-{platform}-production`

5. **Update Technology Stack Section** in this file

6. **Update Best Practices** with platform comparison

**Example: Adding Vercel Support**

```
1. Create: .claude/agents/devops-vercel-agent.md
2. Create: .claude/commands/scaffold-vercel-nextjs.md
3. Create: .claude/commands/add-api-vercel.md (Serverless Functions)
4. Create: .claude/commands/add-database-vercel.md (Vercel Postgres)
5. Create: .claude/commands/deploy-vercel-staging.md
6. Create: .claude/commands/deploy-vercel-production.md
7. Update: CLAUDE.md with Vercel comparison
```

## Troubleshooting

### Command Not Found

**Causes:**
1. Typo in command name
2. Command doesn't exist
3. Plugin not properly installed

**Solutions:**
```
1. List all commands: Type "/" in Claude Code to see available commands
2. Check command name: Review .claude/commands/ directory
3. Verify plugin: Check .claude-plugin/plugin.json exists
4. Reinstall plugin: Follow installation instructions
```

### Agent Confusion

**When agents conflict:**

**Scenario: Frontend agent trying to create Azure Functions**
```
Problem: User asks frontend-development-agent to create an API

Solution:
1. Frontend agent recognizes backend task
2. Agent suggests: "This requires azure-serverless-agent"
3. Agent hands off to correct agent
4. User confirms and task continues
```

**Scenario: Multiple agents needed**
```
Problem: Complex task spans multiple domains

Solution:
1. Primary agent identifies collaborating agents needed
2. Agents work sequentially or in parallel
3. Each agent contributes their expertise
4. Final integration by coordinating agent
```

### Platform-specific Issues

#### Common Azure Pitfalls

**Issue: Cold Starts**
```
Problem: Azure Functions slow to respond initially

Solutions:
- Enable Premium plan or Always On
- Minimize dependencies
- Implement warming triggers
- Use connection pooling
```

**Issue: CORS Errors**
```
Problem: Frontend can't call Azure Functions

Solutions:
- Configure CORS in function.json
- Set in staticwebapp.config.json
- Verify allowed origins
- Check preflight requests
```

**Issue: Environment Variables Not Found**
```
Problem: process.env.VAR_NAME undefined in production

Solutions:
- Set in Azure Portal > Configuration
- Add to GitHub Actions secrets
- Update staticwebapp.config.json
- Check environment spelling
```

#### Common Railway Pitfalls

**Issue: Build Failures**
```
Problem: Railway build fails

Solutions:
- Check buildCommand in railway.toml
- Verify Node.js version compatibility
- Review build logs: railway logs --build
- Clear build cache via dashboard
```

**Issue: Database Connection Timeouts**
```
Problem: Cannot connect to PostgreSQL

Solutions:
- Verify DATABASE_URL environment variable
- Check connection string format
- Implement retry logic
- Use connection pooling
- Verify service is in same project
```

**Issue: Environment Variable Confusion**
```
Problem: Variables from wrong environment

Solutions:
- Check current environment: railway environment
- Switch environments explicitly
- Use environment-specific values
- Document variables in .env.example
```

## Plugin Metadata

**Version**: 1.0.0

**Minimum Claude Code Version**: 2.0.13

**Last Updated**: 2025-10-12

**Author**: Larry W Jordan Jr

**Repository**: https://github.com/larouex/larouex-fullstack-builder

**License**: MIT

**Support**:
- GitHub Issues: https://github.com/larouex/larouex-fullstack-builder/issues
- Documentation: See /docs directory

**Dependencies**:
- Node.js 20+
- npm or pnpm
- Git
- Platform-specific CLIs (Azure CLI or Railway CLI)

## Quick Reference

### Most Used Commands

```
# Project Setup
/scaffold-azure-full          - Complete Azure stack
/scaffold-railway-full        - Complete Railway stack

# Feature Addition
/add-component               - React component
/add-page                    - New page
/add-form                    - Form with validation
/add-api-azure               - Azure Function endpoint
/add-api-railway             - Express.js endpoint

# Deployment
/deploy-azure-staging        - Deploy to Azure staging
/deploy-azure-production     - Deploy to Azure production
/deploy-railway-staging      - Deploy to Railway staging
/deploy-railway-production   - Deploy to Railway production

# Quality
/add-e2e-test               - End-to-end tests
/audit-security             - Security audit
/audit-accessibility        - Accessibility audit
```

### Agent Quick Reference

```
Frontend        → frontend-development-agent
Forms           → forms-workflow-agent
SEO             → content-seo-agent
Azure Backend   → azure-serverless-agent
Azure DevOps    → devops-azure-agent
Railway DevOps  → devops-railway-agent
Auth            → authentication-agent
Testing         → testing-quality-agent
Security        → security-production-agent
Accessibility   → accessibility-compliance-agent
Monitoring      → monitoring-observability-agent
```

### Platform Decision Matrix

| Factor | Azure | Railway |
|--------|-------|---------|
| Scale | Enterprise | Small-Medium |
| Complexity | High | Low |
| Setup Time | Hours | Minutes |
| Pricing | Consumption | Subscription |
| Database | Table Storage | PostgreSQL |
| Best For | Serverless | Full-Stack |

---

**Using This Plugin Effectively:**

1. Start with scaffold commands to create project foundation
2. Use add-* commands iteratively to build features
3. Reference appropriate agents for complex tasks
4. Follow platform-specific patterns (Azure vs Railway)
5. Deploy to staging first, always
6. Audit security and accessibility before production
7. Monitor applications post-deployment

This plugin is designed to accelerate your development while maintaining production-ready code quality. Each command and agent follows industry best practices and provides implementation details to ensure success.
