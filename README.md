# WindowsAD-writeups

![image](https://github.com/user-attachments/assets/5ab7685b-5465-4f6e-954f-fee2842089ba)


![image](https://github.com/user-attachments/assets/449d7af2-cbe7-4000-ba24-48fb39e3b906)

Login as ariifpeycal
![image](https://github.com/user-attachments/assets/4397f733-0c78-4344-9dba-ddebfd6f2300)

![image](https://github.com/user-attachments/assets/df697526-cc94-45a8-a147-c4f728c4e2c4)

![image](https://github.com/user-attachments/assets/1e28ad72-94b7-4b26-afc0-9ef81716b448)

![image](https://github.com/user-attachments/assets/31c174d8-fad8-40fa-8f13-2cdcaf91dab7)

![image](https://github.com/user-attachments/assets/5469bd2c-7ad6-4a5e-b1cc-6589b24fcf5d)

![image](https://github.com/user-attachments/assets/5deccfc8-990c-4614-b98d-be8b73f90b06)


![image](https://github.com/user-attachments/assets/aca9419d-4c8f-4741-8dcd-4d7f838d7d62)

![image](https://github.com/user-attachments/assets/bbe0b749-5f52-4b5a-a06f-6281172f216f)


---

# Windows Active Directory Setup and Management

This guide walks you through the process of setting up and managing Active Directory (AD) on a Windows Server, including configuring users, groups, and Group Policies.

---

## Table of Contents
1. [Naming the Server](#naming-the-server)
2. [Installing AD DS](#installing-ad-ds)
3. [Promoting the Server to a Domain Controller](#promoting-the-server-to-a-domain-controller)
4. [Post-Installation Configuration](#post-installation-configuration)
5. [Managing Active Directory](#managing-active-directory)
   - [Creating Organizational Units](#creating-organizational-units)
   - [Adding Users](#adding-users)
   - [Setting Password Policies](#setting-password-policies)
   - [Managing Groups](#managing-groups)
   - [Delegating Control](#delegating-control)
6. [Group Policy Management](#group-policy-management)

---

## Naming the Server
### Why Name the Server?
Naming a Windows Server, especially a Domain Controller, helps identify it within your network and avoids conflicts.

### Steps to Rename:
1. Open **Server Manager**.
2. Navigate to **Local Server** > **Computer Name** > **Change**.
3. Enter a new name (e.g., `DC01` or `AD-Primary`).
4. Restart the server to apply changes.

![image](https://github.com/user-attachments/assets/37e68c2b-5e56-4b0d-a4b1-068895756264)

---

## Installing AD DS
### Steps to Install:
1. Open **Server Manager** and click **Manage > Add Roles and Features**.
![image](https://github.com/user-attachments/assets/9adaa26a-4ebf-48ae-9048-d547e0b10b14)

3. Select **Role-based or feature-based installation**.
4. Choose the local server and check **Active Directory Domain Services (AD DS)**.
![image](https://github.com/user-attachments/assets/6e538786-ec54-4d7d-a3c3-7f9ef7c0e47f)

6. Add any required features, then proceed with the installation.
![image](https://github.com/user-attachments/assets/fd4c713e-63e2-4907-ae54-828d6c65637d)

---

## Promoting the Server to a Domain Controller
1. In **Server Manager**, click the warning flag and select **Promote this server to a domain controller**.
![image](https://github.com/user-attachments/assets/2b0d931c-b8bd-4f9b-838f-53a6dcdbf2d0)

3. Choose:


   - **Add a new forest** (if creating a new domain) and specify the root domain name (e.g., `example.local`).
![image](https://github.com/user-attachments/assets/27d7ec3e-399c-4c27-b40f-1220905730f3)

5. Configure options:
   - Set **Functional Levels** (highest supported version).
   - Enable **DNS Server** if needed.
   - Set the **Directory Services Restore Mode (DSRM) password**.
![image](https://github.com/user-attachments/assets/e28b705e-3c4f-4348-ae5e-7e75dde984bf)
![image](https://github.com/user-attachments/assets/a14b21d7-7125-44b2-bdcd-aeb064687922)

6. Complete the wizard and allow the server to restart.

---

## Post-Installation Configuration
1. Log in using the domain admin account (e.g., `yourdomain\Administrator`).
2. Verify AD DS functionality via **Active Directory Users and Computers** in **Server Manager**.
![image](https://github.com/user-attachments/assets/5f52c18d-cc15-44cb-967f-a8cf2929e3eb)

---

## Managing Active Directory

### Creating Organizational Units
1. Open **Active Directory Users and Computers**.
2. Navigate to your domain, right-click, and select **New > Organizational Unit**.
3. Enter a name (e.g., `IT_Department`).
4. Ensure **Protect container from accidental deletion** is checked.

![image](https://github.com/user-attachments/assets/2b4b8e4b-f7f0-42b9-89b0-a285f430ba84)
![image](https://github.com/user-attachments/assets/659029ba-3968-4c71-b2a4-72dbd080b90f)


---

### Adding Users
1. Navigate to the desired OU, right-click, and select **New > User**.
3. Fill in details (e.g., `jdoe`) and set a password.
4. Configure options such as requiring the user to change their password at next login.
![image](https://github.com/user-attachments/assets/710239f3-858a-4939-8137-e002965dc0a2)

![image](https://github.com/user-attachments/assets/fc044f8b-482d-4482-8623-ecdf09688c4e)

#### Resetting Passwords
1. Right-click the user account and select **Reset Password**.
2. Enter and confirm the new password.
![image](https://github.com/user-attachments/assets/5bf86bda-480e-4328-b2e9-d938569d9c7d)

#### Enable/Disable a User Account
To disable an account temporarily (e.g., for security reasons):
1. In Active Directory Users and Computers, right-click the user account.
2. Select Disable Account.

![image](https://github.com/user-attachments/assets/2c319e7b-9669-4660-891c-07eec66e3076)

3. To re-enable, right-click the account and select Enable Account.
   
![image](https://github.com/user-attachments/assets/23d23c53-b09f-46ff-9bb6-1c9d52a93be8)

#### Delete a User Account
To remove an account permanently:
1. Right-click the user in Active Directory Users and Computers.
2. Select Delete, then confirm the deletion.


If you want to create a computer account before joining the computer to the domain:

1. Open Active Directory Users and Computers
Go to Server Manager > Tools > Active Directory Users and Computers.
2. Navigate to the Appropriate OU
By default, computers are placed in the Computers container.
If you have a dedicated Organizational Unit (OU) for computers (e.g., Workstations, Servers), navigate to it.
3. Create a New Computer Account
Right-click the OU or container where you want to add the computer.
Select New > Computer.
4. Configure Computer Properties
Enter a Computer Name (e.g., PC01, HR-Laptop01).
Optionally, configure the following:
User or Group: Click Change to specify which user or group can join this computer to the domain. By default, domain admins have this right.
Description: Add a brief description for reference.
5. Save the Computer Account
Click OK to create the computer account.
![image](https://github.com/user-attachments/assets/1acd9475-b95c-4719-8216-10dc363d5ce6)

---

### Setting Password Policies
1. Open **Group Policy Management**.
![image](https://github.com/user-attachments/assets/673fd2fc-fee3-4987-a05a-c91393247b48)

2. Edit the **Default Domain Policy**:
   - Navigate to `Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy`.
     
![image](https://github.com/user-attachments/assets/315b9f2c-1409-411d-80c0-fafaba3989ab)

   - Configure settings like:
     - **Minimum password length: Set minimum password characters.**
     - **Password complexity requirements: Enforces special character, uppercase, etc.**
     - **Maximum password age: Specifies how long passwords are valid before requiring a change.**
     - **Enforce password history: Prevents reusing recent passwords**.

3. Close the editor, and the policies will apply automatically across the domain.
---

### Managing Groups
#### Creating a Group
1. Right-click the desired OU and select **New > Group**.
2. Enter a name (e.g., `IT_Staff`) and choose:
   - **Group Scope**: Domain Local, Global, or Universal.
   - **Group Type**: Security or Distribution.

Group Scope: 
> - Domain Local: For permissions within the domain (e.g., resource access).
> - Global: For organizing users across the domain and assigning permissions.
> - Universal: For multi-domain or forest-wide access and permissions.

Group Type:
> - Security: Used for permissions (e.g., granting file or folder access).
> - Distribution: Used for email distribution lists (doesn’t manage permissions).

![image](https://github.com/user-attachments/assets/bdbef627-0987-45c8-b1e5-4f9687b9eeab)
![image](https://github.com/user-attachments/assets/87a41306-37a4-4c04-a2d3-fcc0b1146cbf)

#### Adding Users to a Group
Creating groups in Active Directory allows you to efficiently manage permissions and assign rights to multiple users at once.
1. Open the user's properties, go to **Member Of**, and click **Add**.
2. Enter the group name and confirm.

![image](https://github.com/user-attachments/assets/4daad44e-eb8e-4939-9182-1d5a183eafeb)

![image](https://github.com/user-attachments/assets/6e05edd5-5c00-40c7-b6b2-6e33aeafe537)

---

### Delegating Control
1. Right-click an OU and select **Delegate Control**.

![image](https://github.com/user-attachments/assets/6daa0e23-e4c2-48fb-95b4-f3a87675cdf5)

3. Add the user or group to delegate.

![image](https://github.com/user-attachments/assets/50d69f85-ec02-44fc-b478-92e198a68e07)

5. Select tasks to delegate (e.g., resetting passwords, creating user accounts).

![image](https://github.com/user-attachments/assets/9aa3db00-f3ea-4d9a-8238-1f69f98be1da)

---

## Group Policy Management
Group Policy allows centralized management of settings for users and computers.

Scope: GPOs can be applied at different levels:
> - Site: Applies to all users and computers in a site.
> - Domain: Applies to all users and computers in the domain.
> - Organizational Unit (OU): Applies to specific OUs.

### Steps to Configure:
1. Open **Group Policy Management**.
2. Create a new GPO:
   - Right-click **Group Policy Objects** > **New**.
   - Name the GPO (e.g., `PasswordPolicy`).
3. Edit the GPO:
   - Navigate to `Computer Configuration` or `User Configuration` depending on the policy.
   - Configure settings such as software deployment, logon scripts, or security restrictions.
![image](https://github.com/user-attachments/assets/e9ff3137-5f2a-4d61-aab0-d4a2cbe84244)

#### Linking GPOs
1. Right-click the desired domain or OU and select **Link an Existing GPO**.
2. Select the GPO to apply.

![image](https://github.com/user-attachments/assets/ce13a7c8-3655-45c9-9698-805c13d9eaeb)

#### Filtering GPOs
- Use **Security Filtering** to apply the GPO to specific users/groups.
- Use **WMI Filters** to target specific criteria (e.g., OS version).
![image](https://github.com/user-attachments/assets/02b56b22-804b-4173-9b59-9af2aa9487d6)

---
6. Configure Common Group Policy Settings
Account and Security Policies
Navigate to:
Copy code
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies
Set policies like password requirements, account lockout, and Kerberos settings.

![image](https://github.com/user-attachments/assets/b1de5a1c-d002-4ed3-b838-f774735f7e31)

Restrict User Actions
Navigate to:
mathematica
Copy code
User Configuration > Policies > Administrative Templates > Control Panel
Disable access to specific features, like the Control Panel.

![image](https://github.com/user-attachments/assets/764193e4-b2a7-4a27-b3ad-11540da736b1)

Logon Scripts
Navigate to:
scss
Copy code
User Configuration > Policies > Windows Settings > Scripts (Logon/Logoff)
Add logon scripts to automate tasks.

![image](https://github.com/user-attachments/assets/4decc82a-f83b-48b4-8eae-401c1943aca9)

Software Deployment
Navigate to:
Copy code
Computer Configuration > Policies > Software Settings > Software Installation
Add software packages for deployment via .msi files.

![image](https://github.com/user-attachments/assets/f7a1401c-7c10-464c-bee5-396478c6c940)
