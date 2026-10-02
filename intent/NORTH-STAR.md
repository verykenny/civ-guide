> DRAFT (proposed 2026-10-02). Kenny: edit, then delete this line. Only Kenny edits this file.

# NORTH STAR

## End state
A persistent, local team of AI agents on Kenny's Mac:
- seats with stable roles that survive restarts and model swaps
- Claude Code on Kenny's subscription for leads and implementers; local models (Ollama) for helper work
- visible at a glance (herdr-style view); messages, work queue and reviews between seats
- Kenny hands a lead one bounded outcome and gets back a reviewed result plus the decisions that need him

## Why
Today Kenny is the message bus between SA / TA / SD sessions, copy-pasting handoffs.
Goal: agents carry the handoffs; Kenny keeps the gates that matter.

## MVP (done = this)
Two seats (owner + checker) deliver one reviewed change on a branch, and the rig
restores after a reboot. (ROADMAP 2.4 + 2.5)

## Constraints
- Privacy-first: local by default; no new third-party service, MCP server or data
  leaving the machine without flagging it first.
- Budget: Claude subscription only. No paid cloud.
- Hardware: MacBook Pro M5 Pro, 24GB unified memory.
- Never commit to main. TDD for code.
- Approval before: installs, tooling/env/config changes, PRs, branch switches,
  force-push, anything sent as Kenny, anything irreversible.
- Every session ends with a clear next step. Kenny's time is the scarce resource.

## Non-goals (for now)
- Building orchestration plumbing from scratch.
- Cloud hosting, public or shared rigs, remote control from the phone.
- Unattended overnight runs before restore (2.5) is proven.
- More than ~4 concurrent seats.

## Not bound to the video
OpenRig + herdr are means, not the goal. If they don't fit, change decision 001
(fallback: herdr + file handoffs).

## Failure modes to guard against (from the video)
- **Scope inflation:** you ask for a doghouse and get a moonbase. Each step looks
  sensible on its own; the total is something nobody asked for.
- **Context-less approval:** an agent says yes to another agent without the context
  to judge. Only Kenny approves.
