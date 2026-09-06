# Work Unit Execution Model

This document defines how **every phase** is executed incrementally.

It does **not** replace [PHASES.md](../PHASES.md). Phases still define scope, capabilities, and phase-level exit criteria. Work units are the **execution method** inside a phase.

**Loop:** Phase → Work Unit → Deliverable → Verification → Report → (Maintainer approval where required) → Next eligible work unit

**Not:** Phase → Build everything → Report at the end

---

## Rules (binding)

1. **One work unit at a time.** An AI agent completes a single work unit, then **stops and reports** before starting the next *significant* work unit.
2. **Stay inside the active phase.** Work units must not implement later-phase functionality. Phase advancement remains maintainer-only ([PHASES.md](../PHASES.md)).
3. **Honor dependencies.** A work unit must not start if a listed **hard dependency** is unmet. Informed-by items should be considered but do not block *proposal* work unless listed as hard dependencies.
4. **Unresolved decisions block dependent implementation.** Product code that depends on a decision may start only when that decision is **Approved** (ADR **Accepted** by a maintainer). See [docs/adr/](adr/).
5. **Agents propose; maintainers Accept.** An agent may draft ADRs (status **Proposed**). Only a maintainer may set an ADR to **Accepted**. Agents must not mark decisions Approved.
6. **Independent work may proceed.** Completing the *entire phase* is not required before moving to another work unit whose hard dependencies are satisfied.
7. **No fake work.** [SECURITY_INTEGRITY.md](../SECURITY_INTEGRITY.md) applies to every work unit. Honest states only: Planned → Implemented → Tested → Verified. Evidence required for Verified claims.
8. **Report after each unit.** The report must include: work unit id, what was delivered, verification performed, blockers, what is waiting on the maintainer, and the next eligible work unit.
9. **Update the work-unit tracker** in the phase's work-unit file (status only, to match reality).

---

## Work unit status values

| Status | Meaning |
|--------|---------|
| **Not started** | Not yet eligible or not yet begun |
| **Ready** | Hard dependencies met; this is (or may be) the next unit |
| **In progress** | An agent is executing this unit |
| **Waiting for maintainer** | Deliverable exists (e.g. Proposed ADR); blocked on Accept/review |
| **Blocked** | Hard dependency unmet |
| **Complete** | Exit criteria met *and* any required maintainer action recorded |

A Propose-ADR unit becomes **Waiting for maintainer** when the ADR is Proposed. It becomes **Complete** only when the ADR is **Accepted** (or Rejected/Deferred with recorded rationale). The agent may still start a *different* unit whose hard dependencies are already met.

---

## Required fields for each work unit

Every work unit definition must include:

- **ID** and **name**
- **Objective**
- **Inputs / dependencies** (hard vs informed-by)
- **Allowed work** (and explicit not-allowed)
- **Deliverables**
- **Verification requirements**
- **Exit criteria**

---

## Agent operating procedure

1. Read `PHASES.md`, `SECURITY_INTEGRITY.md`, this file, and the **active phase's work-unit file**.
2. Identify the **current / next eligible** work unit (hard dependencies satisfied; prefer the documented sequence).
3. Execute **only that unit**.
4. Produce deliverables and run verification.
5. Update the unit's status honestly.
6. **Report and stop** before the next significant unit.
7. If a hard dependency is unmet, **do not bypass it**. Report **Blocked** and what the maintainer or prior unit must provide.

---

## Phase work-unit files

| Phase | Work-unit catalog |
|-------|-------------------|
| 1 | [PHASE1_WORK_UNITS.md](PHASE1_WORK_UNITS.md) |
| 2-4 | To be added when that phase becomes active (same rules apply) |

Until a later phase has its own catalog, agents must **not** invent later-phase work units or implement that phase's features.
