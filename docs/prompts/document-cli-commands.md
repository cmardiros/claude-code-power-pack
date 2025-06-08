# CLI Command Documentation Prompt

Use this prompt to systematically document CLI commands with their complete options and subcommands.

## Prompt Template

```
I need you to document the CLI command `{COMMAND_NAME}` with complete structured output. Follow these steps:

1. **Run the main help command:**
   ```bash
   {COMMAND_NAME} --help
   ```

2. **Identify all subcommands** from the help output that show `[options]` or have parameters.

3. **For each subcommand, run its help:**
   ```bash
   {COMMAND_NAME} {SUBCOMMAND} --help
   ```
   Run these in parallel using multiple tool calls for efficiency.

4. **Create a structured markdown output** with the following format:

## Template Structure

```markdown
# Complete {COMMAND_NAME} Command Reference

## Main Command
```
{COMMAND_NAME} [options] [command]
```
**Description:** {MAIN_DESCRIPTION}

## Commands & Options

### `{subcommand} [options] <required> [optional]`
**Description:** {SUBCOMMAND_DESCRIPTION}
**Required Parameters:** (if any)
- `<param>` - Description

**Optional Parameters:** (if any)
- `[param]` - Description

**Options:**
- `-x, --long-option <value>` - Description [default: "value"]
- `-y, --flag` - Description

### {repeat for each subcommand}

## Global Options
- `-h, --help` - Display help for command
```

## Key Documentation Standards

1. **Parameter Notation:**
   - `<required>` - Required parameters in angle brackets
   - `[optional]` - Optional parameters in square brackets
   - `[args...]` - Multiple values accepted
   - `<value>` - Option requires a value

2. **Option Format:**
   - Show both short (`-x`) and long (`--long`) forms
   - Include default values when available: `[default: "value"]`
   - Group related options together

3. **Parallel Execution:**
   - Use multiple tool calls in a single message to run subcommand help queries in parallel
   - This improves efficiency when documenting commands with many subcommands

4. **Complete Coverage:**
   - Document every subcommand, even if it only has `--help`
   - Include usage patterns and parameter requirements
   - Note any platform-specific limitations

## Example Usage

To document the `claude mcp` command:
```
I need you to document the CLI command `claude mcp` with complete structured output. Follow the steps above.
```

This will produce comprehensive documentation covering all subcommands, options, and usage patterns.