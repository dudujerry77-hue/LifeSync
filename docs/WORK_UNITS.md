# Work Units — Incremental Execution Within a Phase

**Status:** Mandatory for all contributors and AI coding agents
**Subordinate to:** [GOVERNANCE.md](../GOVERNANCE.md), [PHASES.md](../PHASES.md), [SECURITY_INTEGRITY.md](../SECURITY_INTEGRITY.md)

This document does **not** create a new or competing phase system. Phase 0–4 in PHASES.md remain the authoritative sequence of *what the project delivers, in what order*. This document adds one layer of granularity *inside* whichever phase is active, so that an AI agent (or human contributor) always has a single, small, well-bounded piece of work to do next instead of an open-ended phase description.

## The hierarchy

```
Phase → Work Unit → Deliverable → Verification → Approval → Next Work Unit
```

- A **Phase** (PHASES.md) defines the overall objective, scope boundaries, and exit criteria for a stage of the project.
- A **Work Unit** is the smallest independently deliverable slice of work inside that phase — small enough to complete, verify, and report on in one pass.
- A **Deliverable** is the concrete artifact(s) the work unit produces (a file, an ADR, a tested module — never a description of intended future work).
- **Verification** is the evidence, gathered under [SECURITY_INTEGRITY.md](../SECURITY_INTEGRITY.md)'s Verification Rule, that the deliverable actually does what it claims.
- **Approval** is the maintainer sign-off, where the work unit requires it, before anything that depends on it may begin.
- Only then does the **Next Work Unit** become eligible.

A work unit is not optional scaffolding on top of PHASES.md — it is how PHASES.md's phase-level "work that belongs to this phase" and "dependencies" sections get executed safely one increment at a time.

## Work unit fields

Every work unit is defined with exactly these fields:

| Field | Meaning |
|---|---|
| **Objective** | What this unit accomplishes, in one or two sentences. |
| **Dependencies** | What must already be true (prior work units, Accepted ADRs, maintainer approval) before this unit may start. |
| **Allowed work** | The specific, bounded actions permitted — nothing outside this list belongs to the unit. |
| **Deliverables** | The exact artifact(s) produced. |
| **Verification requirements** | What evidence must exist before the deliverable can be called Implemented/Tested/Verified (per SECURITY_INTEGRITY.md). |
| **Exit criteria** | The checklist that must be true for the unit to be considered done. |
| **Maintainer approval required before next dependent unit?** | Yes/No, and if yes, what exactly must be Accepted/approved. |

## Dependency types

An AI agent must classify every work unit's dependency as one (or more) of these four kinds before starting it:

1. **Independent** — can proceed now; nothing else needs to happen first beyond the phase being active.
2. **Requires an Accepted decision** — blocked until a specific ADR in [docs/adr/](adr/) reaches Status: **Accepted** (tracked in [PHASE1_DECISIONS.md](PHASE1_DECISIONS.md) or the equivalent register for a later phase). A **Proposed** ADR does *not* satisfy this — Proposed means "not binding" (see docs/adr/README.md). Drafting an ADR is Independent work; treating its contents as settled before Acceptance is not.
3. **Requires a previous work unit** — blocked until an earlier work unit in the same phase reaches its exit criteria (Deliverables produced and Verified).
4. **Requires explicit maintainer approval** — blocked on a maintainer action that is not merely "accept an ADR" (e.g., confirming a phase exit, approving scope for an otherwise-ambiguous unit). This is distinct from #2 and is called out per-unit only when it applies beyond ADR acceptance.

A work unit may carry more than one dependency type at once (e.g., the vault prototype requires both previous work units *and* several Accepted decisions).

## Status vocabulary

Each work unit is tracked as: **Not started** | **In progress** | **Complete** | **Blocked** (blocked state must name what it is blocked on).

## How an AI agent determines the next eligible work unit

1. Read [PHASES.md](../PHASES.md) to confirm the current active phase.
2. Open this document and find that phase's work unit sequence below.
3. Walk the sequence in order. For each unit not yet Complete, check whether *every* listed dependency is satisfied (previous units Complete; required ADRs Accepted, not merely Proposed; any named maintainer approval given).
4. The **first** unit in the sequence whose dependencies are all satisfied and which is not yet Complete is the next eligible work unit.
5. Work only on that unit. Do not start a later unit "in parallel" even if it looks independent, unless this document explicitly marks it Independent of the units ahead of it in the list.
6. If no unit in the sequence is eligible (everything remaining is Blocked on an Accepted decision or maintainer approval that has not been given), stop and report that the phase is blocked, naming exactly what is being waited on. Do not invent the missing decision and do not skip ahead into unrelated work.
7. On completing a unit: produce the real deliverables, verify them per SECURITY_INTEGRITY.md, update this document's status table and the relevant decision register, and report exactly what was done, what was verified (with evidence), and whether the unit requires maintainer approval before anything downstream proceeds. Then stop at that boundary — do not silently continue into the next unit in the same turn unless it is Independent and was explicitly requested.

## Rules

- Never mark a work unit Complete without real deliverables and evidence satisfying SECURITY_INTEGRITY.md's Verification Rule.
- Never treat a Proposed ADR as if it were Accepted, and never Accept an ADR as an agent — only a maintainer does that.
- Never invent values for a decision that is Unresolved or merely Proposed in order to unblock a work unit.
- Never implement product functionality (e.g., the vault) merely because it is listed under a phase's "work that belongs to this phase" in PHASES.md — it must also be the current eligible work unit with its dependencies satisfied.
- When a later phase becomes ACTIVE, its maintainers/agents append that phase's work unit sequence to this document using the same fields and process below, rather than creating a separate document. Do not pre-define a later phase's work units while an earlier phase is still active, and do not begin them.

---

## Phase 1 — Core Platform Foundations: Work Unit Sequence

**Next eligible work unit: WU-1.3 — Draft ADR: Technology Stack (D1).**
WU-1.1 and WU-1.2 are Complete (ADRs drafted and Proposed). No decision has reached Accepted, so no implementation work unit (WU-1.10 onward) is eligible yet.

This sequence operationalizes the decision order already recommended in [PHASE1_DECISIONS.md](PHASE1_DECISIONS.md#decision-order-recommended): draft each required decision as an ADR, then — only after a maintainer Accepts the relevant ADR(s) — implement the corresponding piece of Phase 1 scaffolding, vault, or auth work.

### Status summary

| ID | Title | Depends on | Approval gate before dependents | Status |
|----|-------|------------|----------------------------------|--------|
| WU-1.1 | Draft ADR: Threat model (D6) | Independent | D6 Accepted | **Complete** (ADR-0001 Proposed) |
| WU-1.2 | Draft ADR: Privacy/data-handling model (D7) | Independent | D7 Accepted | **Complete** (ADR-0002 Proposed) |
| WU-1.3 | Draft ADR: Technology stack (D1) | Independent | D1 Accepted | **Not started — next eligible** |
| WU-1.4 | Draft ADR: Repository/application architecture (D2) | Recommended after WU-1.3 drafted | D2 Accepted | Not started |
| WU-1.5 | Draft ADR: Development/build environment (D9) | Recommended after WU-1.3 drafted | D9 Accepted | Not started |
| WU-1.6 | Draft ADR: Testing strategy (D8) | Recommended after WU-1.3 drafted | D8 Accepted | Not started |
| WU-1.7 | Draft ADR: Core data model (D3) | Recommended after WU-1.4 drafted | D3 Accepted | Not started |
| WU-1.8 | Draft ADR: Vault/encryption architecture (D4) | Recommended after WU-1.7 drafted; informed by WU-1.1/WU-1.2 | D4 Accepted | Not started |
| WU-1.9 | Draft ADR: Authentication/identity approach (D5) | Recommended after WU-1.1 drafted | D5 Accepted | Not started |
| WU-1.10 | Project scaffolding & dev environment | Requires D1, D2, D9 **Accepted** | Maintainer confirms scaffolding matches ADRs | Blocked (no decisions Accepted) |
| WU-1.11 | Executable testing harness | Requires D8 **Accepted**; WU-1.10 Complete | None beyond D8 Acceptance | Blocked |
| WU-1.12 | Core data model implementation | Requires D3 **Accepted**; WU-1.10 Complete | None beyond D3 Acceptance | Blocked |
| WU-1.13 | Vault/encryption prototype + tests | Requires D3, D4, D6, D7 **Accepted**; WU-1.12 Complete | Maintainer reviews prototype against threat model | Blocked |
| WU-1.14 | Auth/identity skeleton | Requires D5, D6 **Accepted**; WU-1.10 Complete | None beyond D5 Acceptance | Blocked |
| WU-1.15 | Phase 1 exit review | Requires WU-1.10–WU-1.14 Complete | Yes — maintainer declares Phase 1 exit criteria met (PHASES.md) | Blocked |

Note: "Recommended after" dependencies are sequencing guidance to reduce rework (an ADR drafted out of order is not invalid), not a hard technical block — unlike "Requires ... Accepted" dependencies, which are hard blocks. An agent should still follow the listed order when picking the next eligible unit, per the "first eligible unit in sequence" rule above.

### WU-1.1 — Draft ADR: Threat Model (D6) — Complete

- **Objective:** Produce a foundation-level threat model covering assets, adversaries, trust boundaries, and priority threats for Phase 1 vault and identity work.
- **Dependencies:** Independent.
- **Allowed work:** Research and draft only; update the D6 register row and ADR index.
- **Deliverables:** `docs/adr/0001-threat-model.md` (Status: Proposed).
- **Verification requirements:** ADR exists, follows the template sections, and is linked from PHASE1_DECISIONS.md and docs/adr/README.md.
- **Exit criteria:** All of the above are true. Met — see referenced files.
- **Maintainer approval required before next dependent unit?** Yes — D6 must reach Accepted before WU-1.13 (vault) or WU-1.14 (auth) may begin. Not yet given.

### WU-1.2 — Draft ADR: Privacy/Data-Handling Model (D7) — Complete

- **Objective:** Define what data Phase 1 may collect/store, minimization and retention/deletion intent, and the no-third-party-sharing default.
- **Dependencies:** Independent.
- **Allowed work:** Research and draft only; update the D7 register row and ADR index.
- **Deliverables:** `docs/adr/0002-privacy-data-handling-model.md` (Status: Proposed).
- **Verification requirements:** ADR exists, follows the template sections, and is linked from PHASE1_DECISIONS.md and docs/adr/README.md.
- **Exit criteria:** All of the above are true. Met — see referenced files.
- **Maintainer approval required before next dependent unit?** Yes — D7 must reach Accepted before WU-1.13 (vault) may begin. Not yet given.

### WU-1.3 — Draft ADR: Technology Stack (D1) — Next eligible

- **Objective:** Propose primary language(s), runtime, and major frameworks/libraries for the application and its tests, with security/supply-chain notes.
- **Dependencies:** Independent — Phase 1 being active is sufficient.
- **Allowed work:** Research options; write a new ADR from `docs/adr/template.md` (next sequential number); update the D1 row and summary table in PHASE1_DECISIONS.md; update the ADR index in docs/adr/README.md. No product code.
- **Deliverables:** `docs/adr/000N-technology-stack.md` (Status: Proposed); updated PHASE1_DECISIONS.md; updated docs/adr/README.md index.
- **Verification requirements:** ADR contains all template sections (Context, Decision drivers, ≥2 considered options, Proposal, Consequences, Security & privacy notes, Evidence required, Alternatives, References); files exist and cross-links resolve.
- **Exit criteria:** ADR committed as Proposed; register and index updated; no unrelated files touched.
- **Maintainer approval required before next dependent unit?** Yes — D1 must reach Accepted before WU-1.10 (scaffolding) may begin. Drafting WU-1.4 onward does not require this approval.

### WU-1.4 — Draft ADR: Repository/Application Architecture (D2)

- **Objective:** Propose the high-level layout — monorepo vs. multi-repo, module boundaries, where vault/UI live — with a privacy-boundary description.
- **Dependencies:** Recommended after WU-1.3 is drafted (architecture is easier to reason about once a candidate stack exists); not a hard technical block.
- **Allowed work:** Same as WU-1.3, scoped to D2.
- **Deliverables:** `docs/adr/000N-repo-architecture.md` (Proposed); updated PHASE1_DECISIONS.md and ADR index.
- **Verification requirements:** Same template-completeness check as WU-1.3.
- **Exit criteria:** ADR committed as Proposed; register and index updated.
- **Maintainer approval required before next dependent unit?** Yes — D2 must reach Accepted before WU-1.10 may begin.

### WU-1.5 — Draft ADR: Development/Build Environment (D9)

- **Objective:** Document how contributors and agents build, run, and test locally; toolchain versions; secret-handling convention (no secrets in git).
- **Dependencies:** Recommended after WU-1.3 is drafted.
- **Allowed work:** Same pattern as WU-1.3, scoped to D9.
- **Deliverables:** `docs/adr/000N-dev-build-environment.md` (Proposed); updated PHASE1_DECISIONS.md and ADR index.
- **Verification requirements:** Same template-completeness check as WU-1.3.
- **Exit criteria:** ADR committed as Proposed; register and index updated.
- **Maintainer approval required before next dependent unit?** Yes — D9 must reach Accepted before WU-1.10 may begin.

### WU-1.6 — Draft ADR: Testing Strategy (D8)

- **Objective:** Define how Phase 1 work is tested (unit/integration/crypto tests) and what "tests have been run" means locally and in CI, aligned with D1.
- **Dependencies:** Recommended after WU-1.3 is drafted.
- **Allowed work:** Same pattern as WU-1.3, scoped to D8.
- **Deliverables:** `docs/adr/000N-testing-strategy.md` (Proposed); updated PHASE1_DECISIONS.md and ADR index.
- **Verification requirements:** Same template-completeness check as WU-1.3.
- **Exit criteria:** ADR committed as Proposed; register and index updated.
- **Maintainer approval required before next dependent unit?** Yes — D8 must reach Accepted before WU-1.11 may begin.

### WU-1.7 — Draft ADR: Core Data Model (D3)

- **Objective:** Document entities and relationships for personal continuity data at a level sufficient for a vault prototype, with explicit non-goals and privacy classification notes.
- **Dependencies:** Recommended after WU-1.4 is drafted (data model is easier to scope with an architecture direction in hand).
- **Allowed work:** Same pattern as WU-1.3, scoped to D3.
- **Deliverables:** `docs/adr/000N-core-data-model.md` (Proposed); updated PHASE1_DECISIONS.md and ADR index.
- **Verification requirements:** Same template-completeness check as WU-1.3.
- **Exit criteria:** ADR committed as Proposed; register and index updated.
- **Maintainer approval required before next dependent unit?** Yes — D3 must reach Accepted before WU-1.12 or WU-1.13 may begin.

### WU-1.8 — Draft ADR: Vault/Encryption Architecture (D4)

- **Objective:** Propose the encryption approach, key hierarchy, what is encrypted, and client-side vs. server-side trust assumptions.
- **Dependencies:** Recommended after WU-1.7 is drafted; must be informed by the threat model (WU-1.1) and privacy model (WU-1.2) already drafted.
- **Allowed work:** Same pattern as WU-1.3, scoped to D4.
- **Deliverables:** `docs/adr/000N-vault-encryption-architecture.md` (Proposed); updated PHASE1_DECISIONS.md and ADR index.
- **Verification requirements:** Same template-completeness check as WU-1.3, plus explicit traceability to WU-1.1's threat list.
- **Exit criteria:** ADR committed as Proposed; register and index updated.
- **Maintainer approval required before next dependent unit?** Yes — D4 must reach Accepted before WU-1.13 may begin.

### WU-1.9 — Draft ADR: Authentication/Identity Approach (D5)

- **Objective:** Propose how a user is identified and authenticated in Phase 1, consistent with privacy-first principles.
- **Dependencies:** Recommended after WU-1.1 is drafted (auth design should reference the threat model).
- **Allowed work:** Same pattern as WU-1.3, scoped to D5.
- **Deliverables:** `docs/adr/000N-authentication-identity.md` (Proposed); updated PHASE1_DECISIONS.md and ADR index.
- **Verification requirements:** Same template-completeness check as WU-1.3.
- **Exit criteria:** ADR committed as Proposed; register and index updated.
- **Maintainer approval required before next dependent unit?** Yes — D5 must reach Accepted before WU-1.14 may begin.

### WU-1.10 — Project Scaffolding & Development Environment — Blocked

- **Objective:** Stand up the minimal buildable project structure and documented local dev setup matching the Accepted D1/D2/D9 ADRs.
- **Dependencies:** Requires an Accepted decision — D1, D2, and D9 must all be Accepted. None are Accepted yet, so this unit is currently **Blocked**.
- **Allowed work (once unblocked):** Create the repository/module layout and dev setup exactly as specified in the Accepted ADRs; no functionality beyond what those ADRs describe.
- **Deliverables:** Buildable scaffold; developer setup instructions a new contributor can follow.
- **Verification requirements:** A clean checkout can follow the documented steps and build successfully; repo layout matches the ADRs.
- **Exit criteria:** Scaffold builds; setup doc exists and matches D9's ADR; layout matches D2's ADR.
- **Maintainer approval required before next dependent unit?** Maintainer confirms the scaffold matches the Accepted ADRs before WU-1.11/WU-1.12/WU-1.14 begin.

### WU-1.11 — Executable Testing Harness — Blocked

- **Objective:** Stand up the test tooling described in the Accepted D8 ADR so that "tests have been run" is a real, reproducible claim.
- **Dependencies:** Requires an Accepted decision — D8 Accepted; requires a previous work unit — WU-1.10 Complete. Currently **Blocked**.
- **Allowed work (once unblocked):** Wire up the test runner/framework named in D8's ADR; no product test content beyond a smoke test proving the harness runs.
- **Deliverables:** Working test command(s) documented and runnable from a clean checkout.
- **Verification requirements:** A smoke test is actually executed and its output recorded.
- **Exit criteria:** Documented test command runs and passes on a clean checkout.
- **Maintainer approval required before next dependent unit?** No beyond D8's Acceptance already required to start.

### WU-1.12 — Core Data Model Implementation — Blocked

- **Objective:** Implement the entities/types described in the Accepted D3 ADR, with invariant tests.
- **Dependencies:** Requires an Accepted decision — D3 Accepted; requires a previous work unit — WU-1.10 Complete. Currently **Blocked**.
- **Allowed work (once unblocked):** Implement only the entities/relationships in D3's ADR; write and run invariant tests.
- **Deliverables:** Data model code/types; executed tests.
- **Verification requirements:** Tests actually run against the real implementation; results recorded.
- **Exit criteria:** Implementation matches ADR; tests pass and were executed, not merely written.
- **Maintainer approval required before next dependent unit?** No beyond D3's Acceptance already required to start.

### WU-1.13 — Vault/Encryption Prototype + Tests — Blocked

- **Objective:** Build a working (or clearly labeled prototype) encrypted vault matching the Accepted D4 ADR, consistent with the Accepted D6 threat model and D7 privacy model, over the Accepted D3 data model.
- **Dependencies:** Requires Accepted decisions — D3, D4, D6, and D7 must **all** be Accepted; requires a previous work unit — WU-1.12 Complete. This is the exact case called out by the maintainer: do not implement the vault merely because Phase 1 lists it — none of D3/D4/D6/D7 are Accepted today, so this unit is **Blocked**.
- **Allowed work (once unblocked):** Implement encryption/decryption and key handling exactly as specified in D4's ADR; no invented cryptographic primitives or trust assumptions beyond what was Accepted.
- **Deliverables:** Vault prototype code; executed encrypt/decrypt (and equivalent) tests; no hardcoded keys.
- **Verification requirements:** Tests for cryptographic and storage primitives are actually run; results recorded; no security claim made without evidence.
- **Exit criteria:** Prototype matches D4's ADR; tests executed and passing; SECURITY_INTEGRITY.md satisfied throughout.
- **Maintainer approval required before next dependent unit?** Yes — maintainer reviews the prototype against the threat model before it is treated as satisfying Phase 1's vault exit criterion.

### WU-1.14 — Auth/Identity Skeleton — Blocked

- **Objective:** Implement the identity/authentication skeleton described in the Accepted D5 ADR, consistent with the Accepted D6 threat model.
- **Dependencies:** Requires Accepted decisions — D5 and D6 must both be Accepted; requires a previous work unit — WU-1.10 Complete. Currently **Blocked**.
- **Allowed work (once unblocked):** Implement only what D5's ADR specifies; no silent auth bypass; no hardcoded secrets.
- **Deliverables:** Auth skeleton code; documentation of session/secret handling.
- **Verification requirements:** Behavior matches the ADR; no bypass paths; secrets not hardcoded (verified by inspection/tests).
- **Exit criteria:** Skeleton matches ADR; SECURITY_INTEGRITY.md satisfied.
- **Maintainer approval required before next dependent unit?** No beyond D5/D6 Acceptance already required to start.

### WU-1.15 — Phase 1 Exit Review — Blocked

- **Objective:** Confirm Phase 1's exit criteria (PHASES.md) are genuinely met and record maintainer declaration of Phase 2 activation.
- **Dependencies:** Requires a previous work unit — WU-1.10 through WU-1.14 all Complete.
- **Allowed work:** Compile evidence against PHASES.md's Phase 1 exit criteria; do not declare the phase advanced.
- **Deliverables:** A written exit-criteria evidence summary for maintainer review.
- **Verification requirements:** Every checked exit-criterion item cites concrete evidence (files, executed tests, ADR Acceptance records).
- **Exit criteria:** Maintainer reviews and declares Phase 1 complete / Phase 2 active in PHASES.md.
- **Maintainer approval required before next dependent unit?** Yes — this is the phase-advancement decision itself; only a maintainer may make it (see PHASES.md, "Phase Advancement Rules").

---

*Last updated: 2026-08-20 — initial work-unit sequence added for Phase 1; no unit beyond WU-1.1/WU-1.2 marked Complete; no decision Accepted.*
