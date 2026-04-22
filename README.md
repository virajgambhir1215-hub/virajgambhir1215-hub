<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>virajgambhir1215-hub / README</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet"/>
<style>
:root {
  --bg: #020608;
  --bg2: #050d0f;
  --bg3: #071015;
  --cyan: #00ff9d;
  --gold: #f0c040;
  --red: #ff2255;
  --purple: #bf5fff;
  --text: #b0ffd0;
  --muted: #3a6050;
  --dim: #1a3028;
  --border: rgba(0,255,157,0.13);
}
* { margin:0; padding:0; box-sizing:border-box; cursor:none !important; }
html { scroll-behavior: smooth; }

body {
  font-family: 'Share Tech Mono', monospace;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  overflow-x: hidden;
  line-height: 1.7;
}

/* scanlines */
body::before {
  content: '';
  position: fixed; inset: 0; z-index: 0; pointer-events: none;
  background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.05) 2px, rgba(0,0,0,0.05) 4px);
}

/* matrix canvas */
#mx { position: fixed; inset: 0; z-index: 0; pointer-events: none; opacity: 0.06; }

/* sweep line */
.sweep {
  position: fixed; top: -4px; left: 0; right: 0; height: 3px;
  z-index: 2; pointer-events: none;
  background: linear-gradient(90deg, transparent, var(--cyan), transparent);
  box-shadow: 0 0 20px var(--cyan), 0 0 50px rgba(0,255,157,0.3);
  animation: swp 8s linear infinite;
}
@keyframes swp { 0% { top: -4px; } 100% { top: 100vh; } }

/* cursor */
#cur {
  position: fixed; width: 10px; height: 10px;
  background: var(--cyan); border-radius: 50%;
  pointer-events: none; z-index: 9999;
  transform: translate(-50%,-50%);
  box-shadow: 0 0 10px var(--cyan), 0 0 30px rgba(0,255,157,0.4);
}
#cur2 {
  position: fixed; width: 28px; height: 28px;
  border: 1px solid rgba(0,255,157,0.4); border-radius: 50%;
  pointer-events: none; z-index: 9998;
  transform: translate(-50%,-50%);
  transition: all 0.08s linear;
}

/* wrapper */
.wrap {
  max-width: 900px; margin: 0 auto;
  padding: 40px 20px 80px;
  position: relative; z-index: 3;
}

/* terminal window */
.terminal {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 10px; overflow: hidden;
  box-shadow: 0 0 60px rgba(0,255,157,0.04), 0 20px 60px rgba(0,0,0,0.7);
  margin-bottom: 20px;
  opacity: 0; transform: translateY(24px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.terminal.vis { opacity: 1; transform: none; }

.term-bar {
  background: #0a1a14;
  padding: 10px 16px;
  display: flex; align-items: center; gap: 8px;
  border-bottom: 1px solid var(--border);
}
.dot { width: 11px; height: 11px; border-radius: 50%; }
.dot.r { background: #ff5f56; box-shadow: 0 0 6px #ff5f56; }
.dot.y { background: #ffbd2e; box-shadow: 0 0 6px #ffbd2e; }
.dot.g { background: #27c93f; box-shadow: 0 0 6px #27c93f; }
.term-title {
  margin: 0 auto;
  font-size: 0.62rem; color: var(--muted); letter-spacing: 2px;
}
.term-body { padding: 22px 26px; }

/* glitch name */
.glitch-wrap { text-align: center; padding: 8px 0 18px; }
.glitch {
  font-family: 'Orbitron', monospace;
  font-size: clamp(1.5rem, 5vw, 2.8rem);
  font-weight: 900; color: var(--cyan);
  letter-spacing: 6px;
  text-shadow: 0 0 20px rgba(0,255,157,0.4), 0 0 60px rgba(0,255,157,0.15);
  display: inline-block; position: relative;
  animation: g1 6s infinite 3s;
}
.glitch::before, .glitch::after {
  content: attr(data-text);
  position: absolute; inset: 0;
  font-family: 'Orbitron', monospace;
  font-size: inherit; font-weight: inherit; letter-spacing: inherit;
}
.glitch::before { color: var(--red); clip-path: polygon(0 20%,100% 20%,100% 40%,0 40%); animation: gb 6s infinite 3s; }
.glitch::after  { color: #00ccff;  clip-path: polygon(0 60%,100% 60%,100% 80%,0 80%); animation: ga 6s infinite 3.05s; }
@keyframes g1 { 0%,85%,100%{transform:none;} 86%{transform:translate(-2px,0);} 88%{transform:translate(2px,0);} 90%{transform:none;} }
@keyframes gb { 0%,85%,100%{opacity:0;transform:none;} 86%{opacity:1;transform:translate(-3px,0);} 88%{transform:translate(3px,0);} 90%{opacity:0;} }
@keyframes ga { 0%,85%,100%{opacity:0;transform:none;} 87%{opacity:1;transform:translate(3px,0);} 89%{transform:translate(-3px,0);} 90%{opacity:0;} }

.subtitle {
  font-size: 0.68rem; color: var(--muted);
  letter-spacing: 2px; margin-top: 10px; text-align: center;
}
.blink { animation: bl 1.3s step-end infinite; }
@keyframes bl { 50% { opacity: 0; } }

/* badges */
.badges { display: flex; flex-wrap: wrap; justify-content: center; gap: 8px; padding: 16px 0 8px; }
.badge {
  display: inline-flex; align-items: center; gap: 7px;
  padding: 6px 14px; border-radius: 5px;
  font-size: 0.6rem; letter-spacing: 0.5px;
  text-decoration: none; border: 1px solid;
  transition: transform 0.2s, box-shadow 0.2s;
  overflow: hidden; position: relative;
}
.badge::before {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.05), transparent);
  transform: translateX(-100%); transition: transform 0.4s;
}
.badge:hover::before { transform: translateX(100%); }
.badge:hover { transform: translateY(-2px); }
.b-li  { background: rgba(0,119,181,0.15); border-color: rgba(0,119,181,0.4); color: #4fbaff; }
.b-gh  { background: rgba(255,255,255,0.05); border-color: rgba(255,255,255,0.15); color: #ccc; }
.b-gm  { background: rgba(209,72,54,0.15); border-color: rgba(209,72,54,0.3); color: #ff7060; }
.b-loc { background: rgba(0,255,157,0.06); border-color: rgba(0,255,157,0.2); color: var(--cyan); }
.b-st  { background: rgba(0,255,157,0.06); border-color: rgba(0,255,157,0.2); color: var(--cyan); font-size: 0.58rem; }
.b-li:hover  { box-shadow: 0 4px 20px rgba(0,119,181,0.3); }
.b-gh:hover  { box-shadow: 0 4px 20px rgba(255,255,255,0.1); }
.b-gm:hover  { box-shadow: 0 4px 20px rgba(209,72,54,0.2); }
.b-loc:hover { box-shadow: 0 4px 20px rgba(0,255,157,0.15); }

.pdot {
  width: 7px; height: 7px; border-radius: 50%;
  background: var(--cyan); display: inline-block;
  box-shadow: 0 0 8px var(--cyan);
  animation: pd 2s ease-in-out infinite;
}
@keyframes pd { 0%,100%{opacity:1;box-shadow:0 0 8px var(--cyan);} 50%{opacity:0.5;box-shadow:0 0 20px var(--cyan);} }

/* section heading */
.sh {
  font-family: 'Orbitron', monospace;
  font-size: 0.8rem; font-weight: 700;
  color: var(--cyan); letter-spacing: 3px; text-transform: uppercase;
  margin-bottom: 16px; display: flex; align-items: center; gap: 10px;
}
.sh::after { content: ''; flex: 1; height: 1px; background: linear-gradient(90deg, var(--border), transparent); }

/* whoami block */
.wblock {
  background: rgba(0,255,157,0.03);
  border: 1px solid var(--border); border-radius: 8px; padding: 18px 20px;
  position: relative; overflow: hidden;
}
.wblock::before {
  content: ''; position: absolute; left: 0; top: 0; bottom: 0;
  width: 2px; background: linear-gradient(180deg, var(--cyan), transparent);
}
.prompt { font-size: 0.63rem; color: var(--muted); margin-bottom: 8px; }
.prompt .u { color: #27c93f; }
.prompt .p { color: var(--cyan); }
.plines { display: flex; flex-direction: column; gap: 4px; }
.pl { font-size: 0.68rem; display: flex; }
.pk { color: var(--muted); min-width: 82px; }
.pv { color: #fff; }
.pv .h { color: var(--cyan); }
.pv .g { color: var(--cyan); }
.qblock {
  border-left: 2px solid var(--cyan); padding: 10px 14px; margin-top: 14px;
  background: rgba(0,255,157,0.03); border-radius: 0 6px 6px 0;
  font-size: 0.68rem; color: var(--muted); font-style: italic; line-height: 1.8;
}

/* about list */
.alist { display: flex; flex-direction: column; gap: 8px; }
.al {
  display: flex; align-items: flex-start; gap: 10px;
  font-size: 0.7rem; line-height: 1.7;
  padding: 8px 12px; border-radius: 6px;
  border: 1px solid transparent;
  transition: background 0.25s, border-color 0.25s, transform 0.25s;
}
.al:hover { background: rgba(0,255,157,0.04); border-color: var(--border); transform: translateX(5px); }
.al b { color: var(--cyan); }
.ali { flex-shrink: 0; margin-top: 1px; }

/* skill section */
.scat { margin-bottom: 16px; }
.clabel {
  font-size: 0.58rem; color: var(--muted);
  letter-spacing: 2px; text-transform: uppercase;
  margin-bottom: 10px; display: flex; align-items: center; gap: 6px;
}
.clabel::after { content: ''; flex: 1; height: 1px; background: var(--dim); }
.srow { display: flex; flex-wrap: wrap; gap: 7px; }
.sk {
  padding: 5px 12px; border-radius: 5px;
  font-size: 0.58rem; letter-spacing: 0.5px; border: 1px solid;
  display: flex; align-items: center; gap: 5px;
  transition: transform 0.2s, box-shadow 0.2s; cursor: default;
}
.sk:hover { transform: translateY(-2px); }
.sk-cy { background: rgba(0,212,255,0.07); border-color: rgba(0,212,255,0.25); color: #00d4ff; }
.sk-re { background: rgba(255,34,85,0.07); border-color: rgba(255,34,85,0.25); color: #ff5577; }
.sk-go { background: rgba(240,192,64,0.07); border-color: rgba(240,192,64,0.25); color: var(--gold); }
.sk-gr { background: rgba(0,255,157,0.07); border-color: rgba(0,255,157,0.2); color: var(--cyan); }
.sk-pu { background: rgba(191,95,255,0.07); border-color: rgba(191,95,255,0.25); color: var(--purple); }
.sk-cy:hover { box-shadow: 0 4px 14px rgba(0,212,255,0.2); }
.sk-re:hover { box-shadow: 0 4px 14px rgba(255,34,85,0.2); }
.sk-go:hover { box-shadow: 0 4px 14px rgba(240,192,64,0.2); }
.sk-gr:hover { box-shadow: 0 4px 14px rgba(0,255,157,0.15); }
.sk-pu:hover { box-shadow: 0 4px 14px rgba(191,95,255,0.2); }

/* project card */
.pcard {
  background: var(--bg3); border: 1px solid var(--border);
  border-radius: 10px; padding: 18px 20px; margin-bottom: 14px;
  position: relative; overflow: hidden;
  transition: border-color 0.3s, box-shadow 0.3s, transform 0.3s;
}
.pcard:hover {
  border-color: rgba(0,255,157,0.35);
  box-shadow: 0 0 40px rgba(0,255,157,0.05), 0 10px 40px rgba(0,0,0,0.5);
  transform: translateY(-3px);
}
.pcard::before {
  content: ''; position: absolute; left: 0; top: 0; bottom: 0; width: 3px;
  background: linear-gradient(180deg, var(--cyan), transparent);
}
.pcard::after {
  content: ''; position: absolute; top: 0; left: -100%; width: 40%; height: 100%;
  background: linear-gradient(90deg, transparent, rgba(0,255,157,0.03), transparent);
  transition: left 0.7s; pointer-events: none;
}
.pcard:hover::after { left: 200%; }
.ptitle { font-family: 'Orbitron', monospace; font-size: 0.82rem; font-weight: 700; color: #fff; letter-spacing: 1px; margin-bottom: 4px; }
.ptag   { font-size: 0.58rem; color: var(--cyan); margin-bottom: 10px; letter-spacing: 1px; }
.pline  { font-size: 0.63rem; color: var(--muted); font-style: italic; margin-bottom: 12px; padding: 5px 10px; border-left: 2px solid var(--muted); }

.ascii {
  background: #020a06; border: 1px solid var(--dim); border-radius: 6px;
  padding: 12px 14px; margin-bottom: 12px;
  font-size: 0.59rem; color: #2a5040; line-height: 1.6;
  overflow-x: auto; white-space: pre;
  font-family: 'Share Tech Mono', monospace;
}
.ascii .hl { color: var(--cyan); }

.pdesc { font-size: 0.68rem; line-height: 1.8; margin-bottom: 10px; }
.pdesc b { color: var(--cyan); }
.pbullets { display: flex; flex-direction: column; gap: 5px; margin-bottom: 12px; }
.pb { font-size: 0.66rem; line-height: 1.6; padding-left: 14px; position: relative; }
.pb::before { content: '▸'; position: absolute; left: 0; color: var(--cyan); }
.pb b { color: var(--cyan); }

.stk { display: flex; flex-wrap: wrap; gap: 5px; margin-top: 6px; }
.sp {
  font-size: 0.56rem; padding: 2px 8px; border-radius: 20px;
  border: 1px solid rgba(0,255,157,0.2); color: var(--cyan);
  background: rgba(0,255,157,0.05);
  transition: background 0.2s, box-shadow 0.2s;
}
.sp:hover { background: rgba(0,255,157,0.15); box-shadow: 0 0 8px rgba(0,255,157,0.2); }

/* table */
.gtbl { width: 100%; border-collapse: collapse; font-size: 0.66rem; margin-top: 4px; }
.gtbl th { background: rgba(0,255,157,0.06); color: var(--cyan); padding: 9px 12px; text-align: left; border: 1px solid var(--dim); font-size: 0.6rem; letter-spacing: 1px; }
.gtbl td { padding: 9px 12px; border: 1px solid var(--dim); color: var(--text); transition: background 0.2s; }
.gtbl tr:hover td { background: rgba(0,255,157,0.03); }
.gtbl b { color: var(--gold); }

/* cert card */
.ccard {
  background: linear-gradient(135deg, rgba(0,255,157,0.05), rgba(240,192,64,0.04));
  border: 1px solid rgba(240,192,64,0.2); border-radius: 10px; padding: 16px 18px;
  transition: box-shadow 0.3s, border-color 0.3s;
}
.ccard:hover { box-shadow: 0 0 30px rgba(240,192,64,0.12); border-color: rgba(240,192,64,0.4); }
.cname { font-family: 'Orbitron', monospace; font-size: 0.75rem; font-weight: 700; color: var(--gold); margin-bottom: 6px; }
.cmeta { font-size: 0.63rem; color: var(--muted); line-height: 1.8; }
.cmeta .h { color: var(--cyan); }
.cmeta .g { color: var(--gold); }
.cstatus {
  display: inline-flex; align-items: center; gap: 6px;
  margin-top: 8px; font-size: 0.6rem; color: var(--cyan);
  background: rgba(0,255,157,0.06); border: 1px solid rgba(0,255,157,0.2);
  padding: 3px 10px; border-radius: 20px;
}
.ctopics { display: flex; flex-wrap: wrap; gap: 5px; margin-top: 10px; }
.ctag { font-size: 0.57rem; padding: 2px 8px; border-radius: 20px; border: 1px solid var(--dim); color: var(--muted); }

/* stats */
.sgrid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.simg {
  width: 100%; border-radius: 8px; border: 1px solid var(--border); display: block;
  transition: transform 0.2s, box-shadow 0.2s;
}
.simg:hover { transform: scale(1.02); box-shadow: 0 0 20px rgba(0,255,157,0.1); }
.sfull { grid-column: 1 / -1; }

/* interest ascii */
.iascii {
  background: #020a06; border: 1px solid var(--dim); border-radius: 8px;
  padding: 16px 18px; font-size: 0.63rem; color: #2a5040;
  line-height: 1.8; white-space: pre; overflow-x: auto;
  font-family: 'Share Tech Mono', monospace;
}
.iascii .hl { color: var(--cyan); }

/* connect table */
.ctbl { width: 100%; border-collapse: collapse; font-size: 0.66rem; }
.ctbl td { padding: 10px 12px; border: 1px solid var(--dim); color: var(--text); transition: background 0.2s; }
.ctbl tr:hover td { background: rgba(0,255,157,0.03); }
.ctbl a { color: var(--cyan); text-decoration: none; }
.ctbl a:hover { text-decoration: underline; }

/* footer */
.footer {
  background: #020a06; border: 1px solid var(--dim); border-radius: 8px;
  padding: 14px; text-align: center; font-size: 0.6rem; color: var(--muted);
  display: flex; flex-direction: column; gap: 8px; margin-top: 14px;
}
.frow { display: flex; justify-content: center; gap: 18px; flex-wrap: wrap; }
.fi { display: flex; align-items: center; gap: 6px; }
.fq { color: var(--text); font-style: italic; margin-top: 2px; }
.fs { color: var(--muted); }

/* scrollbar */
::-webkit-scrollbar { width: 5px; height: 5px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: rgba(0,255,157,0.2); border-radius: 3px; }
::-webkit-scrollbar-thumb:hover { background: rgba(0,255,157,0.4); }

@media (max-width: 600px) {
  .sgrid { grid-template-columns: 1fr; }
  .sfull { grid-column: 1; }
  .glitch { font-size: 1.4rem; letter-spacing: 3px; }
  .term-body { padding: 16px; }
}
</style>
</head>
<body>

<div id="cur"></div>
<div id="cur2"></div>
<canvas id="mx"></canvas>
<div class="sweep"></div>

<div class="wrap">

<!-- ══════ HERO ══════ -->
<div class="terminal">
  <div class="term-bar">
    <div class="dot r"></div><div class="dot y"></div><div class="dot g"></div>
    <div class="term-title">virajgambhir1215-hub / README.md</div>
  </div>
  <div class="term-body">
    <div class="glitch-wrap">
      <div class="glitch" data-text="VIRAJ GAMBHIR">VIRAJ GAMBHIR</div>
      <div class="subtitle">
        &gt;&nbsp;
        <span style="color:var(--cyan)">Aspiring Cybersecurity Analyst</span>
        &nbsp;·&nbsp;
        <span style="color:var(--gold)">Ethical Hacker</span>
        &nbsp;·&nbsp;
        <span style="color:var(--purple)">Embedded Security Builder</span>
        <span class="blink">_</span>
      </div>
    </div>

    <div class="badges">
      <a class="badge b-li" href="https://www.linkedin.com/in/viraj-gambhir-09b7aa313/" target="_blank">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
      <a class="badge b-gh" href="https://github.com/virajgambhir1215-hub" target="_blank">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.374 0 0 5.373 0 12c0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.509 11.509 0 0112 5.803c1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z"/></svg>
        GitHub
      </a>
      <a class="badge b-gm" href="mailto:virajgambhir1215@gmail.com">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M24 5.457v13.909c0 .904-.732 1.636-1.636 1.636h-3.819V11.73L12 16.64l-6.545-4.91v9.273H1.636A1.636 1.636 0 010 19.366V5.457c0-2.023 2.309-3.178 3.927-1.964L5.455 4.64 12 9.548l6.545-4.91 1.528-1.145C21.69 2.28 24 3.434 24 5.457z"/></svg>
        Email
      </a>
      <a class="badge b-loc" href="#">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/></svg>
        Meerut, India
      </a>
    </div>
    <div style="display:flex;justify-content:center;gap:10px;flex-wrap:wrap;margin-top:4px;">
      <span class="badge b-st"><span class="pdot"></span>&nbsp;Open to Opportunities</span>
      <span class="badge b-st" style="color:var(--muted);">&#128065; Profile Views: Live</span>
    </div>
  </div>
</div>

<!-- ══════ WHOAMI ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">whoami.sh</div></div>
  <div class="term-body">
    <div class="sh">&#128272; whoami</div>
    <div class="wblock">
      <div class="prompt"><span class="u">viraj@kali</span>:<span class="p">~$</span> cat profile.txt</div>
      <div class="plines">
        <div class="pl"><span class="pk">Name &nbsp;&nbsp;&nbsp;&nbsp; :</span><span class="pv">&nbsp;<span class="h">Viraj Gambhir</span></span></div>
        <div class="pl"><span class="pk">Role &nbsp;&nbsp;&nbsp;&nbsp; :</span><span class="pv">&nbsp;Aspiring Cybersecurity Analyst</span></div>
        <div class="pl"><span class="pk">Location &nbsp;:</span><span class="pv">&nbsp;Meerut, Uttar Pradesh, India</span></div>
        <div class="pl"><span class="pk">Education :</span><span class="pv">&nbsp;B.Tech CSE @ <span class="h">Gautam Buddha University</span> (CGPA: <span class="g">8.75</span>)</span></div>
        <div class="pl"><span class="pk">Status &nbsp;&nbsp;&nbsp;:</span><span class="pv">&nbsp;2nd Year Undergraduate | Expected Graduation: 2029</span></div>
        <div class="pl"><span class="pk">Passion &nbsp;&nbsp;:</span><span class="pv">&nbsp;Breaking systems to understand how to defend them</span></div>
      </div>
      <div class="qblock">
        "I chose cybersecurity because I've always been curious about how systems work — and how they can be broken and protected. What excites me most is the constant challenge; new threats keep emerging and there's always something new to learn."
      </div>
    </div>
  </div>
</div>

<!-- ══════ ABOUT ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">about.sh</div></div>
  <div class="term-body">
    <div class="sh">&#9889; About Me</div>
    <div class="alist">
      <div class="al"><span class="ali">&#127891;</span><span>Pursuing <b>B.Tech in Computer Science &amp; Engineering</b> at Gautam Buddha University with a <b>CGPA of 8.75</b></span></div>
      <div class="al"><span class="ali">&#128737;&#65039;</span><span>Certified in <b>Cybersecurity &amp; Ethical Hacking</b> — Coincent Program, in association with <b>E-Cell, IIT Madras</b> (Dec 2025 – Jan 2026)</span></div>
      <div class="al"><span class="ali">&#128301;</span><span>Currently exploring <b>penetration testing</b>, <b>network security</b>, and <b>embedded system security</b></span></div>
      <div class="al"><span class="ali">&#127807;</span><span>Learning <b>vulnerability assessment</b>, <b>SOC operations</b>, and <b>advanced Linux security tools</b></span></div>
      <div class="al"><span class="ali">&#127959;&#65039;</span><span>Building security-aware projects — from <b>hardware access control systems</b> to <b>encrypted P2P messengers</b></span></div>
      <div class="al"><span class="ali">&#127919;</span><span>Goal: Become a skilled <b>Penetration Tester / Cybersecurity Analyst</b> helping organizations stay secure</span></div>
      <div class="al"><span class="ali">&#128172;</span><span>Ask me about <b>Kali Linux</b>, <b>ethical hacking</b>, <b>Arduino security projects</b>, or <b>network protocols</b></span></div>
    </div>
  </div>
</div>

<!-- ══════ SKILLS ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">skills.sh</div></div>
  <div class="term-body">
    <div class="sh">&#128295; Tech Stack &amp; Skills</div>
    <div class="scat">
      <div class="clabel">&#128274; Cybersecurity</div>
      <div class="srow">
        <span class="sk sk-cy">&#129009; Kali Linux</span>
        <span class="sk sk-re">&#128128; Ethical Hacking</span>
        <span class="sk sk-cy">&#127760; Network Security</span>
        <span class="sk sk-pu">&#128273; Cryptography</span>
        <span class="sk sk-re">&#127919; Penetration Testing</span>
      </div>
    </div>
    <div class="scat">
      <div class="clabel">&#128187; Programming Languages</div>
      <div class="srow">
        <span class="sk sk-cy">&#9881;&#65039; C</span>
        <span class="sk sk-go">&#9749; Java</span>
      </div>
    </div>
    <div class="scat">
      <div class="clabel">&#9881;&#65039; Hardware &amp; Embedded</div>
      <div class="srow">
        <span class="sk sk-gr">&#129302; Arduino</span>
        <span class="sk sk-re">&#128225; ESP32</span>
        <span class="sk sk-cy">&#128179; RFID RC522</span>
      </div>
    </div>
    <div class="scat">
      <div class="clabel">&#129520; Tools &amp; Platforms</div>
      <div class="srow">
        <span class="sk sk-gr">&#128025; GitHub</span>
        <span class="sk sk-go">&#128039; Linux</span>
        <span class="sk sk-cy">&#128153; VS Code</span>
        <span class="sk sk-pu">&#128296; Arduino IDE</span>
      </div>
    </div>
  </div>
</div>

<!-- ══════ PROJECTS ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">projects.sh</div></div>
  <div class="term-body">
    <div class="sh">&#128640; Featured Projects</div>

    <div class="pcard">
      <div class="ptitle">&#128123; Ghost Chat — Secure P2P Messenger</div>
      <div class="ptag">// Network Security · Encrypted Communication · ESP32</div>
      <div class="pline">Offline. Anonymous. Untraceable.</div>
      <div class="ascii"><span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>
<span class="hl">&#9474;</span>  Device A (ESP32)  &lt;&#9472;&#9472;&#9472;&#9472; <span class="hl">Local Wi-Fi</span> &#9472;&#9472;&#9472;&#9472;&gt;  Device B (ESP32)  <span class="hl">&#9474;</span>
<span class="hl">&#9474;</span>        |                   No Server                    |       <span class="hl">&#9474;</span>
<span class="hl">&#9474;</span>  <span class="hl">Kali Linux Dev</span>    &lt;&#9472;&#9472; Adversarial Test &#9472;&#9472;&gt;   Secure Comms    <span class="hl">&#9474;</span>
<span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span></div>
      <div class="pdesc">A <b>covert peer-to-peer chat application</b> built on ESP32 microcontrollers — anonymous, infrastructure-independent communication over local Wi-Fi. No internet. No servers. No trace.</div>
      <div class="pbullets">
        <div class="pb">&#128274; Zero external server dependency — eliminates third-party interception risk</div>
        <div class="pb">&#128225; Device-to-device communication via Wi-Fi protocols</div>
        <div class="pb">&#128039; Developed &amp; tested on <b>Kali Linux</b> to simulate adversarial network conditions</div>
        <div class="pb">&#127917; Designed with anonymity and reduced attack surface as core principles</div>
      </div>
      <div class="stk">
        <span class="sp">ESP32</span><span class="sp">Java</span><span class="sp">Kali Linux</span><span class="sp">Wi-Fi Protocols</span><span class="sp">P2P Networking</span>
      </div>
    </div>

    <div class="pcard">
      <div class="ptitle">&#128225; RFID Smart Attendance System</div>
      <div class="ptag">// Hardware Security · Embedded Systems · Access Control</div>
      <div class="pline">Hardware security meets access control.</div>
      <div class="ascii"><span class="hl">  [RFID Card]</span> &#9472;&#9472;&gt; <span class="hl">[RC522 Module]</span> &#9472;&#9472;&gt; <span class="hl">[Arduino Uno]</span> &#9472;&#9472;&gt; [Access Log]
       &#8593;                                       |
  Unique Tag ID                         <span class="hl">C-based Auth</span>
  Verification                          Logic Engine</div>
      <div class="pdesc">An <b>automated attendance management system</b> using RFID technology — contactless, tamper-resistant card authentication replacing manual processes entirely.</div>
      <div class="pbullets">
        <div class="pb">&#128272; Unique RFID tag-based identity verification</div>
        <div class="pb">&#128683; Tamper-resistant access logging for authorized users only</div>
        <div class="pb">&#9889; Optimized read latency through efficient <b>C architecture</b></div>
        <div class="pb">&#128737;&#65039; Demonstrates real-world <b>physical security</b> and <b>access control</b> principles</div>
      </div>
      <div class="stk">
        <span class="sp">Arduino Uno</span><span class="sp">RFID RC522</span><span class="sp">C</span><span class="sp">Arduino IDE</span><span class="sp">Embedded Systems</span>
      </div>
    </div>
  </div>
</div>

<!-- ══════ EDUCATION ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">education.sh</div></div>
  <div class="term-body">
    <div class="sh">&#127891; Education</div>
    <table class="gtbl">
      <tr><th>Degree</th><th>Institution</th><th>CGPA</th><th>Year</th></tr>
      <tr><td>B.Tech — Computer Science &amp; Engineering</td><td>Gautam Buddha University, Greater Noida</td><td><b>8.75 / 10</b></td><td>2025 – 2029 (Expected)</td></tr>
    </table>
    <div style="margin-top:12px;font-size:0.63rem;color:var(--muted);">
      <span style="color:var(--cyan)">Relevant Coursework:</span>&nbsp; Cryptography · Network Security · Data Structures · Operating Systems · DBMS
    </div>
  </div>
</div>

<!-- ══════ CERTIFICATIONS ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">certifications.sh</div></div>
  <div class="term-body">
    <div class="sh">&#128220; Certifications</div>
    <div class="ccard">
      <div class="cname">&#128737;&#65039; Cyber Security &amp; Ethical Hacking — Phase 1</div>
      <div class="cmeta">
        Issued by: <span class="h">Coincent</span>&nbsp; · &nbsp;In association with: <span class="g">E-Cell, IIT Madras</span><br>
        Duration: Dec 2025 – Jan 2026 &nbsp;·&nbsp; Issued: 06 Feb 2026
      </div>
      <div class="cstatus"><span class="pdot"></span>&nbsp;Verified &amp; Active</div>
      <div class="ctopics">
        <span class="ctag">Penetration Testing Methodology</span>
        <span class="ctag">Vulnerability Identification</span>
        <span class="ctag">Security Assessment Fundamentals</span>
        <span class="ctag">Ethical Hacking Principles</span>
      </div>
    </div>
  </div>
</div>

<!-- ══════ GITHUB STATS ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">github-stats.sh</div></div>
  <div class="term-body">
    <div class="sh">&#128202; GitHub Stats</div>
    <div class="sgrid">
      <img class="simg" src="https://github-readme-stats.vercel.app/api?username=virajgambhir1215-hub&show_icons=true&theme=chartreuse-dark&hide_border=true&bg_color=020a06&title_color=00ff9d&icon_color=00ff9d&text_color=b0ffd0" alt="GitHub Stats" loading="lazy"/>
      <img class="simg" src="https://github-readme-stats.vercel.app/api/top-langs/?username=virajgambhir1215-hub&layout=compact&theme=chartreuse-dark&hide_border=true&bg_color=020a06&title_color=00ff9d&text_color=b0ffd0" alt="Top Languages" loading="lazy"/>
      <img class="simg sfull" src="https://streak-stats.demolab.com/?user=virajgambhir1215-hub&theme=chartreuse-dark&hide_border=true&background=020a06&stroke=00ff9d&ring=00ff9d&fire=f0c040&currStreakLabel=00ff9d" alt="GitHub Streak" loading="lazy"/>
    </div>
  </div>
</div>

<!-- ══════ INTERESTS ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">interests.sh</div></div>
  <div class="term-body">
    <div class="sh">&#127919; Areas of Interest</div>
    <div class="iascii"><span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>  <span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>  <span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>
<span class="hl">&#9474;</span> Penetration      <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Vulnerability       <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Network          <span class="hl">&#9474;</span>
<span class="hl">&#9474;</span> Testing          <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Assessment          <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Security         <span class="hl">&#9474;</span>
<span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span>  <span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span>  <span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span>
<span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>  <span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>  <span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>
<span class="hl">&#9474;</span> Ethical          <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Cryptography        <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Embedded         <span class="hl">&#9474;</span>
<span class="hl">&#9474;</span> Hacking          <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span>                     <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Security         <span class="hl">&#9474;</span>
<span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span>  <span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span>  <span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span>
<span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>  <span class="hl">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;</span>
<span class="hl">&#9474;</span> SOC              <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Secure System       <span class="hl">&#9474;</span>
<span class="hl">&#9474;</span> Operations       <span class="hl">&#9474;</span>  <span class="hl">&#9474;</span> Design              <span class="hl">&#9474;</span>
<span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span>  <span class="hl">&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</span></div>
  </div>
</div>

<!-- ══════ CONNECT ══════ -->
<div class="terminal">
  <div class="term-bar"><div class="dot r"></div><div class="dot y"></div><div class="dot g"></div><div class="term-title">connect.sh</div></div>
  <div class="term-body">
    <div class="sh">&#129309; Connect With Me</div>
    <table class="ctbl">
      <tr><td>&#128188; LinkedIn</td><td><a href="https://www.linkedin.com/in/viraj-gambhir-09b7aa313/" target="_blank">viraj-gambhir-09b7aa313</a></td></tr>
      <tr><td>&#128025; GitHub</td><td><a href="https://github.com/virajgambhir1215-hub" target="_blank">virajgambhir1215-hub</a></td></tr>
      <tr><td>&#128231; Email</td><td><a href="mailto:virajgambhir1215@gmail.com">virajgambhir1215@gmail.com</a></td></tr>
      <tr><td>&#128205; Location</td><td>Meerut, Uttar Pradesh, India</td></tr>
    </table>

    <div class="footer">
      <div class="frow">
        <div class="fi" style="color:var(--cyan)"><span class="pdot"></span>&nbsp;SYSTEM: ONLINE</div>
        <div class="fi" style="color:var(--gold)">&#9888; THREAT LEVEL: LEARNING</div>
        <div class="fi" style="color:var(--purple)">&#11041; MODE: BUILDER</div>
      </div>
      <div class="fq">"The quieter you become, the more you can hear." — Kali Linux</div>
      <div class="fs">&#11088; If you find my work interesting, consider starring a repository!</div>
    </div>
  </div>
</div>

</div><!-- /wrap -->

<script>
// CURSOR
const cur = document.getElementById('cur');
const cur2 = document.getElementById('cur2');
let mx = 0, my = 0, tx = 0, ty = 0;
document.addEventListener('mousemove', function(e) {
  mx = e.clientX; my = e.clientY;
  cur.style.left = mx + 'px';
  cur.style.top  = my + 'px';
});
setInterval(function() {
  tx += (mx - tx) * 0.1;
  ty += (my - ty) * 0.1;
  cur2.style.left = tx + 'px';
  cur2.style.top  = ty + 'px';
}, 12);

// MATRIX RAIN
(function() {
  var c = document.getElementById('mx');
  var ctx = c.getContext('2d');
  var W, H, cols, drops;
  function resize() {
    W = c.width  = window.innerWidth;
    H = c.height = window.innerHeight;
    cols = Math.floor(W / 16);
    drops = [];
    for (var i = 0; i < cols; i++) drops[i] = Math.random() * -60;
  }
  resize();
  window.addEventListener('resize', resize);
  var chars = 'ABCDEF0123456789!@#$%&<>{}[]|/\\'.split('');
  function draw() {
    ctx.fillStyle = 'rgba(2,6,8,0.06)';
    ctx.fillRect(0, 0, W, H);
    for (var i = 0; i < drops.length; i++) {
      var bright = Math.random() > 0.97;
      ctx.fillStyle = bright ? '#ffffff' : (Math.random() > 0.8 ? '#00ff9d' : '#006030');
      ctx.font = (bright ? 'bold ' : '') + '13px Share Tech Mono,monospace';
      var ch = chars[Math.floor(Math.random() * chars.length)];
      ctx.fillText(ch, i * 16, drops[i] * 16);
      if (drops[i] * 16 > H && Math.random() > 0.975) drops[i] = 0;
      drops[i] += 0.5;
    }
  }
  setInterval(draw, 55);
})();

// SCROLL REVEAL
(function() {
  var els = document.querySelectorAll('.terminal');
  var io = new IntersectionObserver(function(entries) {
    entries.forEach(function(e, i) {
      if (e.isIntersecting) {
        setTimeout(function() { e.target.classList.add('vis'); }, i * 80);
        io.unobserve(e.target);
      }
    });
  }, { threshold: 0.08 });
  els.forEach(function(el) { io.observe(el); });
})();

// TERMINAL TITLE RETYPE ON HOVER
document.querySelectorAll('.terminal').forEach(function(term) {
  var title = term.querySelector('.term-title');
  var orig = title.textContent;
  term.addEventListener('mouseenter', function() {
    var i = 0;
    title.textContent = '';
    var iv = setInterval(function() {
      title.textContent = orig.slice(0, ++i);
      if (i >= orig.length) clearInterval(iv);
    }, 25);
  });
});

// RANDOM GLITCH RETRIGGER
setInterval(function() {
  var g = document.querySelector('.glitch');
  if (g) { g.style.animation = 'none'; void g.offsetWidth; g.style.animation = ''; }
}, 7000);
</script>
</body>
</html>
