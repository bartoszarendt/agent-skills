# Session evidence

Use this when a review's evidence includes agent session transcripts or
delegated runs, or when it compares agent work across sessions, models, or
hosts. A review of the current session alone needs only the main file.

## Inventory before reading

Before reading in depth or dividing substantial work, list the sessions and
delegated runs within the review's scope: each one's time span, model, the
user's turns, and the work it delegated. Separate a main session from the runs
it started, and a child's copy of its parent's history from what the child did.
Count as the user's turns only what the user wrote: hosts and extensions put
other text in the user role, such as wake or progress notices, injected skill
or instruction content, hook output, and briefs or relays another agent or a
supervisor wrote. Label those by their source.
When the problem spans several sessions, the review covers each of them, not
only the newest file. Place events with the user's turns, record changes, and
commit history by time window.

Where it could explain the outcome, check the instructions and configuration in
force for a run: which guidance it actually loaded, machine-local overrides of
tracked settings, and the host and tool versions.

## Read what decided the outcome

When a transcript is too large to read through a tool's output limit, convert it
into readable text in a temporary location outside the repository: the user's
turns, assistant messages, tool calls with their arguments, results, and
completion events. A file you can page through keeps material that limit would
cut. Extracted text can hold secrets
and personal data; keep it out of reports and saved findings.

Use summaries, keyword matches, and message prefixes to find events, then read
in full the user's turns and the stretches around each decision, stop, step
back, review, pause, and handoff that bears on the outcome. Choose a decision's
stretch by time, from the result it acted on to the next assignment, and read
every message, reasoning block, and brief in it. A keyword filter drawn from the
proposal or explanation under test finds only what that explanation predicts.
Copy a remote transcript locally before reading it.

A coordinating session's transcript shows what it asked for and passed on. What
a delegate saw, recommended, and found is in that delegate's own transcript or
output. For each step back, review, or stop the outcome turns on, compare the
delegate's own output with what the coordinator relayed, recorded, and handed
off, and with the assignment that followed. Where the delegate's copy of its
brief is redacted or summarized, read the brief from the call that started it.

## Trace causes

Trace each constraint the work kept to whoever set it: the user's own words, an
approved decision, or an option or mechanism an agent drafted. A source label
dropped when a criterion was copied into another record is a finding.

When a run that succeeded exists for the same work, read it first and list what
it did differently. For each difference, find whether the other run considered
it and what became of it.

Check what the agents could do before judging what they chose: each run's
effective model, the tools a delegate actually had, and its run limit. State a
capability finding for the version and configuration checked; another
configuration of the same tool can behave differently.

## Divide and verify

Divide substantial reading after the inventory. Give each helper the known
sources and starting points, and let it follow further references within the
review's scope. Give it neutral, numbered questions, the competing explanations to test, and the evidence format to cite,
such as session, timestamp, record, and commit. Ask for its full findings in a
file and a bounded summary that marks observed and inferred claims.

Before a conclusion or recommendation rests on a helper's claim, read the source
it cites.

## Host notes

Session layouts change between versions; confirm one from an actual file before
relying on it. Where no note matches, find the session store from the host's
documentation or by listing recently modified session files.

- **Claude Code:** sessions are `<session id>.jsonl` under
  `~/.claude/projects/<project path with separators replaced>/`. Subagent runs
  are in `<session id>/subagents/`, and entries marked `isSidechain` belong to a
  subagent. Large tool results may be stored under `<session id>/tool-results/`.
- **Codex:** sessions are `rollout-<local start time>-<thread id>.jsonl` under
  `~/.codex/sessions/<year>/<month>/<day>/`; timestamps inside are UTC. A
  subagent is a separate rollout whose first line names its parent thread. A
  full-history fork begins with a copy of the parent's items, so start from the
  subagent's own turn. Spawn and message payloads may be encrypted while final
  answers are plain text. When a brief is unavailable or encrypted, report its
  scope as unknown, describe the observed actions separately, and label any
  inference about the assignment.
- **OpenCode:** sessions are kept in a local database rather than per-session
  files; check the installed version's help first. In version 2.2.5,
  `opencode session list --max-count 20 --format json` lists top-level sessions
  in the current project, `opencode session export <session id>` exports one as
  JSON, and `opencode debug paths` shows the database location. Child sessions
  do not appear in that list; find them through each session's parent link in
  the database, read-only.
- **Pi with the pi-subagents extension:** main sessions are under
  `~/.pi/agent/sessions/<project directory>/`. A child run's own session is
  `<main session file name without .jsonl>/<run id>/run-0/session.jsonl` in that
  directory, and
  `subagent-artifacts/<run id>_<agent>_*` holds its `meta.json` (model and
  usage) and `output.md` (its result). Briefs in those files may be redacted;
  read them from the coordinator's subagent tool calls. Directory names that
  begin with `-` need a `./` prefix in shell commands.
