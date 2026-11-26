---
name: resource-cleanup
description: Name the files, folders, worktrees, branches, databases, containers, volumes and images that work creates so they can be traced later, and remove the ones no longer needed once that work ends. Use when a task, phase or milestone finishes or stops, when asked to clean up leftovers of this or earlier sessions, when disk space runs short, or before work moves to another machine. Not for simplifying code or tidying a repository's tracked content.
---

# Resource cleanup

Work leaves things behind outside its result: scratch folders, copies,
worktrees, branches, test databases, containers, volumes, images, caches and
running processes. Each was needed once. Later nobody can tell what it was for
or whether it may go, so it stays and the machine runs out of space. Name what
you create so a later reader can trace it, remove it when its job ends, and
sweep what is left when the work closes.

## Name what you create

Before the step that creates a resource that may outlive the command, choose its
identity so that a failure part-way still leaves it traceable:

- Put files and folders under a location named after the work, such as a task
  or phase id, or a key for the run, such as the date and a short name, where
  there is no id. Inside the project's ignored scratch area that is enough; in a
  temporary directory or anywhere other projects also write, put the project's
  name in it too, never loose at the top of a shared temporary directory.
- Give worktrees, branches, databases, containers, networks and images a name
  carrying the project and that id, and a label where the tool supports one,
  such as a Docker label for the project and the task. Name volumes; an
  anonymous volume can be traced only through the container that mounts it.
- Where a tool assigns the name itself, such as a test framework's fixed
  database or a generated container name, record the exact identity it
  assigned as soon as it exists.
- When something must outlive the step that made it, such as a worktree kept
  for a later proof or an image a later check needs, add a line to one note
  file kept with the work's run output, in the same place each time: the exact
  identifier, what it is for, whether it existed before, and when it can go.
  Scratch removed in the same step needs no note.

## Remove when its job ends

Before a step, a round of work or a delegated run returns, remove what it
created that no later step needs, and stop what it started. Name each thing you
keep, with its purpose and when it can go. A failure is no exception: remove
what the failed attempt left, after saving the output that shows the failure.

## Sweep when the work closes

### Bound the sweep

The sweep covers what the project's work created, in this session or an earlier
one, on this machine, and on another only where the request or the project's
instructions name it: being able to reach a machine does not authorize cleaning
it. Other projects' resources, shared services, and caches several projects use
are outside it, even when they look idle.

When a review of the work, such as a retrospective, will read run output,
scratch or worktrees, let it finish reading first, or exclude what it reads.

### Take the inventory

First read the notes of kept items and any handoff: they say what was kept on
purpose and when it can go. Then list each kind with its size, its age and what you can tell about its origin.
Check the ones that apply:

- ignored folders in the checkout: run output, scratch, build and test output,
  copies of the candidate or of other checkouts, installed dependencies inside
  copies;
- the system temporary directory and any other scratch location the work used;
- worktrees (`git worktree list`), local branches, stashes;
- databases and schemas in local or containerized servers;
- containers, volumes, networks, images and build cache, with the labels and
  mounts that tie them to their creators;
- processes and listening ports the work started;
- backups and exports the work made.

Measure the space the inventory covers before removing anything.

### Attribute each item

Find each item's origin from its name, label or path, which container mounts a
volume, which branch a worktree has checked out, and when it was created
compared with the work's records. A name or label helps find an item; it does
not show who created it. Treat an item as the work's own only where a record, a
note or a report from the work also shows that the work created it. Mark what
existed before the work. An item you cannot attribute is unknown, not
disposable.

### Decide

- **Remove** what is attributable to finished work, unused, and can be rebuilt,
  once its planned use has ended: copies that a recorded commit or candidate
  reference recreates, such as archives, extracted trees and checkouts;
  dependencies a lockfile installs again; build and test output; stopped
  containers of finished runs with volumes holding only fixtures; caches only
  this project uses.
- **Keep** what a later step still needs, a service still in use, and the
  files a record relies on. A disposable service the work started whose job has
  ended is stopped and removed like the rest. A record citing a folder makes it discoverable; it does not
  make every file in it needed. Keep the logs, receipts and outputs that show
  what the work found, and treat copies inside a cited folder as rebuildable.
- **Ask** before deleting evidence a record relies on, data that cannot be
  rebuilt, such as a database with work in it, a worktree with uncommitted
  changes, anything unknown or that existed before the work, and anything
  shared with other projects. Ask once, listing
  each item with its size and what removing it would lose.

Removing rebuildable items of finished work belongs to an ordinary cleanup
request. A request to clean up authorizes no deletion of user data, and no
removal of another project's resources.

### Remove safely

- Select by exact identifier. Never select by a name prefix, pattern or filter
  that can match another run's or another project's resources.
- Before removing, check that nothing uses the item: no running container
  mounts the volume, no process holds the file or port, no client is connected
  to the database.
- Before deleting a folder, resolve its real path and confirm it lies inside the
  area you meant, such as the project's scratch area. Find links and junctions
  inside it and remove each link itself first: a recursive delete can follow it
  into the real target, such as an installed dependency tree or user data.
- Stop a process before removing what it holds open. Remove a clean worktree
  with `git worktree remove`, never by deleting its folder; it refuses one with
  uncommitted changes, which is kept and reported, not forced.
- Delete a branch only when it is merged or the user agrees; a stash is the
  user's unless the work created it.
- Before dropping a database, confirm the server and the database name are the
  ones you mean. Back up data that cannot be rebuilt before you remove it, when
  the user agrees to removing it.
- Never prune machine-wide, such as all unused images, volumes or build cache,
  when other projects share the machine.

### Confirm and record

List each kind again and confirm that what you removed is gone. A pattern that
missed a file leaves it in place. Measure the space again.

Report what was removed with the space it freed, and what was kept, with why
and when it can go. Write the kept items where the project keeps facts about
the machine or the next session's handoff, so the next sweep does not take the
same inventory again.

## Verification

- [ ] Resources created during the work carry its id in their names or labels, and no volume is anonymous.
- [ ] Each step removed what it created and no later step needed, and named what it kept.
- [ ] The sweep covered the project's resources from earlier sessions, and nothing of another project or a shared cache.
- [ ] A review that reads the material finished reading before anything it uses was removed.
- [ ] Every removed item was shown, beyond its name, to come from finished work, was unused, and could be rebuilt, or the user agreed to its removal.
- [ ] Only machines the request or the project's instructions named were cleaned.
- [ ] Removal used exact identifiers and resolved paths, and links inside deleted folders were removed before their containers.
- [ ] A second listing showed the removed items gone, and space was measured before and after.
- [ ] Kept items are recorded with their purpose and when they can go.
