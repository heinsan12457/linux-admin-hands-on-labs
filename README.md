Linux System Administration Lab: User & Group Infrastructure Setup

Project Overview
This project demonstrates a real-world Linux Enterprise scenario where a System Administrator sets up a secure collaborative environment for a development team. The lab focuses on core Linux administration skills including user management, secondary group allocation, and access control validation.

---

Infrastructure Design & Concepts
In an enterprise production environment, granting direct root access to users is highly discouraged for security reasons. Instead, this lab implements **Role-Based Access Control (RBAC)** by grouping users under specific project requirements:

Primary Group: Each created user automatically gets their own primary group for isolated files.
Secondary (Supplementary) Group: Users are added to the `dev_team` secondary group to access shared project files without changing their primary identity.

---
```bash
 Step-by-Step Implementation

Phase 1: Group and User Infrastructure Setup

Creating the Project Group
First, I created a dedicated group named `dev_team` to manage access rights for all developers collectively:

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
```

<img width="935" height="703" alt="Screenshot 2026-07-19 173634" src="https://github.com/user-attachments/assets/6ad1cdcb-0af1-4b46-b039-654eafd24fb1" />

 Phase 2: Deploying Directory Permissions & SGID

To build a secure and frictionless collaborative workspace for the developers, I configured an enterprise-standard web directory structure with advanced security features.

1. Creating the Web Deployment Directory
```bash
sudo mkdir -p /var/www/html/webapp/

2. Assigning Proper Ownership
I transferred the ownership of the web directory from root to alice as the owner, and dev_team as the managing group, using recursive flags:

sudo chown -R alice:dev_team /var/www/html/webapp/

3. Configuring the SGID (Set Group ID) Special Permission
To prevent permissions mismatch and "Permission Denied" issues during multi-user collaboration, I applied the SGID bit (2) alongside proper rwxrwxr-x permissions:

sudo chmod -R 2775 /var/www/html/webapp/

Hardening Sensitive Files (.env protection)
For industry-grade security, I simulated a backend configuration environment by creating a .env file and strictly restricting access so only the file owner (alice) can read or write to it:

touch /var/www/html/webapp/.env
sudo chmod 600 /var/www/html/webapp/.env

I verified the applied permissions using ls -ld and ls -la:
ls -ld /var/www/html/webapp/
ls -la /var/www/html/webapp/.env
```
<img width="591" height="93" alt="Screenshot 2026-07-21 120756" src="https://github.com/user-attachments/assets/e365a9fd-61ad-4ff1-b6e3-666af8c981d6" />

<img width="1412" height="463" alt="image" src="https://github.com/user-attachments/assets/3982b33b-49e9-40ef-8d94-c8fe010d2cae" />







