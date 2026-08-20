# Architecture Decision Records (ADRs)

This directory records **significant** technical and design decisions for LifeSync.

ADRs implement the “Significant changes” path in [GOVERNANCE.md](../../GOVERNANCE.md): architecture, data model, privacy model, security-sensitive design, and other durable choices must be proposed, reviewed, and accepted (or rejected) transparently.

## Rules

1. **Do not treat a decision as established until an ADR is Accepted** by a maintainer (status field updated and recorded in git history).
2. ADRs must obey [SECURITY_INTEGRITY.md](../../SECURITY_INTEGRITY.md): no fake claims; uncertainties labeled UNKNOWN / NOT VERIFIED; security/privacy impact discussed honestly.
3. Phase 1 required decisions are tracked in [PHASE1_DECISIONS.md](../PHASE1_DECISIONS.md). Each required decision should eventually link to one or more ADRs.
4. Product implementation that depends on an Unresolved or merely Proposed decision **must not** proceed as if the decision were settled.
5. Superseded ADRs remain in the tree with status Superseded and a pointer to the replacement.

## Status values

| Status | Meaning |
|--------|---------|
| **Proposed** | Draft under discussion; not binding |
| **Accepted** | Maintainer-approved; binding until superseded |
| **Rejected** | Explicitly not adopted; rationale recorded |
| **Superseded** | Replaced by a later ADR |
| **Deprecated** | No longer recommended but not fully replaced |

## Process

1. Copy `template.md` to `NNNN-short-title.md` (sequential number, zero-padded).
2. Fill in Context, Decision drivers, Considered options, Proposal, Consequences, Security & privacy notes, and Evidence required.
3. Open a PR or design discussion. Do not mark Status: Accepted yourself unless you are a maintainer acting under governance.
4. Maintainer reviews against principles (especially privacy-first) and SECURITY_INTEGRITY.md.
5. On acceptance: set Status to Accepted, date, and approver; update `docs/PHASE1_DECISIONS.md` if applicable.
6. Only after Acceptance may dependent implementation begin.

## Naming

`NNNN-short-hyphenated-title.md` — e.g. `0001-technology-stack.md`

## Index

| ADR | Title | Status |
|-----|-------|--------|
| [0001](0001-threat-model.md) | Foundation Threat Model (D6) | Proposed |
| [0002](0002-privacy-data-handling-model.md) | Privacy and Data-Handling Model (D7) | Proposed |
