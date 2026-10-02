# 001 — Base stack: OpenRig (team layer) + herdr (view), running Claude Code
Status: Proposed (2026-10-02, Claude Opus 5.5). Kenny to accept or reject.

## Context
head-orchestrator-claude stalled (details come from the 0.5 post-mortem). Kenny's working pattern
today: he is the message bus between SA / TA / SD sessions. The video's setup is OpenRig seats
shown in herdr.

## Options
A. OpenRig + herdr: persistent seats, messaging, a work queue, snapshot/restore; runs Claude Code,
   Codex and Pi. Cost: invasive config writes, Node 22, 0.x churn, seats run in acceptEdits.
B. herdr only + file handoffs: light; agent-state view plus `herdr wait`. No topology, queue or restore.
C. Keep building head-orchestrator-claude: full control, but re-solves plumbing others have solved.
D. Claude Code subagents / agent teams only: zero setup, but session-scoped, single harness, not persistent.
E. Claude Managed Agents: cloud, Claude-only, billed per session-hour. Conflicts with local/privacy goals.

## Decision
A, with B as the fallback.

## Why
Kenny's value-add is roles, gates and culture, not tmux plumbing. An OpenRig seat is a stable role
and address with a replaceable occupant, the same concept as this Guide seat.

## Consequences
Its config writes have to be contained (see 002). Re-verify requirements on each release.

## Revisit if
The `rig setup` dry-run shows writes Kenny won't accept; restore (2.5) is unreliable; releases
break things repeatedly; or the subscription can't sustain 2 seats.
