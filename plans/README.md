# Plans Directory

This directory contains implementation plans used for demonstrating the [plan-review-revise workflow](../docs/slash_commands/plan-review-revise-workflow-guide.md).

## Purpose

Plans here serve as input for the `/plan_review_revise` slash command, which analyzes them using different review perspectives and generates improved versions.

## Current Examples

- `logging-infrastructure-plan-v1.md` - Example logging infrastructure implementation plan
- `automated-plan-review-implementation-plan-v2.2.md` - Implementation plan for the plan-review-revise workflow itself

## Usage in Workflow

1. **Create Plans**: Save your implementation plans here (`.md` format recommended)
2. **Run Reviews**: Use `/plan_review_revise` command to analyze them
3. **View Results**: Check `../plan-reviews/` for review outputs and revised plans

## Best Practices

- Use version numbers in filenames (e.g., `my-feature-plan-v1.md`)
- Follow clear structure with objectives, implementation steps, and considerations
- Reference the [workflow guide](../docs/slash_commands/plan-review-revise-workflow-guide.md) for optimal plan formatting

## Related

- **[Plan-Review-Revise Workflow Guide](../docs/slash_commands/plan-review-revise-workflow-guide.md)** - Complete usage documentation
- **[Plan Reviews](../plan-reviews/)** - Generated review outputs and revisions