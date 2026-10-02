<!-- Opt-in pipeline rules, moved out of the global CLAUDE.md.
     Install at ~/templates/agent-pipeline/pipeline.md, alongside agents/ (the files moved from ~/.claude/agents/).
     A project opts in by:
       1. adding this line to its CLAUDE.md:  @~/templates/agent-pipeline/pipeline.md
          (Claude Code asks once to approve external imports)
       2. copying the role agents into its .claude/agents/ (version-controlled with the project). -->
## Workflow — 3-agent pipeline
System Architect → Technical Architect → Senior Developer, human-gated handoffs; hold role boundaries.
Approve before crossing an agent role boundary. Approve plan before action. TA hands SD work in commit-sized chunks.

## Handoffs & hand-backs
Every role transition is a written prompt authored by the sending agent (SA→TA, TA→SD); every return is a structured hand-back (SD→TA, TA→SA). No implicit/verbal handoffs. Forward and back both pass the human gate.

Handoff prompt (forward). The asking agent MUST include:
- Objective: the single task the next agent owns.
- Context & source-of-truth: refs to the plan doc, relevant files, prior decisions.
- Constraints & scope: in/out of scope, role-boundary reminder, branch to use.
- Definition of done: acceptance criteria the next agent is held to.
- Hand-back spec: exactly what to report back and in what shape. MANDATORY; a handoff without it doesn't run. Tailored by the asking agent; the list below is the floor.

Hand-back (return). The receiving agent reports:
- Done vs. DoD, criterion by criterion.
- Artifacts: branch, files touched, commit refs, test status.
- Decisions & assumptions (and why).
- Deviations from the brief + rationale.
- Open questions / blockers.
- Verify-this: what the asking agent should confirm before proceeding.

Loop-closing:
- The asking agent rejects a hand-back missing any required field.
- The asking agent confirms the task is satisfied (or re-prompts); it doesn't silently move on.
- The human approves the handoff prompt before it runs and the hand-back before the chain continues.
