# Research — findings as of 2026-10-02 (Claude Opus 5.5)
Last verified: 2026-10-02. A starting point, not truth; re-verify in 0.7 and before relying on any line.

## The video
- https://www.youtube.com/watch?v=AL-PQuB2wy0 is OpenRig's "agent civilizations" video. It was not watched
  directly (YouTube blocked fetch). Identified via OpenRig PR #54 (the README demo loop is footage from it)
  and tntpgh/herdr-control PR #140 (layout: a herdr tab split into the OpenRig TUI + agent panes).
- Companion post: https://openrig.dev/blog/agent-civilizations. Thesis: the 2026 OpenAI eval breakout
  reads better as a coordination failure in an agent "civilization" than as rogue agents. Two failure
  modes: scope inflation (doghouse → moonbase via locally sensible steps) and approvals from agents that
  lack the context. Fixes: give the deciding agent the context it needs; keep intent in view (OpenRig "Refocus").

## OpenRig
Repo: https://github.com/mvschwarz/openrig. Docs index for agents: https://openrig.dev/llms.txt
- Local daemon + CLI + TUI + MCP, on tmux. Teams defined in YAML (RigSpec). A seat is a stable
  role/address whose occupant can change. Runtimes: Claude Code, Codex, a Pi adapter, terminal nodes.
- Requires Node 22 or 24 + tmux, macOS or Linux. README: Apple-silicon Macs should use Node 22.
- Starters: first-project (Codex), first-project-claude (2 Claude seats, owner + checker),
  first-project-mixed; also conveyor, product-team, implementation-pair, adversarial-review, research-team.
- Snapshot/restore: `rig down --snapshot`; `rig up <name>`.
- Machine writes (read the README section "What OpenRig changes on your machine" before setup):
  - ~/.claude.json (trust/onboarding)
  - workspace .claude/settings.local.json (statusLine + hooks; can replace an existing statusLine) and .mcp.json
  - a block in ~/.tmux.conf
  - seeds openrig-skills into ~/.claude/skills and ~/.agents/skills
  - ~/.codex/config.toml (hooks + trust)
  - optional cmux install
- Shared settings resource: sets acceptEdits and adds Exa/Context7 MCP entries (third parties).
- The daemon checks a GitHub endpoint for plugin releases.
- Seats launch Claude with acceptEdits. YOLO is off by default.
- `rig setup --dry-run` previews; `rig doctor` diagnoses; agents can read help via `rig context get help`.
- Expectations: the author (Show HN thread) says he can't supervise more than ~4–5 agents and gets ~80% of the work done autonomously.

## herdr
Repo: https://github.com/ogulcancelik/herdr
- Terminal agent multiplexer: workspaces/tabs/panes, per-agent state (blocked/working/done/idle),
  detach/reattach, SSH, socket API. Agents can drive it (`herdr wait agent-status …`).
- Install: Homebrew (`brew install herdr`) or the install script. License: AGPL-3.0.
- `herdr integration install claude|codex|pi|…` modifies agent config; treat it as a config change.
- OpenRig opens a rig's seats in herdr: `rig terminal open <rig> --provider herdr`.

## Local models
- Ollama ≥ 0.14 speaks the Anthropic Messages API, so Claude Code can use local models:
  `ANTHROPIC_AUTH_TOKEN=ollama ANTHROPIC_BASE_URL=http://localhost:11434 claude --model <m>`
  (https://docs.ollama.com/api/anthropic-compatibility). Scope this per process only.
  `ollama launch claude` "configures Claude Code automatically"; whether that persists is UNVERIFIED.
- Pi coding agent: the package moved to @earendil-works/pi-coding-agent (May 2026). Point it at Ollama via ~/.pi/agent/models.json.
- 24GB sizing: a 14B dense model at Q8 or a 30B-A3B MoE at Q4 fits alone (~16–19GB for the larger ones).
  Next to Claude Code sessions + the daemon, expect memory pressure. Local seats are helpers
  (triage, summaries, second opinions), not leads.

## Claude plans
Sources: https://support.claude.com/en/articles/11145838 and /11014257
- Pro/Max usage is shared across claude.ai and Claude Code. Session limits reset every 5 hours.
- Max: $100/mo (5x Pro) or $200/mo (20x Pro).
- If ANTHROPIC_API_KEY is set, Claude Code bills API rates instead of the subscription.

## Claude Code config
Source: https://code.claude.com/docs/en/memory
- Claude Code reads CLAUDE.md, not AGENTS.md. The documented pattern is a CLAUDE.md that imports @AGENTS.md.
- It walks up the directory tree loading CLAUDE.md/CLAUDE.local.md. ~/.claude/CLAUDE.md loads in every
  project; files are concatenated, not filtered.
- `/context` shows which memory files loaded. Block-level HTML comments are stripped before injection.
- Subagents: a project-level definition beats a user-level one with the same name.

## Also looked at
- AiCIV / AgentMind (github.com/coreycottrell/agentmind): model-routing tiers for large fleets; relies on cloud inference providers → parked.
- Claude Managed Agents: cloud, Claude-only, billed per session-hour → conflicts with local/privacy goals.
- OpenRig comparison pages (subagents, agent teams, CrewAI, n8n, …): https://openrig.dev/compare
