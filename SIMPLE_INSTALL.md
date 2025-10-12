# Plugin Installation - THE CORRECT WAY

## What You Need
- VSCode with Claude Code extension (v2.0.13 or higher)
- Claude Code running

## Installation Method 1: From GitHub (Recommended for Users)

### Step 1: Add Marketplace
In Claude Code, run:
```
/plugin marketplace add LarouexNonprofitConsulting/larouex-fullstack-plugin
```

### Step 2: Install Plugin
```
/plugin install larouex-fullstack-builder
```

### Step 3: Verify
Type `/scaffold` and you should see:
- `/scaffold-nextjs`
- `/scaffold-azure-full`
- `/scaffold-railway-full`

**That's it!** ✅

---

## Installation Method 2: Local Development (For Plugin Developers)

If you're developing the plugin locally, use this method:

### Step 1: Clone the Repository
```bash
cd ~/Projects  # or wherever you want
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

### Step 2: Create Local Marketplace

Create the marketplace directory:
```bash
mkdir -p ~/.claude/marketplaces/local/.claude-plugin
```

Create a symlink to your plugin:
```bash
cd ~/.claude/marketplaces/local
ln -s /Users/YOU/Projects/larouex-fullstack-plugin larouex-website
```
**Important:** Replace `/Users/YOU/Projects/` with your actual path!

Create file: `~/.claude/marketplaces/local/.claude-plugin/marketplace.json`

```json
{
  "name": "local-dev",
  "owner": {
    "name": "Your Name",
    "url": "https://github.com/yourusername"
  },
  "description": "Local development marketplace",
  "plugins": [
    {
      "name": "larouex-fullstack-builder",
      "source": "./larouex-website"
    }
  ]
}
```

**Important:**
- `owner` must be an object with `name` field (required)
- `owner.url` is optional but recommended
- `source` must be a relative path starting with `./`

### Step 3: Add Local Marketplace
In Claude Code:
```
/plugin marketplace add ~/.claude/marketplaces/local
```

### Step 4: Install Plugin
```
/plugin install larouex-fullstack-builder@local-dev
```

### Step 5: Test Changes
When you make changes to the plugin:
```
/plugin uninstall larouex-fullstack-builder
/plugin install larouex-fullstack-builder@local-dev
```

---

## Verification

After installation, check:

1. **List installed plugins:**
   ```
   /plugin
   ```
   You should see "larouex-fullstack-builder" in the list

2. **Test a command:**
   ```
   /scaffold-nextjs
   ```

3. **See all commands:**
   Type `/` and browse - you'll see 81 new commands!

---

## Troubleshooting

### Plugin not showing up?

1. **Check Claude Code version:**
   - Go to Extensions → Claude Code
   - Must be v2.0.13 or higher

2. **Reinstall the plugin:**
   ```
   /plugin uninstall larouex-fullstack-builder
   /plugin install larouex-fullstack-builder
   ```

3. **Check the plugin directory structure:**
   ```bash
   ls ~/.claude/plugins/larouex-fullstack-builder/
   ```
   Should show:
   - `.claude-plugin/plugin.json`
   - `commands/` (81 files)
   - `agents/` (12 files)

4. **Restart VSCode:**
   - Close VSCode completely
   - Open again

### Commands not appearing?

The plugin uses the `/plugin` installation system. You **cannot** just copy files to `~/.claude/plugins/` - you MUST use `/plugin marketplace add` and `/plugin install`.

---

## What You Get

**81 Commands:**
- Scaffolding: `/scaffold-nextjs`, `/scaffold-azure-full`, `/scaffold-railway-full`
- Components: `/add-component`, `/add-page`, `/add-form`
- APIs: `/add-api-azure`, `/add-api-railway`
- Deploy: `/deploy-azure-production`, `/deploy-railway-production`
- Review: `/review-code`, `/review-security`, `/review-before-deploy`
- And 70+ more!

**12 AI Agents:**
Automatically invoked by commands for specialized tasks.

---

## The Problem with Old Installation Instructions

**❌ WRONG (doesn't work):**
```bash
# This doesn't actually install the plugin!
git clone https://github.com/.../plugin.git ~/.claude/plugins/plugin
```

**✅ CORRECT:**
```
/plugin marketplace add user/repo
/plugin install plugin-name
```

Claude Code's plugin system requires registration through the `/plugin` command. Simply copying files doesn't work.

---

## Need Help?

**GitHub Issues:** https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues

Include:
1. Your OS (Mac/Windows/Linux)
2. Claude Code version
3. Output of `/plugin` command
4. Error messages
