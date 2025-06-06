# Plan-Review-Revise Workflow Guide

## Sync Commands

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

---

## Overview

The automated plan-review-revise workflow provides intelligent, multi-perspective analysis of software development plans using Claude Code slash commands. This system helps teams identify issues, reduce complexity, and improve plan quality before implementation begins.

## Key Features

### 🧠 Intelligent Thinking Budget Allocation
- **Basic (think hard)**: Pattern identification and conflict resolution
- **Enhanced (think super hard)**: Nuanced prioritization and impact analysis  
- **Maximum (ultrathink)**: Comprehensive synthesis with strategic implications

### 🔍 Dual Review Perspectives
- **Simplicity Review**: Focus on complexity reduction and clarity
- **Comprehensive Review**: Multi-layered QA validation covering security, feasibility, and maintainability

### ⚡ Parallel Processing
- Reviews multiple plans and perspectives simultaneously
- Automatic error handling with graceful degradation
- Intelligent synthesis across all review outputs

### 🔄 Automated Revision
- Generates improved plans when critical issues are identified
- Maintains core objectives while addressing key concerns
- Documents changes and rationale with appropriate depth

## How It Works

### Parallel Processing
When multiple plans or perspectives are specified, reviews run in parallel for faster results.

### Thinking Budget Levels
- **"think hard"** - Quick reviews for familiar domains and straightforward plans
- **"think super hard"** - Balanced analysis for production plans (default)
- **"ultrathink"** - Maximum analysis for critical systems and high-risk changes

### Review Perspectives
- **Simplicity** - Focuses on complexity reduction, clarity, over-engineering detection
- **Comprehensive** - Quality standards, security, feasibility, risk identification

### Natural Language Parsing
The system supports natural language input but has limitations. If parsing fails (too fuzzy), fall back to keyword syntax.

### Output Files
- Review analyses saved to `plan-reviews/`: `[plan-name]-v1-[perspective]-review.md`
- Revised plans saved to `plans/`: `[plan-name]-v1-revised.md`

## Prerequisites

**Plans must exist before review**. Ask Claude to create your implementation plan and save it in the `/plans/` folder. Follow prompt engineering best practices.

**Best Practice**: Version your plans (e.g., `logging-infrastructure-plan-v1.md`) to track review and revision cycles.

## How to Use

### Basic Usage

**Keyword Syntax:**
```bash
/plan_review_revise PLANS="my-plan.md" REVIEW_PERSPECTIVES="comprehensive" THINKING_BUDGET="think super hard"
```

**Natural Language Equivalent:**
```bash
/plan_review_revise review my-plan comprehensively and think super hard
```

### Multiple Plans and Perspectives

**Keyword Syntax:**
```bash
/plan_review_revise PLANS="plan1.md,plan2.md" REVIEW_PERSPECTIVES="simplicity,comprehensive" THINKING_BUDGET="ultrathink"
```

**Natural Language Equivalent:**
```bash
/plan_review_revise review plan1.md and plan2.md using both perspectives ultrathink mode
```

### Custom Output Location

**Keyword Syntax:**
```bash
/plan_review_revise PLANS="my-plan.md" REVIEW_PERSPECTIVES="simplicity" OUTPUT_DIR="plan-reviews/sprint-15"
```

**Natural Language Equivalent:**
```bash
/plan_review_revise review my-plan.md for simplicity save to plan-reviews/sprint-15
```

## Examples (Using Dummy `logging-infrastructure-plan.md`)

### Quick Simplicity Check

**Keyword:**
```bash
/plan_review_revise PLANS="logging-infrastructure-plan.md" REVIEW_PERSPECTIVES="simplicity" THINKING_BUDGET="think hard"
```

**Natural Language:**
```bash
/plan_review_revise review the logging infrastructure plan using simplicity perspective and think hard
```

### Comprehensive Analysis

**Keyword:**
```bash
/plan_review_revise PLANS="logging-infrastructure-plan.md" REVIEW_PERSPECTIVES="comprehensive" THINKING_BUDGET="think super hard"
```

**Natural Language:**
```bash
/plan_review_revise analyze the logging infrastructure plan comprehensively and think super hard
```

### Maximum Analysis (Both Perspectives)

**Keyword:**
```bash
/plan_review_revise PLANS="logging-infrastructure-plan.md" REVIEW_PERSPECTIVES="simplicity,comprehensive" THINKING_BUDGET="ultrathink"
```

**Natural Language:**
```bash
/plan_review_revise review logging infrastructure plan both perspectives ultrathink mode
```

### Quick Test Commands
You can try these immediately with the existing plan:

```bash
/plan_review_revise review the logging infrastructure plan for simplicity and think hard
/plan_review_revise analyze logging infrastructure plan comprehensively think super hard  
/plan_review_revise review logging-infrastructure-plan both perspectives ultrathink
```
