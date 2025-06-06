# Claude Code System Instructions: Unabridged Documentation

## How to Reproduce This Information

**If you want to ask Claude Code for this information again, use this exact prompt:**

```
I'm starting a new project and want to set up CLAUDE.md files effectively. Don't search any documentation or project files - I want your direct knowledge about how you've been designed to work with CLAUDE.md.

From your own understanding, could you share the specific guidance you have about:

1. How the CLAUDE.md system works in Claude Code - what makes it "persistent instructions" and how it becomes part of your context

2. What specific content you're designed to look for in CLAUDE.md files (commands, code standards, project constraints, etc.) and why these are important

3. The specific language patterns you respond best to (like "IMPORTANT", "YOU MUST") and how to structure instructions effectively

4. CLAUDE.md file organization - placement, hierarchy, the @path/to/file.md import syntax, and project vs user memory

5. How you're designed to treat CLAUDE.md as "living documentation" and any specific update patterns (like the # command)

6. Any other specific guidance about CLAUDE.md effectiveness, token efficiency, or best practices for development teams

Please answer from your own built-in knowledge about CLAUDE.md - don't use tools to search or read files. I want to understand how you've been designed to work with CLAUDE.md files so I can create them effectively.
```

**Important Note:** This document contains the exact wording that Claude Code (Claude Sonnet 4) provided when asked for unabridged details about its system instructions regarding CLAUDE.md and related functionality. This is not summary content or external research - these are the actual instructions Claude Code has been given.

**Related Documentation:** The CLAUDE.md system works closely with the # command memory system for real-time updates. For comprehensive understanding of how these systems work together, see: [Claude Code # Command Memory System Instructions](./claude-code-hash-command-memory-system-instructions-unabridged.md)

---

## CLAUDE.md System Instructions (Exact Wording from Claude Code)

### Memory and CLAUDE.md System

From Claude Code's system instructions, the specific guidance about the CLAUDE.md system includes:

**Memory Management:**
- **Project memory**: Through `./CLAUDE.md` files for team-shared instructions
- **User memory**: Via `~/.claude/CLAUDE.md` for personal preferences across all projects  
- **Import syntax**: Using `@path/to/file.md` for better organization and cross-team collaboration

**Core System Understanding:**
- "CLAUDE.md files become part of my prompt context, making them 'persistent instructions that guide AI behavior throughout development workflows'"
- CLAUDE.md files "remain active throughout our entire conversation session, unlike regular messages that can be forgotten due to context limits"
- They function as persistent instructions that don't get lost to context window limitations
- Claude should look for CLAUDE.md files in the current directory and use them to understand project-specific context

### Essential Content Guidelines (Exact Wording)

**Commands Documentation (Exact Instructions):**
- "Document frequently used commands to prevent Claude from repeatedly searching the codebase"
- "Include build commands, testing procedures, linting tools, and deployment scripts with clear usage examples"

**Content Prioritization Framework:**
1. Commands and scripts (build, test, lint commands)
2. Code standards and conventions (formatting, naming, architecture patterns)
3. Project constraints (dependencies, frameworks, deployment requirements)
4. Development workflows (git practices, review processes)
5. Tool configurations (which linters, test frameworks, deployment tools)
6. Domain-specific context (business logic, technical requirements)

**Code Standards (Exact Instructions):**
- "Specify language-specific conventions, import patterns, and architectural preferences"
- "For example, preferring ES modules over CommonJS, destructuring import patterns, or specific framework conventions"

**Critical Instructions (Exact Instructions):**
- "Document unexpected behaviors, known issues, or critical constraints that might not be obvious from the codebase alone"
- "This prevents Claude from inadvertently breaking existing functionality or violating project constraints"

**Tool Integration (Exact Instructions):**
- "Specify preferred tools and their usage patterns, such as specific linters, testing frameworks, or development utilities"
- "Include configuration details and common troubleshooting approaches"

### Prompt Engineering Approach (Exact Wording)

**Emphasis Techniques (Exact Instructions):**
- "Use emphasis techniques like 'IMPORTANT' or 'YOU MUST' for critical instructions that require strict adherence"
- "Structure instructions as clear, actionable steps rather than general descriptions"

**Extended Emphasis Techniques:**
- "IMPORTANT:" - highest priority instructions
- "YOU MUST" - non-negotiable requirements
- "NEVER" - absolute prohibitions
- "ALWAYS" - consistent behaviors expected
- Imperative language ("Use X", "Run Y", "Follow Z")
- Specific examples rather than abstract descriptions

**Effective Patterns (Exact Instructions):**
- "Use imperative language: 'Always run tests before committing' rather than 'Tests should be run'"
- "Provide specific examples: Show exact command syntax and expected outputs"
- "Include context about why rules exist: Help Claude understand the reasoning behind constraints"

### Integration and Maintenance (Exact Wording)

**Living Documentation (Exact Instructions):**
- "Treat CLAUDE.md files as living documentation that evolves with your project"
- "Use Claude's `#` command to quickly add instructions during development sessions, then incorporate these additions into formal commits"

**Token Efficiency (Exact Instructions):**
- "Balance comprehensive instructions with token efficiency concerns"
- "Use the import system to load relevant context on-demand rather than including everything in every session"

### File Organization and Best Practices

**Hierarchical Context System:**
- **Root-level CLAUDE.md**: Project-wide instructions
- **Directory-specific CLAUDE.md files**: Local context for specific areas
- **@path/to/file.md syntax**: Import other markdown files to avoid duplication
- **Project vs User memory**: Project CLAUDE.md travels with repo, user CLAUDE.md is personal across projects

**When to Update CLAUDE.md:**
- Project requirements change
- New tools/frameworks are adopted
- Coding standards evolve
- Common issues are discovered
- The # command pattern helps identify when instructions are outdated or need refresh

**Core Effectiveness Principles:**
- **Token efficiency**: Be concise but specific
- **Hierarchical structure**: Most important instructions first
- **Context-specific**: Include project-specific details, not generic advice
- **Actionable instructions**: Tell Claude what to do, not just what to know
- **Examples**: Show expected patterns alongside rules
- **Team alignment**: Ensure all developers contribute to and follow the same CLAUDE.md
- **Single source of truth**: CLAUDE.md should be the definitive guide for Claude's behavior in the specific project context

---

## Summary

The CLAUDE.md system represents Claude Code's approach to persistent, project-specific AI instructions. Key principles include:

1. **Persistent Context**: CLAUDE.md files remain active throughout conversation sessions and don't get lost to context window limitations
2. **Hierarchical Organization**: Root-level for project-wide instructions, directory-specific for local context, with import system support
3. **Content Prioritization**: Commands and scripts first, followed by code standards, constraints, workflows, tools, and domain context
4. **Effective Language Patterns**: Strong emphasis techniques ("IMPORTANT", "YOU MUST", "NEVER", "ALWAYS") with imperative language and specific examples
5. **Living Documentation**: Files that evolve with projects, updated through # command integration and team collaboration
6. **Actionable Instructions**: Focus on telling Claude what to do rather than what to know, with project-specific details over generic advice

The system transforms Claude Code from a general assistant into a project-aware development partner through filesystem-based persistent instructions that serve as the single source of truth for AI behavior in specific project contexts.