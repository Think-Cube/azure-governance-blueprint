# Azure Platform Governance Template

## Change History

| Version | Date       | Author            | Description                  |
|---------|------------|-----------------|------------------------------|
| 1.0     | 20.02.2026 | Think-Cube | Initial version created      |

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

The document does **not cover Azure AD or identity management governance**. A separate, comprehensive disaster recovery plan should also be developed independently.

---

## 2.0 Management Hierarchy

Management in Azure is organized across four primary levels. This section defines how governance is applied at each level within an organization.

> **Reference:** [CAF Management Levels and Hierarchy](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-setup-guide/organize-resources#management-levels-and-hierarchy)

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
- Deploy Application Insights for all supported services (App Services, Function Apps, etc.).  
- Configure Workspace mode, as the classic model will be deprecated.  
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

#### 7.3.1 Budget Alerts

**Recommendations:**
- Monitor costs actively, especially for serverless or dynamic environments.

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]

---

## 8.0 Disaster Recovery

Ensuring business continuity and rapid recovery is critical.

### 8.1 Infrastructure as Code (IaC) Policy

**Recommendations:**
- Implement all resource deployments via IaC.  
- Prefer Bicep or Terraform templates over manual deployments.  
- Maintain version control and enforce PR-based reviews.

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

[REPLACE THIS PLACEHOLDER WITH YOUR POLICY]
