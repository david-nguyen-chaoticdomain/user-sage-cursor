# User Sage Cursor plugin

Cursor Marketplace package for the hosted User Sage MCP connector.

Create and run UX research from chat: surveys, tree tests, card sorts, preference tests, first-click tests, five-second tests, and prototype tests. Recruit with Your Panel, AI Panel, or GenPop through User Sage's hosted MCP.

- **MCP URL:** `https://mcp.usersage.com/mcp`
- **Auth:** Bearer API key (`usg_live_…`) from User Sage → Workspace Settings → Integrations → MCP Connector (Pro)
- **Transport:** remote Streamable HTTP (no local `npx` / CLI)

## Install (once listed)

Search **User Sage** in Cursor’s plugin marketplace, install, paste your API key.

## Local test before publish

1. Copy this folder to `~/.cursor/plugins/local/user-sage`
2. Reload Cursor Window
3. Configure `USERSAGE_API_KEY` under Plugins → Configure
4. Confirm tools: `list_studies`, `create_study`, etc.

Manual MCP (without the plugin):

```json
{
  "mcpServers": {
    "user-sage": {
      "url": "https://mcp.usersage.com/mcp",
      "headers": {
        "Authorization": "Bearer usg_live_…"
      }
    }
  }
}
```

## Publish checklist

1. Public packaging repo: [`david-nguyen-chaoticdomain/user-sage-cursor`](https://github.com/david-nguyen-chaoticdomain/user-sage-cursor) (this `cursor-plugin/` tree is the repo root). Do **not** use `user-sage-mcp` for the public GitHub name — that name is reserved for the private MCP / Vercel project (`user-sage-backend/apps/mcp`).
2. Confirm `https://mcp.usersage.com/mcp` is healthy (not maintenance).
3. Submit the repo at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).
4. Keep Grok Bot template work separate — connector first.

## Tools (server `user-sage` v1)

`list_studies`, `get_study`, `get_study_findings`, `get_study_responses`, `create_study`, `duplicate_study`, `get_recruitment_options`, `start_your_panel_recruitment`, `run_ai_panel`, `launch_genpop_recruitment`
