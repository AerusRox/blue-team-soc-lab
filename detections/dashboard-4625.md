# Failed Logins Dashboard (Event ID 4625)

Splunk dashboard for monitoring failed logon attempts on the Windows 10 victim machine.

## 📌 Overview

Windows Event ID **4625** is generated whenever a logon attempt fails. Monitoring these events is critical for detecting:

- Brute force attacks
- Password spraying
- Credential stuffing
- Account lockout attempts

This dashboard provides a real‑time view of failed logins, helping L1 analysts triage and respond to credential‑based attacks.

**MITRE ATT&CK Mapping:**  
- **T1110** – Brute Force  
- **T1078** – Valid Accounts

## 📊 Dashboard Panels

The dashboard contains five panels. Each panel uses a specific Splunk search and chart type.

| Panel | Search | Chart Type |
| :--- | :--- | :--- |
| **1. Failed Logins Over Time** | `index=windows_security EventCode=4625 \| timechart count` | Line Chart |
| **2. Top Source IPs (Attackers)** | `index=windows_security EventCode=4625 \| stats count by Source_Network_Address \| sort - count \| head 10` | Bar Chart (Horizontal) |
| **3. Top Targeted Accounts** | `index=windows_security EventCode=4625 \| stats count by TargetUserName \| sort - count \| head 10` | Bar Chart (Horizontal) |
| **4. Recent Failed Logins** | `index=windows_security EventCode=4625 \| table _time, Source_Network_Address, TargetUserName, Logon_Type, Failure_Reason \| sort - _time \| head 20` | Table |
| **5. Brute Force Detection** | `index=windows_security EventCode=4625 \| stats count by Source_Network_Address, TargetUserName \| where count > 5 \| sort - count` | Table |

> **Note:** The index name `windows_security` may vary depending on your `inputs.conf`. Adjust if needed.

## 🛠️ How to Create the Dashboard

1. In Splunk Cloud, go to **Dashboards → Create New Dashboard**.
2. Name it: **Failed Logins (4625)**.
3. Click **Add Panel → New**.
4. Paste each search, give it a title, and select the recommended chart type.
5. Click **Apply** and then **Save**.
6. Repeat for all five panels.


> **Privacy Note:** All IP addresses and usernames in screenshots are masked to protect sensitive information.

## 🧪 Example Detections

### Detect Brute Force (More Than 5 Failures from One IP)
```spl
index=windows_security EventCode=4625
| stats count by Source_Network_Address
| where count > 5
| sort - count
