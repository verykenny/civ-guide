# Session 2026-10-02 — Claude Opus 5.5 (claude.ai chat, no access to the Mac)

## Done vs. exit checks
- Seat scaffold created (this folder). No machine checks were run; this session could not reach the Mac.
- Research: the video (youtu.be/AL-PQuB2wy0) is OpenRig's "agent civilizations" talk. YouTube blocked
  fetching, so findings come from the companion blog post, the OpenRig README/docs, and PRs that
  reference the footage. Details: research/sources.md.

## Artifacts / changes
- Seat files: all (initial).
- Machine changes: none.

## Decisions & assumptions (and why)
- Proposed 001: adopt OpenRig + herdr instead of rebuilding orchestration plumbing.
- Proposed 002: run the civilization as a dedicated macOS user `rig`.
- Assumed ~/.claude/CLAUDE.md matches Kenny's June 2026 "Agent Settings — Kenny" doc (possibly plus a
  "Handoffs & hand-backs" block). The replacements in templates/claude-config/ are based on that and
  are UNVERIFIED against the real file (step 0.4).
- Plan tier: Pro is OK for Phases 0–1 and a short supervised Phase 2; Max 5x is the realistic floor
  for regular rig use.

## Deviations from ROADMAP
- None (the ROADMAP was created this session).

## Open questions / blockers
- OQ-1 … OQ-6 seeded.

## Verify-this (next Guide: re-check before building on it)
- [ ] OpenRig's Node requirement on Apple silicon (was: use Node 22). Check the README before 1.4.
- [ ] herdr install method (was: `brew install herdr`).
- [ ] Ollama ≥ 0.14 (Anthropic-API compatibility).
- [ ] Pi package name (was: @earendil-works/pi-coding-agent since May 2026) and OpenRig Pi adapter requirements.
- [ ] Whether `ollama launch claude` persists Claude Code config. The README uses explicit per-process env vars instead.
- [ ] Real contents of ~/.claude/CLAUDE.md and ~/.claude/agents/ vs. the assumption above.

## Next step proposed
0.1 — Kenny reviews NORTH-STAR + ROADMAP — exit check: `grep -rn DRAFT intent plan/ROADMAP.md` → no output.
