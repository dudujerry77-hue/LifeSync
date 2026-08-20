# ADR-0001: Foundation Threat Model

- **Status:** Proposed
- **Date:** 2026-08-20
- **Deciders:** Maintainers (pending review)
- **Phase:** 1
- **Related decisions:** D6 (this ADR); informs D4, D5, D3, D2, D7 (ADR-0002), later phases

## Context

LifeSync is intended to hold highly sensitive personal continuity data (health, finances, documents, relationships, logistics, preferences). Governance requires security-first design and forbids claiming controls that are only planned ([SECURITY_INTEGRITY.md](../../SECURITY_INTEGRITY.md), [GOVERNANCE.md](../../GOVERNANCE.md)).

Before choosing cryptography libraries, auth technologies, or storage engines (D1, D4, D5), the project needs an explicit **foundation threat model**: what we protect, whom we defend against, where trust boundaries sit, and which risks Phase 1 must address versus defer with honest labeling.

This ADR proposes that model. It does **not** select specific algorithms, frameworks, or vendors.

## Decision drivers

- Privacy & user ownership first
- Realistic adversaries for a personal continuity vault (not only nation-state theater, not only “trusted local user”)
- Long-term vision includes integrations, family/caregiver sharing, and possible AI assistance — threats must not assume a forever-local single-user toy
- Phase 1 scope is foundations (vault, identity skeleton, data model) — model must cover Phase 1 assets while stating future surfaces as design constraints
- SECURITY_INTEGRITY.md: honest UNKNOWN where we cannot yet verify

## Considered options

1. **No formal threat model** — implement first, document threats later (rejected: violates security-first rule).
2. **Generic OWASP-only checklist** — useful but insufficient for continuity-specific assets (shared access, emergency access, AI over personal data, integration compromise).
3. **Foundation threat model tailored to LifeSync** — assets, actors, boundaries, Phase 1 priorities, explicit deferred surfaces (**proposed**).

## Proposal (decision)

Adopt the following **foundation threat model** as the baseline for Phase 1 design and for evaluating later ADRs (especially D4 vault/encryption and D5 authentication/identity). Until this ADR is **Accepted**, it is non-binding.

---

### 1. Assets being protected

| Asset class | Examples (vision-level) | Sensitivity |
|-------------|-------------------------|-------------|
| **Primary continuity content** | Documents, notes, health-related records, financial references, relationship/context data, logistics/plans | Critical |
| **Derived continuity knowledge** | Links between entities, timelines, reminders, proactive suggestions grounded in user data | High |
| **Credentials & secrets** | Auth material, encryption keys, recovery material, integration tokens | Critical |
| **Identity & authorization state** | Who the user is, sessions, sharing grants, consent records | High |
| **Metadata** | Timestamps, sizes, counts, graph structure, access patterns, device identifiers | Medium–High (often underestimated) |
| **Backups & exports** | Portable archives, recovery snapshots | Critical (same as primary content) |
| **Audit / access history** | Who accessed what, when (if retained) | High (also a privacy risk if over-collected) |
| **System integrity** | Application code, update channel, configuration | High |

Phase 1 concentrates on protecting primary content, keys/secrets, identity basics, and avoiding reckless metadata leakage in any prototype vault.

---

### 2. Realistic threat actors

| Actor | Motivation / capability | Relevance |
|-------|-------------------------|----------|
| **Curious or malicious local person** | Physical access to unlocked device; family conflict; theft of laptop/phone | High for personal apps |
| **Device/OS malware / shared device** | Credential theft, keylogging, screen capture, local file read | High |
| **Network attacker (on-path)** | Observe or modify traffic if any sync/API exists | High if networked components exist |
| **Account takeover** | Stolen password, session, or recovery path | High once accounts exist |
| **Malicious or compromised integration** | OAuth app, calendar/import connector, webhook abusing granted scopes | High from Phase 3 onward; design D4/D5 to limit blast radius |
| **Honest-but-curious operator / host** | Hosting provider, SaaS dependency, or project operator with server access | High if any server sees plaintext |
| **Insider or compromised maintainer/supply chain** | Malicious dependency, poisoned release, rogue deploy | Medium–High over project lifetime |
| **Abusive intimate partner / coercion** | Forced disclosure, shared-device surveillance | High for continuity/health data |
| **Legal/coercive process against a host** | Subpoena of server-held data | High if host holds decryptable data |
| **Opportunistic internet attacker** | Scanning, credential stuffing, API abuse | High for any public endpoint |
| **Advanced persistent / nation-state** | High capability | In scope as *aspire to reduce*; not a claim of full resistance without evidence |

---

### 3. Trust boundaries (conceptual)

Until D2/D4 decide placement, assume these **logical** boundaries must be defined in later ADRs:

1. **User & local device environment** — end-user control; also malware risk.
2. **LifeSync client application** — code that may hold keys or plaintext transiently.
3. **LifeSync vault storage** — at-rest data; must state whether ciphertext is readable by host.
4. **Optional LifeSync server / relay / sync service** — if any; default posture: **minimize trust** (prefer cannot read plaintext continuity content).
5. **Third-party integrations** — outside trust; least privilege, revocable, scoped.
6. **Shared principals** (family, caregiver) — separate authorization domain; not “same as owner.”
7. **AI / automation components** — if they process personal data, they are a distinct trust and data-flow surface (see §11).
8. **Build & update pipeline** — supply chain boundary.

**Proposed principle:** Any component that is not required to see plaintext continuity content should be designed so it **cannot** see it (cryptographic enforcement preferred over policy-only), once D4 is decided.

---

### 4. Attack surfaces

| Surface | Notes |
|---------|--------|
| Local data at rest | Disk theft, backup extraction, unencrypted exports |
| Local runtime | Memory scraping, debugger, malicious accessibility tools |
| Authentication & recovery | Password reset, recovery keys, backup codes, “remember this device” |
| Authorization / sharing grants | Over-broad shares, confused deputy, leftover access after relationship change |
| APIs / sync endpoints | Injection, IDOR, replay, rate abuse (if networked) |
| Integration connectors | Token theft, scope creep, supplier breach |
| Import/export pipelines | Malicious files, path traversal, plaintext export left on disk |
| Backups | Unencrypted cloud backups of “encrypted” app data; recovery UX that weakens crypto |
| Client updates | Trojanized builds |
| Support / debug channels | Logs containing PII or secrets |
| Future AI features | Prompt injection, over-retention of embeddings, unintended training use |

---

### 5. Abuse and misuse scenarios

- User coerced to unlock or share recovery material.
- Shared household device used to silently browse another person’s continuity data.
- Stalking via location/logistics data if stored.
- Fraud via financial continuity data.
- Medical privacy harm via health-related content.
- User locks themselves out (availability threat) through lost keys — security must not ignore continuity of access for the legitimate owner.
- Malicious “caregiver” invite or social-engineering of sharing features.

---

### 6. Account and device compromise

**Proposed expectations for later ADRs (D4/D5):**

- Compromise of a single session should not silently yield long-term vault keys without additional factors or local secrets, where architecture allows.
- Device loss: at-rest protection must assume attacker gets the storage medium.
- Account recovery is a **primary attack path**; recovery design needs explicit threat analysis in D5 (not invented here).
- Remote wipe / revoke sessions: desirable; **Phase 1 may defer** with status UNKNOWN until architecture exists.

---

### 7. Malicious or compromised integrations

- Integrations are untrusted by default.
- Tokens stored with vault-level care; revocable; least privilege scopes.
- Compromise of one integration must not imply ability to decrypt entire vault.
- Import paths treat external data as potentially hostile (validation, size limits) — detailed controls in later phases/ADRs.

---

### 8. Insider / server compromise

**Proposed posture:** If a server or operator is compromised, impact on **plaintext continuity content** should be minimized by design (e.g., server holds only ciphertext / opaque blobs where feasible).  
Policy-only promises (“we won’t look”) are insufficient as the sole control for Critical assets.

Exact crypto design is **D4**, not this ADR.

---

### 9. Data leakage

Channels: logs, crash reports, analytics (default **off / forbidden** unless D7 and a later ADR explicitly allow), clipboard, screenshots, notifications, URL query params, third-party CDNs, error messages, support tickets.

**Proposed Phase 1 rule:** No third-party analytics or crash reporters that transmit continuity content or identifiers until explicitly approved under privacy model + threat review.

---

### 10. Backups and recovery

- Backups are equivalent sensitivity to live data.
- Recovery UX must not require permanently weakening at-rest protection for convenience without user-understood trade-off.
- Documented recovery failure modes (user loses all keys) are an availability risk and must be stated honestly in D4/D5.

---

### 11. Encryption requirements (requirements-level, not library-level)

**Proposed requirements** for designs that claim to protect Critical assets:

- Continuity content at rest: protected such that extraction of storage without secrets does not yield plaintext (**how** is D4).
- Secrets never hardcoded; never committed to git ([SECURITY_INTEGRITY.md](../../SECURITY_INTEGRITY.md)).
- In-transit protection whenever data leaves the device.
- Clear statement of what remains in plaintext (e.g., necessary metadata) and why.
- No claim of “encrypted” without specifying threat (against whom).

Algorithm and library choices: **out of scope** for this ADR (D1/D4).

---

### 12. Metadata and privacy risks

Metadata can reveal health appointments, financial activity, or relationship graphs even when bodies are encrypted.  
**Proposed:** D3/D4 must explicitly classify metadata; minimize plaintext metadata exposed to untrusted hosts; document residual leakage as known limitation where unavoidable.

---

### 13. Future AI access to personal data

Vision allows gentle, user-controlled proactivity and possible AI assistance. Threats include:

- Over-broad data sent to external model providers
- Retention of prompts/responses on vendor side
- Model-prompt injection leading to exfiltration via tool calls
- User believing data stays local when it does not

**Proposed principles (binding intent for later ADRs):**

- AI processing of continuity data is **opt-in**, purpose-limited, and disclosed.
- External AI providers are **untrusted integrations** unless a future ADR proves otherwise with evidence.
- Default: do not upload full vault or bulk sensitive categories to third-party AI.
- Phase 1: no AI feature implementation required; principles constrain D2/D4/D7 so architecture does not paint the project into forced cloud AI.

---

### 14. Phase 1 priority threats (must inform D4/D5)

1. Unauthorized read of vault contents at rest (device theft / filesystem access).
2. Weak or bypassable authentication/recovery.
3. Accidental plaintext logging or test fixtures containing secrets.
4. Developer/agent introduction of fake crypto or hardcoded keys (process threat; SECURITY_INTEGRITY.md).
5. Unclear trust boundary leading to server-side plaintext by default.

### 15. Explicitly deferred / residual risk (honest)

| Item | Status |
|------|--------|
| Full resistance to nation-state with hardware implant | **UNKNOWN / NOT VERIFIED** — not a Phase 1 claim |
| Formal verification of crypto proofs | Deferred to D4 + evidence |
| Complete coercion resistance | Limited; UX and social threats remain |
| Integration and AI surfaces | Design constraints now; detailed controls in later phases |
| Multi-user sharing attacks | Design constraints now; implementation Phase 4+ |

---

## Consequences

### Positive

- Gives D4/D5/D2 a concrete adversary and boundary language.
- Aligns long-term vision (integrations, sharing, AI) with security constraints early.
- Supports honest marketing and documentation later (no overclaim).

### Negative / trade-offs

- Constrains architecture (e.g., discourages “server reads everything” convenience).
- Recovery vs security tension must be faced explicitly in D5/D4.
- More design work before coding.

### Neutral

- Threat model will need revision when architecture solidifies; revisions via superseding or amending ADR.

## Security & privacy notes

This ADR **is** the security analysis baseline. It does not implement controls. Acceptance means later ADRs are evaluated against it. Privacy handling details are in **ADR-0002 (D7)**.

## Evidence required before treating implementation as Verified

- Each claimed control in code maps to a threat in this model (traceability note in PR or security doc).
- No claim of protection against a threat listed as deferred/UNKNOWN without new evidence and ADR update.
- Tests or reviews cited for cryptographic and auth claims per SECURITY_INTEGRITY.md (after D4/D5 exist).

## Alternatives not chosen (summary)

- Skipping threat modeling fails governance.
- Generic checklists omit continuity-specific actors (coercion, caregiver abuse, AI exfiltration, integration blast radius).

## References

- [GOVERNANCE.md](../../GOVERNANCE.md) — privacy-first principle
- [SECURITY_INTEGRITY.md](../../SECURITY_INTEGRITY.md)
- [PHASES.md](../../PHASES.md) — Phase 1 objectives
- [docs/PHASE1_DECISIONS.md](../PHASE1_DECISIONS.md) — D6
- Companion: [ADR-0002](0002-privacy-data-handling-model.md) (Proposed)
