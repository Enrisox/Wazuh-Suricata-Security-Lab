# Wazuh-Suricata-Security-Lab
My name is Enrico Soci and I am a second-year student at the ITS Academy Olivetti, enrolled in the course “**Information Systems Security & Integration Specialist – DevSecOps**” (**5 LEV ECQ**).
<br>
I am passionate about experimenting and building hands-on labs with the tools at my disposal.
In this lab environment I deploy and experiment with Wazuh and its main integrations — including Suricata and VirusTotal — to monitor, detect, and protect endpoints and small enterprise networks.

---

# Documentation Index

All detailed documentation is inside the `/docs` folder.

## Introduction
- [01_intro.md](docs/01_intro.md)

## Lab Infrastructure
- [02_lab_infrastructure.md](docs/02_lab_setup.md)

## Wazuh Installation & Configuration
- [03_wazuh_installation.md](docs/03_wazuh_installation.md)

## Suricata Setup
- [04_suricata_setup.md](docs/04_suricata_setup.md)

## VirusTotal Integration
- [05_VT.md](docs/05_virustotal_integration.md)

## Wazuh Agent Troubleshooting
- [06_wazuh_agent_troubleshooting.md](docs/06_wazuh_agent_troubleshooting.md)
## Detection Tests (Wazuh + Suricata + VirusTotal)
- [07_detection_tests.md](docs/07_detection_tests.md)



---

##

This lab demonstrates:

- Deployment of Wazuh Manager (OVA)
- Installation of Ubuntu, Kali, Fedora agents
- Suricata IDS on Linux endpoints
- VirusTotal API integration for malware reputation checks
- Detection of:
  - Malware (EICAR test)
  - Network attacks (testmyids.com)
  - Brute-force attempts (Hydra)
  - File integrity tampering
- Troubleshooting and agent management

---

## Tech stack

| Component | Purpose |
|----------|---------|
| **Wazuh Manager** | Log collection, SIEM, EDR |
| **Wazuh Agents** | Endpoint monitoring |
| **Suricata** | Network IDS |
| **VirusTotal API** | Malware reputation |
| **VirtualBox** | Lab virtualization |
| **Ubuntu / Kali / Fedora** | Test endpoints |
| **MikroTik Router(OPTIONAL)** | DHCP, routing |

---

## Contact

If you want to discuss the lab or improvements:

**Enrico Soci – Cybersecurity and DevSecOps Student**  
enricosoci@protonmail.com

---

