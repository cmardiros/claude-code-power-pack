# MCP JSON Installer Prompt

**Prompt:**
```
Convert this MCP JSON configuration to claude mcp add-json commands:

[PASTE YOUR JSON HERE]
```

**Usage:**
1. Copy your MCP JSON configuration 
2. Paste the prompt above
3. Replace `[PASTE YOUR JSON HERE]` with your JSON
4. Claude will generate the correct `claude mcp add-json` commands for each server

**Example Input:**
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

**Example Output:**
```bash
claude mcp add-json macos-notification '{"command":"uvx","args":["git+ssh://git@github.com/githubuser/mcp-project-name.git"]}'
```