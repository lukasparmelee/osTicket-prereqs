# osTicket - Prerequisites and Installation

This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system **osTicket**.  
The goal of this lab was to deploy and configure osTicket within a Windows 10 virtual machine hosted in Microsoft Azure.

---

### 🎥 Video Demonstration
**YouTube:** [How To Install osTicket with Prerequisites](https://www.youtube.com/watch?v=)

---

### 🧰 Environments and Technologies Used
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (RDP)
- Internet Information Services (IIS)
- PHP 7.3.8
- MySQL 5.5.62
- HeidiSQL
- osTicket v1.15.8

---

### 💻 Operating Systems Used
- Windows 10 (21H2)

---

### 🧩 Installation Objectives
1. Create and connect to a Windows 10 virtual machine in Azure  
2. Install and configure IIS with PHP and required extensions  
3. Install MySQL and connect using HeidiSQL  
4. Deploy osTicket to the IIS web root and complete setup  
5. Verify successful installation and secure configuration files  

---

## ⚙️ Installation Steps

### Step 1: Create and Connect to Azure Virtual Machine
- Created a **Windows 10 VM** in Azure named `osticket-vm` (4 vCPUs)  
- Credentials:
  - Username: `labuser`  
  - Password: `osTicketPassword1!`  
- Connected to the VM using **Remote Desktop Protocol (RDP)**  

<p align="center">
  <img src="./ss-1.png" alt="Azure VM setup" width="80%"/>
</p>

---

### Step 2: Install IIS with CGI
Opened **Windows Features** and enabled the following:
- **Internet Information Services (IIS)**  
- **World Wide Web Services → Application Development Features → [✔] CGI**

<p align="center">
  <img src="./ss-2.png" alt="IIS Configuration" width="80%"/>
</p>

Verified IIS was working by navigating to `http://localhost` and confirming the IIS default web page.

---

### Step 3: Install PHP and Dependencies
From the `osTicket-Installation-Files` folder:
1. Installed **PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)**  
2. Installed **URL Rewrite Module (rewrite_amd64_en-US.msi)**  
3. Created the directory `C:\PHP`  
4. Extracted **PHP 7.3.8** to `C:\PHP`  
5. Installed **VC_redist.x86.exe**  

Registered PHP with IIS using **PHP Manager** (`C:\PHP\php-cgi.exe`), then reloaded IIS.  

<p align="center">
  <img src="./PHP-SS.png" alt="PHP Installation" width="80%"/>
</p>

---

### Step 4: Install MySQL
Installed **MySQL 5.5.62 (mysql-5.5.62-win32.msi)**  
Selected *Typical Setup* and configured credentials:
- Username: `root`
- Password: `root`

<p align="center">
  <img src="./sql.png" alt="MySQL Installation" width="80%"/>
</p>

---

### Step 5: Install osTicket
1. Unzipped **osTicket v1.15.8**  
2. Copied the **upload** folder to `C:\inetpub\wwwroot`  
3. Renamed the folder to **osTicket**  
4. Restarted IIS  
5. Opened `http://localhost/osTicket` to start setup  

<p align="center">
  <img src="./os.png" alt="osTicket Installation" width="80%"/>
</p>

Enabled the following PHP extensions from **PHP Manager → Enable or disable an extension**:
- php_imap.dll  
- php_intl.dll  
- php_opcache.dll  

Refreshed the osTicket page to verify they were active.

---

### Step 6: Configure osTicket Files and Permissions
- Renamed  
  `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php` →  
  `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

- Disabled inheritance → Removed all permissions  
- Added new permission: **Everyone → Full Control**

---

### Step 7: Configure MySQL Database in HeidiSQL
Installed **HeidiSQL** and connected with:
- Username: `root`
- Password: `root`

Created a new database named **osTicket**.  

During browser setup:
- MySQL Database: `osTicket`
- MySQL Username: `root`
- MySQL Password: `root`
- Default Admin Account:
  - Username: `Admin1`
  - Password: `179q845Tps`

Clicked **Install Now!** to complete installation.

---

### Step 8: Verify Installation
Successfully accessed:
- **Admin Panel:** [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)  
- **End User Portal:** [http://localhost/osTicket](http://localhost/osTicket)

Confirmed osTicket was fully operational and connected to the database.

---

## 🧾 Summary

This lab demonstrated the complete installation and configuration of osTicket on a Windows 10 virtual machine hosted in Azure.  
It required integration of IIS, PHP, and MySQL, followed by successful deployment and hardening of the osTicket environment.

---

### 🧠 Skills Demonstrated
- Azure Virtual Machine Deployment  
- IIS Web Server Configuration  
- PHP and MySQL Integration  
- osTicket Installation and Hardening  
- Remote Desktop Administration  
- IT Service Management Environment Setup
