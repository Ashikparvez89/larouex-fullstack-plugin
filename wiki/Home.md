# Full-Stack Website Builder - Claude Code Plugin Wiki

> Welcome to the comprehensive documentation for the Full-Stack Website Builder Plugin. This plugin provides 81 commands and 12 specialized AI agents for building modern web applications with Next.js 15, Azure, Railway, Bootstrap, and TypeScript.

## Quick Navigation

### Getting Started
- [Installation Guide](Installation) - Get up and running quickly
- [Quick Start](Quick-Start) - Build your first project in 5 minutes
- [FAQ](FAQ) - Frequently asked questions

### Core Documentation
- [Agents Overview](Agents-Overview) - 12 specialized AI agents
- [Commands Overview](Commands-Overview) - 81 slash commands organized by category
- [Workflows](Workflows) - Common development workflows
- [Architecture](Architecture) - Technical architecture and design

### Platform Guides
- [Azure Platform Guide](Azure-Platform-Guide) - Azure-specific documentation
- [Railway Platform Guide](Railway-Platform-Guide) - Railway-specific documentation

### Features & Commands
- [Scaffolding Commands](Scaffolding-Commands) - Project initialization (6 commands)
- [Azure Commands](Azure-Commands) - Azure cloud operations (10 commands)
- [Railway Commands](Railway-Commands) - Railway deployment (9 commands)
- [Development Commands](Development-Commands) - Pages, components, forms
- [Testing Commands](Testing-Commands) - Testing and quality assurance
- [Review Commands](Review-Commands) - Code review and quality gates
- [Deployment Commands](Deployment-Commands) - Deploy to staging and production
- [Performance Commands](Performance-Commands) - Optimization and monitoring
- [Integration Commands](Integration-Commands) - Email, analytics, social media
- [Advanced Commands](Advanced-Commands) - i18n, real-time, payments, admin

### Quality & Best Practices
- [Code Review System](Code-Review-System) - Automated code review and quality gates
- [Testing & Quality](Testing-Commands) - Testing strategies and tools
- [Troubleshooting](Troubleshooting) - Common issues and solutions

### Resources
- [Examples](Examples) - Real-world examples and tutorials
- [API Reference](API-Reference) - Technical API documentation
- [Contributing](Contributing) - How to contribute to the plugin
- [Changelog](Changelog) - Version history and updates

## What is This Plugin?

The **Full-Stack Website Builder** is a production-ready Claude Code plugin that accelerates modern web development. It provides:

### Key Features

- **81 Slash Commands** - Comprehensive command library covering the entire development lifecycle
- **12 Specialized AI Agents** - Expert agents for frontend, backend, DevOps, testing, security, and more
- **Multi-Platform Support** - Native support for Azure Static Web Apps, Azure Functions, and Railway
- **Next.js 15 Optimized** - Built specifically for Next.js 15 with App Router and Server Components
- **Bootstrap 5 Integration** - Responsive, mobile-first design with Bootstrap 5
- **TypeScript First** - Full TypeScript support with strict type checking
- **Complete Lifecycle** - From scaffolding to production deployment and monitoring

### Technologies Supported

**Frontend:**
- Next.js 15 (App Router)
- React 18
- TypeScript 5
- Bootstrap 5

**Backend:**
- Azure Functions
- Railway Services
- REST APIs
- GraphQL

**Cloud Platforms:**
- Azure Static Web Apps
- Azure Functions
- Railway

**Databases:**
- Azure Cosmos DB
- PostgreSQL
- MongoDB
- Railway PostgreSQL

**Testing:**
- Jest
- React Testing Library
- Playwright
- Cypress

**Analytics & Monitoring:**
- Google Analytics
- Plausible
- Application Insights
- Railway Observability

## Quick Start

### 1. Install the Plugin

```bash
# Option 1: Install from GitHub (Recommended)
# Open Claude Code and run:
claude install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin

# Option 2: Manual Installation
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
cp -r larouex-fullstack-plugin ~/.claude/plugins/
```

### 2. Create Your First Project

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

### 3. Add Features

```bash
# Add a new page
/add-page

# Add a contact form
/add-form

# Add authentication
/add-auth
```

### 4. Deploy

```bash
# Deploy to staging
/deploy-azure-staging
# or
/deploy-railway-staging

# Deploy to production
/deploy-azure-production
# or
/deploy-railway-production
```

## Popular Use Cases

### Building a Corporate Website
1. [Scaffold Azure project](Scaffolding-Commands#scaffold-azure-full)
2. [Add pages and navigation](Development-Commands#add-page)
3. [Add contact form](Development-Commands#add-form)
4. [Configure SEO](Development-Commands#add-seo)
5. [Deploy to production](Deployment-Commands#deploy-azure-production)

### Building a SaaS Application
1. [Scaffold Railway project](Scaffolding-Commands#scaffold-railway-full)
2. [Add authentication](Advanced-Commands#add-auth)
3. [Create admin panel](Advanced-Commands#add-admin-panel)
4. [Add payment processing](Advanced-Commands#add-stripe)
5. [Setup monitoring](Performance-Commands#setup-monitoring)

### Building an E-commerce Site
1. [Scaffold project](Scaffolding-Commands)
2. [Add product pages](Development-Commands#add-page)
3. [Create checkout flow](Advanced-Commands#add-checkout)
4. [Integrate payments](Advanced-Commands#add-stripe)
5. [Add analytics](Integration-Commands#add-analytics-google)

## Statistics

- **Commands**: 81
- **Agents**: 12
- **Supported Platforms**: Azure, Railway, Standalone
- **Technologies**: 20+
- **Lines of Documentation**: 5000+
- **Active Development**: Yes
- **Community Contributors**: Open

## Getting Help

- **Documentation**: Browse this wiki for comprehensive guides
- **Issues**: [Report bugs on GitHub](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
- **Discussions**: [Join the community](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)
- **Examples**: Check out the [Examples](Examples) page for real-world tutorials

## Prerequisites

Before using this plugin, ensure you have:

### Required
- **Node.js 20+** - [Download](https://nodejs.org/)
- **Claude Code 2.0.13+** - [Get Claude Code](https://claude.ai)
- **Git** - For version control

### Platform-Specific
- **Azure Account** - For Azure features ([Free Account](https://azure.microsoft.com/free/))
- **Railway Account** - For Railway features ([Sign Up](https://railway.app/))

### Optional but Recommended
- **VS Code** - For development
- **GitHub Account** - For CI/CD
- **Docker** - For local containerized development

## What's New

### Version 1.0.0 (Latest)
- Added Code Review Agent (12th agent)
- 6 new review commands for automated code review
- Mandatory code review gates in production deployments
- Severity-based issue classification
- Platform-specific validation (Azure/Railway)
- Pre-deployment checklist automation

See the full [Changelog](Changelog) for version history.

## Community

This plugin is built by developers, for developers. Contributions are welcome!

- **Report Bugs**: [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
- **Request Features**: [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
- **Contribute**: See [Contributing Guide](Contributing)
- **Discussions**: [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)

## License

This project is licensed under the **MIT License**. See the [LICENSE](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/blob/main/LICENSE) file for details.

## Author

**Larry W Jordan Jr**
- GitHub: [@larouex](https://github.com/larouex)
- LinkedIn: [Larry W Jordan Jr](https://www.linkedin.com/in/larrywjordanjr/)
- Website: [larouex.com](https://larouex.com)

---

**Ready to build something amazing?** Start with the [Quick Start Guide](Quick-Start) or dive into [Agents Overview](Agents-Overview) to understand the specialized agents at your disposal.
