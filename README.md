# IAM-Lab-
IAM banking identity structure 
Project: Financial Institution IAM Infrastructure (Microsoft Entra ID)

# Objective
The goal of this lab was to architect and deploy a production-ready Identity and Access Management (IAM) structure in Microsoft Entra ID. The simulation mirrors a regional bank's organizational flow, focusing on the core principles of Least Privilege, Role-Based Access Control (RBAC), and Separation of Duties.

---

# 1. Security Group Architecture (Authorization)
To manage access at scale, I established five functional security groups. Using a standardized naming convention (`penair_`) ensures that permissions are assigned to roles rather than individuals, preventing "Privilege Creep."

| Group Name | Functional Responsibility | Security Oversight |
| :--- | :--- | :--- |
| `penair_tellers` | Branch Tellers | Transaction Processing |
| `penair_memberservices` | Member Services | Account Management / Fraud Detection |
| `penair_management` | Branch Managers | Approval Authority |
| `penair_it` | IT Support | System Administration |
| `penair_compliance` | Compliance Officers | PCI DSS Oversight |

---

# 2. Identity Provisioning (Identification)
I created three primary user identities, each with granular attributes (Job Title, Department) to support future **Attribute-Based Access Control (ABAC)** logic.

* **User: `mgr1`** | Title: Manager | Dept: Management
* **User: `msr1`** | Title: MSR | Dept: Member Services
* **User: `teller1`** | Title: Teller | Dept: Branch Ops

---

# Lab Evidence & Documentation

> **Security Note:** To adhere to Zero Trust principles and data privacy standards, all globally unique identifiers (GUIDs) and personal email domains have been masked, while functional group names remain visible to demonstrate the administrative logic.

# Identity Gallery

| 1. High-Level User Directory | 2. Security Group Hierarchy |
| :---: | :---: |
| ![User Directory](./images/users_redacted.png) | ![Group Hierarchy](./images/groups_redacted.png) |

| 3. Granular User Attributes (Teller One Properties) |
| :---: |
| ![User Properties](./images/properties_redacted.png) |

---

# Security Insights (The 2027 Edge)
* ITDR Readiness:By isolating administrative roles (`penair_it`) from branch roles (`penair_tellers`), the "Blast Radius" is significantly reduced in the event of a credential compromise.
* Data Masking: Professional redaction was applied to all system-generated Object IDs and personal UPNs to demonstrate Data Loss Prevention (DLP) best practices.
* Scalability: This manual setup took approximately 30-40 minutes, the structure is designed for transition to Infrastructure as Code (IaC) using Terraform or PowerShell.

---

# Implementation Pathway
1. Define Roles: Mapped business units to technical security groups.
2. Provision Identities:Created user accounts with specific department data.
3. Assign Membership:`Entra ID` -> `Groups` -> `Select Group` -> `Add Members`.
4. Verification:Validated that properties and UPNs aligned with the organizational chart.
