# Reference Architecture – Legal Data Retention & Deletion  
**Platform:** ServiceNow  
**Scope:** Custom Application (Legal & Compliance)

## 1. Purpose

This document describes the reference architecture for a **ServiceNow-based Legal Data Retention & Deletion solution**.

The solution ensures that sensitive legal and compliance-related data is:
- retained according to country-specific regulations,
- deleted or anonymized automatically after retention periods,
- protected by legal holds,
- access-restricted across jurisdictions,
- fully auditable at any point in time.

The architecture is designed for **regulated enterprises** (e.g. healthcare, medical devices, pharma, finance).

---

## 2. Architectural Goals

| Goal | Description |
|----|----|
| Regulatory Compliance | Enforce jurisdiction-specific retention and deletion rules |
| Audit Readiness | Provide immutable evidence of policy decisions and executions |
| Risk Reduction | Eliminate manual deletion processes and human error |
| Governance by Design | Embed compliance directly into operational workflows |
| Scalability | Support large data volumes and multiple countries |

---

## 3. High-Level Architecture Overview (Extended)

The Legal Data Retention & Deletion solution is implemented as a **custom ServiceNow application** that embeds regulatory governance directly into operational workflows.

The architecture follows a **layered and service-oriented model**, separating user interaction, orchestration, policy decisioning, execution, and audit evidence to ensure scalability, security, and auditability.

### 3.1 High-Level System Flow
[Employee Center / Portal]
|
v
[Legal & Compliance Catalog Item]
|
v
[Legal Case Management (Custom App)]
|
+–> [Policy & Rules Engine]
|
+–> [Retention Scheduler]
|
+–> [Legal Hold Service]
|
+–> [Execution Worker]
|
v
[Audit & Evidence Store]

Each component is described in detail below.

---

### 3.2 Employee Center / Portal

**Purpose**  
Provides the primary entry point for employees and business users to submit Legal and Compliance-related requests.

**Responsibilities**
- Capture case context (country, case type, data sensitivity)
- Guide users through jurisdiction-aware forms
- Provide transparency into case status and lifecycle

**Architectural Notes**
- Uses standard ServiceNow UX (Employee Center / Service Portal)
- No sensitive logic is implemented at this layer
- Acts as a controlled intake channel, not a data store

---

### 3.3 Legal & Compliance Catalog Item

**Purpose**  
Acts as the formal initiation mechanism for Legal Data Retention cases.

**Responsibilities**
- Standardize intake across regions and jurisdictions
- Trigger case creation in the custom application scope
- Enforce mandatory data classification at submission time

**Architectural Notes**
- Dynamic form logic adapts based on country and case type
- Prevents incomplete or non-compliant submissions
- Decouples user experience from backend policy logic

---

### 3.4 Legal Case Management (Custom Application)

**Purpose**  
Serves as the **central orchestration layer** and system of record for all retention-related activities.

**Responsibilities**
- Maintain the legal case lifecycle and state model
- Link sensitive artifacts to cases
- Track ownership, jurisdiction, and cross-border flags
- Coordinate policy evaluation, scheduling, holds, and execution

**Architectural Notes**
- Implemented in a dedicated application scope
- Stores only the minimum required sensitive data
- Designed for full traceability and explainability

---

### 3.5 Policy & Rules Engine

**Purpose**  
Determines *what* must happen to data, *when*, and *how*, based on regulatory and organizational rules.

**Responsibilities**
- Resolve applicable retention policy per artifact
- Apply country- and jurisdiction-specific logic
- Determine disposal method (delete vs anonymize)
- Generate policy traceability for audit purposes

**Architectural Notes**
- Table-driven decision model (configuration over code)
- Scripted logic used only for exceptional cases
- Policy resolution is deterministic and reproducible

---

### 3.6 Retention Scheduler

**Purpose**  
Translates policy decisions into **concrete, time-bound execution plans**.

**Responsibilities**
- Create retention schedules per artifact or case
- Calculate notification lead times and grace periods
- Queue execution jobs for future processing
- Recalculate schedules when policies or case attributes change

**Architectural Notes**
- Uses scheduled jobs and/or Flow Designer
- Supports batch-oriented processing
- Scheduling is reversible until execution occurs

---

### 3.7 Legal Hold Service

**Purpose**  
Provides a compliance-safe mechanism to **suspend all automated lifecycle actions**.

**Responsibilities**
- Apply and release legal holds at case or artifact level
- Enforce immediate suspension of scheduled actions
- Record hold reason, approvals, and duration
- Ensure holds override all automation

**Architectural Notes**
- Hold checks are enforced at both scheduling and execution time
- Hold lifecycle is fully audited
- Supports partial and scoped holds

---

### 3.8 Execution Worker

**Purpose**  
Performs the **actual data lifecycle action** in a controlled, auditable manner.

**Responsibilities**
- Execute deletion or anonymization logic
- Re-validate policy and legal hold at runtime
- Support idempotent and retry-safe execution
- Handle integration with external systems when required

**Architectural Notes**
- Implemented as scheduled scripts or scripted APIs
- Designed for controlled batch execution
- Failures are isolated and recoverable

---

### 3.9 Audit & Evidence Store

**Purpose**  
Provides immutable-style evidence to demonstrate regulatory compliance.

**Responsibilities**
- Record all lifecycle actions and decisions
- Capture policy version, timestamps, and execution outcome
- Store notification history and exceptions
- Support audits without operational disruption

**Architectural Notes**
- Separate audit tables for clarity and performance
- Optimized for reporting and evidence export
- Read-only access for auditors

---

### 3.10 Architectural Characteristics

- **Governance by Design**  
  Compliance rules are embedded into platform behavior, not enforced manually.

- **Explainability**  
  Every automated action can be traced back to a policy and decision path.

- **Defense in Depth**  
  Access control, legal holds, and runtime validation operate independently.

- **Scalability**  
  Batch-oriented execution and table-driven policies support multi-country rollout.

---

This architecture ensures that data retention and deletion are **predictable, defensible, and operationally sustainable** — even under regulatory scrutiny.

---

## 4. Logical Architecture Layers

### 4.1 Experience Layer
- Employee Center / Service Portal
- Legal & Compliance Catalog Items
- Agent Workspace / Custom Legal Workspace

**Responsibilities**
- Case submission
- Review and approval
- Hold placement and release
- Transparency for legal users

---

### 4.2 Workflow & Orchestration Layer
- Flow Designer–based lifecycle orchestration
- State-driven case management
- Event-based notifications (pre-deletion alerts)

**Key Flows**
- Case submission & approval
- Retention schedule creation
- Notification before execution
- Execution (delete / anonymize)
- Audit logging

---

### 4.3 Policy & Rules Layer
- Table-driven retention policies
- Country- and jurisdiction-aware rules
- Disposal method resolution (delete vs anonymize)

**Policy Inputs**
- Country / jurisdiction
- Case type
- Data classification
- Cross-border flag

---

### 4.4 Data Layer (Custom Application Scope)

#### Core Tables
| Table | Purpose |
|----|----|
| Legal Case | Parent record for compliance cases |
| Sensitive Artifact | Represents data objects under retention |
| Retention Policy | Defines rules per country and data class |
| Retention Schedule | Concrete execution plan per artifact |
| Legal Hold | Suspension of retention actions |
| Retention Audit | Evidence of all lifecycle actions |

**Design Principles**
- Minimum data storage
- Clear ownership and traceability
- Separation of configuration vs operational data

---

### 4.5 Execution Layer

**Execution Patterns**
- Scheduled script executions for batch processing
- Scripted APIs for anonymization logic
- Runtime re-validation of legal holds and access rules

**Supported Actions**
- Hard delete
- Field-level anonymization
- Attachment cleanup
- External system notification (optional)

---

### 4.6 Audit & Reporting Layer
- Immutable audit records for every action
- Evidence for:
  - policy selection
  - notifications
  - execution results
  - legal holds
- Dashboards for compliance officers and auditors

---

## 5. Security Architecture

### 5.1 Access Control
- Attribute-based access control (ABAC)
- ACLs on all custom tables
- Jurisdiction-aware query restrictions

### 5.2 Sensitive Data Protection
- Role-based access
- Field-level encryption for critical attributes
- Restricted attachment access

### 5.3 Cross-Border Restrictions
- Case visibility enforced by:
  - user country
  - legal entity
  - jurisdiction rules
- Explicit handling of cross-border cases

---

## 6. Legal Hold Architecture

- Holds can be applied at:
  - Case level
  - Artifact level
- Holds immediately suspend:
  - scheduled executions
  - deletion jobs
- Hold lifecycle is fully audited

---

## 7. Non-Functional Requirements

| Category | Requirement |
|----|----|
| Performance | Batch processing with throttling |
| Reliability | Idempotent executions & retries |
| Transparency | Explainable policy decisions |
| Operability | Global pause / kill switch |
| Scalability | Supports multi-country rollout |

---

## 8. Deployment & Lifecycle

- Dedicated application scope (e.g. `x_company_legal_retention`)
- CI/CD via Update Sets or ServiceNow DevOps
- Environments:
  - DEV → TEST → UAT → PROD
- Automated Test Framework (ATF) coverage:
  - policy matching
  - legal hold enforcement
  - access control
  - scheduler execution

---

## 9. Architectural Principles

- **Governance is not a process – it is a platform capability**
- **Compliance must be invisible but enforceable**
- **Auditability is a first-class feature**
- **Automation beats documentation**

---

## 10. Appendix

### Key Concepts
- Retention ≠ Archiving
- Deletion ≠ Anonymization
- Legal Hold overrides all automation

### Out of Scope
- Legal interpretation of regulations
- Country-specific legal advice
- UI branding customization

---

**Owner:** Architecture Team  
**Last Updated:** 2025-01-01  
**Status:** Reference
