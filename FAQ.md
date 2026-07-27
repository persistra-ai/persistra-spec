# Frequently Asked Questions (FAQ)

**Common questions about the Persistra Cognitive Standard (PCS)**

---

## General Questions

### What is PCS?

The Persistra Cognitive Standard (PCS) is a specification defining behavioral requirements for AI systems that externalize cognitive state from inference engines into persistent infrastructure.

PCS enables AI systems to maintain continuity, enforce policies deterministically, and preserve state across sessions and model changes.

### Why does PCS matter?

Current AI systems lose state across sessions, enforce policies probabilistically, and create vendor lock-in through model-specific continuity.

PCS solves these problems by defining how cognitive state should persist independently of any specific model or provider.

### Is PCS a product or platform?

No. PCS is a **specification**—like HTTP or SQL.

It defines behavioral requirements that any implementation can satisfy. Multiple vendors can build PCS-compliant systems, and users can switch between them without losing cognitive state.

### Who created PCS?

PCS was developed by Exocortical Concepts Inc. based on production experience building persistent cognitive systems for software engineering.

The specification is designed to be implementation-independent and vendor-neutral.

---

## Technical Questions

### How does PCS differ from RAG (Retrieval-Augmented Generation)?

**RAG:**
- Retrieves documents/chunks to augment prompts
- Advisory (model may ignore retrieved content)
- No enforcement guarantees
- No persistent state across sessions

**PCS:**
- Externalizes cognitive state (decisions, constraints, policies)
- Deterministic enforcement (violations rejected structurally)
- Persistent state across sessions and models
- Model-agnostic continuity

RAG is a retrieval technique. PCS is a cognitive infrastructure specification.

### How does PCS differ from fine-tuning?

**Fine-tuning:**
- Modifies model weights
- Requires retraining for updates
- Model-specific (not portable)
- Expensive ($50K-$500K per domain)

**PCS:**
- Externalizes state to substrate
- Updates without retraining
- Model-agnostic (portable across models)
- No training costs

Fine-tuning changes the model. PCS externalizes state from the model.

### How does PCS differ from prompt engineering?

**Prompt Engineering:**
- Injects context into prompts
- Limited by context windows
- Probabilistic (model may ignore instructions)
- Repeated overhead every turn

**PCS:**
- Persistent state in external substrate
- Unlimited context (salience-based selection)
- Deterministic enforcement
- State stored once, retrieved selectively

Prompt engineering works within model limitations. PCS removes those limitations architecturally.

### Can I use PCS with any AI model?

Yes. PCS is model-agnostic by design.

A PCS-L3 compliant system must preserve cognitive state across different models (e.g., Claude ↔ Llama ↔ GPT).

This is validated by the Cross-Model Cognitive Continuity (CMCC) tests in the CTS.

---

## Conformance Questions

### What are conformance levels?

PCS defines four progressive levels:

- **L1 (Persistence):** State survives sessions
- **L2 (Governance):** Deterministic policy enforcement
- **L3 (Portability):** Model-agnostic continuity
- **L4 (Federation):** Distributed state coordination

Each level is cumulative. See `CONFORMANCE_LEVELS.md` for details.

### How do I know if a system is PCS-compliant?

A system is PCS-compliant if it passes the Persistra Conformance Test Suite (CTS) for the claimed level.

Conformance claims must specify:
- PCS level (L1-L4)
- Specification version
- CTS version
- Validation date

### Where is the Conformance Test Suite?

**Repository:** [persistra-cts](https://github.com/persistra-ai/persistra-cts)

The CTS contains 24 tests with 202+ assertions validating L1-L3 conformance.

### Can I implement PCS myself?

Yes. PCS is a specification, not a product.

You can build your own PCS-compliant system and validate it against the CTS.

Reference implementations:
- **persistra-kernel:** Minimal reference implementation
- **persistra-reference-architecture:** Structural topology

---

## Implementation Questions

### How do I get started implementing PCS?

1. Read `PCS_SUMMARY.md` for overview
2. Review RFCs (RFC-PCS-0001 through RFC-PCS-0007)
3. Study reference implementations (persistra-kernel)
4. Run CTS tests to understand validation
5. Build your implementation
6. Validate against CTS

See `PCS_IMPLEMENTATION_GUIDE.md` for detailed guidance.

### What programming languages can I use?

Any language. PCS is language-agnostic.

The specification defines observable behavior, not implementation details.

Reference implementations exist in JavaScript and C++, but you can use any language.

### Do I need special hardware?

No. PCS can run on standard hardware.

However, some primitives (like salience ranking) may benefit from hardware acceleration (e.g., Tenstorrent).

### What are the performance requirements?

PCS does not specify performance requirements.

Implementations must satisfy behavioral requirements (correctness, determinism, persistence), but performance is implementation-specific.

---

## Licensing and IP Questions

### What is the licensing model?

PCS uses a FRAND (Fair, Reasonable, And Non-Discriminatory) licensing framework.

See `RFC-PCS-0007` for patent disclosure and licensing details.

### Can I use PCS commercially?

Yes, subject to FRAND licensing terms.

Contact Exocortical Concepts Inc. for commercial licensing.

### Are there patent restrictions?

PCS architectural primitives are subject to pending patent applications.

FRAND licensing ensures fair access for implementers.

See `PATENT_NOTICE.md` for details.

### Can I contribute to the specification?

The specification is currently maintained by Exocortical Concepts Inc.

Future versions may include a community governance model.

---

## Ecosystem Questions

### What tools are available?

**Specification:**
- persistra-spec (this repository)

**Validation:**
- persistra-cts (Conformance Test Suite)

**Reference Implementations:**
- persistra-kernel (minimal kernel)
- persistra-reference-architecture (structural topology)
- pcs-runtime (reference runtime)

**Developer Tools:**
- pcs-developer-runtime (tutorial runtime)

### Is there a community?

The PCS ecosystem is in early stages.

As the specification matures and more implementations emerge, a broader community will develop.

### How do I get support?

For specification questions: Review RFCs and documentation in this repository

For implementation help: Study reference implementations

For commercial licensing: Contact research@persistra.ai

---

## Future Roadmap

### What's next for PCS?

**Near-term:**
- L4 (Federation) validation
- Additional reference implementations
- Community engagement

**Long-term:**
- Hardware acceleration standards
- Multi-vendor ecosystem
- Industry adoption

### Will PCS evolve?

Yes. The specification will evolve based on:
- Implementation experience
- Community feedback
- Emerging use cases

Version 1.0.0 (L1-L3) is frozen. Future versions will maintain backward compatibility.

---

## Additional Resources

- **PCS Summary:** `PCS_SUMMARY.md`
- **Conformance Levels:** `CONFORMANCE_LEVELS.md`
- **Implementation Guide:** `PCS_IMPLEMENTATION_GUIDE.md`
- **RFCs:** `rfcs/` directory
- **CTS Repository:** [persistra-cts](https://github.com/persistra-ai/persistra-cts)
