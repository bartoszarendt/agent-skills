# Portable skill mechanics

Use these conventions for a skill distributed independently across agent hosts.
Follow stricter repository requirements where they apply.

## Identity and description

Use a lowercase hyphenated name of at most 64 characters, matching the directory.
Choose a topic name that describes the work, without a persona or persistent mode.

For this collection, frontmatter contains only `name` and `description`.
Keep the description within 1024 characters and include both capability and
applicability. Other specifications or hosts may permit more fields; those are
outside this collection's format.

Some hosts show only the start of a description in their catalog, such as its
first 500 characters, and choose a skill from that alone. Put the capability
and the main triggers first, and keep the whole description within 500
characters where you can.

Write discriminating descriptions. "Use for every coding task" attracts unrelated
work and duplicates general policy. Explain meaningful exclusions only when they
prevent likely misrouting.

## Discovery and invocation

Hosts differ in how they load descriptions and select skills. Description wording
can guide selection but cannot guarantee activation, invisibility, or a particular
context cost.

Two installed copies with one name, such as a project copy beside a user-level
one, or an old backup in a directory the host scans, leave the host's
precedence to decide which runs, and a directory that fails to load can let the
other copy win. Where behavior suggests the wrong copy, check from a fresh
session in the affected project, preferring the source path or load event the
host reports. Where a marker is needed, put it in a disposable copy, and reach
the skill through the same selection path you are diagnosing: invoking a skill
by name can pick a different copy than the host's own choice from its catalog,
and some hosts list both. If the host exposes neither a source nor a usable
marker, report which copy ran as unverified.

Express user-requested applicability in ordinary language when a procedure needs
an explicit request. Do not claim that wording enforces a host permission gate.
Describe requests, answers, confirmations, and cancellation by their meaning in
context, not by required phrases or language. Mark quoted wording as an example
rather than an exclusive trigger, and do not substitute a list of synonyms.
A loaded skill never grants additional authority for external effects.

Keep host-specific metadata and tools out of portable requirements. If an optional
capability helps, explain the fallback when the environment does not support it.

## References and independence

Keep essential guidance in `SKILL.md`, at or below the collection's 250-line limit.
Put substantial conditional detail in `references/`, one level deep.

Link each reference from the main file using a relative path and explain when
to read it. Do not require another skill, an external shared instruction file,
a router, or files outside the installed directory.

Use references for topic-specific depth, not to hide universal requirements.
Avoid duplicate explanations within the directory; preserve enough local context
for the skill to work when copied alone.

Keep origin links, collection names, and reviewed revision identifiers out of
authored guidance and descriptions. Include any license and notice files required
to travel with the installed skill. Do not put license metadata in this
collection's frontmatter.

## Checks

Validate names, descriptions, frontmatter, line budgets, links, and
required notices using the repository's checks. Inspect actual references to
other skills; ordinary use of a topic word is not a dependency.

Assess behavior separately with realistic scenarios. Structural validity cannot
prove that an instruction preserves intent, applies proportionate effort, or
respects authorization.
