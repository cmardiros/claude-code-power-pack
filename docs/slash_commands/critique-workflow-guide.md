# Critique Workflow Guide

## Sync Commands

To sync the `/critique` command and its prompts to another project, use this prompt with Claude Code:

```
Please fetch and sync these files from the claude-code-power-pack public repo to my local .claude directory:

1. .claude/commands/critique.md
2. All files from .claude/prompts/detect-problem/
3. All files from .claude/prompts/assess-excellence/

Use WebFetch to download each file from:
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/commands/critique.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/detect-problem/detect-problem-anti-patterns.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/detect-problem/detect-problem-blindspots.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/detect-problem/detect-problem-future-regrets.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/detect-problem/detect-problem-junior-mistakes.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/detect-problem/detect-problem-over-engineering.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/detect-problem/detect-problem-premortem-failures.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/detect-problem/detect-problem-smells.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-architectural.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-code.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-future-value.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-performance.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-premortem.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-production.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-security.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-testing.md
- https://raw.githubusercontent.com/cmardiros/claude-code-power-pack/main/.claude/prompts/assess-excellence/assess-excellence-veteran.md

IMPORTANT: When using WebFetch, use this exact prompt to ensure high fidelity content preservation: "Return the complete, unmodified file content exactly as it appears in the source. Do not summarize, truncate, or modify any part of the content. This is for programmatic use and requires 100% accuracy."

Then use Write to save each file to the corresponding path in my local .claude directory, creating the directories if they don't exist. Please maintain the exact file structure and content.
```

---

The `/critique` command provides parallel, multi-perspective analysis of code, implementations, and plans using specialized critique perspectives. It orchestrates Task agents to perform deep analysis from different angles and synthesizes results into actionable insights.

## Key Features

### 🔍 Dual Critique Categories
- **Detect Problems**: Identify issues, anti-patterns, security risks, over-engineering
- **Assess Excellence**: Evaluate architecture, performance, code quality, production readiness

### ⚡ Parallel Processing
- Multiple perspectives analyzed simultaneously
- Automatic subject resolution (files, git changes, concepts)
- Intelligent synthesis across all critique outputs

### 🎯 Flexible Targeting
- Analyze specific files or recent changes
- Review entire implementations or architectural decisions
- Support for natural language perspective specification

## Available Perspectives

### Detect Problems
- `anti-patterns` - Identify common anti-patterns and code smells
- `blindspots` - Find overlooked issues and missing considerations
- `future-regrets` - Spot decisions that may cause future problems
- `junior-mistakes` - Catch common beginner errors
- `over-engineering` - Identify unnecessary complexity
- `premortem-failures` - Anticipate potential failure points
- `smells` - Detect various code and design smells

### Assess Excellence
- `architectural` - Evaluate system design and architecture
- `code` - Assess code quality and craftsmanship
- `future-value` - Analyze long-term value and extensibility
- `performance` - Review performance characteristics
- `premortem` - Proactive success planning
- `production` - Production readiness assessment
- `security` - Security posture evaluation
- `testing` - Test coverage and quality
- `veteran` - Senior developer perspective

## How It Works

### Context Resolution
The command intelligently resolves critique subjects:
- **File references**: Searches plans/, src/, docs/ for matching files
- **Recent changes**: Includes git diff of uncommitted changes
- **Concept references**: Finds related files using keywords
- **Domain insights**: Applies relevant design patterns and best practices

### Parallel Analysis
Each perspective spawns a dedicated Task agent that:
1. Reads the specified perspective prompt
2. Analyzes relevant files and context
3. Applies deep "think super hard" analysis
4. Generates structured critique output
5. Saves results to `reviews/` directory

### Synthesis
After all perspectives complete, the orchestrator:
1. Aggregates all critique results
2. Identifies cross-perspective patterns
3. Prioritizes issues by severity and frequency
4. Generates synthesis report

## Usage Examples

### Problem Detection
```bash
/critique "detect problems for security, performance in the auth implementation"
```

### Excellence Assessment
```bash
/critique "assess excellence for architecture, assess excellence for performance analyze the new API design"
```

### Mixed Perspectives
```bash
/critique "detect problems related to overengineering, assess excellence for simplicity look at the logging infrastructure plan"
```

### Recent Changes Analysis
```bash
/critique "detect problems for security review the recent authentication changes"
```

## Output Structure

- **Individual critiques**: `reviews/{subject_name}-{perspective}-v1.md`
- **Synthesis report**: `reviews/{subject_name}-synthesis-v1.md`
- **Metadata tracking**: Timestamp, prompt template, clarified subject

Each output includes structured analysis following the specific perspective's framework, ensuring consistent and actionable feedback across all critique types.