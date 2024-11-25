# Standard Operating Procedure (SOP) for Setting Up Active Directory Domain Services (ADDS) for _Spiral Network_

**Company Name:** Spiral Network  
**Address:** 130 Henlow Bay.  
**Department:** IT Department  
**Version:** 1.0  
**Written by:** Mike Ogunyemi  
**Approved by:** Head of IT Depertmant - Mike Ogunyemi  
**Date:** 11/22/2024  

---

## Purpose

This Standard Operating Procedure (SOP) describes the steps required to set up Active Directory Domain Services (ADDS) on a Windows Server machine. 
It includes instructions for installing the ADDS role, promoting a server to a Domain Controller, and verifying that the domain is functional.

## Application

This SOP applies to IT administrators and network engineers who are responsible for setting up and managing Active Directory in Spiral Network. 
It is intended for use when configuring a new Windows Server as a Domain Controller in a new or existing Active Directory environment.

## Definitions
_Key words to note_

- **ADDS (Active Directory Domain Services):** A set of services in Windows Server that provides directory services for managing users, computers, and other resources.
- **Domain Controller (DC):** A server that is responsible for handling all authentication and authorization within a Windows domain.
- **DNS (Domain Name System):** A hierarchical system that translates domain names (e.g., spiralnetwork.ca) into IP addresses.
- **DSRM (Directory Services Restore Mode):** A special mode used for recovering Active Directory when a Domain Controller is inoperable.
  
## Procedures

### Step 1: Prepare the Server

1. **Verify System Requirements**:  
   Ensure the server meets the hardware and software requirements for Active Directory Domain Services (ADDS).

2. **Configure Static IP**:  
   Set a static IP address on the server. This is critical for ensuring the server remains accessible on the network and as a DNS server if necessary.

3. **Configure DNS**:  
   In the server's network settings, configure the DNS server to point to the server's own IP address if it will act as the DNS server.

4. **Rename the Server (Optional)**:  
   Rename the server if necessary by navigating to **Control Panel > System and Security > System > Change Settings** and selecting *Change* to modify the computer name. Reboot if the name is changed.

### Step 2: Install the ADDS Role

1. Open **Server Manager** from the Start menu.
2. Click **Manage** in the top right corner, then select **Add Roles and Features**.
3. In the **Add Roles and Features Wizard**, click **Next** until reaching the **Select Features** page.
4. On the **Roles** tab, check **Active Directory Domain Services** and click **Next**.
5. On the **Select Features** page, no additional features are necessary. Click **Next** and then **Install**.
6. Wait for the installation to complete. Once done, click **Close**.

### Step 3: Promote the Server to Domain Controller

1. In **Server Manager**, click the **Notification flag** and select **Promote this server to a domain controller**.
2. **Deployment Configuration**:
   - Select **Add a new forest** and specify the **Root domain name** (e.g., 'spiralnetwork.ca').
3. **Domain Controller Options**:
   - Choose the forest and domain functional levels (e.g., Windows Server 2019 or higher).
   - Set a strong **DSRM password** for recovery purposes.
4. **DNS Options**:  
   Confirm DNS server configuration or allow the system to handle it automatically.
5. **Review**:  
   Review all settings and click **Install** to begin the promotion process.
6. The server will automatically restart to complete the promotion to a Domain Controller.

### Step 4: Verify Domain Controller Installation

1. After the server reboots, log in using the **Administrator** account for the domain (e.g., `Administrator@spiralnetwork.ca`).
2. Open **Active Directory Users and Computers** to verify that the domain is listed and that the server is functioning as a Domain Controller.
3. Confirm DNS functionality by running `nslookup <spiralnetwork.ca>` from the command prompt.

### Step 5: Test Domain Functionality

1. **Join a Client Machine to the Domain**:
   - On a client machine, go to **System Properties > Change Settings** under **Computer name, domain, and workgroup settings**.
   - Select **Domain**, enter the domain name (e.g., `spiralnetwork.ca`), and provide the Domain Admin credentials.
2. **Log in** to the client machine using a domain user account to confirm that the domain is functioning properly.

## Resources

- **Microsoft Documentation for ADDS Setup**:  
   [https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services)

- **Windows Server Backup**:  
   Backup tool to create system and Active Directory backups before any major changes or updates.

- **PowerShell cmdlets**:  
   You can use PowerShell for automating and managing ADDS configurations. For example, `Install-WindowsFeature AD-Domain-Services` to install ADDS via PowerShell.

---

**End**
