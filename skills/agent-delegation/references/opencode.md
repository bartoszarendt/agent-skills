# OpenCode

Commands run from the workspace. `$RUN` is the run directory outside it.
Confirm option names with `opencode run --help` when the installed version
differs; the behavior described here was checked against version 1.18.
Documentation: [CLI](https://opencode.ai/docs/cli/),
[models](https://opencode.ai/docs/models/),
[providers](https://opencode.ai/docs/providers/),
[permissions](https://opencode.ai/docs/permissions/).

## Preflight

```sh
command -v opencode
opencode --version
opencode models
```

Confirm that the selected provider is ready. Depending on the provider, that
means a stored credential listed by `opencode auth list`, an API key in the
environment, or a local provider such as Ollama that needs no credential.
Confirm that the intended model appears in `opencode models`.

## Instructions and configuration

OpenCode reads `AGENTS.md` from the project and its global configuration
directory, falling back to `CLAUDE.md` when no `AGENTS.md` exists. It also loads
`opencode.json` configuration, plugins, and configured MCP servers, whose tools
the delegate can call. `--pure` runs without external plugins.

## Model

Without `-m`, OpenCode selects the model from the `model` configuration key, then
the last used model, then an internal default. The effective model can therefore
differ between machines and sessions. Pass `-m <provider/model>` when cost,
provider, or data handling matters. Many catalog entries are metered; if the
user has not established which models are acceptable, ask.

Reasoning variants use `--variant <name>` where the installed help lists it;
some versions encode the variant in the model value instead.

## Read-only run

```sh
opencode run --format json --agent plan \
  < "$RUN/brief.md" > "$RUN/events.jsonl" 2> "$RUN/stderr.txt"
echo $? > "$RUN/exit.txt"
```

## Write run

```sh
opencode run --format json --agent build -m "<provider/model>" \
  < "$RUN/brief.md" > "$RUN/events.jsonl" 2> "$RUN/stderr.txt"
echo $? > "$RUN/exit.txt"
```

Piped input becomes the message; with a positional message as well, the piped
text is appended to it. The event stream does not echo the brief.

## Permissions

Autonomy comes from the selected agent and its permission rules, which have
three values: `allow`, `ask`, and `deny`. Built-in defaults allow most actions;
`external_directory` and `doom_loop` default to `ask`, and reading `*.env` files
is denied. User or project configuration can change any of these, so inspect it
when the boundary matters.

- Under default rules, `build` edits files and runs shell commands without prompts.
- `plan` restricts edits through permission rules; it is not a sandbox. Confirm
  the workspace is unchanged after the run.
- In a headless `run`, a request that resolves to `ask` is rejected
  automatically unless `--auto` is given. Rejections appear as failed tool calls
  or error events, not as a waiting prompt.
- `--auto` approves every request not explicitly denied. Use it only when the
  user accepts that. Never combine it with `plan`, because it would approve the
  requests that keep that agent read-only.

## Named agent

`--agent <name>` also selects an agent defined in the project's
`.opencode/agents/` or in the global configuration, instead of `plan` or
`build`. Its permission rules are merged with the global configuration, and the
agent's rules take precedence, so a named agent is read-only only when the
merged rules deny edits: inspect the effective permissions before relying on a
read-only run, and compare the workspace after it. Pass `-m` and `--variant`
where the project sets them.
A reasoning effort set in the agent file has no command-line option and applies
through the agent.

## Output

`--format json` writes JSONL events of the types `text`, `reasoning`,
`tool_use`, `step_start`, `step_finish`, and `error`. Every event carries
`sessionID`, the identifier for resuming.

- Assistant text arrives in `text` events at `part.text`. The same `part.id` can
  repeat with updated text; keep the latest text per part. The report is the
  assistant text at the end of the run.
- `tool_use` events record tool calls and their outcomes; a failed call carries
  its error in `part.state.error`. Rejected permission requests are one cause
  among others.
- `step_finish` events carry `part.reason` and, when the provider reports it,
  `part.cost`. Intermediate steps end with `tool-calls`; a finished run ends
  with a final `step_finish` whose `part.reason` is `stop`.
- `error` events, stderr, and the exit status report failures.

Success requires exit status 0, a final `step_finish` with reason `stop`, and no
unresolved `error` events or failed tool calls that affect the task. After a
forced termination on Windows, the npm launcher has exited with status 0; the
missing `stop` step and the recorded cancellation show the run is incomplete.

The final text can be empty when a run ends in tool calls. Inspect the workspace
and require the report in the next brief.

## Resume

Repeat the original agent and any model or permission options. For a read-only
session:

```sh
opencode run --format json --session "<sessionID>" --agent plan \
  < "$RUN/followup.md" > "$RUN/events-2.jsonl" 2> "$RUN/stderr-2.txt"
echo $? > "$RUN/exit-2.txt"
```

For a write session, use `--agent build` in the same position. The agent is
selected per prompt, so omitting it can change the permissions. A resumed
session keeps its model unless `-m` is given. `--continue` resumes the most
recent session; use it only when no identifier exists. `--fork` branches from
an existing session instead of extending it.

## Cancellation

Interrupt the process first (Ctrl+C or SIGINT), then stop its process tree if
it does not exit. Inspect the workspace before resuming.

## Failure signs

- Unknown model or unready provider: correct it or ask; do not substitute
  another provider.
- Failed `tool_use` events: read `part.state.error` and the tool's input first.
  Tool failures also come from missing files, invalid inputs, and command
  errors. Adjust permission configuration, within the user's authorization,
  only when the error shows a rejected or denied permission request.
- No new events for a long time: check whether a long command, the provider, or
  the network is responsible before stopping the run; do not assume the cause.
- Edits after a `plan` run: the effective permission rules allowed them; report
  the edits and review the configuration.
