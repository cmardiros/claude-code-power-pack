PLANS="my-plan" REVIEW_PERSPECTIVES="simplicity|simplicity,comprehensive" THINKING_BUDGET="think hard|think super hard|ultrathink" OUTPUT_DIR="plan-reviews"
---
CLAUDE_PARSING_HINTS:
  PLANS:
    type: "array"
    description: "List of plan files to review (relative to project root)"
    search_paths: ["plans/", "./", "ai-docs/", "docs/"]
    extensions: [".md"]
    natural_language_matching: true
    matching_examples:
      - input: "my plan" -> searches for files containing "my" or "plan"
      - input: "API plan" -> searches for files containing "API" or "api" 
      - input: "security plan" -> searches for files containing "security"
    examples: ["plans/04-structured-logging-plan.md", "plans/05-typer-cli-migration-plan.md"]
    
  REVIEW_PERSPECTIVES:
    type: "array"
    default: ["comprehensive"]
    examples: ["simplicity", "comprehensive", "simplicity,comprehensive"]
    description: "Types of review perspectives to apply"
    
  THINKING_BUDGET:
    type: "string"
    auto_detect: true
    examples: ["think hard", "think super hard", "ultrathink"]
    exact_match_terms: ["think hard", "think super hard", "ultrathink"]
    default: "think super hard"
    description: "Cognitive effort level for analysis and synthesis"
    
  OUTPUT_DIR:
    type: "string"
    default: "plans"
    description: "Directory to write review and revision files"
---

# Claude Code Agent Orchestrator Instructions

You are orchestrating an automated plan review workflow. Your role is to:
1. Parse natural language input using exact string matching for thinking budget terms
2. Spawn Task agents for parallel review execution  
3. Synthesize results and generate revisions when critical issues found

## Natural Language Parsing Examples

**When engineer says**: "my plan comprehensively and think super hard"
**Parse as**:
- PLANS: [find file matching "my plan" in search paths] 
- REVIEW_PERSPECTIVES: ["comprehensive"]
- THINKING_BUDGET: "think super hard"

**When engineer says**: "API plan and security plan using both perspectives with ultrathink"
**Parse as**:
- PLANS: [find files matching "API plan" and "security plan" in search paths]
- REVIEW_PERSPECTIVES: ["simplicity", "comprehensive"] 
- THINKING_BUDGET: "ultrathink"

**When engineer says**: "API plan for simplicity and think hard"
**Parse as**:
- PLANS: [find file matching "API plan" -> likely "API-plan.md"]
- REVIEW_PERSPECTIVES: ["simplicity"]
- THINKING_BUDGET: "think hard"

**When engineer says**: "security plan comprehensive perspective think super hard save to reviews"
**Parse as**:
- PLANS: [find file matching "security plan" -> likely "security-plan.md"]
- REVIEW_PERSPECTIVES: ["comprehensive"]
- THINKING_BUDGET: "think super hard"
- OUTPUT_DIR: "reviews"

## Orchestration Workflow

### Phase 1: Parse and Validate
1. **PARSE** natural language input using exact string matching for thinking budget terms
2. **RESOLVE** plan names intelligently:
   - For phrases like "my plan", "API plan", "security plan": search in plans/, ./, ai-docs/, docs/
   - Match files containing keywords (case-insensitive)
   - Prefer exact matches, then partial matches
   - Example: "API plan" → search for files containing "api" → find "API-plan.md"
3. **VALIDATE** all resolved plan files exist - FAIL with clear error and suggestions if not found
4. **EXTRACT** plan metadata (title, scope) from each file
5. **PREPARE** output directory structure

### Phase 2: Spawn Parallel Review Tasks
For each plan file and perspective combination, **INVOKE Task agent** with:

**Task Description**: "{perspective} review of {plan_file}"

**Task Prompt**: 
```
Review the plan file '{plan_file}' using {perspective} perspective with {thinking_budget} cognitive effort.

1. READ the plan file: {plan_file}
2. READ the prompt template: .claude/prompts/{perspective}_review.md  
3. APPLY the {perspective} review framework with {thinking_budget} depth
4. GENERATE review following the template's output format
5. SAVE to: {output_dir}/{plan_name}-v1-{perspective}-review.md

Include metadata header:
---
COMMAND_INTERPRETATION:
  natural_language_input: "{original_user_input}"
  parsed_thinking_budget: "{thinking_budget}"
  timestamp: "{iso_timestamp}"
  prompt_template: ".claude/prompts/{perspective}_review.md"
---

Apply {thinking_budget} throughout your analysis.
```

### Phase 3: Synthesis and Revision
After all review Tasks complete:

1. **READ** all generated review outputs
2. **ANALYZE** findings across perspectives using {thinking_budget} depth:
   - **"think hard"**: Pattern identification and conflict resolution
   - **"think super hard"**: Nuanced prioritization and impact analysis  
   - **"ultrathink"**: Strategic synthesis with organizational implications
3. **IDENTIFY** critical issues requiring plan revision
4. **GENERATE** revised plan if critical issues found using {thinking_budget} depth:
   - **"think hard"**: Balance trade-offs while maintaining objectives
   - **"think super hard"**: Comprehensive redesign with architectural considerations
   - **"ultrathink"**: Strategic revision with ecosystem implications

### Phase 4: Output Organization
**ORGANIZE** all outputs with clear naming and generate summary report of completed work.

## Error Handling

### Plan Resolution Failed
```
ERROR: Could not resolve plan: 'nonexistent plan'
SEARCHED: plans/, ./, ai-docs/, docs/ for files containing: 'nonexistent', 'plan'
FOUND FILES: plans/API-plan.md, plans/security-plan.md, plans/my-implementation-plan.md
SUGGESTION: Try "API plan", "security plan", or "my plan"
ALTERNATIVE: Use exact path like "plans/your-plan.md"
```

### Invalid Perspective
```
ERROR: Invalid perspective: 'security'
VALID: simplicity, comprehensive
EXAMPLE: /plan_review_revise PLANS="plans/plan.md" REVIEW_PERSPECTIVES="simplicity,comprehensive"
```

### Invalid Thinking Budget
```
ERROR: Invalid thinking budget: 'think really hard'
VALID: "think hard", "think super hard", "ultrathink"
EXACT MATCH REQUIRED: Use these terms exactly as shown
```

## Success Indicators

You'll know the workflow succeeded when:
1. **All plan files found and processed**
2. **Review tasks completed with metadata headers** 
3. **Synthesis applied appropriate thinking budget depth**
4. **Revised plans generated when critical issues found**
5. **Output files follow exact naming conventions**