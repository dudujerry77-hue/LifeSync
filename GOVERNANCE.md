# LifeSync Project Governance

## Overview

LifeSync aims to be a privacy-first personal continuity platform. This document describes how the project is governed, how decisions are made, and how maintainers are added or removed.

## Principles

1. **Privacy & user ownership first** — decisions that affect data handling, encryption, or third-party sharing require extra scrutiny.
2. **Transparency** — major decisions and rationales should be documented publicly (issues, discussions, or RFCs/ADRs).
3. **Inclusivity** — we welcome contributors of all backgrounds and experience levels.
4. **Sustainability** — the project should remain maintainable and respectful of contributor time.
5. **Security, integrity, and no fake implementations** — real, secure, verifiable functionality only. See [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md).
6. **Incremental execution** — phases are executed as small, dependency-aware work units, not as one bulk implementation. See [docs/WORK_UNITS.md](docs/WORK_UNITS.md).

## Roles

### Contributors

Anyone who participates by opening issues, submitting PRs, writing docs, testing, or discussing ideas.

### Maintainers

Maintainers have write access to the repository and are responsible for:

- Reviewing and merging pull requests
- Triaging issues
- Upholding the Code of Conduct
- Guiding technical and product direction within the project principles
- Declaring the active development phase and confirming phase exit criteria (see [PHASES.md](PHASES.md))
- Enforcing the Security, Integrity, and No-Fake-Implementation Policy (see [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md))
- Accepting or rejecting Architecture Decision Records (see [docs/adr/](docs/adr/))
- Reviewing work-unit deliverables that wait on maintainer action

Current maintainers are listed in the repository (initially the repository owner).

### Stewards / Core Team (future)

As the project grows, a small core team may be formed to handle long-term vision, release management, and conflict resolution.

## Decision Making

- **Everyday decisions** (bug fixes, small features, docs): Maintainers decide via PR review.
- **Significant changes** (architecture, data model, privacy model, security-sensitive design, breaking changes): Prefer an **Architecture Decision Record (ADR)** under [docs/adr/](docs/adr/) and/or a design discussion issue. Aim for rough consensus among active maintainers. A decision is **not established** until an ADR is **Accepted** (or an equivalent maintainer-recorded approval).
- **Phase 1 required decisions:** Tracked in [docs/PHASE1_DECISIONS.md](docs/PHASE1_DECISIONS.md). Implementation that depends on an Unresolved decision must not treat that decision as settled.
- **ADRs:** Agents may **Propose**. Only maintainers **Accept**. After Accept, dependent work units may proceed.
- **Governance or Code of Conduct changes**: Require explicit agreement from a majority of current maintainers and a public notice period.
- **Phase advancement**: Only maintainers may declare that a phase’s exit criteria are met and that the next phase is active. Completing a work unit does not advance the phase. The declaration must be recorded (typically by updating PHASES.md). Exit criteria claims must satisfy the Verification Rule in [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md).

## Development Phases

The project progresses through ordered phases defined in **[PHASES.md](PHASES.md)**.

That document is the authoritative source for:

- The current (active) phase
- What capabilities each phase is expected to deliver
- What work belongs in each phase
- What AI coding agents and contributors are allowed to do in the active phase
- Verification requirements and exit criteria for advancing

All contributors and AI agents **must** read PHASES.md and restrict work to the active phase unless a maintainer has given explicit authorization otherwise.

## Work Units

Inside an active phase, work is executed as **work units** ([docs/WORK_UNITS.md](docs/WORK_UNITS.md)):

- One unit at a time; report before the next significant unit
- Hard dependencies must not be bypassed
- Independent units may proceed when their hard dependencies are met; the whole phase need not be finished first
- Later-phase functionality is forbidden until that phase is active

Phase 1 catalog: **[docs/PHASE1_WORK_UNITS.md](docs/PHASE1_WORK_UNITS.md)**.

## Security, Integrity, and No-Fake-Implementation

Because LifeSync handles highly sensitive personal information, the project enforces a strict **Security, Integrity, and No-Fake-Implementation Policy**.

**Authoritative document:** [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md)

Key obligations (full detail in that document):

- Never fake, simulate, or falsely claim that functionality is implemented, secure, tested, integrated, or verified.
- Every feature must have an honest state: Planned → Implemented → Tested → Verified.
- Security must be considered before implementation, not after.
- Claims of verification require concrete evidence.
- Uncertainty must be labeled UNKNOWN / NOT VERIFIED; security/privacy ambiguity must be resolved before implementing.
- Do not describe work as production-ready without the required testing, security review, and verification.

All AI coding agents **must** read and follow SECURITY_INTEGRITY.md before implementing any phase work or feature. Maintainers will reject or require correction of work that violates this policy.

## Architecture Decision Records

Significant technical decisions are recorded as ADRs in **[docs/adr/](docs/adr/)**.  
See that directory for process, status values, and template.  
Phase 1 decision checklist: **[docs/PHASE1_DECISIONS.md](docs/PHASE1_DECISIONS.md)**.

## Becoming a Maintainer

Maintainers are invited based on sustained, high-quality contributions and demonstrated alignment with project principles. There is no formal application process yet; existing maintainers will reach out.

## Removing Maintainers

Maintainers may step down at any time. In rare cases of inactivity or violation of the Code of Conduct, remaining maintainers may remove access after discussion.

## Conflict Resolution

1. Attempt to resolve via civil discussion in issues or private channels.
2. Escalate to maintainers if needed.
3. Code of Conduct enforcement follows the process in CODE_OF_CONDUCT.md.

## Changes to This Document

Updates to GOVERNANCE.md follow the same process as other significant changes and should be recorded in the commit history and ideally linked to an issue or discussion.

---

*This governance model is intentionally lightweight and will evolve as LifeSync grows.*
