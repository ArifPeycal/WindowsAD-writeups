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
You may be prompted to add features that AD DS depends on; click Add Features.
Click Next and then Install to begin the installation process.

