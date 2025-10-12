# Contributing to Larouex Full-Stack Plugin

Thank you for your interest in contributing to the Larouex Full-Stack Plugin! This document provides guidelines and instructions for contributing.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Contribution Workflow](#contribution-workflow)
- [Style Guidelines](#style-guidelines)
- [Commit Messages](#commit-messages)
- [Pull Request Process](#pull-request-process)

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inspiring community for all. Please be respectful and constructive in your interactions.

### Our Standards

- Use welcoming and inclusive language
- Be respectful of differing viewpoints and experiences
- Gracefully accept constructive criticism
- Focus on what is best for the community
- Show empathy towards other community members

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues to avoid duplicates.

When creating a bug report, include:
- Clear, descriptive title
- Steps to reproduce the issue
- Expected vs actual behavior
- Environment details (OS, Claude Code version, etc.)
- Error messages and logs
- Screenshots if applicable

Use the [Bug Report Template](.github/ISSUE_TEMPLATE/bug_report.md).

### Suggesting Features

Feature suggestions are welcome! Please use the [Feature Request Template](.github/ISSUE_TEMPLATE/feature_request.md).

Include:
- Clear description of the feature
- Why this feature would be useful
- Potential implementation approach
- Examples of usage

### Improving Agents

To suggest improvements to existing agents, use the [Agent Improvement Template](.github/ISSUE_TEMPLATE/agent_improvement.md).

### Contributing Code

You can contribute by:
- Adding new commands
- Improving existing commands
- Enhancing agents
- Fixing bugs
- Improving documentation
- Adding tests
- Optimizing performance

## Development Setup

### Prerequisites

- Node.js 20+
- Claude Code 2.0.13+
- Git
- Code editor (VS Code recommended)

### Getting Started

1. **Fork the repository**
   ```bash
   # Click the "Fork" button on GitHub
   ```

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/larouex-fullstack-plugin.git
   cd larouex-fullstack-plugin
   ```

3. **Add upstream remote**
   ```bash
   git remote add upstream https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin.git
   ```

4. **Install in Claude Code**
   ```bash
   # Link to your Claude plugins directory
   ln -s $(pwd) ~/.claude/plugins/larouex-fullstack-plugin-dev
   ```

5. **Test your setup**
   ```bash
   # Start Claude Code and verify commands load
   claude
   # Type / to see commands
   ```

## Contribution Workflow

### 1. Create a Branch

```bash
# Update your main branch
git checkout main
git pull upstream main

# Create feature branch
git checkout -b feature/your-feature-name

# Or for bug fixes
git checkout -b fix/bug-description
```

### 2. Make Your Changes

#### Adding a New Command

1. Create command file:
   ```bash
   touch .claude/commands/your-command.md
   ```

2. Write the command prompt:
   ```markdown
   Brief description of what this command does.

   ## Purpose
   Detailed explanation...

   ## What it Creates
   - File 1
   - File 2

   ## Technologies
   - Technology 1
   - Technology 2

   ## Instructions
   Step-by-step implementation details...
   ```

3. Test the command:
   ```bash
   # In Claude Code
   /your-command
   ```

4. Update documentation:
   - Add to README.md
   - Update CHANGELOG.md

#### Improving an Agent

1. Locate agent file:
   ```bash
   # Agents are in .claude/agents/
   ls .claude/agents/
   ```

2. Edit the agent prompt:
   - Add new capabilities
   - Improve existing guidance
   - Add examples
   - Update best practices

3. Test the agent:
   - Test with real use cases
   - Verify responses are helpful
   - Check for accuracy

#### Fixing a Bug

1. Write a test that reproduces the bug (if applicable)
2. Fix the bug
3. Verify the test passes
4. Test manually
5. Document the fix in CHANGELOG.md

### 3. Test Your Changes

```bash
# Test the specific command/agent
# In Claude Code:
/your-command

# For code review
/review-code

# Verify no new issues introduced
```

### 4. Commit Your Changes

Follow our [commit message guidelines](#commit-messages):

```bash
git add .
git commit -m "feat: add new command for X"
```

### 5. Push to Your Fork

```bash
git push origin feature/your-feature-name
```

### 6. Create Pull Request

1. Go to GitHub
2. Click "New Pull Request"
3. Select your branch
4. Fill out the [PR template](.github/PULL_REQUEST_TEMPLATE.md)
5. Submit the PR

## Style Guidelines

### Command Style

- Use clear, descriptive command names
- Follow naming convention: `/verb-noun` (e.g., `/add-page`, `/deploy-azure`)
- Provide detailed instructions
- Include examples
- Consider edge cases
- Handle errors gracefully

### Agent Style

- Write in a helpful, professional tone
- Provide step-by-step guidance
- Include code examples
- Reference best practices
- Consider different skill levels
- Mention common pitfalls

### Code Examples

When including code in commands/agents:

```typescript
// ✓ Good: Clear, well-commented, follows best practices
interface UserProps {
  name: string;
  email: string;
}

export function UserCard({ name, email }: UserProps) {
  return (
    <div className="card">
      <h3>{name}</h3>
      <p>{email}</p>
    </div>
  );
}
```

```typescript
// ✗ Bad: No types, no structure
function Card(props) {
  return <div>{props.name}{props.email}</div>
}
```

### Documentation Style

- Use clear, concise language
- Include examples
- Format with markdown
- Add code blocks with syntax highlighting
- Use bullet points for lists
- Include screenshots when helpful

## Commit Messages

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- **feat**: New feature
- **fix**: Bug fix
- **docs**: Documentation changes
- **style**: Code style changes (formatting, etc.)
- **refactor**: Code refactoring
- **test**: Adding tests
- **chore**: Maintenance tasks

### Examples

```bash
# Adding a new command
git commit -m "feat(commands): add /deploy-railway-staging command"

# Fixing a bug
git commit -m "fix(agents): correct Azure Functions agent template path"

# Updating documentation
git commit -m "docs(readme): update installation instructions"

# Improving an agent
git commit -m "feat(agents): enhance frontend agent with Tailwind support"
```

### Scope

Use these scopes:
- `commands` - For command changes
- `agents` - For agent changes
- `docs` - For documentation
- `workflows` - For GitHub Actions
- `config` - For configuration files

## Pull Request Process

### Before Submitting

- [ ] Run `/review-code` on your changes
- [ ] Test your changes thoroughly
- [ ] Update documentation
- [ ] Update CHANGELOG.md
- [ ] Fill out PR template completely
- [ ] Ensure CI passes

### PR Requirements

1. **Descriptive Title**: Clear and concise
2. **Detailed Description**: What, why, and how
3. **Type of Change**: Bug fix, feature, etc.
4. **Testing**: Describe tests performed
5. **Code Review**: Run `/review-code`
6. **Documentation**: All docs updated
7. **Breaking Changes**: Clearly noted

### Review Process

1. **Automated Checks**: GitHub Actions will run validation
2. **Code Review**: Maintainers will review your code
3. **Feedback**: Address any requested changes
4. **Approval**: Once approved, PR will be merged

### After Merge

- Your contribution will be included in the next release
- You'll be credited in CHANGELOG.md
- Thank you for contributing!

## Questions?

If you have questions:
- Open an issue with the "question" label
- Check existing documentation
- Review similar PRs for examples

## Recognition

Contributors are recognized in:
- CHANGELOG.md for each release
- GitHub contributors page
- Special mentions for significant contributions

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing to the Larouex Full-Stack Plugin! Your efforts help make web development with Claude Code better for everyone.
