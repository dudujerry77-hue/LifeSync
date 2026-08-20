# Security, Integrity, and No-Fake-Implementation Policy

**Status:** Mandatory for all contributors and AI coding agents  
**Applies to:** Every phase, every feature, every commit, every claim about the system

LifeSync will handle highly sensitive personal information (health, finances, documents, relationships, and other continuity data). Security and implementation integrity are therefore non-negotiable.

This policy is authoritative. It does not replace SECURITY.md (vulnerability reporting) or the privacy-first principles in GOVERNANCE.md; it strengthens them and binds how work is performed and described.

---

## Core Rule

**Never fake, simulate, or falsely claim that functionality is implemented, secure, tested, integrated, or verified.**

An AI agent (and every human contributor) must never:

* Write placeholder code and present it as production functionality.
* Create fake API responses to make a feature appear functional.
* Hardcode credentials, tokens, secrets, personal data, or security decisions.
* Claim an integration works without actually testing it.
* Claim a security control exists when it is only planned.
* Mark a feature as implemented when only the UI exists.
* Mark tests as passing without actually running them.
* Silently bypass authentication, authorization, encryption, validation, or other security controls.
* Disable security mechanisms simply to make development or tests pass.
* Invent libraries, APIs, endpoints, SDK behavior, or system capabilities.
* Hide errors, failed tests, incomplete work, or known vulnerabilities.
* Replace a real implementation with a mock/stub unless it is **explicitly identified** as a mock/stub and approved for that purpose.

Violations of this core rule are treated as serious governance failures.

---

## Implementation Integrity

Every feature or capability must have a clear, honest state:

**Planned → Implemented → Tested → Verified**

- **Planned**: Described in docs, issues, or RFCs; not yet built.
- **Implemented**: Real code exists that performs the intended behavior (not a stub pretending to be complete).
- **Tested**: Automated and/or manual tests have been executed against the real implementation.
- **Verified**: Concrete evidence exists that the feature meets its requirements under the conditions claimed (see Verification Rule below).

Documentation, commit messages, PR descriptions, status checklists, and phase exit claims **must accurately reflect the real state**.  
If something cannot be implemented yet, say so. Do not create a fake implementation.  
If an external service is unavailable, do not pretend the integration works.  
If credentials, keys, infrastructure, or third-party access are required, clearly identify the dependency and do not invent or hardcode substitutes.

---

## Security-First Development

Security must be considered **before** implementation, not after a feature is finished.

For any functionality that touches sensitive data, identity, storage, network, or user control, the agent must explicitly consider at least:

* Authentication
* Authorization
* Least privilege
* Encryption (in transit and at rest where applicable)
* Secure key and secret management
* Input validation and output encoding
* Data isolation (especially multi-user or shared contexts)
* Secure storage
* Network security
* Audit logging (where appropriate and privacy-respecting)
* Privacy and data minimization
* Data deletion and retention controls
* Backup and recovery security
* Dependency and supply-chain risks
* Abuse cases and failure scenarios

**Never weaken a security control merely to make development or tests easier.**  
If a security control blocks progress, surface the conflict honestly and resolve it with maintainers rather than bypassing the control.

Significant security or privacy design choices still follow the “Significant changes” process in GOVERNANCE.md (RFC / design discussion).

---

## Verification Rule

An agent may only claim that something is **verified** when there is concrete evidence, such as:

* A successful automated test that was actually run
* A successful integration test against the real (or explicitly approved test) dependency
* A reproducible manual test with recorded steps and outcome
* A security check or review with documented results
* A build, install, or runtime verification that demonstrates the claimed behavior
* Appropriate external-service verification when an integration is claimed to work

Absence of evidence means the claim must not be made.  
The agent must report failures, incomplete work, and known limitations **honestly**.

---

## Uncertainty Rule

When the agent is uncertain, it must explicitly say:

**UNKNOWN / NOT VERIFIED**

rather than guessing or filling gaps with plausible-sounding but untrue statements.

When requirements are ambiguous **and** the ambiguity affects security, privacy, data integrity, or user safety, the agent must **stop** and resolve the ambiguity (via issue, RFC, or maintainer clarification) before implementing.

---

## Production-Readiness Rule

Do **not** describe code, a feature, or the system as production-ready unless it has actually received the testing, security review, error handling, and verification appropriate for its intended use.

“Works on my machine,” “looks complete in the UI,” or “the happy path seems fine” are not sufficient for a production-ready claim.

---

## Goal

The goal is **not** to produce the most code.  
The goal is to produce **real, secure, verifiable** functionality that protects users and accurately represents its own state.

---

## How AI Agents Must Apply This Policy

1. Read this document **before** implementing any phase work or feature.
2. Treat the Core Rule as an absolute constraint on every change and every status claim.
3. When reporting progress or completing phase exit criteria, use only states that match reality (Planned / Implemented / Tested / Verified) and attach evidence for Verified claims.
4. Prefer incomplete but honest work over complete-looking but fake work.
5. If following this policy conflicts with a request to “just make it work” or “mark it done,” follow this policy and surface the conflict to maintainers.

This policy is part of project governance. Changes to it follow the same process as other significant governance updates (see GOVERNANCE.md).
