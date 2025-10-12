# Full-Stack Website Builder Plugin - Marketplace Setup Guide

## Overview

This guide explains how to host your plugin on GitHub and use it in other projects via Claude Code's plugin marketplace system.

## Prerequisites

- Git repository with your plugin files
- GitHub account
- Claude Code v2.0.13 or higher installed

## Current Plugin Structure

Your plugin is properly configured with:

```
.claude-plugin/
├── plugin.json          # Plugin metadata
└── marketplace.json     # Marketplace listing

.claude/
├── agents/             # 12 specialized agents
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
│   ├── accessibility-compliance-agent.md
│   └── code-review-agent.md
│
├── commands/           # 81 slash commands
│   └── [all command files]
│
└── CLAUDE.md          # Architecture documentation
```

## Step 1: Push Plugin to GitHub

### 1.1 Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `larouex-fullstack-plugin` (or your preferred name)
3. Description: "Full-Stack Website Builder plugin for Claude Code"
4. Choose: **Public** (required for marketplace)
5. Don't initialize with README (you have files already)
6. Click "Create repository"

### 1.2 Push Your Plugin Files

From your current directory, run:

```bash
# Initialize git (if not already done)
git init

# Add all plugin files
git add .claude-plugin/
git add .claude/
git add docs/
git add README.md

# Commit the plugin
git commit -m "Initial plugin release v1.0.0"

# Add your GitHub remote
git remote add origin https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### 1.3 Create a Release Tag (Recommended)

```bash
# Tag the release
git tag -a v1.0.0 -m "Release v1.0.0: Full-Stack Website Builder"

# Push the tag
git push origin v1.0.0
```

## Step 2: Verify Plugin Structure on GitHub

Your repository should have this structure visible:

```
https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── .claude/
│   ├── agents/
│   ├── commands/
│   └── CLAUDE.md
├── docs/
├── assets/ (if you have screenshots)
└── README.md
```

**Critical Requirement**: The `.claude-plugin/marketplace.json` file MUST be in the root of your repository.

## Step 3: Using Your Plugin in Other Projects

### Option A: Install from GitHub Repository

In any Claude Code session for another project:

```
/plugin marketplace add LarouexNonprofitConsulting/larouex-fullstack-plugin
```

Then browse and install:

```
/plugin
```

Select your plugin from the marketplace list and click "Install".

### Option B: Install Directly via URL

```
/plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
```

### Option C: Install Specific Version

```
/plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin@v1.0.0
```

## Step 4: Verify Installation

After installation, verify in your new project:

1. **Check installed plugins:**
   ```
   /plugin list
   ```

2. **Test a command:**
   ```
   /scaffold-nextjs
   ```

3. **Verify agents are available** - They should be automatically referenced when using commands

## Step 5: Update Your marketplace.json

If your GitHub repository URL differs from what's in marketplace.json, update it:

```json
{
  "repository": "https://github.com/YOUR-USERNAME/YOUR-REPO-NAME",
  "bugs": "https://github.com/YOUR-USERNAME/YOUR-REPO-NAME/issues",
  "homepage": "https://github.com/YOUR-USERNAME/YOUR-REPO-NAME#readme",
  "documentation": "https://github.com/YOUR-USERNAME/YOUR-REPO-NAME/wiki"
}
```

## Step 6: Create Screenshots (Optional but Recommended)

Your marketplace.json references these screenshots:

```json
"screenshots": [
  "assets/screenshot-scaffold.png",
  "assets/screenshot-review.png",
  "assets/screenshot-deploy.png"
]
```

Create the `assets/` directory and add PNG screenshots showing:

1. **screenshot-scaffold.png** - Scaffolding a new project
2. **screenshot-review.png** - Code review in action
3. **screenshot-deploy.png** - Deployment workflow

Then commit and push:

```bash
mkdir -p assets
# Add your screenshot files to assets/
git add assets/
git commit -m "Add plugin screenshots"
git push
```

## Step 7: Create Plugin Icon (Optional)

Add a plugin icon at `assets/icon.png`:

- Recommended size: 128x128px
- Format: PNG with transparency
- Should represent your plugin visually

## Distribution Workflow

### For Public Distribution

1. **GitHub Repository (Recommended)**
   - Most common method
   - Easy versioning with git tags
   - Users install via: `/plugin marketplace add user/repo`

2. **Direct URL**
   - Any publicly accessible URL with `.claude-plugin/marketplace.json`
   - Users install via: `/plugin install https://example.com/plugin`

### For Private/Team Use

1. **Private GitHub Repository**
   - Same structure as public
   - Users need GitHub access
   - Install via: `/plugin install https://github.com/org/private-repo` (with authentication)

2. **Local Directory**
   - Share plugin files directly
   - Users copy to their project's `.claude/` directory

## Version Management

### Releasing Updates

1. **Update version in plugin.json:**
   ```json
   {
     "version": "1.1.0"
   }
   ```

2. **Commit and tag:**
   ```bash
   git add .claude-plugin/plugin.json
   git commit -m "Release v1.1.0: Add new features"
   git tag -a v1.1.0 -m "Release v1.1.0"
   git push && git push --tags
   ```

3. **Users update via:**
   ```
   /plugin update larouex-fullstack-builder
   ```

### Version Pinning

Users can pin to specific versions:

```
/plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin@v1.0.0
```

## Troubleshooting

### Plugin Not Found

**Issue:** `/plugin marketplace add` returns "not found"

**Solutions:**
- Verify repository is **public**
- Confirm `.claude-plugin/marketplace.json` exists at repo root
- Check repository URL is correct
- Wait a few minutes (GitHub API caching)

### Commands Not Working

**Issue:** Installed plugin but commands don't appear

**Solutions:**
- Verify `.claude/commands/` directory structure
- Check command files use `.md` extension
- Restart Claude Code session
- Run `/plugin list` to confirm installation

### Agents Not Referenced

**Issue:** Commands run but don't invoke agents

**Solutions:**
- Verify `.claude/agents/` directory structure
- Check agent files use `.md` extension
- Ensure commands reference agents correctly
- Agent invocation is automatic based on command prompts

### Marketplace.json Invalid

**Issue:** Plugin installs but doesn't appear in marketplace

**Solutions:**
- Validate JSON syntax (use https://jsonlint.com)
- Check all required fields are present
- Verify file is named exactly `marketplace.json`
- Confirm file is in `.claude-plugin/` directory

## Example: Complete Setup

Here's a complete example workflow:

```bash
# 1. In your plugin project directory
cd /Users/larrywjordanjr/Projects/larouex-website

# 2. Ensure all plugin files are ready
ls -la .claude-plugin/
ls -la .claude/

# 3. Initialize and push to GitHub
git init
git add .claude-plugin/ .claude/ docs/ README.md
git commit -m "Initial release: Full-Stack Website Builder v1.0.0"
git remote add origin https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
git branch -M main
git push -u origin main

# 4. Tag the release
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0

# 5. In another project, install the plugin
# (In Claude Code for the other project)
/plugin marketplace add LarouexNonprofitConsulting/larouex-fullstack-plugin
/plugin

# 6. Start using commands
/scaffold-nextjs
```

## Best Practices

### 1. Semantic Versioning

Use [SemVer](https://semver.org/) for versions:
- **1.0.0** → Initial release
- **1.1.0** → New features (backwards compatible)
- **1.0.1** → Bug fixes
- **2.0.0** → Breaking changes

### 2. Changelog

Maintain a `CHANGELOG.md` in your repository:

```markdown
# Changelog

## [1.1.0] - 2025-10-15
### Added
- New `/add-chat` command for real-time chat
- Support for WebSocket integration

### Fixed
- Azure deployment script issues

## [1.0.0] - 2025-10-12
### Added
- Initial release with 81 commands and 12 agents
```

### 3. Documentation

Provide comprehensive docs:
- `README.md` - Quick start and overview
- `CLAUDE.md` - Architecture and agent details
- `docs/` - Detailed command documentation
- GitHub Wiki - Tutorials and examples

### 4. Testing

Before each release:
- Test all commands in a fresh project
- Verify agents are invoked correctly
- Check deployment workflows
- Validate all documentation links

### 5. Community

Enable community features:
- GitHub Issues for bug reports
- GitHub Discussions for questions
- Pull requests for contributions
- Clear contribution guidelines

## Sharing Your Plugin

### GitHub README Badge

Add to your README.md:

```markdown
## Installation

Install this plugin in any Claude Code project:

\`\`\`
/plugin marketplace add LarouexNonprofitConsulting/larouex-fullstack-plugin
\`\`\`

Or install directly:

\`\`\`
/plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
\`\`\`
```

### Social Sharing

Share your plugin:
- Dev.to article
- X/Twitter announcement
- LinkedIn post
- Reddit (r/webdev, r/nextjs)
- Discord communities

### Example Announcement

```
🚀 Launching Full-Stack Website Builder for Claude Code!

Build production-ready Next.js websites with 81 commands and 12 specialized agents:

✅ Azure & Railway deployment
✅ Bootstrap 5 integration
✅ Automated code review
✅ Quality gates before production
✅ Comprehensive testing utilities

Install: /plugin marketplace add LarouexNonprofitConsulting/larouex-fullstack-plugin

GitHub: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin

#ClaudeCode #NextJS #WebDev #Azure #Railway
```

## Support and Maintenance

### User Support

Provide support through:
- GitHub Issues - Bug reports and feature requests
- GitHub Discussions - Q&A and community help
- Documentation - Comprehensive guides
- Examples - Real-world use cases

### Maintenance Checklist

**Monthly:**
- [ ] Review and respond to issues
- [ ] Update dependencies in templates
- [ ] Test commands with latest Next.js version
- [ ] Update documentation

**Quarterly:**
- [ ] Major feature additions
- [ ] Performance optimizations
- [ ] Security audits
- [ ] Refactor agents and commands

**Yearly:**
- [ ] Major version release
- [ ] Architecture review
- [ ] Technology stack updates
- [ ] Community survey

## Next Steps

1. **Push to GitHub** - Get your plugin online
2. **Test Installation** - Verify in another project
3. **Create Documentation** - Write comprehensive guides
4. **Add Screenshots** - Visual examples
5. **Announce** - Share with community
6. **Gather Feedback** - Improve based on usage
7. **Iterate** - Regular updates and improvements

## Resources

- [Claude Code Plugin Documentation](https://docs.claude.com/plugins)
- [Marketplace Format Specification](https://docs.claude.com/plugins/marketplace)
- [Plugin Development Guide](https://docs.claude.com/plugins/development)
- [Example Plugins](https://github.com/topics/claude-code-plugin)

## Support

- **Issues**: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues
- **Documentation**: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/wiki
- **Email**: [your-email@example.com]

---

**Your Plugin is Ready!** Follow this guide to share your Full-Stack Website Builder with the Claude Code community.
