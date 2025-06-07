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

### `/critique-prep` & `/critique-request`
**Status**: ✅ Fully Implemented  
**Location**: `.claude/commands/critique-prep.md`, `.claude/commands/critique-request.md`  
**Guide**: [Critique Workflow Guide](critique-workflow-guide.md)

Two-phase critique workflow with human oversight for parallel multi-perspective analysis.

**Available Perspectives:**
- ✅ **Detect Problems**: `anti-patterns`, `blindspots`, `future-regrets`, `junior-mistakes`, `over-engineering`, `premortem-failures`, `smells`
- ✅ **Assess Excellence**: `architectural`, `code`, `future-value`, `performance`, `premortem`, `production`, `security`, `testing`, `veteran`

**Usage Examples:**
```bash
# Phase 1: Prepare with human review
/critique-prep "detect problems for security, performance in the auth implementation"

# Phase 2: Execute when satisfied with preparation
/critique-request critique-prep/auth-implementation-critique-prep-v1.md
```

## Command Structure

Commands are stored in `.claude/commands/` with supporting prompts in `.claude/prompts/`.

## Resources

- **[Complete Power User Guide](../slash-commands-for-power-users.md)** - Comprehensive slash commands tutorial
- **[Main Repository](../../README.md)** - Project overview and setup