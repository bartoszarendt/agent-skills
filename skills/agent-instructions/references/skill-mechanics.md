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

Write discriminating descriptions. "Use for every coding task" attracts unrelated
work and duplicates general policy. Explain meaningful exclusions only when they
prevent likely misrouting.

## Discovery and invocation

Hosts differ in how they load descriptions and select skills. Description wording
can guide selection but cannot guarantee activation, invisibility, or a particular
context cost.

Express user-requested applicability in ordinary language when a procedure needs
an explicit request. Do not claim that wording enforces a host permission gate.
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
