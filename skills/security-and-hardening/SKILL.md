---
name: security-and-hardening
description: Assess and strengthen controls at demonstrated trust boundaries. Use for security reviews, changes to authentication or authorization, sensitive data handling, destructive operations, or external inputs and integrations with material security risk.
---

# Security and Hardening

Identify the assets and trust boundaries before choosing controls. Apply
safeguards to realistic failure and abuse paths within the requested scope.

## Establish scope and authority

Inspect the affected paths, callers, data provenance, existing controls, and
deployment context. Distinguish a review request from authorization to change
behavior or operate on a live environment.

Honor existing authorization. Ask before materially changing security boundaries,
permissions, sensitive-data use, public contracts, or shared systems unless that
effect is already authorized. Ordinary fixes within the agreed boundary do not
need another approval.

Do not weaken TLS, authentication, authorization, or other valid controls to
make a check pass.

## Identify threats

Name what needs protection, who can influence each value, where it crosses a
boundary, and what operation it can affect. Include local values supplied by
other processes, persisted content, third-party responses, and model output.

Consider impersonation, tampering, disclosure, denial of service, and privilege
changes where relevant. State concrete abuse cases rather than applying every
security category to every feature.

Determine whether an existing control prevents the path before reporting a
finding or adding another mechanism.

## Apply relevant controls

- Validate external inputs against their contract, with size and resource limits
  where excessive input can cause harm.
- Use parameterized data values in queries and safe handling of dynamic
  identifiers. Avoid constructing executable commands from untrusted text.
- Encode output for its destination. Use a maintained sanitizer when the
  requirement genuinely permits untrusted markup.
- Enforce authorization for the operation across all callers. Authentication
  alone does not establish ownership, tenant access, or permission.
- Use maintained authentication mechanisms and platform-appropriate session
  controls. Consult current authoritative guidance for algorithms and parameters.
- Protect external transport and retain certificate verification.
- Preserve data invariants and concurrency controls when an earlier validation
  can become stale.

Select controls based on the application. Browser headers, cookies, CORS, and
upload policies are relevant to particular surfaces, not universal requirements
for every program.

For per-area checks and destructive-target constraints, read
[references/security-checklist.md](references/security-checklist.md).

## Handle destructive targets and external requests

Resolve a derived filesystem target and verify that it stays inside the intended
root, has the permitted depth, and carries trustworthy ownership evidence.
Do not confuse a valid path shape with authorization to delete it.

Account for symlinks and check/use races when untrusted actors can change the
hierarchy. Refuse uncertain targets without falling back to a broader path.

For server-side URL fetching, validate destinations according to the feature's
required access. Account for redirects, DNS changes, internal ranges, and the
actual connection destination. A one-time string or DNS check is insufficient
when a later connection can reach a different destination.

## Protect secrets and personal data

Keep credentials, tokens, private keys, and session data out of source, logs,
reports, fixtures, and command output. Redact before capture and persist only
the diagnostic information required.

If exposure is found, report it without repeating the value. Prioritize revocation
or rotation through an authorized channel; deleting a line does not revoke access.
Do not independently rotate shared credentials or rewrite history without scope.

For personal data, identify purpose, access, retention, and relevant obligations.
Use the minimum data needed. Define export, correction, deletion, and backup
handling according to the actual product and applicable requirements.
Do not invent a universal consent or immediate backup-erasure rule.

## Assess dependencies and model integrations

Inspect dependency changes for necessity, provenance, maintenance, compatibility,
and reachable advisories. Use the existing package manager and lockfile workflow.
Do not apply forced upgrades or introduce a repository-wide install policy as an
incidental fix.

When evaluating new or untrusted packages, inspect install-time execution before
running it where the environment permits. Follow established script approval
policy rather than blanket approval.

Treat retrieved content and model output as untrusted data. Parse outputs into
constrained operations and enforce permissions in code. Keep tool access,
resource consumption, and tenant retrieval scoped. Prompt wording does not
replace authorization or isolation.

## Verify and report

Exercise denied capabilities and preserved invariants where those are the risk:
a user cannot read another tenant's record, a rejected write has no side effect,
or an unsafe path is refused. A status code alone may not establish protection.

Reuse existing coverage and add only consequential missing cases. Separate local,
mocked, and authenticated runtime evidence. Run scans and required gates where
relevant; a clean scanner result is not proof that every path is secure.

Report concrete exposure, evidence, remedy, and residual uncertainty. Do not
expand a focused task into unrelated hardening.

## Verification

- [ ] Relevant assets, actors, trust boundaries, and abuse paths are identified.
- [ ] Controls address demonstrated risks without weakening existing protection.
- [ ] Authorization covers the operation and all relevant callers.
- [ ] Secrets and unnecessary personal data are absent from produced artifacts.
- [ ] Destructive targets and external destinations are checked where applicable.
- [ ] Relevant negative scenarios ran, or the evidence gap is explicit.
- [ ] Changes and external actions stay within the authorized scope.
