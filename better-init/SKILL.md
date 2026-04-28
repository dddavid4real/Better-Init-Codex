---
name: better-init
description: >-
  Initialize a new project folder with a concise AGENTS.md, durable project context,
  and linked reference markdown files instead of making the user restate everything
  from scratch. Use this whenever the user wants to bootstrap a fresh directory,
  initialize project context, create or reset project agent instructions, set up a project
  contract, or start a new research/coding project with reusable instructions and
  reference docs. This skill is especially relevant when the project is new,
  underspecified, mixed-purpose, or needs file-based context organization.
metadata:
  version: "1.3.0"
  scope: personal
---

# Better Init

Bootstrap a new project directory so future Codex sessions have the right durable context without bloating `AGENTS.md`.

The goal is to create a clean, reusable setup:
- `AGENTS.md` stays concise and operational
- richer project context lives in markdown files under a reference folder
- the workflow adapts to the real project type instead of copying a generic coding template
- `CLAUDE.md` is created or updated only when the user explicitly wants Claude compatibility

## When to use this skill

Use this skill when the user wants to:
- initialize a brand new project folder
- create, regenerate, or clean up `AGENTS.md`
- set up project-specific context in a new directory
- start a research project, coding project, or mixed workspace and avoid repeating the same instructions later
- establish a reusable project contract plus linked background docs
- create a parallel `CLAUDE.md` for compatibility with Claude-managed folders

## Core principles

1. **Reuse context already given.** If the user already described the project, do not ask them to repeat it.
2. **Ask only for missing essentials.** Use a minimal intake.
3. **Keep `AGENTS.md` short.** Store details in reference docs and link to them by path.
4. **Adapt to the project.** Research projects, coding repos, and mixed folders need different contracts.
5. **Draft before writing.** Show the proposed structure and `AGENTS.md` draft, then ask for confirmation before creating or updating files.
6. **Do not invent tooling.** Only include commands or architecture boundaries you actually discovered.
7. **Preserve compatibility deliberately.** Do not create or rewrite `CLAUDE.md` unless the user asks for it or the existing project clearly depends on it.

## Workflow

### 1. Identify the target project directory

First, determine the real working folder.

- If the user named a directory, use that.
- If they are already inside the intended project directory, confirm that from context.
- If the current location is a mixed workspace, do not treat the whole workspace as one project.

Before drafting anything:
- read any existing `AGENTS.md`
- read any existing `CLAUDE.md` only to preserve compatibility context or when the user asks for Claude support
- inspect the local directory structure
- inspect project-local config files before assuming build/test/lint commands

If the target directory is ambiguous, ask first.

### 2. Run minimal intake

Reuse information already present in the conversation. Only ask for what is missing.

Always gather these essentials:
1. **Project intro** - but only if the user has not already provided it
2. **Preferred name** - ask what the user wants Codex to call them
3. **Reference-doc folder** - default to `doc/`; only ask if the user wants to override it

Offer this optional preference when relevant:
- whether to enable "efficient reply mode" in the generated `AGENTS.md`; default is no unless the user explicitly asks for it
- whether to also create or update a parallel `CLAUDE.md` for Claude compatibility; default is no for Codex-first projects

Also ask clarifying questions when needed for:
- project type (research, coding, mixed, other)
- whether an existing `AGENTS.md` should be replaced or merged
- whether an existing `CLAUDE.md` should be mirrored, preserved, or left untouched
- any missing high-value constraints that would materially change the contract

Also ask clarifying questions first, before proposing files, when the request is ambiguous about the target directory, project type, or whether this should be a coding, research, or mixed setup.

Keep the intake short. Do not interrogate the user with unnecessary setup questions.

## Required standing instructions for the drafted `AGENTS.md`

Include these user-level instructions in the draft:
- Always start conversation responses with the user's preferred name followed by a comma
- Always ask first when something important is unclear or uncertain
- Always figure out the clear plan before starting substantive work

Write these as concise project instructions, not as a long biography or transcript.

## Optional efficient reply mode

If the user explicitly opts in, enable "efficient reply mode" by including the following block in the generated `AGENTS.md` exactly as written.

Rules:
- the option must be explicit and default-off
- copy the block below identically; do not rewrite, summarize, normalize, or reformat it
- do not mention temporary source-file names in downstream generated instructions
- if the user does not opt in, omit the block entirely

Verbatim block to insert:

```markdown
## Output
- Answer is always line 1. Reasoning comes after, never before.
- No preamble. No "Great question!", "Sure!", "Of course!", "Certainly!", "Absolutely!".
- No hollow closings. No "I hope this helps!", "Let me know if you need anything!".
- No restating the prompt. If the task is clear, execute immediately.
- No explaining what you are about to do. Just do it.
- No unsolicited suggestions. Do exactly what was asked, nothing more.
- Structured output only: bullets, tables, code blocks. Prose only when explicitly requested.

## Token Efficiency
- Compress responses. Every sentence must earn its place.
- No redundant context. Do not repeat information already established in the session.
- No long intros or transitions between sections.
- Short responses are correct unless depth is explicitly requested.

## Typography - ASCII Only
- Do not use em dashes. Use hyphens instead.
- Do not use smart or curly quotes. Use straight quotes instead.
- Do not use the ellipsis character. Use three plain dots instead.
- Do not use Unicode bullets. Use hyphens or asterisks instead.
- Do not use non-breaking spaces.
- Do not modify content inside backticks. Treat it as a literal example.

## Sycophancy - Zero Tolerance
- Never validate the user before answering.
- Never say "You're absolutely right!" unless the user made a verifiable correct statement.
- Disagree when wrong. State the correction directly.
- Do not change a correct answer because the user pushes back.

## Accuracy and Speculation Control
- Never speculate about code, files, or APIs you have not read.
- If referencing a file or function: read it first, then answer.
- If unsure: say "I don't know." Never guess confidently.
- Never invent file paths, function names, or API signatures.
- If a user corrects a factual claim: accept it as ground truth for the entire session. Never re-assert the original claim.

## Code Output
- Return the simplest working solution. No over-engineering.
- No abstractions or helpers for single-use operations.
- No speculative features or future-proofing.
- No docstrings or comments on code that was not changed.
- Inline comments only where logic is non-obvious.
- Read the file before modifying it. Never edit blind.

## Warnings and Disclaimers
- No safety disclaimers unless there is a genuine life-safety or legal risk.
- No "Note that...", "Keep in mind that...", "It's worth mentioning..." soft warnings.
- No "As an AI, I..." framing.

## Session Memory
- Learn user corrections and preferences within the session.
- Apply them silently. Do not re-announce learned behavior.
- If the user corrects a mistake: fix it, remember it, move on.

## Scope Control
- Do not add features beyond what was asked.
- Do not refactor surrounding code when fixing a bug.
- Do not create new files unless strictly necessary.

## Override Rule
User instructions always override this file.

```

### 3. Optional planning support for non-trivial setups

Use planning files only as optional execution support for non-trivial setup work.

Before confirmation:
- decide whether planning support would help
- mention that choice in the draft
- explain what would go into planning files versus durable reference docs
- do not invoke `planning-with-files` yet

After confirmation:
- if the approved setup is long-running, exploratory, or multi-phase, invoke `planning-with-files` if it is available and appropriate in the current environment
- otherwise skip planning files entirely and keep the setup lean

Use planning support only for tasks such as:
- multi-step initialization that will continue after bootstrap
- research-heavy discovery work
- setup work that needs explicit progress tracking across sessions

Important distinctions:
- planning files such as `task_plan.md`, `findings.md`, and `progress.md` are execution-tracking artifacts
- reference docs under `doc/` are the durable project references future sessions should consult
- planning files should not replace durable topic docs like `doc/background.md` or `doc/architecture.md`

If you do use planning files:
- keep them in the project directory, not the skill directory
- do not paste large planning contents into `AGENTS.md`
- reference them from `AGENTS.md` only when they are genuinely useful to future work

### 4. Propose a reference-doc structure

Use `doc/` as the default reference folder.

Create only the files that the project actually needs. Examples:
- `doc/background.md`
- `doc/architecture.md`
- `doc/dataset.md`
- `doc/experiments.md`
- `doc/workflow.md`

Rules:
- do not create speculative or empty docs
- prefer a few meaningful files over many shallow ones
- separate durable context by topic
- keep file names obvious and stable

For research-heavy projects, favor files like:
- background
- datasets
- experiments
- literature
- workflow

For coding-heavy projects, favor files like:
- architecture
- domain-boundaries
- environment
- verification

For mixed projects, use a hybrid structure.

### 5. Draft a project-specific `AGENTS.md`

Draft `AGENTS.md` so it is short, operational, and easy to scan.

It should usually include:

```markdown
# Project Contract

## Project Overview
- One concise paragraph on what this project is for

## Reference Files
- `doc/background.md` - [what it contains]
- `doc/...` - [what it contains]
- `task_plan.md` / `findings.md` / `progress.md` - [if relevant]

## User Preferences
- Start responses with "<preferred-name>, "
- Ask first when something important is uncertain
- Establish a clear plan before substantive work

## Build And Test / Research Workflow / Working Approach
- Include only what is actually relevant to this project type

## Safety Rails
### NEVER
- Project-specific things to avoid

### ALWAYS
- Project-specific things to preserve or verify

## Verification
- Only real, discovered verification steps

## Compact Instructions
Preserve:
1. Architecture or research decisions that should not be re-derived
2. Modified files and key changes
3. Current verification status
4. Open risks, TODOs, and rollback notes
```

Adapt the middle sections to the actual project:

#### If this is a coding project
You may include sections like:
- Build And Test
- Architecture Boundaries
- Coding Conventions
- Verification

But only include commands or boundaries if you actually discovered them.

#### If this is a research project
Prefer sections like:
- Research Overview
- Data / Dataset References
- Experiment Tracking
- Scripts / Notebooks / Pipelines
- Validation Workflow

#### If this is a mixed project
Blend both styles, but keep it concise.

### Optional `CLAUDE.md` compatibility

If the user explicitly wants Claude compatibility, draft a parallel `CLAUDE.md` after the `AGENTS.md` draft. Keep it pointer-based and behaviorally aligned with `AGENTS.md`.

Rules:
- Do not create `CLAUDE.md` by default in Codex-first projects.
- If a `CLAUDE.md` already exists, prefer preserving it or making a minimal synchronized update instead of replacing it wholesale.
- Avoid duplicating long reference content in both files; both files should point to the same durable docs.
- If both files exist, make clear which one is primary for Codex (`AGENTS.md`) and which is compatibility-only (`CLAUDE.md`).

## 6. Show the draft before writing

Before creating or updating files, present:
1. the proposed reference folder and files
2. the proposed `AGENTS.md` structure
3. whether "efficient reply mode" is enabled or omitted
4. the actual `AGENTS.md` draft text
5. whether a compatibility `CLAUDE.md` will be created, updated, or left untouched
6. a brief note on what will be stored in planning files versus reference docs

Then ask for confirmation.

Do **not** write files until the user approves.

## 7. After approval, write the files

Once the user approves:
- create or update `AGENTS.md`
- if the user opted in, insert the embedded verbatim "efficient reply mode" block into `AGENTS.md` exactly as written
- create or update `CLAUDE.md` only if the user approved Claude compatibility
- create the chosen reference folder if needed
- create only the approved reference markdown files
- write the topic-specific content into those files
- keep `AGENTS.md` limited to concise operating instructions plus file references, plus the optional "efficient reply mode" block when approved
- if planning support was approved and the work is genuinely non-trivial, invoke `planning-with-files` and keep those planning files separate from the durable reference docs

After writing:
- read back the files you created or updated
- verify that referenced paths actually exist
- summarize the resulting structure briefly for the user

## Anti-patterns

Avoid these mistakes:
- copying a JavaScript project contract into a non-JS project
- inventing install/dev/test/lint commands
- assuming the workspace root is the project root in a heterogeneous directory
- dumping all project background directly into `AGENTS.md`
- creating too many markdown files up front
- skipping the confirmation step before writing files
- invoking `planning-with-files` before the user approves a non-trivial setup draft
- asking the user to restate context they already gave you
- rewriting `CLAUDE.md` just because it exists; treat it as optional compatibility unless requested

## Output expectations

When using this skill successfully, the result should be:
- a concise `AGENTS.md`
- an optional compatibility `CLAUDE.md` only when the user explicitly asked for it
- an optional verbatim "efficient reply mode" block only when the user explicitly asked for it
- a small set of stable reference docs under `doc/` by default
- optional planning files only when the initialization is long-running or genuinely non-trivial
- a clear distinction between execution-tracking files and durable reference docs
- a project contract that matches the real work instead of a copied template

## Example trigger phrases

This skill should be a strong match for prompts like:
- "initialize this new project folder"
- "set up an AGENTS.md for this research project"
- "set up AGENTS.md and a Claude-compatible CLAUDE.md"
- "bootstrap this directory so I don't have to repeat the context every time"
- "create a project contract and put detailed context into separate markdown files"
- "start this new repo and set up persistent project instructions"
