# Contributing to LifeSync

Thank you for your interest in contributing to LifeSync! We welcome contributions of all kinds — code, documentation, design, testing, and ideas.

## Code of Conduct

Please read and follow our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you agree to uphold these standards.

## Mandatory Policies (read before any implementation)

1. **Development Phases** — [PHASES.md](PHASES.md)  
   Work only within the active phase unless maintainers authorize otherwise. **Phase 1 is ACTIVE.**

2. **Security, Integrity, and No-Fake-Implementation** — [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md)  
   Never fake implementations, bypass security controls, invent capabilities, or claim verification without evidence. Use honest feature states: Planned → Implemented → Tested → Verified.

3. **Phase 1 decisions** — [docs/PHASE1_DECISIONS.md](docs/PHASE1_DECISIONS.md)  
   Required decisions (stack, architecture, data model, vault, auth, threat model, privacy model, testing, dev environment) are **Unresolved** until ADRs are Accepted. Do not implement as if they were decided.

4. **ADRs** — [docs/adr/](docs/adr/)  
   Significant decisions use the ADR template and process. Only maintainers Accept ADRs.

AI coding agents **must** follow these documents before implementing any phase work or feature.

## How to Contribute

### Reporting Bugs

- Search existing issues first to avoid duplicates.
- Use the bug report template (when available).
- Include steps to reproduce, expected vs actual behavior, environment details, and screenshots/logs if relevant.
- Report security vulnerabilities privately per [SECURITY.md](SECURITY.md).

### Suggesting Features / Proposing Decisions

- Open a discussion or feature request issue.
- For Phase 1 technical choices, prefer an **ADR** (copy `docs/adr/template.md`).
- Clearly describe the problem and options; do not mark an ADR Accepted unless you are a maintainer.
- Note which phase and which PHASE1_DECISIONS id (D1–D9) the proposal relates to.

### Pull Requests

1. Fork the repository and create a feature branch from `main`.
2. Make your changes with clear, focused commits. State the phase, related decision ids, and real implementation state (Planned / Implemented / Tested / Verified).
3. If the PR implements behavior that depends on a decision, that decision must already be **Approved** (Accepted ADR).
4. Add or update tests and documentation as needed. **Run the tests** before claiming they pass.
5. Ensure the code follows the project style (linting/formatting will be enforced once CI is set up).
6. Open a Pull Request against `main` with honest status. Do not present stubs or UI-only work as complete features.
7. Be responsive to review feedback. Maintainers will reject or require correction of work that violates SECURITY_INTEGRITY.md or assumes Unresolved decisions.

### Development Setup

Detailed local development instructions will be added when decision **D9** (and related stack decisions) are Approved. Until then:

- Prefer small, reviewable PRs (especially ADRs and docs).
- Privacy, security, and data minimization are non-negotiable design principles.
- Never hardcode secrets or disable security controls to “make it work.”

## Governance

See [GOVERNANCE.md](GOVERNANCE.md) for how decisions are made and how maintainers are selected.  
See [PHASES.md](PHASES.md) for the phase system.  
See [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md) for the mandatory integrity and security rules.  
See [docs/PHASE1_DECISIONS.md](docs/PHASE1_DECISIONS.md) for the Phase 1 decision register.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
