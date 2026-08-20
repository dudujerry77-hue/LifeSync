# LifeSync Project Governance

## Overview

LifeSync aims to be a privacy-first personal continuity platform. This document describes how the project is governed, how decisions are made, and how maintainers are added or removed.

## Principles

1. **Privacy & user ownership first** — decisions that affect data handling, encryption, or third-party sharing require extra scrutiny.
2. **Transparency** — major decisions and rationales should be documented publicly (issues, discussions, or RFCs).
3. **Inclusivity** — we welcome contributors of all backgrounds and experience levels.
4. **Sustainability** — the project should remain maintainable and respectful of contributor time.

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

Current maintainers are listed in the repository (initially the repository owner).

### Stewards / Core Team (future)

As the project grows, a small core team may be formed to handle long-term vision, release management, and conflict resolution.

## Decision Making

- **Everyday decisions** (bug fixes, small features, docs): Maintainers decide via PR review.
- **Significant changes** (architecture, data model, privacy model, breaking changes): Prefer an RFC or design discussion issue. Aim for rough consensus among active maintainers.
- **Governance or Code of Conduct changes**: Require explicit agreement from a majority of current maintainers and a public notice period.
- **Phase advancement**: Only maintainers may declare that a phase’s exit criteria are met and that the next phase is active. The declaration must be recorded (typically by updating PHASES.md).

## Development Phases

The project progresses through ordered phases defined in **[PHASES.md](PHASES.md)**.

That document is the authoritative source for:

- The current (active) phase
- What capabilities each phase is expected to deliver
- What work belongs in each phase
- What AI coding agents and contributors are allowed to do in the active phase
- Verification requirements and exit criteria for advancing

All contributors and AI agents **must** read PHASES.md and restrict work to the active phase unless a maintainer has given explicit authorization otherwise.

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
