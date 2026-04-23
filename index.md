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
  width: 320px;
  height: 320px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid #60a5fa;
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

/* HTB (red) */
.card-htb:hover {
  transform: translateY(-6px);
  box-shadow: 0 0 15px rgb(220,20,60), 0 0 30px rgba(220,20,60,0.4);
}

/* LetsDefend (cyan) */
.card-ld:hover {
  transform: translateY(-6px);
  box-shadow: 0 0 15px rgb(0,255,255), 0 0 30px rgba(0,255,255,0.4);
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
  <img class="profile-img" src="assets/images/mewSP.jpg">
  <h1>🛡️ Costabo1</h1>
  <p>Penetration Testing • SOC Analysis • Malware Research</p>
</div>

---

<!-- PORTFOLIO -->
<div class="section">
<h2>📊 Portfolio</h2>

<div class="card-container">

<div class="card card-htb">
<h3>🧠 HackTheBox</h3>
<ul>
<li><a href="facts/index123.md">Facts (Linux + PrivEsc)</a></li>
<li><a href="Silentium.md">Silentium (RCE chain)</a></li>
</ul>
</div>

<div class="card card-ld">
<h3>🔍 LetsDefend</h3>
<ul>
<li>Network Log Analysis</li>
<li>Dynamic Malware Analysis</li>
</ul>
</div>

</div>
</div>

---

<!-- ABOUT -->
<div class="section">
<h2>🔎 About Me</h2>

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
