Linux System Administration Lab: User & Group Infrastructure Setup

Project Overview
This project demonstrates a real-world Linux Enterprise scenario where a System Administrator sets up a secure collaborative environment for a development team. The lab focuses on core Linux administration skills including user management, secondary group allocation, and access control validation.

---

Infrastructure Design & Concepts
In an enterprise production environment, granting direct root access to users is highly discouraged for security reasons. Instead, this lab implements **Role-Based Access Control (RBAC)** by grouping users under specific project requirements:

Primary Group:** Each created user automatically gets their own primary group for isolated files.
Secondary (Supplementary) Group:** Users are added to the `dev_team` secondary group to access shared project files without changing their primary identity.

---

 Step-by-Step Implementation

Phase 1: Group and User Infrastructure Setup

Creating the Project Group
First, I created a dedicated group named `dev_team` to manage access rights for all developers collectively:
```bash
sudo groupadd dev_team
