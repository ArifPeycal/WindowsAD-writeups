# WindowsAD-writeups

![image](https://github.com/user-attachments/assets/5ab7685b-5465-4f6e-954f-fee2842089ba)

Name your server

Naming a Windows Server, especially one that will be a Domain Controller, is an important step as it helps identify the server within your network and avoids conflicts. For example: DC01 for the first Domain Controller or AD-Primary if it's the primary AD server. 

Steps to Change the Server Name:
- Open Server Manager on the Windows Server.
- Go to Local Server and find Computer Name.
- Click on the current name, then select Change.
- Enter the new name and click OK.

![image](https://github.com/user-attachments/assets/37e68c2b-5e56-4b0d-a4b1-068895756264)

- Restart the server to apply the change.

![image](https://github.com/user-attachments/assets/37e68c2b-5e56-4b0d-a4b1-068895756264)

Step 2: Install the Active Directory Domain Services (AD DS) Role
Log in to the Windows Server VM with an administrator account.
Open Server Manager.
Click on Manage > Add Roles and Features.
![image](https://github.com/user-attachments/assets/9adaa26a-4ebf-48ae-9048-d547e0b10b14)

In the Add Roles and Features Wizard:
Choose Role-based or feature-based installation.
Select the local server for the installation.

In the Server Roles section, check Active Directory Domain Services.
![image](https://github.com/user-attachments/assets/6e538786-ec54-4d7d-a3c3-7f9ef7c0e47f)

You may be prompted to add features that AD DS depends on; click Add Features.
Click Next and then Install to begin the installation process.
![image](https://github.com/user-attachments/assets/fd4c713e-63e2-4907-ae54-828d6c65637d)

tep 3: Promote the Server to a Domain Controller
Once AD DS is installed, in Server Manager, click on the Flag icon (which will show a warning) and select Promote this server to a domain controller.
![image](https://github.com/user-attachments/assets/2b0d931c-b8bd-4f9b-838f-53a6dcdbf2d0)

In the Deployment Configuration window, you have several options:
To create a new domain forest, select Add a new forest and provide a root domain name (e.g., example.local).
![image](https://github.com/user-attachments/assets/27d7ec3e-399c-4c27-b40f-1220905730f3)

Configure the Domain Controller Options:
Set the Forest Functional Level and Domain Functional Level (typically, the highest version your environment supports).
Enable Domain Name System (DNS) Server (if this is your only DNS server).
Enter a Directory Services Restore Mode (DSRM) password (used for recovery).
![image](https://github.com/user-attachments/assets/e28b705e-3c4f-4348-ae5e-7e75dde984bf)

Proceed through the Additional Options, Paths, and Review sections. The Prerequisites Check will run to ensure there are no conflicts.
![image](https://github.com/user-attachments/assets/a14b21d7-7125-44b2-bdcd-aeb064687922)

Click Install after the check completes successfully.

Step 4: Post-Installation Configuration
The server will automatically restart to apply changes.
After rebooting, log in with the new domain admin account (e.g., yourdomain\Administrator).

![image](https://github.com/user-attachments/assets/5f52c18d-cc15-44cb-967f-a8cf2929e3eb)

Verify that AD DS is functioning by opening Active Directory Users and Computers in Server Manager.

Managing users in Active Directory (AD) involves tasks like adding new users, forcing password changes, setting up password policies, and managing group memberships. Here’s a guide on how to perform these tasks in Active Directory:


Creating an Organizational Unit (OU) in Active Directory allows you to organize users, computers, and other AD objects logically. This setup makes it easier to manage permissions, apply Group Policies, and delegate administrative control. Here’s how to create an OU in Active Directory:

Steps to Create an Organizational Unit (OU)
Open Active Directory Users and Computers:

Go to Server Manager > Tools > Active Directory Users and Computers.
Navigate to Your Domain:

In the left panel, expand your domain name (e.g., example.com).
Create a New OU:

Right-click on the domain or an existing OU where you want to create the new OU.
Select New > Organizational Unit.
![image](https://github.com/user-attachments/assets/fa8800b3-9c04-4802-b712-a41a3cb4f9a5)

Name the OU:

In the New Object - Organizational Unit dialog box, enter a descriptive name for the OU.
Example: Sales, IT_Department, NewYork_Office.
![image](https://github.com/user-attachments/assets/2b4b8e4b-f7f0-42b9-89b0-a285f430ba84)

![image](https://github.com/user-attachments/assets/659029ba-3968-4c71-b2a4-72dbd080b90f)

Ensure Protect container from accidental deletion is checked. This prevents accidental deletions, which can be helpful for critical OUs.
Finish the Creation:

Click OK or Finish.


1. Add a New User in Active Directory
Open Server Manager and go to Tools > Active Directory Users and Computers.
![image](https://github.com/user-attachments/assets/a9af1e2d-ec7d-4911-bd4e-56ffbdb43c49)

Navigate to the Organizational Unit (OU) where you want to create the user (e.g., Users).
Right-click the OU, select New > User.
Fill in the user details:
First name, Last name, User logon name (e.g., jdoe).

Click Next and enter a password for the user:
You can configure whether the user must change the password at the next login.
Click Next and Finish to create the user account.
![image](https://github.com/user-attachments/assets/710239f3-858a-4939-8137-e002965dc0a2)

![image](https://github.com/user-attachments/assets/fc044f8b-482d-4482-8623-ecdf09688c4e)

. Change a User’s Password
To reset a user’s password in case they’ve forgotten it:
In Active Directory Users and Computers, right-click the user account.
Select Reset Password.
![image](https://github.com/user-attachments/assets/5bf86bda-480e-4328-b2e9-d938569d9c7d)

Enter a new password and confirm it.
You can also check User must change password at next logon to ensure they set a unique password.
Click OK to save the changes.


Set Password Policies
Password policies define requirements like length, complexity, and expiration.
To configure password policies:
Open Group Policy Management from Server Manager > Tools.
Expand your domain, right-click Default Domain Policy, and select Edit.
![image](https://github.com/user-attachments/assets/673fd2fc-fee3-4987-a05a-c91393247b48)

In the Group Policy Editor, go to:
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy.
![image](https://github.com/user-attachments/assets/315b9f2c-1409-411d-80c0-fafaba3989ab)

Configure settings like:
Enforce password history: Prevents reusing recent passwords.
Minimum password length: Set minimum password characters.
Password must meet complexity requirements: Enforces special character, uppercase, etc.
Maximum password age: Specifies how long passwords are valid before requiring a change.
Close the editor, and the policies will apply automatically across the domain.


Creating groups in Active Directory allows you to efficiently manage permissions and assign rights to multiple users at once. Here’s a step-by-step guide on how to create groups in Active Directory:

Steps to Create a Group in Active Directory
1. Open Active Directory Users and Computers
Go to Server Manager > Tools > Active Directory Users and Computers.
2. Navigate to the Desired Location
In the left pane, navigate to the Organizational Unit (OU) or container where you want to create the group (e.g., Users, Groups, or a custom OU like IT_Department).
3. Create the Group
Right-click on the OU or container.
Select New > Group.
![image](https://github.com/user-attachments/assets/bdbef627-0987-45c8-b1e5-4f9687b9eeab)

5. Set Group Information
Group Name: Enter a descriptive name for the group (e.g., Sales_Team, Admins, IT_Staff).
Group Scope:
Domain Local: For permissions within the domain (e.g., resource access).
Global: For organizing users across the domain and assigning permissions.
Universal: For multi-domain or forest-wide access and permissions.
Group Type:
Security: Used for permissions (e.g., granting file or folder access).
Distribution: Used for email distribution lists (doesn’t manage permissions).
Choose the appropriate scope and type for your use case.
6. Save the Group
Click OK to create the group.
![image](https://github.com/user-attachments/assets/87a41306-37a4-4c04-a2d3-fcc0b1146cbf)

Add Users to Groups
Groups are used to assign permissions to multiple users easily.
To add a user to a group:
In Active Directory Users and Computers, find and open the user’s Properties.
Go to the Member Of tab and click Add.
Type the group name (e.g., Domain Users, IT_Support) and click Check Names.
![image](https://github.com/user-attachments/assets/4daad44e-eb8e-4939-9182-1d5a183eafeb)

Once the group is confirmed, click OK to add the user to the group.

![image](https://github.com/user-attachments/assets/6e05edd5-5c00-40c7-b6b2-6e33aeafe537)

6. Enable/Disable a User Account
To disable an account temporarily (e.g., for security reasons):
In Active Directory Users and Computers, right-click the user account.
Select Disable Account.
![image](https://github.com/user-attachments/assets/2c319e7b-9669-4660-891c-07eec66e3076)

To re-enable, right-click the account and select Enable Account.
![image](https://github.com/user-attachments/assets/23d23c53-b09f-46ff-9bb6-1c9d52a93be8)

Delete a User Account
To remove an account permanently:
Right-click the user in Active Directory Users and Computers.
Select Delete, then confirm the deletion.

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

Here’s how to delegate tasks to users in Active Directory:

1. Open Active Directory Users and Computers
On the domain controller or a machine with administrative tools:
Go to Server Manager > Tools > Active Directory Users and Computers.
2. Navigate to the Organizational Unit (OU)
In the left-hand pane, expand your domain and locate the OU where you want to delegate permissions.
Example: HR_Department, IT_Team.
3. Launch the Delegation of Control Wizard
Right-click the OU and select Delegate Control.
![image](https://github.com/user-attachments/assets/6daa0e23-e4c2-48fb-95b4-f3a87675cdf5)

The Delegation of Control Wizard will open.
5. Add the User or Group
Click Next.
Click Add to select the user or group you want to delegate control to:
In the dialog box, type the name of the user or group.
Click Check Names to verify the entry.
Click OK, then Next.
![image](https://github.com/user-attachments/assets/50d69f85-ec02-44fc-b478-92e198a68e07)

6. Select Tasks to Delegate
Choose one of the following options:
Common tasks: Select predefined tasks like:
Resetting user passwords and unlocking accounts.
Creating, deleting, and managing user accounts.
Managing group membership.
Managing specific Group Policies.
Custom task delegation:
Select this option to specify advanced permissions for specific objects (e.g., files, printers, or custom AD attributes).
![image](https://github.com/user-attachments/assets/9aa3db00-f3ea-4d9a-8238-1f69f98be1da)

Click Next.
8. Specify Permissions (For Custom Tasks)
If you selected Custom task delegation:
Choose whether the delegated permissions apply to this OU only or include all child objects.
Specify the object types (e.g., Users, Groups, or Computers).
Assign the necessary permissions by checking the appropriate boxes (e.g., Read, Write, Modify).
9. Finish the Delegation
Review the summary of permissions to be granted and click Finish.
10. Verify Delegated Permissions
After delegation, test the permissions:
Log in as the delegated user or member of the group.
Attempt the delegated tasks (e.g., resetting a password, creating a user, or managing groups).




Group Policy is a powerful feature in Active Directory that allows you to manage settings and configurations for users and computers across your domain. Here’s a step-by-step guide to setting up and managing Group Policy:

1. Open Group Policy Management
Log in to your Domain Controller.
Open Server Manager > Tools > Group Policy Management (GPMC).
2. Understand Group Policy Basics
Group Policy Object (GPO): A set of rules applied to users or computers in the domain.
Scope: GPOs can be applied at different levels:
Site: Applies to all users and computers in a site.
Domain: Applies to all users and computers in the domain.
Organizational Unit (OU): Applies to specific OUs.
3. Create a New GPO
In the Group Policy Management console:
Expand your domain (e.g., example.local).
Right-click the Group Policy Objects container and select New.
Give the GPO a descriptive name (e.g., PasswordPolicy, SoftwareDeployment).
4. Edit the GPO
Right-click the GPO and select Edit to open the Group Policy Management Editor.
Configure settings in the following sections:
Computer Configuration: Policies that apply to computers.
User Configuration: Policies that apply to users.
![image](https://github.com/user-attachments/assets/e9ff3137-5f2a-4d61-aab0-d4a2cbe84244)

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

8. Link the GPO
To apply the GPO, link it to a site, domain, or OU:
Right-click the domain or OU where you want the GPO applied and select Link an Existing GPO.
Choose your GPO from the list and click OK.

![image](https://github.com/user-attachments/assets/ce13a7c8-3655-45c9-9698-805c13d9eaeb)

10. Filter GPO Application
Security Filtering: Apply the GPO only to specific users or groups.
In the Scope tab of the GPO, remove Authenticated Users and add specific groups or users.
WMI Filters: Use WMI filters to target GPOs based on specific computer criteria, such as OS version.
![image](https://github.com/user-attachments/assets/02b56b22-804b-4173-9b59-9af2aa9487d6)


