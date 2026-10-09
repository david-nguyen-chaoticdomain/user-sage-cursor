# User Sage Cursor plugin

Cursor Marketplace package for the hosted User Sage MCP connector.

Plan, create and run UX research from chat: surveys, tree tests, card sorts, preference tests, first-click tests, five-second tests, and prototype tests. Recruit with Your Panel, AI Panel, or GenPop through User Sage's hosted MCP.

- **MCP URL:** `https://mcp.usersage.com/mcp`
- **Auth:** Bearer API key (`usg_live_…`) from User Sage → Workspace Settings → Integrations → MCP Connector (any plan)
- **Transport:** remote Streamable HTTP (no local `npx` / CLI)

## What each plan can do

Any plan can connect. **Free:** `plan_study` and `list_briefs`: plan a study and list your Briefs; each gives a link to open in User Sage, where you create the study from the Brief for free. **Pro (and the 7-day Pro trial):** everything else from chat: create, duplicate and run studies, recruit, read studies and results, and work with Projects, personas and AI panels. Ask for something that needs Pro on a Free workspace and User Sage replies with a plain explanation and a billing link, never an error.

## Install (once listed)

Search **User Sage** in Cursor’s plugin marketplace, install, paste your API key.

## Local test before publish

1. Copy this folder to `~/.cursor/plugins/local/user-sage`
2. Reload Cursor Window
3. Configure `USERSAGE_API_KEY` under Plugins → Configure
4. Confirm tools: `plan_study`, `list_briefs`, and on Pro `list_studies`, `create_study`, etc. If a tool is missing after an update, your client cached an older tool list: reconnect the MCP server or start a new chat.

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

1. Public packaging repo: [`user-sage/user-sage-cursor`](https://github.com/user-sage/user-sage-cursor) (this `cursor-plugin/` tree is the repo root). Do **not** use `user-sage-mcp` for the public GitHub name: that name is reserved for the private MCP / Vercel project (`user-sage-backend/apps/mcp`).
2. Confirm `https://mcp.usersage.com/mcp` is healthy (not maintenance).
3. Submit the repo at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).
4. Keep Grok Bot template work separate: connector first.

## Releasing an update

1. Merge the change to `main` here and bump `version` in `.cursor-plugin/plugin.json`.
2. **The cursor.directory listing does not sync from this repo.** It keeps its own copy of the description, keywords and both components. Open the listing's Edit Plugin form and update it by hand: the Description, the Keywords, and the skill component's Description and Content (copy `skills/user-sage-mcp/SKILL.md` from the line `# User Sage MCP` down, without the `---` header block at the top). The MCP component only changes if `mcp.json` does. Then press Update Plugin.
3. If the plugin is also listed in the official Cursor Marketplace, re-submit it or bump its version at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).

## Tools (server `user-sage`, 20)

Free and Pro: `plan_study`, `list_briefs`

Pro: `list_studies`, `get_study`, `get_study_findings`, `get_study_responses`, `create_study`, `duplicate_study`, `get_recruitment_options`, `start_your_panel_recruitment`, `run_ai_panel`, `launch_genpop_recruitment`, `list_projects`, `get_project`, `list_personas`, `get_persona`, `create_persona`, `list_panels`, `get_panel`, `create_panel`
