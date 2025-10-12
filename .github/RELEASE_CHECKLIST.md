# Plugin Release Checklist

Use this checklist before releasing a new version of the plugin to GitHub.

## Pre-Release Validation

### Version & Documentation
- [ ] Version number updated in:
  - [ ] `.claude-plugin/plugin.json`
  - [ ] `package.json`
  - [ ] `README.md` badges
- [ ] CHANGELOG.md updated with all changes
- [ ] README.md reflects all new features
- [ ] All documentation is up to date

### Code Quality
- [ ] Run `/review-code` on all changes
- [ ] All Critical and High severity issues resolved
- [ ] No security vulnerabilities
- [ ] All tests pass (if applicable)

### Plugin Structure
- [ ] All commands are in `.claude/commands/` and working
- [ ] All agents are in `.claude/agents/` and working
- [ ] plugin.json has correct metadata
- [ ] marketplace.json is accurate
- [ ] All required directories exist:
  - [ ] `.claude/`
  - [ ] `.claude/agents/`
  - [ ] `.claude/commands/`
  - [ ] `.claude-plugin/`
  - [ ] `docs/` (if applicable)

### GitHub Configuration
- [ ] Repository URL correct in all files:
  - [ ] `.claude-plugin/plugin.json`
  - [ ] `package.json`
  - [ ] `README.md`
- [ ] Issue templates created in `.github/ISSUE_TEMPLATE/`
- [ ] Pull request template created
- [ ] GitHub Actions workflows configured
- [ ] LICENSE file present
- [ ] FUNDING.yml configured (optional)

### Testing
- [ ] Test basic commands work
- [ ] Test agents respond correctly
- [ ] Test on clean installation
- [ ] Test Azure-specific features (if applicable)
- [ ] Test Railway-specific features (if applicable)
- [ ] Test error handling

## Release Process

### 1. Create Git Tag
```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

### 2. Create GitHub Release
1. Go to GitHub repository
2. Click "Releases" → "Create a new release"
3. Select the tag you just created
4. Release title: `v1.0.0 - Full-Stack Website Builder Plugin`
5. Add release notes from CHANGELOG.md
6. Attach any additional files (if needed)
7. Check "Set as the latest release"
8. Publish release

### 3. Verify Installation
Test that users can install using:
```bash
# In Claude Code
claude plugin install https://github.com/LarouexNonprofitConsulting/larouex-fullstack-plugin
```

## Post-Release

### Announcements
- [ ] Update plugin marketplace listing (when available)
- [ ] Post announcement in relevant communities
- [ ] Update personal website/portfolio
- [ ] Share on social media (optional)

### Monitoring
- [ ] Monitor GitHub issues for bug reports
- [ ] Watch for installation problems
- [ ] Collect user feedback
- [ ] Plan next version improvements

## Version Numbering

Follow Semantic Versioning (SemVer):
- **MAJOR** (1.0.0): Breaking changes
- **MINOR** (0.1.0): New features, backward compatible
- **PATCH** (0.0.1): Bug fixes, backward compatible

## Release Notes Template

```markdown
## What's New in v1.0.0

### New Features
- Feature 1 description
- Feature 2 description

### New Commands
- `/command-1` - Description
- `/command-2` - Description

### New/Improved Agents
- Agent Name - Improvements

### Bug Fixes
- Fixed issue #123
- Fixed issue #456

### Breaking Changes
- Breaking change 1 (if any)

### Migration Guide
If there are breaking changes, provide migration instructions.

### Full Changelog
See [CHANGELOG.md](CHANGELOG.md) for complete details.
```

## Hotfix Process

If a critical bug is found after release:

1. Create hotfix branch: `git checkout -b hotfix/v1.0.1`
2. Fix the bug
3. Update version to 1.0.1 in all files
4. Update CHANGELOG.md
5. Test thoroughly
6. Merge to main
7. Create new release v1.0.1
8. Tag and push

## Common Issues During Release

### Issue: GitHub Actions fails validation
**Solution**: Run validation locally first:
```bash
# Check JSON files
cat .claude-plugin/plugin.json | jq empty
cat package.json | jq empty

# Verify directory structure
ls -R .claude/
```

### Issue: Users can't install plugin
**Solution**: Verify:
- Repository is public
- Release is published (not draft)
- Repository URL is correct
- plugin.json is valid

### Issue: Commands not showing up
**Solution**: Check:
- Commands are in `.claude/commands/`
- Files end with `.md` extension
- Files are not empty
- Proper markdown formatting

## Support

For questions about the release process:
- Open an issue on GitHub
- Check Claude Code documentation
- Review existing releases for reference
