# Windows Logging Configuration

Configuration guide for enabling advanced audit policies and firewall logging on the Windows 10 victim machine.

## 📌 Overview

By default, Windows does not log all security‑relevant events. To detect attacks such as brute force (Event ID 4625) and port scans (Event IDs 5156/5157), you must enable specific audit policies and firewall logging.

This guide covers:
- Advanced Audit Policy configuration
- Windows Defender Firewall logging
- Verification steps

## 🔧 Step 1: Enable Advanced Audit Policy

Open **Command Prompt as Administrator** and run the following commands:

```cmd
auditpol /set /subcategory:"Logon" /success:enable /failure:enable
auditpol /set /subcategory:"Filtering Platform Connection" /success:enable /failure:enable
auditpol /set /subcategory:"Process Creation" /success:enable /failure:enable
auditpol /set /subcategory:"Account Lockout" /success:enable /failure:enable
