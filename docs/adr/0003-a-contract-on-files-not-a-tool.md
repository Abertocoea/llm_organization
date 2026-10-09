# The system is a contract on files, not a tool

The system is a set of file conventions with rules written in plain text in `AGENTS.md`, so an agent with nothing installed can follow it; skills, scripts and issue trackers are optional layers that read and write the same files. This keeps the system usable with any agent and lets it coexist with skill sets instead of re-implementing them. The check is the independence test: a fresh agent reading only `AGENTS.md` must be able to follow the template.
