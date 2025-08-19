# 🛡️ Penetration Testing Lab - Step by Step

A detailed guide to setting up a safe and practical penetration testing lab.

---

## 1️⃣ Lab Requirements

### Hardware
- Minimum 8–16 GB RAM, 4+ cores CPU
- 100+ GB free disk space
- Virtualization support (VT-x/AMD-V)

### Software
- **Host OS:** Windows 10/11 or Linux
- **Virtualization:** VMware Workstation, VirtualBox, or Hyper-V
- **Guest OS (Target Machines):**
  - Kali Linux (Attacker) – preinstalled with tools
  - Metasploitable 2 / 3 (Vulnerable Linux) – target
  - Windows 10 / Windows Server (for AD testing)
  - DVWA (Damn Vulnerable Web App) – for web testing

### Network Setup
- Use an **isolated virtual network** (NAT/Host-only) to avoid affecting your real network.
- Assign static IPs:
  - Kali: `192.168.56.128`
  - Metasploitable 2: `192.168.56.130`
  - Windows: `192.168.56.132`

---

## 2️⃣ Lab Setup

### Step 1: Install Virtualization
1. Install **VMware Workstation** or **VirtualBox**.
2. Enable **Virtualization** in BIOS.
3. Create a **Host-Only Network** (isolated from Internet).

### Step 2: Setup Attacker Machine
- Install **Kali Linux VM**.
- Update & upgrade packages:
```bash
sudo apt update && sudo apt upgrade -y
