# 🛡️ Home SOC Lab — Security Operations Center Deployment

> A hands-on, self-hosted Security Operations Center (SOC) lab built for learning real-world threat detection, log analysis, and incident response. This repository documents the full deployment process — from infrastructure setup to live alerting.

---

## 📌 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Current Deployments](#current-deployments)
- [Tools & Technologies](#tools--technologies)
- [Getting Started](#getting-started)
- [Repository Structure](#repository-structure)
- [Roadmap](#roadmap)
- [Author](#author)

---

## Overview

This repository serves as the complete documentation hub for my **Home SOC Lab** — a virtualized security monitoring environment designed to simulate enterprise-grade threat detection using open-source tools.

The lab covers:
- **Endpoint monitoring** via Sysmon on Windows
- **Centralized SIEM** via Wazuh (Manager + Agents)
- **File Integrity Monitoring (FIM)** for real-time file change detection
- **Vulnerability Detection** using Wazuh's built-in scanner
- **MITRE ATT&CK** mapping of triggered alerts
- **Custom alerting** with webhook-based notifications
- **Threat Intelligence** integration with VirusTotal

> 🚧 This repository is actively growing. Future deployments including **OpenCTI**, **TheHive**, **Cortex**, and more will be added as the lab expands.

---

## Architecture


<img width="800" height="533" alt="image" src="https://github.com/user-attachments/assets/8a444e1a-d130-4bd8-89c4-a4ddfd27c53d" />


---

## Current Deployments

### ✅ 1. Sysmon — Windows Endpoint Monitoring
**File:** [`Sysmon.pdf`](./Sysmon.pdf)

Microsoft Sysinternals Sysmon installed on the Windows 10 client for deep endpoint telemetry.

**What it captures:**
- Process creation (Event ID 1)
- Network connections
- File creation/modification
- Registry activity

**Key steps covered:**
- Download & install Sysmon with SwiftOnSecurity config
- Verify logging in Windows Event Viewer
- Forward Sysmon logs to Wazuh via `ossec.conf` localfile block
- SOC-level test using `notepad.exe` process creation

---

### ✅ 2. Wazuh Agent — Windows Installation & Registration
**File:** [`Wazu_Agent_installation_at_windows.pdf`](./Wazu_Agent_installation_at_windows.pdf)

Wazuh agent (v4.14.4) deployed on Windows 10, registered and connected to the Ubuntu Wazuh Manager.

**Key steps covered:**
- Download Windows `.msi` installer
- Add agent on server via `manage_agents` and extract authentication key
- Import key into Windows agent GUI
- Start agent service and verify connectivity
- Multiple verification methods: CLI, real-time logs, and dashboard GUI

---

### ✅ 3. Wazuh Manager & Agent Configurations
**File:** [`Wazu_Manager_and_Wazu_agent_Configurations_.pdf`](./Wazu_Manager_and_Wazu_agent_Configurations_.pdf)

Advanced configuration of both the Wazuh Manager (Ubuntu) and the Windows agent to enable missing security modules.

**Modules enabled & configured:**

| Module | Description |
|---|---|
| **File Integrity Monitoring (FIM)** | Real-time monitoring of Downloads, Desktop, Temp folders. Triggers Rules 550/553/554 |
| **Vulnerability Detection** | Enabled on Wazuh Manager; scans agents for known CVEs |
| **Alert Monitor** | Custom `High-Severity-Attack-Alert` monitor with webhook channel |
| **VirusTotal Integration** | Syscheck events forwarded to VirusTotal for hash reputation |
| **MITRE ATT&CK Mapping** | Alerts mapped to ATT&CK techniques (e.g., T1565 Stored Data Manipulation) |

---

### ✅ 4. Wazuh Server Installation
**File:** [`Wazuh Server Installation.txt`](./Wazuh%20Server%20Installation.txt)

Base installation of the Wazuh server stack on Ubuntu.

---

## Tools & Technologies

| Tool | Role | Platform |
|---|---|---|
| **Wazuh** | SIEM / XDR / Log Analysis | Ubuntu Server |
| **Sysmon** | Endpoint Telemetry | Windows 10 |
| **OpenSearch / Kibana** | Dashboard & Search | Ubuntu Server |
| **VirusTotal API** | Threat Intelligence | Integration |
| **Webhook.site** | Alert Testing | External |
| **VMware Workstation** | Virtualization | Host |

---

## Getting Started

> Prerequisites: VMware (or VirtualBox), Ubuntu 22.04 ISO, Windows 10 ISO

### Recommended Deployment Order

```
1. Deploy Ubuntu VM → Install Wazuh Server
2. Deploy Windows 10 VM → Install Sysmon
3. Install & Register Wazuh Agent on Windows
4. Configure ossec.conf (FIM, Sysmon logs, Syscheck)
5. Enable Vulnerability Detection on Manager
6. Set up Alert Monitors & Webhook Channels
7. Integrate VirusTotal
8. Validate: Run FIM tests, check Wazuh Dashboard
```

Each step has a dedicated PDF guide in this repository with screenshots and commands.

---

## Repository Structure

```
home-soc-lab/
│
├── README.md                                  
├── Wazuh Server Installation.txt              ← Wazuh server setup
├── Wazu_Agent_installation_at_windows.pdf     ← Agent deployment guide
├── Wazu_Manager_and_Wazu_agent_Configurations_.pdf  ← Config & module setup
├── Sysmon.pdf                                 ← Sysmon install & Wazuh integration
│
└──
```

---

## Roadmap

- [x] Wazuh Server Installation
- [x] Wazuh Agent on Windows
- [x] Sysmon Integration
- [x] File Integrity Monitoring (FIM)
- [x] Vulnerability Detection
- [x] Custom Alert Monitors
- [x] VirusTotal Integration
- [x] MITRE ATT&CK Mapping
- [ ] **OpenCTI** — Threat Intelligence Platform
- [ ] **TheHive** — Incident Response Platform
- [ ] **Cortex** — Automated Analysis
- [ ] **Shuffle** — SOAR Automation
- [ ] **Suricata** — Network IDS/IPS
- [ ] **Zeek** — Network Traffic Analysis
- [ ] **Kali Linux** — Attack Simulation VM
- [ ] **DVWA** — Vulnerable Web App for testing

---

## Author

**Malaika Umbreen**
Home SOC Lab | Cybersecurity Analyst

---

> ⭐ If this lab documentation helps you build your own SOC, consider starring the repo!
> 
> 📬 Contributions, suggestions, and PRs are welcome as this lab grows.
