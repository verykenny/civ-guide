# 002 — Isolation: run the civilization as a dedicated macOS user `rig`
Status: Proposed (2026-10-02, Claude Opus 5.5). Kenny to accept or reject.

## Context
OpenRig writes to ~/.claude.json, workspace .claude/settings.local.json, ~/.tmux.conf,
~/.claude/skills and ~/.codex/config.toml. It wants Node 22 (Kenny runs 24) and runs seats in
acceptEdits. Kenny's global CLAUDE.md would load into every seat.

## Options
A. Dedicated standard (non-admin) macOS user `rig`: its own ~/.claude, nvm/Node 22 and tmux.conf.
   Ollama on localhost is shared. Homebrew binaries are usable, but Kenny's user does brew installs.
   Cost: ~30 min; work from `su - rig`; a separate Claude Code login (same subscription).
B. Main user, with backups + a slimmed global CLAUDE.md: less friction, but every OpenRig write lands
   in Kenny's daily config.
C. VM/container: strongest isolation; a macOS VM on 24GB is a non-starter for the MVP.

## Decision
A.

## Why
A clean slate for seats; Kenny's daily setup is untouched; it caps the blast radius of acceptEdits
seats; and it removes the global-CLAUDE.md conflict for the rig entirely.

## Consequences
The Guide, running as Kenny, can't run rig-user commands; Kenny runs them via `su - rig`. The
main-user global split (1.2) becomes nice-to-have rather than blocking.

## Revisit if
The friction kills momentum, or OpenRig needs something only the main user can provide.
