# Quick Release Guide

Quick reference for releasing the Larouex Full-Stack Plugin to GitHub.

## Pre-Release Checklist

- [ ] All repository URLs updated to `LarouexNonprofitConsulting/larouex-fullstack-plugin`
- [ ] Version numbers consistent in plugin.json and package.json
- [ ] CHANGELOG.md updated
- [ ] README.md reflects all features
- [ ] All commands and agents tested
- [ ] No uncommitted changes

## Release Commands (Copy & Paste)

### 1. Commit All Changes
```bash
git add .
git commit -m "chore: prepare plugin for GitHub release"
```

### 2. Create GitHub Repository
- Go to: https://github.com/LarouexNonprofitConsulting
- Click "New repository"
- Name: `larouex-fullstack-plugin`
- Public repository
- Don't initialize with README

### 3. Push to GitHub
```bash
git remote add origin https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
git branch -M main
git push -u origin main
```

### 4. Create Release Tag
```bash
git tag -a v1.0.0 -m "Initial release - Full-Stack Website Builder Plugin"
git push origin v1.0.0
```

### 5. Verify Release
- Visit: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/releases
- Check automated release was created
- Verify release notes and artifacts

### 6. Test Installation
```bash
claude plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
```

## Share Your Release

```markdown
🎉 Excited to release the Larouex Full-Stack Plugin for Claude Code!

✨ Features:
- 81 specialized commands for Next.js development
- 12 expert AI agents
- Azure & Railway support
- Complete development lifecycle

📦 Install:
claude plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin

⭐ Star the repo: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
```

## Quick Links

- Repository: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
- Issues: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues
- Releases: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/releases

## Installation Methods

**Direct from GitHub (Recommended):**
```bash
claude plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
```

**Manual:**
```bash
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
cp -r larouex-fullstack-plugin ~/.claude/plugins/
```

**Git in Plugins:**
```bash
cd ~/.claude/plugins
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

## Future Releases

For subsequent releases:

```bash
# Update version in plugin.json and package.json
# Update CHANGELOG.md

git add .
git commit -m "chore: release v1.1.0"
git tag -a v1.1.0 -m "Release v1.1.0"
git push origin main
git push origin v1.1.0
```

GitHub Actions will automatically create the release!

## Need Help?

See full documentation in:
- `GITHUB_RELEASE_COMPLETE.md` - Complete setup details
- `.github/RELEASE_CHECKLIST.md` - Comprehensive checklist
- `.github/CONTRIBUTING.md` - Contribution guidelines
