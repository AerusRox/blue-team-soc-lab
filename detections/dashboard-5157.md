
# Blocked Connections Dashboard (Event ID 5157)

Splunk dashboard for monitoring blocked connection attempts on the Windows 10 victim machine.

## 📌 Overview

Windows Event ID **5157** is generated whenever the Windows Filtering Platform **blocks** a network connection. Monitoring these events is critical for detecting:

- Port scans
- Brute force attempts
- Suspicious outbound connections
- Unauthorized access attempts

This dashboard provides real‑time visibility into blocked traffic, helping L1 analysts identify and respond to network‑based attacks.

**MITRE ATT&CK Mapping:**  
- **T1046** – Network Service Scanning  
- **T1110** – Brute Force  
- **T1071** – Application Layer Protocol

## 📊 Dashboard Panels

The dashboard contains five panels. Each panel uses a specific Splunk search and chart type.

| Panel | Search | Chart Type |
| :--- | :--- | :--- |
| **1. Blocked Connections Over Time** | `index=windows_security EventCode=5157 \| timechart count` | Line Chart |
| **2. Top Source IPs (Attackers)** | `index=windows_security EventCode=5157 \| stats count by Source_Address \| sort - count \| head 10` | Bar Chart (Horizontal) |
| **3. Top Destination Ports** | `index=windows_security EventCode=5157 \| stats count by Destination_Port \| sort - count \| head 10` | Bar Chart (Horizontal) |
| **4. Recent Blocked Connections** | `index=windows_security EventCode=5157 \| table _time, Source_Address, Destination_Address, Destination_Port, Protocol \| sort - _time \| head 20` | Table |
| **5. Port Scan Detection** | `index=windows_security EventCode=5157 \| stats dc(Destination_Port) as unique_ports by Source_Address \| where unique_ports > 10 \| sort - unique_ports` | Table |

> **Note:** The index name `windows_security` may vary depending on your `inputs.conf`. Adjust if needed.

## 🛠️ How to Create the Dashboard

1. In Splunk Cloud, go to **Dashboards → Create New Dashboard**.
2. Name it: **Blocked Connections (5157)**.
3. Click **Add Panel → New**.
4. Paste each search, give it a title, and select the recommended chart type.
5. Click **Apply** and then **Save**.
6. Repeat for all five panels.

## 📸 Screenshot

![Dashboard 5157](../screenshots/dashboard-5157.png)

> **Privacy Note:** All IP addresses and usernames in screenshots are masked to protect sensitive information.

## 🧪 Example Detections

### Detect Port Scan (More Than 10 Unique Ports from One IP)
```spl
index=windows_security EventCode=5157
| stats dc(Destination_Port) as unique_ports by Source_Address
| where unique_ports > 10
| sort - unique_ports
