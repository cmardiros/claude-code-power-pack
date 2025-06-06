# Claude Code Slash Commands: Unabridged System Instructions Documentation

## How to Reproduce This Information

**If you want to ask Claude Code for detailed information about slash commands, use this exact prompt:**

```
I'm trying to optimize my use of Claude Code slash commands for development workflows. Don't search any documentation or project files - I want your direct knowledge about how you've been designed to work with slash commands.

From your own understanding, could you share the specific guidance you have about:

1. How the slash command system works in Claude Code - what makes them reusable prompts and how parameter substitution functions

2. What specific command structures and parameter patterns you're designed to work with (simple arguments, named parameters, defaults)

3. How you process and execute slash commands differently from regular prompts

4. The file organization and storage system for slash commands (.claude/commands/ structure)

5. Best practices for creating effective slash commands that work well with your capabilities

6. Any specific guidance about parameter handling, error cases, or command optimization

7. How slash commands integrate with your other capabilities and tools

Please answer from your own built-in knowledge about slash commands - don't use tools to search or read files. I want to understand how you've been designed to work with slash commands so I can create and use them effectively.
```

**Important Note:** This document contains the exact information that Claude Code provided when asked for unabridged details about its slash command system. This represents Claude Code's actual understanding of how it processes and executes slash commands.

---

## Slash Command System Instructions (From Claude Code Introspection)

### Core Slash Command Mechanics

**System Understanding:**
- Slash commands are "reusable prompts stored as markdown files that accept dynamic parameters"
- They function as "custom AI workflows for development tasks"
- Commands are processed through parameter substitution before execution
- The system treats them as specialized prompt templates with variable injection

### File System and Organization

**Storage Structure:**
- Commands stored in `.claude/commands/` directory
- Each command is a markdown file with `.md` extension
- File name becomes the command name (e.g., `analyze_code.md` → `/analyze_code`)
- Commands are discovered automatically when directory is present
- Claude Code automatically scans `.claude/commands/` for available commands
- Command names derived from filename (without .md extension)
- Commands become available immediately when files are created
- No restart or reload required for new commands

**Project Integration:**
- Commands can be version controlled and shared with teams
- Commands travel with the repository for consistent team workflows
- Directory structure allows for organization and categorization

### Parameter System and Substitution

**Parameter Types and Patterns:**

**Positional Parameters:**
- `{1}`, `{2}`, `{3}` syntax for simple ordered arguments
- Usage: `/command_name arg1 arg2 arg3`
- Direct position-based parameter mapping
- Simple and intuitive for basic commands

**Named Parameters:**
- `{filename}`, `{component_name}` syntax for descriptive parameters
- Clear, self-documenting parameter names
- Better maintainability and readability
- Usage context determines parameter mapping

**Default Value Parameters:**
- `{type:string}` or `{env:development}` syntax for parameters with defaults
- Automatic fallback when parameters not provided
- Enables flexible command usage with sensible defaults
- Type hints and default value specification combined

**Advanced Parameter Types:**
- **Rest Parameters**: `{...}` to capture remaining arguments
- **Optional Parameters**: Handled gracefully when not provided
- **Type-Specified Parameters**: Built-in type validation and defaults

**Legacy Parameter Patterns (Alternative Syntax):**
- `$ARGUMENTS` - Captures all provided arguments as single parameter
- `$PARAMETER_NAME` syntax for specific named values  
- `${PARAM:-default_value}` syntax for optional parameters

### Command Processing Flow

**Detailed Execution Sequence:**
1. Command file located in `.claude/commands/` directory
2. Template loaded with parameter placeholders identified
3. Parameter substitution using patterns like `{1}`, `{2}`, `{param_name}`
4. Expanded prompt sent to Claude for processing
5. Full Claude Code capabilities available during execution

**Parameter Substitution Mechanics:**
- **Template Loading**: Command markdown file loaded as template
- **Parameter Recognition**: `{parameter}` patterns identified and mapped
- **Value Substitution**: Parameters replaced with provided values
- **Default Resolution**: Missing parameters use specified defaults (`{type:string}`)
- **Error Handling**: Missing required parameters handled gracefully
- **Rest Parameter Expansion**: `{...}` captures remaining arguments

**Parameter Handling Specifics:**
- Multi-word parameters require quotes: `PARAM="multi word value"`
- Special characters preserved within quoted parameters
- Nested quotes handled appropriately
- Whitespace preserved in quoted strings
- Named parameters can be provided in any order
- Parameter validation occurs after substitution
- Missing parameters handled gracefully with clear feedback

**Processing Differences from Regular Prompts:**
- Pre-structured context and instructions built into commands
- Specific output format expectations included
- Built-in error handling patterns for parameter validation
- Workflow-specific guidance that regular prompts lack

### Integration with Claude Code Capabilities

**Full Tool Access:**
- Slash commands have access to all Claude Code tools during execution
- Can read files, execute bash commands, search codebases
- Can modify files and create commits
- Support for complex multi-step workflows

**Context Awareness:**
- Commands execute with full project context
- CLAUDE.md files still apply during command execution
- Git repository state and environment context available
- Working directory and file system access maintained

**Performance and Efficiency:**
- Commands processed as single prompt units
- Parameter substitution occurs before main processing
- Full context and capabilities available during execution
- No performance penalty for using commands vs direct prompts
- Commands inherit all resource constraints and capabilities
- Token limits apply to final substituted prompt
- Tool usage governed by same policies as regular prompts

### Command Design Best Practices

**File Naming and Organization:**
- **Kebab-case filenames**: Map to slash command names (e.g., `analyze-code.md` → `/analyze-code`)
- **Descriptive names**: Clear indication of command purpose
- **Single responsibility**: Each command should do one thing well
- **Logical grouping**: Related commands can share common prefixes

**Effective Command Structure:**
- **Clear parameter names**: Use descriptive names like `{component_name}` not `{x}`
- **Include examples**: Show expected usage patterns within command files
- **Error handling**: Anticipate missing parameters or invalid inputs
- **Context setting**: Include relevant background information
- **Output specification**: Define exactly what format you expect

**Parameter Design Excellence:**
- **Descriptive naming**: `{filename}`, `{component_name}` over generic names
- **Sensible defaults**: Provide fallbacks for optional parameters (`{env:development}`)
- **Type hints**: Use `{type:string}` pattern for clarity and validation
- **Rest parameters**: Use `{...}` for variable-length argument lists
- **Parameter validation**: Include checks for required parameters in command logic

**Command Content Optimization:**
- **Token efficiency**: Balance completeness with conciseness
- **Error messages**: Clear guidance when parameters are missing/invalid
- **Escape handling**: Proper handling of special characters in parameters
- **Validation patterns**: Built-in parameter checking and error handling
- **Workflow integration**: Commands should leverage full Claude Code capability set

### Error Handling and Edge Cases

**Parameter Validation:**
- Missing required parameters leave literal `$VARIABLE` in prompt
- Commands should include parameter validation logic where needed
- Clear error messages when required parameters missing

**File System Dependencies:**
- Commands fail gracefully when `.claude/commands/` doesn't exist
- Non-existent command names result in command not found errors
- File permission issues prevent command discovery

### Advanced Command Patterns

**Multi-Parameter Commands:**
- Support for complex parameter combinations
- Conditional logic based on parameter presence
- Parameter-dependent workflow variations

**Template-Based Workflows:**
- Commands can serve as workflow templates
- Support for complex development task automation
- Integration with project-specific patterns and conventions

**Team Collaboration:**
- Commands enable consistent team workflows
- Standardize common development tasks
- Share best practices through command libraries

### Integration Patterns

**Seamless Integration with Claude Code Systems:**
- **Tool usage**: Commands can instruct Claude to use specific tools
- **CLAUDE.md**: Commands inherit project context from CLAUDE.md files
- **File operations**: Commands often involve reading/editing specific files
- **Workflow automation**: Commands can chain multiple operations
- **Memory systems**: Commands can reference and update project memory

**Development Workflow Integration:**
- Commands can be integrated into git hooks
- Support for CI/CD pipeline integration
- IDE integration possible through command execution
- Watch mode and automated triggering supported

**Project-Specific Customization:**
- Commands can be tailored to specific project needs
- Framework-specific command libraries
- Domain-specific workflow automation
- Team coding standard enforcement

---

## Summary

The slash command system represents Claude Code's approach to reusable, parameterized AI workflows. Key principles include:

1. **Template-Based Automation**: Commands function as prompt templates with dynamic parameter injection
2. **Team Collaboration**: Version-controlled commands enable consistent team workflows  
3. **Full Integration**: Commands have access to complete Claude Code capabilities
4. **Flexible Parameterization**: Support for simple, named, and default parameter patterns
5. **Project Context**: Commands execute with full project awareness and context
6. **Workflow Optimization**: Enable standardization and automation of common development tasks

The system is designed to transform repetitive development tasks into reusable, shareable workflows while maintaining the full power and flexibility of Claude Code's capabilities.