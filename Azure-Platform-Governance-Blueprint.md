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
