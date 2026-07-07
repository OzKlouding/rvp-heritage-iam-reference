# RVP Heritage Group — Identity & Access Management Reference Architecture

**Enterprise identity governance, provisioned as code, on the platforms regulated enterprises run.**

`Microsoft Entra ID` · `Azure` · `Terraform` · `SailPoint` · `Okta` · `AWS IAM` · `CyberArk` · `PowerShell` · `Python` · `HIPAA / HITRUST` · `SOX / PCI-DSS` · `Zero Trust` · `Non-Human & AI-Agent Identity`

**Primary cloud: Microsoft Azure / Entra ID.** **Multi-cloud reach: AWS via Entra-federated identity (roadmap).**

---

> **What this is:** A working reference architecture built by **RVP Heritage Group LLC**, a cloud security and IAM consulting firm. It demonstrates identity provisioning and governance as infrastructure-as-code, modeled on a representative healthcare client (**"Heritage Health Systems,"** simulated) with a financial-services variant for cross-vertical portability.
>
> **What this is not:** A live client engagement. "Heritage Health Systems" is a demonstration persona. All identities and data are **synthetic**. This is a reference architecture, not delivered client work.

---

## Why a hiring manager should keep reading

Most IAM portfolios prove someone can click through a tool. This one manages identity **as code**  version-controlled, reproducible, auditable and documents the **design reasoning** behind each decision. It also addresses the identity problem enterprises are racing to solve now: **non-human and AI-agent identity governance**, not just the human-identity problems the field solved years ago.

**Build status (honest):** The Terraform + Entra foundation is built and working — remote Azure state backend plus user and group provisioning modules. Governance, federation, PAM, and compliance modules are on the roadmap below. This is an actively developed environment.

---

## What is built today

| Component | Status | What it does |
|-----------|--------|--------------|
| `infra/` Terraform IaC | Built | Root composition, Azure providers, remote state |
| Azure remote state backend | Built | Terraform state in Azure Blob (`rg-iam-tfstate`) |
| `infra/modules/entra-user` | Built | Automated Entra ID user provisioning |
| `infra/modules/entra-group` | Built | Entra group + membership management (RBAC grouping) |
| `scripts/bootstrap_state_storage.sh` | Built | Bootstraps the Azure state storage |
| `docs/` | Built | Overview, architecture, threat model |

## Documentation

- **[docs/00-overview.md](docs/00-overview.md)** — what this is and the cloud/identity approach
- **[docs/01-architecture.md](docs/01-architecture.md)** — real Terraform structure + target architecture
- **[docs/02-threat-model.md](docs/02-threat-model.md)** — identity threat model incl. AI-agent identity
- **[docs/STATE_BACKEND.md](docs/STATE_BACKEND.md)** — Terraform state backend detail

---

## Roadmap

Modeled across both regulated verticals — the engineering is identical; only compliance mapping and entitlement labels change.

- [x] Terraform IaC foundation + Azure remote state
- [x] Entra user provisioning module
- [x] Entra group management module
- [ ] Access certification campaigns (SailPoint)
- [ ] Break-glass emergency access (monitored)
- [ ] Okta access layer (SSO / MFA / adaptive)
- [ ] Entra-federated AWS (multi-cloud reach)
- [ ] Privileged access governance (CyberArk / Vault)
- [ ] Automation (PowerShell + Python, cross-directory orphan detection)
- [ ] Non-human & AI-agent identity governance
- [ ] Compliance mapping (HITRUST/HIPAA · SOX/PCI-DSS) + Sentinel detections

> **EHR fluency (roadmap):** a design doc for onboarding an Epic-style EHR into the identity fabric for SSO and provisioning — demonstrating healthcare-system integration understanding without proprietary Epic access.

---

## About RVP Heritage Group LLC

**Cloud Security & Identity Access Management consulting.** Texas LLC. Registered federal vendor (SAM.gov, CMBL). Available for C2C contract and prime-contractor teaming.

**Principal — Osman Sharif II**
7+ years enterprise IAM and cloud security consulting across defense, healthcare, telecom, and manufacturing. Fortune 500 delivery including **McKesson, AT&T, L3Harris, and Dow.**

**Core competencies:** Microsoft Entra ID / Azure identity (primary depth — Conditional Access, PIM, lifecycle), IAM-as-Code (Terraform), Identity Governance (SailPoint), Access Management (Okta), multi-cloud IAM via Entra-federated AWS, Privileged Access (CyberArk), automation (PowerShell, Python), and non-human / AI-agent identity governance.

**Certifications:** AZ-104, AZ-305, AZ-700, Terraform Associate. *(Okta Professional, SC-300, and SailPoint credentials in progress.)*

Contact: osman.sa.sharif@gmail.com · LinkedIn: https://www.linkedin.com/in/osman-sharif/

---

*Reference architecture for demonstration. All client personas simulated; all data synthetic. © 2026 RVP Heritage Group LLC.*
