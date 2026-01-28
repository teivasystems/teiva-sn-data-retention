---

## `docs/architecture/c4-container.md`

```markdown
# C4 – Container Diagram (Level 2)

```mermaid
C4Container
title Legal Data Retention & Deletion – Containers

Person(employee, "Employee / Requestor")
Person(legalOps, "Legal Ops / Compliance")
Person(auditor, "Auditor")

System_Boundary(sn, "ServiceNow Platform") {
  Container(portal, "Employee Center / Portal", "ServiceNow UX", "Case submission and status tracking")
  Container(workspace, "Legal Workspace", "ServiceNow Workspace", "Case triage, approvals, legal holds, audit review")
  Container(app, "Retention App (Custom Scope)", "ServiceNow App", "Policy evaluation, scheduling, holds, execution, audit logging")
  ContainerDb(db, "ServiceNow Data Tables", "Now Platform DB", "Cases, artifacts, policies, schedules, holds, audit logs")
  Container(scheduler, "Retention Scheduler", "Scheduled Jobs / Flow", "Generates and executes retention actions in batches")
  Container(audit, "Audit & Reporting", "Dashboards/Reports", "Evidence, exceptions, KPIs, audit exports")
}

System_Ext(idp, "Identity Provider (SSO)", "SAML/OIDC")
System_Ext(extRepo, "External Systems (optional)", "eDiscovery/DLP/Archive/Source systems")
System_Ext(notify, "Notification Channels (optional)", "Email/SMS/Teams")

Rel(employee, portal, "Submits Legal request, checks status")
Rel(legalOps, workspace, "Processes cases, applies holds")
Rel(auditor, audit, "Reviews evidence and audit trail")

Rel(portal, app, "Creates/updates cases", "UI/API")
Rel(workspace, app, "Reviews/approves, holds/release", "UI/API")
Rel(app, db, "Reads/writes domain data", "SQL (platform-managed)")
Rel(scheduler, app, "Triggers evaluation/execution", "Job/Flow Actions")
Rel(app, audit, "Publishes evidence and metrics", "Reports/PA (optional)")

Rel(idp, portal, "AuthN/AuthZ", "SAML/OIDC")
Rel(idp, workspace, "AuthN/AuthZ", "SAML/OIDC")
Rel(idp, app, "Role/group attributes", "SAML/OIDC")

Rel(app, notify, "Pre-deletion notifications", "Email/SMS/Teams")
Rel(app, extRepo, "Optional: execute deletion/anonymization off-platform", "API")
