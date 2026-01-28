# US-05 – Retention Execution (Delete vs Anonymize)

## 1. Narrative
As a **Compliance System**  
I want to execute deletion or anonymization  
So that data is handled according to policy.

## 2. Business Context
Automated execution reduces manual risk and ensures consistency.

## 3. Preconditions
- Schedule due  
- No legal hold active

## 4. Trigger
Scheduled execution job.

## 5. Expected System Behavior
- Policy and hold are revalidated  
- Correct action is executed  
- Partial failures are isolated

## 6. Architectural Components
- Execution Worker  
- Policy & Rules Engine  
- Legal Hold Service  
- Audit & Evidence Store

## 7. Data & Policy Implications
- Data removed or anonymized  
- Schedule marked completed

## 8. Security & Access Control
- Execution runs with system privileges  
- Scoped access enforced

## 9. Audit & Evidence
- Action taken  
- Outcome  
- Exception details

## 10. Non-Functional Expectations
- Idempotency  
- Retry safety

## 11. Out of Scope
- Manual deletion
