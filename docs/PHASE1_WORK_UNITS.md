# Phase 1 Work Units

**Phase:** 1 — Core Platform Foundations (**ACTIVE**)
**Execution rules:** [WORK_UNITS.md](WORK_UNITS.md)
**Decisions:** [PHASE1_DECISIONS.md](PHASE1_DECISIONS.md)
**Integrity:** [SECURITY_INTEGRITY.md](../SECURITY_INTEGRITY.md)

This catalog **does not change** Phase 1 objectives or exit criteria in [PHASES.md](../PHASES.md). It sequences Phase 1 into small units.

**Current / next agent unit:** **P1-WU03** — Propose technology stack (D1)

P1-WU01 and P1-WU02 ADRs are **Proposed** (waiting for maintainer Accept). Those units are not Complete until Accepted. WU03 does not have a *hard* dependency on Accept, so it is the next eligible unit.

---

## Sequence overview

```
P1-WU01 D6 threat model ADR (propose → wait Accept)
P1-WU02 D7 privacy model ADR (propose → wait Accept)
P1-WU03 D1 technology stack ADR
P1-WU04 D2 repository/application architecture ADR
P1-WU05 D9 development/build environment ADR
P1-WU06 D8 testing strategy ADR
P1-WU07 D3 core data model ADR
P1-WU08 D4 vault/encryption architecture ADR
P1-WU09 D5 authentication/identity ADR
P1-WU10 Scaffolding          [hard: D1, D2, D9 Approved]
P1-WU11 Vault prototype      [hard: D3, D4, D6, D7 Approved + WU10]
P1-WU12 Auth skeleton        [hard: D5, D6 Approved + WU10]
P1-WU13 Phase 1 closeout     [hard: WU10–WU12 + remaining Phase 1 exit criteria]
```

WU11 and WU12 are independent of each other once their own hard dependencies are met. Neither may start Phase 2 workflows.

| ID | Name | Status |
|----|------|--------|
| P1-WU01 | Propose threat model (D6) | **Waiting for maintainer** (ADR-0001 Proposed) |
| P1-WU02 | Propose privacy/data-handling model (D7) | **Waiting for maintainer** (ADR-0002 Proposed) |
| P1-WU03 | Propose technology stack (D1) | **Ready** (next) |
| P1-WU04 | Propose application architecture (D2) | Not started |
| P1-WU05 | Propose dev/build environment (D9) | Not started |
| P1-WU06 | Propose testing strategy (D8) | Not started |
| P1-WU07 | Propose core data model (D3) | Not started |
| P1-WU08 | Propose vault/encryption architecture (D4) | Not started |
| P1-WU09 | Propose authentication/identity (D5) | Not started |
| P1-WU10 | Application scaffolding | Blocked (needs D1, D2, D9 Approved) |
| P1-WU11 | Encrypted vault prototype | Blocked |
| P1-WU12 | Auth/identity skeleton | Blocked |
| P1-WU13 | Phase 1 verification closeout | Blocked |

---

## P1-WU01 — Propose threat model (D6)

**Objective:** Record a foundation threat model so later design is security-first.

**Inputs / dependencies:**
- Hard: Phase 1 active; ADR process exists
- Informed-by: project vision, SECURITY_INTEGRITY.md

**Allowed work:** Draft/refine ADR for D6; update decision register to Proposed.
**Not allowed:** Mark ADR Accepted; implement product code; choose crypto libraries.

**Deliverables:** ADR in `docs/adr/` (Proposed); register D6 → Proposed.

**Verification:** ADR covers assets, actors, boundaries, attack surfaces, abuse, recovery, metadata, AI access; no fake Verified security claims; status is Proposed.

**Exit criteria:**
- [x] ADR-0001 exists as Proposed
- [ ] Maintainer Accepts ADR-0001 (then D6 = Approved; this unit Complete)

**Current status:** Waiting for maintainer.

---

## P1-WU02 — Propose privacy / data-handling model (D7)

**Objective:** Operationalize privacy-first data handling before storing personal data.

**Inputs / dependencies:**
- Hard: Phase 1 active
- Informed-by: ADR-0001 (Proposed or Accepted)

**Allowed work:** Draft/refine D7 ADR; register → Proposed.
**Not allowed:** Accept the ADR; implement storage of personal data; add analytics.

**Deliverables:** ADR-0002 Proposed; D7 Proposed in register.

**Verification:** Ownership, consent, minimization, retention/deletion, export, sharing, emergency access, audit, AI access are addressed; unknowns labeled; status Proposed.

**Exit criteria:**
- [x] ADR-0002 exists as Proposed
- [ ] Maintainer Accepts ADR-0002

**Current status:** Waiting for maintainer.

---

## P1-WU03 — Propose technology stack (D1)

**Objective:** Choose language(s), runtime, and major frameworks for app and tests — as a **Proposed ADR only** until Accepted.

**Inputs / dependencies:**
- Hard: none beyond Phase 1 active
- Informed-by: D6/D7 Proposed ADRs (align with privacy/threat posture; do not pick a stack that forces third-party analytics or plaintext-by-default hosting)

**Allowed work:** Compare options; write D1 ADR (Proposed); update register.
**Not allowed:** Scaffold the repo as if the stack were Approved; add application product code; Accept the ADR.

**Deliverables:** `docs/adr/NNNN-technology-stack.md` (Proposed); D1 status Proposed.

**Verification:** Written comparison; supply-chain/security notes; no undeclared we-already-use-X-in-production; status Proposed.

**Exit criteria:**
- [ ] D1 ADR Proposed
- [ ] Maintainer Accepts ADR (D1 Approved) — required before WU10

**Current status:** Ready (next unit for the agent).

---

## P1-WU04 — Propose repository / application architecture (D2)

**Objective:** Define layout, module boundaries, and client/server/local-first shape.

**Inputs / dependencies:**
- Hard: none for *proposal*
- Informed-by: D1 (Proposed or Approved), D6, D7 (trust boundaries)

**Allowed work:** Architecture ADR (Proposed); diagrams/descriptions.
**Not allowed:** Create the application tree as if Approved; implement vault/auth/UI workflows.

**Deliverables:** D2 ADR Proposed; register updated.

**Verification:** Components and trust boundaries described; privacy boundary notes; consistent with Proposed/Accepted D6/D7.

**Exit criteria:** D2 ADR Proposed; later Accepted before WU10.

**Current status:** Not started.

---

## P1-WU05 — Propose development / build environment (D9)

**Objective:** Define how developers/agents build, run, and test; secret conventions.

**Inputs / dependencies:**
- Hard: none for proposal
- Informed-by: D1, D2 (Proposed or Approved)

**Allowed work:** D9 ADR (Proposed).
**Not allowed:** Claim a documented setup is Verified if it does not exist; commit secrets.

**Deliverables:** D9 ADR Proposed.

**Verification:** Setup steps, toolchain versions, no-secrets-in-git convention; status Proposed.

**Exit criteria:** D9 Proposed; Accepted before WU10.

**Current status:** Not started.

---

## P1-WU06 — Propose testing strategy (D8)

**Objective:** Define how Phase 1 work is tested and what “tests have been run” means.

**Inputs / dependencies:**
- Hard: none for proposal
- Informed-by: D1, D9, SECURITY_INTEGRITY.md Verification Rule, D4/D6 (crypto tests will be needed later)

**Allowed work:** D8 ADR (Proposed).
**Not allowed:** Claim tests pass without running them; implement a fake CI that always succeeds.

**Deliverables:** D8 ADR Proposed.

**Verification:** Strategy covers unit/integration/crypto evidence; tools aligned with D1 if D1 is Proposed/Approved.

**Exit criteria:** D8 Proposed; Accepted before treating WU11/WU12 tests as governed strategy (tests may still be required by SECURITY_INTEGRITY.md regardless).

**Current status:** Not started.

---

## P1-WU07 — Propose core data model (D3)

**Objective:** Document continuity entities and relationships sufficient for a vault prototype.

**Inputs / dependencies:**
- Hard: none for proposal
- Informed-by: **D6 and D7** (strongly recommended Accepted; if still Proposed, ADR must not contradict them)

**Allowed work:** D3 ADR (Proposed).
**Not allowed:** Implement a schema in code before D3 Approved; invent Phase 2 workflow entities as if in scope for product features.

**Deliverables:** D3 ADR Proposed (entities, relationships, non-goals, privacy classification).

**Verification:** Aligns with D7 minimization; metadata classified per D6; status Proposed.

**Exit criteria:** D3 Proposed; Accepted before WU11.

**Current status:** Not started.

---

## P1-WU08 — Propose vault / encryption architecture (D4)

**Objective:** Design how data is protected at rest/in transit and key/trust assumptions — without necessarily selecting libraries unless evidence requires it.

**Inputs / dependencies:**
- Hard: none for proposal
- Informed-by: **D6, D7** (should be Accepted before implementation; proposals should map to ADR-0001 threats); D3; D2

**Allowed work:** D4 ADR (Proposed).
**Not allowed:** Implement crypto; hardcoded keys; claim encryption is Verified.

**Deliverables:** D4 ADR Proposed (key hierarchy, what is encrypted, trust boundaries, limitations).

**Verification:** Mapped to D6 priority threats; limitations labeled; no fake algorithm claims.

**Exit criteria:** D4 Proposed; Accepted before WU11.

**Current status:** Not started.

---

## P1-WU09 — Propose authentication / identity approach (D5)

**Objective:** Choose how a user is identified/authenticated for Phase 1, privacy-first.

**Inputs / dependencies:**
- Hard: none for proposal
- Informed-by: D6, D7, D2, D4

**Allowed work:** D5 ADR (Proposed).
**Not allowed:** Implement login/session code before D5 Approved; bypass auth for convenience.

**Deliverables:** D5 ADR Proposed (approach, session/secret handling, out-of-scope).

**Verification:** Recovery treated as an attack path (D6); no silent bypass design; status Proposed.

**Exit criteria:** D5 Proposed; Accepted before WU12.

**Current status:** Not started.

---

## P1-WU10 — Application scaffolding

**Objective:** Create the real project skeleton matching Approved D1, D2, D9.

**Inputs / dependencies:**
- **Hard:** D1, D2, D9 **Approved**; WU03–WU05 Complete (Accepted ADRs)
- Informed-by: D8 if Approved

**Allowed work:** Repo layout, toolchain files, documented install/build/test commands, minimal CI scaffolding if specified by D9/D8.
**Not allowed:** Vault prototype, auth product behavior, Phase 2 UI workflows, undeclared extra stack.

**Deliverables:** Scaffold matching ADRs; contributor can follow setup docs.

**Verification:** Fresh documented setup works (build/test commands actually run); layout matches D2; no secrets in git.

**Exit criteria:** Scaffolding exists; setup instructions verified; matches Approved ADRs.

**Current status:** Blocked.

---

## P1-WU11 — Encrypted vault prototype

**Objective:** Working (or clearly prototyped) privacy-preserving vault with **real** primitives and **run** tests.

**Inputs / dependencies:**
- **Hard:** D3, D4, D6, D7 **Approved**; P1-WU10 Complete
- Informed-by: D8 Approved if present

**Allowed work:** Vault/storage prototype per D4; tests for stated primitives; docs of limitations.
**Not allowed:** Fake encryption; UI-only vault; Phase 2 workflows; integrations; claiming production-ready.

**Deliverables:** Prototype + executed tests + honest status.

**Verification:** Tests actually run; no hardcoded keys; behavior matches D4; controls traceable to D6; data categories match D7.

**Exit criteria:** Prototype + executed tests; no known fake security claims.

**Current status:** Blocked.

---

## P1-WU12 — Auth / identity skeleton

**Objective:** Identity/auth skeleton consistent with Approved D5 and D6.

**Inputs / dependencies:**
- **Hard:** D5, D6 **Approved**; P1-WU10 Complete
- Independent of WU11 except both need scaffolding

**Allowed work:** Auth skeleton per D5; tests that were run.
**Not allowed:** Silent auth bypass; hardcoded credentials; Phase 2/3/4 sharing as a product feature.

**Deliverables:** Skeleton + executed tests + docs of what is *not* implemented.

**Verification:** Matches D5; no bypass; secrets not in git; tests run.

**Exit criteria:** Skeleton in place and tested as claimed.

**Current status:** Blocked.

---

## P1-WU13 — Phase 1 verification closeout

**Objective:** Confirm Phase 1 exit criteria in PHASES.md with evidence; **do not** declare the next phase active.

**Inputs / dependencies:**
- **Hard:** WU10, WU11, WU12 Complete; remaining D1–D9 Approved or maintainer-Deferred

**Allowed work:** Traceability notes, honest checklist, request maintainer phase-exit review.
**Not allowed:** Agent advancing to Phase 2; filling checkboxes without evidence.

**Deliverables:** Closeout report mapping PHASES.md exit criteria to evidence.

**Verification:** Every exit box is true with evidence or explicitly unmet; SECURITY_INTEGRITY.md holds.

**Exit criteria:** Maintainer confirms Phase 1 exit (recorded in PHASES.md). Agent only reports readiness.

**Current status:** Blocked.

---

## After completing a unit — required report shape

1. Work unit ID and new status
2. Deliverables (paths)
3. Verification performed (commands/reviews, honest)
4. Decision statuses touched (still Proposed vs Approved)
5. Blockers / maintainer actions
6. Next eligible work unit (or Blocked + why)
7. Confirmation: no later-phase features; no fake implementations
