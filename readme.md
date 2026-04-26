# 🛡️ Home SOC Lab — Threat Detection & Incident Response

A hands-on Security Operations Center (SOC) home lab built 
to simulate real-world cyberattacks and practice L1 SOC 
analyst skills including alert triage, log analysis, 
MITRE ATT&CK mapping, and incident response.

---

## 🏗️ Lab Architecture

| Component        | Role                    
|-----------------|-------------------------|
| Ubuntu Server   | Wazuh SIEM Manager      | 
| Windows 10 VM   | Target / Wazuh Agent    | 
| Kali Linux      | Attacker Machine        | 

---

## ⚔️ Attacks Simulated

### 🦠 Malware Simulation
- EICAR test file deployment via HTTP server
- LOLBin technique using certutil for file download
- Windows Defender detection and quarantine analysis
- Real-time FIM (File Integrity Monitoring) alerts

### 💻 Windows Attack Scenarios
- Suspicious PowerShell execution
  - Base64 encoded commands (T1027)
  - IEX download cradle / fileless execution (T1059.001)
  - Defender disable attempt (T1562.001)
- Privilege escalation reconnaissance
  - Scheduled task enumeration (T1053)
  - Service path discovery (T1082)
  - Local account enumeration (T1087)
- System & Network reconnaissance
  - whoami /all, net user, netstat
  - wmic service enumeration
  - Registry query analysis

---

## 🔍 SOC L1 Analysis Performed

- Alert triage and severity classification
-  MITRE ATT&CK technique mapping
-  Attack timeline reconstruction
-  IOC (Indicator of Compromise) documentation
-  Wazuh rule analysis (Rule IDs: 92201, 92021, 60107, 60104)
-  Incident report writing
-  Log correlation across multiple events
-  Windows Event ID analysis (4688, 4625, 4672, 5001)

---

## 🗺️ MITRE ATT&CK Coverage

| Tactic             | Technique ID  | Description                    |
|--------------------|--------------|--------------------------------|
| Execution          | T1059.001    | PowerShell                     |
| Execution          | T1059.003    | CMD / certutil                 |
| Defense Evasion    | T1027        | Obfuscated/Encoded Commands    |
| Defense Evasion    | T1562.001    | Disable Windows Defender       |
| Defense Evasion    | T1070.004    | File Deletion                  |
| Defense Evasion    | T1105        | Ingress Tool Transfer          |
| Discovery          | T1082        | System Information Discovery   |
| Discovery          | T1087        | Account Discovery              |
| Discovery          | T1049        | Network Connection Discovery   |
| Discovery          | T1069        | Permission Group Discovery     |
| Discovery          | T1053        | Scheduled Task Enumeration     |

---

## 🛠️ Tools & Technologies

- **SIEM:** Wazuh 4.x (OpenSearch backend)
- **Attacker:** Kali Linux (certutil, smbclient, python3 HTTP)
- **Target:** Windows 10 with Wazuh Agent + Sysmon
- **Monitoring:** Windows Event Logs, Sysmon, FIM, Rootcheck
- **Visualization:** Wazuh Threat Hunting, MITRE ATT&CK map
- **Hypervisor:** VMware Workstation

---


## 📁 Repository Structure

\`\`\`


home-soc-lab/
│
├── 📂 configs/
│   ├── ossec.conf              # Wazuh Windows agent config
│   └── wazuh-manager.conf      # Wazuh server config
│
├── 📂 attack-simulations/
│   ├── malware-simulation.md   # EICAR attack walkthrough
│   ├── powershell-attacks.md   # PS attack commands + analysis
│   └── privilege-escalation.md # PrivEsc recon documentation
│
├── 📂 incident-reports/
│   ├── IR-001-EICAR-Malware.md      # Malware incident report
│   ├── IR-002-PowerShell-Attack.md  # PS attack report
│   └── IR-003-Recon-Activity.md     # Reconnaissance report
│
├── 📂 wazuh-analysis/
│   ├── alert-screenshots/      # Wazuh dashboard screenshots
│   ├── rule-analysis.md        # Rule ID documentation
│   └── mitre-mapping.md        # ATT&CK technique mapping
│
├── 📂 ioc-collection/
│   └── iocs.md                 # All IOCs from simulations
│
└── README.md
\`\`\`

---


##  Key Wazuh Alerts Detected

| Rule ID | Level | Description                              |
|---------|-------|------------------------------------------|
| 92201   | 9 🔴  | PowerShell created new scripting engine  |
| 92021   | 3 🟡  | PowerShell used to delete files          |
| 60107   | 4 🟡  | Failed privileged operation attempt      |
| 60104   | 5 🟠  | Windows audit failure event              |
| 67027   | 3 🟢  | New process created                      |
| 61109   | 5 🟠  | WPAD name resolution timeout             |
| 92154   | 4 🟡  | taskschd.dll loaded (persistence risk)   |

---

##  Skills Demonstrated

\`\`\`
Blue Team
  ├── SIEM configuration and tuning (Wazuh)
  ├── Alert triage and investigation
  ├── Log analysis (Windows Event Logs + Sysmon)
  ├── Incident response documentation
  ├── IOC identification and collection
  └── MITRE ATT&CK framework mapping

Red Team (Attack Simulation)
  ├── Malware delivery via HTTP server
  ├── LOLBin abuse (certutil, PowerShell)
  ├── Defense evasion techniques
  ├── System and network reconnaissance
  └── Fileless attack simulation (IEX cradle)
\`\`\`

---

##  What I Learned

- How attackers use built-in Windows tools (LOLBins) 
  to evade detection
- How SIEM rules correlate multiple events into 
  meaningful alerts
- The importance of behavioral detection over 
  signature-based detection
- How to reconstruct an attack timeline from logs
- Real SOC L1 analyst workflow from alert to 
  escalation

---

## ⚠️ Disclaimer

> This lab and all attack simulations were performed 
> in an isolated virtual environment for educational 
> purposes only. All techniques documented here are 
> for defensive security learning. Never use these 
> techniques on systems you do not own or have 
> explicit written permission to test.

---

## 👩‍💻 Author

**Malaika**  
Aspiring SOC Analyst | Blue Team Enthusiast  

*Built as part of self-directed cybersecurity 
training toward SOC L1 certification*
