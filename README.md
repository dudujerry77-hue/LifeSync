# LifeSync

**Privacy-first personal continuity & life ops platform.**

LifeSync is a digital twin for ordinary life — health records, finances, documents, relationships, skills, preferences, and daily logistics — designed so that critical information stays under your control and the boring coordination work gets lighter.

> **Current phase: Phase 1 — Core Platform Foundations (ACTIVE).**  
> Governance, phases, integrity policy, and an ADR/decision register are in place. **Required Phase 1 technical decisions are still Unresolved.** Product implementation must not invent those decisions; see [docs/PHASE1_DECISIONS.md](docs/PHASE1_DECISIONS.md).

## Vision

Almost everyone struggles with fragmented tools, lost context across life events, and high cognitive load from admin work. LifeSync aims to provide a calm, trustworthy continuity layer that:

- Keeps your data private and portable by default
- Connects the dots across calendars, documents, health, and household logistics
- Offers gentle, proactive help without becoming another noisy dashboard

## Project Status & Phases

Development is organized into ordered phases. See **[PHASES.md](PHASES.md)** for full definitions, allowed work, verification requirements, and exit criteria.

| Phase | Name | Status |
|-------|------|--------|
| 0 | Foundation | Complete |
| 1 | Core Platform Foundations | **ACTIVE** |
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
- [Phase 1 Decision Register](docs/PHASE1_DECISIONS.md) ← **start here for Phase 1 work**
- [Architecture Decision Records](docs/adr/)
- [Security, Integrity & No-Fake-Implementation Policy](SECURITY_INTEGRITY.md) ← mandatory before any implementation
- [Security Policy](SECURITY.md) (vulnerability reporting)
- [License](LICENSE) (MIT)

## Getting Involved

We welcome ideas, issues, and contributions. Please read the contributing guide, code of conduct, **PHASES.md**, **SECURITY_INTEGRITY.md**, and **docs/PHASE1_DECISIONS.md** before opening pull requests.

For Phase 1: propose ADRs for Unresolved decisions; do not implement product code that assumes undecided stack, vault design, data model, or auth approach.

---

Built with the goal that almost everyone can love a tool that solves real, everyday continuity problems — with real, secure, verifiable software.
