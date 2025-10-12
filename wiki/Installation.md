# Installation Guide

This guide will walk you through installing the Full-Stack Website Builder plugin for Claude Code.

## Prerequisites

Before installing the plugin, ensure you have the following installed:

### Required Software

#### 1. Node.js 20+
```bash
# Check if Node.js is installed
node --version

# Should output v20.0.0 or higher
```

**Install Node.js:**
- Download from [nodejs.org](https://nodejs.org/)
- Choose the LTS (Long Term Support) version
- Follow the installation wizard for your operating system

#### 2. Claude Code 2.0.13+
```bash
# Check Claude Code version
claude --version

# Should output 2.0.13 or higher
```

**Get Claude Code:**
- Visit [claude.ai](https://claude.ai)
- Sign up or log in to your account
- Download and install Claude Code CLI

#### 3. Git
```bash
# Check if Git is installed
git --version
```

**Install Git:**
- Download from [git-scm.com](https://git-scm.com/)
- Follow the installation instructions for your OS

### Platform-Specific Requirements

#### For Azure Features

If you plan to use Azure commands, you'll need:

**1. Azure Account**
- Sign up for a [free Azure account](https://azure.microsoft.com/free/)
- Get $200 in free credits for 30 days
- Free services for 12 months

**2. Azure CLI**
```bash
# Install Azure CLI
npm install -g azure-cli

# Verify installation
az --version

# Login to Azure
az login
```

**Alternative installation methods:**
- **macOS**: `brew install azure-cli`
- **Windows**: Download installer from [Microsoft](https://docs.microsoft.com/cli/azure/install-azure-cli-windows)
- **Linux**: Follow [installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli-linux)

#### For Railway Features

If you plan to use Railway commands, you'll need:

**1. Railway Account**
- Sign up at [railway.app](https://railway.app/)
- Free tier available (no credit card required)
- $5/month of usage included

**2. Railway CLI**
```bash
# Install Railway CLI
npm install -g @railway/cli

# Verify installation
railway --version

# Login to Railway
railway login
```

**Alternative installation:**
- **macOS**: `brew install railway`
- **Windows/Linux**: Use npm installation above

### Optional Tools

#### VS Code (Recommended)
- Download from [code.visualstudio.com](https://code.visualstudio.com/)
- Install recommended extensions:
  - ESLint
  - Prettier
  - TypeScript and JavaScript Language Features

#### GitHub Account
- Required for CI/CD workflows
- Sign up at [github.com](https://github.com/)

#### Docker (Optional)
- For local containerized development
- Download from [docker.com](https://www.docker.com/products/docker-desktop)

---

## Installation Methods

There are three ways to install the plugin:

### Method 1: Install from GitHub (Recommended)

This is the easiest and recommended method.

**Step 1: Open Claude Code**
```bash
claude
```

**Step 2: Run the install plugin command**

In Claude Code, type:
```
install plugin from https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
```

**Step 3: Wait for installation**

Claude Code will:
- Clone the repository
- Install the plugin
- Activate it automatically

**Step 4: Verify installation**

Type `/` to see available commands. You should see commands like:
- `/scaffold-azure-full`
- `/scaffold-railway-full`
- `/add-page`
- etc.

---

### Method 2: Manual Installation

If you prefer manual control or the automatic method fails:

**Step 1: Clone the repository**
```bash
cd ~/Downloads
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

**Step 2: Copy to Claude Code plugins directory**

**macOS/Linux:**
```bash
# Create plugins directory if it doesn't exist
mkdir -p ~/.claude/plugins/

# Copy the plugin
cp -r larouex-fullstack-plugin ~/.claude/plugins/
```

**Windows (PowerShell):**
```powershell
# Create plugins directory if it doesn't exist
New-Item -ItemType Directory -Force -Path $env:USERPROFILE\.claude\plugins

# Copy the plugin
Copy-Item -Recurse larouex-fullstack-plugin $env:USERPROFILE\.claude\plugins\
```

**Step 3: Verify the files**
```bash
# macOS/Linux
ls ~/.claude/plugins/larouex-fullstack-plugin

# Windows (PowerShell)
dir $env:USERPROFILE\.claude\plugins\larouex-fullstack-plugin
```

You should see:
```
.claude/
  ├── agents/
  └── commands/
README.md
LICENSE
CHANGELOG.md
```

**Step 4: Restart Claude Code**
```bash
# Exit Claude Code
exit

# Start Claude Code again
claude
```

**Step 5: Verify installation**

Type `/` to see available commands.

---

### Method 3: Install via Git

If you have Claude Code configured to use Git:

**Step 1: Navigate to plugins directory**
```bash
cd ~/.claude/plugins
```

**Step 2: Clone the repository**
```bash
git clone https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
```

**Step 3: Restart Claude Code**
```bash
exit
claude
```

---

## Verifying Installation

After installation, verify everything is working correctly:

### 1. Check Available Commands

In Claude Code, type:
```
/
```

You should see a list of commands including:
- Scaffolding commands (`/scaffold-*`)
- Azure commands (`/add-api-azure`, `/deploy-azure-*`)
- Railway commands (`/add-api-railway`, `/deploy-railway-*`)
- Development commands (`/add-page`, `/add-component`, `/add-form`)
- Review commands (`/review-code`, `/review-before-deploy`)

### 2. Test a Simple Command

Try a non-destructive command:
```
/add-component
```

Claude should recognize the command and ask for details about the component you want to create.

### 3. Check Agent Availability

Ask Claude:
```
What agents are available in the Full-Stack Website Builder plugin?
```

Claude should list all 12 agents:
1. Frontend Development Agent
2. Forms Workflow Agent
3. Content & SEO Agent
4. Azure Serverless Agent
5. DevOps Azure Agent
6. DevOps Railway Agent
7. Monitoring & Observability Agent
8. Testing & Quality Agent
9. Security & Production Agent
10. Accessibility & Compliance Agent
11. Authentication Agent
12. Code Review Agent

### 4. Verify File Structure

Check that the plugin files are in the correct location:

```bash
# macOS/Linux
ls -la ~/.claude/plugins/larouex-fullstack-plugin/.claude/

# Windows (PowerShell)
dir $env:USERPROFILE\.claude\plugins\larouex-fullstack-plugin\.claude\
```

You should see:
```
agents/
commands/
```

---

## Troubleshooting Installation

### Issue: Plugin Not Found

**Symptoms:**
- Commands don't appear when typing `/`
- Claude doesn't recognize plugin commands

**Solutions:**

**1. Check file location**
```bash
# Verify plugin is in correct directory
ls ~/.claude/plugins/larouex-fullstack-plugin
```

**2. Check file permissions**
```bash
# Ensure files are readable
chmod -R 755 ~/.claude/plugins/larouex-fullstack-plugin
```

**3. Restart Claude Code**
```bash
exit
claude
```

**4. Reinstall the plugin**

Remove and reinstall:
```bash
rm -rf ~/.claude/plugins/larouex-fullstack-plugin
# Then follow installation method 1 or 2 again
```

---

### Issue: Commands Not Working

**Symptoms:**
- Commands appear but don't execute
- Errors when running commands

**Solutions:**

**1. Update Claude Code**
```bash
# Check version
claude --version

# Update if needed (method varies by installation)
```

**2. Check command files**
```bash
# Verify .md files exist in commands directory
ls ~/.claude/plugins/larouex-fullstack-plugin/.claude/commands/
```

**3. Check for syntax errors**

Open a command file and verify it's properly formatted:
```bash
cat ~/.claude/plugins/larouex-fullstack-plugin/.claude/commands/add-page.md
```

---

### Issue: Azure CLI Not Working

**Symptoms:**
- Azure commands fail
- Authentication errors

**Solutions:**

**1. Verify Azure CLI installation**
```bash
az --version
```

**2. Login to Azure**
```bash
az login
```

This opens a browser window for authentication.

**3. Set correct subscription**
```bash
# List subscriptions
az account list

# Set the subscription you want to use
az account set --subscription "YOUR_SUBSCRIPTION_ID"
```

**4. Verify credentials**
```bash
az account show
```

---

### Issue: Railway CLI Not Working

**Symptoms:**
- Railway commands fail
- Authentication errors

**Solutions:**

**1. Verify Railway CLI installation**
```bash
railway --version
```

**2. Login to Railway**
```bash
railway login
```

This opens a browser window for authentication.

**3. Link to project**
```bash
# In your project directory
railway link
```

**4. Verify login**
```bash
railway whoami
```

---

### Issue: Node.js Version Mismatch

**Symptoms:**
- TypeScript errors
- Build failures
- Module not found errors

**Solutions:**

**1. Check Node.js version**
```bash
node --version
```

**2. Update Node.js if needed**
- Download latest LTS from [nodejs.org](https://nodejs.org/)
- Or use nvm (Node Version Manager):

```bash
# Install nvm (macOS/Linux)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Install latest LTS
nvm install --lts

# Use the LTS version
nvm use --lts
```

---

## Updating the Plugin

To update to the latest version:

### Automatic Update (GitHub Installation)

If you installed via GitHub:
```
update plugin larouex-fullstack-plugin
```

### Manual Update

**Step 1: Navigate to plugin directory**
```bash
cd ~/.claude/plugins/larouex-fullstack-plugin
```

**Step 2: Pull latest changes**
```bash
git pull origin main
```

**Step 3: Restart Claude Code**
```bash
exit
claude
```

### Check Current Version

```bash
cat ~/.claude/plugins/larouex-fullstack-plugin/CHANGELOG.md
```

Look for the version number at the top.

---

## Uninstalling the Plugin

If you need to uninstall:

**Step 1: Remove plugin directory**
```bash
rm -rf ~/.claude/plugins/larouex-fullstack-plugin
```

**Step 2: Restart Claude Code**
```bash
exit
claude
```

---

## Post-Installation Setup

After installing the plugin, you may want to configure your environment:

### 1. Configure Azure (if using Azure commands)

```bash
# Login
az login

# Set subscription
az account set --subscription "YOUR_SUBSCRIPTION"

# Create resource group
az group create --name myResourceGroup --location eastus
```

### 2. Configure Railway (if using Railway commands)

```bash
# Login
railway login

# Create new project
railway init

# Or link existing project
railway link
```

### 3. Configure Git

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your.email@example.com"
```

### 4. Configure VS Code (optional)

Install recommended extensions:
- ESLint
- Prettier - Code formatter
- TypeScript and JavaScript Language Features
- Azure Tools (if using Azure)
- Railway (if using Railway)

---

## Next Steps

Now that you have the plugin installed:

1. **Read the [Quick Start Guide](Quick-Start)** - Build your first project in 5 minutes
2. **Explore [Agents Overview](Agents-Overview)** - Learn about the 12 specialized agents
3. **Review [Commands Overview](Commands-Overview)** - See all 81 commands
4. **Check out [Examples](Examples)** - Real-world tutorials and examples
5. **Join the Community** - [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)

---

## Getting Help

If you encounter issues during installation:

1. **Check [Troubleshooting](Troubleshooting)** - Common issues and solutions
2. **Review [FAQ](FAQ)** - Frequently asked questions
3. **Report Issues** - [GitHub Issues](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/issues)
4. **Ask Questions** - [GitHub Discussions](https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin/discussions)

---

**Installation complete?** Head over to the [Quick Start Guide](Quick-Start) to build your first project!
