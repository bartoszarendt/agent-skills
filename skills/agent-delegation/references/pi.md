# Pi

Commands run from the workspace. `$RUN` is the run directory outside it.
Confirm option names with `pi --help` when the installed version differs.
Documentation: [JSON mode](https://github.com/earendil-works/pi/blob/main/packages/coding-agent/docs/json.md),
[security](https://github.com/earendil-works/pi/blob/main/packages/coding-agent/docs/security.md);
the installed package also contains these files under `docs/`.

## Preflight

```sh
command -v pi
pi --version
pi --list-models
```

Authentication uses `/login` in an interactive session or a provider API-key
environment variable. Confirm the intended model appears in `--list-models`.

## Instructions and configuration

Pi loads `AGENTS.md` or `CLAUDE.md` context files from its global directory, the
workspace, and parent directories; `AGENTS.override.md` replaces them within a
directory. `--no-context-files` disables that loading.

Project resources in `.pi/` and project `.agents/skills` require project trust.
Non-interactive runs show no trust prompt and follow the saved or default trust
decision. Pass `--no-approve` so project resources stay unloaded, or `--approve`
only when the user trusts the repository and wants those resources. Project trust
controls what loads; it does not restrict what tools do. User-level skills and
extensions load regardless of project trust. `--no-skills` and `--no-extensions`
exclude them when the task needs a controlled environment.

## Model

`--provider <name>` and `--model <pattern>` select the model; the model value
accepts `provider/id` and an optional `:<thinking>` suffix. `--thinking <level>`
sets reasoning effort. Without them, Pi uses its configured default.

## Read-only run

```sh
pi --mode json --no-approve --tools read,grep,find,ls \
  < "$RUN/brief.md" > "$RUN/events.jsonl" 2> "$RUN/stderr.txt"
echo $? > "$RUN/exit.txt"
```

The allowlist applies to built-in, extension, and custom tools, but extension code
still loads and runs with the user's permissions. Add `--no-extensions` when the
task needs no extensions.

## Write run

```sh
pi --mode json --no-approve \
  < "$RUN/brief.md" > "$RUN/events.jsonl" 2> "$RUN/stderr.txt"
echo $? > "$RUN/exit.txt"
```

The default tools read, write, edit, and run shell commands without prompts.
Nothing confines them to the workspace.

## Output

`--mode json` writes JSONL events.

- The first line is the session header, `{"type":"session","id":...}`; `id` is
  the identifier for resuming.
- `message_end` events whose `message.role` is `assistant` carry text parts in
  `message.content` and a `stopReason`. The report is the text of the last
  assistant message.
- A `stopReason` of `error` or `aborted` is a failure even when the exit status is 0.
- `agent_end` marks the end of a run attempt, including failed and aborted
  attempts. Its `willRetry` field shows whether another attempt follows.

Success requires exit status 0, a final `agent_end` with `willRetry: false`, and
a last assistant `stopReason` of `stop`. A run without `agent_end` did not
finish; after a forced termination on Windows, the npm launcher has exited with
status 0, so rely on the recorded cancellation and the missing events.

## Resume

Repeat the original tool, trust, and model options. For a read-only session:

```sh
pi --mode json --no-approve --tools read,grep,find,ls --session "<id>" \
  < "$RUN/followup.md" > "$RUN/events-2.jsonl" 2> "$RUN/stderr-2.txt"
echo $? > "$RUN/exit-2.txt"
```

For a write session, omit `--tools` as in the write run. `--continue` resumes
the most recent session for the directory and can create a new session
identifier; record the identifier from the new header. `--no-session` stores
nothing and prevents resumption.

## Cancellation

Interrupt the process first (Ctrl+C or SIGINT), then stop its process tree if
it does not exit. Inspect the workspace before resuming.

## Boundary

Pi has no sandbox and no permission modes. A write run, its shell commands, and
its extensions act with the full permissions of the user account.

- For ordinary authorized work in a trusted local repository, the direct write
  run is appropriate. Tell the user that writes are not confined, and rely on
  the starting-state comparison and review.
- When the task requires enforced isolation, such as an untrusted repository,
  unmonitored work near sensitive credentials, or a requirement that nothing
  outside the workspace changes, run Pi inside a container, VM, or other
  operating-system boundary that exposes only the required files and
  credentials. A worktree does not provide that isolation.

## Failure signs

- `Model "<x>" not found` or provider authentication errors in stderr: correct
  the model or credentials; do not substitute another provider.
- `stopReason` `error` or `aborted`: treat the run as failed and inspect the events.
- Changes after a read-only run: an extension or other code path wrote them;
  report the changes.
