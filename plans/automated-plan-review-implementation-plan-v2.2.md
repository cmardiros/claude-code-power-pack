# Automated Plan Review Workflow - Implementation Plan v2.2

> NOTE: This is the actual plan Claude Code wrote to implement the `plan_review_revise` slash command.

## Overview

This document provides a detailed implementation plan for creating an automated plan review system using Claude Code slash commands. This streamlined version focuses on two core review perspectives with intelligent thinking budget allocation based on natural language cues.

## Implementation Phases

### Phase 1: Directory Structure and Foundation Setup

#### 1.1 Create Required Directory Structure
```bash
# Create base command and prompt directories
mkdir -p .claude/commands
mkdir -p .claude/prompts
mkdir -p .claude/examples
```

**Required Directory Structure:**
```
.claude/
├── commands/
│   ├── plan_review_revise.md
│   └── manage_review_prompts.md
├── prompts/
│   ├── simplicity_review.md
│   └── comprehensive_review.md
└── examples/
    ├── plans-examples/
    │   ├── api-enhancement-plan.md
    │   └── logging-infrastructure-plan.md
    └── plan-reviews-examples/
```

#### 1.2 Validation Requirements
- Verify `.claude` directory is in project root
- Ensure all subdirectories are created with proper permissions
- Test directory accessibility from Claude Code

### Phase 2: Core Prompt Templates Creation

#### 2.1 Simplicity Review Prompt Template
**File**: `.claude/prompts/simplicity_review.md`

**Content Requirements:**
- Focus on clarity and complexity reduction
- Include specific evaluation criteria for simplicity
- Provide structured output format
- Include examples of simplicity improvements
- Key evaluation questions:
  - Can this plan be simplified without losing core value?
  - Are there unnecessary complexities or over-engineering?
  - Is the plan clear and easy to understand for implementers?
  - What's the minimum viable version of this plan?

#### 2.2 Comprehensive Review Prompt Template
**File**: `.claude/prompts/comprehensive_review.md`

**Content Requirements:**
- Use the provided QA specialist validation framework exactly:
  - Objective Achievement Validation
  - Quality Standards Assessment
  - Alternative Perspective Analysis
  - Implementation Viability Review
  - Risk & Blind Spot Identification
- Structured output format with quality_assessment sections
- Multi-layered validation approach
- Comprehensive analysis covering security, feasibility, maintainability, and cost implications

### Phase 3: Main Command Implementation

#### 3.1 Plan Review and Revision Command
**File**: `.claude/commands/plan_review_revise.md`

**Implementation Requirements:**

**YAML Frontmatter with Thinking Budget Integration:**
```yaml
---
CLAUDE_PARSING_HINTS:
  PLANS:
    type: "array"
    description: "List of plan files to review (relative to project root)"
    search_paths: ["ai-docs/", "./", "docs/", "plans/"]
    extensions: [".md"]
    examples: ["ai-docs/04-structured-logging-plan.md", "ai-docs/05-typer-cli-migration-plan.md"]
    
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
    default: "ai-docs"
    description: "Directory to write review and revision files"
---
```

**Command Structure with Simplified Interface:**

```markdown
Usage: /plan_review_revise PLANS="file1.md,file2.md" REVIEW_PERSPECTIVES="simplicity|comprehensive|simplicity,comprehensive" THINKING_BUDGET="think hard|think super hard|ultrathink" OUTPUT_DIR="ai-docs"

## Natural Language Parsing Advantage

Engineers see exact terms in dropdown → use exact terms in speech → precise parsing

**Example:** 
- Engineer sees: `THINKING_BUDGET="think hard|think super hard|ultrathink"`
- Engineer dictates: *"review my-plan.md using comprehensive perspective and think super hard"*
- Claude Code finds exact match: "think super hard" → perfect reliability

**Parsed Parameters:**
- PLANS: ["my-plan.md"] 
- REVIEW_PERSPECTIVES: ["comprehensive"]
- THINKING_BUDGET: "think super hard"

# Plan Review and Revision with Intelligent Thinking Budget Allocation

Review plans: $PLANS using perspectives: $REVIEW_PERSPECTIVES

Thinking Budget: $THINKING_BUDGET

## Automated Review Workflow

**Phase 1: Plan Discovery and Validation**
1. **PARSE** natural language and DETECT thinking budget using exact string matching
2. **VALIDATE** all specified plan files exist and are readable - FAIL with clear error if not found
3. **EXTRACT** plan metadata (title, scope, complexity indicators)
4. **PREPARE** output directory structure and naming conventions

**Phase 2: Review Perspective Orchestration**
**INVOKE MULTIPLE PARALLEL TASKS** for each plan and perspective combination:

For each plan file, spawn specialized review agents:
- **Simplicity Review Agent** (uses `simplicity_review.md` template)
- **Comprehensive Review Agent** (uses `comprehensive_review.md` template)

**Phase 3: Parallel Review Execution (Always Enabled)**
**INVOKE PARALLEL REVIEWS** using Task coordination:
- Each Task processes one plan + one perspective combination  
- Output to $OUTPUT_DIR/[plan-name]-v1-[perspective]-review.md with metadata header
- Apply $THINKING_BUDGET to each review task
- Handle errors: skip failed reviews, continue with successful ones, report issues in summary

**Phase 4: Review Analysis and Synthesis ($THINKING_BUDGET)**
Apply thinking budget for synthesis:
- **Basic (think hard)**: Pattern identification and conflict resolution
- **Enhanced (think super hard)**: Nuanced prioritization and impact analysis
- **Maximum (ultrathink)**: Comprehensive synthesis with strategic implications

**ANALYZE** all review outputs for critical issues and patterns:
- Aggregate findings across perspectives using allocated thinking budget
- Identify conflicting recommendations through appropriate depth analysis
- Prioritize issues by severity and impact with thinking budget level
- Determine if plan revision is warranted based on comprehensive assessment

**Phase 5: Automated Plan Revision ($THINKING_BUDGET)**
**ALWAYS** generate revised plan when critical issues found:

Apply thinking budget for revision:
- **Basic (think hard)**: Balance trade-offs and maintain objectives  
- **Enhanced (think super hard)**: Comprehensive redesign with architectural considerations
- **Maximum (ultrathink)**: Strategic revision with long-term implications and stakeholder impact

Generate revised plan:
- Include metadata header with interpretation details
- Address critical and high-priority issues systematically
- Maintain core objectives while improving approach
- Document changes and rationale with appropriate depth
- Version as $OUTPUT_DIR/[plan-name]-v1-revised.md

**Phase 6: Output Organization and Summary**
**ORGANIZE** all outputs with clear naming and generate summary report
```

#### 3.2 Output File Format with Simple Observability

**Review File Template:**
```markdown
---
COMMAND_INTERPRETATION:
  natural_language_input: "$USER_INPUT"
  parsed_thinking_budget: "$THINKING_BUDGET"
  timestamp: "$ISO_TIMESTAMP"
  prompt_template: "$PERSPECTIVE_review.md"
---

# $PERSPECTIVE Review - $PLAN_NAME

[Rest of review content...]
```

**Revised Plan File Template:**
```markdown
---
COMMAND_INTERPRETATION:
  natural_language_input: "$USER_INPUT"
  parsed_thinking_budget: "$THINKING_BUDGET"
  timestamp: "$ISO_TIMESTAMP"
  revision_triggered_by: ["$CRITICAL_ISSUE1", "$CRITICAL_ISSUE2"]
  original_plan_version: "v1"
---

# $PLAN_NAME - Revised Plan v1

**Revision Reasons**: $CRITICAL_ISSUES_FOUND

[Rest of revised plan content...]
```

#### 3.3 Supporting Infrastructure

**Note**: The `manage_review_prompts.md` command has been removed as it's not needed for the core workflow. The system uses two fixed prompt templates (simplicity and comprehensive) which are sufficient for most use cases.

### Phase 4: Sample Content and Testing Materials

#### 4.1 Sample Plans for Testing (2 Files for Parallelism Testing)

**File 1**: `.claude/examples/plans-examples/api-enhancement-plan.md`
**File 2**: `.claude/examples/plans-examples/logging-infrastructure-plan.md`

**Implementation Instructions for AI Agent:**
Generate two realistic software development plans for this just-prompt codebase that demonstrate:

1. **Context-Aware Content**: Plans should reference actual components in the just-prompt codebase (LLM providers, CLI structure, authentication, etc.)

2. **Deliberate Testing Elements**:
   - Include 2-3 clear strengths that reviews should identify positively
   - Include 2-3 intentional weaknesses/issues for each review perspective to catch:
     - **Simplicity issues**: Over-engineering, unnecessary complexity, unclear steps
     - **Comprehensive issues**: Missing security considerations, scalability problems, incomplete testing strategy

3. **Realistic Scope**: Each plan should be 200-400 lines of markdown covering:
   - Background/motivation
   - Technical approach
   - Implementation steps
   - Testing strategy
   - Deployment considerations

4. **Differentiated Complexity**:
   - **Plan 1 (api-enhancement-plan.md)**: Moderate complexity, clear structure, some over-engineering
   - **Plan 2 (logging-infrastructure-plan.md)**: Higher complexity, architectural decisions, security gaps

5. **Parallel Processing Validation**: Plans should be independent enough to review simultaneously while having some overlapping concerns (e.g., both touch authentication, both need testing strategies)

#### 4.2 Expected Output Examples
**Directory**: `.claude/examples/plan-reviews-examples/`

**Files to Create (for both sample plans):**
- `api-enhancement-plan-v1-simplicity-review.md` (with metadata header)
- `api-enhancement-plan-v1-comprehensive-review.md` (with metadata header)
- `api-enhancement-plan-v1-revised.md` (with metadata header, if issues found)
- `logging-infrastructure-plan-v1-simplicity-review.md` (with metadata header)
- `logging-infrastructure-plan-v1-comprehensive-review.md` (with metadata header)
- `logging-infrastructure-plan-v1-revised.md` (with metadata header, if issues found)

### Phase 5: Implementation Validation and Testing

#### 5.1 Thinking Budget Tests
```bash
# Test basic thinking budget (named arguments)
/plan_review_revise PLANS="sample_plan.md" REVIEW_PERSPECTIVES="simplicity" THINKING_BUDGET="think hard"

# Test basic thinking budget (natural language)  
"review sample_plan.md using simplicity perspective with think hard"

# Test enhanced thinking budget (named arguments)
/plan_review_revise PLANS="sample_plan.md" REVIEW_PERSPECTIVES="comprehensive" THINKING_BUDGET="think super hard"

# Test enhanced thinking budget (natural language)
"review sample_plan.md comprehensively and think super hard about it"

# Test maximum thinking budget (natural language)
"plan review revise sample_plan.md comprehensive perspective ultrathink mode"

# Test multiple plans (natural language)
"review plan1.md and plan2.md using both simplicity and comprehensive perspectives with think super hard, save to reviews directory"
```

#### 5.2 Error Handling Validation
- Test behavior with non-existent files - should fail gracefully with clear error message
- Test behavior with files containing special characters in names - should fail gracefully
- Test behavior with invalid perspective names - should provide helpful error
- Verify error messages are actionable and specific

#### 5.3 Observability Validation
- Verify metadata headers appear in all output files
- Confirm natural language input is captured in `natural_language_input` field
- Verify exact string matching for thinking budget in `parsed_thinking_budget` field
- Ensure timestamps are ISO format
- Verify prompt_template field shows correct .md filename

#### 5.4 File Naming and Revision Tests
- Verify file naming follows [plan-name]-v1-[perspective]-review.md format
- Verify revised plans follow [plan-name]-v1-revised.md format
- Test that revised plans are always generated when critical issues found
- Validate output directory organization

#### 5.5 Parallel Processing Tests
- Verify multiple Task invocations work correctly (always enabled)
- Test error handling when files don't exist
- Validate output file naming consistency
- Confirm thinking budget application in synthesis phases

### Phase 6: Documentation and Usage Examples

#### 6.1 User Documentation
**File**: `ai-docs/plan-review-workflow-guide-v2.2.md`

**Content Requirements:**
- Complete usage guide with thinking budget examples
- Explanation of simplicity vs comprehensive perspectives
- Natural language examples that trigger different thinking budgets
- How to read and use metadata headers for debugging
- Best practices for plan writing to work well with reviews
- Integration with existing development workflow

#### 6.2 Usage Examples Collection
**File**: `ai-docs/plan-review-usage-examples-v2.2.md`

**Required Examples:**
```bash
# Quick simplicity check
/plan_review_revise PLANS="my-plan.md" REVIEW_PERSPECTIVES="simplicity" THINKING_BUDGET="think hard"

# Thorough comprehensive analysis
/plan_review_revise PLANS="production-plan.md" REVIEW_PERSPECTIVES="comprehensive" THINKING_BUDGET="think super hard"

# Both perspectives with maximum thinking budget
/plan_review_revise PLANS="complex-plan.md" REVIEW_PERSPECTIVES="simplicity,comprehensive" THINKING_BUDGET="ultrathink"

# Multiple plans with enhanced thinking budget
/plan_review_revise PLANS="api-migration-plan.md,database-schema-plan.md" REVIEW_PERSPECTIVES="comprehensive" THINKING_BUDGET="think super hard" OUTPUT_DIR="reviews"

# Multiple plans with multiple perspectives
/plan_review_revise PLANS="feature-plan.md,security-plan.md" REVIEW_PERSPECTIVES="simplicity,comprehensive" THINKING_BUDGET="ultrathink" OUTPUT_DIR="multi-reviews"
```

## Implementation Steps Summary

### Step 1: Foundation Setup
1. Create simplified directory structure
2. Verify Claude Code can access directories
3. Test basic file operations

### Step 2: Prompt Template Creation (2 files only)
1. Write simplicity_review.md template
2. Write comprehensive_review.md template  
3. Test each template individually
4. Validate output format consistency

### Step 3: Main Command Implementation
1. Create plan_review_revise.md with thinking budget YAML frontmatter
2. Implement intelligent thinking budget detection and mapping
3. Add metadata header generation to all output files
4. Test natural language → thinking budget conversion
5. Verify parallel Task coordination with thinking budget application

### Step 4: Supporting Infrastructure
1. Create manage_review_prompts.md command
2. Generate sample testing materials with metadata headers
3. Create expected output examples
4. Set up validation procedures

### Step 5: Testing and Validation
1. Test all thinking budget mapping scenarios
2. Validate natural language detection accuracy  
3. Verify metadata headers contain correct interpretation data
4. Test graceful error handling for missing files and invalid inputs
5. Confirm thinking budget improves output quality appropriately
6. Test error handling and edge cases

### Step 6: Documentation and Examples
1. Write complete user guide with thinking budget focus
2. Create diverse usage examples showing thinking budget variations
3. Document natural language patterns that trigger different budgets
4. Explain how to use metadata headers for debugging
5. Generate team onboarding materials

## Success Criteria

- [ ] Directory structure created correctly
- [ ] Both prompt templates functional and tested
- [ ] Natural language correctly maps to thinking budget terminology
- [ ] All output files include interpretation metadata headers
- [ ] Metadata headers accurately capture command interpretation
- [ ] Thinking budget levels produce measurably different analysis quality
- [ ] Parallel processing works reliably with thinking budget application
- [ ] Auto-revision quality scales with thinking budget level
- [ ] Output files follow exact naming conventions
- [ ] Graceful error handling with clear, actionable error messages
- [ ] Complete documentation with thinking budget examples
- [ ] Integration with existing workflow is seamless

## Thinking Budget Quality Expectations

### Basic (think hard)
- **Simplicity Review**: Detailed complexity analysis with alternatives
- **Comprehensive Review**: Thorough quality assessment with examples
- **Synthesis**: Pattern identification and conflict resolution
- **Revision**: Balanced trade-offs while maintaining objectives

### Enhanced (think super hard) 
- **Simplicity Review**: Comprehensive simplification strategy with multiple approaches
- **Comprehensive Review**: In-depth analysis with edge cases and implications
- **Synthesis**: Nuanced prioritization with impact analysis
- **Revision**: Comprehensive redesign with architectural considerations

### Maximum (ultrathink)
- **Simplicity Review**: Strategic simplification with long-term implications
- **Comprehensive Review**: Exhaustive analysis with stakeholder impact
- **Synthesis**: Strategic synthesis with organizational implications  
- **Revision**: Complete strategic revision with ecosystem considerations

## Observability Features

### Simple Metadata Headers (In Output Files)
Each generated file includes:
- Original natural language input
- Parsed thinking budget  
- ISO timestamp
- Revision triggers (for plan v2 files)
- Prompt template used

### Error Handling Strategy
- **File not found**: Clear error message with attempted search paths
- **Invalid perspective**: List valid perspectives with examples
- **Invalid thinking budget**: Show exact valid terms from dropdown
- **Directory creation failure**: Specific error with permissions guidance
- **Parsing failure**: Fall back to defaults with warning in metadata

### Debugging Support
- **Metadata**: Quick parameter verification in output files
- **Output File Presence**: Missing files indicate where process failed
- **Error Messages**: Actionable guidance for fixing issues
- **Graceful Degradation**: Partial success continues with clear reporting

## Files to be Created (14 total - Simplified from 18)

### Commands (1 file)
- `.claude/commands/plan_review_revise.md`

### Prompt Templates (2 files)
- `.claude/prompts/simplicity_review.md`
- `.claude/prompts/comprehensive_review.md`

### Testing Materials (8 files)
- `.claude/examples/plans-examples/api-enhancement-plan.md`
- `.claude/examples/plans-examples/logging-infrastructure-plan.md`
- `.claude/examples/plan-reviews-examples/api-enhancement-plan-v1-simplicity-review.md`
- `.claude/examples/plan-reviews-examples/api-enhancement-plan-v1-comprehensive-review.md`
- `.claude/examples/plan-reviews-examples/api-enhancement-plan-v1-revised.md`
- `.claude/examples/plan-reviews-examples/logging-infrastructure-plan-v1-simplicity-review.md`
- `.claude/examples/plan-reviews-examples/logging-infrastructure-plan-v1-comprehensive-review.md`
- `.claude/examples/plan-reviews-examples/logging-infrastructure-plan-v1-revised.md`

### Documentation (3 files)
- `ai-docs/plan-review-workflow-guide-v2.2.md`
- `ai-docs/plan-review-usage-examples-v2.2.md`
- `ai-docs/plan-review-thinking-budget-guide.md`

This streamlined v2.2 implementation plan provides Claude with everything needed to build the core automated plan review system with intelligent thinking budget allocation while maintaining elegant simplicity through reduced logging complexity and graceful error handling.