# Wazuh-Suricata-Security-Lab
I’m Enrico, a Cybersecurity student.
In this lab environment I deploy and experiment with Wazuh and its main integrations — including Suricata and VirusTotal — to monitor, detect, and protect endpoints and small enterprise networks

---

# 📚 Documentation Index

All detailed documentation is inside the `/docs` folder.

## **1️⃣ Introduction**
➡️ [01_intro.md](docs/01_intro.md)

## **2️⃣ Lab Infrastructure**
➡️ [02_lab_infrastructure.md](docs/02_lab_setup.md)

## **3️⃣ Wazuh Installation & Configuration**
➡️ [03_wazuh_installation.md](docs/03_wazuh_installation.md)

## **4️⃣ Suricata Setup**
➡️ [04_suricata_setup.md](docs/04_suricata_setup.md)

## **5️⃣ VirusTotal Integration**
➡️ *coming soon*  

## **6️⃣ Wazuh Agent Troubleshooting**
➡️ [06_wazuh_agent_troubleshooting.md](docs/06_wazuh_agent_troubleshooting.md)

## **7️⃣ Detection Tests (Wazuh + Suricata + VirusTotal)**
➡️ [07_detection_tests.md](docs/07_detection_tests.md)



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
| **MikroTik Router** | DHCP, routing |

---

## Contact

If you want to discuss the lab or improvements:

**Enrico Soci – Cybersecurity and DevSecOps Student**  
enricosoci@protonmail.com

---

