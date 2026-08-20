# ADR-0002: Privacy and Data-Handling Model

- **Status:** Proposed
- **Date:** 2026-08-20
- **Deciders:** Maintainers (pending review)
- **Phase:** 1
- **Related decisions:** D7 (this ADR); pairs with D6 / ADR-0001; constrains D3, D4, D5, D2; informs Phases 2–4

## Context

LifeSync’s stated vision is a **privacy-first** personal continuity platform: user-owned data, portable by default, minimal unnecessary collection, calm assistance without becoming a surveillance dashboard ([README.md](../../README.md), [GOVERNANCE.md](../../GOVERNANCE.md)).

Before a data model (D3) or vault (D4) stores personal information, the project needs binding **data-handling rules**: ownership, consent, minimization, retention/deletion, export, sharing, emergency access, auditability, and future AI access.

This ADR proposes those rules at policy/architecture-intent level. It does **not** select databases, crypto libraries, or auth products.

## Decision drivers

- Governance principle: privacy & user ownership first
- SECURITY_INTEGRITY.md: no fake privacy claims; uncertainties labeled
- Threat model (ADR-0001 Proposed): leakage, host compromise, integrations, coercion, metadata
- Long-term features (family sharing, integrations, gentle proactivity, possible AI) must not require abandoning Phase 1 privacy defaults
- Legal regimes vary by jurisdiction; this ADR states product principles, not a substitute for legal advice (**UNKNOWN** on specific regulatory certification)

## Considered options

1. **Defer all privacy rules until product launch** — rejected (too late; data model would ossify badly).
2. **Copy a generic SaaS privacy policy template** — rejected (often assumes server-side profiling and ads; conflicts with vision).
3. **LifeSync-specific privacy & data-handling model** — user ownership, minimization, no silent third-party sharing, explicit rules for sharing/AI/export (**proposed**).

## Proposal (decision)

Adopt the following **Privacy and Data-Handling Model** as the baseline for Phase 1 and as constraints on later phases. Until **Accepted**, non-binding.

---

### 1. Data ownership

- **The user owns their continuity data.** LifeSync software is a tool/custodian of bits, not the data owner.
- Project operators, hosts, and future commercial entities **must not** claim ownership of user continuity content.
- Ownership includes the right to export and delete (subject to honest technical limits, e.g. lost keys — see §6).

---

### 2. Consent and authorization

- Processing beyond what is strictly necessary to provide a user-requested function requires **clear consent** or another explicit lawful basis documented in a future public privacy notice.
- **Authorization** (who may access what) is separate from authentication (who is acting).
- Sharing with another human (family, caregiver) requires **explicit grant** by the owner (or a future legally defined delegate — not Phase 1).
- Integration access requires **explicit, scoped, revocable** authorization.
- Silence, dark patterns, or pre-ticked “share everything” are incompatible with this model.

---

### 3. Data minimization

- Collect and retain only data **needed** for stated continuity functions the user opts into.
- Prefer storing user-provided continuity content over deriving invasive profiles.
- **No advertising identifiers, cross-product tracking, or growth-hacking analytics** by default.
- Phase 1 prototypes must not introduce telemetry that phones home continuity data or stable device identifiers unless a separate Accepted ADR overrides this default.

**Phase 1 allowed data (conceptual categories — exact schema is D3):**

- User-created or user-imported continuity content needed to exercise the vault prototype
- Account/identity material necessary for D5 skeleton
- Local configuration and encryption-related material necessary for vault operation
- Minimal operational logs **local-first**; no continuity payload in remote logs by default

**Phase 1 non-goals (explicit):**

- Behavioral advertising
- Selling or renting personal data
- Building shadow profiles for unrelated third parties
- Mandatory cloud backup of plaintext to operator-controlled systems

---

### 4. Retention and deletion

- Default retention: user-controlled; data remains until user deletes or uninstalls, subject to backup copies the user made.
- **Deletion:** User must be able to delete continuity content they own. Phase 1 must design toward real deletion of primary stores; **Verified** deletion claims require evidence (SECURITY_INTEGRITY.md).
- Backups/exports the user created are the user’s responsibility to delete.
- Server-side copies (if any architecture includes them): deletion and retention windows must be documented when D2/D4 exist.
- Legal hold / operator retention: **UNKNOWN / NOT VERIFIED** pending legal review; product should minimize operator-held plaintext so this is less relevant.

---

### 5. Export and portability

- Users should be able to **export** their continuity data in a documented, practical format (exact format is a later decision).
- Portability is part of “user ownership” and reduces lock-in.
- Exports are **Critical** sensitivity (ADR-0001); export UX must warn that files may be plaintext and must be stored safely.
- Phase 1: design data model (D3) so export is feasible; full export UX may be incomplete but must not be architected out.

---

### 6. Encryption and confidentiality (policy level)

- Confidentiality of continuity content is a **privacy requirement**, not only a security feature.
- Align with ADR-0001: prefer designs where untrusted hosts cannot read plaintext.
- User-understandable description of who can read data under what conditions is required before any production-ready claim.
- Specific mechanisms: **D4**.

---

### 7. Family / shared access

- Sharing is **not** the same as transferring ownership.
- Grants should be least privilege (categories, time-bound where feasible), visible to the owner, and revocable.
- Phase 1: **no multi-user sharing implementation required**; data model and auth should avoid assumptions that block later least-privilege sharing (D3/D5 constraint).
- Coercion and shared-device risk: acknowledge residual risk; optional future “safe” modes are out of scope for Phase 1 implementation but may be noted in UX later.

---

### 8. Emergency / continuity access

- Real life includes emergency access (incapacity, death, lost device). Blind “no recovery ever” can destroy the product’s continuity purpose.
- **Proposed principle:** Emergency/continuity access mechanisms must be **user-configured**, explicit, and narrower than “operator can unlock anyone.”
- Phase 1: document intent; concrete recovery design in D4/D5 without inventing mechanisms here.
- Break-glass operator access to all vaults: **incompatible** with privacy-first defaults unless a future ADR with extraordinary justification is Accepted.

---

### 9. Auditability

- Security-relevant events (auth failures, grant changes, export, deletion, integration token use) should be **auditable** by the user where feasible.
- Audit logs are themselves sensitive; protect and minimize; do not ship full audit payloads to third parties by default.
- Phase 1: define hooks/intent; full audit product may come later.

---

### 10. Future AI access to personal data

Consistent with ADR-0001:

- AI features that read continuity data are **opt-in**, purpose-limited, and disclosed in plain language.
- No hidden use of vault content to train external models by default.
- Prefer on-device or user-controlled processing when practical; external AI = integration trust rules.
- Data sent to AI systems is a **disclosure**; minimization applies (send only needed snippets, not entire vault).
- Phase 1: no AI implementation; architecture must not force all data through a vendor LLM.

---

### 11. Children / sensitive special categories

- Health and related data may be highly sensitive. Product principles treat them as Critical assets.
- Specialized regulatory regimes (e.g., health data rules by jurisdiction): **UNKNOWN / NOT VERIFIED** — requires legal review before regulated-market production claims.
- Phase 1 engineering still applies high protection standards regardless of legal label.

---

### 12. Public statements and integrity

- Privacy claims in README, website, or app store text must match this model and actual implementation state (Planned / Implemented / Tested / Verified).
- Do not describe the system as “fully private,” “unhackable,” or “HIPAA compliant” without Accepted ADR + evidence.

---

## Consequences

### Positive

- Clear defaults for agents and humans designing D3–D5.
- Reduces risk of embedding analytics or server-side profiling early.
- Supports long-term trust and exportability.

### Negative / trade-offs

- Limits monetization patterns that depend on data resale or invasive telemetry.
- Recovery and family features need careful design to avoid conflicting with minimization and consent.
- Some convenience features slower to ship.

### Neutral

- Will need a user-facing privacy notice before production; this ADR is internal governance, not that notice.

## Security & privacy notes

This ADR operationalizes privacy. Security threats and boundaries are in **ADR-0001**. Together they constrain D4 (vault) and D5 (auth). Ambiguities that affect safety must stop implementation until resolved (SECURITY_INTEGRITY.md Uncertainty Rule).

**UNKNOWN / NOT VERIFIED:** jurisdiction-specific compliance certifications; final cloud operator commitments; concrete export format.

## Evidence required before treating implementation as Verified

- Inventory of data categories stored matches this model (no silent extras).
- Demonstration that default builds do not transmit continuity content to third-party analytics.
- Deletion/export behavior matches claims when those features are implemented (executed tests or reproducible manual procedures).
- Sharing/AI features, when built, show explicit consent and scope evidence.

## Alternatives not chosen (summary)

- Deferring privacy rules risks irreversible architecture mistakes.
- Generic SaaS templates conflict with user-ownership and no-ads-by-default vision.

## References

- [GOVERNANCE.md](../../GOVERNANCE.md)
- [SECURITY_INTEGRITY.md](../../SECURITY_INTEGRITY.md)
- [README.md](../../README.md) — vision
- [docs/PHASE1_DECISIONS.md](../PHASE1_DECISIONS.md) — D7
- Companion: [ADR-0001](0001-threat-model.md) (Proposed)
