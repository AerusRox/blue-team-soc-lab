# Blue Team SOC Lab

A home lab simulating a Security Operations Center (SOC) using Splunk Cloud, pfSense, and Sysmon for attack detection and incident response.

## 📌 Introduction

This project is a hands-on Blue Team SOC lab built to develop practical skills in log detection, analysis, and incident response at an L1 (Tier 1) level. The lab simulates a real enterprise environment with network segmentation, endpoint telemetry, and a cloud-based SIEM.

The goal was to move beyond theory and gain real experience with the tools and workflows used by SOC analysts daily — collecting logs, writing detection queries, simulating attacks, and responding to incidents.

**What this lab covers:**
- Centralized log collection from Windows endpoints into Splunk Cloud
- Endpoint telemetry using Sysmon (process creation, network connections, DNS queries)
- Network segmentation and firewall rules using pfSense
- Attack simulation with Nmap (port scanning) and Hydra (RDP brute force)
- Custom Splunk detection queries mapped to MITRE ATT&CK
- SOC dashboards for real-time monitoring
- L1 incident response and prevention playbooks

**Skills demonstrated:**
- SIEM deployment and log onboarding (Splunk Cloud)
- Endpoint telemetry configuration (Sysmon)
- Firewall configuration and network segmentation (pfSense)
- Detection engineering (SPL queries, alerts)
- Incident response (triage, containment, documentation)
