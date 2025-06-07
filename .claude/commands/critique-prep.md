# Critique Preparation

Prepare for multi-perspective critique panel analysis by synthesizing project context and resolving critique subjects. **Think super hard** about context synthesis as it will guide expert agents from different perspectives. Your role:
1. Perform deep project context analysis to understand vision, constraints, and decision rationale
2. Extract critique purpose and resolve specific subjects to be analyzed
3. Generate detailed preparation document for human review before execution by critique request panel

## Preparation Workflow

### Phase 1: Context Synthesis with Perspective Validation

**SYNTHESIZE** project context from user-provided information:
- If user references docs/files, extract key vision, constraints, and decision rationale
- If user references a plan, provide full path to the plan file and instruct agents to read plan carefully
- Distill WHY decisions were made and what trade-offs guide the project

**VALIDATE** context by briefly considering: "Would the requested critique perspectives (security, architecture, performance, etc.) have enough context to provide meaningful analysis? Are there obvious gaps that would lead them astray?"

**REFINE** context if gaps are identified, focusing on what each perspective needs to understand the problem correctly.

**CREATE** focused PROJECT_CONTEXT summary for execution phase

### Phase 2: Subject Resolution and Perspective Extraction
1. **EXTRACT** critique purpose and requested perspectives from natural language input
2. **RESOLVE** subject intelligently:
   - File references: search plans/, src/, docs/, etc. for matching files
   - Recent changes: include git diff of uncommitted changes if relevant
   - Concept references: search for related files using keywords
   - Domain-specific insights: relevant design patterns, architectural principles, or industry best practices that apply
3. **CLARIFY** what will be critiqued:
   - What is being critiqued (files, concepts, implementations)
   - Relevant file paths and/or git diff
   - Background context and motivation
4. **DOCUMENT** requested perspectives with clear intent:
   - Extract specific perspective names and categories from user input
   - For detect-problem requests: identify specific concern types (e.g., "security-vulnerabilities", "performance-bottlenecks", "over-engineering") 
   - For assess-excellence requests: identify specific excellence domains (e.g., "architectural", "security", "performance")
   - For ambiguous language like "detect problems" or "comprehensive assessment": ask for clarification or infer most likely specific perspectives
   - Note if plan files should be emphasized in agent instructions

### Phase 3: Preparation Document Generation

**SAVE** preparation document to: critique-prep/{subject_name}-critique-prep-v1.md

**Preparation Document Format**:
```
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

## Requested Perspectives
{for_each_perspective}
- **{specific_perspective_name}** ({detect_problem_or_assess_excellence}) - {brief_intent_description}
{end_for_each_perspective}

## Special Instructions
{if_plan_files_involved}
- **Plan File Focus**: Agents should read plan file(s) carefully and understand full context
{end_if}
{if_implementation_review}
- **Implementation Review**: Focus on comparing implementation against original intent/plan
{end_if}
{if_current_state_assessment}
- **Current State Analysis**: Broad assessment of existing codebase/architecture
{end_if}

## Critique Purpose
{description_of_what_user_wants_to_achieve_with_this_critique}

## Next Steps
To execute this critique preparation:
```
/critique-request critique-prep/{subject_name}-critique-prep-v1.md
```

## Review Guidelines
Before execution, review and edit this preparation document:
1. **Context accuracy**: Does the synthesized context capture project constraints and rationale?
2. **Subject clarity**: Is the critique subject and scope precisely defined?
3. **Perspective relevance**: Are the selected perspectives appropriate for this analysis?
4. **Purpose clarity**: Is the critique purpose clearly articulated?
5. **Missing elements**: Are there important perspectives or context missing?
```

## Error Handling

### Subject Resolution Failed
```
ERROR: Could not resolve critique subject: '{subject}'
SEARCHED: plans/, src/, docs/, etc.
SUGGESTION: Be more specific about files or scope
```

## Usage Examples

```bash
# Problem detection
/critique-prep "detect problems for security, performance and assess excellence for architecture in the auth implementation"

# Excellence assessment  
/critique-prep "assess excellence for architecture, assess excellence for performance analyze the new API design"

# Mixed perspectives
/critique-prep "detect problems related to overengineering, assess excellence for simplicity look at the logging infrastructure plan"

# Recent changes
/critique-prep "detect problems for security review the recent authentication changes"
```

## Human Review Process

After preparation document generation:
1. **Review** the preparation document for accuracy and completeness
2. **Edit** context synthesis, subject resolution, or requested perspectives as needed
3. **Validate** that the critique purpose and scope are correctly captured
4. **Execute** using `/critique-request` when satisfied with preparation

This preparation phase ensures the critique request panel receives precisely framed context and clear direction for multi-perspective analysis.