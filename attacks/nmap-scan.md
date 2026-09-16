
# Nmap Port Scan

Simulation of a network reconnaissance scan using Nmap in an isolated lab environment.

> **⚠️ EDUCATIONAL PURPOSES ONLY**  
> This document is provided for educational and defensive security training only.  
> **Do not** use these techniques against any system you do not own or have explicit written permission to test.  
> Unauthorized network scanning is illegal and punishable by law.  
> All activities described here were performed in an isolated, offline lab environment.

## 📌 Overview

**Nmap** (Network Mapper) is a free and open‑source tool used for network discovery and security auditing. In this lab, Nmap is used to simulate a port scan against a Windows 10 victim machine to generate **Event ID 5156** (connection allowed) and **Event ID 5157** (connection blocked) logs.

This exercise helps Blue Team analysts understand:
- How port scans appear in Windows Firewall logs.
- How to detect them using Splunk.
- How to respond and prevent them.

**MITRE ATT&CK Mapping:**  
- **T1046** – Network Service Scanning  
- **T1595** – Active Scanning

## 🛠️ Attack Command

From the **Linux Mint attacker** machine, run:

```bash
sudo nmap -Pn -sS -sV 192.168.20.*
