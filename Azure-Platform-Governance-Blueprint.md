# Azure Platform Governance Template

## Change History

| Version | Date       | Author     | Description                                          |
|---------|------------|------------|------------------------------------------------------|
| 1.0     | 20.02.2026 | Think-Cube | Initial version created                              |
| 1.1     | 05.10.2026 | Think-Cube | Updated Azure AD → Microsoft Entra ID; fixed App Insights classic retirement date; added Azure Landing Zones, Container Apps, AKS, AVM, Azure Policy section; expanded Cost Management |

---

## 1.0 Introduction

### 1.1 Purpose

This document establishes the **Azure Platform Governance** framework, outlining strategies, processes, and technologies for building secure and well-managed Azure environments. It provides practical guidance that aligns with both the Microsoft Cloud Adoption Framework (CAF) and the Azure Well-Architected Framework (WAF), focusing specifically on technical implementation and operational aspects for organizations with prior Azure experience.

> **References:**  
> - [Microsoft Cloud Adoption Framework for Azure (CAF)](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework) – Guidance for organizational transformation and cloud adoption readiness.  
> - [Microsoft Azure Well-Architected Framework (WAF)](https://learn.microsoft.com/en-us/azure/architecture/framework/) – Recommendations for developing and managing cloud applications securely and cost-effectively.

**Note:** This template is **not exhaustive** and should be adapted to fit the needs of your organization.

### 1.2 Target Audience

- IT professionals  
- Developers  
- Cloud architects  
This framework assumes prior experience with Azure and focuses on operational and technical governance.

### 1.3 Scope

The document does **not cover Microsoft Entra ID or identity management governance** (formerly Azure Active Directory). For Entra ID governance — including Privileged Identity Management (PIM), Conditional Access, and Identity Protection — refer to the [Microsoft Entra documentation](https://learn.microsoft.com/en-us/entra/). A separate, comprehensive disaster recovery plan should also be developed independently.

---

## 2.0 Management Hierarchy

Management in Azure is organized across four primary levels. This section defines how governance is applied at each level within an organization.

For organizations starting from scratch or scaling to enterprise, the **Azure Landing Zone** architecture is the recommended foundation. It provides pre-built, opinionated configurations for identity, networking, security, and management that align with CAF.

> **References:**
> - [CAF Management Levels and Hierarchy](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-setup-guide/organize-resources#management-levels-and-hierarchy)
> - [Azure Landing Zones](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/) – Proven enterprise-scale reference architectures for Azure environments.

### 2.1 Management Groups

Management Groups provide centralized control for policies, access management, and compliance across multiple subscriptions.

**Guidance:**
- Structure management groups according to business domains, product lines, or environments (e.g., Production, Shared Services, Platform).  
- Apply Azure Policies at the management group level to enforce consistent governance.  
- Limit the number of nested management groups to maintain simplicity and clarity.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 2.2 Subscriptions

Subscriptions act as containers for resource groups and resources, with defined limits and boundaries.

**Guidance:**
- Create separate subscriptions for each product or domain, particularly in large-scale environments.  
- Maintain distinct subscriptions for test or development workloads to manage costs effectively.  
- Consider a shared subscription for central services and infrastructure.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 2.3 Resource Groups

Resource Groups logically organize Azure resources based on lifecycle, purpose, or application.

**Guidance:**
- For microservices or modular architectures, consider separate resource groups per service.  
- Group shared resources by function (e.g., operations, networking).  
- Evaluate resource sharing opportunities where possible (e.g., shared compute resources).

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

---

## 3.0 Naming Convention

A consistent naming convention ensures clarity, discoverability, and enforceability across multiple subscriptions.

> **Reference:** [CAF Resource Naming Guidelines](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming)

### 3.1 Azure Subscriptions

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 3.2 Resource Groups

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 3.3 Resources

> **Reference:** [CAF Resource Abbreviation Examples](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations)

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 3.4 Exceptions

Certain resources may require exceptions to the standard naming convention.

#### 3.4.1 Storage Accounts

Storage accounts do not support separator characters. Remove separators while maintaining meaningful names.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 3.5 Tagging Strategy

Resource tagging enables classification and management across subscriptions and groups.

> **Reference:** [CAF Tagging Strategy](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-tagging)

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

## 4.0 Compliance

This section defines the compliance requirements for the organization, including data residency, logging, and audit processes.

### 4.1 Data Residency

Organizations may have requirements specifying that data must remain within certain geographic boundaries (e.g., EU regions).

#### 4.1.1 Allowed Regions

**Recommendations:**
- Ensure compliance with GDPR and other regulatory requirements.  
- Use Azure Policy to restrict resource deployment to approved regions.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 4.1.2 Approved Global Services

**Recommendations:**
- Enforce restrictions on resource types to comply with regulatory needs.  
- Monitor for unauthorized global services.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 4.2 Logging

#### 4.2.1 Administrative Access Activity

The Azure Activity Log captures subscription-level events, providing audit visibility into operations (who, when, what).

**Recommendations:**
- Export Activity Log data to long-term storage or SIEM systems.  
- Limit access to log storage to authorized personnel only.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 4.2.2 Application Insights

Application Insights enables telemetry and monitoring for applications and services.

**Recommendations:**
- Deploy Application Insights for all supported services (App Services, Function Apps, Container Apps, etc.).
- Use Workspace-based Application Insights only — the classic (non-workspace) model was **retired on February 29, 2024**.
- Link Application Insights to a dedicated Log Analytics Workspace for centralized querying and retention control.
- Adjust data retention to meet organizational requirements.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 4.2.3 Diagnostics Logs

Resource-level diagnostics provide operational logging specific to each resource type (e.g., HTTP logs for App Service, audit logs for IPSecurity).

**Recommendations:**
- Export diagnostic logs to long-term storage (EventHub, Storage Account, or Log Analytics).  
- Maintain a dedicated resource group for log storage.  
- Enforce diagnostic settings via Azure Policy.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

---

## 5.0 Recommendations for Specific Azure Resources

### 5.1 Azure App Configuration

Azure App Configuration centralizes application settings and feature flags.

**Recommendations:**
- Deploy one free instance per subscription where feasible.  
- Enable private endpoints where appropriate.  
- Integrate Key Vault with App Configuration to secure secrets.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 5.2 Azure App Service / Function Apps

**Recommendations:**
- Implement Azure Policies to block FTP access.
- Require HTTPS for all App Service and Function App deployments.
- Use Always On for production App Service plans to prevent cold starts.
- Enforce minimum TLS version 1.2 via Azure Policy.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 5.3 Azure Container Apps

Azure Container Apps is a serverless container platform built on Kubernetes, suitable for microservices, event-driven workloads, and background jobs.

> **Reference:** [Azure Container Apps documentation](https://learn.microsoft.com/en-us/azure/container-apps/)

**Recommendations:**
- Deploy Container Apps into a dedicated Container Apps Environment backed by a VNET for network isolation.
- Use Managed Identity for all outbound service connections (Key Vault, Storage, Service Bus).
- Enable ingress restrictions — expose only the minimum required traffic externally.
- Define CPU and memory limits per container to prevent resource exhaustion.
- Use Dapr where appropriate for service-to-service communication, state management, and pub/sub.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 5.4 Azure Kubernetes Service (AKS)

AKS provides managed Kubernetes for containerized workloads requiring fine-grained control over orchestration.

> **Reference:** [AKS baseline architecture](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks)

**Recommendations:**
- Use the AKS baseline architecture as a starting point for production clusters.
- Enable Microsoft Defender for Containers.
- Use managed node pools with automatic upgrades enabled.
- Restrict cluster API server access to authorized IP ranges or private cluster mode.
- Use Workload Identity (Microsoft Entra Workload ID) instead of pod-managed identity (deprecated).
- Enforce policies via Azure Policy for Kubernetes (Gatekeeper).

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

---

## 6.0 Security

### 6.1 Microsoft Defender for Cloud

Microsoft Defender for Cloud provides security recommendations and ensures best practices for Azure platform security.

**Recommendations:**
- Enable Defender for Cloud across all subscriptions.  
- Activate Defender for SQL, Storage, and other supported services.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 6.2 Application Secrets and Certificate Management

#### 6.2.1 Azure Key Vault

Azure Key Vault manages secrets, certificates, and keys securely.

**Recommendations:**
- Limit Key Vault access to specific networks or IP ranges.  
- Maintain separate Key Vaults for operational and maintenance purposes.  
- Avoid Key Vault references for App Services if Kudu access is granted, to prevent secret exposure.  
- Enable RBAC, access restrictions, soft-delete, and backup plans.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 6.2.2 Managed Identity

Managed Identities provide secure authentication for service-to-service communication without storing credentials.

**Recommendations:**
- Prefer Managed Identity over direct credentials for all supported services.
- Prefer **User-Assigned Managed Identity** over System-Assigned where multiple resources share the same identity or where the identity lifecycle must be managed independently of the resource.
- Use **Workload Identity Federation** for workloads running outside Azure (e.g., GitHub Actions, Azure DevOps pipelines) to authenticate without storing secrets.
- Apply least-privilege RBAC roles to managed identities — avoid Contributor or Owner where a narrower role suffices.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 6.2.3 Secrets and Credentials

**Recommendations:**
- Store all credentials and secrets in Key Vault.  
- Rotate secrets regularly and automate rotation where possible.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 6.2.4 Certificates

**Recommendations:**
- Store all certificates in Key Vault.  
- Automate renewal using Azure Managed Certificates or alternative solutions like Let’s Encrypt.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 6.3 Secret Rotation Policy

**Recommendations:**
- Implement automated rotation for client secrets to enhance security.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 6.4 Customer Managed Keys

**Recommendations:**
- Manage encryption keys centrally using Azure Key Vault.  
- Apply CMK policies across data storage and critical services.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 6.5 Network Security

#### 6.5.1 Web Application Firewall

WAF protects applications from exploits and vulnerabilities.

**Recommendations:**
- Deploy WAF on the central hub subscription.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 6.5.2 Virtual Networks

Virtual Networks provide isolation and secure connectivity.

**Recommendations:**
- Ensure all services reside within VNETs where applicable.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 6.5.3 Private Endpoints

**Recommendations:**
- Use Private Endpoints for sensitive workloads and storage services.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 6.6 Data Protection

#### 6.6.1 Azure SQL Databases

**Recommendations:**
- Disable public network access.  
- Enable Defender for SQL.  
- Use Private Endpoints when possible.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 6.6.2 Azure Cosmos DB

**Recommendations:**
- Restrict public access.  
- Enable Microsoft Defender for Cosmos DB.  
- Use Private Endpoints where applicable.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 6.6.3 Azure Storage Accounts

**Recommendations:**
- Rotate access keys periodically.  
- Use SAS tokens with IP restrictions.  
- Disable public access.  
- Follow Defender for Cloud recommendations.  
- Enable Private Endpoints.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

---

## 7.0 Operational Excellence

### 7.1 Monitoring

#### 7.1.1 Availability Tests

**Recommendations:**
- Implement health check endpoints for each system component.  
- Configure availability tests to alert teams immediately when issues are detected.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 7.1.2 Service Health

**Recommendations:**
- Enable Azure Monitor Service Health alerts to track outages.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 7.1.3 Alerting

**Recommendations:**
- Create centralized alerting workflows (e.g., Logic Apps) to handle metrics and notifications from Azure Monitor.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 7.2 Dashboards

**Recommendations:**
- Use dedicated resource groups for dashboards and workbooks.  
- Create shared dashboards for each system component for visibility.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 7.3 Cost Management

> **Reference:** [Microsoft Cost Management documentation](https://learn.microsoft.com/en-us/azure/cost-management-billing/)

#### 7.3.1 Budget Alerts

**Recommendations:**
- Define budgets at subscription and resource group level with alerts at 80% and 100% of threshold.
- Monitor costs actively, especially for serverless, dynamic, or AI/ML environments where consumption can spike unexpectedly.
- Configure budget alerts to notify both technical and finance stakeholders.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 7.3.2 Cost Allocation

**Recommendations:**
- Enforce a mandatory tagging policy (e.g., `CostCenter`, `Owner`, `Environment`) via Azure Policy to enable cost allocation across teams.
- Use **Azure Cost Management + Billing** views and exports to distribute cost reports per team or product.
- Review and right-size resources monthly — use Azure Advisor cost recommendations as a baseline.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

#### 7.3.3 Cost Anomaly Detection

**Recommendations:**
- Enable **anomaly detection alerts** in Microsoft Cost Management to catch unexpected spend spikes automatically.
- Review anomaly alerts weekly; investigate any deviation above an agreed threshold before month-end.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

---

## 8.0 Disaster Recovery

Ensuring business continuity and rapid recovery is critical.

### 8.1 Infrastructure as Code (IaC) Policy

**Recommendations:**
- Implement all resource deployments via IaC.
- Prefer **Bicep** for Azure-native deployments or **Terraform** for multi-cloud or existing Terraform estates.
- Use **Azure Verified Modules (AVM)** — the official Microsoft-maintained library of reusable Bicep and Terraform modules — as a starting point before writing custom modules.
- Maintain version control and enforce PR-based reviews for all IaC changes.
- Store IaC state (for Terraform) in Azure Storage Account with state locking enabled.
- Use **What-if** (Bicep/ARM) or `terraform plan` in CI pipelines to preview changes before apply.

> **Reference:** [Azure Verified Modules](https://azure.github.io/Azure-Verified-Modules/)

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 8.2 Resource Locks

**Recommendations:**
- Apply locks on critical resources (e.g., VNets, gateways) to prevent accidental deletion or modification.  
- Enforce locks through Azure Policy.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 8.3 Soft Delete

**Recommendations:**
- Enable soft delete for supported resources to mitigate accidental deletion impact.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 8.4 Database Backups

**Recommendations:**
- Implement automated backup policies for all critical databases.
- Test restore procedures periodically.
- Define Recovery Time Objective (RTO) and Recovery Point Objective (RPO) per service and align backup frequency accordingly.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

---

## 9.0 Azure Policy Management

Azure Policy is the primary enforcement mechanism for governance across the Azure platform. It evaluates resources against defined rules and can audit, deny, or automatically remediate non-compliant resources.

> **Reference:** [Azure Policy documentation](https://learn.microsoft.com/en-us/azure/governance/policy/)

### 9.1 Policy Assignment Strategy

**Recommendations:**
- Assign policies at the **Management Group** level for organization-wide enforcement; use subscription or resource group scope only for exceptions.
- Use **Policy Initiatives** (policy sets) to group related policies — prefer built-in initiatives (e.g., Azure Security Benchmark, ISO 27001, NIST SP 800-53) before creating custom ones.
- Set new policies to **Audit** mode first; switch to **Deny** only after validating impact in non-production environments.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 9.2 Built-in Initiatives

Microsoft provides built-in regulatory compliance initiatives that can be assigned out-of-the-box:

- **Microsoft Cloud Security Benchmark (MCSB)** — enabled by default in Defender for Cloud
- **ISO 27001:2013**
- **NIST SP 800-53 Rev. 5**
- **PCI DSS v4**
- **CIS Microsoft Azure Foundations Benchmark**

**Recommendations:**
- Assign the relevant compliance initiative to the root management group to get an organization-wide compliance score.
- Review the compliance dashboard in Defender for Cloud monthly.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 9.3 Remediation

**Recommendations:**
- Configure **remediation tasks** for `deployIfNotExists` and `modify` policies to automatically bring existing resources into compliance.
- Assign a **Managed Identity** to policies that perform remediation — scope its permissions to the minimum required.
- Track remediation progress via the Azure Policy compliance dashboard.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

### 9.4 Exemptions

**Recommendations:**
- Use **policy exemptions** (waiver or mitigated) rather than assigning exclusion scopes, to maintain an audit trail.
- Set an expiry date on all exemptions and review them quarterly.
- Document the business justification for every active exemption.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]
