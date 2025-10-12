# Architecture Documentation

## Overview

The Laravel-NextJS Claude Plugin is designed as a comprehensive development accelerator for full-stack web applications using Next.js 15 with TypeScript and Bootstrap 5. The plugin leverages Claude's AI capabilities through a specialized agent system and command-driven workflow to automate common development tasks.

### Plugin Architecture Philosophy

The plugin follows three core architectural principles:

1. **Specialization over Generalization**: Instead of one monolithic agent, the plugin uses 11 specialized agents, each an expert in their domain (DevOps, security, components, etc.).

2. **Platform Agnostic by Design**: While optimized for Azure and Railway, the architecture supports easy extension to other platforms (AWS, Vercel, etc.) through abstraction patterns.

3. **Convention over Configuration**: Sensible defaults reduce cognitive load while maintaining flexibility for customization.

### Key Design Principles

- **Declarative Commands**: Users describe what they want, not how to do it
- **Agent Orchestration**: Commands invoke appropriate agents automatically
- **Code Generation Safety**: All generated code follows best practices and security standards
- **Developer Experience First**: Optimize for clarity, speed, and reliability

### Technology Choices

- **Next.js 15**: Modern React framework with App Router and Server Components
- **TypeScript**: Type safety and enhanced developer experience
- **Bootstrap 5**: Rapid UI development with consistent design system
- **Azure & Railway**: Production-grade hosting with different use cases
- **Claude AI**: Advanced code generation and architectural reasoning

## System Architecture

### Plugin Structure

```
larouex-website/
├── .claude-plugin/           # Plugin manifests and metadata
│   └── manifest.json         # Plugin configuration
├── .claude/
│   ├── agents/              # AI specialist agents
│   │   ├── architecture-agent.md
│   │   ├── bootstrap-component-agent.md
│   │   ├── devops-azure-agent.md
│   │   ├── devops-railway-agent.md
│   │   ├── forms-agent.md
│   │   ├── nextjs-app-router-agent.md
│   │   ├── nextjs-component-agent.md
│   │   ├── platform-engineer-agent.md
│   │   ├── security-agent.md
│   │   ├── seo-agent.md
│   │   └── typescript-agent.md
│   └── commands/            # Slash commands
│       ├── add-component.md
│       ├── add-form.md
│       ├── add-page.md
│       ├── deploy-azure.md
│       ├── deploy-railway.md
│       ├── init-project.md
│       ├── scaffold-azure.md
│       ├── scaffold-railway.md
│       ├── secure-app.md
│       └── setup-seo.md
├── docs/                    # Documentation
│   ├── ARCHITECTURE.md      # This file
│   ├── CONTRIBUTING.md      # Contribution guidelines
│   └── QUICK_START.md       # Getting started guide
└── examples/                # Templates and examples
    ├── components/
    ├── forms/
    └── pages/
```

### Agent System Architecture

#### Agent Discovery Mechanism

Agents are discovered through the `.claude/agents/` directory. Each agent is a Markdown file that defines:

- **Expertise Area**: The agent's specialized domain
- **Capabilities**: What the agent can do
- **Context**: Technologies, patterns, and best practices
- **Output Format**: Expected code structure and style

#### Agent Prompt Structure

Each agent follows a standardized structure:

```markdown
# [Agent Name]

You are [role description].

## Core Responsibilities
- Responsibility 1
- Responsibility 2

## Technologies
- Technology 1
- Technology 2

## Patterns and Best Practices
- Pattern 1
- Pattern 2

## Code Generation Rules
- Rule 1
- Rule 2

## Output Format
Expected structure
```

#### How Agents Are Invoked

When a command is executed:

1. Command markdown references specific agents by name
2. Claude's routing system identifies the appropriate agent(s)
3. Agent context is injected into the generation process
4. Multiple agents can collaborate on complex tasks

Example from `/add-component`:
```markdown
Use the [nextjs-component-agent] and [bootstrap-component-agent] to create...
```

#### Agent State Management

Agents are stateless between invocations. Each command execution provides:

- Current project context (file structure, dependencies)
- Command parameters (component name, options)
- Relevant existing code (for consistency)
- Previous command outputs (for chaining)

### Command System Architecture

#### Command Discovery

Commands are discovered through the `.claude/commands/` directory. Each command is a Markdown file containing:

- Command description (what it does)
- Agent references (which agents to invoke)
- Technology specifications (Next.js 15, TypeScript, etc.)
- Output expectations (files to create, changes to make)

#### Command Execution Flow

1. **User Invocation**: User types `/command-name [parameters]`
2. **Command Resolution**: Claude loads the command markdown
3. **Context Gathering**: Current project state is analyzed
4. **Agent Selection**: Referenced agents are activated
5. **Code Generation**: Agents generate appropriate code
6. **File Operations**: Files are created or modified
7. **Validation**: Generated code is checked for correctness
8. **Feedback**: Results are reported to the user

#### Parameter Passing

Commands accept parameters through natural language:

```bash
/add-component ProductCard
/add-page dashboard/analytics
/add-form contact-us with-validation
```

Parameters are parsed and provided to agents as context.

#### Output Handling

Commands produce multiple types of output:

- **Files Created**: New source files, tests, styles
- **Files Modified**: Updated configurations, imports
- **Instructions**: Manual steps if required
- **Validation Results**: Errors or warnings

## Technology Decisions

### Why Next.js 15?

Next.js 15 was chosen for several architectural reasons:

1. **App Router Maturity**: The App Router provides a stable, modern routing system with built-in layouts, loading states, and error boundaries.

2. **Server Components by Default**: Reduces client-side JavaScript, improving performance and SEO.

3. **Streaming and Suspense**: Better user experience with progressive rendering.

4. **Full-Stack Framework**: API routes, server actions, and middleware in one framework.

5. **Production Ready**: Battle-tested at scale with strong ecosystem support.

6. **Developer Experience**: Fast Refresh, TypeScript integration, and excellent error messages.

### Why Azure AND Railway?

The plugin supports dual platforms to serve different use cases:

#### Azure (Enterprise Use Case)

- **Enterprise Requirements**: Active Directory integration, compliance certifications
- **Scalability**: Global CDN, unlimited scaling, enterprise SLAs
- **Integration**: Seamless integration with Azure services (Cosmos DB, Azure Functions, etc.)
- **Complexity**: More complex setup, higher learning curve
- **Cost**: Pay-as-you-grow with enterprise discounts

#### Railway (Startup/Agency Use Case)

- **Developer Experience**: Instant deployments, simple configuration
- **Speed**: Get production apps running in minutes
- **Cost**: Predictable pricing, generous free tier
- **Simplicity**: No DevOps expertise required
- **Ideal For**: MVPs, client projects, side projects

The plugin's architecture abstracts platform differences through specialized DevOps agents, allowing developers to switch platforms easily.

### Why Bootstrap 5?

Bootstrap 5 was selected for UI development:

1. **Rapid Development**: Pre-built components accelerate development
2. **Consistency**: Design system ensures visual coherence
3. **Responsive by Default**: Mobile-first grid system
4. **Customization**: SASS variables allow brand customization
5. **No jQuery**: Modern, vanilla JavaScript implementation
6. **Battle-Tested**: Proven across millions of websites
7. **Accessibility**: ARIA attributes and keyboard navigation built-in

The plugin could be extended to support other UI frameworks (Tailwind, Material-UI) through additional agents.

### Why TypeScript?

TypeScript provides critical benefits for generated code:

1. **Type Safety**: Catch errors before runtime, especially important for AI-generated code
2. **IntelliSense**: Better developer experience in IDEs
3. **Refactoring**: Safe, automated refactoring across large codebases
4. **Documentation**: Types serve as inline documentation
5. **Team Scalability**: Enforces contracts between team members
6. **Next.js Integration**: First-class TypeScript support in Next.js

## Design Patterns

### Platform Abstraction Pattern

Platform-specific commands and agents are isolated to enable easy extension:

```
Generic Layer (Platform Agnostic)
├── nextjs-app-router-agent
├── nextjs-component-agent
└── typescript-agent

Platform Layer (Platform Specific)
├── Azure
│   ├── devops-azure-agent
│   ├── scaffold-azure.md
│   └── deploy-azure.md
└── Railway
    ├── devops-railway-agent
    ├── scaffold-railway.md
    └── deploy-railway.md
```

**Benefits**:
- Add new platforms without modifying generic code
- Switch platforms without rewriting application code
- Platform-specific optimizations without complexity

**Implementation**:
- Platform agents encapsulate platform knowledge
- Platform commands reference platform-specific agents
- Generic commands remain platform-agnostic

### Agent Specialization Pattern

Rather than one generic "web development agent", we use 11 specialized agents:

**Rationale**:
- **Focused Expertise**: Each agent masters one domain deeply
- **Token Efficiency**: Only relevant context is loaded per task
- **Maintainability**: Update one agent without affecting others
- **Composition**: Complex tasks combine multiple agents
- **Clarity**: Clear boundaries of responsibility

**Agent Categories**:

1. **Infrastructure Agents**: `devops-azure-agent`, `devops-railway-agent`
2. **Framework Agents**: `nextjs-app-router-agent`, `nextjs-component-agent`
3. **UI Agents**: `bootstrap-component-agent`, `forms-agent`
4. **Cross-Cutting Agents**: `security-agent`, `seo-agent`, `typescript-agent`
5. **Meta Agents**: `architecture-agent`, `platform-engineer-agent`

### Command Composition Pattern

Commands can be chained to create complex workflows:

```bash
# Basic workflow
/init-project my-app
/scaffold-railway
/add-page home
/add-component Hero
/deploy-railway

# Each command builds on previous state
# State is maintained through file system
```

**Implementation**:
- Commands are idempotent (safe to run multiple times)
- Commands check for prerequisites
- Commands provide clear success/failure feedback
- Commands document next steps

### Convention over Configuration

The plugin uses strong conventions to reduce decision fatigue:

**File Locations**:
- Components: `src/app/components/[ComponentName]/`
- Pages: `src/app/[route]/page.tsx`
- API Routes: `src/app/api/[route]/route.ts`
- Styles: `src/app/styles/`

**Naming Conventions**:
- Components: PascalCase (e.g., `ProductCard`)
- Pages: kebab-case (e.g., `product-details`)
- Files: Match Next.js conventions (e.g., `page.tsx`, `layout.tsx`)

**Code Structure**:
- TypeScript strict mode enabled
- Server Components by default
- Client Components explicitly marked with `'use client'`
- Barrel exports for components

**Override Mechanism**:
Users can override conventions through configuration files or command parameters.

## Data Flow

### Command Execution Flow

```
┌─────────────────────────────────────────────────────────────┐
│ 1. User Invocation                                          │
│    /add-component ProductCard                               │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Command Prompt Sent to Claude                            │
│    - Load add-component.md                                  │
│    - Parse parameters (ProductCard)                         │
│    - Gather project context                                 │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Agent(s) Selected                                        │
│    - nextjs-component-agent (primary)                       │
│    - bootstrap-component-agent (UI framework)               │
│    - typescript-agent (type generation)                     │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. Code Generation                                          │
│    - Generate component file                                │
│    - Generate types file                                    │
│    - Generate styles file                                   │
│    - Generate barrel export                                 │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. File Operations                                          │
│    - Create src/app/components/ProductCard/                 │
│    - Write ProductCard.tsx                                  │
│    - Write ProductCard.types.ts                             │
│    - Write index.ts                                         │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│ 6. Validation                                               │
│    - Check TypeScript syntax                                │
│    - Verify imports                                         │
│    - Validate file structure                                │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│ 7. User Feedback                                            │
│    - Report created files                                   │
│    - Provide usage examples                                 │
│    - Suggest next steps                                     │
└─────────────────────────────────────────────────────────────┘
```

### Multi-Agent Workflows

Complex workflows involve multiple agents collaborating:

#### Example: Adding a Secure Contact Form

```
User: /add-form contact-us with-validation

Flow:
1. forms-agent
   - Designs form structure
   - Plans validation rules
   - Defines submission flow

2. typescript-agent
   - Creates TypeScript interfaces
   - Types for form data
   - Types for API responses

3. security-agent
   - Adds CSRF protection
   - Implements rate limiting
   - Sanitizes inputs
   - Validates on server

4. nextjs-component-agent
   - Creates form component
   - Implements Server Action
   - Handles loading states
   - Manages error boundaries

5. bootstrap-component-agent
   - Applies Bootstrap styling
   - Ensures responsive layout
   - Adds validation feedback UI

Output:
- src/app/components/ContactForm/ContactForm.tsx
- src/app/components/ContactForm/ContactForm.types.ts
- src/app/components/ContactForm/validation.ts
- src/app/api/contact/route.ts
- Updated configuration for rate limiting
```

## Scalability Considerations

### Adding New Platforms

To add support for a new platform (e.g., Vercel, AWS, Google Cloud):

**1. Create Platform DevOps Agent**

File: `.claude/agents/devops-vercel-agent.md`

```markdown
# DevOps Vercel Agent

You are a Vercel deployment specialist...

## Vercel-Specific Knowledge
- Edge Functions
- Middleware configuration
- Environment variables
- Build optimization
- Analytics integration
```

**2. Create Scaffold Command**

File: `.claude/commands/scaffold-vercel.md`

```markdown
Set up this Next.js 15 project for Vercel deployment.

Use the [devops-vercel-agent] to create:
- vercel.json configuration
- Environment variable templates
- Build optimization settings
```

**3. Create Deployment Command**

File: `.claude/commands/deploy-vercel.md`

```markdown
Deploy the application to Vercel.

Use the [devops-vercel-agent] to:
- Validate configuration
- Run pre-deployment checks
- Execute deployment
- Verify deployment
```

**4. Update Documentation**

Add platform to QUICK_START.md and platform comparison table.

### Adding New Commands

To add a new command:

**1. Identify Purpose**

What developer task does this automate?

**2. Choose Template**

```markdown
# Command Template

[1-2 sentence description of what command does]

Use the [agent-name] and [agent-name] to [action].

## Technologies
- Next.js 15
- TypeScript
- [Other technologies]

## Expected Output
- File 1: Description
- File 2: Description

## Parameters
- parameter1: Description
- parameter2: Description (optional)
```

**3. Create Command File**

File: `.claude/commands/your-command.md`

**4. Test Command**

```bash
/your-command [parameters]
```

Verify:
- Correct files created
- Valid TypeScript
- Follows conventions
- Proper error handling

**5. Document Command**

Add to QUICK_START.md command reference.

### Adding New Agents

Create a new agent when:

1. **New Domain Expertise**: A specialized domain not covered by existing agents (e.g., GraphQL, WebSockets)
2. **Platform Addition**: New hosting platform or service integration
3. **Framework Addition**: Supporting a new framework (e.g., Tailwind CSS, Prisma)
4. **Complex Cross-Cutting Concern**: Authentication, monitoring, internationalization

**Agent Creation Process**:

**1. Define Agent Scope**

```
Agent Name: authentication-agent
Purpose: Handle authentication and authorization
Scope: OAuth, JWT, session management, RBAC
Technologies: NextAuth.js, JWT, cookies
```

**2. Create Agent File**

File: `.claude/agents/authentication-agent.md`

**3. Structure Agent Content**

```markdown
# Authentication Agent

You are an authentication and authorization specialist for Next.js 15 applications.

## Core Responsibilities
- Implement secure authentication flows
- Set up authorization (RBAC, ABAC)
- Manage sessions and tokens
- Integrate OAuth providers

## Technologies
- NextAuth.js v5
- JWT (JSON Web Tokens)
- HTTP-only cookies
- OAuth 2.0 / OIDC

## Patterns and Best Practices
- Secure token storage
- CSRF protection
- Password hashing (bcrypt)
- Multi-factor authentication

## Security Considerations
- Never store passwords in plain text
- Use HTTP-only cookies for tokens
- Implement rate limiting
- Validate all inputs

## Code Generation Rules
- Use NextAuth.js for OAuth
- Implement API route protection
- Create middleware for auth checks
- Type all auth-related interfaces

## Output Format
Standard Next.js route handlers and middleware
```

**4. Reference Agent in Commands**

Update existing commands or create new ones that reference the agent.

**5. Test Agent**

Validate generated code follows security best practices.

## Performance Considerations

### Token Optimization

AI models have token limits. The plugin optimizes token usage:

**Agent Specialization**:
- Load only relevant agent context
- 11 small agents vs. 1 large agent reduces tokens per task

**Command Brevity**:
- Commands are concise (under 150 words)
- Focus on what, not how
- Reference agents instead of duplicating knowledge

**Context Pruning**:
- Only include relevant project files
- Summarize large files
- Use file trees instead of full content

**Example Token Comparison**:

```
Monolithic Approach:
- Generic agent: 5,000 tokens
- Project context: 3,000 tokens
- Total: 8,000 tokens per request

Specialized Approach:
- Specific agent: 800 tokens
- Relevant context: 1,500 tokens
- Total: 2,300 tokens per request

Savings: 71% fewer tokens
```

### File Structure Efficiency

The plugin's file structure is optimized for:

**Discovery Speed**:
- Flat agent directory (11 files)
- Flat command directory (10 files)
- No deep nesting to search

**Caching**:
- Agents are cacheable between requests
- Commands are cacheable
- Project context is incrementally updated

**Parallel Processing**:
- Multiple agents can work simultaneously
- File operations can be parallelized

## Security Architecture

### Secrets Management

**Environment Variables**:
- Never commit secrets to repository
- Use `.env.local` (git-ignored)
- Provide `.env.example` templates
- Document required variables

**Agent Guidelines**:
```markdown
## Security Rules
- Never hardcode API keys
- Always use process.env.VARIABLE_NAME
- Validate environment variables at startup
- Use different keys for dev/staging/prod
```

**Platform Integration**:
- Azure: Use Azure Key Vault for secrets
- Railway: Use Railway environment variables
- Both: Support .env.local for local development

### Code Generation Safety

**Security Agent Oversight**:
- All generated code reviewed for common vulnerabilities
- SQL injection prevention
- XSS prevention
- CSRF protection
- Input validation

**TypeScript Enforcement**:
- Strict mode prevents common errors
- Type checking catches issues early
- No implicit `any` types

**Best Practices Embedded**:
```typescript
// Generated code always includes:

// 1. Input validation
const validated = schema.parse(input);

// 2. Error handling
try {
  // operation
} catch (error) {
  // proper error handling
}

// 3. Type safety
interface Props {
  data: ValidatedData;
}
```

**Rate Limiting**:
- API routes include rate limiting by default
- Prevents abuse of generated endpoints

**Content Security Policy**:
- Generated apps include CSP headers
- Prevents XSS attacks

## Testing Strategy

### Command Validation

**Manual Testing**:
1. Create test project
2. Run command
3. Verify files created
4. Check file contents
5. Run TypeScript compiler
6. Start dev server
7. Test in browser

**Automated Testing** (Future):
```bash
# Test runner for commands
npm run test:commands

# Tests:
# - Command produces expected files
# - Generated code compiles
# - No TypeScript errors
# - Follows conventions
```

### Agent Testing

**Validation Checklist**:
- [ ] Agent produces valid TypeScript
- [ ] Code follows Next.js 15 patterns
- [ ] Security best practices applied
- [ ] Bootstrap classes used correctly
- [ ] Components are properly typed
- [ ] Files follow naming conventions
- [ ] Imports are correct
- [ ] Code is idiomatic and readable

**Test Scenarios**:
```bash
# Test each agent with various inputs
/add-component SimpleComponent
/add-component ComplexComponent with-state with-api
/add-page home
/add-page dashboard/settings
/add-form contact-us with-validation
```

## Future Architecture

### Planned Improvements

**1. Additional Platform Support**
- Vercel integration (highest priority)
- AWS Amplify
- Google Cloud Run
- Netlify
- Cloudflare Pages

**2. Agent Enhancements**
- `testing-agent`: Generate Jest/React Testing Library tests
- `api-agent`: Specialized REST/GraphQL API creation
- `database-agent`: Prisma/Drizzle ORM integration
- `authentication-agent`: NextAuth.js integration
- `monitoring-agent`: Logging and observability

**3. Command Expansion**
- `/add-test`: Generate tests for components
- `/add-api`: Create API routes
- `/add-db-model`: Create database models
- `/refactor`: AI-assisted refactoring
- `/optimize`: Performance optimization suggestions
- `/audit`: Security and performance audits

**4. Interactive Workflows**
- Multi-step wizards for complex setups
- Interactive component builders
- Guided deployment workflows

**5. Template Library**
- Pre-built page templates (landing, dashboard, etc.)
- Component library (cards, navbars, modals)
- Form templates (contact, registration, checkout)

### Extension Points

The plugin architecture supports extensions through:

**1. Plugin Hooks** (Future)

```javascript
// .claude-plugin/hooks.js
module.exports = {
  beforeGenerate: async (context) => {
    // Custom pre-generation logic
  },
  afterGenerate: async (files, context) => {
    // Custom post-generation logic
  }
};
```

**2. Custom Agents**

Developers can add their own agents:

```bash
.claude/agents/custom-agent.md
```

Command can reference custom agents:

```markdown
Use the [custom-agent] to...
```

**3. Platform Adapters** (Future)

```typescript
// .claude-plugin/adapters/custom-platform.ts
export class CustomPlatformAdapter implements PlatformAdapter {
  async deploy(config: DeployConfig): Promise<DeployResult> {
    // Custom deployment logic
  }
}
```

**4. Configuration Extensions**

```json
// .claude-plugin/config.json
{
  "extends": "base",
  "customAgents": ["./agents/custom-agent.md"],
  "customCommands": ["./commands/custom-command.md"],
  "platforms": {
    "custom": {
      "adapter": "./adapters/custom-platform.js"
    }
  }
}
```

## Conclusion

The Laravel-NextJS Claude Plugin demonstrates a scalable, maintainable architecture for AI-assisted development. By combining specialized agents, declarative commands, and platform abstraction, it enables rapid development while maintaining code quality and security.

The architecture is designed for extension, allowing the community to add new platforms, agents, and commands as the ecosystem evolves.

Key architectural strengths:

1. **Separation of Concerns**: Agents, commands, and platforms are isolated
2. **Composability**: Components combine to create complex workflows
3. **Extensibility**: New capabilities can be added without modifying core
4. **Maintainability**: Clear structure and conventions ease updates
5. **Scalability**: Pattern supports growth in features and platforms

For questions or suggestions about the architecture, please see CONTRIBUTING.md.
