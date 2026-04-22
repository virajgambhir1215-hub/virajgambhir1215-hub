<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>virajgambhir1215-hub / README</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Rajdhani:wght@400;600;700&display=swap" rel="stylesheet"/>
<style>
:root{
  --bg:#020608;--bg2:#050d0f;--bg3:#071015;
  --cyan:#00ff9d;--cyan2:#00ccff;--cyan3:rgba(0,255,157,.12);
  --gold:#f0c040;--green:#00ff9d;--red:#ff2255;--purple:#bf5fff;
  --text:#b0ffd0;--muted:#3a6050;--dim:#1a3028;
  --border:rgba(0,255,157,.12);
  --glow:0 0 20px rgba(0,255,157,.3),0 0 60px rgba(0,255,157,.1);
  --font-mono:'Share Tech Mono',monospace;
  --font-display:'Orbitron',monospace;
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}

/* CURSOR */
*{cursor:none!important;}
#cur{position:fixed;width:10px;height:10px;background:var(--cyan);border-radius:50%;pointer-events:none;z-index:99999;transform:translate(-50%,-50%);box-shadow:0 0 10px var(--cyan),0 0 30px rgba(0,255,157,.4);transition:width .1s,height .1s;}
#cur2{position:fixed;width:28px;height:28px;border:1px solid rgba(0,255,157,.4);border-radius:50%;pointer-events:none;z-index:99998;transform:translate(-50%,-50%);transition:all .1s linear;}

body{
  font-family:var(--font-mono);
  background:var(--bg);
  color:var(--text);
  min-height:100vh;
  overflow-x:hidden;
  line-height:1.7;
}

/* SCANLINES */
body::before{content:'';position:fixed;inset:0;z-index:0;pointer-events:none;
  background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,.05) 2px,rgba(0,0,0,.05) 4px);}

/* MATRIX BG */
#mx{position:fixed;inset:0;z-index:0;pointer-events:none;opacity:.055;}

/* GLOW SWEEP */
.sweep{position:fixed;top:-4px;left:0;right:0;height:3px;z-index:2;pointer-events:none;
  background:linear-gradient(90deg,transparent,var(--cyan),transparent);
  box-shadow:0 0 20px var(--cyan),0 0 50px rgba(0,255,157,.3);
  animation:swp 8s linear infinite;}
@keyframes swp{0%{top:-4px;}100%{top:100vh;}}

/* WRAPPER */
.wrap{max-width:900px;margin:0 auto;padding:40px 24px 80px;position:relative;z-index:3;}

/* ─── TERMINAL WINDOW ─── */
.terminal{
  background:var(--bg2);
  border:1px solid var(--border);
  border-radius:10px;
  overflow:hidden;
  box-shadow:0 0 0 1px var(--border),0 0 60px rgba(0,255,157,.05),0 30px 80px rgba(0,0,0,.7);
  margin-bottom:24px;
}
.term-bar{
  background:#0a1a14;
  padding:10px 16px;
  display:flex;align-items:center;gap:8px;
  border-bottom:1px solid var(--border);
}
.tdot{width:11px;height:11px;border-radius:50%;}
.tdot.r{background:#ff5f56;box-shadow:0 0 6px #ff5f56;}
.tdot.y{background:#ffbd2e;box-shadow:0 0 6px #ffbd2e;}
.tdot.g{background:#27c93f;box-shadow:0 0 6px #27c93f;}
.term-title{margin-left:auto;margin-right:auto;font-size:.65rem;color:var(--muted);letter-spacing:2px;}
.term-body{padding:24px 28px;}

/* ─── GLITCH TITLE ─── */
.glitch-wrap{text-align:center;padding:10px 0 20px;position:relative;}
.glitch{
  font-family:var(--font-display);
  font-size:clamp(1.4rem,5vw,2.8rem);
  font-weight:900;
  color:var(--cyan);
  letter-spacing:6px;
  text-shadow:var(--glow);
  position:relative;display:inline-block;
  animation:glitch1 5s infinite 4s;
}
.glitch::before,.glitch::after{
  content:attr(data-text);
  position:absolute;inset:0;
  font-family:var(--font-display);font-size:inherit;font-weight:inherit;letter-spacing:inherit;
}
.glitch::before{color:var(--red);animation:gb 5s infinite 4s;clip-path:polygon(0 20%,100% 20%,100% 40%,0 40%);}
.glitch::after{color:#00ccff;animation:ga 5s infinite 4.05s;clip-path:polygon(0 60%,100% 60%,100% 80%,0 80%);}
@keyframes glitch1{0%,86%,100%{transform:none;}87%{transform:translate(-2px,0);}89%{transform:translate(2px,0);}91%{transform:none;}}
@keyframes gb{0%,86%,100%{transform:none;opacity:0;}87%{transform:translate(-3px,0);opacity:1;}89%{transform:translate(3px,0);}91%{opacity:0;}}
@keyframes ga{0%,86%,100%{transform:none;opacity:0;}88%{transform:translate(3px,0);opacity:1;}90%{transform:translate(-3px,0);}91%{opacity:0;}}

.subtitle{
  font-size:.7rem;color:var(--muted);letter-spacing:2px;
  margin-top:10px;text-align:center;
}
.subtitle span{color:var(--cyan);animation:blink 1.4s step-end infinite;}
@keyframes blink{50%{opacity:0;}}

/* ─── BADGES ─── */
.badges{display:flex;flex-wrap:wrap;justify-content:center;gap:8px;padding:18px 0 10px;}
.badge{
  display:inline-flex;align-items:center;gap:7px;
  padding:6px 14px;border-radius:5px;font-size:.62rem;letter-spacing:.5px;
  text-decoration:none;border:1px solid;
  transition:transform .2s,box-shadow .2s;
  position:relative;overflow:hidden;
}
.badge::before{content:'';position:absolute;inset:0;background:linear-gradient(90deg,transparent,rgba(255,255,255,.05),transparent);transform:translateX(-100%);transition:transform .4s;}
.badge:hover::before{transform:translateX(100%);}
.badge:hover{transform:translateY(-2px);}
.badge.li{background:rgba(0,119,181,.15);border-color:rgba(0,119,181,.4);color:#4fbaff;}
.badge.li:hover{box-shadow:0 4px 20px rgba(0,119,181,.3);}
.badge.gh{background:rgba(255,255,255,.05);border-color:rgba(255,255,255,.15);color:#ccc;}
.badge.gh:hover{box-shadow:0 4px 20px rgba(255,255,255,.1);}
.badge.gm{background:rgba(209,72,54,.15);border-color:rgba(209,72,54,.3);color:#ff7060;}
.badge.gm:hover{box-shadow:0 4px 20px rgba(209,72,54,.2);}
.badge.loc{background:rgba(0,255,157,.06);border-color:rgba(0,255,157,.2);color:var(--cyan);}
.badge.loc:hover{box-shadow:0 4px 20px rgba(0,255,157,.15);}
.badge.st{background:rgba(0,255,157,.06);border-color:rgba(0,255,157,.2);color:var(--cyan);font-size:.58rem;}

.badge svg{width:14px;height:14px;flex-shrink:0;}

/* PULSE STATUS */
.pulse-dot{width:7px;height:7px;border-radius:50%;background:var(--green);display:inline-block;box-shadow:0 0 8px var(--green);animation:pdot 2s ease-in-out infinite;margin-right:4px;}
@keyframes pdot{0%,100%{opacity:1;box-shadow:0 0 8px var(--green);}50%{opacity:.5;box-shadow:0 0 20px var(--green),0 0 40px rgba(0,255,157,.3);}}

/* ─── DIVIDER ─── */
.div{height:1px;background:linear-gradient(90deg,transparent,var(--border),var(--cyan),var(--border),transparent);margin:28px 0;position:relative;}
.div::after{content:'◆';position:absolute;left:50%;transform:translateX(-50%) translateY(-50%);background:var(--bg2);padding:0 10px;color:var(--muted);font-size:.6rem;}

/* ─── SECTION HEADING ─── */
.sh{
  font-family:var(--font-display);font-size:.85rem;font-weight:700;
  color:var(--cyan);letter-spacing:3px;text-transform:uppercase;
  margin-bottom:18px;display:flex;align-items:center;gap:12px;
}
.sh::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,var(--border),transparent);}
.sh-icon{font-size:1rem;}

/* ─── WHOAMI BLOCK ─── */
.whoami-block{
  background:rgba(0,255,157,.03);
  border:1px solid var(--border);border-radius:8px;padding:20px 22px;
  position:relative;overflow:hidden;
}
.whoami-block::before{content:'';position:absolute;left:0;top:0;bottom:0;width:2px;background:linear-gradient(180deg,var(--cyan),transparent);}
.prompt{font-size:.65rem;color:var(--muted);margin-bottom:8px;}
.prompt span{color:var(--cyan);}
.profile-lines{display:flex;flex-direction:column;gap:4px;}
.pl{font-size:.7rem;color:var(--text);display:flex;gap:0;}
.pk{color:var(--muted);min-width:80px;}
.pv{color:#fff;}
.pv .h{color:var(--cyan);}
.pv .g{color:var(--green);}
.quote-block{
  border-left:2px solid var(--cyan);padding:10px 16px;margin-top:16px;
  background:rgba(0,255,157,.03);border-radius:0 6px 6px 0;
  font-size:.7rem;color:var(--muted);font-style:italic;line-height:1.8;
}

/* ─── ABOUT LIST ─── */
.about-list{display:flex;flex-direction:column;gap:10px;}
.al{
  display:flex;align-items:flex-start;gap:10px;
  font-size:.72rem;color:var(--text);line-height:1.7;
  padding:8px 14px;border-radius:6px;border:1px solid transparent;
  transition:background .25s,border-color .25s,transform .25s;
}
.al:hover{background:rgba(0,255,157,.04);border-color:var(--border);transform:translateX(4px);}
.al-icon{font-size:.9rem;flex-shrink:0;margin-top:1px;}
.al b{color:var(--cyan);}

/* ─── SKILL BADGES ─── */
.skill-cat{margin-bottom:18px;}
.cat-label{font-size:.6rem;color:var(--muted);letter-spacing:2px;text-transform:uppercase;margin-bottom:10px;display:flex;align-items:center;gap:6px;}
.cat-label::after{content:'';flex:1;height:1px;background:var(--dim);}
.skill-row{display:flex;flex-wrap:wrap;gap:8px;}
.skbadge{
  padding:6px 14px;border-radius:5px;font-size:.6rem;letter-spacing:.5px;
  border:1px solid;display:flex;align-items:center;gap:6px;
  transition:transform .2s,box-shadow .2s;cursor:default;
}
.skbadge:hover{transform:translateY(-2px);}
.skbadge.cy{background:rgba(0,212,255,.07);border-color:rgba(0,212,255,.25);color:#00d4ff;}
.skbadge.cy:hover{box-shadow:0 4px 15px rgba(0,212,255,.2);}
.skbadge.re{background:rgba(255,34,85,.07);border-color:rgba(255,34,85,.25);color:#ff5577;}
.skbadge.re:hover{box-shadow:0 4px 15px rgba(255,34,85,.2);}
.skbadge.go{background:rgba(240,192,64,.07);border-color:rgba(240,192,64,.25);color:var(--gold);}
.skbadge.go:hover{box-shadow:0 4px 15px rgba(240,192,64,.2);}
.skbadge.gr{background:rgba(0,255,157,.07);border-color:rgba(0,255,157,.2);color:var(--cyan);}
.skbadge.gr:hover{box-shadow:0 4px 15px rgba(0,255,157,.15);}
.skbadge.pu{background:rgba(191,95,255,.07);border-color:rgba(191,95,255,.25);color:var(--purple);}
.skbadge.pu:hover{box-shadow:0 4px 15px rgba(191,95,255,.2);}

/* ─── PROJECT CARD ─── */
.proj-card{
  background:var(--bg3);border:1px solid var(--border);border-radius:10px;
  padding:20px 22px;margin-bottom:16px;position:relative;overflow:hidden;
  transition:border-color .3s,box-shadow .3s,transform .3s;
}
.proj-card:hover{border-color:rgba(0,255,157,.35);box-shadow:0 0 40px rgba(0,255,157,.06),0 10px 40px rgba(0,0,0,.5);transform:translateY(-3px);}
.proj-card::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:linear-gradient(180deg,var(--cyan),transparent);}
.proj-card::after{content:'';position:absolute;top:0;left:-100%;width:40%;height:100%;background:linear-gradient(90deg,transparent,rgba(0,255,157,.03),transparent);transition:left .7s;pointer-events:none;}
.proj-card:hover::after{left:200%;}
.proj-title{font-family:var(--font-display);font-size:.85rem;font-weight:700;color:#fff;letter-spacing:1px;margin-bottom:4px;}
.proj-tag{font-size:.6rem;color:var(--cyan);margin-bottom:12px;letter-spacing:1px;}
.proj-tagline{font-size:.65rem;color:var(--muted);font-style:italic;margin-bottom:14px;padding:6px 10px;border-left:2px solid var(--muted);background:rgba(255,255,255,.02);}

/* ASCII diagram */
.ascii{
  background:#020a06;border:1px solid var(--dim);border-radius:6px;
  padding:14px 16px;margin-bottom:14px;
  font-size:.6rem;color:var(--muted);line-height:1.6;
  overflow-x:auto;white-space:pre;
}
.ascii .hl{color:var(--cyan);}

.proj-desc{font-size:.7rem;color:var(--text);line-height:1.8;margin-bottom:12px;}
.proj-desc b{color:var(--cyan);}

.proj-bullets{display:flex;flex-direction:column;gap:6px;margin-bottom:14px;}
.pb{font-size:.68rem;color:var(--text);padding-left:14px;position:relative;line-height:1.6;}
.pb::before{content:'▸';position:absolute;left:0;color:var(--cyan);}
.pb b{color:var(--cyan);}

.stk{display:flex;flex-wrap:wrap;gap:5px;margin-top:4px;}
.sp{font-size:.57rem;padding:2px 9px;border-radius:20px;border:1px solid rgba(0,255,157,.2);color:var(--cyan);background:rgba(0,255,157,.05);transition:background .2s,box-shadow .2s;}
.sp:hover{background:rgba(0,255,157,.15);box-shadow:0 0 8px rgba(0,255,157,.25);}

/* ─── TABLE ─── */
.gtable{width:100%;border-collapse:collapse;font-size:.68rem;margin-top:4px;}
.gtable th{background:rgba(0,255,157,.06);color:var(--cyan);padding:9px 14px;text-align:left;border:1px solid var(--dim);letter-spacing:1px;font-size:.62rem;}
.gtable td{padding:9px 14px;border:1px solid var(--dim);color:var(--text);transition:background .2s;}
.gtable tr:hover td{background:rgba(0,255,157,.03);}
.gtable b{color:var(--gold);}

/* ─── CERT CARD ─── */
.cert-card{
  background:linear-gradient(135deg,rgba(0,255,157,.05),rgba(240,192,64,.04));
  border:1px solid rgba(240,192,64,.2);border-radius:10px;padding:18px 20px;
  transition:box-shadow .3s,border-color .3s;position:relative;overflow:hidden;
}
.cert-card:hover{box-shadow:0 0 30px rgba(240,192,64,.12);border-color:rgba(240,192,64,.4);}
.cert-name{font-family:var(--font-display);font-size:.78rem;font-weight:700;color:var(--gold);margin-bottom:6px;}
.cert-meta{font-size:.65rem;color:var(--muted);line-height:1.8;}
.cert-status{display:inline-flex;align-items:center;gap:6px;margin-top:8px;font-size:.62rem;color:var(--green);background:rgba(0,255,157,.06);border:1px solid rgba(0,255,157,.2);padding:3px 10px;border-radius:20px;}
.cert-topics{display:flex;flex-wrap:wrap;gap:5px;margin-top:10px;}
.ctag{font-size:.58rem;padding:2px 8px;border-radius:20px;border:1px solid var(--dim);color:var(--muted);background:rgba(0,0,0,.3);}

/* ─── STATS SECTION ─── */
.stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.stat-img{width:100%;border-radius:8px;border:1px solid var(--border);transition:transform .2s,box-shadow .2s;display:block;}
.stat-img:hover{transform:scale(1.02);box-shadow:0 0 20px rgba(0,255,157,.1);}
.stat-full{grid-column:1/-1;}

/* ─── INTEREST GRID ─── */
.int-ascii{
  background:#020a06;border:1px solid var(--dim);border-radius:8px;
  padding:18px 20px;font-size:.65rem;color:var(--muted);line-height:1.8;
  white-space:pre;overflow-x:auto;
}
.int-ascii .hl{color:var(--cyan);}

/* ─── CONNECT TABLE ─── */
.ctable{width:100%;border-collapse:collapse;font-size:.68rem;}
.ctable td{padding:10px 14px;border:1px solid var(--dim);transition:background .2s;}
.ctable tr:hover td{background:rgba(0,255,157,.03);}
.ctable a{color:var(--cyan);text-decoration:none;}
.ctable a:hover{text-decoration:underline;}

/* ─── FOOTER ─── */
.footer{
  background:#020a06;border:1px solid var(--dim);border-radius:8px;
  padding:16px;text-align:center;
  font-size:.62rem;color:var(--muted);
  display:flex;flex-direction:column;gap:8px;
  margin-top:4px;
}
.footer-status{display:flex;justify-content:center;gap:20px;flex-wrap:wrap;}
.fs-item{display:flex;align-items:center;gap:6px;color:var(--muted);}
.fs-item.active{color:var(--cyan);}
.footer-quote{color:var(--text);font-style:italic;margin-top:4px;}
.footer-star{color:var(--muted);}

/* ─── TYPEWRITER ─── */
.typewriter{overflow:hidden;white-space:nowrap;border-right:2px solid var(--cyan);width:0;animation:tw 2s steps(40) var(--tw-delay,3s) forwards,curb .8s step-end var(--tw-delay,3s) 3;}
@keyframes tw{to{width:100%;}}
@keyframes curb{50%{border-color:transparent;}}

/* ─── REVEAL ─── */
.reveal{opacity:0;transform:translateY(24px);transition:opacity .7s ease,transform .7s ease;}
.reveal.vis{opacity:1;transform:none;}

/* ─── SCROLLBAR ─── */
::-webkit-scrollbar{width:6px;height:6px;}
::-webkit-scrollbar-track{background:#020608;}
::-webkit-scrollbar-thumb{background:rgba(0,255,157,.2);border-radius:3px;}
::-webkit-scrollbar-thumb:hover{background:rgba(0,255,157,.4);}

@media(max-width:600px){
  .stats-grid{grid-template-columns:1fr;}
  .stat-full{grid-column:1;}
  .glitch{font-size:1.4rem;}
  .badges{gap:6px;}
  .badge{font-size:.55rem;padding:5px 10px;}
}
</style>
</head>
<body>
<div id="cur"></div><div id="cur2"></div>
<canvas id="mx"></canvas>
<div class="sweep"></div>

<div class="wrap">

  <!-- ══ HERO TERMINAL ══ -->
  <div class="terminal reveal" style="--tw-delay:0s">
    <div class="term-bar">
      <div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div>
      <div class="term-title">virajgambhir1215-hub / README.md — bash</div>
    </div>
    <div class="term-body">
      <div class="glitch-wrap">
        <div class="glitch" data-text="VIRAJ GAMBHIR">VIRAJ GAMBHIR</div>
        <div class="subtitle">&gt; <span style="color:var(--cyan)">Aspiring Cybersecurity Analyst</span> · <span style="color:var(--gold)">Ethical Hacker</span> · <span style="color:var(--purple)">Embedded Security Builder</span><span style="animation:blink 1.2s step-end infinite">_</span></div>
      </div>

      <div class="badges">
        <a class="badge li" href="https://www.linkedin.com/in/viraj-gambhir-09b7aa313/" target="_blank">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
          LinkedIn
        </a>
        <a class="badge gh" href="https://github.com/virajgambhir1215-hub" target="_blank">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.374 0 0 5.373 0 12c0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.509 11.509 0 0112 5.803c1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z"/></svg>
          GitHub
        </a>
        <a class="badge gm" href="mailto:virajgambhir1215@gmail.com">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M24 5.457v13.909c0 .904-.732 1.636-1.636 1.636h-3.819V11.73L12 16.64l-6.545-4.91v9.273H1.636A1.636 1.636 0 010 19.366V5.457c0-2.023 2.309-3.178 3.927-1.964L5.455 4.64 12 9.548l6.545-4.910 1.528-1.145C21.69 2.28 24 3.434 24 5.457z"/></svg>
          Email
        </a>
        <a class="badge loc" href="#">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/></svg>
          Meerut, India
        </a>
      </div>
      <div style="display:flex;justify-content:center;gap:10px;flex-wrap:wrap;margin-top:6px;">
        <span class="badge st"><span class="pulse-dot"></span>Open to Opportunities</span>
        <span class="badge st" style="color:var(--muted)">👁 Profile Views: Live</span>
      </div>
    </div>
  </div>

  <!-- ══ WHOAMI ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">whoami.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">🔐</span> whoami</div>
      <div class="whoami-block">
        <div class="prompt"><span style="color:var(--green)">viraj@kali</span><span style="color:var(--muted)">:~$</span> <span style="color:#fff">cat profile.txt</span></div>
        <div class="profile-lines">
          <div class="pl"><span class="pk">Name     :</span><span class="pv"> <span class="h">Viraj Gambhir</span></span></div>
          <div class="pl"><span class="pk">Role     :</span><span class="pv"> Aspiring Cybersecurity Analyst</span></div>
          <div class="pl"><span class="pk">Location :</span><span class="pv"> Meerut, Uttar Pradesh, India</span></div>
          <div class="pl"><span class="pk">Education:</span><span class="pv"> B.Tech CSE @ <span class="h">Gautam Buddha University</span> (CGPA: <span class="g">8.75</span>)</span></div>
          <div class="pl"><span class="pk">Status   :</span><span class="pv"> 2nd Year Undergraduate | Expected Graduation: 2029</span></div>
          <div class="pl"><span class="pk">Passion  :</span><span class="pv"> Breaking systems to understand how to defend them</span></div>
        </div>
        <div class="quote-block">
          "I chose cybersecurity because I've always been curious about how systems work — and how they can be broken and protected. What excites me most is the constant challenge; new threats keep emerging and there's always something new to learn."
        </div>
      </div>
    </div>
  </div>

  <!-- ══ ABOUT ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">about.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">⚡</span> About Me</div>
      <div class="about-list">
        <div class="al"><span class="al-icon">🎓</span><span>Pursuing <b>B.Tech in Computer Science & Engineering</b> at Gautam Buddha University with a <b>CGPA of 8.75</b></span></div>
        <div class="al"><span class="al-icon">🛡️</span><span>Certified in <b>Cybersecurity & Ethical Hacking</b> — Coincent Program, in association with <b>E-Cell, IIT Madras</b> (Dec 2025 – Jan 2026)</span></div>
        <div class="al"><span class="al-icon">🔭</span><span>Currently exploring <b>penetration testing</b>, <b>network security</b>, and <b>embedded system security</b></span></div>
        <div class="al"><span class="al-icon">🌱</span><span>Learning <b>vulnerability assessment</b>, <b>SOC operations</b>, and <b>advanced Linux security tools</b></span></div>
        <div class="al"><span class="al-icon">🏗️</span><span>I build security-aware projects — from <b>hardware access control systems</b> to <b>encrypted P2P messengers</b></span></div>
        <div class="al"><span class="al-icon">🎯</span><span>Goal: Become a skilled <b>Penetration Tester / Cybersecurity Analyst</b> helping organizations stay secure</span></div>
        <div class="al"><span class="al-icon">💬</span><span>Ask me about <b>Kali Linux</b>, <b>ethical hacking</b>, <b>Arduino security projects</b>, or <b>network protocols</b></span></div>
      </div>
    </div>
  </div>

  <!-- ══ SKILLS ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">skills.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">🛠️</span> Tech Stack & Skills</div>
      <div class="skill-cat">
        <div class="cat-label">🔒 Cybersecurity</div>
        <div class="skill-row">
          <span class="skbadge cy">🐉 Kali Linux</span>
          <span class="skbadge re">💀 Ethical Hacking</span>
          <span class="skbadge cy">🌐 Network Security</span>
          <span class="skbadge pu">🔑 Cryptography</span>
          <span class="skbadge re">🎯 Penetration Testing</span>
        </div>
      </div>
      <div class="skill-cat">
        <div class="cat-label">💻 Programming Languages</div>
        <div class="skill-row">
          <span class="skbadge cy">⚙️ C</span>
          <span class="skbadge go">☕ Java</span>
        </div>
      </div>
      <div class="skill-cat">
        <div class="cat-label">⚙️ Hardware & Embedded</div>
        <div class="skill-row">
          <span class="skbadge gr">🤖 Arduino</span>
          <span class="skbadge re">📡 ESP32</span>
          <span class="skbadge cy">💳 RFID RC522</span>
        </div>
      </div>
      <div class="skill-cat">
        <div class="cat-label">🧰 Tools & Platforms</div>
        <div class="skill-row">
          <span class="skbadge gr">🐙 GitHub</span>
          <span class="skbadge go">🐧 Linux</span>
          <span class="skbadge cy">💙 VS Code</span>
          <span class="skbadge pu">🔧 Arduino IDE</span>
        </div>
      </div>
    </div>
  </div>

  <!-- ══ PROJECTS ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">projects.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">🚀</span> Featured Projects</div>

      <div class="proj-card">
        <div class="proj-title">👻 Ghost Chat — Secure P2P Messenger</div>
        <div class="proj-tag">// Network Security · Encrypted Communication · ESP32</div>
        <div class="proj-tagline">Offline. Anonymous. Untraceable.</div>
        <div class="ascii"><span class="hl">┌──────────────────────────────────────────────────────────────┐</span>
<span class="hl">│</span>  Device A (ESP32)  ◄──── <span class="hl">Local Wi-Fi</span> ────►  Device B (ESP32)  <span class="hl">│</span>
<span class="hl">│</span>        │                   No Server                    │       <span class="hl">│</span>
<span class="hl">│</span>  <span class="hl">Kali Linux Dev</span>    ◄── Adversarial Test ──►   Secure Comms    <span class="hl">│</span>
<span class="hl">└──────────────────────────────────────────────────────────────┘</span></div>
        <div class="proj-desc">A <b>covert peer-to-peer chat application</b> built on ESP32 microcontrollers — anonymous, infrastructure-independent communication over local Wi-Fi networks. No internet. No servers. No trace.</div>
        <div class="proj-bullets">
          <div class="pb">🔒 Zero external server dependency — eliminates third-party interception risk</div>
          <div class="pb">📡 Device-to-device communication via Wi-Fi protocols</div>
          <div class="pb">🐧 Developed & tested on <b>Kali Linux</b> to simulate adversarial network conditions</div>
          <div class="pb">🎭 Designed with anonymity and reduced attack surface as core principles</div>
        </div>
        <div class="stk"><span class="sp">ESP32</span><span class="sp">Java</span><span class="sp">Kali Linux</span><span class="sp">Wi-Fi Protocols</span><span class="sp">P2P Networking</span></div>
      </div>

      <div class="proj-card">
        <div class="proj-title">📡 RFID Smart Attendance System</div>
        <div class="proj-tag">// Hardware Security · Embedded Systems · Access Control</div>
        <div class="proj-tagline">Hardware security meets access control.</div>
        <div class="ascii"><span class="hl">  [RFID Card]</span> ──► <span class="hl">[RC522 Module]</span> ──► <span class="hl">[Arduino Uno]</span> ──► [Access Log]
       ↑                                       │
  Unique Tag ID                         <span class="hl">C-based Auth</span>
  Verification                          Logic Engine</div>
        <div class="proj-desc">An <b>automated attendance management system</b> using RFID technology — contactless, tamper-resistant card authentication that replaces manual processes entirely.</div>
        <div class="proj-bullets">
          <div class="pb">🔐 Unique RFID tag-based identity verification</div>
          <div class="pb">🚫 Tamper-resistant access logging for authorized users only</div>
          <div class="pb">⚡ Optimized read latency through efficient <b>C architecture</b></div>
          <div class="pb">🛡️ Demonstrates real-world <b>physical security</b> and <b>access control</b> principles</div>
        </div>
        <div class="stk"><span class="sp">Arduino Uno</span><span class="sp">RFID RC522</span><span class="sp">C</span><span class="sp">Arduino IDE</span><span class="sp">Embedded Systems</span></div>
      </div>
    </div>
  </div>

  <!-- ══ EDUCATION ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">education.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">🎓</span> Education</div>
      <table class="gtable">
        <tr><th>Degree</th><th>Institution</th><th>CGPA</th><th>Year</th></tr>
        <tr><td>B.Tech — Computer Science & Engineering</td><td>Gautam Buddha University, Greater Noida</td><td><b>8.75 / 10</b></td><td>2025 – 2029 (Expected)</td></tr>
      </table>
      <div style="margin-top:12px;font-size:.65rem;color:var(--muted);">
        <span style="color:var(--cyan)">Relevant Coursework:</span> Cryptography · Network Security · Data Structures · Operating Systems · DBMS
      </div>
    </div>
  </div>

  <!-- ══ CERTIFICATIONS ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">certifications.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">📜</span> Certifications</div>
      <div class="cert-card">
        <div class="cert-name">🛡️ Cyber Security & Ethical Hacking — Phase 1</div>
        <div class="cert-meta">
          Issued by: <span style="color:var(--cyan)">Coincent</span> · In association with: <span style="color:var(--gold)">E-Cell, IIT Madras</span><br>
          Duration: Dec 2025 – Jan 2026 &nbsp;·&nbsp; Issued: 06 Feb 2026
        </div>
        <div class="cert-status"><span class="pulse-dot"></span> Verified & Active</div>
        <div class="cert-topics">
          <span class="ctag">Penetration Testing Methodology</span>
          <span class="ctag">Vulnerability Identification</span>
          <span class="ctag">Security Assessment Fundamentals</span>
          <span class="ctag">Ethical Hacking Principles</span>
        </div>
      </div>
    </div>
  </div>

  <!-- ══ GITHUB STATS ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">github-stats.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">📊</span> GitHub Stats</div>
      <div class="stats-grid">
        <img class="stat-img" src="https://github-readme-stats.vercel.app/api?username=virajgambhir1215-hub&show_icons=true&theme=chartreuse-dark&hide_border=true&bg_color=020a06&title_color=00ff9d&icon_color=00ff9d&text_color=b0ffd0" alt="GitHub Stats" loading="lazy"/>
        <img class="stat-img" src="https://github-readme-stats.vercel.app/api/top-langs/?username=virajgambhir1215-hub&layout=compact&theme=chartreuse-dark&hide_border=true&bg_color=020a06&title_color=00ff9d&text_color=b0ffd0" alt="Top Languages" loading="lazy"/>
        <img class="stat-img stat-full" src="https://streak-stats.demolab.com/?user=virajgambhir1215-hub&theme=chartreuse-dark&hide_border=true&background=020a06&stroke=00ff9d&ring=00ff9d&fire=f0c040&currStreakLabel=00ff9d" alt="GitHub Streak" loading="lazy"/>
      </div>
    </div>
  </div>

  <!-- ══ INTERESTS ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">interests.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">🎯</span> Areas of Interest</div>
      <div class="int-ascii"><span class="hl">┌──────────────────┐</span>  <span class="hl">┌────────────────────┐</span>  <span class="hl">┌──────────────────┐</span>
<span class="hl">│</span> Penetration      <span class="hl">│</span>  <span class="hl">│</span> Vulnerability       <span class="hl">│</span>  <span class="hl">│</span> Network          <span class="hl">│</span>
<span class="hl">│</span> Testing          <span class="hl">│</span>  <span class="hl">│</span> Assessment          <span class="hl">│</span>  <span class="hl">│</span> Security         <span class="hl">│</span>
<span class="hl">└──────────────────┘</span>  <span class="hl">└────────────────────┘</span>  <span class="hl">└──────────────────┘</span>
<span class="hl">┌──────────────────┐</span>  <span class="hl">┌────────────────────┐</span>  <span class="hl">┌──────────────────┐</span>
<span class="hl">│</span> Ethical          <span class="hl">│</span>  <span class="hl">│</span> Cryptography        <span class="hl">│</span>  <span class="hl">│</span> Embedded         <span class="hl">│</span>
<span class="hl">│</span> Hacking          <span class="hl">│</span>  <span class="hl">│</span>                     <span class="hl">│</span>  <span class="hl">│</span> Security         <span class="hl">│</span>
<span class="hl">└──────────────────┘</span>  <span class="hl">└────────────────────┘</span>  <span class="hl">└──────────────────┘</span>
<span class="hl">┌──────────────────┐</span>  <span class="hl">┌────────────────────┐</span>
<span class="hl">│</span> SOC              <span class="hl">│</span>  <span class="hl">│</span> Secure System       <span class="hl">│</span>
<span class="hl">│</span> Operations       <span class="hl">│</span>  <span class="hl">│</span> Design              <span class="hl">│</span>
<span class="hl">└──────────────────┘</span>  <span class="hl">└────────────────────┘</span></div>
    </div>
  </div>

  <!-- ══ CONNECT ══ -->
  <div class="terminal reveal">
    <div class="term-bar"><div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div><div class="term-title">connect.sh</div></div>
    <div class="term-body">
      <div class="sh"><span class="sh-icon">🤝</span> Connect With Me</div>
      <table class="ctable">
        <tr><td>💼 LinkedIn</td><td><a href="https://www.linkedin.com/in/viraj-gambhir-09b7aa313/" target="_blank">viraj-gambhir-09b7aa313</a></td></tr>
        <tr><td>🐙 GitHub</td><td><a href="https://github.com/virajgambhir1215-hub" target="_blank">virajgambhir1215-hub</a></td></tr>
        <tr><td>📧 Email</td><td><a href="mailto:virajgambhir1215@gmail.com">virajgambhir1215@gmail.com</a></td></tr>
        <tr><td>📍 Location</td><td>Meerut, Uttar Pradesh, India</td></tr>
      </table>

      <div class="footer" style="margin-top:16px;">
        <div class="footer-status">
          <div class="fs-item active"><span class="pulse-dot"></span> SYSTEM: ONLINE</div>
          <div class="fs-item" style="color:var(--gold);">⚠ THREAT LEVEL: LEARNING</div>
          <div class="fs-item" style="color:var(--purple);">⬡ MODE: BUILDER</div>
        </div>
        <div class="footer-quote">"The quieter you become, the more you can hear." — Kali Linux</div>
        <div class="footer-star">⭐ If you find my work interesting, consider starring a repository!</div>
      </div>
    </div>
  </div>

</div><!-- /wrap -->

<script>
/* CURSOR */
const cur=document.getElementById('cur'),cur2=document.getElementById('cur2');
let mx=0,my=0,t2x=0,t2y=0;
document.addEventListener('mousemove',e=>{
  mx=e.clientX;my=e.clientY;
  cur.style.left=mx+'px';cur.style.top=my+'px';
});
setInterval(()=>{
  t2x+=(mx-t2x)*.1;t2y+=(my-t2y)*.1;
  cur2.style.left=t2x+'px';cur2.style.top=t2y+'px';
},12);

/* MATRIX */
(function(){
  const c=document.getElementById('mx'),ctx=c.getContext('2d');
  let W,H,cols,drops;
  function resize(){W=c.width=window.innerWidth;H=c.height=window.innerHeight;cols=Math.floor(W/16);drops=Array.from({length:cols},()=>Math.random()*-60);}
  resize();window.addEventListener('resize',resize);
  const chars='ABCDEF0123456789!@#$%^&*<>{}[]|/\\アイウエオ'.split('');
  function draw(){
    ctx.fillStyle='rgba(2,6,8,.06)';ctx.fillRect(0,0,W,H);
    drops.forEach((y,i)=>{
      const bright=Math.random()>.97;
      ctx.fillStyle=bright?'#ffffff':Math.random()>.8?'#00ff9d':'#007040';
      ctx.font=(bright?'bold ':'')+'13px Share Tech Mono,monospace';
      ctx.fillText(chars[Math.floor(Math.random()*chars.length)],i*16,y*16);
      if(y*16>H&&Math.random()>.975)drops[i]=0;
      drops[i]+=.5;
    });
  }
  setInterval(draw,55);
})();

/* REVEAL */
(function(){
  const els=document.querySelectorAll('.reveal');
  const io=new IntersectionObserver(entries=>{
    entries.forEach((e,i)=>{
      if(e.isIntersecting){
        setTimeout(()=>e.target.classList.add('vis'),i*80);
        io.unobserve(e.target);
      }
    });
  },{threshold:.08});
  els.forEach(el=>io.observe(el));
})();

/* TYPEWRITER for terminal titles — subtle re-type on hover */
document.querySelectorAll('.term-title').forEach(el=>{
  const orig=el.textContent;
  el.closest('.terminal').addEventListener('mouseenter',()=>{
    let i=0;el.textContent='';
    const iv=setInterval(()=>{
      el.textContent=orig.slice(0,++i);
      if(i>=orig.length)clearInterval(iv);
    },28);
  });
});

/* GLITCH random trigger */
setInterval(()=>{
  const g=document.querySelector('.glitch');
  if(g){g.style.animation='none';void g.offsetWidth;g.style.animation='';}
},7000);
</script>
</body>
</html>
