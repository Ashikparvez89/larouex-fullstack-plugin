# Changelog

All notable changes to the Full-Stack Website Builder Plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- code-review-agent: Automated code review specialist (12th agent)
- 6 new review commands: /review-code, /review-component, /review-api, /review-security, /review-performance, /review-before-deploy
- Mandatory code review gates in production deployment commands
- Severity-based issue classification (Critical, High, Medium, Low, Info)
- Platform-specific validation (Azure Functions, Railway Prisma)
- Pre-deployment checklist automation

### Changed
- /deploy-azure-production now requires /review-before-deploy completion
- /deploy-railway-production now requires /review-before-deploy completion
- Total agents increased from 11 to 12
- Total commands increased from 75 to 81

### Planned
- Additional platform support (Vercel, AWS, Netlify)
- Enhanced agent collaboration
- Visual project templates
- Interactive command builder

## [1.0.0] - 2025-01-12

### Added
- Initial release of Full-Stack Website Builder Plugin
- 11 specialized AI agents:
  - frontend-development-agent
  - forms-workflow-agent
  - content-seo-agent
  - azure-serverless-agent
  - devops-azure-agent
  - devops-railway-agent
  - monitoring-observability-agent
  - testing-quality-agent
  - security-production-agent
  - accessibility-compliance-agent
  - authentication-agent
- 75 slash commands organized in 23 categories:
  - 6 scaffolding commands (Azure, Railway, generic)
  - 8 Azure platform commands
  - 7 Railway platform commands
  - 5 page & component commands
  - 3 forms & validation commands
  - 4 content & SEO commands
  - 4 authentication & security commands
  - 4 testing & quality commands
  - 4 performance optimization commands
  - 3 email & notifications commands
  - 3 file upload & storage commands
  - 3 search & filtering commands
  - 3 analytics & tracking commands
  - 2 internationalization commands
  - 3 data visualization commands
  - 3 real-time features commands
  - 3 documentation commands
  - 3 error handling commands
  - 3 scheduled jobs commands
  - 3 social integration commands
  - 2 payment processing commands
  - 3 admin panel commands
  - 4 migration & upgrade commands
- Comprehensive documentation:
  - README.md with quick start guide
  - CLAUDE.md with architecture for AI context
  - docs/AGENTS.md with complete agent reference
  - docs/COMMANDS.md with full command reference
  - docs/ARCHITECTURE.md with technical details
  - docs/CONTRIBUTING.md with contribution guidelines
- Support for Next.js 15 with App Router
- Support for Bootstrap 5.3+ UI framework
- Support for TypeScript 5 strict mode
- Azure Static Web Apps deployment support
- Azure Functions v4 backend support
- Railway platform deployment support
- PostgreSQL + Prisma ORM support
- Application Insights monitoring integration
- Complete testing infrastructure (Jest, Playwright)
- WCAG 2.1 AA accessibility support
- Security best practices and auditing
- Multi-environment deployment (staging/production)

### Documentation
- Complete README with installation and usage
- Detailed agent documentation (53 KB)
- Comprehensive command reference (71 KB)
- Architecture documentation
- Contributing guidelines
- Examples and workflows

## [Pre-release]

### Development Phase
- Agent consolidation from 21 to 11 agents
- Command standardization and naming conventions
- Platform-specific command separation (Azure vs Railway)
- Documentation structure planning

---

## Version Numbering

This plugin follows [Semantic Versioning](https://semver.org/):
- MAJOR version for incompatible API changes
- MINOR version for added functionality (backwards compatible)
- PATCH version for backwards compatible bug fixes

## Categories

- **Added** - New features
- **Changed** - Changes to existing functionality
- **Deprecated** - Soon-to-be removed features
- **Removed** - Removed features
- **Fixed** - Bug fixes
- **Security** - Vulnerability fixes
