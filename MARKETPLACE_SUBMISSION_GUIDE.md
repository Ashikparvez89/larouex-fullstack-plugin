# Claude Code Marketplace Submission Guide

## Overview

This guide explains how to submit the Full-Stack Website Builder plugin to the Claude Code Marketplace for easy installation by users.

## Prerequisites

- [x] GitHub repository published: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
- [x] Plugin version tagged: v1.0.0
- [x] All documentation complete (README, Wiki, CHANGELOG)
- [x] Plugin manifest files created (plugin.json, marketplace.json)
- [ ] Screenshots created (need 3 screenshots)
- [ ] Icon created (need plugin icon)

## Installation Methods for Users

Once approved on the marketplace, users can install via:

### Method 1: Claude Code Marketplace (Easiest)

```bash
# In Claude Code
/install larouex-fullstack-builder

# Or browse marketplace
/marketplace
# Search for "Full-Stack Website Builder"
# Click "Install"
```

### Method 2: Direct URL Installation

```bash
# Install from GitHub URL
/install-plugin https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
```

### Method 3: Manual Installation (Advanced)

```bash
# Clone to Claude Code plugins directory
cd ~/.claude/plugins
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

## Marketplace Submission Process

### Step 1: Create Required Assets

#### Create Plugin Icon (Required)

Create `assets/icon.png`:
- Size: 512x512 pixels
- Format: PNG with transparency
- Design: Logo or representative icon
- Style: Professional, clean, recognizable

Suggested design:
- Next.js logo + Azure/Railway symbols
- Or: "FSB" monogram with gradient
- Or: Building blocks representing full-stack

#### Create Screenshots (Required - 3 minimum)

Create these in `assets/` directory:

**screenshot-scaffold.png**
- Show: `/scaffold-azure-full` command output
- Caption: "Scaffold complete project in seconds"
- Size: 1920x1080 or 1280x720

**screenshot-review.png**
- Show: `/review-code` output with findings
- Caption: "Automated code review catches issues"
- Size: 1920x1080 or 1280x720

**screenshot-deploy.png**
- Show: `/deploy-azure-production` with quality gates
- Caption: "Safe production deployment with gates"
- Size: 1920x1080 or 1280x720

### Step 2: Update Repository

```bash
# Commit marketplace files
cd /Users/larrywjordanjr/Projects/larouex-website
git add .claude-plugin/marketplace.json
git add assets/icon.png
git add assets/screenshot-*.png
git commit -m "Add marketplace assets for Claude Code"
git push origin main

# Tag marketplace-ready version
git tag -a v1.0.1 -m "Marketplace submission version"
git push origin v1.0.1
```

### Step 3: Submit to Marketplace

Visit: https://claude.ai/marketplace/submit (or equivalent submission form)

Fill out the submission form:

**Basic Information:**
- Plugin Name: `larouex-fullstack-builder`
- Display Name: `Full-Stack Website Builder`
- Author: `Larry W Jordan Jr`
- Publisher: `LarouexNonprofitConsulting`
- Version: `1.0.0`
- License: `MIT`

**Repository Information:**
- Repository URL: `https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin`
- Homepage: `https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin#readme`
- Documentation: `https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/wiki`
- Bug Reports: `https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues`

**Description:**
- Short: (from marketplace.json)
- Long: (from marketplace.json)

**Categories:** (select all that apply)
- [x] Web Development
- [x] Deployment
- [x] Full-Stack

**Keywords:**
nextjs, azure, railway, bootstrap, typescript, react, serverless, devops, code-review, quality-gates, accessibility, testing

**Assets:**
- Icon: Upload `assets/icon.png`
- Screenshots: Upload 3 screenshots

**Minimum Version:**
- Claude Code: `>=2.0.13`

**Support:**
- Support URL: `https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues`
- Documentation URL: `https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/wiki`

### Step 4: Testing Before Submission

Test the plugin installation process:

```bash
# Test Method 1: Direct GitHub install
claude plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin

# Verify installation
claude plugin list
# Should show: larouex-fullstack-builder (1.0.0)

# Test a command
/scaffold-nextjs

# Uninstall
claude plugin uninstall larouex-fullstack-builder
```

### Step 5: Review Checklist

Before submitting, verify:

**Plugin Structure:**
- [x] `.claude-plugin/plugin.json` exists and valid
- [x] `.claude-plugin/marketplace.json` exists and valid
- [x] `.claude/agents/` contains 12 agent files
- [x] `.claude/commands/` contains 81 command files
- [x] All agent files end with `-agent.md`
- [x] All command files end with `.md`

**Documentation:**
- [x] README.md comprehensive and up-to-date
- [x] CHANGELOG.md with version history
- [x] LICENSE file (MIT)
- [x] Wiki with 42+ pages
- [x] Installation guide in wiki
- [x] Examples and tutorials

**Assets:**
- [ ] Icon (512x512 PNG)
- [ ] 3 screenshots (1280x720 or larger)
- [ ] All assets in `assets/` directory

**Repository:**
- [x] Public GitHub repository
- [x] Latest version tagged (v1.0.0)
- [x] All files committed and pushed
- [x] Repository topics added
- [x] Repository description set

**Testing:**
- [ ] Plugin installs without errors
- [ ] All 81 commands accessible
- [ ] Sample commands execute successfully
- [ ] Documentation links work
- [ ] No broken links in README

## Approval Process

After submission:

1. **Initial Review (1-3 days)**
   - Automated checks for malicious code
   - Manifest validation
   - Asset verification

2. **Manual Review (3-7 days)**
   - Code quality review
   - Documentation review
   - Security audit
   - User experience evaluation

3. **Approval or Feedback (1-2 days)**
   - Approved: Plugin appears in marketplace
   - Feedback: Address issues and resubmit

4. **Publication**
   - Plugin listed in Claude Code Marketplace
   - Users can search and install
   - Download statistics tracked

## Post-Submission

Once approved:

### Update README Installation Section

```markdown
## Installation

### Option 1: Claude Code Marketplace (Recommended)

1. Open Claude Code
2. Run: `/install larouex-fullstack-builder`
3. Plugin automatically installs and activates

Or browse the marketplace:
```
/marketplace
```
Search for "Full-Stack Website Builder" and click Install.

### Option 2: Direct GitHub
...
```

### Monitor and Maintain

- Respond to GitHub Issues within 48 hours
- Update documentation as needed
- Release updates for bug fixes
- Add new features based on feedback
- Keep dependencies up-to-date

### Version Updates

When releasing new versions:

```bash
# Update version in plugin.json and marketplace.json
# Update CHANGELOG.md
# Commit changes
git add .
git commit -m "Release v1.1.0: [features]"
git push origin main

# Tag release
git tag -a v1.1.0 -m "Release v1.1.0"
git push origin v1.1.0

# Marketplace auto-detects new version
# Or manually submit update notification
```

## Troubleshooting Submission Issues

### Issue: "Invalid plugin.json"
**Solution:** Validate JSON syntax at https://jsonlint.com/

### Issue: "Missing required fields"
**Solution:** Ensure all required fields in marketplace.json are filled

### Issue: "Assets not found"
**Solution:** Verify assets paths are relative to repository root

### Issue: "Icon wrong format"
**Solution:** Convert to PNG 512x512, ensure transparency

### Issue: "Screenshots too small"
**Solution:** Minimum 1280x720, recommended 1920x1080

### Issue: "Repository not accessible"
**Solution:** Ensure repository is public, not private

### Issue: "Version mismatch"
**Solution:** Ensure plugin.json and marketplace.json versions match

## Support and Questions

- GitHub Issues: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues
- Wiki: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/wiki
- Email: [Your support email]

## Next Steps

1. [ ] Create plugin icon (512x512 PNG)
2. [ ] Create 3 screenshots (1920x1080)
3. [ ] Add assets to repository
4. [ ] Commit and push
5. [ ] Submit to Claude Code Marketplace
6. [ ] Wait for approval (1-2 weeks)
7. [ ] Update README with marketplace install
8. [ ] Announce on social media

---

**Current Status:** Ready for asset creation and submission
**Target Submission Date:** [Set your date]
**Expected Approval:** 2-3 weeks after submission
