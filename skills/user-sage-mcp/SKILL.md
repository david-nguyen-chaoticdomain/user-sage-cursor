---
name: user-sage-mcp
description: >-
  Use when the user wants to plan, create, inspect, or recruit for a User Sage
  UX research study from chat (survey, tree test, card sort, preference test,
  first-click test, five-second test, prototype test, AI Panel, Your Panel, or
  GenPop), or work with their Briefs, Projects, personas, or AI panels. Prefer
  the User Sage MCP tools over guessing study structure.
---

# User Sage MCP

## Setup

1. Any [app.usersage.com](https://app.usersage.com) workspace can connect, Free included.
2. Workspace Settings, Integrations, MCP Connector, Generate key (`usg_live_...`). Shown once; store it.
3. Install this plugin and paste the key into `USERSAGE_API_KEY`.

Remote endpoint: `https://mcp.usersage.com/mcp` (Bearer token). No local process. On a 401, check the key.

## What each plan can do

- **Free:** `plan_study` and `list_briefs`. Plan a study and list Briefs; each gives a link to open in User Sage, where the researcher creates the study from the Brief for free and does everything else.
- **Pro (and the 7-day Pro trial):** every other tool: create and duplicate studies, run an AI Panel, recruit, read studies and results, and work with Projects, personas and AI panels.

A call that needs Pro on a Free workspace is not an error. User Sage replies with `upgradeRequired`, a plain explanation, the matching page in the app (`dashboardUrl`) and the billing link (`upgradeUrl`). Relay it plainly: the feature needs Pro, here is the billing link, and here is the same thing in the app. Do not call a Pro tool just to find out, and never retry a refused call. If a Pro feature would help the researcher, suggest it and say plainly that it needs Pro.

## Tool map

Plan (every plan):
- `plan_study`: turns a research question into a Study Brief (recommended method, runner-up, drafted study, audience, suggested participants, a SIMULATED read) and returns `briefUrl`. 4 credits, charged only when a plan is produced; repeating the exact same call within a few minutes returns the same plan without charging. Never creates a study.
- `list_briefs`: the workspace's Briefs, newest first, each with a `briefUrl`. Never shows a Brief's contents: the link is the way in.

Read (Pro):
- `list_studies`: workspace study index
- `get_study`: full config and raw results (large; prefer findings or responses)
- `get_study_findings`: takeaway and aggregates
- `get_study_responses`: paged individual responses
- `get_recruitment_options`: which recruitment paths are available for a study

Write and run (Pro):
- `create_study`: persist a real study (survey, tree test, card sort, preference, first-click, five-second, or prototype test)
- `duplicate_study`: draft clone
- `start_your_panel_recruitment`: shareable Your Panel link
- `run_ai_panel`: spends credits; a panel of simulated people takes the study
- `launch_genpop_recruitment`: real paid participants; confirm with the researcher first

Projects, personas and AI panels (Pro):
- `list_projects`: Projects with a `projectUrl`; a Project id is `project_id` on `plan_study` and `list_briefs`
- `list_personas`, `get_persona`: the personas available, then one in full (goals, pain points, behaviors, five trait scores)
- `create_persona`: saves a persona you drafted; behavioral, never demographic; free
- `list_panels`, `get_panel`: AI panels, then one with its simulated people
- `create_panel`: generates simulated people from a persona (1 to 20) as a new panel; free

## Habits

- Plan first when the researcher has a question but no method: ask for the decision, who the participants are and what they already have; say `plan_study` costs 4 credits and confirm; call it once; show the method and why, the drafted study, the SIMULATED read and the `briefUrl`.
- The plan keeps the researcher's own words; everything else is a proposal listed in `assumptions`. Relay the assumptions and do not present a proposed decision, success target or audience as the researcher's.
- After a plan: on Free, give them `briefUrl` (Create study draft is free in the app) and do not offer to create from chat. On Pro, after they approve, pass the reply's `createStudyInput` to `create_study`.
- A survey made from a plan may have a placeholder for a screen people look at. If the user gave you the screen, pass it on the survey step as `imageUrl` (a public link) or `imageBase64` (never both): it fills the placeholder. Never invent an image or a link. If you do not have it, or the attach fails, the study is still created: `setupNotes` says "Upload the screen people will see" and `builderUrl` is where to add it. Say so, and do not call the study complete.
- Call `get_recruitment_options` before proposing how to recruit.
- Prefer `get_study_findings` over `get_study` for "what did we learn?"
- Keep AI Panel results (simulated people, a hypothesis) and real-participant results separate, and say which is which.
- For spendy actions (`run_ai_panel`, `launch_genpop_recruitment`), confirm the researcher wants to spend credits or funds before calling.
- Confirm before `create_persona` or `create_panel`. Existing studies, personas and panels cannot be edited or deleted through this connector; send the researcher to the app.
- After `create_study`, give them the builder, preview and results URLs from the tool result.
- If a tool named here is missing, the client cached an older tool list: reconnect the User Sage MCP server or start a new chat.
