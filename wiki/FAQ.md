# Frequently Asked Questions (FAQ)

Common questions and answers about the Full-Stack Website Builder plugin.

## General Questions

### What is this plugin?

The Full-Stack Website Builder is a comprehensive Claude Code plugin that provides 81 slash commands and 12 specialized AI agents for building modern web applications with Next.js 15, Azure, Railway, Bootstrap, and TypeScript.

### Who is this plugin for?

This plugin is designed for:
- Professional developers building Next.js applications
- Teams needing rapid full-stack development
- Developers deploying to Azure or Railway
- Anyone wanting production-ready code templates

### What technologies does it support?

**Frontend:**
- Next.js 15 with App Router
- React 18
- TypeScript 5
- Bootstrap 5

**Backend:**
- Azure Functions
- Express.js on Railway
- REST APIs

**Databases:**
- Azure Table Storage
- PostgreSQL with Prisma
- Railway PostgreSQL

**Cloud Platforms:**
- Azure Static Web Apps
- Railway

### Is it free?

Yes! The plugin is open-source and free to use under the MIT license. However:
- Azure services have their own pricing
- Railway has a free tier and paid plans
- Claude Code itself may have its own pricing

---

## Installation & Setup

### How do I install the plugin?

Three installation methods:

**Method 1 (Recommended):**
```
claude install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
```

**Method 2:** Manual installation - see [Installation Guide](Installation)

**Method 3:** Git clone to `~/.claude/plugins/`

See full [Installation Guide](Installation) for details.

### What are the prerequisites?

**Required:**
- Node.js 20+
- Claude Code 2.0.13+
- Git

**Platform-specific:**
- Azure account + Azure CLI (for Azure commands)
- Railway account + Railway CLI (for Railway commands)

### How do I verify installation?

In Claude Code, type `/` and you should see plugin commands like:
- `/scaffold-azure-full`
- `/add-page`
- `/deploy-railway-staging`

### The plugin isn't working. What should I do?

1. Verify installation location: `ls ~/.claude/plugins/larouex-fullstack-plugin`
2. Check Claude Code version: `claude --version` (need 2.0.13+)
3. Restart Claude Code: `exit` then `claude`
4. See [Troubleshooting](Troubleshooting) for more help

---

## Platform Questions

### Azure vs Railway: Which should I choose?

| Factor | Azure | Railway |
|--------|-------|---------|
| **Best for** | Enterprise apps | Startups, MVPs |
| **Setup complexity** | Medium | Low |
| **Database** | Table Storage | PostgreSQL |
| **Pricing** | Pay-per-use | Fixed tiers |
| **Scale** | Massive | Small-Medium |
| **Learning curve** | Steeper | Easier |

**Choose Azure if:**
- Building enterprise applications
- Need Microsoft ecosystem integration
- Want serverless architecture
- Require global CDN

**Choose Railway if:**
- Want rapid development
- Prefer traditional server architecture
- Need PostgreSQL with ORM
- Want simpler deployment

### Can I use both Azure and Railway?

Yes! The plugin supports both platforms. You can:
- Start with Railway for development
- Migrate to Azure for production
- Use Azure for one project, Railway for another
- The frontend code is mostly platform-agnostic

### How do I switch platforms?

Use migration commands:
- `/migrate-azure-to-railway` - Move from Azure to Railway
- `/migrate-railway-to-azure` - Move from Railway to Azure

These commands help adapt your code to the new platform.

### Do I need an Azure/Railway account immediately?

No! You can:
1. Start with `/scaffold-nextjs` (platform-agnostic)
2. Develop locally
3. Choose platform later
4. Use migration commands to adapt

---

## Usage Questions

### How do I start a new project?

**For Azure:**
```bash
claude
/scaffold-azure-full
```

**For Railway:**
```bash
claude
/scaffold-railway-full
```

See [Quick Start](Quick-Start) for complete tutorials.

### What's the typical workflow?

1. **Scaffold** project
2. **Add** pages and components
3. **Build** features (forms, auth, APIs)
4. **Test** thoroughly
5. **Review** code
6. **Deploy** to staging
7. **Deploy** to production

See [Workflows](Workflows) for detailed patterns.

### How do I add a new page?

```bash
/add-page
```

Claude will ask for:
- Page name
- Route path
- Layout type

The command creates the page with routing, metadata, and responsive layout.

### How do I add authentication?

```bash
/add-auth
```

This sets up:
- NextAuth.js configuration
- Login/signup pages
- Protected routes
- Session management

See [Authentication Agent](Authentication-Agent) for details.

### What if a command fails?

1. **Check error message** - Often explains the issue
2. **Verify prerequisites** - Are required tools installed?
3. **Check file permissions** - Can Claude write files?
4. **Try again** - Some failures are transient
5. **Report issue** - [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)

---

## Deployment Questions

### How do I deploy to staging?

**Azure:**
```bash
/deploy-azure-staging
```

**Railway:**
```bash
/deploy-railway-staging
```

Always test in staging before production!

### How do I deploy to production?

**Required:** Run pre-deployment review first!

```bash
/review-before-deploy
```

If all checks pass:
```bash
/deploy-azure-production
# or
/deploy-railway-production
```

### What is `/review-before-deploy`?

This command is a **mandatory quality gate** that checks:
- All tests pass
- No security vulnerabilities
- Performance benchmarks met
- Accessibility compliance
- Documentation updated
- Environment variables configured

It provides a GO/NO-GO recommendation.

### Can I skip the review?

Technically yes, but **strongly discouraged**. The review:
- Catches critical issues before production
- Prevents outages
- Ensures quality
- Takes only a few minutes

### How do I rollback a deployment?

**Azure:**
- Use deployment slots
- Swap back to previous slot

**Railway:**
- Use Railway dashboard
- Rollback to previous deployment

See platform-specific guides: [Azure](Azure-Platform-Guide) | [Railway](Railway-Platform-Guide)

### How long does deployment take?

**Azure:**
- Staging: 3-5 minutes
- Production: 3-5 minutes

**Railway:**
- Staging: 2-3 minutes
- Production: 2-3 minutes

Times vary based on project size.

---

## Agent Questions

### What are agents?

Agents are specialized AI assistants with expertise in specific domains like frontend development, Azure serverless, security, etc. When you use a command, Claude invokes the appropriate agent(s).

### How many agents are there?

**12 specialized agents:**
1. Frontend Development
2. Forms Workflow
3. Content & SEO
4. Azure Serverless
5. DevOps Azure
6. DevOps Railway
7. Monitoring & Observability
8. Testing & Quality
9. Security & Production
10. Accessibility & Compliance
11. Authentication
12. Code Review

See [Agents Overview](Agents-Overview) for details.

### Do I need to choose an agent?

No! Claude automatically selects the right agent(s) based on your command. Multiple agents often collaborate on complex features.

### Can agents work together?

Yes! Complex features often involve multiple agents. For example, creating an admin panel uses:
- Frontend Development Agent (UI)
- Authentication Agent (access control)
- DevOps Agent (APIs)
- Security Agent (validation)

---

## Command Questions

### How many commands are there?

**81 commands** organized into 10 categories:
- Scaffolding (6)
- Azure (8)
- Railway (7)
- Development (20+)
- Testing (8)
- Review (6)
- Deployment (4)
- Performance (6)
- Integration (10+)
- Advanced (12+)

See [Commands Overview](Commands-Overview) for the complete list.

### How do I see all commands?

In Claude Code, type `/` to see available commands. Or browse:
- [Commands Overview](Commands-Overview)
- [Scaffolding Commands](Scaffolding-Commands)
- [Development Commands](Development-Commands)

### Can I create my own commands?

Yes! Add new command files to `commands/` in the plugin directory. Follow the existing command format.

See [Contributing](Contributing) for guidelines.

### Are commands platform-specific?

Some commands are platform-specific:
- `/add-api-azure` - Azure only
- `/add-api-railway` - Railway only

Others are platform-agnostic:
- `/add-page` - Works anywhere
- `/add-component` - Works anywhere
- `/add-form` - Works anywhere

---

## Testing Questions

### How do I add tests?

```bash
# Unit tests
/add-tests

# End-to-end tests
/add-e2e-test

# Integration tests
/add-integration-test
```

### What testing frameworks are used?

- **Unit tests**: Jest + React Testing Library
- **E2E tests**: Playwright
- **Integration tests**: Jest + Supertest

### Do I need to write tests manually?

The plugin generates initial tests, but you should:
1. Review generated tests
2. Add test cases for edge cases
3. Ensure adequate coverage
4. Run tests regularly

### How do I run tests?

```bash
# Run all tests
npm test

# Run with coverage
npm test -- --coverage

# Run E2E tests
npm run test:e2e
```

---

## Troubleshooting Questions

### Commands aren't showing up

**Causes:**
- Plugin not installed correctly
- Claude Code version too old
- File permissions issue

**Solutions:**
1. Verify installation: `ls ~/.claude/plugins/larouex-fullstack-plugin`
2. Update Claude Code to 2.0.13+
3. Fix permissions: `chmod -R 755 ~/.claude/plugins/larouex-fullstack-plugin`
4. Restart Claude Code

### Azure deployment fails

**Common causes:**
- Not logged in: `az login`
- Wrong subscription: `az account set --subscription "YOUR_SUBSCRIPTION"`
- Missing resource group: Create in Azure Portal
- GitHub secrets not configured

See [Azure Platform Guide](Azure-Platform-Guide) and [Troubleshooting](Troubleshooting).

### Railway deployment fails

**Common causes:**
- Not logged in: `railway login`
- Project not linked: `railway link`
- Environment variables missing
- Build errors

See [Railway Platform Guide](Railway-Platform-Guide) and [Troubleshooting](Troubleshooting).

### TypeScript errors after scaffolding

**Solution:**
```bash
# Install dependencies
npm install

# Generate types
npm run build

# Restart TypeScript server in VS Code
Cmd+Shift+P > "TypeScript: Restart TS Server"
```

---

## Contribution Questions

### Can I contribute to the plugin?

Yes! Contributions are welcome. See [Contributing](Contributing) for guidelines.

### How do I report bugs?

[GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)

Provide:
- Description of the issue
- Steps to reproduce
- Expected vs actual behavior
- Claude Code version
- Platform (Azure/Railway)

### How do I request features?

[GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues) with label "feature request"

Include:
- Description of feature
- Use case
- Proposed implementation (optional)

### How do I get help?

1. Check this FAQ
2. See [Troubleshooting](Troubleshooting)
3. Browse [Examples](Examples)
4. Ask in [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)
5. Report issues on [GitHub](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)

---

## Advanced Questions

### Can I modify the plugin?

Yes! It's open-source (MIT license). You can:
- Fork the repository
- Modify commands
- Add new agents
- Customize for your needs

### How do I update the plugin?

**If installed via GitHub:**
```
update plugin larouex-fullstack-plugin
```

**If manually installed:**
```bash
cd ~/.claude/plugins/larouex-fullstack-plugin
git pull origin main
```

Restart Claude Code after updating.

### What's the plugin architecture?

See [Architecture](Architecture) for technical details.

Key components:
- **Agents**: Specialized AI assistants in `agents/` at root level
- **Commands**: Slash commands in `commands/` at root level
- **Metadata**: Plugin configuration in `.claude-plugin/`

### Can I use this plugin commercially?

Yes! The MIT license allows commercial use. See [LICENSE](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/blob/main/LICENSE).

### Is there a roadmap?

See README "Roadmap" section for planned features. Major items:
- Additional cloud platform support (AWS, GCP, Vercel)
- GraphQL scaffolding
- Database migration tools
- Component library generator
- Mobile app scaffolding

---

## Still Have Questions?

- **Documentation**: Browse the full [Wiki](Home)
- **Discussions**: [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)
- **Issues**: [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
- **Examples**: [Real-world Examples](Examples)

---

**Can't find your answer?** Ask in [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions) - the community is happy to help!
