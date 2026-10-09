# llm_organization

A system for organizing coding projects around an LLM Wiki second brain: projects waste fewer tokens rediscovering themselves, and their lessons flow into a shared wiki that later projects reuse. `README.md` explains it for humans.

If `local/AGENTS.local.md` exists, read it: it holds this machine's personal configuration and working notes. `local/` is not versioned.

## Layout

- `project-template/`: the files copied into every new project. The core of the system.
- `wiki-schema/`: rules that extend an LLM Wiki schema so it can ingest projects.
- `scripts/`: automation for the mechanical steps.

## Rules for working on this repo

- **Contract on files.** The system is a set of file conventions written in plain text. Every rule must work for an agent with no skills installed: skills, scripts and trackers are optional layers on top.
- **Independence test.** Before changing `project-template/`, check that a fresh agent reading only the template's `AGENTS.md` could follow it.
- **Portable.** Rules live in `AGENTS.md`; each `CLAUDE.md` holds only `@AGENTS.md`.
- **English and placeholders.** Everything versioned is in English. Personal values (paths, names, language) are `{{PLACEHOLDERS}}` filled at install time. The user's own content follows the language setting.
- **Lean template.** Each line in the template's `AGENTS.md` costs tokens in every session of every project: keep it around one screen, and add a file to the template only when every project needs it from day one.
