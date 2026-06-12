# AgentTemp MCP

MCP (Model Context Protocol) server configuration for AgentTemp - Email verification infrastructure for AI agents.

## What is MCP?

Model Context Protocol (MCP) allows AI agents (Claude, Cursor, Windsurf, etc.) to directly interact with AgentTemp's API through structured tools.

## Quick Setup

### 1. Get API Key

Create an API key from the AgentTemp Dashboard (set `AGENTTEMP_API_KEY` or pass `--api-key`).

### 2. Add to Your MCP Client

**Claude Desktop:**
```json
{
  "mcpServers": {
    "agenttemp": {
      "url": "https://tempmailai.vercel.app/api/mcp",
      "headers": {
        "Authorization": "Bearer at_live_..."
      }
    }
  }
}
```

**Cursor:**
Add to `~/.cursor/mcp.json`:
```json
{
  "mcpServers": {
    "agenttemp": {
      "url": "https://tempmailai.vercel.app/api/mcp",
      "headers": {
        "Authorization": "Bearer at_live_..."
      }
    }
  }
}
```

**Windsurf:**
Add to your Cascade configuration.

### 3. Available Tools

| Tool | Description |
|------|-------------|
| `create_inbox` | Create a temporary email inbox |
| `list_inboxes` | List all your inboxes |
| `get_inbox` | Get inbox details |
| `delete_inbox` | Delete an inbox |
| `list_messages` | List messages in an inbox |
| `get_message` | Get a specific message |
| `list_extractions` | List OTP/link extractions |
| `wait_for_email` | Wait for any email |
| `wait_for_otp` | Wait for OTP extraction |
| `wait_for_magic_link` | Wait for magic link |
| `wait_for_password_reset` | Wait for password reset link |
| `check_wait` | Check wait status (non-blocking) |

## Example Usage

```typescript
// Agent will use these tools automatically
// Just ask: "Create a temp email and wait for the OTP"

// Behind the scenes:
const inbox = await create_inbox({ ttlSeconds: 3600 });
const wait = await wait_for_otp({ inboxId: inbox.id, timeoutSeconds: 120 });
console.log(wait.result?.value); // "123456"
```

## Resources

- **Node.js SDK**: https://github.com/kunalgawade19042002-gif/agenttemp-node
- **Python SDK**: https://github.com/kunalgawade19042002-gif/agenttemp-python
- **CLI Tool**: https://github.com/kunalgawade19042002-gif/agenttemp-cli
- **API Docs**: https://tempmailai.vercel.app/api/v1/openapi.json

## License

MIT
