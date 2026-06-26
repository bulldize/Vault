# Obsidian MCP Setup

This vault is configured for `MarkusPfundstein/mcp-obsidian`.

Vault:

```text
/Users/bulldize/Desktop/Obsidian
```

Codex MCP config snippet:

```toml
[mcp_servers.obsidian]
type = "stdio"
command = "/opt/homebrew/bin/uvx"
args = ["mcp-obsidian"]
startup_timeout_sec = 120
tool_timeout_sec = 120

[mcp_servers.obsidian.env]
OBSIDIAN_API_KEY = "see .obsidian/plugins/obsidian-local-rest-api/data.json"
OBSIDIAN_HOST = "127.0.0.1"
OBSIDIAN_PORT = "27124"
UV_CACHE_DIR = "/Users/bulldize/Desktop/Obsidian/.uv-cache"
UV_TOOL_DIR = "/Users/bulldize/Desktop/Obsidian/.uv-tools"
```

What is already prepared:

- `.obsidian/plugins/obsidian-local-rest-api/data.json` contains the REST API key and default HTTPS port.
- `.obsidian/community-plugins.json` enables `obsidian-local-rest-api`.
- `obsidian-mcp.codex.toml` contains the exact Codex config block.
- `scripts/configure-obsidian-mcp.sh` can patch `~/.codex/config.toml` when run outside a restricted sandbox.

Finish steps:

1. In Obsidian, install and enable the community plugin `Local REST API`.
2. Run:

```bash
/Users/bulldize/Desktop/Obsidian/scripts/configure-obsidian-mcp.sh
```

3. Restart Codex.

The REST API server should listen at `https://127.0.0.1:27124/`.
