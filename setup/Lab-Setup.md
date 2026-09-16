## 🏗️ Network Diagram

![Network Diagram](setup/Setup.png)

## 🧠 Diagram Logic

The lab uses network segmentation to simulate a real enterprise environment. All traffic between networks is routed through pfSense.

### Network Segments

| Network | Subnet | Purpose | Connected Device |
| :--- | :--- | :--- | :--- |
| **WAN (em0)** | NAT (192.168.168.141) | Internet access | pfSense → Internet |
| **OPT1 (em1)** | 192.168.10.0/24 | Attacker network | Linux Mint |
| **LAN (em2)** | 192.168.20.0/24 | Victim network | Windows 10 |

### pfSense Interface Configuration

| Interface | IP Address | Role |
| :--- | :--- | :--- |
| **WAN (em0)** | 192.168.168.141 (NAT) | Internet gateway |
| **OPT1 (em1)** | 192.168.10.1/24 | Attacker network gateway |
| **LAN (em2)** | 192.168.20.1/24 | Victim network gateway |

### Host Details

| Host | Role | IP Address | Gateway | DNS |
| :--- | :--- | :--- | :--- | :--- |
| **Linux Mint** | Attacker | DHCP (e.g., 192.168.10.50) | 192.168.10.1 | 192.168.10.1 |
| **Windows 10** | Victim | 192.168.20.106 | 192.168.20.1 | 192.168.20.1 |

### How It Works

1. **Linux Mint (Attacker)** is on the OPT1 network and generates attack traffic.
2. **pfSense Firewall** routes traffic between OPT1, LAN, and the internet. It also forwards its own logs to Splunk Cloud.
3. **Windows 10 (Victim)** is on the LAN network. It runs Sysmon and Splunk Universal Forwarder, sending logs to Splunk Cloud.
4. **Splunk Cloud** collects and analyzes all logs via HTTPS (TCP 443) over the internet.
5. All internet-bound traffic from the lab passes through pfSense's WAN interface (NAT).
