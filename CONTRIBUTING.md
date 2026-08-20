# Contributing to LifeSync

Thank you for your interest in contributing to LifeSync! We welcome contributions of all kinds — code, documentation, design, testing, and ideas.

## Code of Conduct

Please read and follow our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you agree to uphold these standards.

## Mandatory Policies (read before any implementation)

1. **Development Phases** — [PHASES.md](PHASES.md)  
   Work only within the active phase unless maintainers authorize otherwise.

2. **Security, Integrity, and No-Fake-Implementation** — [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md)  
   Never fake implementations, bypass security controls, invent capabilities, or claim verification without evidence. Use honest feature states: Planned → Implemented → Tested → Verified.

AI coding agents **must** follow both documents before implementing any phase work or feature.

## How to Contribute

### Reporting Bugs

- Search existing issues first to avoid duplicates.
- Use the bug report template (when available).
- Include steps to reproduce, expected vs actual behavior, environment details, and screenshots/logs if relevant.
- Report security vulnerabilities privately per [SECURITY.md](SECURITY.md).

### Suggesting Features

- Open a discussion or feature request issue.
- Clearly describe the problem you are solving and why it matters for personal continuity / life ops.
- Propose a high-level solution if you have one, but stay open to alternatives.
- Note which phase the suggestion would belong to.

### Pull Requests

1. Fork the repository and create a feature branch from `main`.
2. Make your changes with clear, focused commits. State the phase the work belongs to and the real implementation state (Planned / Implemented / Tested / Verified).
3. Add or update tests and documentation as needed. **Run the tests** before claiming they pass.
4. Ensure the code follows the project style (linting/formatting will be enforced once CI is set up).
5. Open a Pull Request against `main` with a clear description of the change, the phase it serves, linked issues, and honest status. Do not present stubs or UI-only work as complete features.
6. Be responsive to review feedback. Maintainers will reject or require correction of work that violates SECURITY_INTEGRITY.md.

### Development Setup (placeholder)

Detailed local development instructions will be added as the project matures (primarily during Phase 1). In the meantime:

- Prefer small, reviewable PRs.
- Privacy, security, and data minimization are non-negotiable design principles.
- Never hardcode secrets or disable security controls to “make it work.”

## Governance

See [GOVERNANCE.md](GOVERNANCE.md) for how decisions are made and how maintainers are selected.  
See [PHASES.md](PHASES.md) for the phase system.  
See [SECURITY_INTEGRITY.md](SECURITY_INTEGRITY.md) for the mandatory integrity and security rules.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
