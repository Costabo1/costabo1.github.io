---

layout: default
title: Costabo1 Portfolio
---

<style>
body {
  background-color: #0b1220;
  color: #e5e7eb;
  text-align: center;
}

/* ================= HERO ================= */

.hero {
  padding: 60px 20px 20px;
}

.hero h1 {
  font-size: 40px;
}

.hero p {
  color: #9ca3af;
}

/* ================= PROFILE ================= */

.profile-img {
  width: 420px;
  height: 420px;
  border-radius: 50%;
  object-fit: cover;
  border: 5px solid #60a5fa;
  cursor: pointer;

  box-shadow: 0 0 15px #60a5fa, 0 4px 15px rgba(0,0,0,0.4);
  animation: socPulse 2.5s infinite ease-in-out;
  transition: all 0.3s ease;
}

.profile-img:hover {
  transform: scale(1.05);
}

.profile-img:active {
  animation: none;
  border-color: rgb(168, 85, 247);
  box-shadow:
    0 0 25px rgb(168, 85, 247),
    0 0 50px rgba(168, 85, 247, 0.7),
    0 0 80px rgba(168, 85, 247, 0.5);
}

/* Pulse */
@keyframes socPulse {
  0% { box-shadow: 0 0 10px #60a5fa; }
  50% { box-shadow: 0 0 30px #60a5fa; }
  100% { box-shadow: 0 0 10px #60a5fa; }
}

  /* ================= TERMINAL HEADER ================= */

.terminal {
  display: inline-block;
  font-family: monospace;
  font-size: 16px;
  color: #22c55e;
  background: rgba(0,0,0,0.6);
  padding: 10px 16px;
  border-radius: 6px;
  margin-top: 10px;
  box-shadow: 0 0 10px rgba(34,197,94,0.4);
}

/* typing effect */
.typing {
  overflow: hidden;
  border-right: 2px solid #22c55e;
  white-space: nowrap;
  width: 0;
  animation:
    typing 4s steps(40, end) forwards,
    blink 0.8s infinite;
}

/* typing animation */
@keyframes typing {
  from { width: 0; }
  to { width: 100%; }
}

/* cursor blink */
@keyframes blink {
  50% { border-color: transparent; }
}

/* ================= ICONS ================= */

.icon {
  width: 22px;
  height: 22px;
  margin-right: 8px;
  vertical-align: middle;
  stroke: currentColor;
  fill: none;
  stroke-width: 2;
  transition: 0.3s;
}

.icon-htb { color: rgb(220,20,60); }   /* red */
.icon-ld  { color: rgb(0,255,255); }   /* cyan */
.icon-lab { color: rgb(255,165,0); }   /* orange */

/* glow on hover */
.card:hover .icon {
  filter: drop-shadow(0 0 6px currentColor);
}

/* ================= SECTION ================= */

.section {
  padding: 60px 20px;
}

.section h2 {
  margin-bottom: 20px;
}

/* ================= CARDS ================= */

.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 20px;
  max-width: 900px;
  margin: auto;
}

.card {
  background: #111827;
  border-radius: 12px;
  padding: 20px;
  transition: 0.3s;
}

/* HTB */
.card-htb:hover {
  transform: translateY(-6px);
  box-shadow: 0 0 15px rgb(220,20,60), 0 0 30px rgba(220,20,60,0.4);
}

/* LetsDefend */
.card-ld:hover {
  transform: translateY(-6px);
  box-shadow: 0 0 15px rgb(0,255,255), 0 0 30px rgba(0,255,255,0.4);
}

/* Research Lab */
.card-lab:hover {
  transform: translateY(-6px);
  box-shadow: 0 0 15px rgb(255,165,0), 0 0 30px rgba(255,165,0,0.5);
}

.card a {
  color: #60a5fa;
  text-decoration: none;
}

/* ================= SKILLS ================= */

.skills {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
}

.skill {
  background: #111827;
  padding: 8px 14px;
  border-radius: 20px;
  border: 1px solid #2d3748;
  font-size: 14px;
}
</style>

<!-- HERO -->

<div class="hero">
  <img class="profile-img" src="assets/images/mewSP.jpg" alt="Profile">
  <h1>Costabo1</h1>
 <div class="terminal">
  <span class="typing">$ Power up the bass cannon...</span>
</div>

<p>Penetration Testing • SOC Analysis • Malware Research</p>
</div>

---

<!-- SECURITY DASHBOARD -->

<div class="section">
<h2>
<svg class="icon" viewBox="0 0 24 24">
  <rect x="3" y="3" width="7" height="7"></rect>
  <rect x="14" y="3" width="7" height="4"></rect>
  <rect x="14" y="9" width="7" height="12"></rect>
  <rect x="3" y="12" width="7" height="9"></rect>
</svg>
Security Dashboard
</h2>

<div class="card-container">

<div class="card card-htb">
<h3>
<svg class="icon icon-htb" viewBox="0 0 24 24">
  <path d="M3 7l9-4 9 4-9 4-9-4z"></path>
  <path d="M3 7v10l9 4 9-4V7"></path>
</svg>
HackTheBox
</h3>
<ul>
<li><a href="facts/index11.md">Facts (Linux + PrivEsc)</a></li>
<li><a href="Silentium.md">Silentium (RCE chain)</a></li>
</ul>
</div>

<div class="card card-ld">
<h3>
<svg class="icon icon-ld" viewBox="0 0 24 24">
  <path d="M12 3l7 4v5c0 5-3.5 8-7 9-3.5-1-7-4-7-9V7l7-4z"></path>
</svg>
LetsDefend
</h3>
<ul>
<li>Network Log Analysis</li>
<li>Dynamic Malware Analysis</li>
</ul>
</div>

<div class="card card-lab">
<h3>
<svg class="icon icon-lab" viewBox="0 0 24 24">
  <path d="M9 18h6"></path>
  <path d="M10 22h4"></path>
  <path d="M12 2a7 7 0 0 0-4 12c1 1 2 2 2 4h4c0-2 1-3 2-4a7 7 0 0 0-4-12z"></path>
</svg>
Research Lab
</h3>
<ul>
<li>Custom Detection Models</li>
<li>Automation Scripts</li>
<li>Exploit Development (WIP)</li>
</ul>
</div>

</div>
</div>

---

<!-- ABOUT -->

<div class="section">
<h2>About Me</h2>

<p>
Security enthusiast focused on real-world attack simulation and defensive analysis.
</p>

<div class="skills">
<span class="skill">Web Exploitation</span>
<span class="skill">Active Directory</span>
<span class="skill">Cloud Security</span>
<span class="skill">Malware Analysis</span>
<span class="skill">SIEM</span>
</div>

</div>
