# civ-guide

A "seat" any model can sit in to guide you toward a local multi-agent setup
(OpenRig + herdr + Claude Code + Ollama), or to pick up where the last model left off.
Protocol: `AGENTS.md`. Memory: everything else.

## Set up
1. Put this folder at `~/projects/civ-guide`.
2. `git init` and commit per your branch conventions. Git is how you see exactly
   what each model changed; the Guide never commits.
3. Edit `intent/NORTH-STAR.md` and `plan/ROADMAP.md` (both DRAFT) and delete the
   DRAFT lines. That is step 0.1.

## Start a session (from this folder)
- **Claude Code:** `claude` → "Boot."
- **Codex / Pi / OpenCode:** they read AGENTS.md natively → "Boot."
- **Local model through Claude Code** (per-process only; never export these in ~/.zshrc):
  `ANTHROPIC_AUTH_TOKEN=ollama ANTHROPIC_BASE_URL=http://localhost:11434 claude --model <model>`
  Small models may not hold the protocol. The Guide is told to say so.
- **Chat UI** (claude.ai, LM Studio): paste mode. Copy the boot pack:
  `cat AGENTS.md intent/NORTH-STAR.md state/STATUS.md plan/ROADMAP.md state/OPEN-QUESTIONS.md "$(ls -t log/2*.md | head -1)" | pbcopy`

## End a session
Say "handoff" → review `git diff` → commit.

## You own
`intent/` and `plan/ROADMAP.md`. Decisions are Proposed until you mark them Accepted.
