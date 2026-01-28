---

## `docs/architecture/c4-component-retention.md`

This focuses on the *Retention App* internals (policy engine, scheduling, holds, execution, audit).

```markdown
# C4 – Component Diagram (Level 3)
## Retention App (Custom Scope)

```mermaid
C4Component
title Retention App – Components

Container_Boundary(app, "Retention App (Custom Scope)") {

  Component(caseSvc, "Case Service", "Script Includes / Flow Actions", "Manages case lifecycle, state transitions, ownership")
  Component(policyEngine, "Policy Engine", "Script Includes", "Resolves applicable retention rule (country, case type, data class)")
  Component(scheduleSvc, "Schedule Service", "Script Includes", "Creates retention schedules and notification timeline")
  Component(holdSvc, "Legal Hold Service", "Script Includes", "Applies/releases holds; blocks execution for held scope")
  Component(notifySvc, "Notification Service", "Flow/Notifications", "Sends pre-action alerts and execution outcomes")
  Component(execWorker, "Execution Worker", "Scheduled Script / Scripted API", "Performs delete/anonymize; ensures idempotency; records outcomes")
  Component(auditSvc, "Audit Service", "Script Includes", "Writes immutable-style evidence logs and exception traces")
  Component(accessCtrl, "Access Control Layer", "ACLs + ABAC rules", "Enforces jurisdiction and cross-border access restrictions")
}

ContainerDb(db, "ServiceNow Data Tables", "Now Platform DB", "Cases, artifacts, policies, schedules, holds, audit logs")
System_Ext(notify, "Notification Channels (optional)", "Email/SMS/Teams")
System_Ext(extRepo, "External Systems (optional)", "eDiscovery/DLP/Archive/Source systems")

Rel(caseSvc, db, "CRUD cases/artifacts")
Rel(policyEngine, db, "Reads retention policies")
Rel(scheduleSvc, db, "Writes schedules, reads artifacts")
Rel(holdSvc, db, "Writes/reads holds")
Rel(execWorker, db, "Reads schedules, writes results, updates artifacts")
Rel(auditSvc, db, "Writes audit/evidence logs")
Rel(accessCtrl, db, "Guards read/write with ACL + ABAC constraints")

Rel(scheduleSvc, notifySvc, "Triggers notifications", "Event/Flow")
Rel(notifySvc, notify, "Sends notifications", "Email/SMS/Teams")

Rel(execWorker, extRepo, "Optional: execute off-platform deletion/anonymization", "API")
Rel(execWorker, holdSvc, "Re-check hold at runtime", "Internal API")
Rel(execWorker, policyEngine, "Re-validate policy snapshot", "Internal API")
Rel(execWorker, auditSvc, "Logs all actions + exceptions", "Internal API")
