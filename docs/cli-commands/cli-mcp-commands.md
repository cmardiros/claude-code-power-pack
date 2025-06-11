# Complete Claude MCP Command Reference

## Quick Example

**Given this MCP JSON configuration:**
```json
{
  "mcpServers": {
    "macos-notification": {
      "command": "uvx",
      "args": ["git+ssh://git@github.com/githubuser/mcp-project-name.git"]
    }
  }
}
```

**Add the server (local scope - default):**
```bash
claude mcp add-json macos-notification '{"command":"uvx","args":["git+ssh://git@github.com/githubuser/mcp-project-name.git"]}'
```

**Add the server at user scope:**
```bash
claude mcp add-json macos-notification '{"command":"uvx","args":["git+ssh://git@github.com/githubuser/mcp-project-name.git"]}' --scope user
```

**Remove the server:**
```bash
claude mcp remove macos-notification
```

**Get server details:**
```bash
claude mcp get macos-notification
```

## Main Command
```
claude mcp [options] [command]
```
**Description:** Configure and manage MCP servers

## Commands & Options

### `serve [options]`
**Description:** Start the Claude Code MCP server

**Options:**
- `-d, --debug` - Enable debug mode
- `--verbose` - Override verbose mode setting from config
- `-h, --help` - Display help for command

### `add [options] <name> <commandOrUrl> [args...]`
**Description:** Add a server

**Required Parameters:**
- `<name>` - Server name
- `<commandOrUrl>` - Command or URL for the server

**Optional Parameters:**
- `[args...]` - Additional arguments for the server

**Options:**
- `-s, --scope <scope>` - Configuration scope (local, user, or project) [default: "local"]
- `-t, --transport <transport>` - Transport type (stdio, sse) [default: "stdio"]
- `-e, --env <env...>` - Set environment variables (e.g. -e KEY=value)
- `-H, --header <header...>` - Set HTTP headers for SSE transport (e.g. -H "X-Api-Key: abc123" -H "X-Custom: value")
- `-h, --help` - Display help for command

### `remove [options] <name>`
**Description:** Remove an MCP server

**Required Parameters:**
- `<name>` - Server name to remove

**Options:**
- `-s, --scope <scope>` - Configuration scope (local, user, or project) [default: "local"]
- `-h, --help` - Display help for command

### `list [options]`
**Description:** List configured MCP servers

**Options:**
- `-h, --help` - Display help for command

### `get [options] <name>`
**Description:** Get details about an MCP server

**Required Parameters:**
- `<name>` - Server name to get details for

**Options:**
- `-h, --help` - Display help for command

### `add-json [options] <name> <json>`
**Description:** Add an MCP server (stdio or SSE) with a JSON string

**Required Parameters:**
- `<name>` - Server name
- `<json>` - JSON configuration string

**Options:**
- `-s, --scope <scope>` - Configuration scope (local, user, or project) [default: "local"]
- `-h, --help` - Display help for command

### `add-from-claude-desktop [options]`
**Description:** Import MCP servers from Claude Desktop (Mac and WSL only)

**Options:**
- `-s, --scope <scope>` - Configuration scope (local, user, or project) [default: "local"]
- `-h, --help` - Display help for command

### `reset-project-choices [options]`
**Description:** Reset all approved and rejected project-scoped (.mcp.json) servers within this project

**Options:**
- `-h, --help` - Display help for command

### `help [command]`
**Description:** Display help for command

**Optional Parameters:**
- `[command]` - Specific command to get help for

## Global Options
- `-h, --help` - Display help for command

## Configuration Scopes

The `--scope` option appears in multiple commands and accepts these values:
- `local` - Configuration applies to current directory only [default]
- `user` - Configuration applies to current user globally  
- `project` - Configuration applies to current project

## Transport Types

The `--transport` option in the `add` command supports:
- `stdio` - Standard input/output transport [default]
- `sse` - Server-sent events transport

## Usage Examples

```bash
# Add a new MCP server with stdio transport
claude mcp add my-server "/path/to/server" --scope user

# Add a server with SSE transport and headers
claude mcp add api-server "https://api.example.com" --transport sse --header "X-Api-Key: abc123"

# List all configured servers
claude mcp list

# Remove a server from user scope
claude mcp remove my-server --scope user

# Import servers from Claude Desktop
claude mcp add-from-claude-desktop --scope user
```