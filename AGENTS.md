# llm_organization

A system for organizing coding projects around an LLM Wiki second brain: projects waste fewer tokens rediscovering themselves, and their lessons flow into a shared wiki that later projects reuse. `README.md` explains it for humans.

If `local/AGENTS.local.md` exists, read it: it holds this machine's personal configuration and working notes. `local/` is not versioned.

Language: write docs in English; talk to the user in the language `local/AGENTS.local.md` sets (English if absent).

## Start here

- `docs/index.md` lists the docs; `docs/adr/` explains why the system is designed this way.
- Recent history: the last 3 entries of `docs/log.md` (local only, git-ignored).
- This repo follows its own template: apply the *Docs*, *ADRs* and *Log* sections of `project-template/AGENTS.md` here too.

## Layout

- `project-template/`: the files copied into every new project. The core of the system.
- `wiki-schema/`: rules that extend an LLM Wiki schema so it can ingest projects.
- `scripts/`: automation for the mechanical steps.

## Rules for working on this repo

- **Contract on files.** The system is a set of file conventions written in plain text. Every rule must work for an agent with no skills installed: skills, scripts and trackers are optional layers on top.
- **Independence test.** Before changing `project-template/`, check that a fresh agent reading only the template's `AGENTS.md` could follow it.
- **Portable.** Rules live in `AGENTS.md`; each `CLAUDE.md` holds only `@AGENTS.md`.
- **English and placeholders.** Everything versioned is in English. Personal values (paths, names, languages) are `{{PLACEHOLDERS}}` filled at install time; in a public repo they go in a git-ignored local file that `AGENTS.md` points to. The user's own content follows the language settings.
- **Lean template.** Each line in the template's `AGENTS.md` costs tokens in every session of every project: keep it around one screen, and add a file to the template only when every project needs it from day one.
