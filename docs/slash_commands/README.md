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

## Resources

- **[Complete Power User Guide](../slash-commands-for-power-users.md)** - Comprehensive slash commands tutorial
- **[Main Repository](../../README.md)** - Project overview and setup