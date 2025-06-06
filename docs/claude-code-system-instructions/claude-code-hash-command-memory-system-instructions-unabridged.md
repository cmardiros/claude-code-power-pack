# Claude Code # Command Memory System: Unabridged System Instructions Documentation

## How to Reproduce This Information

**If you want to ask Claude Code for detailed information about the # memory feature, use this exact prompt:**

```
I want to understand how to use the # syntax for adding memories in Claude Code. I've seen examples like:

# Add to memory. Try "Always use descriptive variable names"
# to memorize

From your direct knowledge about Claude Code:

1. What happens when I type `# Remember this project uses TypeScript`?
2. How does the `#` memory syntax work - does it save to CLAUDE.md files?
3. Can you explain the simplest way to add something to memory using `#`?
4. Do these memories persist between different Claude Code sessions?
5. Is there a difference between `# Add to memory` and just `# some instruction`?
6. How do # memories integrate with existing CLAUDE.md files?
7. What types of information work best as # memories?

Please answer based on your understanding of the `#` memory feature, not searching documentation.
```

**Important Note:** This document contains the exact information that Claude Code provided when asked for unabridged details about its # command memory system. This represents Claude Code's actual understanding of how it processes and manages memory additions.

**Related Documentation:** The # command system works closely with the CLAUDE.md system. For comprehensive understanding of how these systems work together, see: [Claude Code CLAUDE.md System Instructions](./claude-code-claudemd-system-instructions-unabridged.md)

---

## # Command Memory System Instructions (From Claude Code Introspection)

### Core Memory System Mechanics

**System Understanding:**
- The # command "creates persistent memories by automatically appending content to your project's CLAUDE.md file"
- "Makes memories available across all future sessions in that project directory"
- "The persistence comes from storing information in the filesystem rather than just session memory"
- "# followed by any text as a memory command"
- "No special formatting is required - just # your instruction or information here"
- "The system is designed to be simple and natural"
- "The system is built for simplicity - just use # followed by what you want remembered"
- Integrates directly with the existing CLAUDE.md hierarchical system
- Enables real-time capture of insights and preferences during development work

### Processing and Storage

**Processing Flow:**
- "# command recognized during conversation"
- "automatically append the content (minus the #) to your CLAUDE.md file"
- "The information becomes part of my persistent context for that project, loaded at the start of every new session"
- Immediate integration into persistent context

**Usage Examples:**
- Simple syntax: `# Remember that this project uses React hooks exclusively`
- `# Use TypeScript interfaces over types for this project`
- `# Always run npm run type-check before commits`

### Integration with CLAUDE.md Hierarchy

**File Target Selection:**
- **Project-level memories**: Added to `./CLAUDE.md` for team-shared context
- **User-level memories**: Added to `~/.claude/CLAUDE.md` for personal preferences
- **Context-dependent placement**: System determines appropriate location based on content scope

**Enhancement vs Replacement:**
- "# commands enhance rather than replace existing CLAUDE.md content"
- "New memories are appended to preserve existing project context while adding new information"
- Maintains existing instruction structure and hierarchy
- Preserves manually written CLAUDE.md content

### Memory Content and Persistence

**What Makes Good Memories:**
- "Project-specific preferences and conventions"
- "Custom workflows and processes"
- "Important context about the codebase"
- "Recurring instructions you don't want to repeat"
- "Domain-specific knowledge for the project"

**Memory Quality Guidelines:**
- "Memories should be specific enough to be actionable but general enough to remain relevant over time"
- Built-in organizational assistance for clarity and grouping
- Automatic maintenance of readability and structure

**Persistence Mechanics:**
- Memories "survive beyond the current conversation"
- Become part of the permanent CLAUDE.md instruction set
- Available in all future sessions within the same context
- Integrated into the hierarchical context loading system

### Session Integration and Context Building

**Real-Time Learning:**
- Memories added during active development sessions
- Capture insights as they're discovered
- Build project knowledge incrementally
- Adapt AI behavior based on actual usage patterns

**Context Availability:**
- "# command memories load automatically when I start working in a project directory"
- "They become part of my base context, influencing how I approach tasks throughout the conversation"
- Future conversations automatically include these memories
- No restart or reload required for memory activation
- Seamless integration with existing persistent instructions

### Best Practices for Memory Creation

**Effective Memory Content:**
- **Specific preferences**: "Use TypeScript interfaces over types for this project"
- **Tool configurations**: "Always run `npm run type-check` before commits"
- **Project patterns**: "API responses use camelCase, database uses snake_case"
- **Team conventions**: "Prefer functional components with hooks over class components"
- **Domain knowledge**: "User roles: admin, editor, viewer with specific permissions"

**Memory Scope Considerations:**
- **Project-specific**: Technical decisions, architecture patterns, team preferences
- **Personal**: Individual coding style, preferred shortcuts, personal workflow preferences
- **Universal**: General preferences that apply across all projects

### Memory Organization and Management

**Built-in Organization Assistance:**
- "I'm designed to help organize memories by suggesting logical groupings and helping maintain clarity"
- System automatically maintains readability and structure

**Hierarchical Integration:**
- Memories follow the same priority system as CLAUDE.md files
- Project memories take precedence over user memories for conflicts
- Directory-specific memories override broader project memories
- Maintains existing import and reference patterns

**Content Organization:**
- New memories organized logically within existing CLAUDE.md structure
- Related memories grouped together when possible
- Maintains readability and structure of instruction files
- Can be manually reorganized and refined later

**Simplicity Focus:**
- "The system is built for simplicity - just use # followed by what you want remembered"
- No complex syntax or formatting requirements
- Natural language processing for memory content

### Advanced Memory Patterns

**Incremental Learning:**
- Build project understanding over time through repeated # commands
- Capture evolving team preferences and standards
- Document discovered patterns and anti-patterns
- Create living documentation of project evolution

**Context-Aware Memory Addition:**
- System considers current working directory for memory placement
- Understands project vs personal scope based on content
- Integrates with existing project context and constraints
- Maintains consistency with established patterns

### Team Collaboration Through Memories

**Shared Knowledge Building:**
- Project-level memories become team knowledge
- Capture and share discovered best practices
- Document team decisions and reasoning
- Create consistent AI behavior across team members

**Version Control Integration:**
- # command updates to CLAUDE.md can be committed with regular changes
- Memory evolution tracked through git history
- Team members can review and refine shared memories
- Collaborative improvement of AI instruction quality

---

## Additional System Guidance for # Command Memory

### Memory Content Guidelines

**High-Value Memory Types:**
- **Decision Documentation**: "Chose Redux over Context API for complex state management"
- **Tool Integration**: "Use Prettier with 2-space indentation and single quotes"
- **Architecture Decisions**: "Services communicate via REST APIs, no direct database access"
- **Domain Rules**: "Price calculations always use BigDecimal to avoid floating point errors"
- **Workflow Preferences**: "Feature branches follow pattern: feature/TICKET-123-description"

**Avoid Low-Value Memories:**
- Generic programming advice that applies to all projects
- Temporary decisions that may change frequently
- Information already well-documented elsewhere
- Personal reminders not relevant to AI assistance

### Memory Timing and Context

**Optimal Memory Addition Timing:**
- **During discovery**: When learning new project patterns
- **After decisions**: Document choices and reasoning
- **Problem resolution**: Capture solutions to complex issues
- **Standard establishment**: When team agrees on conventions
- **Tool adoption**: When integrating new development tools

**Context Sensitivity:**
- Consider current working directory for memory scope
- Understand when memories should be project vs personal
- Recognize team vs individual decision contexts
- Maintain awareness of existing instruction hierarchy

### Memory Evolution and Maintenance

**Iterative Improvement:**
- Memories can be refined through subsequent # commands
- Existing memories can be updated or clarified
- Contradictory memories resolved through latest additions
- Gradual improvement of instruction quality over time

**Manual Refinement:**
- # command memories can be manually edited in CLAUDE.md files
- Organize and structure memories for better readability
- Combine related memories for efficiency
- Remove outdated or superseded memories

### Integration with Development Workflows

**Git Workflow Integration:**
- Memory additions can be included in regular commits
- Changes to CLAUDE.md tracked like other project files
- Team review of memory additions through pull requests
- Memory evolution as part of project development history

**Continuous Learning:**
- # command enables ongoing AI improvement during development
- Captures knowledge that emerges through actual usage
- Builds project-specific AI expertise over time
- Creates increasingly effective development assistance

---

## Summary

The # command memory system represents Claude Code's approach to continuous learning and context building. Key principles include:

1. **Real-Time Learning**: Capture insights and preferences during active development
2. **Persistent Context**: Memories survive sessions and become permanent instructions
3. **Hierarchical Integration**: Works seamlessly with existing CLAUDE.md system
4. **Team Collaboration**: Project memories become shared team knowledge
5. **Incremental Improvement**: Build AI effectiveness gradually through usage
6. **Context Awareness**: Smart placement of memories based on scope and content

The system transforms Claude Code from a static AI assistant into a continuously learning development partner that adapts to project needs and team preferences through real-world usage patterns. The # command bridges the gap between immediate needs and long-term AI optimization, creating a feedback loop that improves development assistance over time.