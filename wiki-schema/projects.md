# Projects in the wiki

This extension lets an LLM Wiki ingest **projects** as sources, next to articles and books. It adds one page type and one flow; the base operations (ingest, query, lint, index, log) keep working as the vault's schema defines them, and its general rules (frontmatter, citations, contradictions, completion checks) apply to project pages too.

The vault's schema links here with one line, e.g. *"For projects, follow `{{WIKI_SCHEMA_PATH}}/projects.md`."* The extension adds an entry to three of the schema's lists: a `project` page type, a `project` log type, and a Projects section in the index, placed after the sources section.

**Language and names.** Write pages in the vault's language and use its date format. Translate every English name below into the vault's language the same way the vault names its own things: folders in `raw/` and `wiki/`, the page type, frontmatter keys and values, section headings, the log type (e.g. a vault with `fonti/` and `concetti/` gets `raw/progetti/`, `wiki/progetti/`, type `progetto`, `stato: attivo`).

## What a project contributes

A project's `docs/` holds what its code can't tell: decisions (ADRs), traps, a session log. Those are the wiki's raw material; code never enters the vault. The wiki gets the **lessons** that hold beyond the project, merged into concept and entity pages, so a later project or a question reuses experience from several projects at once.

## Layout

- **Snapshot** (raw, immutable): `raw/projects/YYYY-MM-DD-<project>/` holds a copy of the project's `AGENTS.md` and `docs/` at that date. The date is the ingestion date; `<project>` is the project page's slug.
- **Project page**: `wiki/projects/<project>.md`, one per project, updated by every ingestion. It takes the role of the source-summary page: a project gets no separate page among the sources. Pages that hold a project's lessons list the project page as their source (`[[<project>]]`); the project page lists its snapshots in the `snapshots` frontmatter, as plain folder names, since a snapshot is a folder.

## Project page

Frontmatter: the vault's standard keys, plus `type: project`, `status: active | paused | finished`, `location` (the project's folder or repo URL) and `snapshots` (the list of snapshot folders, oldest first).

Sections:

- **Purpose**: one or two lines.
- **Stack**: the main technologies, each linked to its entity page.
- **Status**: where the project stands and how it went.
- **Lessons**: one bullet per lesson, linked to the concept or entity page where it lives, citing the snapshot.
- **Reusable**: code worth reusing, with its path inside the project. Reading the project's code to find it is fine; copying it into the vault is not.
- **Decisions**: the ADRs that shaped the project, one line each, citing the snapshot; without ADRs, the decisions recorded in the log.

## Ingest a project

Run it only when the user asks, at a milestone: an important feature closed, the project paused or finished, or a new project about to start that could use these lessons. Not at every session: the day-to-day chronicle stays in the project's log.

These are the vault's ingest steps applied to a project, with the project page in the role of the source summary:

1. **Snapshot**: copy the project's `AGENTS.md` and `docs/` into a new snapshot folder. Code and everything else outside `docs/` stay in the project.
2. **Read what's new**: on the first ingestion, read the whole snapshot. Afterwards, compare the project with the newest snapshot listed on its page (e.g. `diff -r`) and read only what changed: new log entries, new or superseded ADRs, changed docs pages.
3. **Discuss**: present the 3-5 lessons that hold beyond this project, and the change in status, and ask the user what to emphasise. If the docs and the code visibly disagree, ask about that too.
4. **Project page**: create it, or update it in place (status, lessons, decisions, the new snapshot in `snapshots`); the snapshots keep the history.
5. **Integrate**: put each lesson in the concept or entity page where a future reader will look for it, creating the page if needed, with a link to the project page. When a lesson contradicts what the wiki already says, flag it the way the vault's schema flags contradictions.
6. **Bookkeeping**: update the overview if the lessons change the big picture, add new pages to the index, and append a log entry: `## [YYYY-MM-DD] project | <project>`, listing the pages created and updated.

Done when: the vault's own completion checks pass, every lesson from step 3 lives in a concept or entity page that links to the project page, and the project page lists the new snapshot.

## Queries across projects

Answer as for any query: start from the index, then read the concept pages where lessons live and the project pages they link to. Cite project pages and snapshots like any other source.

## Lint

Add to the vault's lint pass: project pages whose newest snapshot is missing from `raw/`; lessons listed on a project page but not present on any concept or entity page; `status: active` projects with no snapshot in the last 3 months, as a prompt for the user rather than a fix.
