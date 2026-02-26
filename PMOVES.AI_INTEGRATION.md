# PMOVES.AI Integration Guide for E2B MCP Server

## Integration Overview

E2B MCP Server provides sandboxed code execution capabilities via the Model Context Protocol. It allows Claude Desktop, Claude Code, and PMOVES.AI agents to execute Python and JavaScript code in isolated E2B sandbox environments with full library and system access.

## Service Details

- **Name:** E2B MCP Server
- **Slug:** e2b-mcp-server
- **Tier:** worker
- **Port:** None (stdio MCP transport)
- **Health Check:** N/A (process-level, not HTTP)
- **NATS Enabled:** False
- **GPU Enabled:** False

## Integration Points

### MCP Tool Bridge
- Transport: stdio (subprocess invocation)
- Provides code interpreter capabilities to MCP-compatible clients
- Available in JavaScript and Python editions

### Agent Integration
```
Claude Code / Agent Zero → MCP stdio → E2B Sandbox
                                      → Isolated Code Execution
                                      → Result Return
```

### BoTZ Integration
- Also available via BoTZ E2B feature module at `features/e2b/`
- SSE transport at `http://localhost:7071/sse` (when running via BoTZ)

## Next Steps

### 1. Customize Environment Variables

- `E2B_API_KEY` - Required API key for E2B sandbox access

### 2. Configure MCP Client

For Claude Desktop integration:
```json
{
  "mcpServers": {
    "e2b": {
      "command": "npx",
      "args": ["-y", "@anthropic/e2b-mcp-server"]
    }
  }
}
```

### 3. Test Integration

```bash
# Verify MCP server starts
npx -y @anthropic/e2b-mcp-server --help

# Verify E2B API key
echo $E2B_API_KEY
```

## Files Created

- `PMOVES.AI_INTEGRATION.md` - This integration guide

## Support

For questions or issues, see the PMOVES.AI documentation.
