# Critique Orchestrator

Orchestrate parallel critiques from specified perspectives. Your role:
1. Extract critique subject from original user input and map perspectives to prompt files
2. Spawn Task agents for each perspective prompt
3. Synthesize results to identify gaps, strengths, and prioritized issues

## Orchestration Workflow

### Phase 1: Context Clarification and Perspective Mapping
1. **EXTRACT** critique subject and scope from natural language input
2. **RESOLVE** subject intelligently:
   - File references: search plans/, src/, docs/, etc. for matching files
   - Recent changes: include git diff of uncommitted changes if relevant
   - Concept references: search for related files using keywords
   - Domain-specific insights: relevant design patterns, architectural principles, or industry best practices that apply
3. **MAP** perspectives to prompt files:
   - Scan `/prompts/detect-problem/` and `/prompts/assess-excellence/` folders for prompt files
   - Extract perspective names from user input (e.g., "detect-problem-security" → `/prompts/detect-problem/security.md`)
   - Validate each requested perspective has a corresponding prompt file
   - ERROR if any perspective prompt is missing
4. **CLARIFY** context for sub-agents:
   - What is being critiqued (files, concepts, implementations)
   - Relevant file paths and/or git diff
   - Background context and motivation
   - Domain-specific insights: relevant design patterns, architectural principles, or industry best practices that apply

### Phase 2: Spawn Parallel Critique Tasks
For each mapped perspective prompt, **INVOKE Task agent** with:

**Task Description**: "{perspective} critique of {subject}"

**Task Prompt**:
```
Perform critique using the specified perspective prompt.

## Context
**Subject**: {clarified_subject_description}
**Scope**: {clarified_scope}
**Files/Changes**: {relevant_files_and_or_git_diff}
**Background**: {background_context}

## Instructions
1. READ the prompt: /prompts/{perspective_category}/{perspective_name}.md
2. READ all relevant files and/or git diff identified above
3. APPLY the perspective prompt with "think super hard" depth
4. GENERATE critique following the prompt's output format
5. SAVE to: reviews/{subject_name}-{perspective}-v1.md

Include metadata:
---
CRITIQUE_METADATA:
  timestamp: "{iso_timestamp}"
  prompt_template: "/prompts/{perspective_category}/{perspective_name}.md"
  clarified_subject: "{clarified_subject_description}"
---
```

### Phase 3: Synthesis
After all critique Tasks complete:
1. **READ** all generated critique outputs
2. **IDENTIFY** cross-perspective findings:
   - Major issues found by detect-problem perspectives
   - Strengths reinforced by assess-excellence perspectives
   - Conflicting views and blind spots
3. **PRIORITIZE** by severity and frequency
4. **GENERATE** synthesis: reviews/{subject_name}-synthesis-v1.md

## Perspective Mapping Examples

**User input**: "detect problems for security, performance and assess excellence for architecture in the auth implementation"
**Maps to**:
- `/prompts/detect-problem/security.md`
- `/prompts/detect-problem/performance.md`
- `/prompts/assess-excellence/architecture.md`

**User input**: "detect problems related to overengineering look at the logging plan"
**Maps to**:
- `/prompts/detect-problem/overengineering.md`

## Error Handling

### Subject Resolution Failed
```
ERROR: Could not resolve critique subject: '{subject}'
SEARCHED: plans/, src/, docs/, etc.
SUGGESTION: Be more specific about files or scope
```

### Perspective Prompt Missing
```
ERROR: Perspective prompt not found: '{perspective}'
EXPECTED: /prompts/{detect-problem|assess-excellence}/{perspective_name}.md
AVAILABLE: {list_available_detect_and_assess_prompts}
```

## Usage Examples

```bash
# Problem detection
/critique "detect problems for security, performance and assess excellence for architecture in the auth implementation"

# Excellence assessment  
/critique "assess excellence for architecture, assess excellence for performance analyze the new API design"

# Mixed perspectives
/critique "detect problems related to overengineering, assess excellence for simplicity look at the logging infrastructure plan"

# Recent changes
/critique "detect problems for security review the recent authentication changes"
```