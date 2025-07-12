# 💻 My Cybersecurity Lab Project

## 🔗 Project Website  
Check out the live demo here: [Tyrone’s Cyber Lab](https://tyrone.studio)

---

This project documents the creation of my personal cybersecurity lab using **VirtualBox** and the **Wazuh** security monitoring platform. It covers:

- 🖥️ Virtual machine setup  
- 🌐 Network configuration  
- 💾 Disk expansion  
- 🛡️ Wazuh installation  
- 🛠️ Troubleshooting solutions  

---

## 🧠 Project Overview

In this lab, I set up **three virtual machines** and a **centralized monitoring system**:

- **Ubuntu VM** – Hosts the Wazuh Security Platform  
- **Kali Linux VM** – Loaded with penetration testing tools  
- **Windows 11 VM** – Simulates a monitored target system  
- **Wazuh** – A powerful, open-source SIEM and threat detection platform  

---

## 🧰 VirtualBox Environment

At the heart of the lab is **Oracle VM VirtualBox**, which allows me to run multiple isolated operating systems.

📷 *My VirtualBox Manager:*

![My VirtualBox Manager](https://github.com/user-attachments/assets/adb41d8d-326e-431c-a6af-18d348a49511)

- Ubuntu: 4GB RAM, 3 CPUs  
- All VMs connected to `lab-net` for internal communication  

---

## 🛠️ Phase 1: VM Setup

### 🐧 Ubuntu VM

Acts as the central server running **Wazuh**.

<img width="1883" height="1017" alt="ubuntu" src="https://github.com/user-attachments/assets/3b845064-76c1-43e6-91a6-8a05b9caa1f7" />



### 😈 Kali Linux VM  
Designed for ethical hacking and penetration testing.

<img width="1262" height="891" alt="Kalimachine" src="https://github.com/user-attachments/assets/560fd502-857d-45d8-b394-726c68eb18e7" />

### 🪟 Windows 11 VM
Represents a typical workstation monitored for security incidents.

<img width="1022" height="858" alt="windows11machine" src="https://github.com/user-attachments/assets/e56cc2b4-5bac-45b5-b3bf-a70aa3e8b260" />

---

## 🌐 Phase 2: Network Configuration

### Network Objectives:

Ubuntu needs both internet access and internal network access

Kali Linux and Windows 11 require internal lab access

- **Ubuntu Netplan Configuration**

  <img width="870" height="385" alt="ubuntu-network" src="https://github.com/user-attachments/assets/66e96253-1bc2-42d4-a466-c82e2c48ba86" />

- **Adapter 1 (enp0s3):** Configured with NAT (Network Address Translation) for internet access.

  <img width="1661" height="602" alt="ubuntu-enp0s3" src="https://github.com/user-attachments/assets/1e47635b-7591-4792-ac1c-59359164ca94" />
  
- **Adapter 2 (enp0s8):** Set up as an Internal Network called lab-net with a static IP address of 192.168.100.20.

  <img width="1035" height="572" alt="ubuntu-network2" src="https://github.com/user-attachments/assets/1d6666d8-0928-47e2-9777-ed8f9acba00a" />

- **Kali Linux VM:** Configured its network adapter (typically eth1 or similar) to be part of the Internal Network lab-net with a static IP address of 192.168.100.10
  
  <img width="1156" height="563" alt="Kali-networkdone" src="https://github.com/user-attachments/assets/a4f689dc-7f0f-4bae-8951-ceb60fe9c0a1" />

- **Windows 11 VM:** Configured its Ethernet adapter to be part of the Internal Network lab-net with a static IP address of 192.168.100.30.
- <img width="1022" height="858" alt="windows11machine" src="https://github.com/user-attachments/assets/c5586a81-e668-4738-94a3-ecc7f9cbde77" />

---

## 🛡️ Phase 4: Installing Wazuh
Used the official all‑in‑one installation script:

curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
sudo bash ./wazuh-install.sh -a
Installs:

Wazuh Manager

Wazuh Indexer

Filebeat

Wazuh Dashboard

- **🌐 Access: https://192.168.100.20**
- Username: admin
- Password: generated during install
  
  <img width="1912" height="1020" alt="wazuh-dash" src="https://github.com/user-attachments/assets/1ba88377-ad56-4ea0-8343-178eee3d9746" />

---

## 🔐 Phase 5: Securing Wazuh Dashboard
UI password change failed ("Resource 'admin' is reserved").

/usr/share/wazuh-indexer/bin/opensearch-cli securityadmin \
  --cluster-name opensearch-cluster \
  -cd /usr/share/wazuh-indexer/plugins/opensearch-security/securityconfig \
  -cn wazuh-admin \
  -p <NEW_PASSWORD> \
  -h 192.168.100.20


✅ Admin password successfully updated.


---

## ✨ Phase 6: Deploying Wazuh Agent
Installed the agent on Windows 11 VM via the Wazuh dashboard’s generated command.


| Agent Name          | Status   | IP Address     |
| ------------------- | -------- | -------------- |
| windows11-tyronelab | ✅ Active | 192.168.100.30 |



<img width="1901" height="737" alt="agent-dep1" src="https://github.com/user-attachments/assets/453a151d-54f7-498e-8ed3-dc7be2b6c7b1" />

---

## ✅ Conclusion
This lab demonstrates proficiency in:

🔧 VM provisioning & management

🌐 Network design & troubleshooting

💾 Disk management

🛡️ SIEM integration with Wazuh

🔍 Real‑time security monitoring

🧠 Author: Tyrone Joel

 


