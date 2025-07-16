# 🛡️ Real-Time Nmap Scan Detection with Suricata + Wazuh  
> Advanced SOC Analyst Project | Threat Detection | Blue Team Hands-on

[![SOC Analyst Project](https://img.shields.io/badge/SOC%20Role-Learner-blue)](https://github.com/syedfaizan9920)
[![Detection with Wazuh](https://img.shields.io/badge/Detection-Wazuh-green)](https://documentation.wazuh.com/)
[![NIDS Engine](https://img.shields.io/badge/Tool-Suricata-orange)](https://suricata.io/)
[![Threat Simulated](https://img.shields.io/badge/Threat-NmapScan-critical)](https://nmap.org/)
[![Logs Format](https://img.shields.io/badge/Log-eve.json-lightgrey)]()

---

## 📌 Overview

This project demonstrates how to detect **Nmap network scans** in real time using:
- **Suricata** (as the Network Intrusion Detection System)
- **Wazuh** (as the SIEM and alert management platform)

The system logs suspicious activity, generates alerts, and enables defenders to respond to reconnaissance attempts — a critical phase of the cyber kill chain.

---

## 🧰 Tools & Technologies Used

| Tool        | Purpose                                |
|-------------|----------------------------------------|
| **Suricata**| Deep packet inspection & rule-based detection |
| **Emerging Threats Rules** | Community-driven detection rules |
| **Wazuh SIEM** | Log collection, parsing, and visualization |
| **Nmap**    | Simulating real-world reconnaissance   |
| **Ubuntu**  | Linux-based test environment           |

---

## 🚀 Implementation Steps

### 🔧 1. Install Suricata
```bash
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt-get update
sudo apt-get install suricata -y
```
---
cd /tmp
curl -LO https://rules.emergingthreats.net/open/suricata-6.0.8/emerging.rules.tar.gz
tar -xvzf emerging.rules.tar.gz
sudo mkdir -p /etc/suricata/rules
sudo mv rules/*.rules /etc/suricata/rules/
sudo chmod 640 /etc/suricata/rules/*.rules

---

⚙️ 3. Configure Suricata
Edit /etc/suricata/suricata.yaml:

HOME_NET: "[192.168.100.13]"
EXTERNAL_NET: "!$HOME_NET"

af-packet:
  - interface: enp0s3
---

Then restart Suricata:

sudo systemctl restart suricata
sudo systemctl enable suricata

---
🔗 4. Integrate with Wazuh
Edit Wazuh Agent config:
```
<localfile>
  <log_format>json</log_format>
  <location>/var/log/suricata/eve.json</location>
</localfile>
```
---
Restart:
sudo systemctl restart wazuh-agent

---
🧪 5. Simulate Attack
nmap -sS -T4 192.168.100.13
---
📊 6. Visualize Alerts
---
Go to Wazuh Dashboard > Security Events > NIDS

Look for alerts like:

ET SCAN Nmap Scripting Engine Detected

ET SCAN Potential SSH Scan

---
📈 Project Output
---
| Feature                 | Status       |
| ----------------------- | ------------ |
| Suricata detection      | ✅ Enabled    |
| Nmap scan alerting      | ✅ Working    |
| Log forwarding to Wazuh | ✅ Integrated |
| Real-time visibility    | ✅ Achieved   |

---
👨‍💻 About Me
---
Faizanullah Syed

SOC Analyst (In Training) | Cybersecurity Enthusiast

📍 https://unmaskcyber.com

📫 Email: faizanullah.syed19@gmail.com

🔗 LinkedIn | faizanullah-syed

---

📎 Tags
---
#SOCAnalyst #Suricata #Wazuh #Nmap #BlueTeam #CyberSecurityProjects #NetworkSecurity #ThreatDetection
