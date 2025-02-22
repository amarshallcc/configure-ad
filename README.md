<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

<p>
<strong>1. Microsoft Azure (Virtual Machines/Compute)</strong>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
What it does: Azure provides virtual machines (VMs) that act like real computers in the cloud. These VMs can run different operating systems and be used to host applications, store data, or manage networks.

Purpose: This step is about setting up and managing cloud-based computers (VMs) in Azure, making it possible to run software and services without needing physical hardware.

Steps:

Create a Resource Group – This is like a folder in Azure that helps organize all your cloud resources.
Create a Virtual Network and Subnet – This sets up the “road system” that allows different VMs to communicate.
Create the Domain Controller VM (DC-1) – This is a Windows Server that will act as the central hub for managing users and devices.
Set the Domain Controller’s Private IP Address to Static – Ensures the server keeps the same IP address, which is important for networking.
Create a Client VM (Client-1) – This is a regular Windows 10 computer that will connect to the domain controller.
Attach Client-1 to the Same Virtual Network as DC-1 – This allows them to communicate within the same network.
Set Client-1’s DNS to DC-1’s Private IP Address – Makes sure Client-1 can find and connect to the domain controller.
Restart Client-1 and Verify Connection to DC-1 – Ensures the setup is working correctly.

<p>

<strong>2. Remote Desktop into the client</strong>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
What it does: Remote Desktop allows you to access and control a computer from another location, as if you were sitting right in front of it.

Purpose: This step ensures that IT administrators can manage machines remotely, troubleshoot issues, and configure settings without needing physical access.

Steps:

Log into Client-1 as an Admin – Use the “jane_admin” account for administrative access.
Open System Properties and Enable Remote Desktop – This allows users to connect remotely to the machine.
Allow “Domain Users” Access to Remote Desktop – Ensures that non-admin users can log in remotely if needed.
Test Remote Access by Logging in as a Normal User – Verifies that the setup is working correctly.

</p>
<strong>3. Active Directory Domain Services (ADDS)</strong>
</p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
What it does: Active Directory is like a company directory that keeps track of users, computers, and security settings in a network. It controls who can log in, what they can access, and how everything is organized.

Purpose: This step sets up a system to manage users and security policies efficiently, making sure only authorized people can access specific resources.

Steps:

Log into DC-1 and Install Active Directory Domain Services (ADDS) – This turns the server into a domain controller, which manages users and security.
Promote the Server to a Domain Controller (mydomain.com) – Establishes a new network directory for managing users and computers.
Restart and Log in as “mydomain.com\labuser” – Ensures the domain controller is properly set up.
Create Organizational Units (OUs) – These are folders that help organize users and computers:
“_EMPLOYEES” – For regular users.
“_ADMINS” – For IT administrators.
“_CLIENTS” – For company computers.
Create a New Admin User (jane_admin) – Gives administrative access to a specific user.
Join Client-1 to the Domain (mydomain.com) – Connects the client machine to the domain so it can be managed centrally.
Verify Client-1 in Active Directory – Confirms that the computer has successfully joined the domain.
Move Client-1 to the “_CLIENTS” OU – Keeps things organized.


<strong>4. PowerShell</strong>
</p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
What it does: PowerShell is a command-line tool that automates tasks, making it easier to manage systems, create users, and configure settings.

Purpose: This step is about using PowerShell to automate user creation and other administrative tasks instead of doing them manually.

Steps:

Log into DC-1 as jane_admin – Use the admin account for performing administrative tasks.
Open PowerShell as an Administrator – Ensures access to system-level commands.
Create a New Script File in PowerShell_ise – This allows us to run multiple commands at once.
Paste and Run a Script to Create Multiple Users – Instead of manually creating users one by one, this script automates the process.
Verify the New Users in Active Directory – Ensures that the script worked and users were created properly.
Attempt to Log into Client-1 with a New User Account – Confirms that the new accounts can log into the system.

<p>
