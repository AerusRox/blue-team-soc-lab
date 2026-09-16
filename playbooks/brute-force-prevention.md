
# Brute Force Prevention Playbook


## 📌 Overview

Brute force attacks attempt to gain unauthorized access by systematically trying many passwords. This playbook covers:

- **Prevention measures** to reduce the risk of a successful brute force attack.
- **Detection** using Splunk and Windows Event ID 4625.
- **Response steps** for L1 analysts when an attack is detected.

**MITRE ATT&CK Mapping:**  
- **T1110** – Brute Force  
- **T1078** – Valid Accounts

## 🛡️ Prevention Measures

| Measure | How to Implement |
| :--- | :--- |
| **Account Lockout Policy** | Lock account after 5 failed attempts for 15 minutes. |
| **Strong Password Policy** | Require minimum 12 characters, complexity, and history. |
| **Multi-Factor Authentication (MFA)** | Enable MFA for all administrative and remote access accounts. |
| **RDP Restrictions** | Limit RDP access to specific IP addresses or VPN only. |
| **Network Level Authentication (NLA)** | Require NLA for RDP connections. |
| **Fail2Ban / Firewall Blocking** | Automatically block IPs after repeated failures using pfSense or Windows Firewall. |
| **Disable Unused Accounts** | Disable default accounts like `Administrator` if not needed. |
| **Monitor and Alert** | Set up Splunk alerts for Event ID 4625 to detect attacks early. |

## 🔍 Detection

Use the following Splunk searches to detect brute force activity.

### Basic Detection (Multiple Failures from One IP)
```spl
index=windows_security EventCode=4625
| stats count by Source_Network_Address
| where count > 5
| sort - count
