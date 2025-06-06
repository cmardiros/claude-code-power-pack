# Critique Orchestrator

Orchestrate parallel critiques from specified perspectives. Your role:
1. Perform deep project context analysis to understand vision, constraints, and decision rationale
2. Extract critique subject and map perspectives to prompt files
3. Spawn Task agents with rich contextual foundation
4. Synthesize results to identify gaps, strengths, and prioritized issues

## Orchestration Workflow

### Phase 1: Context Synthesis

**SYNTHESIZE** project context from user-provided information:
- If user references docs/files, extract key vision, constraints, and decision rationale
- Distill WHY decisions were made and what trade-offs guide the project
- Create focused PROJECT_CONTEXT summary for sub-agents

### Phase 2: Subject Resolution and Perspective Mapping
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

### Phase 3: Spawn Parallel Critique Tasks
For each mapped perspective prompt, **INVOKE Task agent** with:

**Task Description**: "{perspective} critique of {subject}"

**Task Prompt**:
```
Perform critique using the specified perspective prompt.

## Project Context
{synthesized_context_from_user_input}

## Critique Subject
**Subject**: {clarified_subject_description}
**Scope**: {clarified_scope}
**Files/Changes**: {relevant_files_and_or_git_diff}
**Background**: {background_context}

## Instructions
1. READ the prompt: /prompts/{perspective_category}/{perspective_name}.md
2. READ all relevant files and/or git diff identified above
3. **Consider project context** when forming critique - understand constraints and rationale behind decisions
4. APPLY the perspective prompt with "think super hard" depth
5. SAVE to: reviews/{subject_name}-{perspective}-v1.md

Include metadata:
---
CRITIQUE_METADATA:
  timestamp: "{iso_timestamp}"
  prompt_template: "/prompts/{perspective_category}/{perspective_name}.md"
  clarified_subject: "{clarified_subject_description}"
---
```

### Phase 4: Synthesis
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

## Context-Aware Critique Enhancement

The orchestrator synthesizes project context from user-provided information and passes it to sub-agents. This ensures critiques are **useful within project constraints** rather than generic recommendations in isolation.