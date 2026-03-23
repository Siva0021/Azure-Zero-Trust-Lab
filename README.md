# Azure-Zero-Trust-Lab
Build a secure environment where access is never "trusted" by default. You will demonstrate how to protect Blob Storage and VMs using identity-based security rather than just passwords.
# Azure Zero-Trust Identity & Security Lab
[![Azure](https://img.shields.io)](https://azure.microsoft.com)
[![Security](https://img.shields.io)](https://azure.microsoft.comen-us/solutions/zero-trust/)

## 📌 Project Overview
This project demonstrates a **Zero-Trust Security Architecture** within Microsoft Azure. The goal was to move away from traditional perimeter-based security and implement identity-driven access controls for cloud infrastructure.

## 🛠 Tech Stack & Services
*   **Identity**: Entra ID (Azure AD), Conditional Access, MFA.
*   **Compute**: Linux VM (Ubuntu) with System-Assigned Managed Identity.
*   **Storage**: Azure Blob Storage (IAM-only access).
*   **Governance**: Azure Role-Based Access Control (RBAC).
*   **Monitoring**: Log Analytics Workspace & KQL.

## 🔒 Implemented Security Features
1.  **Conditional Access Policies**: Enforced MFA for all administrative actions and blocked legacy authentication protocols.
2.  **Managed Identities**: Configured a VM to access Storage Blobs via a **System-Assigned Identity**, eliminating the need for connection strings or stored passwords.
3.  **Storage Hardening**: Disabled Public Access and Storage Account Key access, forcing all requests to be authorized via Entra ID.
4.  **Least Privilege**: Assigned the `Storage Blob Data Reader` role specifically to the VM identity, following the principle of least privilege.

## 📊 Architecture Diagram
![Architecture Diagram](path-to-your-image.png)
*(Note: Upload your Draw.io or Lucidchart export here)*

## 🚀 How to Deploy
I have included an **Azure CLI** script (`deploy-lab.sh`) in this repo to automate the environment setup:
1. Login: `az login`
2. Run script: `./deploy-lab.sh`

## 📈 Monitoring & Auditing
I used **Kusto Query Language (KQL)** to monitor sign-in logs. Example query used to find unauthorized access attempts:
```kql
SigninLogs

| where ResultType != 0
| summarize count() by UserPrincipalName, IPAddress, Location
