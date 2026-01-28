# US-06 – Cross-Border Access Restriction

## 1. Narrative
As a **Compliance System**  
I want to restrict access to cases across jurisdictions  
So that cross-border data exposure is prevented.

## 2. Business Context
Cross-border access violations are a major regulatory risk.

## 3. Preconditions
- Case has jurisdiction metadata

## 4. Trigger
User attempts to access a case or artifact.

## 5. Expected System Behavior
- Access is evaluated dynamically  
- Unauthorized access is blocked  
- Behavior is consistent across UI and API

## 6. Architectural Components
- Access Control Layer  
- Legal Case Management

## 7. Data & Policy Implications
- No data mutation

## 8. Security & Access Control
- ABAC rules enforced  
- Least privilege principle

## 9. Audit & Evidence
- Access attempts logged (where required)

## 10. Non-Functional Expectations
- No performance degradation

## 11. Out of Scope
- Identity governance outside ServiceNow
