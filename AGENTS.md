# AGENTS.md

Guidance for agents working on this repository. The skills are reusable content
for other projects; these instructions govern their maintenance and distribution.

## Repository model

`skills/` is the authoritative authored content. Use the external `skills` CLI
to place unchanged skill directories where supported agent applications discover
them. There is no custom installer, runtime, host adapter, or generated skill body.

```text
skills/<name>/SKILL.md          required frontmatter and instructions
skills/<name>/references/*.md   optional detail, linked from the entrypoint
skills/<name>/LICENSE.txt       required license text, when applicable
skills/<name>/NOTICE            required notices, when applicable
README.md                      installation, refresh, removal, and user guidance
tmp/                           ignored reference material; never edit or commit
```

Host-neutral content does not prohibit external installation tooling. A skill
must work after copying its complete directory without running that tooling.

## Skill contract

- Frontmatter contains exactly `name` and `description`. The name matches the
  directory, uses lowercase letters, digits, and single hyphens, and is at most
  64 characters. The description is at most 1024 characters and states capability
  and applicability. Follow the [Agent Skills format](https://agentskills.io/specification).
- Keep each `SKILL.md` at or below 250 lines. Put substantial conditional detail
  one level deep under `references/`; link it from the entrypoint with a useful
  reading condition.
- Keep each skill independently usable. Do not link to or require another skill,
  a shared external instruction file, or a host-specific tool. Ordinary topic
  words such as "planning" are not cross-skill dependencies.
- Phrase optional environment capabilities conditionally and provide a usable
  fallback. Do not add host-only frontmatter or invocation settings.
- Maintain one skill per topic. Extend an existing skill when it already owns
  the responsibility.
- Include a proportionate verification checklist.
- Retain required license text, attribution, and modification notices with the
  affected skill. Keep origin links, collection names, and reviewed revision
  identifiers out of authored guidance and descriptions. This does not remove
  legal notices or links to useful technical documentation.

## Writing and behavior

Use imperative, concrete language with explicit conditions. Avoid personas,
slogans, arbitrary quotas, and unsupported universal claims.

Preserve the requested outcome, existing authorization, and user work. Separate
analysis, implementation, and external actions. Permit routine autonomy and
continued independent work without adding approval gates.

Scale investigation, task detail, tests, and verification to the consequence.
Inspect existing mechanisms and coverage before adding more. Do not turn a
reference checklist into an unconditional requirement for every task.

Keep entrypoints, references, and completion criteria consistent. Do not let a
checklist reintroduce a blanket rule removed from the main instructions.

## Installation contract

README.md owns the commands and supported workflow. Use its pinned CLI version
for reproducible verification; assess behavior before changing that pin.

- Prefer user-level shared installation for a personal set used across projects.
  Use project-local installation for a repository-specific selection.
- Use `bartoszarendt/skills` as the normal installation source. Local checkout
  paths are for testing unpublished changes in isolated destinations. Publishing
  requires its own authorization; do not commit or push merely to test installation.
- Installed directories are managed snapshots. Edit this repository, then
  publish through the authorized workflow and deliberately refresh selected
  skills. Local edits do not propagate automatically. Refresh local test sources
  by repeating `add`.
- Codex and OpenCode use the shared `.agents/skills` location in this workflow.
  Claude Code receives per-skill links. Do not create redundant host copies or
  change skill contents for a host.
- A copy installation is an explicit alternative when links are unsuitable.
  Report whether the result is shared or copied; link failure must not be
  described as successful sharing.
- Select scope, hosts, source, and skill names deliberately. Do not assume a
  host selection isolates access to a directory other hosts can already read.
- Inspect existing selected destinations before install, refresh, or removal.
  The external installer can replace local edits and is not an ownership-aware
  updater. Stop on unexpected user-owned content and resolve it before writing.
  Do not rely on interactive prompts, especially when running under an agent.
- Remove only the requested installation and account for shared consumers.
  Preserve unrelated skills and authored source files.
- Do not alter consuming projects' `AGENTS.md`, `CLAUDE.md`, agent permissions,
  or activation settings merely to advertise installed skills.
- Keep absolute local paths and Windows junctions out of portable project state.
  For a committed project installation, use the documented copy workflow and a
  portable source. Inspect generated files and the installer lockfile together.

Do not add an installer wrapper, package manifest, lifecycle service, or tracking
format without a concrete need the existing workflow cannot meet.

## Change workflow

1. Inspect the working tree and preserve unrelated changes.
2. Read the affected skill and its references; establish the intended behavior.
3. Revise the smallest coherent set of instructions and update README when
   names, scope, discovery, or installation behavior changes.
4. Check applicable terms before incorporating third-party material.
5. Run checks appropriate to the change and report actual results and gaps.

## Content checks

Run from the repository root in Git Bash on Windows:

```bash
# Discover skills without installing them
npx -y skills@1.7.0 add ./ --list

# Frontmatter keys and directory/name agreement
for f in skills/*/SKILL.md; do d=$(basename "$(dirname "$f")")
  keys=$(awk 'NR==1{next} /^---$/{exit} /^[a-zA-Z-]+:/{sub(/:.*/,""); printf "%s ", $0}' "$f")
  [ "$keys" = "name description " ] || echo "frontmatter keys [$keys]: $f"
  grep -q "^name: $d$" "$f" || echo "name mismatch: $f"
done

# Entrypoint line budget
wc -l skills/*/SKILL.md | awk '$2 != "total" && $1 > 250 {print "over budget:", $2}'

# Explicit references to another skill
for d in skills/*/; do n=$(basename "$d")
  grep -rlF --include='*.md' -e "\`$n\`" -e "skills/$n/" -e "../$n/" -e "\$$n" skills | grep -v "^skills/$n/" | sed "s|$| references $n|"
done
```

All checks except discovery must print nothing. Also verify name and description
lengths, checklists, local links, and required legal files for affected material.
Review indirect dependencies manually; token matching cannot establish semantics.

For material instruction changes, assess realistic routine, ambiguous, and
authorization-limited requests. Static packaging checks do not prove behavior.

## Installation verification

When installation commands, layout assumptions, or the CLI version change, use
temporary source, destination, and user-profile locations. Do not test against
the user's actual global skills or other projects.

Verify the consequential cases: complete directory contents, shared link targets,
deliberate refresh, selected-name collisions, unrelated-skill preservation,
removal, and explicit copy or reported fallback. Exercise project-local placement
when its documented behavior changes.

Confirm resolved targets stay inside the temporary workspace before destructive
fixture operations. Account for cleanup without traversing a link into user data.

Distinguish filesystem installation, installer listing, and live agent discovery.
Do not claim host-runtime compatibility from a successful copy or list command.
State the platforms and hosts actually exercised; unavailable live or cross-OS
checks remain limitations.
