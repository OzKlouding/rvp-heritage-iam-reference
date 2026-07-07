## 02 - Threat Model

An identity-centric threat model for the reference architecture. The goal is not an exhaustive enterprise risk assessment but a demonstration of how identity threats are reasoned about and mitigated by design.

## Scope

Threats to the identity plane: provisioning, authentication, authorization, privileged access, and increasingly non-human and AI-agent identities. Framed against a HIPAA-regulated healthcare context (PHI protection) with notes on the financial-services variant (SOX/PCI).

## Key threats and mitigations

| # | Threat | Scenario | Mitigation in this architecture |
|---|--------|----------|--------------------------------|
| T1 | Over-provisioned access | A user accumulates entitlements across role changes (privilege creep) | Group-based RBAC as code; access certification campaigns (roadmap); least-privilege by default |
| T2 | Orphaned accounts | A leaver's access persists after departure | Automated deprovisioning tied to HR source of truth; cross-directory orphan detection (roadmap) |
| T3 | Privileged account abuse | Standing admin rights are compromised or misused | Just-in-time elevation (PIM); break-glass accounts monitored and alerted (roadmap); PAM for service accounts (roadmap) |
| T4 | Credential compromise | Phished or stolen user credentials | Conditional Access + phishing-resistant MFA; risk-based sign-in policy |
| T5 | Federation weakness | Misconfigured SAML/OAuth trust allows token abuse | Signed assertions, audience restriction, short token lifetimes, certificate lifecycle management |
| T6 | Emergency-access misuse | Break-glass account used outside a real emergency | Break-glass excluded from normal policy but heavily monitored; every use triggers an alert and review |
| T7 | Non-human identity sprawl | Service accounts and AI agents operate with unowned, unscoped, standing access | Every non-human identity has a human owner, JIT-scoped permissions, and a revocation (kill-switch) path; governed like any other identity |
| T8 | Unmonitored access drift | Access changes accumulate without detection | IaC change control (all changes version-controlled); log monitoring and KQL detections (roadmap) |

## Emerging focus: AI-agent identity (T7)

The differentiating threat class. As enterprises deploy AI agents that take actions on their behalf, those agents become identities with access to sensitive systems, and most identity programs have no governance model for them. This architecture treats an AI agent as a first-class identity: it must have a human owner, receive just-in-time and least-privilege access, be fully audited, and be instantly revocable. Threat scenarios are mapped against MITRE ATT&CK and the emerging MITRE ATLAS (adversarial AI) framework.

This is the identity problem healthcare and financial services are both beginning to confront, and governing it is a direct extension of established IAM discipline.

## Compliance framing

- Healthcare: threats map to HIPAA Security Rule access-control requirements and HITRUST CSF controls (access management, audit logging, least privilege).
- Finance: the same threats map to SOX access certification, PCI-DSS access restriction, and segregation-of-duties requirements.

The underlying controls are identical; only the compliance mapping changes.