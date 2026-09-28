---
name: user-sage-mcp
description: >-
  Use when the user wants to create, inspect, or recruit for a User Sage UX
  research study from chat (survey, tree test, card sort, preference test,
  first-click test, five-second test, prototype test, AI Panel, Your Panel, or
  GenPop). Prefer the User Sage MCP tools over guessing study structure.
---

# User Sage MCP

## Setup

1. User needs a Pro workspace on [app.usersage.com](https://app.usersage.com).
2. Settings → MCP connector → Generate key (`usg_live_…`). Shown once; store it.
3. Install this plugin and paste the key into `USERSAGE_API_KEY`.

Remote endpoint: `https://mcp.usersage.com/mcp` (Bearer token). No local process.

## Tool map

Read:
- `list_studies` — workspace study index
- `get_study` — full config + raw results (large; prefer findings/responses when possible)
- `get_study_findings` — takeaway + aggregates
- `get_study_responses` — paged individual responses
- `get_recruitment_options` — which recruitment paths are available for a study

Write / run:
- `create_study` — persist a real study (survey, tree test, card sort, preference, first-click, five-second, or prototype test)
- `duplicate_study` — draft clone
- `start_your_panel_recruitment` — shareable Your Panel link
- `run_ai_panel` — spend credits; synthetic panel
- `launch_genpop_recruitment` — real paid participants; confirm with the researcher first

## Habits

- Call `get_recruitment_options` before proposing how to recruit.
- Prefer `get_study_findings` over `get_study` for “what did we learn?”
- For spendy actions (`run_ai_panel`, `launch_genpop_recruitment`), confirm the researcher wants to spend credits/funds before calling.
- After `create_study`, give them the builder / preview / results URLs from the tool result.
