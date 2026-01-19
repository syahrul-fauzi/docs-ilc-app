# Risk Assessment Matrix - ILC-APP

This document identifies potential security risks and the controls implemented to mitigate them.

## 1. Risk Matrix

| Risk ID | Vulnerability | Impact | Likelihood | Risk Level | Mitigation Control | Status |
|---------|---------------|--------|------------|------------|-------------------|--------|
| SEC-001 | Unauthorized Access to PII | High | Medium | High | RBAC-based PII masking/unmasking. Encryption at rest (AES-256). | Implemented |
| SEC-002 | SQL Injection / NoSQL Injection | High | Low | Medium | Use of ORM/Typed clients. Input validation at API gateway. | Implemented |
| SEC-003 | Session Hijacking | Medium | Medium | Medium | TLS 1.2+ in transit. 15-minute inactivity timeout. | Implemented |
| SEC-004 | AI Prompt Injection | Medium | Medium | Medium | Input sanitization for AI queries. System prompt hardening. | Implemented |
| SEC-005 | Cross-Border Data Leakage | High | Low | Medium | Jurisdiction detection and data residency compliance. | Implemented |

## 2. Compliance Checklist (GDPR/PDPA)

- [x] **Right to Access**: Users can view their profile and billing history.
- [x] **Data Minimization**: Only essential PII is collected.
- [x] **Security by Design**: RBAC and encryption implemented from the start.
- [x] **Jurisdiction Awareness**: Automated checks for SG/MY legal restrictions.

## 3. Remediation Timeline

- **OWASP Top 10 Scan**: Scheduled weekly.
- **PII Audit**: Conducted monthly.
- **Key Rotation**: Every 90 days.
