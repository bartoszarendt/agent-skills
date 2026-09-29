# Skills

A collection of self-contained agent skills for evidence-based development.
Each skill provides topic-specific guidance while preserving the user's scope,
existing authorization, project conventions, and proportionate verification.

Install individual directories for a project or user. The skills are plain
Markdown; they require no hooks, plugin runtime, scripts, or particular agent host.

## Skills

| Skill | Use it for |
|---|---|
| [agent-delegation](skills/agent-delegation/) | Running tasks in a separate Claude Code, Codex, OpenCode, or Pi CLI process and verifying the result. |
| [agent-instructions](skills/agent-instructions/) | Writing clear, scoped agent guidance and checking how its rules interact. |
| [api-design](skills/api-design/) | Defining programming contracts, consumer compatibility, and retry safety. |
| [code-review](skills/code-review/) | Investigating actionable defects and reporting evidence, impact, and gaps. |
| [code-simplification](skills/code-simplification/) | Removing demonstrated complexity while preserving intended behavior. |
| [debugging](skills/debugging/) | Diagnosing failures, testing explanations, and verifying focused corrections. |
| [documentation-and-adrs](skills/documentation-and-adrs/) | Keeping documentation accurate and recording consequential rationale. |
| [domain-language](skills/domain-language/) | Resolving domain terminology and maintaining a useful glossary. |
| [frontend-design](skills/frontend-design/) | Visual composition, styling, assets, and rendered web implementation. |
| [incremental-implementation](skills/incremental-implementation/) | Completing work in coherent increments with relevant final-state evidence. |
| [interview](skills/interview/) | Examining and stress-testing a proposal through rounds of questions and user decisions. |
| [performance-optimization](skills/performance-optimization/) | Diagnosing and improving performance across code, services, builds, and tests without hiding correctness trade-offs. |
| [planning](skills/planning/) | Sequencing multi-step work and parallel opportunities, from a brief outline to detailed task contracts with evidence of completion. |
| [security-and-hardening](skills/security-and-hardening/) | Assessing actual trust boundaries and applying relevant controls. |
| [task-handoff](skills/task-handoff/) | Preserving state, decisions, authorization, and next actions across sessions. |
| [testing-and-verification](skills/testing-and-verification/) | Selecting and maintaining checks that protect consequential behavior. |
| [ui-ux](skills/ui-ux/) | User journeys, navigation, interaction states, accessibility, and usable data presentation. |

Several skills contain references for conditional depth. Read them when the
main skill identifies a relevant case, rather than loading the entire collection.

### Design scopes

Use `api-design` for contracts between pieces of software, including internal
modules and component props. Use `ui-ux` for how people understand and complete
tasks. Use `frontend-design` for visual composition and implementation. A feature
can involve all three concerns; each skill remains independently usable.

## Working approach

- Inspect relevant evidence before changing code.
- Use the smallest coherent solution that meets the requested outcome.
- Make routine decisions independently within existing authorization.
- Preserve user work, intentional contracts, and meaningful operational constraints.
- Inspect existing coverage before adding tests; protect a named consequential gap.
- Verify in proportion to risk, and distinguish implementation from verified or deployed work.
- Keep one source of truth for plans, documentation, and decisions.

These skills supplement applicable instructions. Loading a skill does not
authorize commits, external communication, deployment, or shared-system changes.

## Install

Use the external [skills CLI](https://github.com/vercel-labs/skills). No custom
installer or plugin setup is required. The commands below pin **1.7.0**, the
version verified for this workflow; it requires **Node.js 22.20.0 or newer**
with npm. Remote Git sources also need Git and any required repository access.

### Personal skills shared across agent applications

Use the GitHub repository as the normal installation source; no local checkout
is needed. First discover the published skills and inspect existing installations:

```bash
npx skills@1.7.0 add bartoszarendt/skills --list
npx skills@1.7.0 list --global --agent codex claude-code opencode
```

Install a selected set for use across your projects:

```bash
npx skills@1.7.0 add bartoszarendt/skills --global --agent codex claude-code opencode --skill planning interview ui-ux
```

Omit `--skill` to select interactively in a normal terminal. Under an agent or
in a non-interactive environment, supply the intended skill names explicitly.
These commands install published content. Local changes must be committed and
pushed through an authorized workflow before they are available from GitHub.

This workflow uses the following locations, where `~` means your user directory:

| Location | Purpose |
|---|---|
| `~/.agents/skills/<name>/` | One installed copy, read by Codex and OpenCode |
| `~/.claude/skills/<name>` | Per-skill link to that copy for Claude Code |

On Windows the CLI uses directory junctions. If linking fails, it reports a
fallback to copies. Read the installation result: a successful copy is usable,
but is no longer one shared set of files. An explicit `--copy` selects that
independent-copy behavior.

These discovery paths are documented by
[Codex](https://developers.openai.com/codex/skills),
[OpenCode](https://opencode.ai/docs/skills/), and
[Claude Code](https://code.claude.com/docs/en/skills).
Other compatible applications may also read the shared directory; host selection
is not an access-isolation boundary.

### Existing files and collisions

Inspect any same-named skills at the intended destinations before writing.
The installer can replace a selected directory, including locally added files.
It does not provide digest-based protection for your edits. Do not rely on an
approval prompt: execution under an agent may be non-interactive.

Keep authored changes here and treat installed copies as managed output. Preserve
or reconcile any existing customizations before replacing them. Avoid `--all`
or `--yes` until the scope and affected destinations are understood.

### Refresh and remove

An installation is a snapshot, not a live link to the repository. After the
intended changes are published, repeat `add` with the intended names, scope,
and hosts:

```bash
npx skills@1.7.0 add bartoszarendt/skills --global --agent codex claude-code opencode --skill planning
```

For installations from a published Git source, the CLI also supports updates; keep
the install source and scope consistent and inspect the affected destinations
before refreshing.

List the result, and remove only a deliberately selected skill when needed:

```bash
npx skills@1.7.0 list --global --agent codex claude-code opencode
npx skills@1.7.0 remove planning --global --agent codex claude-code opencode
```

Removing a shared installation affects consumers of that shared copy. The remove
command operates on installed paths, not the authored directory in this checkout.
Check for local changes before removal.

A renamed or retired skill does not remove its previous installation. Remove the
old name, then add any replacement with the same scope and hosts.
`merge-conflict-resolution` (later `git-conflict-resolution`) and
`git-workflow-and-versioning` have been retired without replacement.

### Project-local or another computer

Use project-local installation when a repository needs a deliberate skill set.
Run from the consuming project's root and omit `--global`:

```bash
npx skills@1.7.0 add bartoszarendt/skills --agent codex claude-code opencode --skill planning interview
```

The shared copy is under `.agents/skills/`, with per-skill Claude links and
`skills-lock.json` recording the installation.

For a clone-ready team installation, use a published Git source and `--copy`
instead of committing Windows junctions. Once the intended skills are published:

```bash
npx skills@1.7.0 add bartoszarendt/skills --agent codex claude-code opencode --skill planning interview --copy
```

Review and commit the complete installed directories and `skills-lock.json`
according to the consuming project's policy. Copies are independent; refresh
all intended hosts together. Do not commit machine-specific link targets.

On another computer, repeat the installation from the same published revision.
User-level installations do not
synchronize across machines. Remote commands install published content, not
uncommitted changes in this checkout.

To install manually, copy a complete skill directory into a documented discovery
location, including references and required legal files. Manual copies need
manual refresh and do not gain the CLI's installation record.

### Testing unpublished changes

Maintainers can use a local checkout as the source in an isolated test destination:

```powershell
npx skills@1.7.0 add "C:\apps\skillset" --agent codex claude-code opencode --skill planning
```

Run from a disposable project's root, not the authored skill directory. A local
source is a development option, not the normal install command. Its lockfile
depends on the local directory layout. Refresh it by repeating `add`; do not
use `skills update` as the refresh mechanism for a local source.

### Verify availability

Use `skills list` to check the installer result, then start a fresh session in each
intended application and confirm the selected skills appear in its skill picker
or available-skills list. Check that a referenced file can be read when the skill
is used. Restart or reload when an existing session does not reflect the change.

Filesystem installation and CLI listing do not establish live host discovery.
The installer lifecycle was checked on Windows using local fixtures and an
isolated user profile:
shared placement, Claude junctions, directory contents, explicit refresh, selected
replacement and removal, project-local placement, copy mode, and an injected
link-failure fallback. Downloading this repository from GitHub, live agent
sessions, and Linux/macOS installs were not exercised in that check.

## Plan format

The plan guidance supports both a short task description and a phase-based plan,
optionally linked from a concise overview. Use the project's existing template,
work-unit names, and identifiers first; phases are the default without one.

Add detailed contracts, boundaries, anchors, proof, and likely misfires only
where interpretation risk warrants them. Map acceptance criteria to tasks or
owned integration gates. Preserve source intent when creating derived tasks,
and keep implemented, verified, blocked, deferred, and deployed states distinct.

The portable example is in
[the plan-format reference](skills/planning/references/plan-format.md).

## Collection rules

- Frontmatter contains only `name` and `description`.
- Each skill works independently, with references inside its own directory.
- Optional host capabilities have a usable fallback.
- Each `SKILL.md` stays at or below 250 lines.
- Instructions use concrete actions, clear conditions, and proportionate checks.
- Each skill includes a verification checklist.

See [AGENTS.md](AGENTS.md) for authoring and validation instructions.

## License

MIT for the collection; see [LICENSE](LICENSE).
