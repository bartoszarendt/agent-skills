---
name: domain-language
description: Define consistent domain terms and resolve conflicting meanings against project evidence. Use when naming concepts, clarifying an overloaded vocabulary, or creating or updating a project glossary.
---

# Domain Language

Make the terms used in requirements and code precise enough to support consistent
decisions. Record domain meanings without turning the glossary into a design
specification.

## Find the existing vocabulary

Inspect relevant specifications, documentation, interfaces, and code. Use the
project's established glossary or vocabulary source before creating another.

Identify the context in which a term has meaning. The same word may legitimately
mean different things in separate domains. Do not infer domain boundaries from
filenames or the presence of a particular context-map document.

## Resolve ambiguity

When terms conflict, show the competing meanings and the consequence of choosing
one. Check discoverable facts before asking the user.

Propose a canonical term when evidence supports it. Use concrete scenarios to
test distinctions: partial shipment, canceled subscription, outstanding invoice,
or another relevant lifecycle transition.

Distinguish current implementation from intended behavior. If the code disagrees
with the user's proposal, establish whether that difference is the requested
change. Do not automatically treat the implementation as the desired contract.

Make routine terminology choices within the task independently. Ask before
renaming a public contract or changing a meaning that affects persisted data,
business rules, or another material commitment.

## Record settled meanings

Within authorized documentation work, update the existing glossary when a term
is resolved. If none exists and a glossary is useful, propose or use a small
document in the project's documentation location.

Define each concept in a sentence or two. Include disallowed synonyms only when
they prevent demonstrated confusion. Keep terms specific to the domain;
general programming vocabulary usually needs no glossary entry.

For a lightweight format and optional context map, see
[references/context-format.md](references/context-format.md).

A request to discuss or analyze terms does not automatically authorize file
creation, symbol renames, or behavior changes. Deliver proposed definitions when
that is the scope.

## Handle decisions separately

If terminology exposes a consequential ownership or architecture decision,
record its rationale in the existing decision source when the task authorizes it.
Use a separate decision record only when lasting consequences or project rules
justify one.

Keep definitions, implementation proposals, and approved decisions distinct.
Do not create a second decision-log convention inside the glossary.

## Verification

- [ ] Terms reflect the relevant domain and actual or explicitly proposed behavior.
- [ ] Conflicting meanings and their consequences were resolved or named.
- [ ] The existing vocabulary source was reused where available.
- [ ] Definitions are concise and avoid unnecessary implementation detail.
- [ ] Public renames and semantic changes stayed within authorization.
