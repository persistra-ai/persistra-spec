# Security Policy

## Reporting Security Issues

**We take security seriously.** If you discover a security issue in the PCS specifications, please report it responsibly.

### How to Report

**Email:** security@persistra.ai

**Please include:**
- Description of the issue
- Affected RFC(s)
- Potential impact
- Suggested clarification or fix

**Response time:** We aim to acknowledge reports within 48 hours and provide a detailed response within 7 days.

### Scope

This security policy applies to:
- RFC specifications and their security implications
- Conformance requirements
- Security-relevant guidance in specifications

### Out of Scope

- Implementation vulnerabilities (report to implementation maintainers)
- Theoretical attacks without proof of concept
- Editorial issues (use GitHub issues for non-security editorial feedback)

---

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

---

## Security Considerations in Specifications

**The PCS RFC series includes security considerations sections** that address:
- Threat models for cognitive infrastructure
- Security boundaries and trust assumptions
- Cryptographic requirements
- Audit trail integrity
- Access control patterns

**If you identify a security gap in the specifications**, please report it so we can issue an errata or updated RFC.

---

## Vulnerability Disclosure Timeline

**If a specification security issue is confirmed:**

1. **Day 0:** Acknowledgment sent to reporter
2. **Day 1-7:** Validation and impact assessment
3. **Day 7-30:** Errata or RFC update development
4. **Day 30:** Coordinated disclosure (if applicable)
5. **Day 30+:** Public disclosure and specification update

**We follow responsible disclosure practices** and will credit reporters (unless anonymity is requested).

---

## Security Contacts

**Security issues:** security@persistra.ai  
**Specification questions:** research@persistra.ai  
**Standards body inquiries:** licensing@persistra.ai

---

## Additional Resources

- [RFC-PCS-0001](rfcs/RFC-PCS-0001_OverviewAndScope.md) - Overview and scope
- [RFC-PCS-0004](rfcs/RFC-PCS-0004_ConformanceTestSuiteRequirements.md) - Conformance testing
- [persistra-cts](https://github.com/persistra-ai/persistra-cts) - Reference implementation

---

**Last Updated:** July 2026  
**Version:** 1.0.0
