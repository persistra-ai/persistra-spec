# PCS Limitations and Non-Goals

**What PCS does NOT specify**

---

## Overview

PCS is a specification for cognitive infrastructure, not a complete AI system. This document clarifies what PCS does and does not address.

---

## What PCS Does NOT Specify

### 1. Model Architectures

**PCS does not specify:**
- Model training methods
- Neural network architectures
- Tokenization strategies
- Embedding generation algorithms
- Inference optimization techniques

**Why:** PCS is model-agnostic. Any model can work with PCS-compliant infrastructure.

---

### 2. Performance Requirements

**PCS does not specify:**
- Latency targets
- Throughput requirements
- Memory usage limits
- Scalability thresholds

**Why:** Performance is implementation-specific. PCS defines behavioral correctness, not performance characteristics.

**Note:** Implementations should document their performance characteristics separately.

---

### 3. User Interfaces

**PCS does not specify:**
- Application UIs
- Developer tools
- Monitoring dashboards
- Configuration interfaces

**Why:** UI is application-specific. PCS defines infrastructure behavior, not presentation.

---

### 4. Business Models

**PCS does not specify:**
- Pricing strategies
- Licensing terms (beyond FRAND framework)
- Service level agreements
- Support models

**Why:** Business models are implementation-specific.

---

### 5. Deployment Environments

**PCS does not specify:**
- Cloud vs. on-premise deployment
- Container orchestration
- Network topology
- Hardware requirements

**Why:** PCS is deployment-neutral. Implementations can run anywhere.

---

### 6. Programming Languages

**PCS does not specify:**
- Implementation languages
- API design
- SDK structure
- Library interfaces

**Why:** PCS is language-agnostic. Implementations can use any language.

---

### 7. Storage Backends

**PCS does not specify:**
- Database choices
- File system requirements
- Caching strategies
- Replication methods

**Why:** Storage is implementation-specific. PCS defines what must be stored, not how.

---

### 8. Security Mechanisms

**PCS does not specify:**
- Authentication methods
- Authorization models
- Encryption algorithms
- Key management

**Why:** Security is implementation-specific, though PCS enables audit trails that support security.

**Note:** Implementations should follow security best practices for their deployment environment.

---

### 9. Networking Protocols

**PCS does not specify:**
- Communication protocols
- API formats (REST, gRPC, etc.)
- Message serialization
- Network security

**Why:** Protocol choices are implementation-specific.

---

### 10. Optimization Strategies

**PCS does not specify:**
- Caching strategies
- Prefetching algorithms
- Compression methods
- Index structures

**Why:** Optimizations are implementation-specific.

---

## Known Limitations

### 1. L4 (Federation) Validation Pending

**Status:** Specification complete, validation not yet implemented

**Impact:** L4 conformance cannot yet be claimed

**Timeline:** Future CTS release

---

### 2. Hardware Acceleration Not Standardized

**Status:** Research exploration (Tenstorrent) underway

**Impact:** No standard hardware acceleration interface yet

**Timeline:** Future specification versions may address this

---

### 3. Multi-Tenancy Not Specified

**Status:** Not addressed in current specification

**Impact:** Implementations must design their own multi-tenancy models

**Timeline:** May be addressed in future versions

---

### 4. Real-Time Guarantees Not Specified

**Status:** PCS defines correctness, not timing

**Impact:** Real-time systems must verify timing separately

**Timeline:** May be addressed in future versions for specific use cases

---

### 5. Conflict Resolution Not Fully Specified

**Status:** L4 defines requirements but not algorithms

**Impact:** Implementations must choose conflict resolution strategies

**Timeline:** Future versions may provide more guidance

---

## Future Work

### Potential Future Additions

**Under consideration for future specification versions:**

1. **Hardware Acceleration Standards**
   - Standard interfaces for DPU/NPU/IPU acceleration
   - Performance benchmarking methodology

2. **Multi-Tenancy Guidelines**
   - Isolation requirements
   - Resource allocation
   - Security boundaries

3. **Real-Time Extensions**
   - Timing guarantees for safety-critical systems
   - Deterministic scheduling

4. **Federation Protocols**
   - Standard protocols for L4 implementations
   - Interoperability between vendors

5. **Observability Standards**
   - Metrics and monitoring
   - Debugging interfaces
   - Performance profiling

---

## What PCS DOES Specify

**For clarity, PCS specifies:**

1. **Behavioral Requirements**
   - Persistent cognitive state
   - Deterministic policy enforcement
   - Cross-session continuity
   - Model-agnostic interoperability

2. **Conformance Levels**
   - L1: Persistence
   - L2: Governance
   - L3: Portability
   - L4: Federation

3. **Validation Methodology**
   - CTS test suite requirements
   - Conformance claim format
   - Validation procedures

4. **Intellectual Property Framework**
   - FRAND licensing
   - Patent disclosure
   - Certification program

---

## Guidance for Implementers

### What You Must Implement

- All behavioral requirements for your claimed conformance level
- Pass CTS tests for your claimed level
- Follow FRAND licensing terms

### What You Can Choose

- Programming language
- Storage backend
- Performance characteristics
- Deployment environment
- API design
- Security mechanisms
- Optimization strategies

### What You Should Document

- Performance characteristics
- Security model
- Deployment requirements
- API interfaces
- Limitations of your implementation

---

## Relationship to Other Specifications

PCS is intentionally narrow in scope. It complements other specifications:

- **Security:** Follow industry standards (OAuth, TLS, etc.)
- **Networking:** Use standard protocols (HTTP, gRPC, etc.)
- **Storage:** Use appropriate databases for your use case
- **Monitoring:** Use standard observability tools

PCS focuses on cognitive infrastructure behavior, not the full system stack.

---

## Questions?

If you're unsure whether something is in scope for PCS:

1. Check the RFCs (RFC-PCS-0001 through RFC-PCS-0007)
2. Review the CTS tests (what's tested is in scope)
3. See FAQ.md for common questions
4. Contact: research@persistra.ai

---

## Summary

**PCS is a focused specification for cognitive infrastructure.**

It defines what cognitive state must persist and how it must behave, but leaves implementation details to builders.

This narrow scope enables:
- Multiple implementations
- Innovation in optimization
- Deployment flexibility
- Language/platform neutrality

**PCS provides the foundation. You build the system.**
