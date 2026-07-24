# Sprint 2 – Enterprise RBAC

**Phase:** Phase 1 – Identity Foundation

**Sprint:** Sprint 2 – Enterprise RBAC

**Status:** Completed

**Project:** CloudOne Enterprise Hybrid Data Platform
## Objective

Implement enterprise Role-Based Access Control (RBAC) for the CloudOne Enterprise Hybrid Data Platform by assigning Azure built-in roles to Microsoft Entra security groups according to the approved enterprise security architecture.

## Scope

This sprint covered the implementation of enterprise identity and access management for the CloudOne Enterprise Hybrid Data Platform, including:

- Creation and validation of Microsoft Entra security groups.
- Assignment of Azure built-in RBAC roles.
- Implementation of least-privilege access.
- Management Group and Subscription-level role assignments.
- Validation of enterprise security architecture.
## Implementation Summary

During this sprint, enterprise Role-Based Access Control (RBAC) was implemented using Microsoft Entra security groups and Azure built-in roles. Role assignments were configured following the principle of least privilege to support secure administration, governance, monitoring, data engineering, database administration, and enterprise architecture.
## RBAC Assignments

| Security Group | Azure Role | Scope | Status |
|----------------|------------|-------|--------|
| GRP-CONE-PLATFORM-ADMINS | Contributor | CONE-MGMT-SUB | ✅ Completed |

| GRP-CONE-GOVERNANCE-ADMINS | Resource Policy Contributor | CONE-MGMT-SUB | ✅ Completed |
| GRP-CONE-SECURITY-ADMINS | Security Admin | CONE-MGMT-SUB | ✅ Completed |
| GRP-CONE-DATA-ENGINEERS | Data Factory Contributor | CONE-MGMT-SUB | ✅ Completed |
| GRP-CONE-DBA | SQL Server Contributor | CONE-MGMT-SUB | ✅ Completed |
| GRP-CONE-MONITORING-OPERATORS | Monitoring Contributor | CONE-MGMT-SUB | ✅ Completed |
| GRP-CONE-AUDITORS | Reader | CONE-MGMT-SUB | ✅ Completed |
| GRP-CONE-ENTERPRISE-ARCHITECTS | Reader | MG-CLOUDONE-ENTERPRISE | ✅ Completed |
| GRP-CONE-BI-DEVELOPERS | Power BI Workspace Roles | Deferred | ⏳ Planned |
| GRP-CONE-RELEASE-MANAGERS | Azure DevOps / CI-CD Roles | Deferred | ⏳ Planned |

## Validation

The RBAC implementation was validated by verifying:

- All Microsoft Entra security groups were successfully assigned the intended Azure roles.
- Subscription-level role assignments were confirmed in Azure Access Control (IAM).
- Management Group role inheritance was verified for Enterprise Architects.
- The principle of least privilege was maintained across all assignments.
- Deferred role assignments were documented for future implementation phases.

## Lessons Learned

- Management Group role assignments simplify governance across multiple subscriptions.
- Assigning Azure roles to Microsoft Entra security groups is more scalable than assigning roles directly to individual users.
- Following the principle of least privilege improves security while maintaining operational efficiency.
- Service-specific permissions, such as Power BI and Azure DevOps, should be assigned during their respective implementation phases rather than prematurely.

## Next Steps

The next sprint will focus on building the enterprise platform foundation by implementing the core Azure infrastructure required for the CloudOne Enterprise Hybrid Data Platform, following the approved enterprise architecture.