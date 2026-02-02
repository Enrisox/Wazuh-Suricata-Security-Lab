# 🛡️ Wazuh-Suricata-Security-Lab
### Threat Detection & Endpoint Monitoring

## 📖 Introduction
This repository documents my hands-on experience with **Wazuh**, an enterprise-grade, open-source security monitoring platform. As a Cybersecurity student, my goal is to master the integration of SIEM and XDR capabilities to protect corporate networks.

In this lab, I simulate real-world attack scenarios to analyze how telemetry is gathered and transformed into actionable alerts. 

> [!IMPORTANT]
> **Ethical Note:** To promote responsible security practices, I have chosen not to publish the specific exploit commands used during the "attack phase." Instead, this documentation focuses on **detection patterns, log analysis, and alert refinement.**

## 🛠️ Lab Architecture & Hardware
To ensure a high-performance environment capable of handling real-time indexing and traffic analysis, I deployed the following stack:

* **Host Machine:** High-performance workstation (AMD Ryzen 9 7900, 12 Cores, 32GB DDR5 RAM).
* **Hypervisor:** Oracle VirtualBox.
* **Networking:** * **MikroTik HAP AC Lite:** Used for physical/virtual network segmentation.
    * **Bridge Mode:** All VMs are configured in bridge mode to simulate a realistic local network topology.

## 🖥️ Deployment Stack
The lab consists of three main components:
1.  **Wazuh Manager (OVA):** The central brain for log analysis and dashboarding.
2.  **Kali Linux:** Used as the controlled "Attacker" node to generate security events.
3.  **Ubuntu Server (Endpoint):** The "Target" node, monitored via the Wazuh Agent and integrated with Suricata for IDS/IPS.

## 🎯 Project Objectives
* **Mastering the Learning Curve:** Transitioning from basic monitoring to advanced rule tuning.
* **Log Integration:** Collecting events from Syslog, Suricata, and OSSEC agents.
* **Alert Engineering:** Analyzing the "Security Events" dashboard to filter noise and focus on high-severity threats (MITRE ATT&CK mapping).
