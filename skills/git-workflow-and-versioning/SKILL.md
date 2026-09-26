---
name: git-workflow-and-versioning
description: Prepare commits, branches, pull requests, versions, and releases using repository conventions while preserving user work. Use when the requested task includes Git history, integration, versioning, or release actions.
---

# Git Workflow and Versioning

Keep changes reviewable and preserve work that belongs to others. Follow the
repository's established workflow and the user's authorization.

## Inspect state and conventions

Check the current branch, working tree, index, remotes, and any operation already
in progress. Distinguish task changes from unrelated modifications.

Read relevant history, contribution instructions, templates, hooks, release
configuration, and generated-file ownership. Do not assume the default branch,
commit format, version source, or changelog process.

Use a simple conventional format only when the repository has none and the task
needs one. Do not introduce a branching model or release tool as a side effect.

## Establish authorization

Commit or push only when explicitly requested or necessarily implied by the
requested outcome, such as creating or updating a pull request. Authorization
applies to the named task and destination; do not extend it to unrelated work.

Check exact targets before operations that discard changes, delete branches,
rewrite history, or move tags. Require authorization covering the effect even
for local unpushed commits. A backup can reduce risk but does not grant permission.

Do not repeatedly ask for an action already authorized. When the requested
integration destination is unresolved, investigate the branch configuration and
history before asking.

## Prepare coherent commits

Group changes by a reviewable reason to change. Necessary restructuring can
belong with a behavior change; separate independent cleanup, upgrades, and
formatting when that improves review or rollback.

Stage deliberately by file or hunk. Read the full staged diff and check for
unrelated changes, secrets, unintended generated files, and local configuration.
Do not stage or alter unrelated user work.

Use project tooling for generated artifacts and package managers for lockfiles.
Include generated files when the repository's release or ownership rules require
them, including new artifacts that the task intentionally introduces.

Run relevant checks and required hooks against the candidate being committed.
Do not claim a staged subset is verified merely because the larger working tree
passed; inspect or isolate it when the difference could affect behavior.

Write a subject that states the change, with a body explaining the problem,
reason, and material constraints when useful. Scale the message to complexity.

## Preserve hooks and history

Do not bypass hooks, disable signing, or weaken checks without explicit
authorization. Diagnose a failure before retrying. Inspect whether a commit
exists before choosing amend; a failed pre-commit hook does not create one.

A rejected push requires investigation of the remote state. Do not force past it.
Prefer an additive revert for shared history. Force-pushing or rewriting shared
history requires explicit authorization covering that operation and its effects;
use the least destructive method and verify the remote state immediately before it.

Treat untracked files and stashes as user work. Do not use reset, clean, restore,
stash deletion, or branch deletion merely for convenience.

## Complete the requested integration

Verify the relevant candidate and identify the correct base branch from evidence.
If the user already requested a PR or merge, carry out that authorized workflow.
Offer options only when a material choice is still unresolved.

Use the repository template for PRs. Describe the problem, resulting behavior,
verification, and material gaps. A PR request does not imply permission to merge
or deploy it.

For a merge, run relevant checks on the merged result when integration could
invalidate earlier evidence. Preserve the branch and report a failed gate.
Delete branches only when cleanup is covered by the request or established
authorized workflow; successful merging alone does not require deletion.

Keep local commits, pushed commits, opened PRs, merged changes, and deployed
releases distinct in the report.

## Version and release according to commitments

Use the project's versioning policy and release tooling. When semantic versioning
applies, classify changes by the supported public contract rather than diff size.
Investigate uncertain compatibility instead of selecting a major version solely
because evidence is missing.

Account for consumer migrations, runtime requirements, defaults, and persisted
formats. Experimental status does not erase real user or data commitments.

Write user-relevant changelog entries when the project requires them. Feed
generated changelogs through their source mechanism. Keep version files and tags
consistent with the repository's chosen source of truth.

Treat a published release as immutable unless the user explicitly authorizes a
correction with known consequences. Pushing a tag may publish artifacts; confirm
that the requested release action covers those external effects.

## Verification

- [ ] Branch, index, working tree, and relevant remote state were inspected.
- [ ] Staged and committed changes belong to the authorized task.
- [ ] Relevant checks and required hooks exercised the candidate.
- [ ] Messages, generated artifacts, and versions follow repository conventions.
- [ ] History rewrites, deletions, pushes, and releases have appropriate authorization.
- [ ] The final report distinguishes local, remote, integrated, and deployed state.
