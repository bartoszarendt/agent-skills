# Codex

Commands run from the workspace. `$RUN` is the run directory outside it.
Confirm option names with `codex exec --help` when the installed version differs.
Documentation: [non-interactive mode](https://developers.openai.com/codex/noninteractive).

## Preflight

```sh
command -v codex
codex --version
codex login status
```

Several installations can coexist; confirm that the active binary is the
intended one.

## Instructions and configuration

Codex reads `AGENTS.md` files (and `AGENTS.override.md`) along the path to the
working directory, plus its user configuration, MCP servers, and the user's
installed skills. `--ignore-user-config` skips `config.toml` while keeping
authentication.

## Read-only run

```sh
codex exec --json -s read-only -o "$RUN/final.md" - \
  < "$RUN/brief.md" > "$RUN/events.jsonl" 2> "$RUN/stderr.txt"
echo $? > "$RUN/exit.txt"
```

`codex exec` defaults to a read-only sandbox, but configuration can change that
default; pass `-s` explicitly. Codex reads files through shell commands, so the
brief must permit read-only commands; a brief that forbids all commands leaves
it unable to perform shell-based file inspection.

The read-only sandbox blocks writes through sandboxed commands. MCP servers,
connectors, web search, and browser actions have separate controls. When the
task requires enforced no-write behavior, restrict or disable write-capable
integrations as well, for example with `--ignore-user-config` when they are
defined in the user's `config.toml`, and confirm which remain.

## Write run

```sh
codex exec --json -s workspace-write -o "$RUN/final.md" - \
  < "$RUN/brief.md" > "$RUN/events.jsonl" 2> "$RUN/stderr.txt"
echo $? > "$RUN/exit.txt"
```

The trailing `-` reads the brief from stdin. Model and effort:
`-m <model>` and `-c model_reasoning_effort=<level>`. Outside a Git repository,
add `--skip-git-repo-check`. `--add-dir <dir>` adds a writable directory and
widens the boundary.

## Output

`--json` writes JSONL events. `-o` writes the final agent message to a file.

- `thread.started` carries `thread_id`, the identifier for resuming.
- `turn.completed` marks a finished turn and carries usage.
- `turn.failed` and `error` events indicate failure.
- `item.*` events record messages, reasoning, commands, file changes, and tool
  calls; inspect them for failed or denied commands.

Success requires exit status 0, a `turn.completed` event, no `turn.failed`
event, and a non-empty final message. All four are needed: after an interrupt,
Codex can stop the running command, write a final message, and emit
`turn.completed` while exiting with status 130.

## Resume

Place `-s` before `resume`, using the original run's sandbox mode. For a
read-only session:

```sh
codex exec -s read-only resume "<thread_id>" --json -o "$RUN/final-2.md" - \
  < "$RUN/followup.md" > "$RUN/events-2.jsonl" 2> "$RUN/stderr-2.txt"
echo $? > "$RUN/exit-2.txt"
```

For a write session, use `-s workspace-write` in the same position. Without
`-s`, the resumed turn uses the active configuration. `resume --last` picks the
most recent session; use it only when no identifier exists. `--ephemeral`
stores no session files and prevents resumption.

## Cancellation

Interrupt the process first (Ctrl+C or SIGINT), then stop its process tree if
it does not exit. A cancelled run may have no `turn.completed` event; inspect
the workspace before resuming.

## Boundary

`read-only` and `workspace-write` are enforced sandboxes for commands the model
runs; they do not govern MCP servers or other integrations. `workspace-write` allows writes inside the workspace and added directories
and disables network access by default. Enable network only when the task needs
it and the user accepts it: `-c sandbox_workspace_write.network_access=true`.

`-s danger-full-access` and `--dangerously-bypass-approvals-and-sandbox` remove
the sandbox. Use them only with the user's explicit acceptance, preferably
inside an external container or VM.

Whether the sandbox can write `.git` varies by version and platform. Do not rely
on it either to prevent or to permit commits; the brief states the rule.

## Windows

On native Windows, sandboxed commands have been reported to fail with access
denied (`0xC0070005`) when the shell Codex prefers, such as `pwsh`, is installed
under a `WindowsApps` directory. Check with `(Get-Command pwsh -All).Source`. If
affected, remove `WindowsApps` entries from `PATH` for the Codex process only so
it falls back to Windows PowerShell. A delegate that cannot run commands may
still report success; check the command items in the event stream.

## Failure signs

- Authentication errors in stderr: run `codex login` before dispatching again.
- An unsupported model or effort value: correct it; do not change provider
  silently.
- Commands denied by the sandbox: widen access only with the user's acceptance,
  or run the check yourself after the delegate finishes.
- Empty final message: treat the run as failed and inspect the events.
