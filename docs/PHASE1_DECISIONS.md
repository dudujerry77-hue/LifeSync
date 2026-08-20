# Phase 1 Decision Register

**Phase status:** ACTIVE (see [PHASES.md](../PHASES.md))  
**Purpose:** List every decision that must be made (or explicitly deferred) before Phase 1 implementation can proceed in a controlled, auditable way.

**Rules:**

- Status values for each decision: **Unresolved** | **Proposed** (ADR exists, not Accepted) | **Approved** (ADR Accepted) | **Deferred** (maintainer explicitly postponed with rationale).
- **No decision is Approved until a maintainer accepts a corresponding ADR** (or equivalent recorded governance action).
- Agents must **not** invent or assume values for Unresolved decisions.
- Agents may draft ADRs (status Proposed) for Unresolved items.
- Product implementation that depends on a decision may begin only when that decision is **Approved**.
- All claims remain subject to [SECURITY_INTEGRITY.md](../SECURITY_INTEGRITY.md).

---

## Required decisions

### D1 — Technology stack

| Field | Value |
|-------|--------|
| **Status** | Unresolved |
| **Description** | Primary language(s), runtime, major frameworks/libraries for application and tests |
| **Why required before implementation** | Scaffolding, dependencies, and CI cannot be honest without a chosen stack |
| **ADR** | *(none yet)* |
| **Required evidence for Approval** | Written comparison of options; security/supply-chain notes; maintainer Acceptance of ADR |
| **Required evidence after implementation** | Project builds with documented commands; dependency list matches ADR; no undeclared major tech |

### D2 — Repository / application architecture

| Field | Value |
|-------|--------|
| **Status** | Unresolved |
| **Description** | High-level layout: monorepo vs multi-repo, module boundaries, client/server/local-first shape, where vault and UI live |
| **Why required before implementation** | File layout and module boundaries must match an intentional structure |
| **ADR** | *(none yet)* |
| **Required evidence for Approval** | Diagram or clear description of components and boundaries; privacy boundary notes; maintainer Acceptance |
| **Required evidence after implementation** | Repo layout matches ADR; documented map of directories |

### D3 — Core data model

| Field | Value |
|-------|--------|
| **Status** | Unresolved |
| **Description** | Entities and relationships for personal continuity (what is stored conceptually: documents, events, people, health items, etc.) at a level sufficient for a vault prototype |
| **Why required before implementation** | Storage and APIs must not invent an undeclared schema |
| **ADR** | *(none yet)* |
| **Required evidence for Approval** | Documented entity list and relationships; explicit non-goals; privacy classification notes; maintainer review/Acceptance |
| **Required evidence after implementation** | Schema/docs match ADR; tests cover core entity invariants where applicable |

### D4 — Vault / encryption architecture

| Field | Value |
|-------|--------|
| **Status** | Unresolved |
| **Description** | How personal data is protected at rest (and in transit if applicable): encryption approach, key hierarchy, what is encrypted vs not, client-side vs server-side trust assumptions |
| **Why required before implementation** | Any vault prototype without an approved design risks fake or unsafe cryptography |
| **ADR** | *(none yet)* |
| **Required evidence for Approval** | Threat-relevant design description; key management approach; explicit trust boundaries; known limitations labeled honestly; maintainer Acceptance |
| **Required evidence after implementation** | Prototype matches ADR; tests for encrypt/decrypt or equivalent primitives **actually run**; no hardcoded keys; SECURITY_INTEGRITY.md satisfied |

### D5 — Authentication / identity approach

| Field | Value |
|-------|--------|
| **Status** | Unresolved |
| **Description** | How a user is identified and authenticated for Phase 1 (local-only, password, passkeys, external IdP, etc.) consistent with privacy-first preference |
| **Why required before implementation** | Auth skeleton must not invent an undeclared identity model |
| **ADR** | *(none yet)* |
| **Required evidence for Approval** | Chosen approach and rationale; session/secret handling notes; explicit out-of-scope items; maintainer Acceptance |
| **Required evidence after implementation** | Skeleton matches ADR; no silent auth bypass; secrets not hardcoded |

### D6 — Threat model

| Field | Value |
|-------|--------|
| **Status** | **Proposed** |
| **Description** | Foundation-level threat model: assets, adversaries, trust boundaries, priority threats for Phase 1 vault and identity |
| **Why required before implementation** | Security-first development requires threats to be stated before building controls |
| **ADR** | [ADR-0001](adr/0001-threat-model.md) (Status: **Proposed** — not Accepted) |
| **Required evidence for Approval** | Written threat model covering Phase 1 scope; mapped to D4/D5 controls at high level; maintainer Acceptance of ADR-0001 |
| **Required evidence after implementation** | Controls claimed in code are traceable to threats; unverified controls not claimed as Verified |

### D7 — Privacy / data-handling model

| Field | Value |
|-------|--------|
| **Status** | **Proposed** |
| **Description** | What data is collected/stored in Phase 1, minimization rules, retention/deletion intent, no third-party sharing default, user ownership statements |
| **Why required before implementation** | Privacy-first principle must be operationalized before storing personal data |
| **ADR** | [ADR-0002](adr/0002-privacy-data-handling-model.md) (Status: **Proposed** — not Accepted) |
| **Required evidence for Approval** | Written data-handling rules for Phase 1; explicit non-goals (e.g. no analytics); maintainer Acceptance of ADR-0002 |
| **Required evidence after implementation** | Implementation does not store categories outside the model; deletion path sketched or implemented as claimed |

### D8 — Testing strategy

| Field | Value |
|-------|--------|
| **Status** | Unresolved |
| **Description** | How Phase 1 work will be tested (unit/integration, crypto tests, what “tests have been run” means in CI vs local) |
| **Why required before implementation** | Verification Rule requires a real plan for evidence |
| **ADR** | *(none yet)* |
| **Required evidence for Approval** | Documented strategy; tools aligned with D1; maintainer Acceptance |
| **Required evidence after implementation** | Documented commands to run tests; at least one executed test run recorded for claimed Verified items |

### D9 — Development / build environment

| Field | Value |
|-------|--------|
| **Status** | Unresolved |
| **Description** | How developers (and agents) build, run, and test locally; toolchain versions; env var / secret conventions (no secrets in git) |
| **Why required before implementation** | Reproducible setup is required for honest verification by others |
| **ADR** | *(none yet)* |
| **Required evidence for Approval** | Documented setup steps; secret-handling convention; maintainer Acceptance |
| **Required evidence after implementation** | README or docs/dev match ADR; a clean checkout can follow setup without undocumented steps |

---

## Decision order (recommended)

This order is operationalized as a concrete, dependency-checked work unit sequence in **[docs/WORK_UNITS.md](WORK_UNITS.md)** — consult that document to find the current next eligible unit rather than re-deriving it from this list.

Suggested sequence for proposals (not mandatory, but reduces rework):

1. D6 Threat model (draft can evolve with D4/D5) — **ADR-0001 Proposed**
2. D7 Privacy / data-handling model — **ADR-0002 Proposed**
3. D1 Technology stack
4. D2 Repository / application architecture
5. D9 Development / build environment
6. D8 Testing strategy
7. D3 Core data model
8. D4 Vault / encryption architecture
9. D5 Authentication / identity approach

Implementation of scaffolding should wait until at least D1, D2, D9 are Approved.  
Vault prototype implementation should wait until D3, D4, D6, D7 are Approved.  
Auth skeleton should wait until D5 and D6 are Approved.

---

## Summary table

| ID | Decision | Status | ADR |
|----|----------|--------|-----|
| D1 | Technology stack | Unresolved | — |
| D2 | Repository / application architecture | Unresolved | — |
| D3 | Core data model | Unresolved | — |
| D4 | Vault / encryption architecture | Unresolved | — |
| D5 | Authentication / identity approach | Unresolved | — |
| D6 | Threat model | **Proposed** | [ADR-0001](adr/0001-threat-model.md) |
| D7 | Privacy / data-handling model | **Proposed** | [ADR-0002](adr/0002-privacy-data-handling-model.md) |
| D8 | Testing strategy | Unresolved | — |
| D9 | Development / build environment | Unresolved | — |

**Approved count:** 0 / 9  
**Proposed (awaiting maintainer review):** 2 / 9 (D6, D7)

---

*Last updated: 2026-08-20 — ADR-0001 and ADR-0002 added as Proposed; no decisions Approved.*
