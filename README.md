<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# osTicket - Prerequisites and Installation
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.

## Video Demonstration
- [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

## Environments and Technologies Used
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (RDP) – To connect to the Windows 10 VM
- Internet Information Services (IIS) – Web Server for hosting osTicket
- PHP – Backend support for osTicket
- MySQL – Database for osTicket
- HeidiSQL – Database management GUI

## Operating Systems Used
- Windows 10 (21H2)

## List of Prerequisites
1. Create a Windows 10 Virtual Machine in Microsoft Azure  
2. Enable and configure IIS (Internet Information Services)  
3. Install PHP Manager for IIS and Rewrite Module  
4. Download and install PHP (v7.3+ recommended)  
5. Install MySQL Server  
6. Install HeidiSQL to manage the MySQL database  
7. Download and extract osTicket to the IIS web root directory  
8. Configure osTicket permissions and complete setup in the browser  

---

## Installation Steps

### Step 1: Create and connect to the Windows 10 VM
<p align="center">
  <img src="./ss-1.png" alt="Azure VM setup" width="80%"/>
</p>

Used Microsoft Azure to deploy a Windows 10 Virtual Machine as a secure, cloud-based environment for hosting osTicket. Configured networking and inbound security rules, then accessed the VM remotely using Remote Desktop Protocol (RDP). This step established the foundation for installing and managing all other required components.

---

### Step 2: Install and configure IIS
<p align="center">
  <img src="./ss-2.png" height="80%" width="80%" alt="IIS Setup"/>
</p>

Enabled Internet Information Services (IIS) through Windows Features, including required modules like CGI and Common HTTP Features. Verified successful setup by browsing to http://localhost and confirming the IIS default web page loaded. Configured IIS to serve as the main web server for hosting the osTicket application.

---

### Step 3: Install PHP
<p align="center">
  <img src="./PHP-SS.png" height="80%" width="80%" alt="PHP Installation"/>
  Install MySQL
  <img src="./sql.png" height="80%" width="80%" alt="MySQL Installation"/>
  Install osTicket
  <img src="./os.png" height="80%" width="80%" alt="osTicket Installation"/>
</p>

Installed PHP 7.3 and configured it in IIS using PHP Manager and the URL Rewrite Module to ensure compatibility with osTicket. Set up MySQL Server as the backend database and connected via HeidiSQL to create the osTicket database. Downloaded and extracted osTicket into the C:\inetpub\wwwroot\osTicket directory, configured file permissions, and completed the web-based installation wizard. After setup, verified that tickets could be created, assigned, and managed within the osTicket dashboard.

---

## About

This project documents the installation and setup of osTicket, an open-source support ticketing system widely used in IT support and Service Desk environments. It demonstrates the ability to configure and manage server infrastructure, perform IIS and database integration, and deploy a fully functional web-based help desk system.

### Skills Demonstrated
- Azure Virtual Machine Deployment  
- IIS and Web Server Configuration  
- PHP and MySQL Setup  
- Remote Desktop Administration  
- IT Service Management Software Deployment  
