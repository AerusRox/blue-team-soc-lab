# Sysmon Installation & Configuration

Configuration guide for installing Sysmon on the Windows 10 victim machine to capture detailed endpoint telemetry.

## 📌 Overview

Sysmon (System Monitor) is a Windows system service and device driver that logs system activity to the Windows Event Log. It provides detailed information about process creation, network connections, file changes, and more — making it essential for threat detection.

## 📥 Step 1: Download Sysmon

1. Go to the official Microsoft Sysinternals page:  
   [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
2. Download **Sysmon.zip**.
3. Extract the ZIP file to `C:\Sysmon`.

You should now have `Sysmon64.exe` in `C:\Sysmon`.

## 📄 Step 2: Download a Configuration File

Sysmon needs a configuration file to know what to log. We'll use the **SwiftOnSecurity** config, a widely used and well‑maintained baseline.

Open **PowerShell as Administrator** and run:

```powershell
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/SwiftOnSecurity/sysmon-config/master/sysmonconfig-export.xml" -OutFile "C:\Sysmon\sysmonconfig.xml"
