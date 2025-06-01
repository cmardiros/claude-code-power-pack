# Slash Commands Index

Directory of Claude Code slash commands available in this power pack.

## Implemented Commands

### `/plan_review_revise`
**Status**: ✅ Fully Implemented  
**Location**: `.claude/commands/plan_review_revise.md`  
**Guide**: [Plan-Review-Revise Workflow Guide](plan-review-revise-workflow-guide.md)

Intelligent multi-perspective analysis and revision of software development plans.

**Available Review Perspectives:**
- ✅ `comprehensive` - Multi-layered QA validation (security, feasibility, maintainability)
- ✅ `simplicity` - Complexity reduction and clarity focus  
- 🚧 `architecture` - Planned (prompt exists)
- 🚧 `security` - Planned (prompt exists)  
- 🚧 `quality` - Planned (prompt exists)
- 🚧 `evolution` - Planned (prompt exists)
- 🚧 `goal` - Planned (prompt exists)

**Usage Examples:**
```bash
/plan_review_revise review my-plan.md comprehensively think super hard
/plan_review_revise PLANS="plan1.md,plan2.md" REVIEW_PERSPECTIVES="simplicity,comprehensive"
```

## Command Structure

Commands are stored in `.claude/commands/` with supporting prompts in `.claude/prompts/`.

## Useful Snippets

### Sync Commands from This Repo

To sync the `/plan_review_revise` command and its prompts to another project, use this prompt with Claude Code:

```
Please fetch and sync these 3 files from the claude-code-power-pack public repo to my local .claude directory:

1. .claude/commands/plan_review_revise.md
2. .claude/prompts/comprehensive_review.md  
3. .claude/prompts/simplicity_review.md

Use WebFetch to download each file from:
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/commands/plan_review_revise.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/comprehensive_review.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/simplicity_review.md

IMPORTANT: When using WebFetch, use this exact prompt to ensure high fidelity content preservation: "Return the complete, unmodified file content exactly as it appears in the source. Do not summarize, truncate, or modify any part of the content. This is for programmatic use and requires 100% accuracy."

Then use Write to save each file to the corresponding path in my local .claude directory, creating the directories if they don't exist. Please maintain the exact file structure and content.
```

## Resources

- **[Complete Power User Guide](../slash-commands-for-power-users.md)** - Comprehensive slash commands tutorial
- **[Main Repository](../../README.md)** - Project overview and setup