# US-04 – Pre-Deletion Notification

## 1. Narrative
As a **Data Owner or Legal User**  
I want to be notified before data is deleted or anonymized  
So that I can intervene if required.

## 2. Business Context
Pre-notifications reduce accidental data loss and improve trust.

## 3. Preconditions
- Retention schedule exists  
- No active legal hold

## 4. Trigger
Notification lead time is reached.

## 5. Expected System Behavior
- Notifications are sent to responsible users  
- Notification is logged  
- Execution is still blockable via hold

## 6. Architectural Components
- Retention Scheduler  
- Notification Service  
- Legal Hold Service

## 7. Data & Policy Implications
- No data mutation yet

## 8. Security & Access Control
- Notifications respect jurisdiction visibility

## 9. Audit & Evidence
- Recipient, timestamp, channel

## 10. Non-Functional Expectations
- Guaranteed delivery attempt  
- Idempotent notifications

## 11. Out of Scope
- Notification channel branding
