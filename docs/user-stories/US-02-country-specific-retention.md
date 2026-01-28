# US-02 – Country-Specific Retention Policy Resolution

## 1. Narrative
As a **Compliance System**  
I want to resolve the correct retention policy  
So that data lifecycle actions comply with local regulations.

## 2. Business & Regulatory Context
Retention rules vary by country and data class. Incorrect resolution exposes the organization to regulatory penalties.

## 3. Preconditions
- Legal Case is approved  
- Sensitive artifacts are registered

## 4. Trigger
Case approval or artifact registration.

## 5. Expected System Behavior
- Applicable policy is resolved deterministically  
- Retention duration and disposal method are assigned  
- Policy version is recorded for traceability

## 6. Architectural Components
- Legal Case Management  
- Policy & Rules Engine  
- Retention Scheduler

## 7. Data & Policy Implications
- Creation of Retention Schedule records  
- Policy snapshot stored for audit

## 8. Security & Access Control
- Policies are read-only for non-admin roles

## 9. Audit & Evidence
- Policy ID and version  
- Resolution timestamp

## 10. Non-Functional Expectations
- Table-driven evaluation  
- Reproducible outcomes

## 11. Out of Scope
- Legal interpretation of regulations
