There are several ways to install MCP servers to Claude Code, each suited for different use cases:

## Method 1: Add Individual MCP Servers

**Basic command syntax:**
```bash
claude mcp add   [args...]
```

**Examples:**
```bash
# Add filesystem server
claude mcp add filesystem npx -y @modelcontextprotocol/server-filesystem ~/Documents ~/Downloads

# Add with environment variables
claude mcp add my-server -e API_KEY=123 -- /path/to/server arg1 arg2

# Add SSE server
claude mcp add --transport sse sse-server https://example.com/sse-endpoint
```

## Method 2: Scope-Based Installation

You can specify where the configuration is stored using the `-s` or `--scope` flag[6]:

- **Local scope** (default): Available only in current project
- **Project scope**: Shared with everyone via `.mcp.json` file  
- **User scope**: Available across all your projects

```bash
claude mcp add -s user filesystem npx -y @modelcontextprotocol/server-filesystem ~/Documents
```

## Method 3: Import from Claude Desktop

If you already have MCP servers configured in Claude Desktop[6]:

```bash
claude mcp add-from-claude-desktop
```

This provides an interactive dialog to select which servers to import. Works on macOS and Windows Subsystem for Linux (WSL)[6].

## Method 4: Batch Installation Script

For multiple servers at once[3]:

```bash
# Sequential thinking
claude mcp add sequential-thinking npx -y @modelcontextprotocol/server-sequential-thinking

# Filesystem  
claude mcp add filesystem npx -y @modelcontextprotocol/server-filesystem ~/Documents ~/Downloads

# Puppeteer
claude mcp add puppeteer npx -y @modelcontextprotocol/server-puppeteer

# Web fetching
claude mcp add fetch npx -y @kazh/mcp-server-fetch

# Browser tools
claude mcp add browser-tools npx -y @deskai/mcp-server-browser-tools@1.2.1
```

## Method 5: Use Claude Code as MCP Server

To run Claude Code itself as an MCP server that other applications can connect to[6]:

```bash
claude mcp serve
```

## Management Commands

**List configured servers:**
```bash
claude mcp list
```

**Get server details:**
```bash
claude mcp get 
```

**Remove a server:**
```bash
claude mcp remove 
```

**Check MCP status within Claude Code:**
```
/mcp
```

## Important Notes

- Set environment variables with `-e` flags (e.g., `-e KEY=value`)[6]
- Configure startup timeout using `MCP_TIMEOUT` environment variable[6]
- Use third-party MCP servers at your own risk, especially those that access the internet[6]
- For some servers, you may need Node.js installed[4]

The most common approach is Method 1 for individual servers, while Method 3 is convenient if you're already using Claude Desktop with configured MCP servers[15].

[1] https://www.digitalocean.com/community/tutorials/claude-code-mcp-server
[2] https://modelcontextprotocol.io/quickstart/server
[3] https://www.reddit.com/r/ClaudeAI/comments/1jf4hnt/setting_up_mcp_servers_in_claude_code_a_tech/
[4] https://modelcontextprotocol.io/quickstart/user
[5] https://www.youtube.com/watch?v=oM2dXJnD80c
[6] https://docs.anthropic.com/en/docs/claude-code/tutorials
[7] https://www.getmesa.com/blog/how-to-connect-mcp-server-claude/
[8] https://github.com/steipete/claude-code-mcp
[9] https://playbooks.com/mcp/claude-code
[10] https://www.reddit.com/r/ClaudeAI/comments/1iztm9b/how_to_get_mcp_servers_running_on_claude_code/
[11] https://scottspence.com/posts/configuring-mcp-tools-in-claude-code
[12] https://www.youtube.com/watch?v=JzgZlSKA_3E
[13] https://www.youtube.com/watch?v=EOo8-j0jbAk
[14] https://www.reddit.com/r/ClaudeAI/comments/1jouzt4/open_source_mcp_alternative_to_claude_desktop/
[15] tools.code_analysis