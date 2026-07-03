# ransomware-simulation-and-defense-lab
This repository provides an automated SOAR framework to neutralize ransomware at machine speed. By replacing manual SOC triage with autonomous remediation, this project resolves high MTTR issues. It detects LotL threats better than static SIEM monitoring, ensuring instant, closed-loop defense.

# 🛡️ Ransomware Simulation and Defense Lab

> A virtualized cybersecurity laboratory that simulates a real-world ransomware attack and demonstrates an automated incident response pipeline using **Snort IDS** and **SOAR** techniques.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Ubuntu%20%7C%20Kali-success)
![VirtualBox](https://img.shields.io/badge/Virtualization-VirtualBox-orange)
![Snort](https://img.shields.io/badge/IDS-Snort%203-red)
![SOAR](https://img.shields.io/badge/SOAR-Automated%20Response-purple)
![License](https://img.shields.io/badge/License-Educational-yellow)

---

# 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Problem Statement](#-problem-statement)
- [Objectives](#-objectives)
- [Key Features](#-key-features)
- [Technology Stack](#-technology-stack)
- [System Architecture](#-system-architecture)
- [Architecture Components](#-architecture-components)
- [Project Workflow](#-project-workflow)
- [Installation](#-installation)
- [Project Structure](#-project-structure)
- [Results](#-results)
- [Future Scope](#-future-scope)
- [License](#-license)

---

# 📌 Project Overview

Ransomware has become one of the most destructive cyber threats affecting organizations, governments, hospitals, educational institutions, and businesses worldwide. Traditional incident response often depends on human intervention, which increases the time required to detect, investigate, and recover from an attack.

The **Ransomware Simulation and Defense Lab** was developed to demonstrate how ransomware attacks can be detected and automatically remediated inside a completely isolated virtual environment.

Instead of deploying real malware, this project uses a **safe educational ransomware simulation** that encrypts only predefined sample files inside a controlled directory. Once encryption is completed, the simulated malware sends a network beacon to a monitoring server.

The defense infrastructure continuously monitors network traffic using **Snort Intrusion Detection System (IDS)**. When the predefined ransomware signature is detected, a custom **SOAR (Security Orchestration, Automation and Response)** engine automatically launches an incident response playbook that remotely executes a recovery script on the infected machine.

The complete attack, detection, response, and recovery cycle happens automatically without manual intervention, demonstrating how modern Security Operations Centers (SOCs) automate ransomware response.

The entire environment is isolated inside **Oracle VM VirtualBox**, ensuring that no malicious activity can escape to the host computer or public networks.

---

# ❗ Problem Statement

Modern ransomware attacks encrypt valuable data within seconds, causing:

- Data loss
- Business downtime
- Financial damage
- Operational disruption
- Delayed incident response
- Human dependency during recovery

Most organizations rely on manual security operations where analysts must:

1. Detect the attack
2. Verify the alert
3. Investigate logs
4. Identify affected systems
5. Execute remediation manually

This process increases the **Mean Time To Respond (MTTR)** and allows ransomware to cause greater damage.

This project demonstrates how detection and response can be fully automated using an IDS and SOAR pipeline.

---

# 🎯 Objectives

The primary objectives of this project are:

- Simulate a ransomware attack inside an isolated virtual lab.
- Demonstrate safe file encryption using Python.
- Detect ransomware behavior using Snort IDS.
- Generate real-time security alerts.
- Automate incident response using a custom SOAR engine.
- Restore encrypted files automatically.
- Reduce human intervention during ransomware recovery.
- Demonstrate cross-platform orchestration between Linux and Windows.
- Understand enterprise SOC workflows.
- Learn practical offensive and defensive cybersecurity techniques.

---

# ⭐ Key Features

## Offensive Security

- Safe ransomware simulation
- Recursive file encryption
- Fernet (AES-128) encryption
- Automatic file renaming
- Command & Control (C2) beacon generation
- Remote payload execution using SSH
- Hidden payload deployment

---

## Defensive Security

- Real-time Snort IDS monitoring
- Signature-based ransomware detection
- Automated alert generation
- Continuous log monitoring
- SOAR automation pipeline
- Automatic incident response
- Remote PowerShell execution
- Automatic file recovery

---

## Infrastructure

- Fully virtualized environment
- Host-Only isolated network
- Three-machine cybersecurity lab
- Cross-platform communication
- Secure SSH-based orchestration
- Modular architecture
- Easily extendable design

---

# 🛠️ Technology Stack

## Programming Languages

| Technology | Purpose |
|------------|----------|
| Python 3 | Ransomware simulation, automation, recovery |
| PowerShell | Remote remediation on Windows |
| Bash | Linux automation |

---

## Operating Systems

| Operating System | Role |
|------------------|------|
| Kali Linux | Attacker Machine |
| Windows 10 | Victim Machine |
| Ubuntu Server | SOC / Defense Machine |

---

## Security Tools

| Tool | Purpose |
|------|----------|
| Snort 3 | Intrusion Detection System |
| OpenSSH | Secure remote access |
| sshpass | Password-based SSH automation |
| Netcat | Network testing |
| Cryptography Library | File encryption & decryption |

---

## Virtualization

- Oracle VM VirtualBox
- Host-Only Networking
- Virtual Machine Isolation

---

## Networking

- TCP/IP
- SSH
- SCP
- TCP Socket Programming
- Port 22 (SSH)
- Port 80 (Beacon Communication)

---

## Security Concepts

- Ransomware Simulation
- AES Encryption
- Fernet Encryption
- Signature-Based Detection
- Intrusion Detection System (IDS)
- Security Orchestration Automation and Response (SOAR)
- Command and Control (C2)
- Incident Response
- Cross-Platform Automation

---

# 🏗️ System Architecture

The project follows a **three-node isolated cybersecurity architecture** where each virtual machine performs a dedicated role within the attack and defense lifecycle. The entire lab is deployed using **Oracle VM VirtualBox** with a **Host-Only Network**, ensuring that all ransomware activity remains confined to a safe environment. :contentReference[oaicite:0]{index=0}

```text
                    ┌──────────────────────────────┐
                    │      Kali Linux VM           │
                    │     (Attacker Node)          │
                    └──────────────┬───────────────┘
                                   │
                     SSH / SCP (Port 22)
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │      Windows 10 VM           │
                    │      (Target Machine)        │
                    │                              │
                    │ • attack.py                  │
                    │ • decrypt.py                 │
                    │ • Sample Files               │
                    └──────────────┬───────────────┘
                                   │
                     TCP Beacon (Port 80)
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │      Ubuntu Server VM        │
                    │   (Watchtower / SOC Node)    │
                    │                              │
                    │  Snort IDS                   │
                    │  SOAR Daemon                 │
                    │  SSH Automation              │
                    └──────────────┬───────────────┘
                                   │
                      Remote PowerShell via SSH
                                   │
                                   ▼
                    Automatically Executes
                         decrypt.py
                    Restores Encrypted Files
```

---

# 🖥️ Architecture Components

## 🐉 1. Kali Linux (Attacker Node)

The Kali Linux virtual machine simulates a threat actor or Command-and-Control (C2) server. It stages the attack by securely transferring the ransomware payload (`attack.py` and `decrypt.py`) to the Windows machine using SSH/SCP over Port 22, then remotely triggers the attack. :contentReference[oaicite:1]{index=1}

**Responsibilities**
- Simulate attacker behavior
- Deploy payloads
- Execute ransomware remotely
- Manage secure communication

---

## 🪟 2. Windows 10 (Target Node)

The Windows virtual machine represents a victim endpoint. It contains a dedicated folder with harmless sample files that are encrypted during the simulation. After encryption, the ransomware sends a predefined TCP beacon to the defense server, mimicking attacker telemetry. :contentReference[oaicite:2]{index=2}

**Responsibilities**
- Execute ransomware simulation
- Encrypt sample files
- Send C2 beacon
- Execute recovery script when instructed

---

## 🐧 3. Ubuntu Server (Watchtower / SOC)

The Ubuntu Server acts as the Security Operations Center (SOC). It continuously monitors network traffic with Snort IDS and runs a custom Python SOAR daemon that watches Snort alerts. When the ransomware signature is detected, it automatically connects back to the Windows machine and launches the recovery process. :contentReference[oaicite:3]{index=3}

**Responsibilities**
- Monitor network traffic
- Detect ransomware beacon
- Generate alerts
- Trigger automated incident response
- Restore encrypted files

---

# 🔒 Why an Isolated Virtual Environment?

The entire project runs inside a **Host-Only VirtualBox network**, meaning the attacker, victim, and defense machines can communicate only with each other. This prevents the simulated ransomware from reaching the host operating system or external networks, making the lab safe for learning, experimentation, and demonstrations. :contentReference[oaicite:4]{index=4}

---

# 🚀 Project Workflow

This project demonstrates a **complete ransomware attack lifecycle** along with an **automated defense mechanism** inside a secure virtual lab. Unlike traditional demonstrations that stop after file encryption, this project implements a **closed-loop detection and response pipeline**, where the attack is automatically detected, analyzed, and remediated without requiring manual intervention.

The workflow closely resembles how modern **Security Operations Centers (SOCs)** detect and respond to ransomware incidents in enterprise environments.

The complete process consists of three major phases:

- **Attack Phase** – Simulating a ransomware attack on the target machine.
- **Detection Phase** – Identifying the ransomware activity using Snort IDS.
- **Response & Recovery Phase** – Automatically restoring encrypted files using a custom SOAR engine.

---

# 🔄 Complete Attack-to-Defense Workflow

```text
Initialize Virtual Lab
        │
        ▼
Start Ubuntu Watchtower
        │
        ▼
Launch Snort IDS
        │
        ▼
Start SOAR Daemon
        │
        ▼
Transfer Payload to Windows
        │
        ▼
Execute attack.py
        │
        ▼
Encrypt Target Files
        │
        ▼
Send TCP Beacon
        │
        ▼
Snort Detects Signature
        │
        ▼
Generate Security Alert
        │
        ▼
SOAR Parses Alert
        │
        ▼
SSH into Windows
        │
        ▼
Execute decrypt.py
        │
        ▼
Restore Files
        │
        ▼
Incident Successfully Resolved
```

---

# ⚔️ Phase 1 – Attack Simulation

The attack phase simulates how ransomware typically compromises a victim's system. Instead of using real malware, this project uses a custom-built Python script (`attack.py`) that safely encrypts only predefined files inside a controlled directory.

The attack is executed inside an isolated virtual environment, ensuring there is **zero risk to the host operating system or external networks**.

---

## Step 1 – Preparing the Virtual Lab

Three virtual machines are created using Oracle VM VirtualBox.

| Virtual Machine | Role |
|-----------------|------|
| Kali Linux | Attacker |
| Windows 10 | Victim |
| Ubuntu Server | Security Operations Center (SOC) |

All machines communicate through a **Host-Only Virtual Network**, preventing any malicious traffic from escaping the laboratory.

---

## Step 2 – Payload Deployment

The attacker machine securely transfers the ransomware payload to the Windows target using **SSH/SCP**.

Transferred files include:

- `attack.py`
- `decrypt.py`

The payload is stored inside a hidden directory to simulate how real attackers attempt to conceal malicious files.

---

## Step 3 – Payload Execution

After deployment, the attacker remotely executes the ransomware script.

The Python ransomware immediately begins its operation by:

- Searching the target directory
- Locating supported files
- Reading file contents
- Encrypting data
- Renaming encrypted files
- Generating an encryption key

Unlike real ransomware, this simulation only affects predefined sample files inside the lab.

---

## Step 4 – File Encryption

The ransomware encrypts every eligible file using the **Fernet cryptography library**, which internally uses **AES-128 symmetric encryption**.

For every file:

1. Read original data
2. Encrypt contents
3. Create encrypted version
4. Rename file
5. Remove original copy

Example:

```
Report.pdf
↓

Report.pdf.locked
```

At this stage, the victim can no longer access the original files.

---

## Step 5 – Command & Control (C2) Beacon

Immediately after encryption, the ransomware sends a predefined TCP message to the Ubuntu defense server.

Example Beacon:

```
This file contains danger ransomware code.
```

This beacon simulates how real ransomware communicates with its Command-and-Control (C2) server after successfully compromising a victim.

---

# 🛡️ Phase 2 – Threat Detection

The Ubuntu server continuously monitors incoming network traffic using **Snort 3 Intrusion Detection System (IDS)**.

Unlike antivirus software that scans files, Snort analyzes **network packets** in real time.

---

## Step 6 – Packet Inspection

Every packet entering the network interface is inspected.

Snort examines:

- Source IP
- Destination IP
- Protocol
- Port Number
- Payload Content

---

## Step 7 – Signature Matching

A custom Snort rule searches for the exact ransomware beacon.

Example:

```snort
content:"This file contains danger ransomware code";
```

When this string is found inside a TCP packet, Snort immediately classifies it as a ransomware event.

---

## Step 8 – Alert Generation

Once detected, Snort writes a high-priority alert to:

```
/var/log/snort/alert_fast.txt
```

This alert contains information such as:

- Timestamp
- Rule ID
- Source IP
- Destination IP
- Alert Message

This log becomes the trigger for the automated defense system.

---

# 🤖 Phase 3 – Automated Response (SOAR)

Instead of waiting for a human analyst, the custom SOAR daemon immediately reacts to the Snort alert.

The SOAR engine continuously monitors the Snort alert log for newly generated ransomware events.

---

## Step 9 – Log Monitoring

The Python SOAR daemon watches:

```
/var/log/snort/alert_fast.txt
```

Whenever a new alert appears:

- Parse the alert
- Verify Rule ID
- Extract attacker information
- Start remediation

---

## Step 10 – Automatic SSH Connection

After verifying the attack, the Ubuntu server automatically establishes an SSH connection with the Windows victim.

This removes the need for:

- Manual login
- Remote Desktop
- Human interaction

The entire process happens automatically.

---

## Step 11 – Remote PowerShell Execution

The SOAR daemon generates a PowerShell command and executes it remotely on Windows.

The command searches for:

```
decrypt.py
```

Once located, it automatically runs the recovery script.

---

## Step 12 – File Recovery

The recovery script:

- Finds encrypted files
- Loads the encryption key
- Decrypts file contents
- Restores original filenames
- Deletes encrypted copies

Example:

```
Report.pdf.locked

↓

Report.pdf
```

Within seconds, every encrypted file is restored.

---

# ✅ Final Outcome

The entire ransomware lifecycle is completed automatically.

| Stage | Status |
|---------|--------|
| Payload Delivered | ✅ |
| Files Encrypted | ✅ |
| Beacon Sent | ✅ |
| Snort Detection | ✅ |
| Alert Generated | ✅ |
| SOAR Triggered | ✅ |
| SSH Connected | ✅ |
| PowerShell Executed | ✅ |
| Files Restored | ✅ |

The project demonstrates how modern SOC environments combine **Intrusion Detection Systems (IDS)** with **Security Orchestration, Automation, and Response (SOAR)** platforms to minimize incident response time and automate ransomware recovery.

---

---

# 📄 Core Files Explained

| File | Description |
|------|-------------|
| **attack.py** | Simulates ransomware by encrypting files and sending a TCP beacon. |
| **decrypt.py** | Restores encrypted files using the stored encryption key. |
| **soar_daemon.py** | Monitors Snort alerts and automatically launches the recovery process. |
| **local.rules** | Contains the custom Snort rule used to detect the ransomware beacon. |
| **snort.lua** | Configures the Snort 3 IDS engine. |
| **requirements.txt** | Lists the required Python packages for the project. |

---

# ⚙️ Installation & Setup Guide

This section explains how to recreate the complete **Ransomware Simulation and Defense Lab** from scratch. The lab consists of three virtual machines connected through an isolated Host-Only network, ensuring that the ransomware simulation remains completely contained and safe.


# 📋 Prerequisites

Before starting, ensure you have the following:

| Requirement | Version |
|-------------|----------|
| Oracle VM VirtualBox | Latest |
| Kali Linux | Latest |
| Ubuntu Server | 22.04 LTS (or compatible) |
| Windows 10 | 64-bit |
| Python | 3.x |
| Snort | Version 3 |
| OpenSSH | Enabled on Windows |
| Git | Latest |

---

# 💻 Hardware Requirements

| Component | Minimum |
|-----------|---------|
| CPU | Dual Core (Quad Core Recommended) |
| RAM | 8 GB (16 GB Recommended) |
| Storage | 40 GB Free |
| Virtualization | Intel VT-x / AMD-V Enabled |

---

# 🖥️ Virtual Machine Configuration

Create the following virtual machines inside Oracle VM VirtualBox.

| Virtual Machine | Operating System | Purpose |
|----------------|------------------|----------|
| Kali Linux | Linux | Attacker Machine |
| Ubuntu Server | Linux | Detection & SOAR |
| Windows 10 | Windows | Victim Machine |

---

# 🌐 Network Configuration

Configure all three VMs to use the **Host-Only Adapter**.

This provides:

- Isolated communication
- No Internet exposure
- Safe malware execution
- Internal packet monitoring

Example IP configuration:

| Machine | IP Address |
|----------|------------|
| Kali Linux | `192.168.1.50` |
| Ubuntu Server | `192.168.1.85` |
| Windows 10 | `192.168.1.60` |

> Replace these addresses with your own if your environment differs.

---


---

# 🐍 Install Python Dependencies

Install all required Python packages.

```bash
pip install -r requirements.txt
```

or install manually

```bash
pip install cryptography
```

---

# 🛡️ Install Snort 3 (Ubuntu)

Install Snort following the official documentation or your preferred installation method.

Verify installation:

```bash
snort -V
```

Expected output:

```text
Snort Version 3.x.x
```

---

# 📄 Configure Snort

Copy the custom detection rule into the Snort rules directory.

```
local.rules
```

Configure Snort to load the rule.

Example rule:

```snort
alert tcp any any -> any 80 (
msg:"RANSOMWARE PAYLOAD DETECTED";
content:"This file contains danger ransomware code";
sid:1000001;
rev:1;
)
```

---

# 🔐 Enable OpenSSH on Windows

Open:

```
Settings
→ Apps
→ Optional Features
→ Add Feature
```

Install:

- OpenSSH Server

Start the service:

```powershell
Start-Service sshd
```

Enable automatic startup:

```powershell
Set-Service -Name sshd -StartupType Automatic
```

Verify:

```powershell
Get-Service sshd
```

---

# 📂 Prepare the Target Directory

Create the directory that will contain the sample files.

```text
C:\RansomwareLab
```

Copy a few harmless files into the folder for testing, such as:

```text
example.pdf
report.pdf
notes.txt
image.jpg
presentation.pptx
```

These files will be encrypted and later restored during the simulation.

---

# 📤 Transfer Project Files

Copy the project files from the Kali Linux machine to the Windows target using SCP.

Example:

```bash
scp attack.py Lab@192.168.1.60:C:/RansomwareLab/

scp decrypt.py Lab@192.168.1.60:C:/RansomwareLab/
```

---


---

# 📂 Important Files

## attack.py

Responsible for:

- Searching target files
- Encrypting files
- Renaming files
- Sending ransomware beacon

---

## decrypt.py

Responsible for:

- Locating encrypted files
- Decrypting file contents
- Restoring original filenames

---

## soar_daemon.py

Responsible for:

- Monitoring Snort alerts
- Detecting ransomware events
- Executing automated incident response
- Launching remote recovery

---

## local.rules

Contains the custom Snort detection signature used to identify the ransomware beacon.

---

## snort.lua

Contains the Snort engine configuration.

---


# ✅ Setup Checklist

Before running the project, verify the following:

- [x] VirtualBox installed
- [x] Kali Linux VM created
- [x] Ubuntu Server VM created
- [x] Windows 10 VM created
- [x] Host-Only network configured
- [x] Python installed
- [x] Snort installed
- [x] OpenSSH enabled on Windows
- [x] Project cloned
- [x] Dependencies installed
- [x] Target directory created
- [x] Sample files added
- [x] Detection rules configured

