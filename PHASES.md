# LifeSync Development Phases

This document defines the ordered development phases for LifeSync. It is the authoritative source for what work is in scope at any time, what an AI coding agent (or human contributor) may do, and the criteria required to advance.

**Current phase:** Phase 0 — Foundation (complete). The project is ready to enter Phase 1.

Maintainers declare the active phase. Agents and contributors **must** restrict work to the active phase (and any explicitly allowed preparatory work for the next phase). Advancing phases requires explicit maintainer confirmation that exit criteria are met.

**Mandatory companion policy:** Before implementing any phase work or feature, every AI agent and contributor **must** read and follow [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md) (Security, Integrity, and No-Fake-Implementation Policy). Phase exit criteria and status claims are subject to that policy’s Verification Rule and Core Rule.

---

## How an AI Agent Must Use This Document

1. Read this file, `GOVERNANCE.md`, and **`SECURITY_INTEGRITY.md`** before starting any substantial work.
2. Identify the **current (active) phase**.
3. Only perform work that belongs to the active phase (or is listed as allowed preparatory work).
4. Do **not** implement features, architecture, or scope belonging to later phases unless a maintainer has explicitly authorized it.
5. When proposing or completing work, state which phase it belongs to and how it satisfies (or moves toward) the phase’s verification and exit criteria — using only honest states (Planned / Implemented / Tested / Verified) and concrete evidence for Verified claims.
6. Do not advance the phase yourself. Report readiness against exit criteria; a maintainer decides advancement and updates the “Current phase” declaration.
7. Respect the project principles in `GOVERNANCE.md` (especially privacy & user ownership first) and the mandatory rules in `SECURITY_INTEGRITY.md` at every phase.
8. Never fake implementations, bypass security controls, invent capabilities, or claim verification without evidence.

---

## Phase 0 — Foundation

**Status:** Complete  
**Objective:** Establish a healthy, well-governed open repository so that future development can proceed safely and transparently.

### Capabilities / features gained
- Public repository with clear vision and status
- Lightweight but complete governance (roles, decision-making, CoC, security policy, license, integrity policy)
- Contribution guidelines

### Work that belongs to this phase
- Repository creation and basic structure
- Governance documents (CODE_OF_CONDUCT, CONTRIBUTING, GOVERNANCE, SECURITY, SECURITY_INTEGRITY, LICENSE, README, PHASES)
- Initial project vision statement

### What an AI agent is allowed / expected to do
- Maintain and improve governance and documentation clarity
- Fix typos, broken links, or inconsistencies in existing docs
- Propose (but not unilaterally apply) small governance refinements
- **Not** start product code, data models, or feature implementation

### Dependencies
- None (starting point)

### Verification requirements
- All core governance files exist and are linked from README
- Principles and decision processes are documented
- License, security reporting path, and integrity policy are present

### Exit criteria (all must be true)
- [x] Repository exists and is public (or intentionally private)
- [x] CODE_OF_CONDUCT.md, CONTRIBUTING.md, GOVERNANCE.md, SECURITY.md, SECURITY_INTEGRITY.md, LICENSE, PHASES.md, and README.md are present and coherent
- [x] Project vision and high-level status are stated
- [x] Maintainers can begin Phase 1 work

**Advancement:** Maintainers declare Phase 1 active.

---

## Phase 1 — Core Platform Foundations

**Objective:** Establish the technical and privacy foundations required before any user-facing continuity workflows: core data model concepts, encrypted personal vault approach, identity/auth basics, and project scaffolding that respects privacy-first principles.

### Capabilities / features gained
- Defined (documented) core data model oriented around personal continuity entities
- Encrypted vault design and initial implementation approach (user-owned / privacy-preserving)
- Basic project structure, tooling, and development setup
- Authentication / identity skeleton consistent with privacy goals
- Clear boundaries for what data is stored and how it is protected

### Work that belongs to this phase
- Architecture and design discussions / RFCs for data model and vault
- Scaffolding the application (language, framework, repo layout)
- Implementing or prototyping the encrypted vault and core storage primitives
- Basic auth / user identity (local-first or privacy-respecting options preferred)
- Development environment documentation and minimal CI scaffolding
- Security and privacy threat modeling at the foundation level

### What an AI agent is allowed / expected to do
- Propose and implement scaffolding, data-model documentation, and vault prototypes **within** the privacy-first constraints and SECURITY_INTEGRITY.md rules
- Write tests for cryptographic and storage primitives and actually run them before claiming they pass
- Update development setup docs
- Open design issues / RFCs for significant choices
- **Not** implement full user-facing workflows, external integrations, or multi-user sharing beyond what is required to validate the vault
- **Not** introduce third-party data sharing or analytics without explicit maintainer approval
- **Not** fake vault/encryption behavior, hardcode secrets, or claim security properties without evidence

### Dependencies
- Phase 0 complete

### Verification requirements
- Documented core data model (entities relevant to personal continuity)
- Working (or clearly prototyped) encrypted vault with tests that have been run
- Development setup that a new contributor can follow
- Privacy and security considerations recorded for the chosen approach
- No regression of governance principles or integrity policy
- All status claims obey SECURITY_INTEGRITY.md

### Exit criteria (all must be true)
- [ ] Core data model is documented and reviewed by maintainers
- [ ] Encrypted vault (or equivalent privacy-preserving storage) has a working prototype with tests that have actually been executed
- [ ] Basic project scaffolding and local development instructions exist
- [ ] Auth / identity approach is chosen and sketched in a way consistent with privacy-first principles
- [ ] Maintainers confirm the foundation is solid enough to support the first real workflows
- [ ] No known fake implementations or unverified security claims remain in the delivered work

**Advancement:** Maintainer declaration after exit criteria are verified under the Verification Rule.

---

## Phase 2 — First Continuity Workflows (MVP)

**Objective:** Deliver the first narrow, high-value continuity workflows so a real user can experience tangible relief from fragmentation and cognitive load, while staying within the privacy and scope boundaries established earlier.

### Capabilities / features gained
- At least one (preferably 1–2) concrete end-to-end continuity workflows
- Ability for a user to store, retrieve, and act on personal continuity data for those workflows
- Minimal UI or interface sufficient to use the workflows
- Feedback loop from early users / testers

### Work that belongs to this phase
- Selection and detailed design of the initial workflow(s) (must align with the existing vision of personal continuity)
- Implementation of those workflows on top of the Phase 1 vault and data model
- Basic user interface or interaction surface
- Manual and automated verification of the workflows
- Documentation of how the workflows serve the continuity goals

### What an AI agent is allowed / expected to do
- Implement the agreed MVP workflows and supporting UI with real behavior (not UI-only shells presented as complete)
- Add tests covering the workflows and run them before claiming success
- Improve ergonomics and reliability of the chosen scope
- Document usage and honest feature state
- **Not** expand into additional domains or integrations beyond the agreed MVP set without maintainer approval
- **Not** weaken privacy guarantees established in Phase 1
- **Not** mark workflows “implemented” or “verified” without evidence required by SECURITY_INTEGRITY.md

### Dependencies
- Phase 1 exit criteria met

### Verification requirements
- Documented description of each MVP workflow and the user problem it addresses
- Working end-to-end path for each workflow (happy path + basic error cases) with evidence
- Tests for core logic that have been executed
- Privacy properties of Phase 1 still hold
- Early feedback captured (even if informal)
- Honest state reporting only

### Exit criteria (all must be true)
- [ ] At least one complete continuity workflow is usable end-to-end with real implementation
- [ ] The workflow demonstrably reduces a real continuity / admin pain point
- [ ] Tests and basic documentation exist; tests have been run
- [ ] Maintainers and early testers agree the MVP is coherent and ready for limited expansion
- [ ] No fake or UI-only implementations are presented as complete

**Advancement:** Maintainer declaration after exit criteria are verified under the Verification Rule.

---

## Phase 3 — Connections & Gentle Proactivity

**Objective:** Connect the continuity layer to external sources the user already uses (calendars, documents, etc.) and introduce carefully scoped, transparent, user-controlled proactive assistance — without becoming noisy or privacy-invasive.

### Capabilities / features gained
- Controlled integrations / import paths for selected external data sources
- Conflict detection and gentle, explainable suggestions
- User controls over what is connected and what proactivity is allowed
- Improved continuity across the domains already in scope

### Work that belongs to this phase
- Design and implementation of integration boundaries (privacy-preserving)
- Import / sync mechanisms for the chosen sources
- Proactive suggestion engine that is transparent and opt-in / controllable
- UX for managing connections and notification preferences
- Security review of integration surfaces

### What an AI agent is allowed / expected to do
- Implement approved integrations and the proactivity layer under the stated constraints and SECURITY_INTEGRITY.md
- Add tests, especially around data boundaries and user controls, and run them
- Document integration and privacy implications honestly
- **Not** add unrestricted third-party access, background data collection, or opaque AI behavior
- **Not** expand the set of integrations beyond what maintainers have approved for this phase
- **Not** claim an integration works without actual testing against the real or approved test dependency
- **Not** invent API behavior or fake successful responses

### Dependencies
- Phase 2 exit criteria met

### Verification requirements
- Integrations respect user consent and data minimization
- Proactive features are explainable and controllable
- Privacy threat model updated for new surfaces
- Tests covering integration boundaries and controls (executed)
- Evidence for any “works” claim

### Exit criteria (all must be true)
- [ ] At least one external connection path works end-to-end with clear user controls and verified behavior
- [ ] Gentle proactivity is present, transparent, and can be limited or disabled by the user
- [ ] Privacy and security review of the new surfaces is documented and accepted by maintainers
- [ ] Maintainers confirm the system remains calm and trustworthy
- [ ] No unverified integration or security claims remain

**Advancement:** Maintainer declaration after exit criteria are verified under the Verification Rule.

---

## Phase 4 — Expansion, Sharing & Hardening

**Objective:** Broaden supported continuity domains, add carefully designed sharing / family / caregiver capabilities where they serve real continuity needs, and harden the system for reliability, accessibility, and long-term maintainability.

### Capabilities / features gained
- Support for additional life domains consistent with the original vision
- Controlled sharing models (e.g., family or caregiver views) that preserve user ownership
- Improved reliability, performance, accessibility, and operational readiness
- Clearer public roadmap and release practices

### Work that belongs to this phase
- Domain expansion guided by user need and vision alignment
- Sharing / multi-party continuity features with strong consent and auditability
- Hardening (testing, observability, accessibility, performance)
- Release and support processes
- Community and documentation maturity

### What an AI agent is allowed / expected to do
- Implement approved domain expansions and sharing features under SECURITY_INTEGRITY.md
- Strengthen test coverage, docs, and operational tooling; run tests before claiming results
- Help maintain the phase and roadmap documentation with accurate status
- **Not** introduce features that conflict with privacy-first principles or the established governance
- **Not** treat this phase as open-ended; significant new directions still require design discussion / RFC
- **Not** claim production readiness without the required verification and security review

### Dependencies
- Phase 3 exit criteria met

### Verification requirements
- New domains and sharing models have documented privacy and consent models
- System remains coherent with the original vision
- Quality, security, and accessibility bars appropriate for broader use are met with evidence
- Roadmap and release process are visible
- Honest state reporting throughout

### Exit criteria (all must be true)
- [ ] Additional domains or sharing capabilities are live and aligned with vision
- [ ] Hardening and quality gates appropriate for the user base are in place and verified
- [ ] Maintainers judge the project ready for sustained public use and community growth
- [ ] Ongoing governance, phase discipline, and integrity policy remain effective

**Advancement / ongoing:** After Phase 4 the project moves into continuous improvement under normal governance. New major capabilities continue to follow the decision-making rules in GOVERNANCE.md (RFCs for significant changes, etc.) and SECURITY_INTEGRITY.md.

---

## Phase Advancement Rules

- Only maintainers declare that a phase is complete and the next phase is active.
- The declaration should be recorded (commit updating this file, or a linked issue / discussion).
- Agents and contributors must not assume advancement has occurred until it is recorded.
- Skipping phases is not allowed without explicit maintainer decision and documented rationale.
- Work that spans phases is discouraged; prefer completing the current phase first.
- All exit-criteria claims are subject to the Verification Rule and Core Rule in SECURITY_INTEGRITY.md. Fake or unverified claims are invalid grounds for advancement.

## Relationship to Other Governance

- This phase system does **not** replace GOVERNANCE.md, the Code of Conduct, SECURITY.md, or SECURITY_INTEGRITY.md.
- Significant architectural or privacy decisions still follow the “Significant changes” process in GOVERNANCE.md.
- The phase system constrains *scope and sequencing*; SECURITY_INTEGRITY.md constrains *honesty, security, and verification* of all work. Neither overrides the other; both apply.
