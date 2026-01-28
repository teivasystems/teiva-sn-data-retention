# US-03 – Legal Hold Application & Enforcement

## 1. Narrative
As a **Legal Operations user**  
I want to apply a legal hold  
So that no automated deletion or anonymization occurs.

## 2. Business & Regulatory Context
Legal holds prevent destruction of data relevant to litigation or investigations.

## 3. Preconditions
- Case exists  
- User has Legal Hold role

## 4. Trigger
Legal user applies a hold in the workspace.

## 5. Expected System Behavior
- All related retention schedules are suspended  
- No execution occurs while hold is active  
- Hold overrides all policies

## 6. Architectural Components
- Legal Case Management  
- Legal Hold Service  
- Retention Scheduler  
- Execution Worker

## 7. Data & Policy Implications
- Schedules marked “On Hold”  
- Hold scope recorded

## 8. Security & Access Control
- Only authorized roles can apply/release holds

## 9. Audit & Evidence
- Hold reason, approver, timestamps

## 10. Non-Functional Expectations
- Immediate enforcement  
- Runtime re-check during execution

## 11. Out of Scope
- Legal decision-making itself
