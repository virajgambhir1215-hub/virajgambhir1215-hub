<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Viraj Gambhir // Cybersecurity Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@300;400;500;600;700&family=Share+Tech+Mono&family=Orbitron:wght@400;500;700;900&display=swap" rel="stylesheet"/>
<style>
:root {
  --bg:        #04080f;
  --bg2:       #060d18;
  --bg3:       #081020;
  --cyan:      #00d4ff;
  --cyan2:     #00a8cc;
  --cyan3:     rgba(0,212,255,0.15);
  --gold:      #e8c46a;
  --gold2:     rgba(232,196,106,0.15);
  --green:     #00ff88;
  --red:       #ff2255;
  --purple:    #7b2fff;
  --text:      #cdd6e8;
  --muted:     #4a6080;
  --border:    rgba(0,212,255,0.12);
  --sidebar-w: 260px;
  --glow-c:    0 0 20px rgba(0,212,255,0.4),0 0 60px rgba(0,212,255,0.15);
  --glow-g:    0 0 20px rgba(232,196,106,0.4),0 0 60px rgba(232,196,106,0.15);
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}

/* ── CURSOR ── */
*{cursor:none!important;}
#cursor{position:fixed;width:12px;height:12px;border:2px solid var(--cyan);border-radius:50%;pointer-events:none;z-index:99999;transform:translate(-50%,-50%);transition:width .15s,height .15s,border-color .15s;mix-blend-mode:screen;}
#cursor-trail{position:fixed;width:30px;height:30px;border:1px solid rgba(0,212,255,0.3);border-radius:50%;pointer-events:none;z-index:99998;transform:translate(-50%,-50%);transition:all .08s linear;mix-blend-mode:screen;}
body:has(.card:hover) #cursor{width:20px;height:20px;border-color:var(--gold);}

body{
  font-family:'Share Tech Mono',monospace;
  background:var(--bg);
  color:var(--text);
  min-height:100vh;
  overflow-x:hidden;
}

/* ══ BOOT SCREEN ══ */
#boot{
  position:fixed;inset:0;background:#000;z-index:9999;
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:16px;
  font-family:'Share Tech Mono',monospace;
}
#boot.out{animation:bootOut .8s ease forwards;}
@keyframes bootOut{to{opacity:0;filter:blur(8px);pointer-events:none;}}

.boot-hex{
  width:100px;height:100px;
  position:relative;display:flex;align-items:center;justify-content:center;
}
.boot-hex svg{position:absolute;inset:0;animation:hexSpin 3s linear infinite;}
.boot-hex-text{font-family:'Orbitron',monospace;font-size:1.4rem;font-weight:900;color:var(--cyan);
  text-shadow:var(--glow-c);animation:hexPulse 1s ease-in-out infinite;}
@keyframes hexSpin{to{transform:rotate(360deg);}}
@keyframes hexPulse{0%,100%{opacity:.7;}50%{opacity:1;}}

.boot-status{font-size:.65rem;color:var(--cyan);letter-spacing:3px;text-transform:uppercase;}
.boot-log{width:420px;display:flex;flex-direction:column;gap:5px;}
.blog{font-size:.65rem;opacity:0;transition:opacity .1s;}
.blog.on{opacity:1;}
.blog .ok{color:var(--green);}
.blog .warn{color:var(--gold);}
.blog .err{color:var(--red);}

.boot-progress-wrap{width:420px;position:relative;}
.boot-progress-track{height:2px;background:rgba(0,212,255,.1);border-radius:1px;overflow:hidden;}
.boot-progress-bar{height:100%;width:0%;background:linear-gradient(90deg,var(--cyan2),var(--cyan),#fff);
  box-shadow:0 0 12px var(--cyan);animation:bprog 2.2s ease .6s forwards;}
@keyframes bprog{to{width:100%;}}
.boot-progress-pct{position:absolute;right:0;top:-18px;font-size:.6rem;color:var(--cyan);}

/* ══ PARTICLE CANVAS ══ */
#particle-canvas{position:fixed;inset:0;z-index:0;pointer-events:none;opacity:.6;}

/* ══ HEX GRID BG ══ */
.hex-bg{
  position:fixed;inset:0;z-index:0;pointer-events:none;
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='56' height='100'%3E%3Cpath d='M28 66L0 50V18L28 2l28 16v32L28 66z' fill='none' stroke='rgba(0,212,255,0.04)' stroke-width='1'/%3E%3C/svg%3E");
  background-size:56px 100px;
  animation:hexDrift 20s linear infinite;
}
@keyframes hexDrift{0%{background-position:0 0;}100%{background-position:56px 100px;}}

/* ══ SCAN LINES ══ */
.scanlines{
  position:fixed;inset:0;z-index:1;pointer-events:none;
  background:repeating-linear-gradient(0deg,transparent,transparent 3px,rgba(0,0,0,.04) 3px,rgba(0,0,0,.04) 4px);
}
.scan-sweep{
  position:fixed;top:0;left:0;right:0;height:3px;z-index:2;pointer-events:none;
  background:linear-gradient(90deg,transparent,rgba(0,212,255,.6),transparent);
  animation:sweep 6s linear infinite;
  box-shadow:0 0 20px var(--cyan),0 0 60px rgba(0,212,255,.3);
}
@keyframes sweep{0%{top:-3px;}100%{top:100vh;}}

/* ══ NOISE OVERLAY ══ */
.noise{
  position:fixed;inset:0;z-index:1;pointer-events:none;opacity:.025;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}

/* ══ PAGE ══ */
.page{
  width:210mm;min-height:297mm;margin:40px auto;
  display:flex;position:relative;z-index:3;
  box-shadow:0 0 0 1px var(--border),0 0 80px rgba(0,212,255,.08),0 40px 120px rgba(0,0,0,.8);
  background:var(--bg);
  overflow:hidden;
}

/* corner brackets */
.page::before,.page::after{content:'';position:absolute;width:24px;height:24px;z-index:10;}
.page::before{top:8px;left:8px;border-top:2px solid var(--cyan);border-left:2px solid var(--cyan);opacity:.6;}
.page::after{top:8px;right:8px;border-top:2px solid var(--cyan);border-right:2px solid var(--cyan);opacity:.6;}

/* animated top accent bar */
.top-bar{position:absolute;top:0;left:0;right:0;height:2px;z-index:10;overflow:hidden;}
.top-bar::before{
  content:'';position:absolute;top:0;left:-100%;width:100%;height:100%;
  background:linear-gradient(90deg,transparent,var(--cyan),var(--gold),var(--cyan),transparent);
  animation:topScan 3s ease 3s forwards;
}
@keyframes topScan{0%{left:-100%;}100%{left:100%;}}
.top-bar::after{
  content:'';position:absolute;top:0;left:0;right:0;height:100%;
  background:linear-gradient(90deg,transparent 0%,rgba(0,212,255,.3) 50%,transparent 100%);
  animation:topGlow 4s ease-in-out 4s infinite;
}
@keyframes topGlow{0%,100%{opacity:0;}50%{opacity:1;}}

/* ══ SIDEBAR ══ */
.sidebar{
  width:var(--sidebar-w);min-width:var(--sidebar-w);
  background:var(--bg2);
  border-right:1px solid var(--border);
  padding:32px 18px;
  display:flex;flex-direction:column;gap:24px;
  position:relative;overflow:hidden;
}

/* circuit trace lines on sidebar */
.sidebar::before{
  content:'';position:absolute;inset:0;pointer-events:none;
  background:
    linear-gradient(180deg,transparent 20%,rgba(0,212,255,.03) 20%,rgba(0,212,255,.03) 20.5%,transparent 20.5%),
    linear-gradient(180deg,transparent 55%,rgba(0,212,255,.03) 55%,rgba(0,212,255,.03) 55.5%,transparent 55.5%),
    linear-gradient(90deg,transparent 40%,rgba(0,212,255,.03) 40%,rgba(0,212,255,.03) 40.5%,transparent 40.5%);
}

/* dot grid */
.sidebar::after{
  content:'';position:absolute;inset:0;pointer-events:none;
  background-image:radial-gradient(rgba(0,212,255,.05) 1px,transparent 1px);
  background-size:16px 16px;
  animation:dotBreath 5s ease-in-out infinite;
}
@keyframes dotBreath{0%,100%{opacity:.4;}50%{opacity:1;}}

/* ── AVATAR ── */
.av-wrap{display:flex;flex-direction:column;align-items:center;gap:14px;position:relative;z-index:1;}

.av-outer{
  position:relative;width:110px;height:110px;
  display:flex;align-items:center;justify-content:center;
}
.av-ring1,.av-ring2,.av-ring3{
  position:absolute;border-radius:50%;border:1px solid;
}
.av-ring1{inset:-4px;border-color:rgba(0,212,255,.5);animation:ringR1 4s linear infinite;}
.av-ring2{inset:-12px;border-color:rgba(0,212,255,.2);animation:ringR2 7s linear infinite reverse;}
.av-ring3{inset:-22px;border-color:rgba(0,212,255,.08);animation:ringR3 12s linear infinite;}
@keyframes ringR1{to{transform:rotate(360deg);}}
@keyframes ringR2{to{transform:rotate(360deg);}}
@keyframes ringR3{to{transform:rotate(360deg);}}

/* ring dots */
.av-ring1::before,.av-ring2::before{
  content:'';position:absolute;top:-4px;left:50%;transform:translateX(-50%);
  width:6px;height:6px;border-radius:50%;background:var(--cyan);
  box-shadow:0 0 8px var(--cyan);
}
.av-ring2::before{top:-3px;width:4px;height:4px;background:var(--gold);}

.av{
  width:90px;height:90px;border-radius:50%;
  background:linear-gradient(135deg,#051525,#0a2540);
  border:2px solid var(--cyan);
  box-shadow:0 0 30px rgba(0,212,255,.3),inset 0 0 30px rgba(0,212,255,.05);
  display:flex;align-items:center;justify-content:center;
  font-family:'Orbitron',monospace;font-size:1.6rem;font-weight:900;
  color:var(--cyan);letter-spacing:2px;
  animation:avGlow 3s ease-in-out infinite;
  transition:transform .3s;position:relative;z-index:1;
}
.av:hover{transform:scale(1.08);}
@keyframes avGlow{
  0%,100%{box-shadow:0 0 30px rgba(0,212,255,.3),inset 0 0 30px rgba(0,212,255,.05);}
  50%{box-shadow:0 0 50px rgba(0,212,255,.5),inset 0 0 50px rgba(0,212,255,.1);}
}

.av-name{
  font-family:'Orbitron',monospace;font-size:.75rem;font-weight:700;
  color:#fff;text-align:center;letter-spacing:2px;
  text-shadow:0 0 20px rgba(0,212,255,.5);
  position:relative;z-index:1;
}
.av-tag{
  font-size:.55rem;color:var(--cyan);letter-spacing:2.5px;
  text-transform:uppercase;border:1px solid rgba(0,212,255,.3);
  padding:3px 10px;border-radius:20px;
  background:rgba(0,212,255,.06);
  animation:tagPulse 3s ease-in-out infinite;
  position:relative;z-index:1;
}
@keyframes tagPulse{0%,100%{box-shadow:none;}50%{box-shadow:0 0 12px rgba(0,212,255,.3);}}

/* ── S-SECTIONS ── */
.ss{display:flex;flex-direction:column;gap:10px;position:relative;z-index:1;}
.st{
  font-family:'Orbitron',monospace;font-size:.55rem;font-weight:700;
  letter-spacing:3px;text-transform:uppercase;color:var(--cyan);
  padding-bottom:7px;border-bottom:1px solid var(--border);
  position:relative;overflow:hidden;
}
.st::after{
  content:'';position:absolute;bottom:0;left:-100%;width:100%;height:1px;
  background:linear-gradient(90deg,transparent,var(--cyan),transparent);
  box-shadow:0 0 8px var(--cyan);
  animation:stScan 4s ease-in-out infinite;
}
@keyframes stScan{0%{left:-100%;}50%{left:0%;}100%{left:100%;}}

/* contact */
.ci{display:flex;flex-direction:column;gap:2px;}
.cl{font-size:.52rem;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px;}
.cv{font-size:.62rem;color:var(--text);word-break:break-all;}
.cv a{color:var(--cyan);text-decoration:none;transition:color .2s,text-shadow .2s;}
.cv a:hover{color:#fff;text-shadow:0 0 10px var(--cyan);}

/* skill bars */
.ski{display:flex;flex-direction:column;gap:5px;}
.skr{display:flex;justify-content:space-between;align-items:center;}
.skn{font-size:.62rem;color:var(--text);}
.skp{font-size:.55rem;color:var(--cyan);}
.skbar{height:3px;background:rgba(255,255,255,.05);border-radius:2px;overflow:hidden;position:relative;}
.skfill{
  height:100%;border-radius:2px;width:0%;
  background:linear-gradient(90deg,var(--cyan2),var(--cyan),rgba(255,255,255,.8));
  box-shadow:0 0 8px rgba(0,212,255,.6);
  transition:width 1.6s cubic-bezier(.16,1,.3,1);
  position:relative;
}
.skfill::after{
  content:'';position:absolute;right:0;top:-2px;width:4px;height:7px;border-radius:2px;
  background:#fff;box-shadow:0 0 6px var(--cyan);
  opacity:0;transition:opacity .3s;
}
.ski:hover .skfill::after{opacity:1;}

/* tags */
.tg-group{display:flex;flex-wrap:wrap;gap:5px;}
.tg{
  font-size:.55rem;padding:3px 8px;border-radius:20px;
  border:1px solid var(--border);color:var(--muted);
  background:rgba(0,212,255,.04);letter-spacing:.5px;
  transition:all .25s;
}
.tg:hover{background:rgba(0,212,255,.15);color:var(--cyan);border-color:var(--cyan);box-shadow:0 0 10px rgba(0,212,255,.2);}

/* cert card */
.cert{
  background:linear-gradient(135deg,rgba(0,212,255,.07),rgba(232,196,106,.05));
  border:1px solid rgba(232,196,106,.2);
  border-radius:6px;padding:10px 12px;
  transition:box-shadow .3s,border-color .3s;position:relative;overflow:hidden;
}
.cert::before{
  content:'';position:absolute;top:0;left:-100%;width:50%;height:100%;
  background:linear-gradient(90deg,transparent,rgba(232,196,106,.06),transparent);
  transition:left .6s;
}
.cert:hover::before{left:200%;}
.cert:hover{box-shadow:0 0 25px rgba(232,196,106,.2);border-color:var(--gold);}
.cert-name{font-size:.65rem;font-weight:700;color:var(--gold);line-height:1.5;}
.cert-sub{font-size:.58rem;color:var(--muted);margin-top:3px;}
.cert-badge{font-size:.58rem;color:var(--green);margin-top:4px;display:flex;align-items:center;gap:4px;}
.cert-badge::before{content:'';width:6px;height:6px;border-radius:50%;background:var(--green);box-shadow:0 0 6px var(--green);display:inline-block;animation:statusPulse 2s infinite;}

/* ══ MAIN ══ */
.main{
  flex:1;padding:32px 28px 32px 26px;
  display:flex;flex-direction:column;gap:24px;
  overflow:hidden;position:relative;
}

/* ── HEADER ── */
.hdr{padding-bottom:20px;border-bottom:1px solid var(--border);position:relative;}

.hdr-name{
  font-family:'Orbitron',monospace;
  font-size:2rem;font-weight:900;letter-spacing:4px;
  line-height:1;color:#fff;
  position:relative;display:inline-block;
}
.hdr-name .acc{color:var(--cyan);text-shadow:0 0 30px rgba(0,212,255,.6);}
.hdr-name::after{
  content:attr(data-text);
  position:absolute;inset:0;
  color:var(--red);
  clip-path:polygon(0 0,100% 0,100% 0,0 0);
  animation:nameGlitch 6s infinite 4s;
}
@keyframes nameGlitch{
  0%,88%,100%{clip-path:polygon(0 0,100% 0,100% 0,0 0);transform:translate(0);}
  89%{clip-path:polygon(0 25%,100% 25%,100% 40%,0 40%);transform:translate(-3px,0);filter:hue-rotate(90deg);}
  91%{clip-path:polygon(0 60%,100% 60%,100% 75%,0 75%);transform:translate(3px,0);}
  93%{clip-path:polygon(0 0,100% 0,100% 0,0 0);transform:translate(0);}
}

.hdr-role{
  font-family:'Share Tech Mono',monospace;
  font-size:.68rem;color:var(--cyan);letter-spacing:3px;text-transform:uppercase;
  margin-top:7px;
  overflow:hidden;white-space:nowrap;width:0;border-right:2px solid var(--cyan);
  animation:tw 2s steps(55) 3.2s forwards, curBlink .8s step-end 3.2s 4;
}
@keyframes tw{to{width:100%;}}
@keyframes curBlink{50%{border-color:transparent;}}

.hdr-quote{
  font-size:.7rem;color:var(--muted);font-style:italic;
  margin-top:9px;line-height:1.6;
  opacity:0;animation:fadeSlide .6s ease 5.2s forwards;
  border-left:2px solid var(--cyan);padding-left:10px;
}
@keyframes fadeSlide{to{opacity:1;transform:none;}}

/* status pills */
.status-row{display:flex;gap:10px;margin-top:12px;flex-wrap:wrap;}
.spill{
  display:flex;align-items:center;gap:6px;
  font-size:.58rem;padding:4px 10px;border-radius:20px;
  border:1px solid;
}
.spill.green{border-color:rgba(0,255,136,.3);color:var(--green);background:rgba(0,255,136,.05);}
.spill.cyan{border-color:var(--border);color:var(--cyan);background:rgba(0,212,255,.05);}
.spill.gold{border-color:rgba(232,196,106,.3);color:var(--gold);background:rgba(232,196,106,.05);}
.sdot{width:6px;height:6px;border-radius:50%;}
.sdot.g{background:var(--green);box-shadow:0 0 6px var(--green);animation:statusPulse 2s infinite;}
.sdot.c{background:var(--cyan);box-shadow:0 0 6px var(--cyan);animation:statusPulse 2.5s infinite .5s;}
.sdot.o{background:var(--gold);box-shadow:0 0 6px var(--gold);animation:statusPulse 3s infinite 1s;}
@keyframes statusPulse{0%,100%{opacity:1;}50%{opacity:.4;}}

/* ── SECTION ── */
.sec{display:flex;flex-direction:column;gap:12px;}
.sec-title{
  font-family:'Orbitron',monospace;font-size:.6rem;font-weight:700;
  letter-spacing:4px;text-transform:uppercase;color:var(--cyan);
  display:flex;align-items:center;gap:10px;
}
.sec-title::before{content:'//';opacity:.5;font-size:.7rem;}
.sec-title::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,var(--border),transparent);}

/* summary */
.sum{
  font-size:.72rem;line-height:1.85;color:var(--text);
  border-left:2px solid var(--cyan);padding:14px 16px;
  border-radius:0 8px 8px 0;
  background:linear-gradient(135deg,rgba(0,212,255,.04),transparent);
  position:relative;overflow:hidden;
  transition:background .3s;
}
.sum:hover{background:linear-gradient(135deg,rgba(0,212,255,.07),transparent);}
.sum::before{
  content:'';position:absolute;top:-100%;left:0;right:0;height:100%;
  background:linear-gradient(180deg,transparent,rgba(0,212,255,.04),transparent);
  animation:sumShimmer 5s ease-in-out infinite 5s;
}
@keyframes sumShimmer{0%,100%{top:-100%;}50%{top:100%;}}

/* ── CARDS ── */
.card{
  background:var(--bg2);border:1px solid var(--border);
  border-radius:10px;padding:15px 17px;
  position:relative;overflow:hidden;
  transition:border-color .3s,box-shadow .3s,transform .3s;
}
.card:hover{
  border-color:rgba(0,212,255,.4);
  box-shadow:0 0 40px rgba(0,212,255,.08),0 10px 40px rgba(0,0,0,.5);
  transform:translateY(-3px);
}
/* left accent bar */
.card::before{
  content:'';position:absolute;left:0;top:0;bottom:0;width:3px;
  background:linear-gradient(180deg,var(--cyan),var(--cyan2),transparent);
  transition:box-shadow .3s;
}
.card:hover::before{box-shadow:0 0 15px var(--cyan);}
/* shimmer sweep */
.card::after{
  content:'';position:absolute;top:0;left:-100%;width:40%;height:100%;
  background:linear-gradient(90deg,transparent,rgba(0,212,255,.04),transparent);
  transition:left .8s ease;pointer-events:none;
}
.card:hover::after{left:200%;}
/* corner bracket */
.card-corner{position:absolute;top:8px;right:8px;width:14px;height:14px;
  border-top:1.5px solid rgba(0,212,255,.3);border-right:1.5px solid rgba(0,212,255,.3);}

.ch{display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:4px;}
.ct{font-family:'Orbitron',monospace;font-size:.78rem;font-weight:700;color:#fff;letter-spacing:.5px;}
.cs{font-size:.65rem;color:var(--cyan);font-weight:600;margin-top:2px;}
.cd{
  font-size:.58rem;color:var(--muted);white-space:nowrap;
  padding:2px 8px;border:1px solid var(--border);border-radius:20px;
  transition:color .2s,border-color .2s;
}
.card:hover .cd{color:var(--cyan);border-color:rgba(0,212,255,.35);}

.card ul{margin-top:9px;padding-left:0;list-style:none;display:flex;flex-direction:column;gap:5px;}
.card ul li{font-size:.68rem;color:var(--text);line-height:1.65;padding-left:16px;position:relative;}
.card ul li::before{content:'▸';position:absolute;left:0;color:var(--cyan);font-size:.6rem;}

.stk{display:flex;flex-wrap:wrap;gap:4px;margin-top:9px;}
.sp{
  font-size:.55rem;padding:2px 8px;border-radius:20px;
  border:1px solid rgba(0,212,255,.2);color:var(--cyan);
  background:rgba(0,212,255,.05);
  transition:background .2s,box-shadow .2s;
}
.sp:hover{background:rgba(0,212,255,.18);box-shadow:0 0 8px rgba(0,212,255,.25);}

/* ── EDU CARD ── */
.edu{
  background:var(--bg2);border:1px solid var(--border);
  border-radius:10px;padding:15px 17px;
  display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:12px;
  position:relative;overflow:hidden;
  transition:border-color .3s,box-shadow .3s,transform .3s;
}
.edu:hover{border-color:rgba(232,196,106,.35);box-shadow:0 0 35px rgba(232,196,106,.07);transform:translateY(-3px);}
.edu::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:linear-gradient(180deg,var(--gold),#c49a3a,transparent);}
.edu::after{content:'';position:absolute;top:0;left:-100%;width:40%;height:100%;background:linear-gradient(90deg,transparent,rgba(232,196,106,.04),transparent);transition:left .8s;pointer-events:none;}
.edu:hover::after{left:200%;}

.ed{font-family:'Orbitron',monospace;font-size:.8rem;font-weight:700;color:#fff;}
.eu{font-size:.68rem;color:var(--cyan);margin-top:3px;}
.ec{font-size:.6rem;color:var(--muted);margin-top:4px;}
.em{text-align:right;}
.cgpa{font-family:'Orbitron',monospace;font-size:1.3rem;font-weight:900;color:var(--gold);
  text-shadow:0 0 20px rgba(232,196,106,.5);animation:cgpaPulse 3s ease-in-out infinite;}
@keyframes cgpaPulse{0%,100%{text-shadow:0 0 10px rgba(232,196,106,.3);}50%{text-shadow:0 0 25px rgba(232,196,106,.7),0 0 50px rgba(232,196,106,.3);}}
.cgpalabel{font-size:.52rem;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px;}
.ey{font-size:.58rem;color:var(--muted);margin-top:4px;}

/* ── RADAR CHART SECTION ── */
.radar-wrap{display:flex;align-items:center;gap:20px;flex-wrap:wrap;}
#radarCanvas{flex-shrink:0;}
.radar-legend{display:flex;flex-direction:column;gap:7px;flex:1;}
.rl-item{display:flex;align-items:center;gap:8px;font-size:.62rem;color:var(--text);}
.rl-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.rl-bar-wrap{flex:1;height:3px;background:rgba(255,255,255,.06);border-radius:2px;overflow:hidden;}
.rl-bar{height:100%;border-radius:2px;width:0%;transition:width 1.8s cubic-bezier(.16,1,.3,1);}

/* ── INTEREST TAGS (large) ── */
.int-grid{display:flex;flex-wrap:wrap;gap:8px;}
.itag{
  font-size:.62rem;padding:6px 14px;border-radius:6px;
  border:1px solid var(--border);color:var(--muted);
  background:rgba(0,212,255,.03);
  transition:all .3s;position:relative;overflow:hidden;
}
.itag::before{
  content:'';position:absolute;inset:0;
  background:linear-gradient(135deg,rgba(0,212,255,.1),transparent);
  opacity:0;transition:opacity .3s;
}
.itag:hover::before{opacity:1;}
.itag:hover{border-color:rgba(0,212,255,.4);color:var(--cyan);transform:translateY(-2px);box-shadow:0 4px 20px rgba(0,212,255,.12);}

/* ── REVEAL ── */
.reveal{opacity:0;transform:translateY(28px);transition:opacity .8s ease,transform .8s ease;}
.reveal.vis{opacity:1;transform:none;}

/* ── PRINT ── */
@media print{
  body{background:var(--bg);-webkit-print-color-adjust:exact;print-color-adjust:exact;}
  .page{margin:0;box-shadow:none;width:100%;}
  #boot,#particle-canvas,.scan-sweep,.hex-bg,.scanlines,.noise,#cursor,#cursor-trail{display:none!important;}
  .reveal{opacity:1;transform:none;}
  .hdr-role{width:100%;animation:none;border:none;}
}
@media screen and (max-width:760px){
  .page{width:100%;flex-direction:column;margin:0;}
  .sidebar{width:100%;min-width:unset;}
  .hdr-role{animation:none;width:100%;border:none;}
}
</style>
</head>
<body>

<!-- CURSOR -->
<div id="cursor"></div>
<div id="cursor-trail"></div>

<!-- BOOT -->
<div id="boot">
  <div class="boot-hex">
    <svg viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
      <polygon points="50,5 95,27.5 95,72.5 50,95 5,72.5 5,27.5" stroke="rgba(0,212,255,0.6)" stroke-width="1.5"/>
      <polygon points="50,15 85,32.5 85,67.5 50,85 15,67.5 15,32.5" stroke="rgba(0,212,255,0.3)" stroke-width="1"/>
      <line x1="50" y1="5" x2="50" y2="15" stroke="rgba(0,212,255,0.8)" stroke-width="1.5"/>
      <line x1="95" y1="27.5" x2="85" y2="32.5" stroke="rgba(0,212,255,0.8)" stroke-width="1.5"/>
      <line x1="95" y1="72.5" x2="85" y2="67.5" stroke="rgba(0,212,255,0.8)" stroke-width="1.5"/>
      <line x1="50" y1="95" x2="50" y2="85" stroke="rgba(0,212,255,0.8)" stroke-width="1.5"/>
      <line x1="5" y1="72.5" x2="15" y2="67.5" stroke="rgba(0,212,255,0.8)" stroke-width="1.5"/>
      <line x1="5" y1="27.5" x2="15" y2="32.5" stroke="rgba(0,212,255,0.8)" stroke-width="1.5"/>
      <circle cx="50" cy="50" r="3" fill="rgba(0,212,255,0.8)"/>
    </svg>
    <div class="boot-hex-text">VG</div>
  </div>
  <div class="boot-status" id="boot-status">INITIALIZING...</div>
  <div class="boot-log">
    <div class="blog" id="b1">&gt; <span class="ok">SYS</span> :: Booting secure environment...</div>
    <div class="blog" id="b2">&gt; <span class="ok">NET</span> :: Establishing encrypted channel... <span class="ok">✓</span></div>
    <div class="blog" id="b3">&gt; <span class="warn">SEC</span> :: Scanning for threats... <span class="ok">CLEAN</span></div>
    <div class="blog" id="b4">&gt; <span class="ok">DB </span> :: Loading profile: VIRAJ GAMBHIR...</div>
    <div class="blog" id="b5">&gt; <span class="ok">AUTH</span> :: Identity verified — Cybersecurity Analyst</div>
    <div class="blog" id="b6">&gt; <span class="ok">SYS</span> :: Portfolio decrypted. <span class="warn">Access GRANTED ■</span></div>
  </div>
  <div class="boot-progress-wrap">
    <div class="boot-progress-pct" id="boot-pct">0%</div>
    <div class="boot-progress-track">
      <div class="boot-progress-bar"></div>
    </div>
  </div>
</div>

<!-- BACKGROUNDS -->
<canvas id="particle-canvas"></canvas>
<div class="hex-bg"></div>
<div class="scanlines"></div>
<div class="scan-sweep"></div>
<div class="noise"></div>

<div class="page">
  <div class="top-bar"></div>

  <!-- ══ SIDEBAR ══ -->
  <aside class="sidebar">

    <div class="av-wrap reveal">
      <div class="av-outer">
        <div class="av-ring3"></div>
        <div class="av-ring2"></div>
        <div class="av-ring1"></div>
        <div class="av">VG</div>
      </div>
      <div class="av-name">VIRAJ GAMBHIR</div>
      <div class="av-tag">🔐 CYBERSECURITY</div>
    </div>

    <div class="ss reveal">
      <div class="st">Contact</div>
      <div class="ci"><span class="cl">Phone</span><span class="cv">+91 9084970468</span></div>
      <div class="ci"><span class="cl">Email</span><span class="cv"><a href="mailto:virajgambhir1215@gmail.com">virajgambhir1215@gmail.com</a></span></div>
      <div class="ci"><span class="cl">LinkedIn</span><span class="cv"><a href="https://www.linkedin.com/in/viraj-gambhir-09b7aa313/" target="_blank">viraj-gambhir</a></span></div>
      <div class="ci"><span class="cl">GitHub</span><span class="cv"><a href="https://github.com/virajgambhir1215-hub" target="_blank">virajgambhir1215-hub</a></span></div>
      <div class="ci"><span class="cl">Location</span><span class="cv">Meerut, Uttar Pradesh, India</span></div>
    </div>

    <div class="ss reveal">
      <div class="st">Core Skills</div>
      <div class="ski"><div class="skr"><span class="skn">Ethical Hacking</span><span class="skp">78%</span></div><div class="skbar"><div class="skfill" data-w="78" style="background:linear-gradient(90deg,#0096b8,#00d4ff,rgba(255,255,255,.8))"></div></div></div>
      <div class="ski"><div class="skr"><span class="skn">Kali Linux</span><span class="skp">75%</span></div><div class="skbar"><div class="skfill" data-w="75"></div></div></div>
      <div class="ski"><div class="skr"><span class="skn">Network Security</span><span class="skp">70%</span></div><div class="skbar"><div class="skfill" data-w="70"></div></div></div>
      <div class="ski"><div class="skr"><span class="skn">Java</span><span class="skp">72%</span></div><div class="skbar"><div class="skfill" data-w="72" style="background:linear-gradient(90deg,#b87a00,#e8c46a,rgba(255,255,255,.8));box-shadow:0 0 8px rgba(232,196,106,.6)"></div></div></div>
      <div class="ski"><div class="skr"><span class="skn">C Programming</span><span class="skp">68%</span></div><div class="skbar"><div class="skfill" data-w="68"></div></div></div>
      <div class="ski"><div class="skr"><span class="skn">Cryptography</span><span class="skp">65%</span></div><div class="skbar"><div class="skfill" data-w="65" style="background:linear-gradient(90deg,#5a1acc,#7b2fff,rgba(255,255,255,.8));box-shadow:0 0 8px rgba(123,47,255,.6)"></div></div></div>
    </div>

    <div class="ss reveal">
      <div class="st">Tools & Platforms</div>
      <div class="tg-group">
        <span class="tg">Kali Linux</span><span class="tg">Arduino IDE</span>
        <span class="tg">ESP32</span><span class="tg">GitHub</span>
        <span class="tg">Linux CLI</span><span class="tg">RFID RC522</span>
        <span class="tg">Wi-Fi Protocols</span><span class="tg">Arduino Uno</span>
      </div>
    </div>

    <div class="ss reveal">
      <div class="st">Soft Skills</div>
      <div class="tg-group">
        <span class="tg">Analytical Thinking</span><span class="tg">Problem Solving</span>
        <span class="tg">Adaptability</span><span class="tg">Curiosity-Driven</span>
        <span class="tg">Team Collaboration</span>
      </div>
    </div>

    <div class="ss reveal">
      <div class="st">Certification</div>
      <div class="cert">
        <div class="cert-name">Coincent — Cyber Security &amp; Ethical Hacking</div>
        <div class="cert-sub">Phase 1 Certified &nbsp;·&nbsp; 3-Month Program</div>
        <div class="cert-sub" style="color:var(--muted);margin-top:2px;">Dec 2025 – Jan 2026 &nbsp;·&nbsp; E-Cell IIT Madras</div>
        <div class="cert-badge">Verified &amp; Issued 06 Feb 2026</div>
      </div>
    </div>

  </aside>

  <!-- ══ MAIN ══ -->
  <main class="main">

    <header class="hdr reveal">
      <div class="hdr-name" data-text="VIRAJ GAMBHIR">VIRAJ <span class="acc">GAMBHIR</span></div>
      <div class="hdr-role">// Cybersecurity Analyst &nbsp;·&nbsp; Ethical Hacker &nbsp;·&nbsp; Builder</div>
      <div class="hdr-quote">"Breaking systems to build better defenses — one vulnerability at a time."</div>
      <div class="status-row">
        <div class="spill green"><div class="sdot g"></div>Open to Opportunities</div>
        <div class="spill cyan"><div class="sdot c"></div>Meerut, India</div>
        <div class="spill gold"><div class="sdot o"></div>CGPA: 8.75</div>
      </div>
    </header>

    <section class="sec reveal">
      <div class="sec-title">Professional Summary</div>
      <div class="sum">
        Cybersecurity enthusiast and B.Tech CSE undergraduate at Gautam Buddha University (CGPA: 8.75) with certified expertise in Ethical Hacking &amp; Cybersecurity through the Coincent program (E-Cell, IIT Madras). Passionate about penetration testing, embedded security, and building secure communication systems. Experienced in developing real-world hardware security projects — from RFID access control to encrypted P2P messengers. Driven to grow into a skilled Cybersecurity Analyst or Penetration Tester who helps organizations build attack-proof, resilient infrastructures.
      </div>
    </section>

    <!-- SKILL RADAR -->
    <section class="sec reveal">
      <div class="sec-title">Skill Proficiency Radar</div>
      <div class="radar-wrap">
        <canvas id="radarCanvas" width="160" height="160"></canvas>
        <div class="radar-legend">
          <div class="rl-item"><div class="rl-dot" style="background:#00d4ff;box-shadow:0 0 6px #00d4ff"></div><span style="min-width:110px">Ethical Hacking</span><div class="rl-bar-wrap"><div class="rl-bar" data-w="78" style="background:linear-gradient(90deg,#00a8cc,#00d4ff)"></div></div><span style="color:var(--cyan);margin-left:6px;font-size:.55rem">78%</span></div>
          <div class="rl-item"><div class="rl-dot" style="background:#00d4ff;box-shadow:0 0 6px #00d4ff"></div><span style="min-width:110px">Kali Linux</span><div class="rl-bar-wrap"><div class="rl-bar" data-w="75" style="background:linear-gradient(90deg,#00a8cc,#00d4ff)"></div></div><span style="color:var(--cyan);margin-left:6px;font-size:.55rem">75%</span></div>
          <div class="rl-item"><div class="rl-dot" style="background:#00ff88;box-shadow:0 0 6px #00ff88"></div><span style="min-width:110px">Network Security</span><div class="rl-bar-wrap"><div class="rl-bar" data-w="70" style="background:linear-gradient(90deg,#00cc66,#00ff88)"></div></div><span style="color:var(--green);margin-left:6px;font-size:.55rem">70%</span></div>
          <div class="rl-item"><div class="rl-dot" style="background:#e8c46a;box-shadow:0 0 6px #e8c46a"></div><span style="min-width:110px">Java</span><div class="rl-bar-wrap"><div class="rl-bar" data-w="72" style="background:linear-gradient(90deg,#b87a00,#e8c46a)"></div></div><span style="color:var(--gold);margin-left:6px;font-size:.55rem">72%</span></div>
          <div class="rl-item"><div class="rl-dot" style="background:#00d4ff;box-shadow:0 0 6px #00d4ff"></div><span style="min-width:110px">C Programming</span><div class="rl-bar-wrap"><div class="rl-bar" data-w="68" style="background:linear-gradient(90deg,#00a8cc,#00d4ff)"></div></div><span style="color:var(--cyan);margin-left:6px;font-size:.55rem">68%</span></div>
          <div class="rl-item"><div class="rl-dot" style="background:#7b2fff;box-shadow:0 0 6px #7b2fff"></div><span style="min-width:110px">Cryptography</span><div class="rl-bar-wrap"><div class="rl-bar" data-w="65" style="background:linear-gradient(90deg,#5a1acc,#7b2fff)"></div></div><span style="color:var(--purple);margin-left:6px;font-size:.55rem">65%</span></div>
        </div>
      </div>
    </section>

    <section class="sec reveal">
      <div class="sec-title">Projects</div>

      <div class="card">
        <div class="card-corner"></div>
        <div class="ch">
          <div><div class="ct">Ghost Chat — Secure P2P Messenger</div><div class="cs">Network Security · Encrypted Communication</div></div>
          <div class="cd">2024</div>
        </div>
        <ul>
          <li>Built a covert offline P2P chat application on ESP32 microcontrollers — anonymous, server-free communication over local Wi-Fi, eliminating interception attack surfaces.</li>
          <li>Developed and adversarially tested using Kali Linux to simulate real-world network threats and validate communication integrity under attack conditions.</li>
          <li>Applied core principles of network anonymity, protocol-level security, and secure system design — demonstrating a genuine offensive security mindset.</li>
          <li>Zero dependency on external infrastructure, making the system resistant to surveillance and third-party data harvesting.</li>
        </ul>
        <div class="stk">
          <span class="sp">ESP32</span><span class="sp">Kali Linux</span><span class="sp">Java</span>
          <span class="sp">Wi-Fi Protocols</span><span class="sp">P2P Networking</span><span class="sp">Secure Comms</span>
        </div>
      </div>

      <div class="card">
        <div class="card-corner"></div>
        <div class="ch">
          <div><div class="ct">RFID Smart Attendance System</div><div class="cs">Hardware Security · Embedded Access Control</div></div>
          <div class="cd">2024</div>
        </div>
        <ul>
          <li>Engineered a contactless attendance system using Arduino Uno and RFID RC522 — replacing manual processes with tamper-resistant card-based identity verification.</li>
          <li>Implemented secure access logging with unique RFID tag authentication, ensuring only authorized individuals are recorded — core physical security principles.</li>
          <li>Designed entirely in C, optimizing read latency and minimizing false authentication events through tight hardware-level control.</li>
          <li>Demonstrated real-world understanding of physical access control systems — a critical domain in enterprise cybersecurity.</li>
        </ul>
        <div class="stk">
          <span class="sp">Arduino Uno</span><span class="sp">RFID RC522</span><span class="sp">C</span>
          <span class="sp">Arduino IDE</span><span class="sp">Access Control</span><span class="sp">Embedded Systems</span>
        </div>
      </div>
    </section>

    <section class="sec reveal">
      <div class="sec-title">Certification &amp; Training</div>
      <div class="card">
        <div class="card-corner"></div>
        <div class="ch">
          <div><div class="ct">Cyber Security &amp; Ethical Hacking — Coincent</div><div class="cs">Phase 1 Certified · E-Cell IIT Madras · Issued 06 Feb 2026</div></div>
          <div class="cd">Dec 2025 – Jan 2026</div>
        </div>
        <ul>
          <li>Completed a structured 2-month cybersecurity program covering ethical hacking, penetration testing methodology, and vulnerability identification fundamentals.</li>
          <li>Gained practical exposure to security assessment techniques, network defense strategies, and real-world threat simulation scenarios.</li>
          <li>Awarded Phase 1 Certification by Coincent in association with E-Cell, IIT Madras upon demonstrating core cybersecurity competencies.</li>
        </ul>
      </div>
    </section>

    <section class="sec reveal">
      <div class="sec-title">Education</div>
      <div class="edu">
        <div>
          <div class="ed">B.Tech — Computer Science &amp; Engineering</div>
          <div class="eu">Gautam Buddha University, Greater Noida, India</div>
          <div class="ec">Cryptography · Network Security · Data Structures · Operating Systems · DBMS</div>
        </div>
        <div class="em">
          <div class="cgpa">8.75</div>
          <div class="cgpalabel">CGPA</div>
          <div class="ey">2025 – 2029 (Expected)</div>
        </div>
      </div>
    </section>

    <section class="sec reveal">
      <div class="sec-title">Areas of Interest</div>
      <div class="int-grid">
        <span class="itag">⚔️ Penetration Testing</span>
        <span class="itag">🔍 Vulnerability Assessment</span>
        <span class="itag">🌐 Network Security</span>
        <span class="itag">🔐 Secure System Design</span>
        <span class="itag">🎯 Ethical Hacking</span>
        <span class="itag">🔑 Cryptography</span>
        <span class="itag">🔧 Embedded Security</span>
        <span class="itag">📡 SOC Operations</span>
      </div>
    </section>

  </main>
</div>

<script>
/* ══ CURSOR ══ */
const cur = document.getElementById('cursor');
const tra = document.getElementById('cursor-trail');
let mx=0,my=0,tx=0,ty=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cur.style.left=mx+'px';cur.style.top=my+'px';});
setInterval(()=>{tx+=(mx-tx)*.12;ty+=(my-ty)*.12;tra.style.left=tx+'px';tra.style.top=ty+'px';},16);

/* ══ BOOT SEQUENCE ══ */
(function(){
  const ids=['b1','b2','b3','b4','b5','b6'];
  const statuses=['INITIALIZING...','LOADING MODULES...','SCANNING...','FETCHING PROFILE...','AUTHENTICATING...','ACCESS GRANTED'];
  const pct=document.getElementById('boot-pct');
  const stat=document.getElementById('boot-status');
  ids.forEach((id,i)=>{
    setTimeout(()=>{
      document.getElementById(id).classList.add('on');
      stat.textContent=statuses[i];
      const p=Math.round((i+1)/ids.length*100);
      pct.textContent=p+'%';
    },i*350+200);
  });
  setTimeout(()=>{
    document.getElementById('boot').classList.add('out');
    setTimeout(()=>{document.getElementById('boot').remove();},900);
    initReveal();
    animateBars();
    drawRadar();
    animateRadarBars();
  },ids.length*350+600);
})();

/* ══ PARTICLE NETWORK ══ */
(function(){
  const canvas=document.getElementById('particle-canvas');
  const ctx=canvas.getContext('2d');
  let W,H,pts=[];
  function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight;}
  resize();window.addEventListener('resize',resize);

  class Pt{
    constructor(){this.reset();}
    reset(){
      this.x=Math.random()*W;this.y=Math.random()*H;
      this.vx=(Math.random()-.5)*.4;this.vy=(Math.random()-.5)*.4;
      this.r=Math.random()*2+.5;this.alpha=Math.random()*.6+.2;
      this.color=Math.random()>.7?'232,196,106':'0,212,255';
    }
    update(){
      this.x+=this.vx;this.y+=this.vy;
      if(this.x<0||this.x>W||this.y<0||this.y>H)this.reset();
    }
    draw(){
      ctx.beginPath();ctx.arc(this.x,this.y,this.r,0,Math.PI*2);
      ctx.fillStyle=`rgba(${this.color},${this.alpha})`;ctx.fill();
    }
  }

  for(let i=0;i<80;i++)pts.push(new Pt());

  function frame(){
    ctx.clearRect(0,0,W,H);
    pts.forEach(p=>{p.update();p.draw();});
    pts.forEach((a,i)=>{
      pts.slice(i+1).forEach(b=>{
        const d=Math.hypot(a.x-b.x,a.y-b.y);
        if(d<120){
          ctx.beginPath();ctx.moveTo(a.x,a.y);ctx.lineTo(b.x,b.y);
          ctx.strokeStyle=`rgba(0,212,255,${(1-d/120)*.12})`;ctx.lineWidth=.5;ctx.stroke();
        }
      });
    });
    requestAnimationFrame(frame);
  }
  frame();
})();

/* ══ REVEAL ══ */
function initReveal(){
  const els=document.querySelectorAll('.reveal');
  const io=new IntersectionObserver(entries=>{
    entries.forEach((e,idx)=>{
      if(e.isIntersecting){
        setTimeout(()=>e.target.classList.add('vis'),idx*100);
        io.unobserve(e.target);
      }
    });
  },{threshold:.1});
  els.forEach(el=>io.observe(el));
}

/* ══ SKILL BARS ══ */
function animateBars(){
  setTimeout(()=>{
    document.querySelectorAll('.skfill').forEach((el,i)=>{
      setTimeout(()=>{el.style.width=el.dataset.w+'%';},i*160+300);
    });
  },400);
}

/* ══ RADAR CHART ══ */
function drawRadar(){
  const canvas=document.getElementById('radarCanvas');
  const ctx=canvas.getContext('2d');
  const cx=80,cy=80,R=65;
  const labels=['Hacking','Kali','NetSec','Java','C','Crypto'];
  const vals=[.78,.75,.70,.72,.68,.65];
  const N=6;
  let frame=0;
  const colors=['#00d4ff','#00d4ff','#00ff88','#e8c46a','#00d4ff','#7b2fff'];

  function draw(){
    ctx.clearRect(0,0,160,160);
    frame=Math.min(frame+.04,1);
    const ease=t=>1-Math.pow(1-t,3);
    const t=ease(frame);

    // web rings
    [.25,.5,.75,1].forEach(r=>{
      ctx.beginPath();
      for(let i=0;i<N;i++){
        const a=i/N*Math.PI*2-Math.PI/2;
        const x=cx+R*r*Math.cos(a);const y=cy+R*r*Math.sin(a);
        i===0?ctx.moveTo(x,y):ctx.lineTo(x,y);
      }
      ctx.closePath();
      ctx.strokeStyle=`rgba(0,212,255,${r===1?.15:.08})`;ctx.lineWidth=.8;ctx.stroke();
    });

    // spokes
    for(let i=0;i<N;i++){
      const a=i/N*Math.PI*2-Math.PI/2;
      ctx.beginPath();ctx.moveTo(cx,cy);
      ctx.lineTo(cx+R*Math.cos(a),cy+R*Math.sin(a));
      ctx.strokeStyle='rgba(0,212,255,0.1)';ctx.lineWidth=.8;ctx.stroke();
    }

    // filled area
    ctx.beginPath();
    vals.forEach((v,i)=>{
      const a=i/N*Math.PI*2-Math.PI/2;
      const rv=v*R*t;
      const x=cx+rv*Math.cos(a);const y=cy+rv*Math.sin(a);
      i===0?ctx.moveTo(x,y):ctx.lineTo(x,y);
    });
    ctx.closePath();
    ctx.fillStyle='rgba(0,212,255,0.08)';ctx.fill();
    ctx.strokeStyle='rgba(0,212,255,0.5)';ctx.lineWidth=1.5;ctx.stroke();

    // dots + glow
    vals.forEach((v,i)=>{
      const a=i/N*Math.PI*2-Math.PI/2;
      const rv=v*R*t;
      const x=cx+rv*Math.cos(a);const y=cy+rv*Math.sin(a);
      ctx.beginPath();ctx.arc(x,y,3,0,Math.PI*2);
      ctx.fillStyle=colors[i];ctx.fill();
      ctx.beginPath();ctx.arc(x,y,5,0,Math.PI*2);
      ctx.fillStyle=`rgba(0,212,255,.15)`;ctx.fill();
    });

    // center dot
    ctx.beginPath();ctx.arc(cx,cy,3,0,Math.PI*2);
    ctx.fillStyle='rgba(0,212,255,.5)';ctx.fill();

    if(frame<1)requestAnimationFrame(draw);
  }
  requestAnimationFrame(draw);
}

function animateRadarBars(){
  setTimeout(()=>{
    document.querySelectorAll('.rl-bar').forEach((el,i)=>{
      setTimeout(()=>{el.style.width=el.dataset.w+'%';},i*180+400);
    });
  },600);
}
</script>
</body>
</html>
