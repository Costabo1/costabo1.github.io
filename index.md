---
layout: default
title: Costabo1 Portfolio
---

<style>
/* =========================
   CYBER DASHBOARD THEME
   ========================= */

body {
  background-color: #0b1220;
}

/* Profile image glow */
.profile-img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid #60a5fa;
  box-shadow: 0 0 15px #60a5fa, 0 4px 15px rgba(0,0,0,0.4);
  transition: 0.3s ease;
}

.profile-img:hover {
  box-shadow: 0 0 25px #60a5fa, 0 0 40px rgba(96,165,250,0.5);
  transform: scale(1.05);
}

/* Card layout */
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 16px;
  margin-top: 20px;
}

/* Cyber glow cards */
.card {
  background: #111827;
  border: 1px solid #2d3748;
  border-radius: 12px;
  padding: 16px;
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  box-shadow: 0 0 10px rgba(0,0,0,0.6);
}

/* Glow hover effect */
.card:hover {
  transform: translateY(-6px);
  box-shadow: 0 0 15px #60a5fa, 0 0 30px rgba(96,165,250,0.4);
}

/* Links */
.card a {
  color: #60a5fa;
  text-decoration: none;
  font-weight: bold;
}

.card a:hover {
  text-shadow: 0 0 8px #60a5fa;
}
</style>

# 🛡️ Costabo1 Portfolio

<div style="text-align:center; margin: 20px 0;">
  <img class="profile-img" src="assets/images/mewSP.jpg" alt="Profile Image">
</div>

> Penetration testing writeups and security research

---

## 📊 Security Dashboard

<div class="card-container">

<div class="card">
<h3>🧠 HackTheBox Writeups</h3>
<ul>
<li><a href="facts/index123.md">Facts (Linux + Cloud + PrivEsc)</a></li>
<li><a href="Silentium.md">Silentium (Gogs + S3 + RCE chain)</a></li>
</ul>
</div>

<div class="card">
<h3>🔍 LetsDefend SOC Labs</h3>
<ul>
<li>Network Log Analysis</li>
<li>Dynamic Malware Analysis</li>
</ul>
</div>

<div class="card">
<h3>⚙️ Focus Areas</h3>
<ul>
<li>Web Exploitation</li>
<li>Active Directory Attacks</li>
<li>Cloud Security (AWS / S3)</li>
<li>Malware Analysis</li>
</ul>
</div>

</div>

---

## 🔎 About Me

Security enthusiast focused on real-world attack simulation and defensive analysis.

- 🧪 Offensive Security (HTB, labs)
- 📡 SOC / SIEM investigations
- ☁️ Cloud security research
- 🐛 Malware behavior analysis
