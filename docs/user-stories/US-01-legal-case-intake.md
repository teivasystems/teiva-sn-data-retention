# US-01 – Legal Case Intake & Classification

## 1. Narrative (User Intent)
As an **Employee or Business User**  
I want to submit a Legal & Compliance request  
So that sensitive data is classified and governed from the moment it enters the platform.

## 2. Business & Regulatory Context
Unclassified legal data creates immediate compliance risk. Early classification ensures downstream retention, access control, and auditability.

## 3. Preconditions & Assumptions
- Employee is authenticated  
- Jurisdiction and country are known  
- User has access to Legal & Compliance catalog

## 4. Trigger
User submits a Legal & Compliance catalog item via Employee Center.

## 5. Expected System Behavior
- A Legal Case is created in the custom application  
- Country, case type, and sensitivity classification are mandatory  
- Case is routed for legal review before activation

## 6. Architectural Components Involved
- Employee Center / Portal  
- Legal & Compliance Catalog Item  
- Legal Case Management  
- Access Control Layer

## 7. Data & Policy Implications
- Case attributes drive downstream policy resolution  
- No retention schedule is created before approval

## 8. Security & Access Control
- Case visibility restricted by jurisdiction  
- Only authorized Legal roles can modify classification

## 9. Audit & Evidence Requirements
- Submission timestamp  
- Submitting user  
- Initial classification values

## 10. Non-Functional Expectations
- Low-latency case creation  
- Deterministic validation behavior

## 11. Out of Scope
- Legal interpretation of the request  
- UI customization beyond standard portal components
