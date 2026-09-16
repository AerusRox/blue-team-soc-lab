
# Port Scan Prevention Playbook

## 📌 Overview

Port scanning is used by attackers to discover open ports and services on a target system. It is often the first step in a larger attack. This playbook covers:

- **Prevention measures** to reduce the attack surface and block scans.
- **Detection** using Splunk and Windows Event IDs **5156** (allowed) and **5157** (blocked).
- **Response steps** for L1 analysts when a scan is detected.

**MITRE ATT&CK Mapping:**  
- **T1046** – Network Service Scanning  
- **T1595** – Active Scanning

## 🛡️ Prevention Measures

| Measure | How to Implement |
| :--- | :--- |
| **Firewall Rules** | Block unnecessary inbound ports at pfSense and Windows Firewall. |
| **IDS/IPS** | Enable Suricata or Snort on pfSense to detect and block scans. |
| **Rate Limiting** | Limit connection attempts per IP per second on pfSense. |
| **Port Knocking** | Hide sensitive services (e.g., SSH, RDP) behind port knocking. |
| **Network Segmentation** | Separate critical systems from user networks using VLANs. |
| **Disable Unused Services** | Stop or disable services that are not required (e.g., SMBv1, Telnet). |
| **Honeypots** | Deploy honeypots to detect and divert scanners. |
| **Logging and Monitoring** | Enable Windows Firewall logging (Event IDs 5156/5157) and forward to Splunk. |

## 🔍 Detection

Use the following Splunk searches to detect port scanning activity.

### Basic Detection (Multiple Ports from One IP – Allowed Connections)
```spl
index=windows_security EventCode=5156
| stats dc(Destination_Port) as unique_ports by Source_Address
| where unique_ports > 10
| sort - unique_ports
