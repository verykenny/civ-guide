> DRAFT (proposed 2026-10-02). Kenny: edit, then delete this line. Changes need Kenny's approval of the exact diff.

# ROADMAP

Each step: **do** → **exit check** (a command or observation that proves it).
STATUS refers to steps by number. Commands are starting points; the Guide checks
current docs before giving them.

## Phase 0 — Ground truth (read-only; nothing installed or changed)
0.1 Kenny reviews/edits NORTH-STAR and ROADMAP; deletes the DRAFT lines.
    Exit: `grep -rn DRAFT intent plan/ROADMAP.md` → no output.
0.2 Machine inventory: `sw_vers`, `sysctl -n hw.memsize`, `df -h ~`, `which -a node`,
    `node -v`, `nvm ls`, `brew --version`, `tmux -V`, `ollama --version`, `ollama list`,
    `claude --version`.
    Exit: every row in inventory/machine.md has a value + date.
0.3 Env sweep: are ANTHROPIC_API_KEY / ANTHROPIC_BASE_URL / ANTHROPIC_AUTH_TOKEN set in
    the env, ~/.zshrc, ~/.zprofile or ~/.claude/settings.json? Report set/unset only, never values.
    Exit: recorded in inventory/machine.md.
0.4 Claude config audit (main user): ~/.claude/CLAUDE.md, agents/, skills/, commands/,
    settings.json (hooks, permissions, env), MCP servers in ~/.claude.json. In one real
    project, run `/context` and note which memory files load.
    Exit: inventory/claude-config.md (paths + one-line summaries, no secrets).
0.5 Post-mortem of ~/projects/head-orchestrator-claude: what it tried, where it broke,
    what to salvage (role prompts, hand-back spec, kickoff templates). (OQ-5)
    Exit: decisions/003-head-orchestrator-salvage.md.
0.6 Kenny accepts or rejects decisions 001 (stack) and 002 (isolation); answers OQ-1 (plan tier).
    Exit: both decisions show Accepted/Rejected; OQ-1 closed.
0.7 Re-verify research/sources.md against upstream (OpenRig requirements, herdr install,
    Ollama version, Pi package).
    Exit: "Last verified" date updated; changes logged.

## Phase 1 — Clean base (every step approval-gated; add the changes.md row BEFORE each change)
1.1 Back up ~/.claude, ~/.claude.json, ~/.tmux.conf, ~/.codex (if present) to ~/backups/pre-rig-<date>/.
    Exit: `ls` of the backup dir; paths in changes.md.
1.2 Split the main-user global CLAUDE.md: move the pipeline rules and ~/.claude/agents/* to
    ~/templates/agent-pipeline/ (drafts in templates/claude-config/); install the slim global
    after Kenny edits it; opt pipeline projects (e.g. ink-capture) back in via import +
    project .claude/agents/.
    Exit: `/context` in a scratch dir shows only the slim global; in ink-capture the pipeline
    rules + agents load.
1.3 (if 002 accepted) Kenny creates a standard (non-admin) macOS user `rig` in System Settings.
    Exit: `id rig`; `su - rig -c whoami` → rig.
1.4 As rig: nvm + the Node version OpenRig requires on Apple silicon (was 22); Claude Code;
    log in with the subscription. Confirm no ANTHROPIC_API_KEY in rig's env.
    Exit: `node -v`, `claude --version`, login shows the subscription account.
1.5 As rig: install templates/claude-config/rig-user-CLAUDE.md as /Users/rig/.claude/CLAUDE.md.
    Exit: `/context` in a rig-owned dir shows it.
1.6 As Kenny: `brew install tmux herdr` (check current herdr install docs). As rig: verify both
    run. Hold off on `herdr integration install …` (it changes agent config); decide in Phase 2.
    Exit: `tmux -V` and `herdr --version` as rig.
1.7 As rig: `npm install -g @openrig/cli`; `rig setup --dry-run`. Guide + Kenny review every
    planned write; decide Exa/Context7 (OQ-3) and cmux (OQ-6).
    Exit: every planned write listed in changes.md with undo.
1.8 As rig: apply `rig setup` (core, not --full) only if 1.7 was clean; run `rig doctor`.
    Exit: `rig doctor` healthy, or each warning explained in the log.

## Phase 2 — MVP civilization  ← the goal
2.1 Sandbox repo owned by rig (OQ-4): tiny project, one passing test, on a feature branch.
    Exit: `git branch --show-current` ≠ main; tests pass.
2.2 `rig specs preview first-project-claude --kind rig` → `rig up first-project-claude --cwd . --plan`
    → review → `rig up first-project-claude --cwd .`
    Exit: `rig ps --nodes --rig first-project-claude` → both seats ready.
2.3 View: `rig tui --shared`; `rig terminal open first-project-claude --provider herdr`.
    Exit: Kenny sees both seats in herdr.
2.4 One bounded task to the owner seat via `rig send` (seat names per `rig ps`). The owner
    records it in the queue; the checker reviews the exact candidate.
    Exit: reviewed change on a branch; Kenny has tried it.
2.5 Recovery: `rig down --snapshot` → reboot → `rig up first-project-claude`; check per-seat restore.
    Exit: runbooks/recover-after-reboot.md written from what actually worked.
2.6 Usage check: how much of the 5-hour window did 2.4 consume?
    Exit: note in inventory/machine.md; plan-tier decision if needed.
MVP done = 2.4 + 2.5.

## Phase 3 — Local seat
3.1 Pick one tool-capable local model that leaves headroom next to 2 Claude seats
    (target ≤ ~16GB resident). Record why.
    Exit: decision file; memory pressure green with the model loaded + 2 seats up.
3.2 As rig: install Pi (current package name); point ~/.pi/agent/models.json at Ollama.
    Exit: Pi completes a trivial tool-using task standalone.
3.3 Add a Pi seat via OpenRig's Pi adapter in a low-stakes role (summaries / triage /
    second-opinion review).
    Exit: the seat completes one queued task.
3.4 Measure tok/s, memory pressure, quality vs Claude.
    Exit: decision: keep / smaller model / drop.

## Phase 4 — Kenny's pipeline as a rig
4.1 Map SA → TA → SD + the hand-back spec onto AgentSpecs / RigSpec / CULTURE.md; keep the
    human gates at role transitions.
    Exit: `rig specs preview` of the new spec reviewed by Kenny.
4.2 One small real feature (e.g. ink-capture) end to end.
    Exit: feature on a branch with the full hand-back chain; Kenny opens the PR himself.
4.3 Retro.
    Exit: decisions + a proposed ROADMAP diff for what's next.

## Phase 5 — (optional) The Guide becomes a seat
Promote this protocol to an OpenRig seat (e.g. guide@ops) that reads rig state directly.
Only after Phase 4.
