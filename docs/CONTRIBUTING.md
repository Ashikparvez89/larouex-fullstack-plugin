# Contributing Guide

## Welcome

Thank you for your interest in contributing to the Laravel-NextJS Claude Plugin! This project aims to accelerate Next.js development through AI-powered code generation, and we welcome contributions from developers of all skill levels.

Whether you're fixing a bug, adding a feature, improving documentation, or suggesting enhancements, your contributions help make this plugin better for everyone.

### Code of Conduct

We are committed to providing a welcoming and inclusive environment. By participating in this project, you agree to:

- Be respectful and constructive in all interactions
- Welcome newcomers and help them get started
- Accept constructive criticism gracefully
- Focus on what is best for the community
- Show empathy towards other community members

Please report any unacceptable behavior to the project maintainers.

## Ways to Contribute

There are many ways to contribute to this project:

### Report Bugs

Found a bug? Help us fix it by:
- Checking if the bug has already been reported
- Creating a detailed bug report with reproduction steps
- Including relevant system information and error messages

### Suggest Features

Have an idea for improvement?
- Check existing feature requests
- Describe the use case and expected behavior
- Explain how it would benefit users

### Add Commands

Extend the plugin's capabilities:
- Create new slash commands for common tasks
- Improve existing command prompts
- Add support for new workflows

### Improve Agents

Enhance the AI specialists:
- Refine agent prompts for better output
- Add new patterns and best practices
- Create specialized agents for new domains

### Fix Documentation

Help others understand the plugin:
- Fix typos and unclear explanations
- Add examples and tutorials
- Improve getting started guides

### Add Examples

Provide templates and samples:
- Create example components
- Build sample applications
- Document common patterns

## Getting Started

### Development Setup

1. **Fork and Clone**

```bash
# Fork the repository on GitHub
# Then clone your fork
git clone https://github.com/YOUR_USERNAME/larouex-website.git
cd larouex-website
```

2. **Install Dependencies**

```bash
# Install Node.js dependencies
npm install

# Or using yarn
yarn install

# Or using pnpm
pnpm install
```

3. **Test Locally**

```bash
# Start the development server
npm run dev

# Test commands using Claude CLI
/add-component TestComponent
```

### Project Structure

Understanding the project structure helps you know where to make changes:

```
larouex-website/
├── .claude-plugin/         # Plugin configuration
│   └── manifest.json       # Plugin metadata
├── .claude/
│   ├── agents/            # AI specialist agents
│   └── commands/          # Slash commands
├── docs/                  # Documentation
│   ├── ARCHITECTURE.md    # Technical architecture
│   ├── CONTRIBUTING.md    # This file
│   └── QUICK_START.md     # Getting started guide
├── examples/              # Templates and examples
├── src/                   # Next.js application source
│   └── app/              # App Router pages and components
└── package.json          # Project dependencies
```

## Adding New Commands

Commands are the primary way users interact with the plugin. Each command is a Markdown file that describes what Claude should do.

### Command Template

Create a new file in `.claude/commands/your-command-name.md`:

```markdown
# Short description of what this command does (1-2 sentences)

Use the [agent-name] and [agent-name] to [specific action].

## Technologies
- Next.js 15
- TypeScript
- [Other relevant technologies]

## Requirements
- [Any prerequisites or conditions]

## Expected Output
Create/modify the following:
- File path 1: Description of what it contains
- File path 2: Description of what it contains

## Usage Example
/your-command-name [parameters]

## Parameters
- parameter1: Description (required)
- parameter2: Description (optional)

## Notes
- Any important considerations
- Edge cases to handle
- Related commands
```

### Command Guidelines

When creating or improving commands:

**1. Keep Prompts Concise**
- Under 150 words if possible
- Focus on what, not how
- Let agents handle the implementation details

**2. Reference Appropriate Agents**
- Use specialized agents for their expertise
- Multiple agents can collaborate on complex tasks
- Example: `[nextjs-component-agent]` and `[bootstrap-component-agent]`

**3. Specify Technologies**
- Always mention Next.js 15
- Include TypeScript
- List any other frameworks or libraries

**4. Include Expected Outputs**
- List files that will be created
- Describe modifications to existing files
- Mention any configuration changes

**5. Add Platform Suffix if Needed**
- Generic commands: `/add-component`
- Platform-specific: `/deploy-azure`, `/deploy-railway`

### Command Naming Convention

Follow these naming patterns:

**Generic Commands** (platform-agnostic):
- `/action-target`
- Examples: `/add-component`, `/add-page`, `/add-form`

**Platform-Specific Commands**:
- `/action-platform-target`
- Examples: `/deploy-azure`, `/scaffold-railway`, `/deploy-vercel`

**Operation Commands**:
- `/verb-noun`
- Examples: `/init-project`, `/setup-seo`, `/secure-app`

**Avoid**:
- Abbreviated names (`/add-comp`)
- Unclear actions (`/do-thing`)
- Inconsistent patterns

### Testing New Commands

Before submitting a new command:

1. **Create Test Project**
```bash
mkdir test-project
cd test-project
npm init -y
```

2. **Run Your Command**
```bash
/your-command-name test-parameter
```

3. **Verify Output**
- [ ] All expected files created
- [ ] Files are in correct locations
- [ ] TypeScript compiles without errors
- [ ] Code follows project conventions
- [ ] No syntax errors

4. **Test Integration**
```bash
# Start dev server
npm run dev

# Verify in browser
# Test functionality
```

5. **Test Edge Cases**
- Empty parameters
- Special characters in names
- Existing files (idempotency)
- Invalid inputs

## Improving Existing Agents

Agents are AI specialists that generate code following specific patterns and best practices.

### Agent Structure

A well-structured agent includes:

```markdown
# Agent Name

You are a [role description with expertise area].

## Core Responsibilities
- Primary responsibility 1
- Primary responsibility 2
- Primary responsibility 3

## Technologies and Tools
- Technology 1 (with version if relevant)
- Technology 2
- Framework 1
- Tool 1

## Patterns and Best Practices
- Pattern 1: Explanation
- Pattern 2: Explanation
- Best practice 1
- Best practice 2

## Code Generation Rules
- Rule 1: Specific guideline
- Rule 2: Specific guideline
- Convention 1
- Convention 2

## Security Considerations
- Security practice 1
- Security practice 2

## Output Format
Description of expected code structure, file organization, and style.

## Example
Optional: Show example of well-formed output
```

### Agent Guidelines

When improving agents:

**1. Clear Purpose**
- Define exactly what the agent specializes in
- Avoid overlap with other agents
- Focus on a specific domain

**2. Specific Capabilities**
- List concrete tasks the agent performs
- Provide examples of typical outputs
- Include edge cases and error handling

**3. Best Practices Included**
- Current industry standards
- Framework-specific patterns
- Performance considerations
- Security guidelines

**4. Consistent Style**
- Follow established code style
- Use proper TypeScript types
- Follow Next.js conventions
- Apply Bootstrap patterns (for UI components)

**5. Examples and Patterns**
- Show before/after code
- Provide templates
- Demonstrate complex scenarios

### When to Modify Agents

**Update Existing Agent When**:
- Fixing incorrect patterns
- Adding new best practices
- Improving clarity
- Updating for new framework versions
- Enhancing error handling

**Create New Agent When**:
- Adding support for new technology
- Introducing new platform
- Covering new domain expertise
- Handling complex cross-cutting concern

## Creating New Agents

New agents extend the plugin's capabilities in specific domains.

### When to Create a New Agent

Create a new agent when:

1. **New Domain Expertise Required**
   - Testing (Jest, React Testing Library)
   - Database (Prisma, Drizzle)
   - Authentication (NextAuth.js)
   - API (GraphQL, tRPC)

2. **Platform Addition**
   - New hosting platform (Vercel, AWS)
   - New cloud service integration
   - Platform-specific optimizations

3. **Framework Addition**
   - UI framework (Tailwind CSS, Material-UI)
   - State management (Zustand, Redux)
   - Data fetching (React Query, SWR)

4. **Complex Cross-Cutting Concern**
   - Monitoring and logging
   - Internationalization (i18n)
   - Accessibility (a11y)
   - Analytics integration

### Agent Template

Create a new file in `.claude/agents/your-agent-name.md`:

```markdown
# Your Agent Name

You are a [descriptive role] specializing in [domain] for Next.js 15 applications using TypeScript and Bootstrap 5.

## Core Responsibilities

List 3-5 primary responsibilities:
- Responsibility 1: Generate [type of code]
- Responsibility 2: Implement [pattern]
- Responsibility 3: Ensure [quality aspect]

## Technologies and Tools

List all relevant technologies:
- Next.js 15 (App Router)
- TypeScript (Strict Mode)
- [Your specialty technology]
- [Related tools]

## Patterns and Best Practices

Document patterns this agent should follow:

### Pattern 1: [Pattern Name]
Description and when to use it.

### Pattern 2: [Pattern Name]
Description and when to use it.

### Best Practices
- Best practice 1
- Best practice 2
- Best practice 3

## Code Generation Rules

Specific rules for generated code:

### File Organization
- Where to place files
- How to structure directories
- Naming conventions

### Code Style
- TypeScript usage
- Component structure
- Import organization
- Comment guidelines

### Testing
- What to test
- How to structure tests

### Performance
- Optimization techniques
- What to avoid

## Security Considerations

Security guidelines specific to this domain:
- Security concern 1
- Security concern 2
- Validation rules
- Authentication/Authorization

## Error Handling

How to handle errors in this domain:
- Error types to catch
- Error messages to provide
- Fallback behaviors

## Output Format

Describe the structure of generated code:

```
expected-directory/
├── file1.tsx
├── file2.types.ts
└── file3.module.css
```

## Example Output

Provide a complete example of what this agent generates:

```typescript
// Example code showing proper structure and patterns
```

## Integration

How this agent works with other agents:
- Works with [agent-name] for [purpose]
- Complements [agent-name] by [explanation]

## References

Links to relevant documentation:
- [Technology Documentation](https://example.com)
- [Best Practices Guide](https://example.com)
```

### Agent Naming Convention

Follow these patterns:

**Domain Agents**:
- `[domain]-agent`
- Examples: `authentication-agent`, `testing-agent`, `database-agent`

**Platform Agents**:
- `devops-[platform]-agent`
- Examples: `devops-azure-agent`, `devops-vercel-agent`

**Technology Agents**:
- `[technology]-agent`
- Examples: `graphql-agent`, `prisma-agent`, `tailwind-agent`

**Must**:
- End with `-agent`
- Use lowercase with hyphens
- Be descriptive and clear

**Avoid**:
- Generic names like `helper-agent`
- Abbreviations like `auth-ag`
- Ambiguous names

### Agent Testing

Validate your agent through:

1. **Syntax Check**
   - Markdown is well-formed
   - Code blocks are properly formatted
   - Links are valid

2. **Functionality Test**
   - Create test command that uses your agent
   - Run command and verify output
   - Check that code compiles
   - Validate against best practices

3. **Integration Test**
   - Test agent with related agents
   - Verify no conflicts
   - Check for consistency

4. **Documentation Review**
   - Clear and understandable
   - Complete coverage of responsibilities
   - Good examples provided

## Adding Platform Support

Adding support for a new deployment platform expands the plugin's reach.

### Platform Requirements

To add a new platform, you need:

1. **Platform Knowledge**
   - Deployment process
   - Configuration requirements
   - Environment variable handling
   - Build and runtime requirements

2. **CLI or API Access**
   - Command-line deployment tools
   - API for programmatic deployment
   - Authentication methods

3. **Documentation**
   - Platform-specific guides
   - Best practices
   - Troubleshooting

### Platform Integration Steps

**1. Create DevOps Agent**

File: `.claude/agents/devops-[platform]-agent.md`

```markdown
# DevOps [Platform] Agent

You are a [Platform] deployment specialist for Next.js 15 applications.

## Platform-Specific Knowledge
- [Platform] architecture
- Deployment workflow
- Environment configuration
- Optimization techniques

## Core Responsibilities
- Configure project for [Platform]
- Set up deployment pipeline
- Manage environment variables
- Optimize for [Platform] features

[Continue with full agent structure...]
```

**2. Add Scaffold Command**

File: `.claude/commands/scaffold-[platform].md`

```markdown
Set up this Next.js 15 project for [Platform] deployment.

Use the [devops-[platform]-agent] to create:
- [Platform] configuration files
- Environment variable templates
- Build optimization settings
- Deployment scripts

[Continue with full command structure...]
```

**3. Add Deployment Command**

File: `.claude/commands/deploy-[platform].md`

```markdown
Deploy the application to [Platform].

Use the [devops-[platform]-agent] and [platform-engineer-agent] to:
- Validate project configuration
- Run pre-deployment checks
- Execute deployment
- Verify successful deployment
- Provide deployment URL

[Continue with full command structure...]
```

**4. Add Platform-Specific Features**

Additional commands for platform features:
- `/optimize-[platform]`: Platform-specific optimizations
- `/logs-[platform]`: View deployment logs
- `/rollback-[platform]`: Rollback deployment

**5. Update Documentation**

Update the following files:
- `docs/QUICK_START.md`: Add platform to deployment options
- `docs/ARCHITECTURE.md`: Document platform architecture
- `README.md`: Add platform to supported list

**6. Add Examples**

Create example configurations:
- Configuration file templates
- Environment variable examples
- Deployment workflow examples

### Platform Examples

#### Example: Adding Vercel Support

**Step 1: DevOps Agent**

`.claude/agents/devops-vercel-agent.md`:
```markdown
# DevOps Vercel Agent

You are a Vercel deployment specialist for Next.js 15 applications.

## Platform-Specific Knowledge
- Vercel Edge Network
- Edge Functions and Middleware
- Environment Variables and Secrets
- Build Configuration
- Analytics Integration

## Core Responsibilities
- Configure vercel.json
- Set up environment variables
- Optimize for Edge Functions
- Configure build settings
- Set up domain and DNS

[Full agent content...]
```

**Step 2: Scaffold Command**

`.claude/commands/scaffold-vercel.md`:
```markdown
Set up this Next.js 15 project for Vercel deployment.

Use the [devops-vercel-agent] to create:
- vercel.json configuration
- .vercelignore file
- Environment variable templates (.env.example)
- Build optimization settings
- README with deployment instructions

[Full command content...]
```

**Step 3: Deploy Command**

`.claude/commands/deploy-vercel.md`:
```markdown
Deploy the application to Vercel.

Use the [devops-vercel-agent] and [platform-engineer-agent] to:
1. Validate vercel.json configuration
2. Check environment variables
3. Run build locally to verify
4. Deploy using Vercel CLI
5. Verify deployment
6. Provide deployment URL and dashboard link

[Full command content...]
```

## Documentation Standards

Good documentation helps everyone understand and use the plugin effectively.

### Markdown Guidelines

Follow these Markdown best practices:

**Headers**:
```markdown
# H1 for document title (only one per file)
## H2 for major sections
### H3 for subsections
#### H4 for detailed points
```

**Code Blocks**:
````markdown
```typescript
// Use language-specific syntax highlighting
const example: string = "formatted code";
```

```bash
# Shell commands
npm install
```
````

**Links**:
```markdown
# Relative links for internal docs
See [Architecture](ARCHITECTURE.md)

# Absolute links for external resources
See [Next.js Docs](https://nextjs.org/docs)
```

**Lists**:
```markdown
# Unordered lists for non-sequential items
- Item 1
- Item 2

# Ordered lists for sequential steps
1. Step 1
2. Step 2
```

**Emphasis**:
```markdown
**Bold** for important terms
*Italic* for emphasis
`code` for inline code or commands
```

### Documentation Requirements

**Every Command Needs**:
- Clear description of purpose
- Usage examples
- Parameter documentation
- Expected output
- Related commands

**Every Agent Needs**:
- Role description
- Core responsibilities
- Technologies used
- Code generation rules
- Example output

**Examples for Complex Features**:
- Step-by-step tutorials
- Real-world use cases
- Common pitfalls and solutions
- Best practices

## Code Quality Standards

### TypeScript Standards

All TypeScript code should follow these standards:

**1. Strict Mode**
```typescript
// tsconfig.json should have strict: true
"strict": true,
"noImplicitAny": true,
"strictNullChecks": true
```

**2. Proper Types**
```typescript
// Good: Explicit types
interface UserProps {
  name: string;
  email: string;
  age?: number;
}

// Avoid: any type
const user: any = getData(); // Bad

// Good: Proper typing
const user: User = getData(); // Good
```

**3. JSDoc Comments**
```typescript
/**
 * Validates user email address
 * @param email - The email to validate
 * @returns true if valid, false otherwise
 */
function validateEmail(email: string): boolean {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}
```

**4. Consistent Naming**
```typescript
// PascalCase for types and components
interface UserData {}
function UserProfile() {}

// camelCase for variables and functions
const userData = {};
function getUserData() {}

// UPPER_CASE for constants
const API_URL = "https://api.example.com";
```

### Testing Requirements

While automated tests are future work, manual testing is required:

**Test Generated Code**:
- [ ] TypeScript compiles without errors
- [ ] No ESLint warnings
- [ ] Follows project conventions
- [ ] Properly formatted (Prettier)

**Validate Patterns**:
- [ ] Uses Next.js 15 App Router patterns
- [ ] Server/Client Components used correctly
- [ ] Follows React best practices
- [ ] Implements proper error handling

**Check for Errors**:
- [ ] No runtime errors
- [ ] No console warnings
- [ ] Handles edge cases
- [ ] Provides user feedback

## Pull Request Process

### PR Guidelines

Follow these steps to submit a pull request:

**1. Fork Repository**
```bash
# Fork on GitHub, then:
git clone https://github.com/YOUR_USERNAME/larouex-website.git
cd larouex-website
```

**2. Create Feature Branch**
```bash
# Create branch from main
git checkout -b feature/your-feature-name

# Or for bug fixes
git checkout -b fix/bug-description
```

**3. Make Changes**
- Follow code quality standards
- Test thoroughly
- Update documentation
- Add examples if needed

**4. Commit Changes**
```bash
# Stage changes
git add .

# Commit with descriptive message
git commit -m "feat: add Vercel deployment support"

# Follow conventional commits:
# feat: new feature
# fix: bug fix
# docs: documentation changes
# refactor: code refactoring
# test: adding tests
# chore: maintenance
```

**5. Push to Fork**
```bash
git push origin feature/your-feature-name
```

**6. Submit PR**
- Go to original repository
- Click "New Pull Request"
- Select your branch
- Fill out PR template

### PR Template

When creating a PR, include:

```markdown
## Description
Brief description of what this PR does.

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Code refactoring
- [ ] Other (describe)

## Changes Made
- Change 1
- Change 2
- Change 3

## Code Review
- [ ] Ran /review-code on all changes
- [ ] Addressed all Critical severity issues
- [ ] Addressed all High severity issues
- [ ] Documented any Medium issues that won't be fixed

## Testing Done
- [ ] Tested locally
- [ ] Verified TypeScript compilation
- [ ] Checked in browser
- [ ] Tested edge cases

## Related Issues
Closes #123

## Screenshots (if applicable)
Add screenshots for UI changes

## Checklist
- [ ] Code follows project style
- [ ] Code review completed (see above)
- [ ] Documentation updated
- [ ] Examples added (if needed)
- [ ] Self-review completed
- [ ] No breaking changes (or documented)
```

### Review Process

After submitting a PR:

1. **Automated Checks** (if configured)
   - TypeScript compilation
   - Linting
   - Format checking

2. **Maintainer Review**
   - Code quality assessment
   - Pattern validation
   - Documentation review
   - Testing verification

3. **Feedback and Iteration**
   - Address reviewer comments
   - Make requested changes
   - Push updates to same branch

4. **Approval and Merge**
   - Maintainer approves
   - PR is merged
   - Branch is deleted

## Issue Reporting

### Bug Reports

Use this template for bug reports:

```markdown
## Bug Description
Clear description of the bug.

## Steps to Reproduce
1. Run command `/add-component Example`
2. Check generated file
3. See error

## Expected Behavior
What should happen.

## Actual Behavior
What actually happens.

## Environment
- OS: [e.g., macOS 14.0]
- Node.js: [e.g., v20.0.0]
- Next.js: [e.g., 15.0.0]
- Plugin Version: [e.g., 1.0.0]

## Error Messages
```
Paste error messages here
```

## Additional Context
Any other relevant information.
```

### Feature Requests

Use this template for feature requests:

```markdown
## Feature Description
Clear description of the proposed feature.

## Use Case
Why is this feature needed? What problem does it solve?

## Proposed Solution
How should this feature work?

## Alternatives Considered
What other approaches did you consider?

## Additional Context
Any mockups, examples, or references.
```

### Questions

For questions:

```markdown
## Question
Your question here.

## What I've Tried
What you've already attempted.

## Context
Relevant background information.
```

## Community Guidelines

### Code of Conduct

Our community is built on respect and collaboration:

**Do**:
- Be welcoming and inclusive
- Provide constructive feedback
- Respect differing viewpoints
- Accept constructive criticism
- Focus on what's best for the community

**Don't**:
- Use offensive language
- Make personal attacks
- Harass others
- Publish private information
- Engage in unprofessional behavior

### Communication Channels

**GitHub Issues**: Bug reports, feature requests
**GitHub Discussions**: Questions, ideas, general discussion
**Pull Requests**: Code contributions and reviews

### Getting Help

Need help contributing?

1. Check existing documentation
2. Search closed issues
3. Ask in GitHub Discussions
4. Tag maintainers in issues (if urgent)

### Best Practices for Contributors

**Communication**:
- Be clear and concise
- Provide context
- Be patient
- Ask questions

**Collaboration**:
- Review others' PRs
- Help answer questions
- Share knowledge
- Encourage newcomers

**Quality**:
- Test thoroughly
- Document changes
- Follow conventions
- Consider edge cases

## Recognition

### Contributors

All contributors are recognized in:
- Contributors section in README
- Release notes for their contributions
- Project acknowledgments

### Types of Contributions Recognized

- Code contributions
- Documentation improvements
- Bug reports
- Feature suggestions
- Community support
- Code reviews
- Examples and tutorials

## License

This project is licensed under the MIT License. By contributing, you agree that your contributions will be licensed under the same license.

### What This Means

- Your contributions are open source
- Others can use, modify, and distribute your contributions
- You retain copyright to your contributions
- No warranty is provided

### Copyright

When contributing code:
- You retain copyright
- You grant license to use your contribution
- Your contribution must be your original work
- You have rights to contribute it

## Getting Started Checklist

Ready to contribute? Follow this checklist:

- [ ] Read ARCHITECTURE.md to understand the system
- [ ] Read QUICK_START.md to learn how to use the plugin
- [ ] Set up development environment
- [ ] Test commands locally
- [ ] Browse existing issues for ideas
- [ ] Choose an issue or feature to work on
- [ ] Fork the repository
- [ ] Create a feature branch
- [ ] Make your changes
- [ ] Test thoroughly
- [ ] Update documentation
- [ ] Submit pull request
- [ ] Respond to feedback
- [ ] Celebrate your contribution!

## Thank You

Thank you for contributing to the Laravel-NextJS Claude Plugin! Your contributions help developers build better applications faster. We appreciate your time, effort, and expertise.

Questions? Reach out to the maintainers or ask in GitHub Discussions.

Happy coding!
