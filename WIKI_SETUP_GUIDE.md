# GitHub Wiki Setup Guide

This guide explains how to set up and maintain the GitHub Wiki for the Full-Stack Website Builder plugin.

## What is a GitHub Wiki?

GitHub Wikis provide a way to create comprehensive documentation for your project. Unlike README files, wikis:
- Support multiple pages with navigation
- Allow in-browser editing
- Have their own Git repository
- Support markdown formatting
- Can be cloned and edited locally

## Overview

The wiki includes:
- **20 main documentation pages**
- **12 individual agent pages**
- **10 command category pages**
- **Special pages**: Sidebar and Footer
- **Total**: 42+ markdown files

## Step 1: Enable GitHub Wiki

### Enable Wiki on Repository

1. Go to your GitHub repository:
   ```
   https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
   ```

2. Click on **Settings** tab

3. Scroll down to **Features** section

4. Check the box for **Wikis**

5. Click **Save**

6. A **Wiki** tab will now appear in your repository navigation

## Step 2: Initialize the Wiki

### Create the First Page

1. Click the **Wiki** tab

2. Click **Create the first page**

3. Title: `Home`

4. Add some placeholder content:
   ```markdown
   # Welcome
   
   This wiki is being set up. Please check back soon!
   ```

5. Click **Save Page**

This initializes the wiki Git repository.

## Step 3: Clone the Wiki Repository

### Get the Wiki Repository URL

The wiki has its own Git repository separate from your main repo:

```
https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.wiki.git
```

### Clone Locally

```bash
# Navigate to where you want to clone the wiki
cd ~/projects

# Clone the wiki repository
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.wiki.git

# Enter the wiki directory
cd larouex-fullstack-plugin.wiki
```

## Step 4: Copy Wiki Files

### Copy from Plugin to Wiki Repository

All wiki markdown files are located in the `wiki/` directory of this plugin.

```bash
# Assuming you're in the wiki repository directory
# and the plugin is at ~/projects/larouex-website

# Copy all wiki files
cp ~/projects/larouex-website/wiki/*.md .

# Verify files were copied
ls -la
```

You should see all wiki markdown files:
- Home.md
- Installation.md
- Quick-Start.md
- Agents-Overview.md
- [All other .md files]
- _Sidebar.md
- _Footer.md

### File Naming Convention

GitHub Wiki uses specific naming conventions:
- **Spaces** in page names become **dashes** in file names
- Example: "Quick Start" page → `Quick-Start.md` file
- Special pages start with underscore: `_Sidebar.md`, `_Footer.md`

## Step 5: Commit and Push to GitHub Wiki

### Add and Commit Files

```bash
# Check status
git status

# Add all markdown files
git add *.md

# Commit with descriptive message
git commit -m "Add comprehensive wiki documentation

- Home page with navigation
- Installation guide
- Quick start tutorials
- 12 agent pages
- Command documentation
- Platform guides
- Troubleshooting and FAQ
- Sidebar and footer navigation"

# Push to GitHub
git push origin master
```

**Note**: Wiki repositories use `master` as the default branch, not `main`.

### Verify Upload

1. Go to your repository's Wiki tab on GitHub
2. You should see all pages in the sidebar
3. Click through pages to verify content displays correctly

## Step 6: Configure Wiki Settings

### Enable Features

In repository Settings → Features:
- ✅ **Wikis** - Already enabled
- ✅ **Issues** - For bug reports
- ✅ **Discussions** - For community questions

### Set Permissions

In repository Settings → General:
- **Wiki access**: Restrict editing to collaborators
- This prevents spam and maintains quality

## Step 7: Customize the Wiki

### Update Sidebar Navigation

The `_Sidebar.md` file creates navigation in the left sidebar.

**Current structure:**
```markdown
### Full-Stack Website Builder Wiki

**Getting Started**
- [Home](Home)
- [Installation](Installation)
- [Quick Start](Quick-Start)

**Agents** (12 total)
...
```

**To modify:**
1. Edit `_Sidebar.md` locally
2. Commit and push changes
3. Refresh wiki to see updates

### Update Footer

The `_Footer.md` file appears at the bottom of every page.

**Current footer:**
```markdown
**Full-Stack Website Builder - Claude Code Plugin**
Version: 1.0.0 | License: MIT
```

**To modify:**
1. Edit `_Footer.md` locally
2. Commit and push changes

## Step 8: Link Wiki from README

### Add Wiki Link to Main README

In your main repository `README.md`, add a prominent link to the wiki:

```markdown
## Documentation

📚 **[Visit the Full Documentation Wiki](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/wiki)**

Our comprehensive wiki includes:
- Installation guides
- 12 specialized agent documentation
- 81 command references
- Platform-specific guides (Azure & Railway)
- Examples and tutorials
```

### Add Badge

Add a documentation badge to the top of README:

```markdown
[![Documentation](https://img.shields.io/badge/docs-wiki-blue)](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/wiki)
```

## Maintaining the Wiki

### Updating Content

**Method 1: Edit on GitHub (Quick Changes)**

1. Navigate to wiki page on GitHub
2. Click **Edit** button
3. Make changes
4. Add commit message
5. Click **Save Page**

**Method 2: Edit Locally (Major Updates)**

1. Clone wiki repository (if not already done)
2. Edit markdown files
3. Commit and push changes

```bash
cd larouex-fullstack-plugin.wiki

# Edit files
vim Installation.md

# Commit changes
git add Installation.md
git commit -m "Update installation instructions for v1.1"
git push origin master
```

### Syncing with Plugin Repository

Keep the `wiki/` directory in your plugin repository in sync:

```bash
# In your plugin repository
cd ~/projects/larouex-website

# Copy updated files from wiki repo
cp ~/projects/larouex-fullstack-plugin.wiki/*.md wiki/

# Commit to plugin repository
git add wiki/
git commit -m "Sync wiki documentation"
git push origin main
```

This ensures the wiki source files are backed up in the main repository.

### Version Updates

When releasing a new version:

1. Update `Changelog.md` with new version
2. Update version number in `_Footer.md`
3. Update any changed commands or features
4. Commit and push changes

## Wiki Best Practices

### Content Organization

1. **Home Page**: Overview and navigation hub
2. **Getting Started**: Installation, Quick Start, FAQ
3. **Reference**: Agents, Commands
4. **Guides**: Workflows, Platform-specific guides
5. **Resources**: Examples, Troubleshooting, Contributing

### Writing Style

- **Clear headings**: Use H2 (##) for main sections
- **Code blocks**: Use triple backticks with language
- **Links**: Link between related wiki pages
- **Examples**: Include practical examples
- **Tables**: Use for comparisons and quick reference

### Markdown Tips

**Internal Links:**
```markdown
[Link to Installation](Installation)
```

**External Links:**
```markdown
[GitHub](https://github.com)
```

**Code Blocks:**
```markdown
```bash
npm install
```
```

**Tables:**
```markdown
| Column 1 | Column 2 |
|----------|----------|
| Data     | Data     |
```

### Images

To add images to wiki:

1. Create `images/` directory in wiki repository
2. Add images
3. Reference in markdown:
   ```markdown
   ![Alt text](images/screenshot.png)
   ```

## Troubleshooting

### Wiki Not Showing Up

**Problem**: Wiki tab doesn't appear

**Solution**:
1. Go to repository Settings
2. Enable Wikis in Features
3. Refresh browser

### Pages Not Linking

**Problem**: Links between pages broken

**Solution**:
- Use page name without `.md` extension
- Replace spaces with dashes
- Example: `[Quick Start](Quick-Start)` not `[Quick Start](Quick-Start.md)`

### Sidebar Not Appearing

**Problem**: Sidebar doesn't show

**Solution**:
1. Ensure file is named exactly `_Sidebar.md`
2. Check file is committed and pushed
3. Refresh browser with hard reload (Cmd+Shift+R / Ctrl+Shift+F5)

### Images Not Loading

**Problem**: Images don't display

**Solution**:
1. Verify images are in wiki repository
2. Check image path is correct
3. Use relative paths: `images/file.png` not `/images/file.png`

## Advanced: Automation

### Automated Sync Script

Create a script to sync wiki changes:

```bash
#!/bin/bash
# sync-wiki.sh

PLUGIN_DIR="$HOME/projects/larouex-website"
WIKI_DIR="$HOME/projects/larouex-fullstack-plugin.wiki"

# Copy from plugin to wiki
echo "Syncing wiki files..."
cp "$PLUGIN_DIR/wiki/"*.md "$WIKI_DIR/"

cd "$WIKI_DIR"

# Check if there are changes
if [[ -n $(git status -s) ]]; then
    echo "Changes detected. Committing..."
    git add *.md
    git commit -m "Auto-sync wiki from plugin repository"
    git push origin master
    echo "Wiki updated!"
else
    echo "No changes to sync."
fi
```

Make executable:
```bash
chmod +x sync-wiki.sh
```

Run to sync:
```bash
./sync-wiki.sh
```

### GitHub Actions (Optional)

You can't directly update wiki via GitHub Actions, but you can:
1. Generate documentation
2. Create a PR reminder to update wiki
3. Validate markdown files

## Resources

- [GitHub Wiki Documentation](https://docs.github.com/en/communities/documenting-your-project-with-wikis)
- [Markdown Guide](https://www.markdownguide.org/)
- [GitHub Flavored Markdown](https://github.github.com/gfm/)

## Next Steps

After setting up the wiki:

1. **Announce the wiki** in your README
2. **Share the wiki URL** with users
3. **Encourage contributions** via Issues/Discussions
4. **Keep it updated** with each release
5. **Monitor for spam** if wiki editing is public

## Support

For issues with wiki setup:
- [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
- [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)

---

**Wiki URL**: `https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/wiki`

**Last Updated**: 2025-10-12
