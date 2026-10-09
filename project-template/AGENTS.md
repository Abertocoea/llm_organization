# {{PROJECT_NAME}}

{{ONE_LINE_PURPOSE}}

Language: write docs in {{DOCS_LANGUAGE}}; talk to the user in {{USER_LANGUAGE}}.

## Start here

- Commands: <!-- install, run, test: one line each -->
- Map: <!-- top-level folders: one line each -->
- Conventions: <!-- only the ones the code doesn't show -->
- `docs/index.md` lists the project docs: read the pages the task touches.
- Recent history: the last 3 entries of `docs/log.md`.

## Second brain

Lessons from past projects live in the second brain at `{{SECOND_BRAIN_PATH}}`. Before choosing an approach (a library, a pattern, a data format), read its `wiki/index.md`, then only the pages it points to. From a project, the second brain is read-only.

## Docs

`docs/` holds what the code can't tell: reasons, decisions, traps, context. Each fact has one home: open tasks in the issue tracker (or in the log, when there is none), decisions in ADRs, history in the log.

Update docs at exactly three moments:

1. **Decision** that meets the ADR criteria below: write an ADR right away.
2. **End of feature**: answer the five questions and touch only the files where the answer is yes.
   1. Did the shape of the system change? → `docs/architecture.md` (create it once two or more parts talk to each other)
   2. Did you find traps or reasons the code doesn't show? → `docs/modules/<name>.md`, or `docs/architecture.md` when they span modules
   3. Is there a new file in `docs/`? → `docs/index.md`
   4. Did the commands, the folder map or the every-session rules change? → this file
   5. Is there a new lesson useful to other projects (not already in the second brain)? → suggest ingesting this project into the second brain; the user decides.
3. **End of session**: append one entry to `docs/log.md`. A session that closes a feature does moment 2, then moment 3.

Grow on demand: `GLOSSARY.md` at the first clarified domain term; a local `AGENTS.md` plus `CLAUDE.md` (`@AGENTS.md`) inside a large module's folder.

## ADRs

`docs/adr/NNNN-slug.md` (create the folder with the first ADR), numbered after the highest existing one. Write an ADR only when the decision is all three: hard to reverse, surprising without context, the result of a real trade-off.

Format: a title and 1-3 sentences (context, decision, why). Add Status, Considered options or Consequences only when they add value. When a decision changes, a new ADR supersedes the old one, and the old one stays.

## Log

Append-only. Each entry starts with `## [YYYY-MM-DD] session | <title>`, followed by bullets for what was done and what is open, linking issues, ADRs and commits (when they exist) instead of repeating them.
