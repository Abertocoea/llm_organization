# llm_organization

A lightweight way to organize coding projects so that AI coding agents (Claude Code, Codex, OpenCode, …):

1. **spend fewer tokens**: each project carries a short map and a small `docs/` folder, so the agent stops rediscovering the project at every session;
2. **learn across projects**: lessons from each project flow into a personal **second brain**, which later projects can read and you can query about several projects at once.

It's a set of file conventions, not a tool. Any agent that reads `AGENTS.md` can follow it, with nothing installed.

## Origin

The second brain follows the **LLM Wiki** pattern from [Andrej Karpathy's idea file](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f): an LLM incrementally builds and maintains a wiki of interlinked markdown pages from your sources, instead of rediscovering them at every question.

This repo extends that idea in two ways: a **project template** that keeps each project's knowledge compact and current, and **project ingestion**, which treats a project as one more source for the wiki.

Inside each project, the template adopts the conventions of [Matt Pocock's skills](https://github.com/mattpocock/skills): ADRs in `docs/adr/` with his short format and his three criteria for when a decision deserves one, and an optional `GLOSSARY.md` for domain terms. His skills therefore work on projects built from this template, though the template doesn't require them.

## How it works

```
second brain (LLM Wiki vault)          your projects
├── raw/        immutable sources      ├── project-a/
└── wiki/       pages the LLM writes   │   ├── AGENTS.md   short map + rules
                                       │   └── docs/       decisions, traps, log
          ▲                            └── project-b/
          │  ingest at milestones                 │
          └───────────────────────────────────────┘
          ▼  read when a task could reuse a past lesson
```

- **Inside a project**, the agent reads `AGENTS.md` and only the docs the task touches. Docs are updated at three moments: a decision (an ADR), the end of a session (a log entry), and the end of a feature (five quick questions).
- **Between projects**, a project's docs are ingested into the second brain at meaningful milestones: a snapshot, a project page, and lessons merged into the wiki's concept pages.

## Repo layout

| Folder | What it is |
|---|---|
| [`project-template/`](project-template/) | The files to copy into every new project |
| [`wiki-schema/`](wiki-schema/) | The extension that lets an LLM Wiki ingest projects |
| [`scripts/`](scripts/) | Automation for the mechanical steps (none yet) |

## Use the template by hand

1. Copy `project-template/` into your project's root (`AGENTS.md`, `CLAUDE.md`, `docs/`).
2. In `AGENTS.md`, replace the placeholders:
   - `{{PROJECT_NAME}}` and `{{ONE_LINE_PURPOSE}}`;
   - `{{DOCS_LANGUAGE}}` and `{{USER_LANGUAGE}}`: the language of the docs and the one your agent talks to you in (usually the same; a public repo may want English docs);
   - `{{SECOND_BRAIN_PATH}}`: the absolute path of your LLM Wiki vault.

   If `{{DOCS_LANGUAGE}}` isn't English, also translate the few lines of `docs/index.md` and `docs/log.md`, so your docs don't end up in two languages.

   In a public repo, keep personal values such as `{{SECOND_BRAIN_PATH}}` out of `AGENTS.md`: put them in a git-ignored local file and have `AGENTS.md` point to it.
3. Fill in the commented lines under *Start here* (commands, folder map, conventions), or ask your agent to fill them after exploring the project once.
4. Work as usual. The agent follows the rules in `AGENTS.md`.

`CLAUDE.md` contains only `@AGENTS.md`, so Claude Code reads the same rules as every other agent.

## Optional layers

The template works on its own. These layers can sit on top:

- **Skills** that automate the steps `AGENTS.md` already describes, such as [mattpocock/skills](https://github.com/mattpocock/skills), whose conventions the template follows.
- **An issue tracker.** When a project uses one, log entries link to issues instead of repeating them.
- **Scripts** for scaffolding and installation (planned).

## License

[MIT](LICENSE)
