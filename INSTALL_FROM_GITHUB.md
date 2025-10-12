# Install Plugin from GitHub - Claude Code 2.0

## Current Working Method: Manual Installation

Since Claude Code 2.0 may not have `/install-plugin` command yet, here's the manual installation method that definitely works:

### Step 1: Find Your Claude Code Plugins Directory

```bash
# Claude Code plugins are typically stored here:
~/.claude/plugins/

# Create it if it doesn't exist:
mkdir -p ~/.claude/plugins
```

### Step 2: Clone Your Plugin Repository

```bash
cd ~/.claude/plugins

git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

Your directory structure should now be:
```
~/.claude/plugins/
└── larouex-fullstack-plugin/
    ├── .claude-plugin/
    │   ├── plugin.json
    │   └── marketplace.json
    ├── .claude/
    │   ├── agents/           (12 agents)
    │   └── commands/         (81 commands)
    ├── README.md
    └── ...
```

### Step 3: Restart Claude Code

**In VSCode:**
1. Press `Cmd+Shift+P` (Mac) or `Ctrl+Shift+P` (Windows/Linux)
2. Type: "Reload Window"
3. Press Enter

**Or completely restart VSCode:**
- Close VSCode
- Reopen VSCode
- Open Claude Code

### Step 4: Verify Installation

In Claude Code, try typing:
```
/scaffold-nextjs
```

You should see the command autocomplete. If you see all 81 commands available, the plugin is installed!

### Step 5: Test a Command

```bash
# Create a test directory
mkdir ~/test-plugin
cd ~/test-plugin

# In Claude Code, run:
/scaffold-nextjs
```

## Alternative: Link Plugin from Your Projects Directory

If you want to develop and use the plugin simultaneously:

```bash
# Instead of cloning, create a symlink
cd ~/.claude/plugins
ln -s /Users/larrywjordanjr/Projects/larouex-website larouex-fullstack-plugin

# Now any changes you make to the plugin are immediately available
```

## Troubleshooting

### Issue 1: Commands Not Showing Up

**Solution 1: Check plugin directory structure**
```bash
ls -la ~/.claude/plugins/larouex-fullstack-plugin/.claude-plugin/
# Should show: plugin.json

ls -la ~/.claude/plugins/larouex-fullstack-plugin/.claude/
# Should show: agents/ commands/
```

**Solution 2: Verify plugin.json is valid**
```bash
cd ~/.claude/plugins/larouex-fullstack-plugin
cat .claude-plugin/plugin.json
# Should be valid JSON
```

**Solution 3: Check Claude Code recognizes plugins directory**
```bash
# Check if Claude Code settings point to the right location
# In VSCode: Settings → Search for "Claude Code" → Check plugins path
```

### Issue 2: Plugin Not Loading

**Try these steps:**
1. Close all Claude Code instances
2. Delete and re-clone the plugin:
   ```bash
   cd ~/.claude/plugins
   rm -rf larouex-fullstack-plugin
   git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
   ```
3. Restart VSCode completely (not just reload window)
4. Open Claude Code and try `/scaffold-nextjs`

### Issue 3: "Claude Code doesn't recognize .claude directory"

**Check your plugin.json format:**
```json
{
  "name": "larouex-fullstack-builder",
  "version": "1.0.0",
  "description": "...",
  "agents": [],
  "commands": []
}
```

The `agents` and `commands` arrays should be empty - Claude Code auto-discovers from the directories.

### Issue 4: Permission Issues

```bash
# Fix permissions
chmod -R 755 ~/.claude/plugins/larouex-fullstack-plugin
```

## Check Claude Code Version

Make sure you have Claude Code 2.0.13 or higher:

```bash
# In VSCode, check the Claude Code extension version
# Extensions → Claude Code → Check version number
```

Your plugin requires `>=2.0.13` (specified in plugin.json).

## Update Plugin to Latest Version

```bash
cd ~/.claude/plugins/larouex-fullstack-plugin
git pull origin main

# Restart Claude Code
```

## Uninstall Plugin

```bash
# Remove the plugin directory
rm -rf ~/.claude/plugins/larouex-fullstack-plugin

# Restart Claude Code
```

## Development Workflow

If you're developing the plugin:

```bash
# Work in your original directory
cd /Users/larrywjordanjr/Projects/larouex-website

# Make changes to agents or commands
# Changes are immediately available if you used symlink method
# Or commit and pull if you cloned

# Test changes
# Reload Claude Code window in VSCode
```

## Expected Result

After successful installation, you should have access to:

**12 Agents:**
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
- code-review-agent

**81 Commands:**
- All scaffold commands (/scaffold-azure-full, etc.)
- All add commands (/add-page, /add-component, etc.)
- All review commands (/review-code, etc.)
- All deploy commands (/deploy-azure-production, etc.)
- And 70+ more commands

## Quick Verification Checklist

- [ ] Plugin cloned to `~/.claude/plugins/larouex-fullstack-plugin/`
- [ ] Directory structure looks correct (`.claude-plugin/`, `.claude/agents/`, `.claude/commands/`)
- [ ] VSCode reloaded/restarted
- [ ] Claude Code version >= 2.0.13
- [ ] Can see `/scaffold-nextjs` in autocomplete
- [ ] Command executes successfully

## Support

If you continue having issues:
1. Check: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues
2. Create an issue with:
   - Claude Code version
   - OS (Mac/Windows/Linux)
   - Error messages
   - What you tried

---

**The manual clone method should work 100% of the time with Claude Code 2.0+**
