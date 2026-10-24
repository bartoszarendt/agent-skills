# Agent configuration

Use this when reviewing, adding, or loading configuration that an agent host
executes or trusts: hook definitions, tool server definitions, settings and
permission files, agent definitions, and environment overrides, whether a
repository, a package, or a user supplies them.

## Where it can act

For each item, establish:

- **Command execution:** what runs, when it runs, such as when a workspace
  opens, on a tool call, or at session start or end, with which arguments, and
  whether untrusted values reach a shell through interpolation.
- **Package resolution:** what a command fetches and runs, such as a package
  runner or a container image. A tag, a version range, or a latest marker can
  resolve to different code after review; treat it as unreviewed. Pin only to
  a version someone reviewed, and review it statically rather than starting it
  to see what it does.
- **Credential propagation:** which secrets reach the process through
  environment variables, headers, or files, and whether an override such as an
  API base URL or a proxy could send requests that carry them elsewhere.
- **Permission expansion:** allow lists, automatic approval of tools or
  servers, bypass modes, and broad file or network access, compared with what
  the work needs.
- **Output retention:** what it writes or sends, such as logs, transcripts,
  captured tool input and output, summaries sent to a model, or telemetry;
  where that goes, how long it stays, and what redaction applies.

## Workspaces you do not trust

When reviewing or adding a workspace you do not trust, inspect its agent
configuration before a trusted session loads it, and do not run its setup or
install steps to learn what they do. Report an item that would run on load as
a finding even when nothing has run yet.

## Report

Name each item, what it can execute, reach, or expose, and the condition under
which it does. Configuration can load in a scope you did not inspect, such as a
user-level or another host's settings; state which scopes you checked.
