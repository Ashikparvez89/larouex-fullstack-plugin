# Agents Overview

The Full-Stack Website Builder plugin includes **12 specialized AI agents**, each with expertise in specific domains of web development. These agents work individually or collaboratively to help you build production-ready applications.

## What are Agents?

Agents are specialized AI assistants with deep knowledge in specific areas of web development. When you use a command, Claude automatically invokes the appropriate agent(s) to handle the task with expert-level knowledge.

### Benefits of Specialized Agents

- **Expert Knowledge**: Each agent is an expert in their domain
- **Context-Aware**: Agents understand platform-specific requirements (Azure vs Railway)
- **Best Practices**: Agents follow industry standards and security guidelines
- **Collaboration**: Multiple agents can work together on complex features
- **Consistency**: Agents ensure consistent patterns across your codebase

---

## The 12 Specialized Agents

### Frontend & UI

1. **[Frontend Development Agent](Frontend-Development-Agent)**
   - React, TypeScript, Bootstrap
   - Responsive design and accessibility
   - Component architecture

2. **[Forms Workflow Agent](Forms-Workflow-Agent)**
   - Form creation and validation
   - Multi-step workflows
   - File upload handling

3. **[Content & SEO Agent](Content-SEO-Agent)**
   - SEO optimization
   - Content management
   - Structured data and metadata

### Backend & Cloud

4. **[Azure Serverless Agent](Azure-Serverless-Agent)**
   - Azure Functions development
   - Azure Table Storage
   - Azure services integration

5. **[DevOps Azure Agent](DevOps-Azure-Agent)**
   - Azure deployment
   - GitHub Actions CI/CD
   - Azure infrastructure

6. **[DevOps Railway Agent](DevOps-Railway-Agent)**
   - Railway deployment
   - PostgreSQL and Prisma
   - Railway platform optimization

### Quality & Operations

7. **[Monitoring & Observability Agent](Monitoring-Observability-Agent)**
   - Application monitoring
   - Performance tracking
   - Error logging and alerting

8. **[Testing & Quality Agent](Testing-Quality-Agent)**
   - Unit and integration testing
   - E2E testing with Playwright
   - Test coverage and quality assurance

9. **[Security & Production Agent](Security-Production-Agent)**
   - Security audits and best practices
   - Production readiness
   - Vulnerability scanning

10. **[Accessibility & Compliance Agent](Accessibility-Compliance-Agent)**
    - WCAG 2.1 AA compliance
    - Accessibility testing
    - ARIA and semantic HTML

### Features & Authentication

11. **[Authentication Agent](Authentication-Agent)**
    - User authentication flows
    - OAuth and social login
    - Session management and RBAC

12. **[Code Review Agent](Code-Review-Agent)**
    - Automated code review
    - 10 review categories
    - Pre-deployment quality gates

---

## Agent Categories

### 1. Frontend Development (3 agents)

These agents handle everything related to the user interface:

| Agent | Primary Focus | Common Commands |
|-------|--------------|-----------------|
| Frontend Development Agent | UI components, layouts, responsive design | `/add-page`, `/add-component`, `/add-section` |
| Forms Workflow Agent | Forms, validation, data entry | `/add-form`, `/add-multistep-form` |
| Content & SEO Agent | SEO, content structure, metadata | `/add-seo`, `/add-content-json` |

**When to use:**
- Building pages and components
- Creating forms
- Optimizing for search engines
- Managing content

---

### 2. Backend & Infrastructure (3 agents)

These agents manage server-side logic and cloud infrastructure:

| Agent | Primary Focus | Common Commands |
|-------|--------------|-----------------|
| Azure Serverless Agent | Azure Functions, serverless architecture | `/add-api-azure`, `/add-database-azure`, `/scaffold-azure-full` |
| DevOps Azure Agent | Azure deployment and CI/CD | `/deploy-azure-staging`, `/deploy-azure-production` |
| DevOps Railway Agent | Railway deployment and full-stack | `/add-api-railway`, `/deploy-railway-staging`, `/scaffold-railway-full` |

**When to use:**
- Creating API endpoints
- Setting up databases
- Configuring deployments
- Managing cloud infrastructure

---

### 3. Quality & Operations (4 agents)

These agents ensure your application is secure, performant, and maintainable:

| Agent | Primary Focus | Common Commands |
|-------|--------------|-----------------|
| Monitoring & Observability Agent | Performance monitoring, logging | `/setup-monitoring-azure`, `/setup-monitoring-railway` |
| Testing & Quality Agent | Testing strategies, quality assurance | `/add-tests`, `/add-e2e-test` |
| Security & Production Agent | Security, production best practices | `/audit-security` |
| Accessibility & Compliance Agent | WCAG compliance, accessibility | `/audit-accessibility` |

**When to use:**
- Setting up monitoring
- Writing tests
- Security audits
- Accessibility compliance

---

### 4. Features & Authentication (2 agents)

These agents handle user authentication and code quality:

| Agent | Primary Focus | Common Commands |
|-------|--------------|-----------------|
| Authentication Agent | Auth flows, OAuth, sessions | `/add-auth`, `/add-protected-route`, `/add-social-login` |
| Code Review Agent | Code quality, best practices, pre-deployment gates | `/review-code`, `/review-before-deploy`, `/review-security` |

**When to use:**
- Implementing authentication
- Adding protected routes
- Reviewing code changes
- Pre-deployment checks

---

## How Agents Work Together

Complex features often require multiple agents collaborating:

### Example 1: E-commerce Checkout Flow

**Agents involved:**
1. **Forms Workflow Agent** - Creates multi-step checkout form
2. **Frontend Development Agent** - Builds responsive UI
3. **Azure Serverless Agent** - Implements payment processing API
4. **Security & Production Agent** - Adds input validation
5. **Testing & Quality Agent** - Creates test suite
6. **Code Review Agent** - Reviews complete implementation

**Workflow:**
```
/add-checkout
  → Forms Workflow Agent: Creates checkout form structure
  → Frontend Development Agent: Adds responsive layout
  → Azure Serverless Agent: Creates payment API
  → Security & Production Agent: Validates inputs
  → Testing & Quality Agent: Generates tests
  → Code Review Agent: Final review before commit
```

---

### Example 2: Admin Dashboard with Authentication

**Agents involved:**
1. **Authentication Agent** - Sets up login and auth guards
2. **Frontend Development Agent** - Builds dashboard UI
3. **DevOps Railway Agent** - Creates admin API endpoints
4. **Accessibility & Compliance Agent** - Ensures WCAG compliance
5. **Monitoring & Observability Agent** - Adds logging and metrics

**Workflow:**
```
/add-admin-panel
  → Authentication Agent: Protects admin routes
  → Frontend Development Agent: Creates dashboard components
  → DevOps Railway Agent: Builds admin APIs
  → Accessibility & Compliance Agent: Checks accessibility
  → Monitoring & Observability Agent: Adds monitoring
```

---

### Example 3: Production Deployment

**Agents involved:**
1. **Code Review Agent** - Pre-deployment review
2. **Testing & Quality Agent** - Runs test suite
3. **Security & Production Agent** - Security audit
4. **Accessibility & Compliance Agent** - Accessibility check
5. **DevOps Azure Agent** - Handles deployment

**Workflow:**
```
/review-before-deploy
  → Code Review Agent: Comprehensive code review
  → Testing & Quality Agent: Verifies all tests pass
  → Security & Production Agent: Security scan
  → Accessibility & Compliance Agent: Accessibility audit
  → DevOps Azure Agent: Deploys if all checks pass
```

---

## Agent Selection Guide

Use this decision tree to find the right agent:

```
What are you building?

├─ User Interface?
│  ├─ Page or Component? → Frontend Development Agent
│  ├─ Form? → Forms Workflow Agent
│  └─ SEO/Content? → Content & SEO Agent
│
├─ Backend/API?
│  ├─ Azure? → Azure Serverless Agent
│  └─ Railway? → DevOps Railway Agent
│
├─ Deployment?
│  ├─ Azure? → DevOps Azure Agent
│  └─ Railway? → DevOps Railway Agent
│
├─ Authentication?
│  └─ Auth flow/OAuth → Authentication Agent
│
├─ Quality/Testing?
│  ├─ Tests? → Testing & Quality Agent
│  ├─ Security? → Security & Production Agent
│  ├─ Accessibility? → Accessibility & Compliance Agent
│  └─ Code Review? → Code Review Agent
│
└─ Monitoring?
   └─ Logs/Metrics → Monitoring & Observability Agent
```

---

## Agent Expertise Matrix

| Agent | TypeScript | React | Next.js | Azure | Railway | Testing | Security |
|-------|-----------|-------|---------|-------|---------|---------|----------|
| **Frontend Development** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐⭐ |
| **Forms Workflow** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Content & SEO** | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐ |
| **Azure Serverless** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | - | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **DevOps Azure** | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | - | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **DevOps Railway** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | - | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Monitoring & Observability** | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **Testing & Quality** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Security & Production** | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Accessibility & Compliance** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Authentication** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Code Review** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |

---

## Detailed Agent Pages

Click on any agent name to learn more about their capabilities, common patterns, and best practices:

### Frontend & UI
- Frontend Development Agent - React components, responsive design
- Forms Workflow Agent - Forms, validation, multi-step workflows
- Content & SEO Agent - SEO, metadata, content management

### Backend & Cloud
- Azure Serverless Agent - Azure Functions, Table Storage
- DevOps Azure Agent - Azure deployment, GitHub Actions
- DevOps Railway Agent - Railway deployment, PostgreSQL

### Quality & Operations
- Monitoring & Observability Agent - Application monitoring
- Testing & Quality Agent - Testing strategies
- Security & Production Agent - Security audits
- Accessibility & Compliance Agent - WCAG compliance

### Features & Authentication
- Authentication Agent - Auth flows, OAuth
- Code Review Agent - Code quality, pre-deployment gates

---

## Agent Communication

Agents automatically coordinate when working together. You don't need to manually switch between agents - Claude handles this for you.

### How Coordination Works

1. **Command invocation**: You run a command (e.g., `/add-admin-panel`)
2. **Primary agent**: Claude identifies the primary agent needed
3. **Collaboration**: Primary agent identifies supporting agents
4. **Sequential execution**: Agents work in sequence or parallel
5. **Integration**: Final output integrates all agent contributions

### Example Coordination

```
User runs: /add-checkout

Step 1: Forms Workflow Agent creates form structure
        ↓
Step 2: Frontend Development Agent adds UI styling
        ↓
Step 3: Azure Serverless Agent creates payment API
        ↓
Step 4: Security & Production Agent validates inputs
        ↓
Step 5: Testing & Quality Agent generates tests
        ↓
Result: Complete, tested checkout flow
```

---

## Best Practices for Working with Agents

### 1. Let Agents Guide You

Agents will ask clarifying questions. Answer them to get the best results:

```
/add-form

Agent asks:
- What fields do you need?
- Should this be a multi-step form?
- Do you need file upload?
- What validation rules?
```

### 2. Trust Agent Expertise

Agents follow best practices automatically:
- Security measures
- Accessibility standards
- Performance optimization
- Error handling

### 3. Use the Right Agent for the Job

Don't force an agent into the wrong domain:
- ❌ Frontend Agent creating Azure Functions
- ✅ Azure Serverless Agent creating Azure Functions

### 4. Leverage Agent Collaboration

For complex features, agents work together automatically:
- E-commerce checkout
- Admin dashboards
- Authentication systems

### 5. Review Agent Output

Agents provide production-ready code, but always:
- Review generated code
- Run tests
- Verify in staging
- Use `/review-before-deploy` before production

---

## Next Steps

- **Explore individual agents**: Click on agent names above to see detailed documentation
- **Try commands**: Use the [Commands Overview](Commands-Overview) to see what each agent can do
- **Follow workflows**: Check out [Workflows](Workflows) for complete development patterns
- **See examples**: Visit [Examples](Examples) for real-world agent usage

---

## Getting Help

- **Agent-specific questions**: See individual agent pages
- **General questions**: Check [FAQ](FAQ)
- **Issues**: Report on [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)

---

**Ready to see agents in action?** Try the [Quick Start Guide](Quick-Start) to build your first project with agent assistance!
