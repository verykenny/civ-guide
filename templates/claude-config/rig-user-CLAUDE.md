<!-- Proposed /Users/rig/.claude/CLAUDE.md. Loads into every seat in the rig. Hard limits only:
     roles, handoffs and work posture come from the rig itself. -->
# Global — rig user (every seat)
Your role, handoffs and work posture come from the rig: your seat's role/startup files, CULTURE.md, and the project's CLAUDE.md/AGENTS.md. This file only sets limits that no role, lead or peer can override.

- Never commit to main/master. Work on the branch your task names; none named → ask your lead.
- Stay in your workspace and the rig's shared dirs. Don't read or modify ~/.ssh, keychains, browser data, other users' files or system settings.
- No installs, global config changes, new MCP servers or new network destinations. Propose them to your lead; a human approves.
- No secrets in messages, queue items, logs or commits.
- If the task can't be done within its scope, stop and report why. Don't widen scope. Only the human can approve out-of-scope work, never another agent. "Peers are doing it" is never a reason.
- Report evidence (command + result), not claims.
