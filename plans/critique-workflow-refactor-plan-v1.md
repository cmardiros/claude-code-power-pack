# Critique Workflow Refactor Plan v1

## Problem Statement

The current single `/critique` command performs all phases (1-4) in one execution without human oversight of critical decision points. This creates a significant blindspot:

- **Phase 1-2 (Context Synthesis & Perspective Mapping)** are crucial framing decisions that dramatically impact critique quality
- No visibility into how the orchestrator interprets user requests before spawning agents
- No opportunity to iterate on context synthesis or refine perspective mapping
- When critiques miss the mark, it's unclear whether the issue was agent execution or orchestrator framing

**Core Issue**: The orchestrator's interpretation and framing of the problem happens in a black box, but this framing is often more important than the individual expert analyses.

## Key Requirements

### Functional Requirements
1. **Human-in-the-loop review** after Phase 1-2 completion
2. **Iteration capability** on context synthesis and perspective mapping
3. **Full transparency** of exact prompts that will be sent to Task agents
4. **Maintain existing functionality** - all current critique capabilities preserved
5. **Clear separation** between preparation and execution phases
6. **Reproducible execution** from finalized preparation documents

### User Experience Requirements
1. **Intuitive command naming** that doesn't conflict with "implementation plans"
2. **Backward compatibility** considerations for existing users
3. **Clear workflow guidance** in documentation
4. **Efficient iteration** on preparation without re-running expensive operations

### Technical Requirements
1. **Structured output format** for preparation documents
2. **Input validation** for execution command
3. **Error handling** for missing or malformed preparation files
4. **Metadata tracking** across both phases

## Proposed Solution

### Two-Command Architecture

#### Command 1: `/critique-prep`
**Purpose**: Context synthesis, subject resolution, and execution preparation
- Performs Phases 1-2 from current workflow
- Outputs structured preparation document
- Allows human review and iteration

#### Command 2: `/critique-request`  
**Purpose**: Execute critique based on finalized preparation
- Reads preparation document
- Performs Phases 3-4 from current workflow
- Spawns Task agents with exact prompts from prep document

### Workflow Flow
```
User Input → /critique-prep → Preparation Doc → Human Review/Edit → /critique-request → Critique Results
```

## Implementation Details

### File Structure Changes

#### New Command Files
- `.claude/commands/critique-prep.md` (new)
- `.claude/commands/critique-request.md` (new)
- `.claude/commands/critique.md` (keep for transition, mark deprecated)

#### Output Locations
- **Preparation documents**: `critique-prep/{subject_name}-critique-prep-v1.md`
- **Individual critiques**: `reviews/{subject_name}-{perspective}-v1.md` (unchanged)
- **Synthesis**: `reviews/{subject_name}-synthesis-v1.md` (unchanged)
- **Orchestrator prompts**: `reviews/{subject_name}-orchestrator-prompt-v1.md` (unchanged)

### Preparation Document Format

```markdown
---
CRITIQUE_PREP_METADATA:
  timestamp: "{iso_timestamp}"
  subject: "{subject_name}"
  original_request: "{user_input}"
  perspectives_count: {number}
  status: "ready_for_execution"
---

# Critique Preparation: {subject_name}

## Original Request
{original_user_input}

## Synthesized Context
{project_context_synthesis}

## Resolved Subject
**Subject**: {clarified_subject_description}
**Scope**: {clarified_scope}  
**Files/Changes**: {relevant_files_and_or_git_diff}
**Background**: {background_context}

## Perspective Mapping
{for_each_perspective}
- **{perspective_name}**: `.claude/prompts/{category}/{category}-{perspective}.md` ✓
{end_for_each_perspective}

## Planned Task Invocations
{for_each_perspective}
### {perspective_name} ({category})
**Task Description**: "{perspective} critique of {subject}"

**Complete Task Prompt**:
```
{exact_complete_task_prompt_with_all_variables_resolved}
```
{end_for_each_perspective}

## Execution Instructions
To execute this critique preparation:
```
/critique-request critique-prep/{subject_name}-critique-prep-v1.md
```
```

### Command Specifications

#### `/critique-prep` Command
- **Input**: Natural language critique request (same as current `/critique`)
- **Phases**: 1-2 from current workflow
- **Output**: Preparation document in `critique-prep/` directory
- **Validation**: Verify all perspective prompts exist before creating prep document
- **Error Handling**: Clear messaging for missing prompts or unresolved subjects

#### `/critique-request` Command  
- **Input**: Path to preparation document
- **Phases**: 3-4 from current workflow
- **Validation**: 
  - Preparation file exists and is valid
  - All referenced prompt files still exist
  - Preparation document has `status: "ready_for_execution"`
- **Output**: Same as current workflow (individual critiques + synthesis)

## File Changes Required

### New Files
1. `.claude/commands/critique-prep.md`
2. `.claude/commands/critique-request.md`

### Modified Files
1. `docs/slash_commands/critique-workflow-guide.md` - Update for two-command workflow
2. `docs/slash_commands/README.md` - Update command listings

### Removed Files
1. `.claude/commands/critique.md` - Replace with new two-command workflow

### Directory Creation
- `critique-prep/` directory for preparation documents

## Documentation Updates Required

### docs/slash_commands/critique-workflow-guide.md
- **New sections needed**:
  - "Two-Phase Workflow Overview"
  - "Phase 1: Preparation with /critique-prep"
  - "Phase 2: Execution with /critique-request"  
  - "Human Review and Iteration Guide"
  - "Migration from Single-Command Workflow"
- **Updated sections**:
  - Sync commands section (new command files)
  - Usage examples (show both phases)
  - Behind-the-scenes workflow
- **New examples**:
  - Iterating on preparation documents
  - Reviewing and editing context synthesis
  - Modifying perspective mapping before execution

### docs/slash_commands/README.md
- Add `/critique-prep` and `/critique-request` to command listings
- Update `/critique` status (deprecated but functional)

## Migration Strategy

### Breaking Changes Approach
1. **Replace existing `/critique` command** completely
2. **Clean transition** - single new workflow to learn
3. **Clear documentation** explaining the new two-phase approach

## Success Criteria

### Functional Success
- [ ] `/critique-prep` generates valid preparation documents
- [ ] Human can review and edit preparation documents
- [ ] `/critique-request` executes critiques identical to current workflow
- [ ] All existing perspective prompts work with new workflow
- [ ] Error handling provides clear guidance for common issues

### User Experience Success  
- [ ] Documentation clearly explains new workflow benefits
- [ ] Migration path is obvious and low-friction
- [ ] New workflow feels more controlled and transparent
- [ ] Iteration on preparation is efficient and intuitive

### Technical Success
- [ ] Preparation documents are human-readable and editable
- [ ] File validation prevents execution of invalid preparations
- [ ] Metadata tracking works across both commands
- [ ] No regression in critique quality or capabilities

## Risk Mitigation

### Potential Risks
1. **Preparation documents** becoming stale if files change
2. **Workflow complexity** deterring usage
3. **Learning curve** for new two-phase approach

### Mitigation Strategies
1. **Clear documentation** with step-by-step examples
2. **Validation warnings** if preparation references missing files
3. **Progressive disclosure** - simple cases remain simple
4. **Comprehensive examples** showing workflow benefits

## Implementation Phases

### Phase 1: Core Implementation
1. Create new command files
2. Implement basic preparation document generation
3. Implement basic execution from preparation documents
4. Basic validation and error handling

### Phase 2: Polish and Documentation
1. Update all documentation
2. Add comprehensive examples
3. Improve error messages and user guidance
4. Add deprecation notice to existing command

### Phase 3: User Adoption Support
1. Monitor usage patterns
2. Gather user feedback
3. Refine workflow based on real usage
4. Add advanced features based on user needs

This refactor will provide the human oversight and control needed while maintaining all existing functionality and providing a clear migration path.