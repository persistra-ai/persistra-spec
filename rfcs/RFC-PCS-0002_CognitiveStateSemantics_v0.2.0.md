RFC-PCS-0002

Cognitive State Semantics
Version: 0.2.0
Status: Draft
Intended Status: Standards Track
Updates: RFC-PCS-0001
Expires: 2027-03-22 (six months from publication; renew on revision)

Changelog:
- Version 0.2.0 (2026-09-22): Added Section 4.6 (Epistemic Gate State), Section 4.7 (Enforcement Trace State), Section 4.8 (Salience-Based Selection State); clarified traceability requirements in Section 4.2. The added schemas close three proof boundaries identified during external architecture review: replay prevention, inline gate execution, and the PEP-to-CSE flow.
- Version 0.1.0 (Initial draft)

1. Status of This Document

This document defines normative semantic requirements for cognitive state types under the Persistent Cognitive Substrate (PCS).

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, NOT RECOMMENDED and MAY in this document are to be interpreted as described in BCP 14 (RFC 2119 and RFC 8174) when, and only when, they appear in all capitals, as shown here.

Conformance to this RFC is determined exclusively by observable behavior as validated by the Persistent Cognitive Substrate Conformance Test Suite (PCS-CTS).

This document does not prescribe internal data structures, field names, storage engines, serialization formats, or registry mechanisms. Where Section 4 lists schema elements, the element names are illustrative; a conformant implementation MUST preserve the semantics of each listed element, and equivalent representations are conformant under Section 5.

2. Scope

This RFC defines:
- The required semantic categories of persistent cognitive state.
- The behavioral guarantees associated with each category.
- The interoperability requirements governing state portability and exchange.

This RFC does not define:
- A required record structure.
- A required serialization format.
- A required storage topology.
- A required registry implementation.

3. General Requirements for Persistent Cognitive State

All PCS-compliant systems:
1. MUST maintain persistent cognitive state independently of transient model execution context.
2. MUST preserve state across sessions, process restarts, and model transitions.
3. MUST provide stable identity for persistent state elements.
4. MUST ensure that state mutation is governed by deterministic policy evaluation.
5. MUST support export and import of cognitive state without semantic loss.

These requirements are behavioral and are agnostic to representation.

4. Required Semantic State Categories

PCS implementations MUST support the following semantic state categories.

The internal representation of these categories is implementation-defined.

4.1 Decision State

Decision state represents durable architectural, operational, or contextual determinations that influence future behavior.

A PCS implementation:
1. MUST support durable persistence of decisions.
2. MUST NOT allow retroactive mutation of committed decisions.
3. MUST provide stable identity for each decision element.
4. MUST retain sufficient metadata to establish provenance and temporal ordering.
5. MUST ensure decisions remain retrievable independent of conversational history.

The mechanism used to enforce immutability is implementation-defined.

4.2 Policy State

Policy state represents enforceable constraints governing system behavior.

A PCS implementation:
1. MUST evaluate policy deterministically prior to output emission.
2. MUST prevent outputs that violate active policy state.
3. MUST support policy updates subject to governance rules.
4. MUST provide traceability between policy evaluation and enforcement outcome, including structured enforcement metadata as defined in Section 4.7.
5. MUST preserve policy continuity across sessions and model transitions.

The method of policy representation is implementation-defined.

4.3 Intent State

Intent state represents long-lived guiding constraints or mission-level invariants.

A PCS implementation:
1. MUST support persistence of intent state across sessions and model transitions.
2. MUST ensure intent state constrains downstream decision and policy evaluation.
3. MUST ensure that transient contextual input does not override persistent intent state unless explicitly governed.
4. MUST provide stable identity and governance for intent state elements.
5. MUST ensure intent state is evaluated prior to action commitment.

This RFC does not mandate a specific representation or priority mechanism.

4.4 Identity-Scoped State

Identity-scoped state represents cognitive state partitioned by namespace, tenant, user, or agent identity.

A PCS implementation:
1. MUST provide isolation between identity scopes.
2. MUST prevent cross-scope state leakage.
3. MUST support explicit scope resolution during state retrieval.
4. MUST preserve scope boundaries during state export and import.

Namespace implementation details are not prescribed.

4.5 Provenance and Audit State

Provenance state represents traceability information associated with cognitive state.

A PCS implementation:
1. MUST maintain traceability metadata sufficient to reconstruct state lineage.
2. MUST record state creation and mutation events.
3. MUST support deterministic replay of state transitions where applicable.
4. MUST ensure audit artifacts are tamper-evident.
5. MUST preserve provenance during export and import.

The storage mechanism for audit data is implementation-defined.

4.6 Epistemic Gate State

Epistemic gate state represents validation tokens and state requirements that govern model invocation based on state availability.

A PCS implementation:
1. MUST support validation of required state classes before model invocation.
2. MUST generate cryptographically verifiable gate tokens when required state is present.
3. MUST prevent model invocation when required state classes are missing (fail-closed behavior).
4. MUST include replay prevention in gate tokens via nonce tracking.
5. MUST maintain persistent tracking of used nonces to prevent token reuse.
5a. MUST reject tokens whose timestamp falls outside the accepted validity window, and MUST retain used nonces for at least the length of that window, so that pruning can never reopen a replay path.
6. MUST provide deterministic blocking when gate validation fails.
7. MUST emit trace evidence of gate evaluation outcomes.

Note: Requirement 5a retains its current numbering in v0.2.0 to preserve test name and matrix row stability. It will be renumbered to requirement 6 in v0.3.0, with subsequent requirements renumbered accordingly.

Gate token schema. A conformant gate token MUST carry the following elements (names illustrative); see Section 1: nonce (unique identifier preventing replay; REQUIRED); timestamp (ISO 8601 creation time; REQUIRED); required_state_classes (array of state class identifiers; REQUIRED); signature (cryptographic integrity protection; REQUIRED); metadata (OPTIONAL).

Nonce tracking. An implementation MUST persist used nonces across application restarts, MUST reject tokens with previously used nonces, MUST support automatic pruning of expired nonces (age-based or count-based), subject to requirement 5a, and MUST maintain nonce tracking independently of session state. The cryptographic mechanism and nonce storage format are implementation-defined.

4.7 Enforcement Trace State

Enforcement trace state represents structured metadata capturing policy enforcement decisions and their outcomes.

A PCS implementation:
1. MUST record enforcement decisions when policy violations are detected, and SHOULD record allowed outcomes as well, so that replay can show a policy was evaluated and held.
2. MUST capture sufficient metadata to reconstruct enforcement reasoning.
3. MUST maintain enforcement counters for decisions and policies.
4. MUST timestamp enforcement events.
5. MUST ensure enforcement metadata is tamper-evident.
6. MUST support retrieval of enforcement history for audit purposes.
7. If salience-based selection (Section 4.8) is implemented, MUST feed enforcement metadata into authority calculations.

Enforcement trace schema. A conformant enforcement trace MUST carry the following elements (names illustrative) enforcement_decision (boolean, whether output was blocked; REQUIRED); violated_policy and violated_terms (REQUIRED when blocked); action (e.g., "blocked", "allowed"; REQUIRED); timestamp (ISO 8601; REQUIRED); decision_id and policy_id (OPTIONAL).

Enforcement counters. An implementation MUST maintain enforcement_count per decision and per policy, MUST increment counters atomically, MUST persist counters across restarts, and MUST provide retrieval of enforcement metadata including counters and timestamps. The storage mechanism is implementation-defined.

4.8 Salience-Based Selection State

Salience-based selection state represents deterministic prioritization of state under memory or context constraints. It exists so that what the model is shown under a constraint is decided by the substrate, reproducibly, rather than by the model or by chance.

A PCS implementation that supports contextual salience:
1. MUST calculate salience scores deterministically from defined factors.
2. MUST support configurable weighting of salience factors (recency, importance, authority).
3. MUST ensure salience calculation is substrate-resident (not model-selected).
4. MUST select highest-salience items when under constraint.
5. MUST emit trace evidence of selection decisions.
6. MUST ensure selection is reproducible given identical inputs and configuration.
7. MAY incorporate enforcement history into authority calculations.

Salience calculation. A conformant calculation MUST use deterministic algorithms (no randomness in selection), MUST support at minimum recency decay and importance weighting, MUST emit evidence including total candidates, selected count, and selection strategy, and MUST preserve highest-salience items under constraint.

Selection evidence schema. A conformant selection trace MUST carry the following elements (names illustrative): strategy (REQUIRED); totalCandidates (REQUIRED); maxItems (REQUIRED); selectedCount (REQUIRED); selectedIds (REQUIRED); highestSalienceRetained (boolean; REQUIRED); deterministic (boolean; REQUIRED, MUST be true). It MAY include highestSalience, lowestSalience, and avgSalience.

Authority weighting (optional). If implemented: authority MUST be derived from enforcement metadata (enforcement_count, violation_attempts) and calculated deterministically; the authority weight MUST appear in the salience configuration; the weighting configuration MUST be documented, and where weighted sums are used, weights SHOULD be normalized to sum to 1.0. The salience algorithm and weighting formula are otherwise implementation-defined, provided they meet the determinism and traceability requirements above.

5. Interoperability Requirements

PCS-compliant systems MUST support semantic interoperability of cognitive state.

Specifically:
1. Implementations MUST support export of cognitive state in a form that preserves:
   - Stable identity
   - Category semantics
   - Governance constraints
   - Provenance metadata
2. Implementations MUST support import of compliant cognitive state without semantic degradation.
3. Interoperability MUST NOT depend on shared model internals.
4. Equivalent representations that preserve required semantics MUST be considered conformant, even if structural formats differ.
5. Conformance is determined by semantic equivalence, not by structural equivalence.

This RFC does not mandate a registry, schema format, or canonical serialization mechanism.

6. Extensibility

PCS implementations:
1. MAY define additional state categories beyond those required in Section 4.
2. MUST NOT redefine the semantics of required categories.
3. MUST ensure extensions do not compromise required isolation, immutability, governance, or interoperability guarantees.
4. MUST ensure extensions are namespace-safe and do not collide with required semantic categories.

7. Conformance

A system claiming conformance to RFC-PCS-0002:
1. MUST satisfy all normative requirements in Sections 3–6. except as conditioned below for Sections 4.6 through 4.8
2. MUST pass corresponding tests in the PCS Conformance Test Suite (CTS).
3. MUST declare its conformance level (L1–L4) as defined in RFC-PCS-0001.

A system claiming conformance to RFC-PCS-0002 v0.2.0:
1. MUST implement Section 4.6 (Epistemic Gate State) if claiming epistemic gating capability.
2. MUST implement Section 4.7 (Enforcement Trace State) if claiming policy enforcement capability.
3. MAY implement Section 4.8 (Salience-Based Selection State) as an optional enhancement.
4. MUST pass corresponding tests in the PCS Conformance Test Suite (CTS) for claimed capabilities.

Failure to meet any REQUIRED or MUST-level obligation constitutes non-conformance.

8. Security Considerations

Implementations:
1. MUST protect cognitive state against unauthorized modification.
2. MUST ensure isolation boundaries are enforced.
3. SHOULD implement cryptographic integrity protection for exported state.
4. SHOULD implement access control mechanisms aligned with policy state.

Epistemic gate security. Gate tokens MUST use cryptographic integrity protection to prevent tampering; nonce tracking MUST be persistent and tamper-evident; implementations MUST bound the replay window by the token validity window defined in Section 4.6, requirement 5a.

Enforcement trace security. Enforcement metadata MUST be tamper-evident; enforcement counters MUST be protected against unauthorized modification; implementations SHOULD use cryptographic signatures for enforcement traces.

This section defines required security outcomes, not specific security mechanisms.

9. Relationship to Intellectual Property

PCS is an open architectural specification.
However, certain implementations of PCS requirements may be subject to existing or pending intellectual property rights.

Implementers are responsible for ensuring appropriate licensing where required.
This approach aligns with historical standards where open specifications coexist with licensed essential patents.

10. Future Work
Hardware-level enforcement and computational parity of substrate primitives on accelerator silicon (conformance level L4) are outside the scope of this version and are reserved for future work. Phase 1 numerical equivalence against a TT-Metalium-targeted reference has been demonstrated; on-silicon execution has not been specified or validated.

11. Conclusion

This RFC defines the semantic foundation for persistent cognitive state in AI systems.

By specifying required behaviors rather than required structures, PCS enables diverse implementations while ensuring interoperability, auditability, and governance.

End of RFC-PCS-0002 v0.2.0
