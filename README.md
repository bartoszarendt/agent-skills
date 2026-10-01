# Skills

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

A lightweight skill set for coding agents: plain Markdown, no plugins or
scripts, and one set of files for Claude Code, Codex, OpenCode, and other tools
that read [Agent Skills](https://agentskills.io/specification).

## Quick start

Requires Node.js 22.20.0 or newer. List the available skills, then install a
selection for your user account:

```bash
npx skills@1.7.0 add bartoszarendt/agent-skills --list
npx skills@1.7.0 add bartoszarendt/agent-skills --global --agent codex claude-code opencode --skill planning debugging code-audit
```

Start a new agent session to pick them up. See [Install](#install) for
project-local installs, refresh, removal, and existing files.

## Approach

**A working set, not a catalogue.** The collection contains skills I use. When a
skill stops changing how agents work, I remove it.

**Judgment, not process.** The skills do not define phases, slash commands, or
personas. Each one covers decisions in a specific area, such as what to test,
where a trust boundary lies, or how much detail a plan needs, within the
workflow a project already uses.

**Project and user instructions come first.** Skills supplement them. Loading a
skill does not authorize commits, pushes, deployment, or external messages, and
does not add approval steps to work you have already asked for.

**Effort in proportion to consequence.** Investigation, tests, and verification
scale with what a change can break. Checklists are there to confirm the relevant
points, not to turn a small fix into a long procedure.

**Reported state matches evidence.** Skills ask agents to keep implemented,
verified, and deployed work distinct, and to state what was not checked.

**Portable and independent.** Frontmatter contains only `name` and
`description`. There are no hooks, scripts, host-specific settings, or
dependencies between skills. Copying one directory is enough.

**Short entrypoints.** Each `SKILL.md` stays at or below 250 lines. Detail that
only some tasks need lives in the skill's `references/` directory.

## Skills

### Clarify and plan

| Skill | Use it for |
|---|---|
| [interview](skills/interview/) | Examining or stress-testing a proposal or open topic through rounds of questions and user decisions, until the work can proceed without invented requirements, including clarifying material uncertainty during other work. |
| [planning](skills/planning/) | Sequencing multi-step work and parallel opportunities, from a brief outline to detailed task contracts with evidence of completion. |
| [exploration](skills/exploration/) | Answering how something works, where it lives, or what depends on it, with cited evidence and stated coverage. |

`exploration` establishes what exists and how it works. `code-audit` judges
whether it is defective, `debugging` explains why it misbehaves, `interview`
settles what the user intends, and `planning` sequences the agreed work.

### Build

| Skill | Use it for |
|---|---|
| [implementation](skills/implementation/) | Completing work in coherent increments with relevant final-state evidence. |
| [api-design](skills/api-design/) | Defining programming contracts, consumer compatibility, and retry safety. |
| [ui-ux](skills/ui-ux/) | User journeys, navigation, interaction states, accessibility, and usable data presentation. |
| [frontend-design](skills/frontend-design/) | Visual composition, styling, assets, and rendered web implementation. |

`api-design` covers contracts between pieces of software, including internal
modules and component props. `ui-ux` covers how people understand and complete
tasks. `frontend-design` covers visual composition and implementation. A feature
can involve all three.

### Verify and improve

| Skill | Use it for |
|---|---|
| [testing-and-verification](skills/testing-and-verification/) | Selecting and maintaining checks that protect consequential behavior. |
| [debugging](skills/debugging/) | Diagnosing failures, testing explanations, and verifying focused corrections. |
| [code-audit](skills/code-audit/) | Auditing a codebase, module, or change for actionable defects, with evidence, impact, and stated coverage. |
| [code-simplification](skills/code-simplification/) | Removing demonstrated complexity while preserving intended behavior. |
| [performance-optimization](skills/performance-optimization/) | Diagnosing and improving performance across code, services, builds, and tests without hiding correctness trade-offs. |
| [security-and-hardening](skills/security-and-hardening/) | Assessing actual trust boundaries and applying relevant controls. |

### Continuity and agents

| Skill | Use it for |
|---|---|
| [documentation-and-adrs](skills/documentation-and-adrs/) | Keeping documentation accurate and recording consequential rationale. |
| [handoff](skills/handoff/) | Transferring or resuming any kind of work with its state, decisions, authorization, and next actions. |
| [agent-delegation](skills/agent-delegation/) | Running tasks in a separate Claude Code, Codex, OpenCode, or Pi CLI process and verifying the result. |
| [agent-instructions](skills/agent-instructions/) | Writing clear, scoped agent guidance and checking how its rules interact. |

## How skills load

An agent host shows the agent each installed skill's name and description. When
a task matches a description, the agent reads that `SKILL.md`, and it reads a
file under `references/` only when the skill points to it for the case at hand.
You can also ask for a skill by name; some hosts additionally offer a skill
picker or command.

## Install

The commands use the external [skills CLI](https://github.com/vercel-labs/skills),
pinned to **1.7.0**, the version verified for this workflow. It requires
**Node.js 22.20.0 or newer** with npm; remote Git sources also need Git.

### User-level installation

Use this for a personal set shared across your projects. Check what is already
installed, then add the skills you want:

```bash
npx skills@1.7.0 list --global --agent codex claude-code opencode
npx skills@1.7.0 add bartoszarendt/agent-skills --global --agent codex claude-code opencode --skill planning interview ui-ux
```

Omit `--skill` to choose interactively in a terminal. When an agent or script
runs the command, name the skills explicitly.

| Location (`~` is your user directory) | Purpose |
|---|---|
| `~/.agents/skills/<name>/` | One installed copy, read by Codex and OpenCode |
| `~/.claude/skills/<name>` | Per-skill link to that copy for Claude Code |

These locations are documented by [Codex](https://developers.openai.com/codex/skills),
[OpenCode](https://opencode.ai/docs/skills/), and
[Claude Code](https://code.claude.com/docs/en/skills). Other compatible
applications may also read the shared directory; choosing hosts does not restrict
access to it.

On Windows the CLI links with directory junctions. If linking fails, it falls
back to copies and says so. A copy works but is no longer shared between hosts.
`--copy` selects copies explicitly.

### Existing files

The installer can replace a same-named directory, including files you added, and
does not protect local edits. Do not rely on a confirmation prompt: when an
agent runs the command, there may be none. Before installing, refreshing,
or removing, check the destinations for local edits and keep your own changes
elsewhere. Avoid `--all` and `--yes` until you know which destinations they
affect.

### Refresh and remove

An installation is a snapshot. To pick up published changes, repeat `add` with
the same names, scope, and hosts:

```bash
npx skills@1.7.0 add bartoszarendt/agent-skills --global --agent codex claude-code opencode --skill planning
```

The CLI also supports updates for Git sources; keep the source and scope
consistent and check the destinations first. To remove a skill:

```bash
npx skills@1.7.0 remove planning --global --agent codex claude-code opencode
```

Removal affects every host that reads the shared copy. It operates on installed
paths, not on this repository.

<details>
<summary>Project-local installation, team copies, and other computers</summary>

Use a project-local installation when a repository needs its own skill set. Run
from that project's root without `--global`:

```bash
npx skills@1.7.0 add bartoszarendt/agent-skills --agent codex claude-code opencode --skill planning interview
```

The shared copy goes under `.agents/skills/`, with per-skill Claude links and a
`skills-lock.json` recording the installation.

To commit skills for a team, use `--copy` rather than committing Windows
junctions:

```bash
npx skills@1.7.0 add bartoszarendt/agent-skills --agent codex claude-code opencode --skill planning interview --copy
```

Review and commit the complete installed directories together with
`skills-lock.json`, following the project's policy. Copies are independent, so
refresh all hosts together, and do not commit machine-specific link targets.

User-level installations do not synchronize between machines. Repeat the
installation on each computer.

To install manually, copy a complete skill directory, including `references/`,
into a documented discovery location. Manual copies need manual refresh and have
no installation record.

</details>

<details>
<summary>Verify availability</summary>

`skills list` confirms the files are in place, not that a host sees them. Start
a new session in each application and check that the skills appear in its skill
list or picker, and that a referenced file can be read when a skill is used.

The installer workflow was checked on Windows with local fixtures and an
isolated user profile. Linux, macOS, installing from GitHub, and live agent
sessions were not part of that check.

</details>

## Contributing

[AGENTS.md](AGENTS.md) holds the authoring rules and the content checks to run
before a change. To try unpublished changes, install from a local checkout into
a disposable project:

```bash
npx skills@1.7.0 add <path-to-checkout> --agent codex claude-code opencode --skill planning
```

Repeat `add` to refresh a local source; `skills update` does not apply to it.

## License

[MIT](LICENSE).
