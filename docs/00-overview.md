# 00 - Overview

## What this is

This repository is the Identity & Access Management reference architecture of RVP Heritage Group LLC, a cloud security and IAM consulting firm. It demonstrates how RVP designs, provisions, and governs enterprise identity using infrastructure-as-code on the platforms regulated enterprises actually run.

The environment is modeled on a representative healthcare client, "Heritage Health Systems" (a simulated HIPAA-regulated organization), with a financial-services variant to demonstrate that the same architecture serves multiple regulated verticals.

> This is a reference architecture, not a delivered client engagement. "Heritage Health Systems" is a demonstration persona. All identities and data are synthetic. Nothing here represents real client work or real production data.

## Cloud and identity approach

Primary plane: Microsoft Azure / Entra ID. Identity governance, provisioning, and access control are anchored in Entra, managed as code with Terraform. Terraform state is stored remotely in Azure Blob Storage (see STATE_BACKEND.md).

Multi-cloud reach: AWS via Entra-federated identity (roadmap). AWS is integrated with Entra as the identity provider, demonstrating governance of a second cloud from a single identity source of truth, the pattern real hybrid enterprises run.

## What is built today

- Terraform IaC foundation (`infra/`) with remote Azure state backend
- `entra-user` module: automated Entra user provisioning
- `entra-group` module: Entra group management with membership
- State bootstrap automation (`scripts/`)

## What is on the roadmap

Access certification, break-glass emergency access, Okta access layer, Entra-federated AWS, privileged access governance, automation (PowerShell/Python), non-human & AI-agent identity governance, and compliance control mapping (HITRUST/HIPAA and SOX/PCI-DSS). See the repository README for full status.

## Who built it

Osman Sharif II: 7+ years enterprise IAM and cloud security consulting across defense, healthcare, telecom, and manufacturing, including Fortune 500 delivery (McKesson, AT&T, L3Harris, Dow). Azure-certified (AZ-104, AZ-305, AZ-700) and Terraform Associate, with SailPoint, Okta, and SC-300 credentials in progress.