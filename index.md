---
layout: default
title: Costabo1 Portfolio
---

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: linear-gradient(135deg, #0a0e27 0%, #1a1a3e 50%, #0f1428 100%);
  background-attachment: fixed;
  color: #e5e7eb;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  overflow-x: hidden;
}

/* Animated background grid effect */
body::before {
  content: '';
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    linear-gradient(0deg, transparent 24%, rgba(0, 255, 200, 0.05) 25%, rgba(0, 255, 200, 0.05) 26%, transparent 27%, transparent 74%, rgba(0, 255, 200, 0.05) 75%, rgba(0, 255, 200, 0.05) 76%, transparent 77%, transparent),
    linear-gradient(90deg, transparent 24%, rgba(0, 255, 200, 0.05) 25%, rgba(0, 255, 200, 0.05) 26%, transparent 27%, transparent 74%, rgba(0, 255, 200, 0.05) 75%, rgba(0, 255, 200, 0.05) 76%, transparent 77%, transparent);
  background-size: 50px 50px;
  pointer-events: none;
  z-index: 0;
}

/* Ensure content sits above background */
.hero, .section, .card-container, .card {
  position: relative;
  z-index: 1;
}

/* ================= HERO ================= */

.hero {
  padding: 80px 20px 40px;
  text-align: center;
  background: linear-gradient(180deg, rgba(10,14,39,0.8), rgba(26,26,62,0.6));
  border-bottom: 2px solid #00ffc8;
  box-shadow: 0 0 30px rgba(0, 255, 200, 0.1);
}

.hero h1 {
  font-size: clamp(32px, 5vw, 52px);
  background: linear-gradient(135deg, #00ffc8, #60a5fa, #ec4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 800;
  letter-spacing: -1px;
  margin-bottom: 15px;
}

.hero p {
  color: #9ca3af;
  font-size: 16px;
  margin-top: 15px;
}

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
  margin-bottom: 30px;
}

.profile-img:hover {
  transform: scale(1.05);
  border-color: #00ffc8;
  box-shadow: 0 0 25px #00ffc8, 0 4px 15px rgba(0,255,200,0.4);
}

.profile-img:active {
  animation: none;
  border-color: rgb(168, 85, 247);
  box-shadow: 0 0 25px rgb(168, 85, 247), 0 0 50px rgba(168, 85, 247, 0.7);
}

@keyframes socPulse {
  0% { box-shadow: 0 0 10px #60a5fa; }
  50% { box-shadow: 0 0 30px #60a5fa; }
  100% { box-shadow: 0 0 10px #60a5fa; }
}

/* ================= TERMINAL HEADER ================= */

.terminal {
  display: inline-block;
  font-family: 'Courier New', monospace;
  font-size: 16px;
  color: #00ffc8;
  background: rgba(0,0,0,0.7);
  padding: 12px 20px;
  border-radius: 6px;
  margin-top: 15px;
  border: 1px solid #00ffc8;
  box-shadow: 
    0 0 10px rgba(0,255,200,0.4),
    inset 0 0 10px rgba(0,255,200,0.1);
}

.typing {
  overflow: hidden;
  border-right: 2px solid #00ffc8;
  white-space: nowrap;
  width: 0;
  animation: typing 4s steps(40, end) forwards, blink 0.8s infinite;
  letter-spacing: 1px;
}

@keyframes typing {
  from { width: 0; }
  to { width: 100%; }
}

@keyframes blink {
  50% { border-color: transparent; }
}

/* ================= ICONS ================= */

.icon {
  width: 28px;
  height: 28px;
  margin-right: 10px;
  vertical-align: middle;
  transition: all 0.3s;
}

.icon-htb { color: rgb(220,20,60); }
.icon-ld { color: rgb(0,255,255); }
.icon-lab { color: rgb(255,165,0); }

.card:hover .icon {
  transform: scale(1.2);
  filter: drop-shadow(0 0 8px currentColor);
}

/* ================= SECTION ================= */

.section {
  padding: 60px 20px;
  max-width: 1200px;
  margin: 0 auto;
}

.section h2 {
  font-size: clamp(24px, 4vw, 36px);
  margin-bottom: 40px;
  text-align: center;
  background: linear-gradient(135deg, #00ffc8, #60a5fa);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 700;
  position: relative;
  padding-bottom: 15px;
}

.section h2::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #00ffc8, transparent);
}

/* ================= CARDS ================= */

.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 25px;
  max-width: 1100px;
  margin: 0 auto;
}

.card {
  background: linear-gradient(135deg, #1a1a3e 0%, #2d2d5f 100%);
  border-radius: 12px;
  padding: 25px;
  transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
  border: 1px solid rgba(0,255,200,0.1);
  position: relative;
  overflow: hidden;
}

.card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(0,255,200,0.1), transparent);
  transition: left 0.5s;
  pointer-events: none;
}

.card:hover::before {
  left: 100%;
}

.card h3 {
  font-size: 18px;
  margin-bottom: 15px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.card ul {
  list-style: none;
  padding-left: 0;
}

.card li {
  padding: 6px 0;
  border-bottom: 1px solid rgba(0,255,200,0.1);
  font-size: 14px;
}

.card li:last-child {
  border-bottom: none;
}

.card a {
  color: #60a5fa;
  text-decoration: none;
  transition: all 0.3s;
  position: relative;
}

.card a::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, #60a5fa, #00ffc8);
  transition: width 0.3s;
}

.card a:hover::after {
  width: 100%;
}

/* Card hover effects */
.card-htb:hover {
  transform: translateY(-8px);
  box-shadow: 0 0 20px rgb(220,20,60), 0 0 40px rgba(220,20,60,0.3);
  border-color: rgb(220,20,60);
}

.card-ld:hover {
  transform: translateY(-8px);
  box-shadow: 0 0 20px rgb(0,255,255), 0 0 40px rgba(0,255,255,0.3);
  border-color: rgb(0,255,255);
}

.card-lab:hover {
  transform: translateY(-8px);
  box-shadow: 0 0 20px rgb(255,165,0), 0 0 40px rgba(255,165,0,0.3);
  border-color: rgb(255,165,0);
}

/* ================= SKILLS ================= */

.skills {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 12px;
  max-width: 900px;
  margin: 30px auto 0;
}

.skill {
  background: linear-gradient(135deg, rgba(0,255,200,0.1), rgba(96,165,250,0.1));
  padding: 10px 18px;
  border-radius: 20px;
  border: 1px solid #00ffc8;
  font-size: 14px;
  transition: all 0.3s;
  cursor: pointer;
}

.skill:hover {
  background: linear-gradient(135deg, rgba(0,255,200,0.2), rgba(96,165,250,0.2));
  box-shadow: 0 0 15px rgba(0,255,200,0.3);
  transform: translateY(-2px);
}

/* ================= FOOTER ================= */

.footer {
  text-align: center;
  padding: 40px 20px;
  border-top: 1px solid rgba(0,255,200,0.1);
  color: #6b7280;
  font-size: 14px;
}

.footer a {
  color: #60a5fa;
  text-decoration: none;
  transition: color 0.3s;
}

.footer a:hover {
  color: #00ffc8;
}

/* ================= RESPONSIVE ================= */

@media (max-width: 768px) {
  .hero {
    padding: 60px 20px 30px;
  }

  .profile-img {
    width: 280px;
    height: 280px;
  }

  .card-container {
    grid-template-columns: 1fr;
  }

  .section h2 {
    font-size: 28px;
  }
}
</style>

<!-- HERO SECTION -->
<div class="hero">
  <img class="profile-img" src="assets/images/mewSP.jpg" alt="Costabo1 Profile">
  
  <h1>Costabo1</h1>
  
  <div class="terminal">
    <span class="typing">$ Power up the bass cannon...</span>
  </div>
  
  <p><i class="fas fa-crosshairs"></i> Penetration Testing • SOC Analysis • Malware Research</p>
</div>

---

<!-- SECURITY DASHBOARD -->
<div class="section">
  <h2><i class="fas fa-shield-alt"></i> Security Dashboard</h2>

  <div class="card-container">
    <!-- HackTheBox Card -->
    <div class="card card-htb">
      <h3>
        <i class="fas fa-cube icon icon-htb"></i>
        HackTheBox
      </h3>
      <ul>
        <li><a href="facts/index11.md"><i class="fas fa-file-alt"></i> Facts (Linux + PrivEsc)</a></li>
        <li><a href="Silentium.md"><i class="fas fa-network-wired"></i> Silentium (RCE chain)</a></li>
      </ul>
    </div>

    <!-- LetsDefend Card -->
    <div class="card card-ld">
      <h3>
        <i class="fas fa-shield-virus icon icon-ld"></i>
        LetsDefend
      </h3>
      <ul>
        <li><i class="fas fa-chart-line"></i> Network Log Analysis</li>
        <li><i class="fas fa-virus"></i> Dynamic Malware Analysis</li>
        <li><i class="fas fa-search"></i> SIEM & Detection Engineering</li>
      </ul>
    </div>

    <!-- Research Lab Card -->
    <div class="card card-lab">
      <h3>
        <i class="fas fa-flask icon icon-lab"></i>
        Research Lab
      </h3>
      <ul>
        <li><i class="fas fa-brain"></i> Custom Detection Models</li>
        <li><i class="fas fa-code"></i> Automation Scripts</li>
        <li><i class="fas fa-bomb"></i> Exploit Development (WIP)</li>
      </ul>
    </div>
  </div>
</div>

---

<!-- ABOUT SECTION -->
<div class="section">
  <h2><i class="fas fa-user-secret"></i> About Me</h2>

  <p style="text-align: center; font-size: 16px; color: #d1d5db; max-width: 700px; margin: 0 auto 30px;">
    Security enthusiast focused on <strong>real-world attack simulation</strong> and <strong>defensive analysis</strong>. 
    Experienced in penetration testing, SOC operations, and building detection capabilities from the ground up.
  </p>

  <div class="skills">
    <span class="skill"><i class="fas fa-globe"></i> Web Exploitation</span>
    <span class="skill"><i class="fas fa-network-wired"></i> Active Directory</span>
    <span class="skill"><i class="fas fa-cloud"></i> Cloud Security</span>
    <span class="skill"><i class="fas fa-virus"></i> Malware Analysis</span>
    <span class="skill"><i class="fas fa-eye"></i> SIEM</span>
    <span class="skill"><i class="fas fa-terminal"></i> Python & Bash</span>
  </div>
</div>

---

<!-- FOOTER -->
<div class="footer">
  <p>
    <i class="fas fa-code"></i> Built with <span style="color: #ec4899;">❤</span> | 
    <a href="https://github.com/Costabo1"><i class="fab fa-github"></i> GitHub</a> | 
    Last updated: 2026
  </p>
</div>
