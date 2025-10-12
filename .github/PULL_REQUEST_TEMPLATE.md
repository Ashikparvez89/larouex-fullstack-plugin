# Pull Request

## Description

Please provide a brief description of the changes in this PR.

## Type of Change

Please check the options that are relevant:

- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Performance improvement
- [ ] Code refactoring
- [ ] Agent improvement
- [ ] New command
- [ ] Command enhancement

## Related Issue

Fixes #(issue number)

## Changes Made

Please provide a detailed list of changes:

- Change 1
- Change 2
- Change 3

## Commands/Agents Affected

List which commands or agents are affected by this change:

### New Commands
- `/new-command-1` - Description
- `/new-command-2` - Description

### Modified Commands
- `/existing-command-1` - What changed
- `/existing-command-2` - What changed

### New/Modified Agents
- Agent Name - What changed

## Testing Done

Please describe the tests you ran to verify your changes:

- [ ] Tested command execution
- [ ] Tested with Azure platform
- [ ] Tested with Railway platform
- [ ] Tested platform-agnostic scenarios
- [ ] Tested edge cases
- [ ] Tested error handling

### Test Details

```bash
# Commands tested
/command-name

# Test scenarios
1. Scenario 1: Description
2. Scenario 2: Description
```

## Code Review

- [ ] I have run `/review-code` on my changes
- [ ] I have addressed all Critical and High severity issues
- [ ] Any remaining issues are documented with justification

### Code Review Results

```
Summary of /review-code results:
- Critical: 0
- High: 0
- Medium: X (justified below)
- Low: X
```

## Documentation Updated

- [ ] README.md updated (if adding new commands)
- [ ] Command documentation added/updated in `.claude/commands/`
- [ ] Agent documentation added/updated in `.claude/agents/`
- [ ] CHANGELOG.md updated
- [ ] Example usage provided
- [ ] Inline code comments added

## Screenshots/Examples

If applicable, add screenshots or example outputs:

```bash
# Example command usage
/your-command

# Output or result
```

## Checklist

Before submitting, please ensure:

- [ ] My code follows the project's style guidelines
- [ ] I have performed a self-review of my own code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] My changes generate no new warnings or errors
- [ ] I have tested my changes thoroughly
- [ ] All existing tests pass (if applicable)
- [ ] I have updated the documentation accordingly
- [ ] I have updated CHANGELOG.md with my changes
- [ ] My commit messages are clear and descriptive

## Platform-Specific Considerations

If your changes are platform-specific:

### Azure
- [ ] Tested with Azure Static Web Apps
- [ ] Tested with Azure Functions
- [ ] Azure-specific documentation updated

### Railway
- [ ] Tested with Railway deployments
- [ ] Railway-specific documentation updated

### Both/Generic
- [ ] Works across both platforms
- [ ] Platform-agnostic approach used

## Breaking Changes

If this PR includes breaking changes, please describe:

1. What breaks:
2. Migration path:
3. Deprecation notices added:

## Additional Notes

Add any additional notes, concerns, or context for reviewers:

## Reviewer Checklist

For maintainers reviewing this PR:

- [ ] Code quality is acceptable
- [ ] Tests are adequate
- [ ] Documentation is complete
- [ ] No security concerns
- [ ] Follows plugin architecture
- [ ] Consistent with existing patterns
- [ ] CHANGELOG.md updated appropriately
