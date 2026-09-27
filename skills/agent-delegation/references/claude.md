# Claude Code

Commands run from the workspace. `$RUN` is the run directory outside it.
Confirm option names with `claude --help` when the installed version differs.
Documentation: [programmatic use](https://code.claude.com/docs/en/headless),
[CLI reference](https://code.claude.com/docs/en/cli-reference),
[permissions](https://code.claude.com/docs/en/permissions),
[sandboxing](https://code.claude.com/docs/en/sandboxing).

## Preflight

```sh
claude --version
claude auth status
```

When launched from inside another Claude Code session, the child inherits the
`CLAUDECODE` environment variable. Recent versions start normally with it. If
the child refuses to start as a nested session, remove that variable for the
child only:

- POSIX shell: `env -u CLAUDECODE claude ...`
- PowerShell: save `$env:CLAUDECODE`, run `Remove-Item Env:CLAUDECODE`, launch
  the child, then restore the saved value.

## Instructions and configuration

Print mode loads the same context as an interactive session: `CLAUDE.md`,
settings, hooks, skills, and MCP servers. It does not read `AGENTS.md` unless a
`CLAUDE.md` imports it; copy load-bearing rules from `AGENTS.md` into the brief.

Print mode shows no workspace trust dialog. It runs hooks from the project's
`.claude/settings.json` and connects servers from its `.mcp.json` even in a
folder never trusted before. An untrusted repository therefore requires an
isolated environment, such as a container or VM.

`--bare` controls startup only: it skips `CLAUDE.md`, hooks, skills, plugins,
and MCP servers. The shell and file tools remain, so an allowed command such as
`npm test` still runs repository code with the process's permissions; `--bare`
does not replace an isolation boundary. It also never reads OAuth or keychain
credentials, so subscription logins stop working. Do not add it by default; use
it with `ANTHROPIC_API_KEY` or another non-OAuth credential when ambient
configuration must be excluded.

Options that exclude parts of the ambient configuration, and what each leaves:

- `--tools <list>` restricts which built-in tools exist; omit the agent tool to
  prevent further delegation. MCP tools are not built-in tools and remain.
- `--strict-mcp-config` without `--mcp-config` excludes configured MCP servers
  and their tools. Hooks, `CLAUDE.md`, skills, and plugins still load.
- `--disable-slash-commands` disables skills in the child.

## Permissions

Without `--permission-mode`, print mode starts in the manual mode, so pass one.

- `plan`: analysis without edits.
- `acceptEdits`: file edits in the working directories, common filesystem
  commands such as `mkdir`, `touch`, `mv`, and `cp`, and the read-only command
  set run without approval. Other shell commands and network requests need an
  allow rule.
- `--allowedTools` adds allow rules to those in settings. It is not an exclusive
  allowlist: rules from settings and the mode's own approvals still apply. Use
  `--tools` to limit which tools exist and `--disallowedTools` to deny.
- A request that nothing approves is denied in print mode. On versions that
  support it, `--permission-prompts none` also tells Claude not to retry denied
  requests.
- `bypassPermissions` (`--dangerously-skip-permissions`) requires the user's
  explicit acceptance.

Permission rules use the form `Bash(npm test *)`; the space before `*` limits
the match to that command prefix. A rule applies only to the named shell tool.
When the child has more than one shell tool, as on Windows where `Bash` and
`PowerShell` can both be present, add the same exact rule for each shell tool
it may use; a denial under one tool appears in `permission_denials`.

## Read-only run

```sh
claude -p --output-format json --permission-mode plan --tools Read,Glob,Grep \
  --strict-mcp-config \
  < "$RUN/brief.md" > "$RUN/result.json" 2> "$RUN/stderr.txt"
echo $? > "$RUN/exit.txt"
```

`--strict-mcp-config` removes configured MCP tools, some of which can write or
run code. If the task needs a specific MCP server, pass it with `--mcp-config`
instead of loading all of them. Hooks still load and can write. Compare the
workspace state after the run.

## Write run

```sh
claude -p --output-format json --permission-mode acceptEdits \
  --allowedTools "Bash(npm test *)" "Bash(npm run lint *)" \
  < "$RUN/brief.md" > "$RUN/result.json" 2> "$RUN/stderr.txt"
echo $? > "$RUN/exit.txt"
```

Replace the example rules with the brief's check commands, for each shell tool
the child may use. This run confines
file edits through permissions, but allowed shell commands run with the user's
permissions.

When shell containment is required on macOS, Linux, or WSL2, enable the shell
sandbox through a settings file, for example `$RUN/settings.json` containing
`{"sandbox": {"enabled": true, "failIfUnavailable": true, "allowUnsandboxedCommands": false}}`,
passed as `--settings "$RUN/settings.json"`. `failIfUnavailable` stops the run
instead of falling back to unsandboxed commands, and `allowUnsandboxedCommands`
prevents retrying a blocked command outside the sandbox. Sandboxed commands then
run without allow rules by default.

These settings merge with the user, project, local, and managed settings, which
can defeat the intended boundary. Before relying on the sandbox for required
containment, inspect the effective configuration and confirm that:

- `sandbox.excludedCommands` lists no command the task may run, because
  excluded commands run outside the sandbox;
- `sandbox.filesystem.disabled` is not `true`, because that removes filesystem
  isolation;
- merged `sandbox.filesystem.allowWrite` paths and additional directories stay
  within the task's boundary, because filesystem arrays combine across scopes;
- network settings match what the task is allowed to reach.

If the effective configuration cannot be established or does not meet the
boundary, use a container or VM instead. See the sandboxing documentation for
filesystem and network options. Native Windows has no Claude shell sandbox; use
WSL2, a container, or a VM there.

Limits: `--max-turns <n>` and `--max-budget-usd <amount>`. Model and effort:
`--model <name>` and `--effort <level>`.

## Named agent

`--agent <name>` runs the session as an agent defined in the project's
`.claude/agents/` or among the user's agents. Combine it with the read-only or
write run above, and still pass `--permission-mode`, and `--model` and
`--effort` where the project sets them, rather than relying on the agent file's
own settings in print mode. A review that must record its result in a file
needs an edit tool and `acceptEdits`, with the brief limiting writes to that
file; compare the workspace after the run.

## Output

`--output-format json` writes one result object. Read:

- `result`: the final report text. Failures inside the run, such as missing
  authentication, also appear here, with a non-zero exit status.
- `session_id`: the identifier for resuming.
- `is_error` and `subtype`: success requires exit status 0, `is_error: false`,
  and `subtype: "success"`; `error_*` subtypes indicate limits or execution
  failure. A result object can describe a failure, so its presence alone is not
  success.
- `num_turns`, `total_cost_usd`, `usage`: run metadata; cost is an estimate.
- `permission_denials`, when present: requests the run was refused.

For progress monitoring, use `--output-format stream-json --verbose` and read the
final `type: "result"` line, which carries the same fields.

## Resume

Repeat the original permission and tool options. For a read-only session:

```sh
claude -p --output-format json --resume "<session_id>" \
  --permission-mode plan --tools Read,Glob,Grep --strict-mcp-config \
  < "$RUN/followup.md" > "$RUN/result-2.json" 2> "$RUN/stderr-2.txt"
echo $? > "$RUN/exit-2.txt"
```

For a write session, repeat the write run's options with `--resume` in the same
way. `--continue` resumes the most recent session; use it only when no
identifier exists. `--no-session-persistence` prevents resumption.

## Cancellation

SIGINT ends the current turn before exit. SIGTERM exits with status 143, leaves
the turn unfinished, records no result, and terminates running shell commands.
Inspect the workspace either way; a resumed session continues from the next
prompt, not the interrupted turn.

## Boundary

Permission modes and rules govern Claude's own tools; they are not an operating
system boundary. The shell sandbox covers shell commands and their child
processes; file edits remain governed by permissions. Deny rules for commands such as `git commit` can be bypassed
through scripts or aliases, so the brief's instructions and the review remain
the controls for actions a rule cannot contain.

## Failure signs

- `claude auth status` reports no login: authenticate before dispatch. If the
  delegating agent runs in its own sandbox, credential stores may be
  unreachable; check outside that sandbox before concluding the login is invalid.
- `permission_denials` lists a required check command: add a narrow allow rule
  and resume with otherwise unchanged options.
- `error_max_turns` or a budget error: resume with a narrower follow-up, or raise
  the limit if the user accepts the cost.
- Empty `result`: inspect stderr and the workspace, and require the report next time.
