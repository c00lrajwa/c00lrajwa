<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KHAN - GitHub Profile Preview</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=VT323&display=swap');

  :root {
    --green: #00ff41;
    --dark-green: #00cc33;
    --dim-green: #003b00;
    --black: #000000;
    --red: #ff0000;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #000;
    color: var(--green);
    font-family: 'Share Tech Mono', monospace;
    overflow-x: hidden;
  }

  /* MATRIX CANVAS */
  #matrix {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    opacity: 0.08;
  }

  .content {
    position: relative;
    z-index: 1;
    max-width: 900px;
    margin: 0 auto;
    padding: 20px;
  }

  /* HEADER */
  .hero {
    text-align: center;
    padding: 60px 20px 40px;
    border-bottom: 1px solid var(--dim-green);
  }

  .ascii-name {
    font-family: 'VT323', monospace;
    font-size: clamp(28px, 6vw, 56px);
    color: var(--green);
    text-shadow: 0 0 10px var(--green), 0 0 30px var(--green), 0 0 60px var(--green);
    letter-spacing: 8px;
    animation: flicker 4s infinite;
    line-height: 1.1;
  }

  .ascii-art {
    font-size: clamp(6px, 1.5vw, 11px);
    line-height: 1.2;
    color: var(--green);
    text-shadow: 0 0 5px var(--green);
    white-space: pre;
    overflow-x: auto;
  }

  @keyframes flicker {
    0%, 95%, 100% { opacity: 1; }
    96% { opacity: 0.4; }
    97% { opacity: 1; }
    98% { opacity: 0.2; }
    99% { opacity: 1; }
  }

  .subtitle {
    font-size: 14px;
    color: var(--dark-green);
    letter-spacing: 6px;
    margin-top: 10px;
    animation: blink 2s step-end infinite;
  }

  @keyframes blink {
    50% { opacity: 0; }
  }

  /* SECTIONS */
  .section {
    margin: 30px 0;
    border: 1px solid var(--dim-green);
    padding: 20px;
    position: relative;
    background: rgba(0, 255, 65, 0.02);
  }

  .section::before {
    content: attr(data-title);
    position: absolute;
    top: -12px;
    left: 20px;
    background: #000;
    padding: 0 10px;
    color: var(--green);
    font-size: 12px;
    letter-spacing: 3px;
    text-shadow: 0 0 8px var(--green);
  }

  /* TERMINAL */
  .terminal {
    background: #000;
    border: 1px solid var(--green);
    padding: 20px;
    font-size: 13px;
    line-height: 2;
    box-shadow: 0 0 20px rgba(0, 255, 65, 0.15), inset 0 0 30px rgba(0, 255, 65, 0.03);
  }

  .terminal-header {
    display: flex;
    gap: 8px;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--dim-green);
  }

  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot-red { background: #ff5f56; box-shadow: 0 0 6px #ff5f56; }
  .dot-yellow { background: #ffbd2e; box-shadow: 0 0 6px #ffbd2e; }
  .dot-green { background: #27c93f; box-shadow: 0 0 6px #27c93f; }

  .prompt { color: var(--green); }
  .cmd { color: #fff; }
  .output { color: var(--dark-green); padding-left: 10px; }
  .cursor { 
    display: inline-block;
    width: 8px; height: 16px;
    background: var(--green);
    animation: blink 1s step-end infinite;
    vertical-align: middle;
  }

  /* TYPING ANIMATION */
  .typing-line {
    overflow: hidden;
    white-space: nowrap;
    animation: typing 0.5s steps(40, end) forwards;
    width: 0;
  }

  .typing-line:nth-child(1) { animation-delay: 0.5s; }
  .typing-line:nth-child(2) { animation-delay: 1.5s; }
  .typing-line:nth-child(3) { animation-delay: 2.5s; }
  .typing-line:nth-child(4) { animation-delay: 3.5s; }
  .typing-line:nth-child(5) { animation-delay: 4.5s; }
  .typing-line:nth-child(6) { animation-delay: 5s; }
  .typing-line:nth-child(7) { animation-delay: 5.5s; }

  @keyframes typing {
    from { width: 0; }
    to { width: 100%; }
  }

  /* SKILL BARS */
  .skill-row {
    display: flex;
    align-items: center;
    gap: 15px;
    margin: 10px 0;
  }

  .skill-name {
    width: 160px;
    font-size: 13px;
    color: var(--dark-green);
    flex-shrink: 0;
  }

  .skill-bar-bg {
    flex: 1;
    height: 16px;
    background: rgba(0, 255, 65, 0.08);
    border: 1px solid var(--dim-green);
    position: relative;
    overflow: hidden;
  }

  .skill-bar-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--dim-green), var(--green));
    box-shadow: 0 0 10px var(--green);
    position: relative;
    animation: fillBar 2s ease forwards;
    transform-origin: left;
    transform: scaleX(0);
  }

  @keyframes fillBar {
    to { transform: scaleX(1); }
  }

  .skill-pct {
    width: 40px;
    font-size: 12px;
    color: var(--green);
    text-align: right;
  }

  /* VISITOR COUNTER */
  .counter-box {
    text-align: center;
    padding: 20px;
    border: 1px solid var(--green);
    box-shadow: 0 0 30px rgba(0, 255, 65, 0.1);
    position: relative;
  }

  .counter-display {
    font-family: 'VT323', monospace;
    font-size: 72px;
    color: var(--green);
    text-shadow: 0 0 20px var(--green), 0 0 40px var(--green);
    letter-spacing: 10px;
    line-height: 1;
  }

  .counter-label {
    font-size: 11px;
    letter-spacing: 5px;
    color: var(--dark-green);
    margin-top: 10px;
  }

  /* STATUS BADGE */
  .status-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 10px;
  }

  .status-item {
    border: 1px solid var(--dim-green);
    padding: 12px;
    font-size: 12px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .status-val { color: var(--green); font-size: 14px; }
  .status-online { color: #00ff41; }
  .status-warn { color: #ffbd2e; }

  /* BADGES */
  .badge-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    justify-content: center;
  }

  .badge {
    background: #000;
    border: 1px solid var(--green);
    color: var(--green);
    padding: 6px 14px;
    font-size: 11px;
    letter-spacing: 1px;
    text-shadow: 0 0 5px var(--green);
    box-shadow: 0 0 8px rgba(0, 255, 65, 0.1);
    transition: all 0.3s;
    cursor: default;
  }

  .badge:hover {
    background: var(--dim-green);
    box-shadow: 0 0 15px var(--green);
  }

  /* SCAN LINE EFFECT */
  body::after {
    content: '';
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0, 0, 0, 0.05) 2px,
      rgba(0, 0, 0, 0.05) 4px
    );
    pointer-events: none;
    z-index: 10;
  }

  /* FOOTER */
  .footer {
    text-align: center;
    padding: 40px 20px;
    border-top: 1px solid var(--dim-green);
    color: var(--dark-green);
    font-size: 11px;
    letter-spacing: 3px;
  }

  /* GLITCH */
  .glitch {
    position: relative;
  }
  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0;
    width: 100%;
  }
  .glitch::before {
    color: #ff0000;
    animation: glitch1 3s infinite;
    clip-path: polygon(0 0, 100% 0, 100% 40%, 0 40%);
  }
  .glitch::after {
    color: #00ffff;
    animation: glitch2 3s infinite;
    clip-path: polygon(0 60%, 100% 60%, 100% 100%, 0 100%);
  }
  @keyframes glitch1 {
    0%, 85%, 100% { transform: translateX(0); }
    86% { transform: translateX(-3px); }
    87% { transform: translateX(3px); }
    88% { transform: translateX(0); }
  }
  @keyframes glitch2 {
    0%, 90%, 100% { transform: translateX(0); }
    91% { transform: translateX(3px); }
    92% { transform: translateX(-3px); }
    93% { transform: translateX(0); }
  }

  pre { overflow-x: auto; }
</style>
</head>
<body>

<canvas id="matrix"></canvas>

<div class="content">
  
  <!-- HERO -->
  <div class="hero">
    <div class="ascii-name glitch" data-text="[ KHAN ]">[ KHAN ]</div>
    <pre class="ascii-art">
██╗  ██╗██╗  ██╗ █████╗ ███╗   ██╗
██║ ██╔╝██║  ██║██╔══██╗████╗  ██║
█████╔╝ ███████║███████║██╔██╗ ██║
██╔═██╗ ██╔══██║██╔══██║██║╚██╗██║
██║  ██╗██║  ██║██║  ██║██║ ╚████║
╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═══╝</pre>
    <div class="subtitle">〔 SYSTEM BREACH AUTHORIZED 〕 <span class="cursor"></span></div>
  </div>

  <!-- STATUS GRID -->
  <div class="section" data-title="〔 SYSTEM STATUS 〕">
    <div class="status-grid">
      <div class="status-item">
        <span>IDENTITY</span>
        <span class="status-val">[ CLASSIFIED ]</span>
      </div>
      <div class="status-item">
        <span>ACCESS LEVEL</span>
        <span class="status-val status-online">ROOT ✓</span>
      </div>
      <div class="status-item">
        <span>STATUS</span>
        <span class="status-val status-online">● ONLINE</span>
      </div>
      <div class="status-item">
        <span>THREAT LEVEL</span>
        <span class="status-val" style="color: #ff0000;">■ MAXIMUM</span>
      </div>
      <div class="status-item">
        <span>LOCATION</span>
        <span class="status-val">[REDACTED]</span>
      </div>
      <div class="status-item">
        <span>COFFEE</span>
        <span class="status-val status-warn">████░░ 80%</span>
      </div>
    </div>
  </div>

  <!-- LIVE TERMINAL -->
  <div class="section" data-title="〔 LIVE TERMINAL 〕">
    <div class="terminal">
      <div class="terminal-header">
        <div class="dot dot-red"></div>
        <div class="dot dot-yellow"></div>
        <div class="dot dot-green"></div>
        <span style="margin-left: 10px; font-size: 11px; color: #555;">KHAN@root — bash — 80×24</span>
      </div>
      <div id="terminal-lines"></div>
      <div><span class="prompt">[KHAN@root ~]$ </span><span class="cursor"></span></div>
    </div>
  </div>

  <!-- SKILL BARS -->
  <div class="section" data-title="〔 SKILL MATRIX 〕">
    <div id="skills"></div>
  </div>

  <!-- VISITOR COUNTER -->
  <div class="section" data-title="〔 SURVEILLANCE LOG 〕">
    <div class="counter-box">
      <div style="font-size: 11px; color: #555; letter-spacing: 3px; margin-bottom: 15px;">
        [ UNAUTHORIZED ACCESS DETECTED — YOUR IP HAS BEEN LOGGED ]
      </div>
      <div class="counter-display" id="counter">000000</div>
      <div class="counter-label">TOTAL INFILTRATIONS ON THIS PROFILE</div>
      <div style="margin-top: 15px; font-size: 11px; color: #333;">
        [ DATA COLLECTION COMPLETE ] [ IDENTITY: CLASSIFIED ] [ ✓ ]
      </div>
    </div>
  </div>

  <!-- ARSENAL -->
  <div class="section" data-title="〔 ARSENAL / TOOLS 〕">
    <div class="badge-grid">
      <div class="badge">⚡ PYTHON</div>
      <div class="badge">⚡ JAVASCRIPT</div>
      <div class="badge">⚡ LINUX</div>
      <div class="badge">⚡ KALI</div>
      <div class="badge">⚡ DOCKER</div>
      <div class="badge">⚡ REACT</div>
      <div class="badge">⚡ NODE.JS</div>
      <div class="badge">⚡ BASH</div>
      <div class="badge">⚡ MYSQL</div>
      <div class="badge">⚡ MONGODB</div>
      <div class="badge">⚡ WIRESHARK</div>
      <div class="badge">⚡ METASPLOIT</div>
      <div class="badge">⚡ NMAP</div>
      <div class="badge">⚡ BURP SUITE</div>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="footer">
    <div style="font-size: 20px; color: var(--green); margin-bottom: 10px; text-shadow: 0 0 10px var(--green);">
      〔 SESSION TERMINATED 〕
    </div>
    ALL DATA ENCRYPTED · SEE YOU IN THE MATRIX<br><br>
    <span style="color: #222;">[ MADE WITH </span><span style="color: #ff0000;">❤</span><span style="color: #222;"> BY KHAN ]</span>
  </div>

</div>

<script>
// ═══════════════════════════════════════
// MATRIX RAIN
// ═══════════════════════════════════════
const canvas = document.getElementById('matrix');
const ctx = canvas.getContext('2d');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const chars = 'アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ!@#$%^&*';
const fontSize = 14;
const columns = canvas.width / fontSize;
const drops = Array(Math.floor(columns)).fill(1);

function drawMatrix() {
  ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  ctx.fillStyle = '#00ff41';
  ctx.font = fontSize + 'px monospace';
  
  drops.forEach((y, i) => {
    const char = chars[Math.floor(Math.random() * chars.length)];
    ctx.fillStyle = Math.random() > 0.95 ? '#ffffff' : '#00ff41';
    ctx.fillText(char, i * fontSize, y * fontSize);
    if (y * fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
    drops[i]++;
  });
}

setInterval(drawMatrix, 40);

window.addEventListener('resize', () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
});

// ═══════════════════════════════════════
// TERMINAL TYPING
// ═══════════════════════════════════════
const lines = [
  { type: 'prompt', text: '[KHAN@root ~]$ ./scan_network.sh --target=github.com' },
  { type: 'output', text: '> Initializing nmap scan...' },
  { type: 'output', text: '> Ports open: 22, 80, 443 — Target SECURED' },
  { type: 'prompt', text: '[KHAN@root ~]$ git log --oneline -3' },
  { type: 'output', text: '> a1b2c3d fix: memory leak in core module (+1337 lines)' },
  { type: 'output', text: '> e4f5g6h feat: implement zero-day detection system' },
  { type: 'prompt', text: '[KHAN@root ~]$ cat /proc/brain | grep status' },
  { type: 'output', text: '> Coffee: 80% | Focus: 100% | Bug Mode: ACTIVE | Sleep: LOL' },
];

const terminalEl = document.getElementById('terminal-lines');
let lineIdx = 0;

function typeNextLine() {
  if (lineIdx >= lines.length) { lineIdx = 0; terminalEl.innerHTML = ''; }
  const line = lines[lineIdx++];
  const div = document.createElement('div');
  div.style.lineHeight = '1.8';
  
  const span = document.createElement('span');
  span.className = line.type === 'prompt' ? 'prompt' : 'output';
  div.appendChild(span);
  terminalEl.appendChild(div);
  
  let charIdx = 0;
  const interval = setInterval(() => {
    if (charIdx < line.text.length) {
      span.textContent += line.text[charIdx++];
    } else {
      clearInterval(interval);
      setTimeout(typeNextLine, line.type === 'output' ? 400 : 800);
    }
  }, line.type === 'prompt' ? 30 : 15);
}

setTimeout(typeNextLine, 500);

// ═══════════════════════════════════════
// SKILL BARS
// ═══════════════════════════════════════
const skills = [
  { name: 'Python', pct: 95 },
  { name: 'Cybersecurity', pct: 90 },
  { name: 'Linux / Bash', pct: 95 },
  { name: 'JavaScript', pct: 88 },
  { name: 'React / Node.js', pct: 85 },
  { name: 'SQL / NoSQL', pct: 80 },
  { name: 'Docker / K8s', pct: 72 },
  { name: 'CTF / Hacking', pct: 99 },
];

const skillsEl = document.getElementById('skills');
skills.forEach((s, i) => {
  skillsEl.innerHTML += `
  <div class="skill-row">
    <div class="skill-name">${s.name}</div>
    <div class="skill-bar-bg">
      <div class="skill-bar-fill" style="width:${s.pct}%; animation-delay:${i * 0.15}s"></div>
    </div>
    <div class="skill-pct">${s.pct}%</div>
  </div>`;
});

// ═══════════════════════════════════════
// VISITOR COUNTER
// ═══════════════════════════════════════
const counterEl = document.getElementById('counter');
let count = 0;
const target = Math.floor(Math.random() * 50000) + 100000;

function animateCounter() {
  if (count < target) {
    count += Math.floor((target - count) / 15) + 1;
    if (count > target) count = target;
    counterEl.textContent = String(count).padStart(6, '0');
    requestAnimationFrame(animateCounter);
  }
}

setTimeout(animateCounter, 800);
</script>
</body>
</html>
