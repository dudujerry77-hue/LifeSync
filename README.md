# LifeSync

**Privacy-first personal continuity & life ops platform.**

LifeSync is a digital twin for ordinary life — health records, finances, documents, relationships, skills, preferences, and daily logistics — designed so that critical information stays under your control and the boring coordination work gets lighter.

> **Current phase: Phase 1 — Core Platform Foundations (ACTIVE).**  
> **Current work unit: P1-WU03 — Propose technology stack (D1).**  
> See [docs/PHASE1_WORK_UNITS.md](docs/PHASE1_WORK_UNITS.md). D6/D7 ADRs are Proposed (awaiting maintainer Accept). Product implementation must not invent Unresolved decisions; see [docs/PHASE1_DECISIONS.md](docs/PHASE1_DECISIONS.md).

## Vision

Almost everyone struggles with fragmented tools, lost context across life events, and high cognitive load from admin work. LifeSync aims to provide a calm, trustworthy continuity layer that:

- Keeps your data private and portable by default
- Connects the dots across calendars, documents, health, and household logistics
- Offers gentle, proactive help without becoming another noisy dashboard

## Project Status & Phases

Development is organized into ordered phases, executed as **work units**. See **[PHASES.md](PHASES.md)** and **[docs/WORK_UNITS.md](docs/WORK_UNITS.md)**.

| Phase | Name | Status |
|-------|------|--------|
| 0 | Foundation | Complete |
| 1 | Core Platform Foundations | **ACTIVE** (next unit: P1-WU03) |
| 2 | First Continuity Workflows (MVP) | Upcoming |
| 3 | Connections & Gentle Proactivity | Upcoming |
| 4 | Expansion, Sharing & Hardening | Upcoming |

High-level checklist:

- [x] Repository & basic governance
- [ ] Phase 1 required decisions (ADRs) — see [docs/PHASE1_DECISIONS.md](docs/PHASE1_DECISIONS.md)
- [ ] Core data model & encrypted vault (after decisions Approved)
- [ ] MVP workflows (Phase 2)
- [ ] Connections & proactivity (Phase 3)
- [ ] Broader expansion & hardening (Phase 4)

## Governance & Community

- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Contributing Guide](CONTRIBUTING.md)
- [Governance](GOVERNANCE.md)
- [Development Phases](PHASES.md)
- [Work Unit Execution](docs/WORK_UNITS.md)
- [Phase 1 Work Units](docs/PHASE1_WORK_UNITS.md) ← **start here for the next increment**
- [Phase 1 Decision Register](docs/PHASE1_DECISIONS.md)
- [Architecture Decision Records](docs/adr/)
- [Security, Integrity & No-Fake-Implementation Policy](SECURITY_INTEGRITY.md) ← mandatory before any implementation
- [Security Policy](SECURITY.md) (vulnerability reporting)
- [License](LICENSE) (MIT)

## Getting Involved

We welcome ideas, issues, and contributions. Please read the contributing guide, code of conduct, **PHASES.md**, **SECURITY_INTEGRITY.md**, **docs/WORK_UNITS.md**, and **docs/PHASE1_WORK_UNITS.md** before opening pull requests.

For Phase 1: complete one work unit at a time. Propose ADRs for Unresolved decisions; do not implement product code that assumes undecided stack, vault design, data model, or auth approach.

---

Built with the goal that almost everyone can love a tool that solves real, everyday continuity problems — with real, secure, verifiable software.
