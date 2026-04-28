# Better Init for Codex

A Codex skill for bootstrapping a new project folder with the right long-lived context.

Instead of stuffing everything into `AGENTS.md`, **Better Init** helps Codex create:
- a concise, project-specific `AGENTS.md`
- a small set of durable reference docs under `doc/` by default
- an approval-first setup flow that drafts before writing files
- an optional verbatim instruction block for efficient answering style when the user explicitly chooses it
- a parallel `CLAUDE.md` only when Claude compatibility is explicitly wanted

## What the skill does

Better Init guides Codex to:
- identify the real target directory instead of assuming the whole workspace is one project
- inspect local files before inventing commands, tooling, or architecture
- ask only for missing essentials
- keep `AGENTS.md` concise and path-based
- store richer project context in focused markdown files
- adapt the setup for coding, research, or mixed workspaces
- separate durable reference docs from optional planning files
- show the proposed structure and `AGENTS.md` draft before writing anything
- preserve Claude compatibility deliberately instead of creating `CLAUDE.md` by default

## When to use it

Use this skill when you want Codex to:
- initialize a new project folder
- create, regenerate, or clean up a project `AGENTS.md`
- set up reusable project context for future sessions
- organize project background into markdown files instead of one giant instruction file
- bootstrap a research project, coding repo, or mixed workspace without bad defaults
- create a compatible `CLAUDE.md` only when that is part of the task

Typical examples:
- a fresh code repository that still needs project-local instructions
- a research folder with papers, notes, datasets, and scripts
- a mixed workspace where Codex should not invent repo-wide commands
- any project where you want a draft-first, confirm-before-write setup

## Key behaviors

Better Init is opinionated in a few important ways:
- **Minimal intake**: reuse what the user already said and ask only for missing essentials
- **User preferences preserved**: include the user's preferred name and core working rules in the drafted `AGENTS.md`
- **Efficient reply mode**: include the full reply-efficiency block only when the user explicitly chooses it
- **`doc/` by default**: use `doc/` for durable references unless the user wants another folder
- **Concise `AGENTS.md`**: keep it focused on durable instructions and file references unless the user opts into the extra verbatim block
- **Claude compatibility is deliberate**: create or update `CLAUDE.md` only when requested or clearly required
- **Planning support only when useful**: use planning files for non-trivial setups, not for every bootstrap
- **Draft first**: never write files before showing the proposed structure and asking for approval

## Optional planning support

Better Init can work with a planning-file workflow for longer project initialization runs.

Use planning files when setup is multi-step, exploratory, or likely to continue across sessions.

Skip them when the project only needs a clean `AGENTS.md` plus a few reference docs.

The important distinction:
- `AGENTS.md` is the durable project contract
- `doc/` holds long-lived background and reference material
- planning files track execution state only when that state is useful

## Efficient reply mode

Better Init can optionally enable "efficient reply mode" inside the generated `AGENTS.md`.

- This option is off by default.
- The block is included only when the user explicitly chooses it.
- When included, the contents are copied identically.
- Downstream generated instructions should not mention temporary source-file names.

## Installation

Copy the `better-init` folder into your personal Codex skills directory:

```bash
git clone https://github.com/dddavid4real/Better-Init-Codex.git
cd Better-Init-Codex
cp -R better-init ~/.codex/skills/
```

After copying, start a new Codex session or reload your current one so the skill list refreshes.

## Usage

Invoke the skill by asking Codex to use Better Init:

```text
Use Better Init to initialize this research folder.
```

Or provide a little context up front:

```text
Use Better Init to set up this new repo with a clean AGENTS.md.
```

```text
Use Better Init here. This folder has papers, scripts, and notes; draft the structure first.
```

```text
Use Better Init to set up this repo and enable efficient reply mode.
```

```text
Use Better Init and also create a CLAUDE.md for compatibility.
```

## What a successful run should produce

A good Better Init run usually ends with:
- a concise `AGENTS.md`
- an optional verbatim "efficient reply mode" block only when the user explicitly asked for it
- no temporary source-file naming leaked into downstream project instructions
- a small, useful set of reference docs under `doc/`
- project instructions that match the real folder contents
- no invented commands or boilerplate
- clear confirmation before any files are written

## Expected project structure

After using Better Init, a project will usually end up with something like this:

```text
your-project/
|-- AGENTS.md
|-- task_plan.md
|-- findings.md
|-- progress.md
`-- doc/
    |-- background.md
    |-- architecture.md
    |-- dataset.md
    `-- workflow.md
```

The exact files depend on the project.

For example:
- coding projects may lean toward `architecture.md`, `domain-boundaries.md`, or `verification.md`
- research projects may lean toward `background.md`, `dataset.md`, `experiments.md`, or `literature.md`
- mixed workspaces may use a smaller hybrid set

The important idea is simple:
- `AGENTS.md` stays short and operational by default
- the optional "efficient reply mode" content is included only when the user explicitly wants it
- detailed, durable context lives in separate markdown files
- planning files track non-trivial setup work across sessions
- Codex gets clearer project guidance with less clutter

## Acknowledgement

Part of the idea is from @Tw93: https://x.com/HiTw93/status/2032091246588518683

The verbatim contents used for the optional "efficient reply mode" came from https://github.com/drona23/claude-token-efficient.

## License

MIT. See [LICENSE](./LICENSE).
