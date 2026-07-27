# Persistra Cognitive Standard (PCS)

**Normative specification for cognitive infrastructure**

[![RFC DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.21418899-blue)](https://doi.org/10.5281/zenodo.21418899)
[![License](https://img.shields.io/badge/license-Source--Available-blue)](LICENSE)

---

## What is PCS?

**PCS is external cognitive infrastructure for AI systems** - the persistent substrate that lets people and enterprises own cognitive state, keep continuity across models and sessions, and dramatically reduce dependence on context windows, prompt orchestration, and monolithic frontier models.

**This is not a feature, product, or platform. It's an architectural reframe of AI itself.**

This repository contains the normative specification defining conformance requirements for cognitive infrastructure implementations.

---

## 1. Scope

The PCS specification defines conformance requirements for systems that externalize cognitive state from models into persistent infrastructure (exocortex).

PCS does not define model architectures, training techniques, inference strategies, or optimization methods. It defines observable behavioral guarantees regarding the handling of externalized cognitive state.

Conformance is determined exclusively by externally verifiable behavior, not by implementation structure.

## 2. Normative Content

The following documents are normative:

- RFC-PCS-0001 — Overview and Scope
- RFC-PCS-0002 — Cognitive State Semantics
- RFC-PCS-0003 — Cross-Model Cognitive Continuity (CMCC)
- RFC-PCS-0004 — Conformance Test Suite Requirements (PCS-CTS)
- RFC-PCS-0005 — Reference Implementation Requirements
- RFC-PCS-0006 — Certification Program and Mark Usage
- RFC-PCS-0007 — Patent Disclosure and FRAND Licensing Framework
- CONFORMANCE_LEVELS.md
- Versioned snapshots under /versions/

These documents define required behaviors using normative language (MUST, SHOULD, MAY).

Implementations claiming PCS conformance MUST satisfy all requirements for the declared conformance level.

## 3. Conformance Levels

PCS defines four conformance levels:

- L1 — Persistence (Persistent cognitive state and session continuity)
- L2 — Deterministic Governance (Policy enforcement)
- L3 — Cross-Model Cognitive Continuity (CMCC)
- L4 — Federation (Distributed cognitive state)

Current validation status is defined in CONFORMANCE_LEVELS.md.

Conformance claims MUST reference a specific PCS version and conformance level.

## 4. Informative Content

The following documents are informative:

- PCS_SUMMARY.md
- PCS_IMPLEMENTATION_GUIDE.md
- FAQ.md
- COMPARISON.md
- LIMITATIONS.md

Informative documents provide context and guidance but do not modify normative requirements.

## 5. Relationship to Other Repositories

PCS is part of the Persistra ecosystem:

- persistra-cts — Conformance Test Suite (authoritative validation)
- persistra-kernel — Minimal reference implementation (informative)
- persistra-reference-architecture — Structural topology documentation (informative)

The specification is authoritative. Implementations are illustrative.

## 6. Versioning

Each PCS release is versioned under /versions/ and tagged in Git.

Conformance claims MUST specify:
- PCS version
- Conformance level
- CTS version used for validation

## 7. Citation

If you reference the PCS RFC specifications, please cite:

**Mansfield, S. (2026).** *Persistra Cognitive Standard (PCS) RFC Specifications* (Version 1.1). Zenodo. https://doi.org/10.5281/zenodo.21418899

```bibtex
@misc{mansfield2026pcs_rfcs,
  author       = {Mansfield, Stephen},
  title        = {Persistra Cognitive Standard (PCS) RFC Specifications},
  year         = {2026},
  publisher    = {Zenodo},
  version      = {1.0},
  doi          = {10.5281/zenodo.21418899},
  url          = {https://doi.org/10.5281/zenodo.21418899}
}
```

**For the research paper validating PCS:**

**Mansfield, S. (2026).** *The Model is Not the Mind: From Stateless Inference to Long-Horizon Cognition* (Version v2.0 — corrected preprint). Zenodo. https://doi.org/10.5281/zenodo.21071446

## 8. Intellectual Property

PCS is developed by Exocortical Concepts Inc.

See INTELLECTUAL_PROPERTY_NOTICE.md and RFC-PCS-0007 for intellectual property information.

## 9. Status

Normative content may evolve until version 1.0.0 is declared stable.
