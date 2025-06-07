# Critique Request

Execute critique analysis based on a finalized preparation document. Your role:
1. Read and validate the preparation document
2. Spawn parallel Task agents with the exact prompts from preparation
3. Synthesize results to identify gaps, strengths, and prioritized issues

## Execution Workflow

### Phase 1: Preparation Document Validation and Perspective Mapping

**READ** the specified preparation document and **VALIDATE**:
- File exists and is properly formatted
- Subject and files are still valid/current
- Status is "ready_for_execution"
- All required fields are present

**MAP** requested perspectives to prompt files intelligently:
- Scan `.claude/prompts/detect-problem/` and `.claude/prompts/assess-excellence/` folders for prompt files
- Map specific perspective names to best matching prompts:
  - For detect-problem: "security-vulnerabilities" → detect-problem-security.md, "performance-bottlenecks" → detect-problem-performance.md, "over-engineering" → detect-problem-over-engineering.md
  - For assess-excellence: "architectural" → assess-excellence-architectural.md, "security" → assess-excellence-security.md
  - For generic names: "security" → detect-problem-security.md OR assess-excellence-security.md based on category
- Validate each requested perspective has a corresponding prompt file
- ERROR if any perspective prompt is missing

### Phase 2: Parallel Critique Task Execution

For each mapped perspective from the preparation document:

1. **DOCUMENT orchestrator prompt** - save to: reviews/{subject_name}-orchestrator-prompt-v1.md

2. **GENERATE task prompt** using context from preparation document and **INVOKE Task agent** with:

**Task Description**: "{perspective} critique of {subject}"

**Task Prompt**:
```
Perform critique using the specified perspective prompt.

## Project Context
{synthesized_context_from_preparation}

## Critique Subject  
**Subject**: {clarified_subject_from_preparation}
**Scope**: {clarified_scope_from_preparation}
**Files/Changes**: {relevant_files_from_preparation}
**Background**: {background_context_from_preparation}

## Instructions
1. READ the prompt: .claude/prompts/{perspective_category}/{perspective_category}-{perspective_name}.md
2. READ all relevant files and/or git diff identified above
{if_plan_file_focus}
3. **READ PLAN FILE CAREFULLY**: Pay special attention to the plan file(s) - understand the full context, rationale, constraints, and intended outcomes
{end_if}
{if_implementation_review}
3. **IMPLEMENTATION REVIEW FOCUS**: Compare the implementation against the original plan/intent - identify deviations, improvements, or issues
{end_if}
{if_current_state_assessment}
3. **CURRENT STATE ANALYSIS**: Conduct broad assessment of the existing codebase/architecture from your perspective
{end_if}
4. **Consider project context** when forming critique - understand constraints and rationale behind decisions
5. APPLY the perspective prompt with "think super hard" depth
6. SAVE to: reviews/{subject_name}-{perspective}-v1.md

Include metadata:
---
CRITIQUE_METADATA:
  timestamp: "{iso_timestamp}"
  prompt_template: ".claude/prompts/{perspective_category}/{perspective_category}-{perspective_name}.md"
  clarified_subject: "{clarified_subject_description}"
---
```

**Orchestrator Prompt Documentation Format**:
```
---
ORCHESTRATOR_METADATA:
  timestamp: "{iso_timestamp}"
  subject: "{subject_name}"
  preparation_file: "{preparation_file_path}"
  perspectives_count: {number_of_perspectives}
---

# Orchestrator Prompt Documentation

## Preparation File
{preparation_file_path}

## User Request (from preparation)
{original_user_input_from_prep}

## Resolved Context (from preparation)
{synthesized_context_from_prep}

## Task Invocations
{for_each_mapped_perspective}
### {perspective_name} ({category})
**Task Description**: "{perspective} critique of {subject}"

**Complete Task Prompt**:
```
{generated_task_prompt_with_preparation_context}
```
{end_for_each_perspective}
```

### Phase 3: Results Synthesis

After all critique Tasks complete:
1. **READ** all generated critique outputs
2. **IDENTIFY** cross-perspective patterns:
   - **Consensus findings**: Issues/strengths multiple perspectives agree on
   - **Conflicting opinions**: Where expert perspectives disagree and why
   - **Common themes**: Patterns emerging across different critiques
3. **EVALUATE** context-aware findings:
   - Issues vs. acceptable boundaries given project constraints
   - Suggestions that align with vs. miss strategic context
4. **PRIORITIZE** by severity, frequency, and cross-perspective agreement
5. **GENERATE** synthesis with:
   - Executive summary
   - Cross-perspective consensus vs. unresolved differences
   - Prioritized issues with concrete recommendations
   - Key insights and takeaways
6. **SAVE** to: reviews/{subject_name}-synthesis-v1.md

## Input Validation

### Missing Preparation File
```
ERROR: Preparation file not found: '{file_path}'
SUGGESTION: Check file path or run /critique-prep first
```

### Invalid Preparation Format
```
ERROR: Invalid preparation document format
ISSUES: {list_specific_formatting_issues}
SUGGESTION: Review preparation document structure
```

### Missing Perspective Prompts
```
ERROR: Referenced perspective prompt not found: '{prompt_path}'
AVAILABLE: {list_available_prompts}
SUGGESTION: Update preparation document or add missing prompt file
```

### Stale Subject References
```
WARNING: Referenced file not found: '{file_path}'
SUGGESTION: Update preparation document with current file paths
```

## Usage Examples

```bash
# Execute prepared critique
/critique-request critique-prep/auth-implementation-critique-prep-v1.md

# Execute with relative path
/critique-request critique-prep/logging-plan-critique-prep-v1.md

# Execute after editing preparation
/critique-request critique-prep/api-design-critique-prep-v1.md
```

## Perspective Mapping Examples

**Preparation document**: 
```
- **security-vulnerabilities** (detect-problem) - identify potential security issues
- **architectural** (assess-excellence) - evaluate architectural quality
```
**Maps to**:
- `security-vulnerabilities` → `.claude/prompts/detect-problem/detect-problem-security.md`
- `architectural` → `.claude/prompts/assess-excellence/assess-excellence-architectural.md`

**Preparation document**:
```
- **over-engineering** (detect-problem) - find unnecessary complexity
- **performance** (assess-excellence) - evaluate performance characteristics  
```
**Maps to**:
- `over-engineering` → `.claude/prompts/detect-problem/detect-problem-over-engineering.md`
- `performance` → `.claude/prompts/assess-excellence/assess-excellence-performance.md`

## Expected Input Format

The preparation document must contain:

```markdown
---
CRITIQUE_PREP_METADATA:
  timestamp: "2024-01-15T10:30:00Z"
  subject: "subject-name"
  original_request: "original user input"
  perspectives_count: 3
  status: "ready_for_execution"
---

# Critique Preparation: {subject}

## Original Request
{user_input}

## Synthesized Context
{context}

## Resolved Subject
**Subject**: {description}
**Scope**: {scope}
**Files/Changes**: {files}
**Background**: {background}

## Requested Perspectives
- **perspective1** (detect-problem) - brief intent description
- **perspective2** (assess-excellence) - brief intent description

## Special Instructions
- **Plan File Focus**: Agents should read plan file(s) carefully and understand full context
- **Implementation Review**: Focus on comparing implementation against original intent/plan
- **Current State Analysis**: Broad assessment of existing codebase/architecture

## Critique Purpose
{description_of_what_user_wants_to_achieve}
```

## Output Structure

### Generated Files
- **Individual critiques**: `reviews/{subject_name}-{perspective}-v1.md`
- **Synthesis report**: `reviews/{subject_name}-synthesis-v1.md`
- **Orchestrator prompts**: `reviews/{subject_name}-orchestrator-prompt-v1.md`

### Synthesis Report Format
```markdown
---
SYNTHESIS_METADATA:
  timestamp: "{iso_timestamp}"
  subject: "{subject_name}"
  preparation_file: "{prep_file_path}"
  perspectives_analyzed: [{list_of_perspectives}]
  total_issues_found: {number}
  consensus_issues: {number}
---

# Critique Synthesis: {subject_name}

## Executive Summary
{high_level_findings_and_recommendations}

## Cross-Perspective Analysis

### Consensus Findings
{issues_and_strengths_multiple_perspectives_agree_on}

### Conflicting Opinions
{where_expert_perspectives_disagree_and_analysis_of_why}

### Common Themes
{patterns_emerging_across_different_critiques}

## Prioritized Issues
{ranked_by_severity_frequency_and_cross_perspective_agreement}

## Key Insights and Recommendations
{actionable_recommendations_based_on_synthesis}
```

This execution phase ensures the exact critique analysis defined in your preparation document is carried out with full transparency and comprehensive synthesis.