# Simple Installation - 3 Steps

## What You Need
- VSCode with Claude Code extension (v2.0.13 or higher)
- Terminal/Command Prompt
- Git

## Installation (Takes 2 minutes)

### Step 1: Copy Plugin to Claude
Open terminal and run these **exact commands**:

**Mac/Linux:**
```bash
mkdir -p ~/.claude/plugins
cd ~/.claude/plugins
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

**Windows (PowerShell):**
```powershell
mkdir -Force $env:USERPROFILE\.claude\plugins
cd $env:USERPROFILE\.claude\plugins
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

**Verify the structure looks correct:**
```bash
# You should see commands/ and agents/ at the root level:
~/.claude/plugins/larouex-fullstack-plugin/
├── .claude-plugin/plugin.json
├── commands/          ✅ 81 command files
└── agents/            ✅ 12 agent files
```

### Step 2: Restart VSCode
- **Close VSCode completely** (don't just "Reload Window")
- Open VSCode again
- Open Claude Code

### Step 3: Test It
In Claude Code, type:
```
/scaffold
```

You should see autocomplete with:
- `/scaffold-nextjs`
- `/scaffold-azure-full`
- `/scaffold-railway-full`

**If you see these commands, installation successful!** ✅

## That's It!

If you see the commands, you're done. If not, try these:

### Quick Fix 1: Check the folder exists
```bash
# Mac/Linux
ls ~/.claude/plugins/larouex-fullstack-plugin/.claude-plugin/

# Windows
dir %USERPROFILE%\.claude\plugins\larouex-fullstack-plugin\.claude-plugin\
```

You should see `plugin.json`.

### Quick Fix 2: Use a symlink instead (for development)
```bash
# Mac/Linux
cd ~/.claude/plugins
ln -s /Users/larrywjordanjr/Projects/larouex-website larouex-fullstack-plugin

# Windows (as Administrator)
cd %USERPROFILE%\.claude\plugins
mklink /D larouex-fullstack-plugin C:\path\to\your\larouex-website
```

Then restart VSCode.

## Still Not Working?

1. Check Claude Code version: Go to Extensions → Claude Code → Should be 2.0.13 or higher
2. Check if `.claude-plugin/plugin.json` exists in the plugin folder
3. Try deleting and re-cloning:
   ```bash
   rm -rf ~/.claude/plugins/larouex-fullstack-plugin
   # Then repeat Step 1
   ```

## What You Get

After installation you'll have access to:
- **81 commands** (type `/` to see them all)
- **12 AI agents** (automatically used by commands)

Try:
- `/scaffold-nextjs` - Create new Next.js project
- `/add-component` - Add React component
- `/add-page` - Add new page
- `/review-code` - Review your code

## Need Help?

Create an issue: https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues

Tell me:
1. Your OS (Mac/Windows/Linux)
2. Claude Code version
3. What error you see
