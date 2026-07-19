Linux System Administration Lab: User & Group Infrastructure Setup

Project Overview
This project demonstrates a real-world Linux Enterprise scenario where a System Administrator sets up a secure collaborative environment for a development team. The lab focuses on core Linux administration skills including user management, secondary group allocation, and access control validation.

---

Infrastructure Design & Concepts
In an enterprise production environment, granting direct root access to users is highly discouraged for security reasons. Instead, this lab implements **Role-Based Access Control (RBAC)** by grouping users under specific project requirements:

Primary Group: Each created user automatically gets their own primary group for isolated files.
Secondary (Supplementary) Group:** Users are added to the `dev_team` secondary group to access shared project files without changing their primary identity.

---

 Step-by-Step Implementation

Phase 1: Group and User Infrastructure Setup

Creating the Project Group
First, I created a dedicated group named `dev_team` to manage access rights for all developers collectively:

<img width="935" height="703" alt="Image" src="https://github.com/user-attachments/assets/65f324be-8d85-4d5d-8cc8-3aae4798021b" />

```bash

sudo groupadd dev_team

Next, I provisioned two regular user accounts for the new developers (alice and bob). The -m flag was explicitly used to automatically create their respective home directories (/home/alice and /home/bob):
sudo useradd -m alice
sudo useradd -m bob

I configured secure initial passwords for both accounts using the passwd utility.
sudo passwd alice
sudo passwd bob

To grant them development access, I appended both users to the dev_team group. I carefully used the -aG (Append Supplementary Groups) flags to prevent accidentally overwriting their existing group memberships:
sudo usermod -aG dev_team alice
sudo usermod -aG dev_team bob

To ensure the infrastructure was configured correctly according to enterprise standards, I verified the users using the id utility:
id alice
id bob



