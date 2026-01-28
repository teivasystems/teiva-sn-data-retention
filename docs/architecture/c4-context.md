# C4 – System Context (Level 1)

```mermaid
C4Context
title Legal Data Retention & Deletion – System Context

Person(employee, "Employee / Requestor", "Submits Legal & Compliance requests")
Person(legalOps, "Legal Ops / Compliance", "Reviews cases, applies legal holds, audits evidence")
Person(auditor, "Auditor", "Validates compliance, checks evidence and policy adherence")

System_Boundary(sn, "ServiceNow Platform") {
  System(retentionApp, "Legal Data Retention & Deletion App", "Custom ServiceNow app for case-based retention, holds, anonymization/deletion, and audit evidence")
}

System_Ext(idp, "Identity Provider (SSO)", "User authentication and group/role provisioning")
System_Ext(extRepo, "External Systems (optional)", "eDiscovery / DLP / Archiving / Source systems holding referenced records")
System_Ext(notify, "Email/SMS/Teams (optional)", "Outbound notifications")

Rel(employee, retentionApp, "Submits requests, receives status updates", "Portal/Employee Center")
Rel(legalOps, retentionApp, "Processes cases, manages holds, runs audits", "Workspace")
Rel(auditor, retentionApp, "Views evidence and audit trail", "Reports/Dashboards")

Rel(idp, retentionApp, "Authenticates users, provides group/role attributes", "SAML/OIDC")
Rel(retentionApp, extRepo, "Optionally syncs metadata / executes deletion in source systems", "API")
Rel(retentionApp, notify, "Sends pre-deletion notifications", "Email/SMS/Teams")
