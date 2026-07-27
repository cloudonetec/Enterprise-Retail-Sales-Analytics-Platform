# Phase 3 – Platform Foundation

## Phase Status

**Status:** ✅ Completed  
**Architecture Version:** CloudOne Enterprise Hybrid Data Platform v2.1  
**Phase Owner:** CloudOne Platform Team  
**Primary Region:** North Europe  

---

## 1. Phase Objective

The objective of Phase 3 was to establish the shared platform foundation required to support the CloudOne Enterprise Hybrid Data Platform.

This phase focused on enterprise networking, centralized security, monitoring foundations, backup infrastructure, and platform services that will be reused by later phases.

The architecture for Phase 3 includes Azure Monitor, Log Analytics, Azure Key Vault, Hub Virtual Network, Private DNS, Private Endpoints, Network Security Groups, Azure Backup, Recovery Services Vault, and Cost Management. Some components were deployed during this phase, while others were intentionally deferred until their dependencies are available.

---

## 2. Phase Scope

The following areas were included in Phase 3:

| Area | Scope |
|------|-------|
| Networking | Hub Virtual Network and enterprise subnet structure |
| Network Security | Network Security Group for management resources |
| Monitoring Foundation | Log Analytics Workspace |
| Secrets Management | Azure Key Vault |
| Backup Foundation | Recovery Services Vault |
| Resource Organization | Dedicated management resource groups |
| Security Hardening Preparation | Private DNS and Private Endpoint readiness |
| Operational Readiness | Monitoring, backup, and recovery foundations |

---

## 3. Resource Groups

| Resource Group | Region | Purpose | Status |
|----------------|--------|---------|--------|
| RG-CONE-MGMT-NETWORK | North Europe | Hub networking and network security resources | ✅ Deployed |
| RG-CONE-MGMT-SECURITY | North Europe | Enterprise security services | ✅ Deployed |
| RG-CONE-MGMT-MONITORING | North Europe | Centralized monitoring services | ✅ Deployed |
| RG-CONE-MGMT-BACKUP | North Europe | Backup and recovery services | ✅ Deployed |
| RG-CONE-SHARED | North Europe | Shared platform services | ✅ Existing |
| RG-CONE-PROD | North Europe | Production platform resources | ✅ Existing |

---

## 4. Resources Implemented

| Resource Type | Resource Name | Resource Group | Region | Status |
|---------------|---------------|----------------|--------|--------|
| Virtual Network | VNET-CONE-HUB-NEU-01 | RG-CONE-MGMT-NETWORK | North Europe | ✅ Deployed |
| Network Security Group | NSG-CONE-MGMT-NEU-01 | RG-CONE-MGMT-NETWORK | North Europe | ✅ Deployed |
| Log Analytics Workspace | LAW-CONE-MGMT-NEU-01 | RG-CONE-MGMT-MONITORING | North Europe | ✅ Deployed |
| Azure Key Vault | kv-cone-mgmt-neu-01 | RG-CONE-MGMT-SECURITY | North Europe | ✅ Deployed |
| Recovery Services Vault | RSV-CONE-MGMT-NEU-01 | RG-CONE-MGMT-BACKUP | North Europe | ✅ Deployed |

---

## 5. Hub Virtual Network

### 5.1 Virtual Network Configuration

| Setting | Value |
|---------|-------|
| Name | VNET-CONE-HUB-NEU-01 |
| Resource Group | RG-CONE-MGMT-NETWORK |
| Region | North Europe |
| Address Space | 10.0.0.0/16 |
| Architecture Role | Enterprise Hub Network |

### 5.2 Subnet Layout

| Subnet | CIDR | Purpose |
|--------|------|---------|
| AzureFirewallSubnet | 10.0.0.0/26 | Reserved for future Azure Firewall deployment |
| GatewaySubnet | 10.0.1.0/27 | Reserved for VPN Gateway or ExpressRoute Gateway |
| ManagementSubnet | 10.0.2.0/24 | Management and administration resources |
| PrivateEndpointSubnet | 10.0.3.0/24 | Private Endpoints for Azure platform services |
| SharedServicesSubnet | 10.0.4.0/24 | Shared platform and enterprise services |

### 5.3 Validation

| Validation Item | Result |
|-----------------|--------|
| Address space verified | ✅ Passed |
| Subnet address ranges verified | ✅ Passed |
| Reserved subnet names verified | ✅ Passed |
| Region verified | ✅ Passed |
| Naming standard verified | ✅ Passed |
| Mandatory tags verified | ✅ Passed |

---

## 6. Network Security Group

### 6.1 Configuration

| Setting | Value |
|---------|-------|
| Name | NSG-CONE-MGMT-NEU-01 |
| Resource Group | RG-CONE-MGMT-NETWORK |
| Region | North Europe |
| Associated Subnet | ManagementSubnet |
| Custom Security Rules | None configured |
| Default Rules | Azure default rules retained |

### 6.2 Design Decision

The NSG was associated only with the ManagementSubnet.

No custom inbound or outbound rules were created because no management workloads have been deployed into the subnet yet. Security rules will be introduced when actual workloads and traffic flows are known.

### 6.3 Validation

| Validation Item | Result |
|-----------------|--------|
| NSG deployment verified | ✅ Passed |
| Subnet association verified | ✅ Passed |
| Default rules verified | ✅ Passed |
| No unnecessary custom rules | ✅ Passed |

---

## 7. Log Analytics Workspace

### 7.1 Configuration

| Setting | Value |
|---------|-------|
| Name | LAW-CONE-MGMT-NEU-01 |
| Resource Group | RG-CONE-MGMT-MONITORING |
| Region | North Europe |
| Purpose | Centralized logging, diagnostics, monitoring, and alerting foundation |

### 7.2 Current State

The workspace has been deployed successfully.

Diagnostic settings, log collection, alert rules, workbooks, and action groups have not yet been configured because the supported workloads have not been deployed.

These items will be implemented during Phase 12 – Monitoring and Incident Response.

### 7.3 Validation

| Validation Item | Result |
|-----------------|--------|
| Workspace deployment verified | ✅ Passed |
| Region verified | ✅ Passed |
| Naming standard verified | ✅ Passed |
| Ready for diagnostic integration | ✅ Passed |

---

## 8. Azure Key Vault

### 8.1 Configuration

| Setting | Value |
|---------|-------|
| Name | kv-cone-mgmt-neu-01 |
| Resource Group | RG-CONE-MGMT-SECURITY |
| Region | North Europe |
| SKU | Standard |
| Permission Model | Azure RBAC |
| Soft Delete | Enabled |
| Purge Protection | Enabled |
| Retention Period | 90 days |
| Public Network Access | Enabled |
| Public Access Scope | All networks |
| Private Endpoint | Not configured |
| VM Deployment Access | Disabled |
| ARM Template Deployment Access | Disabled |
| Azure Disk Encryption Access | Disabled |

### 8.2 Object State

| Object Type | Current State |
|-------------|---------------|
| Keys | Empty |
| Secrets | Empty |
| Certificates | Empty |

### 8.3 Design Decisions

- Azure RBAC was selected instead of legacy access policies.
- Soft Delete and Purge Protection were enabled to protect against accidental or malicious deletion.
- Public access remains enabled temporarily.
- Private Endpoint and Private DNS integration were deferred to Phase 6.
- Diagnostic settings were deferred to Phase 12.

### 8.4 Validation

| Validation Item | Result |
|-----------------|--------|
| Vault URI verified | ✅ Passed |
| Azure RBAC permission model verified | ✅ Passed |
| Soft Delete verified | ✅ Passed |
| Purge Protection verified | ✅ Passed |
| Retention period verified | ✅ Passed |
| Public network access verified | ✅ Passed |
| Keys, secrets, and certificates reviewed | ✅ Passed |
| Diagnostic settings state reviewed | ✅ Passed |

---

## 9. Recovery Services Vault

### 9.1 Configuration

| Setting | Value |
|---------|-------|
| Name | RSV-CONE-MGMT-NEU-01 |
| Resource Group | RG-CONE-MGMT-BACKUP |
| Region | North Europe |
| Storage Redundancy | Geo-redundant storage |
| Encryption | Microsoft-managed keys |
| Immutability | Enabled, not locked |
| Public Network Access | Enabled |
| Public Access Scope | All networks |
| Private Endpoint | Not configured |
| Cross Region Restore | Disabled |
| System Assigned Managed Identity | Off |
| User Assigned Managed Identity | None |
| Resource Locks | None |
| Security Level | Good |

### 9.2 Backup State

| Backup Component | Current State |
|------------------|---------------|
| Backup Policies | Not configured |
| Protected Workloads | None |
| Backup Items | None |
| Restore Testing | Not performed |
| Disaster Recovery Testing | Not performed |

### 9.3 Security State

| Security Component | Current State |
|--------------------|---------------|
| Immutable Vault | Enabled, not locked |
| Threat Detection | Not configured |
| Multi-User Authorization | Not configured |
| Soft Delete Settings | Available |
| Encryption Settings | Microsoft-managed keys |
| Security PIN | Available |

### 9.4 Design Decisions

- Geo-redundant storage was selected for stronger backup resilience.
- Immutability was enabled but not locked to allow changes during implementation.
- Public access remains enabled until private connectivity is implemented.
- Backup policies were deferred because no protected production workloads exist.
- Restore and DR testing were deferred to Phase 13.
- Multi-User Authorization and final immutability locking will be reviewed in Phase 13.

### 9.5 Validation

| Validation Item | Result |
|-----------------|--------|
| Vault status verified as Active | ✅ Passed |
| Region verified | ✅ Passed |
| Subscription verified | ✅ Passed |
| Resource group verified | ✅ Passed |
| Managed identity state verified | ✅ Passed |
| Public networking verified | ✅ Passed |
| Security level verified | ✅ Passed |
| Immutability state verified | ✅ Passed |
| Backup section reviewed | ✅ Passed |
| Site Recovery section reviewed | ✅ Passed |
| Resource locks reviewed | ✅ Passed |

---

## 10. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Management platform deployed in North Europe | West Europe deployment was blocked by tenant-root Azure Policy |
| Public access retained temporarily | Private networking will be implemented when data services are deployed |
| Private DNS deferred | Private DNS is required only when Private Endpoints are introduced |
| Private Endpoints deferred | Target services such as ADLS Gen2 and Azure SQL are deployed in later phases |
| Diagnostic settings deferred | Central monitoring configuration belongs to Phase 12 |
| Alert rules and workbooks deferred | Operational workloads and telemetry are not yet available |
| Backup policies deferred | No production workloads currently require protection |
| Immutability not locked | Backup configuration may still change before production |
| Resource locks not applied | Locks could interfere with ongoing implementation |
| No custom NSG rules created | No workload traffic requirements exist yet |

---

## 11. Revisit and Deferred Items

The detailed living register is maintained in:

```text
docs/CloudOne-Revisit-and-Deferred-Register.md

| Component | Original Phase | Status | Trigger Phase | Trigger Condition | Review Required |
|-----------|----------------|--------|---------------|-------------------|-----------------|
| Private DNS Zones | Phase 3 | ⏸ Deferred | Phase 6 | First Private Endpoint required | ⬜ |
| Azure Key Vault Private Endpoint | Phase 3 | 🔄 Revisit | Phase 6 | ADLS Gen2 private networking implementation begins | ⬜ |
| Recovery Services Vault Private Endpoint | Phase 3 | 🔄 Revisit | Phase 6 | Private networking implementation begins | ⬜ |
| Disable Key Vault Public Access | Phase 3 | 🔄 Revisit | Phase 6 | Key Vault Private Endpoint validated | ⬜ |
| Disable Recovery Services Vault Public Access | Phase 3 | 🔄 Revisit | Phase 6 | Recovery Services Vault Private Endpoint validated | ⬜ |
| Log Analytics Diagnostic Integration | Phase 3 | 🔄 Revisit | Phase 12 | Supported workloads deployed | ⬜ |
| Azure Monitor Diagnostic Settings | Phase 3 | ⏸ Deferred | Phase 12 | Central monitoring implementation begins | ⬜ |
| Alert Rules and Action Groups | Phase 3 | ⏸ Deferred | Phase 12 | Operational telemetry available | ⬜ |
| Monitoring Workbooks | Phase 3 | ⏸ Deferred | Phase 12 | Monitoring dashboards required | ⬜ |
| Recovery Services Vault Backup Policies | Phase 3 | ⏸ Deferred | Phase 13 | Production workloads available | ⬜ |
| Protected Workloads | Phase 3 | ⏸ Deferred | Phase 13 | Backup-eligible resources deployed | ⬜ |
| Backup Restore Testing | Phase 3 | ⏸ Deferred | Phase 13 | Backup policies operational | ⬜ |
| Disaster Recovery Testing | Phase 3 | ⏸ Deferred | Phase 13 | DR design approved | ⬜ |
| Immutable Vault Lock Review | Phase 3 | 🔄 Revisit | Phase 13 | Backup strategy finalized | ⬜ |
| Multi-User Authorization | Phase 3 | ⏸ Deferred | Phase 13 | Production operational governance approved | ⬜ |
| Resource Delete Locks | Phase 3 | ⏸ Deferred | Phase 14 | Platform implementation completed | ⬜ |