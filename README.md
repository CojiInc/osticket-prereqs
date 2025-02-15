# osTicket Installation Guide

<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

## osTicket - Prerequisites and Installation
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.

### Video Demonstration
- [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

## Environments and Technologies Used
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

## Operating Systems Used
- Windows 10 (21H2)

## List of Prerequisites
- Microsoft Azure Virtual Machine (Windows 10, 4 vCPUs)
- Remote Desktop Client
- osTicket Installation Files
- Internet Information Services (IIS) with CGI Enabled
- MySQL Database (Version 5.5.62)

## Installation Steps
### 1. Create an Azure Virtual Machine
- Name: `osticket-vm`
- Username: `labuser`
- Password: `osTicketPassword1!`
- Log in using **Remote Desktop**

### 2. Download and Extract osTicket Installation Files
- Download `osTicket-Installation-Files.zip`
- Extract to Desktop as `osTicket-Installation-Files`

### 3. Install and Enable IIS with CGI
1. Open **Windows Features** and enable:
   - `Internet Information Services (IIS)`
   - `World Wide Web Services -> Application Development Features -> [X] CGI`

### 4. Install Required Components
- **Install PHP Manager for IIS** (`PHPManagerForIIS_V1.5.0.msi` from `osTicket-Installation-Files`)
- **Install Rewrite Module** (`rewrite_amd64_en-US.msi`)

### 5. Configure PHP
1. Create directory: `C:\PHP`
2. Extract `php-7.3.8-nts-Win32-VC15-x86.zip` to `C:\PHP`
3. Install **VC Redistributable** (`VC_redist.x86.exe`)

### 6. Install MySQL 5.5.62
- Install `mysql-5.5.62-win32.msi` (Typical Setup)
- Run Configuration Wizard:
  - Standard Configuration
  - Username: `root`
  - Password: `root`

### 7. Configure IIS
- Open **IIS as Admin**
- Register PHP:
  - **PHP Manager** → Set `C:\PHP\php-cgi.exe`
- Reload IIS (Stop and Start Server)

### 8. Install osTicket
1. Extract `osTicket-v1.15.8.zip`
2. Copy `upload` folder to `C:\inetpub\wwwroot`
3. Rename `upload` to `osTicket`
4. Reload IIS (Stop and Start Server)
5. Navigate to **Sites → Default → osTicket**
6. Click **Browse *:80**

### 9. Enable PHP Extensions
- Open IIS → Sites → Default → osTicket
- **PHP Manager** → Enable extensions:
  - `php_imap.dll`
  - `php_intl.dll`
  - `php_opcache.dll`
- Refresh osTicket in browser

### 10. Configure osTicket
- Rename `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php` → `ost-config.php`
- Assign Permissions:
  - **Disable inheritance** → Remove all
  - **New permissions:** Grant `Everyone` **All** access
- Continue osTicket setup in browser:
  - Set **Helpdesk Name** and **Default Email**

### 11. Configure Database
- Install **HeidiSQL**
- Open HeidiSQL → Create a new session (`root/root`)
- Create database: `osTicket`
- Continue browser setup:
  - **MySQL Database:** `osTicket`
  - **MySQL Username:** `root`
  - **MySQL Password:** `root`
  - Click **Install Now!**

### 12. Final Steps
- Access **Admin Panel**: `http://localhost/osTicket/scp/login.php`
- Access **User Portal**: `http://localhost/osTicket/`
- **Clean Up**:
  - Delete `C:\inetpub\wwwroot\osTicket\setup`
  - Set `C:\inetpub\wwwroot\osTicket\include\ost-config.php` to **Read-Only**

## Congratulations! 🎉
Your osTicket helpdesk is now successfully installed and configured!

