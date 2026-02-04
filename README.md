# ServiceNow Employee Service Request Portal

A complete ServiceNow mini-project implementing an employee service request system with approval workflow, email notifications, and dynamic forms.

## 📌 Project Overview

The goal of this project is to:
- Trigger approvals when an Employee Service Request is submitted
- Assign approvals to a specific manager/user
- Automatically update request status based on approval outcome
- Handle both approval and rejection scenarios
- Send email notifications to approvers and requesters
- Create dynamic forms with conditional fields
- Document the complete implementation for portfolio

This project follows ServiceNow best practices using Flow Designer instead of legacy workflows.

## ✨ Features
- **Service Catalog Item** with dynamic form
- **UI Policies** for conditional field display
- **Flow Designer Workflow** with approval automation
- **Email Notifications** for approvers and requesters
- **Complete Documentation** for implementation
- **Test scripts** for validation
- **Demo materials** for presentation

## 🛠️ Technologies & Modules Used
- ServiceNow Flow Designer
- Service Catalog
- Requested Item (`sc_req_item`)
- Approval Engine
- Flow Logic (If / Else)
- User & Role Management
- Email Notifications
- UI Policies
- Knowledge Management
- Reporting

---

## 📋 Implementation Steps

### Step 1: Create Service Catalog Category
1. Navigate to `Service Catalog → Catalog Definitions → Categories`
2. Click "New"
3. Fill: Title: Employee Services, Catalog: Service Catalog
4. Click "Submit"

### Step 2: Create Catalog Item
1. Navigate to `Service Catalog → Catalog Definitions → Maintain Items`
2. Click "New" → Select "Catalog Item"
3. Configure:
   - Name: Employee Service Request
   - Category: Employee Services
   - Short Description: Request IT services

### Step 3: Add Variables
#### Variable 1: Service Type
- Type: Multiple Choice
- Question: Select Service Type
- Choices: Laptop Request, Software Access, ID Card
- Mandatory: Yes

#### Variable 2: Business Justification
- Type: Single Line Text
- Question: Why do you need this service?
- Mandatory: Yes

#### Variable 3: Urgency
- Type: Select Box
- Question: How urgent is this request?
- Choices: Low, Medium, High

#### Variable 4: Laptop Configuration
- Type: Multiple Line Text
- Question: Laptop specifications needed
- Mandatory: Yes (conditionally)

### Step 4: Create UI Policy
1. Navigate to `Service Catalog → Catalog UI Policies`
2. Create policy:
   - Name: Show Laptop Configuration
   - Condition: Service Type = "Laptop Request"
   - Action: Show and make mandatory Laptop Configuration field

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

### 5. Email Notifications
- **To Manager**: When approval is requested
- **To Employee**: When request is approved/rejected

---

