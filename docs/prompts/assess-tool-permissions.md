# Tool Permission Assessment Prompt

Generate a comprehensive assessment of all available Claude Code tools, categorizing them by safety level for persistent access and providing permission specifications.

## Instructions

1. **List all available tools** including:
   - All core Claude Code tools
   - Only the built-in `mcp__ide__getDiagnostics` MCP tool (exclude other MCP servers)
   - The `Update` tool (always include this as a built-in tool even if not in standard lists)

2. **Categorize each tool** into one of three categories:
   - **Read-Only Tools (Safe for Persistent Access)**: Tools that only read/fetch data without modifying anything
   - **Tools with Write Access (Require Caution)**: Tools that can modify files, execute code, or change system state
   - **Mixed Capabilities**: Tools that have both read and write capabilities or special considerations

3. **Special Considerations**:
   - Mark `Task` tool as **NOT safe for persistent use** due to its agentic/sub-agentic nature (can spawn agents that use other tools)
   - Always include `Update` tool in the write access category
   - Consider `Bash` as particularly dangerous due to system command execution capabilities

4. **Generate Permission Specifications**: For tools marked as "Safe for Persistent Access", provide example permission allow list entries using this format:
   ```json
   {
     "permissions": {
       "allow": [
         "toolname",
         "toolname(pattern:*)"
       ],
       "deny": []
     }
   }
   ```

## Output Format

Structure your response as follows:

### Tool Safety Assessment

#### Read-Only Tools (Safe for Persistent Access)
- **Tool Name** - Description of what it does and why it's safe

#### Tools with Write Access (Require Caution)  
- **Tool Name** - ⚠️ **CAPABILITY** Description of write/modification capabilities

#### Mixed Capabilities
- **Tool Name** - Description of mixed read/write capabilities and considerations

### Recommended Persistent Access Configuration

```json
{
  "permissions": {
    "allow": [
      // List only the truly safe read-only tools here
    ],
    "deny": []
  }
}
```

### Security Notes
- Highlight any tools that require special attention
- Note any tools that could be used to bypass other restrictions
- Provide guidance on tool combinations that might create security risks

---

**Usage**: Save this prompt and use it whenever you need to assess tool permissions for Claude Code configurations. Results should be written to `docs/prompt-results/assess-tool-permissions-results.md`.