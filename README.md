# ServiceNow Employee Service Approval Flow

This project demonstrates the implementation of an end-to-end approval workflow in ServiceNow using Flow Designer. The workflow handles manager approval for Employee Service Requests submitted through the Service Catalog.

---

## 📌 Project Overview

The goal of this project is to:
- Trigger approvals when an Employee Service Request is submitted
- Assign approvals to a specific manager/user
- Automatically update request status based on approval outcome
- Handle both approval and rejection scenarios

This project follows ServiceNow best practices using Flow Designer instead of legacy workflows.

---

## 🛠️ Technologies & Modules Used

- ServiceNow Flow Designer
- Service Catalog
- Requested Item (`sc_req_item`)
- Approval Engine
- Flow Logic (If / Else)
- User & Role Management

---

## 🔄 Workflow Logic

### 1. Trigger
- Triggered when a **Catalog Item is Requested**
- Catalog Item: **Employee Service Request**

### 2. Ask For Approval
- Approval is requested for a specific user (manager)
- Approver is defined using a scripted rule with user `sys_id`

### 3. Approval Condition
- If Approval State = **Approved**
  - Update Requested Item:
    - Approval → Approved
    - State → Closed Complete
    - Work Notes → "Request approved by manager"

### 4. Rejection Condition (Else)
- If Approval State = **Rejected**
  - Update Requested Item:
    - Approval → Rejected
    - State → Closed Incomplete
    - Work Notes → "Request rejected by manager"

---

## 🧩 Key Configuration Details

### Scripted Approver Logic
```javascript
answer = [];
answer.push('USER_SYS_ID');
