# Security checklist

Select checks from the threat model and changed surface. This is a set of
prompts, not a requirement to introduce every control into every project.

## Credentials and diagnostic output

- Inspect produced artifacts and relevant diffs for credentials, tokens, private
  keys, session data, and unnecessary personal data.
- Use placeholder examples and synthetic fixtures where possible.
- Redact sensitive values before logging or capturing them.
- On exposure, report the affected credential without repeating its value and
  coordinate authorized revocation or rotation.
- Do not confuse removing a secret from a file with revoking it.

## Authentication and authorization

- Use maintained authentication mechanisms and current platform guidance.
- Check signature, expiry, issuer, audience, and scope where the token contract
  requires them.
- Apply session cookie and CSRF controls appropriate to the browser flow.
- Verify relevant logout, reset, expiry, and revocation behavior.
- Enforce ownership, role, and tenant checks at a boundary covering all callers.
- Exercise denied capabilities, including absence of data or side effects.
- Bound authentication abuse according to the workload. For multiple instances,
  confirm that enforcement has the intended aggregate behavior.

## Input and output

- Parse external values according to their actual schema and trust boundary.
- Bound sizes, numeric ranges, decompression, recursion, and expensive operations
  where untrusted inputs can exhaust resources.
- Use parameterized query values and safe allowlisting or quoting for dynamic
  identifiers that cannot be bound as values.
- Use structured process invocation where supported; also consider option
  injection and the invoked program's argument semantics.
- Encode for the output context, and sanitize permitted untrusted markup with a
  maintained mechanism.
- Validate uploads by content and allowed use, with suitable storage, size limits,
  access control, and serving behavior.

## Destructive paths

Before a delete, move, or overwrite named by data:

1. Establish the exact authorized operation and intended root.
2. Resolve and canonicalize both root and target, accounting for symlinks and
   platform path comparison.
3. Check containment and required depth. Refuse the root itself when only children
   are permitted; a string prefix is not a containment check.
4. Verify ownership evidence from a trusted source before teardown removes it.
5. Prevent an untrusted actor from swapping the target or an ancestor between
   checking and operating, using supported descriptor-based mechanisms or a
   controlled immutable hierarchy.

A marker writable by the same untrusted actor is only self-attestation. A
well-formed path or missing marker does not authorize a fallback target.
Fail closed on uncertainty and report the refusal without exposing sensitive paths.

## Server-side fetching

- Define destinations the feature actually needs.
- Restrict protocols, ports, and addresses as the threat model requires.
- Check redirects at each hop or refuse them when they are not needed.
- Ensure the address used for the connection meets the policy; a DNS precheck
  followed by another unconstrained lookup leaves a gap.
- Account for internal, loopback, link-local, and other disallowed ranges.
- Bound response size, time, and connection use.
- Do not disable TLS verification to bypass a failed fetch.

## Browser controls

Select header and origin policies for the application. Do not paste a generic
header set that breaks required embedding, scripts, or supported integrations.

Verify required CSP, transport, framing, MIME, and referrer controls in actual
responses. Assess subdomain consequences before applying broad transport policy.

Configure CORS for the intended browser consumers. Do not treat CORS as
authentication or server-side authorization.

## Data protection

Identify data purpose, classification, access, retention, and applicable legal
or contractual requirements. Seek current authoritative guidance where those
requirements are uncertain.

Check export, correction, deletion, indexes, caches, analytics, and backups
according to the actual retention and recovery model. Distinguish deletion from
the active system, scheduled expiry, and restrictions on restored data.

Assess third-party sharing and its required basis, agreements, and user controls
rather than assuming one universal consent rule.

## Dependencies

Use the project's package manager, authoritative lockfiles, and installation
policy. Inspect new or changed install scripts before executing untrusted code
where supported.

Run relevant advisory or provenance checks and assess reachable impact across
runtime, build, test, and deployment. Record meaningful deferrals and follow-up.
Do not silently force upgrades, bypass checks, or change repository-wide policy.

## Model features

- Treat retrieved documents and model output as untrusted data.
- Parse generated operations into an allowlisted contract.
- Enforce permissions in application code and constrain tool arguments.
- Keep secrets and cross-tenant information outside the model's permitted context.
- Do not treat a hidden prompt as an access-control mechanism.
- Bound consumption, recursion, and external effects.
- Preserve existing authorization and require it for additional destructive effects.
- Separate local or mocked validation from live-provider proof.

## Error handling

Give users enough information to recover without leaking sensitive internal state.
Use correlation and scoped diagnostic detail where useful. Failure of an
authorization decision should not grant access.

Preserve useful distinctions in internal errors and reports. A generic fallback
that hides invalid state is not a security fix.
