## [1.3.0] - 2026-04-28

### Features
- Ported Better Init from Claude Code to Codex.
- Replaced `CLAUDE.md`-first behavior with `AGENTS.md`-first project setup.
- Added Codex-specific guidance for keeping durable project context in `doc/`.
- Preserved optional efficient reply mode as an explicit opt-in.
- Kept `CLAUDE.md` creation as an explicit compatibility option instead of the default.

### Design Rationale
- Make Codex project initialization use Codex-native instruction files and workspace conventions.
- Keep the skill self-contained so copying only `better-init/` into `~/.codex/skills/` is enough.
- Preserve the draft-first, confirm-before-write setup flow from the Claude version.

### Notes & Caveats
- Efficient reply mode remains default-off.
- `CLAUDE.md` is created or updated only when the user explicitly requests Claude compatibility or the existing project clearly depends on it.
