<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>CodewithSaket — Saket Raj 🚀</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&family=Exo+2:wght@300;400;700;900&display=swap" rel="stylesheet"/>
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#02020a;
  --neon:#00ffe7;
  --pink:#ff2d78;
  --gold:#ffd700;
  --purple:#a855f7;
  --blue:#38bdf8;
  --text:#e0e0f0;
  --dim:#4a4a6a;
}
html{scroll-behavior:smooth}
body{
  background:var(--bg);
  color:var(--text);
  font-family:'Exo 2',sans-serif;
  overflow-x:hidden;
  /* Removed cursor:none from body — only hide when JS cursor is ready */
}
body.cursor-ready { cursor: none; }

/* ── CUSTOM CURSOR ── */
#cur{
  position:fixed;top:0;left:0;
  pointer-events:none;z-index:9999;
  /* Start hidden, shown via JS */
  opacity:0;transition:opacity .3s;
}
#cur.active{opacity:1}
#curCanvas{display:block}

/* ── STARFIELD ── */
#stars{position:fixed;inset:0;z-index:0;pointer-events:none}

/* ── NAV ── */
nav{
  position:fixed;top:0;width:100%;z-index:200;
  padding:18px 48px;
  display:flex;justify-content:space-between;align-items:center;
  background:rgba(2,2,10,0.85);
  border-bottom:1px solid rgba(0,255,231,0.1);
  backdrop-filter:blur(16px);
}
.nav-logo{
  font-family:'Orbitron',sans-serif;
  font-size:15px;font-weight:900;
  color:var(--neon);
  letter-spacing:.12em;
  text-shadow:0 0 20px var(--neon),0 0 40px rgba(0,255,231,.3);
  animation:logoPulse 3s ease-in-out infinite;
}
@keyframes logoPulse{
  0%,100%{text-shadow:0 0 20px var(--neon),0 0 40px rgba(0,255,231,.3)}
  50%{text-shadow:0 0 40px var(--neon),0 0 80px rgba(0,255,231,.5),0 0 120px rgba(0,255,231,.2)}
}
.nav-links{display:flex;gap:28px}
.nav-links a{
  font-family:'Share Tech Mono',monospace;font-size:12px;
  color:var(--dim);text-decoration:none;letter-spacing:.1em;
  transition:all .2s;position:relative;
  cursor:pointer;
}
.nav-links a::after{content:'';position:absolute;bottom:-4px;left:0;width:0;height:1px;background:var(--neon);transition:width .3s}
.nav-links a:hover{color:var(--neon)}
.nav-links a:hover::after{width:100%}
.status-pill{
  display:flex;align-items:center;gap:8px;
  font-family:'Share Tech Mono',monospace;font-size:11px;
  color:var(--neon);
  border:1px solid rgba(0,255,231,.3);
  padding:6px 14px;border-radius:20px;
  background:rgba(0,255,231,.04);
}
.status-dot{
  width:7px;height:7px;
  background:var(--neon);border-radius:50%;
  animation:blink 1.2s ease-in-out infinite;
  box-shadow:0 0 8px var(--neon);
  flex-shrink:0;
}
@keyframes blink{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.3;transform:scale(.7)}}

/* ── HERO ── */
.hero{
  position:relative;min-height:100vh;
  display:flex;align-items:center;
  padding:100px 48px 80px;
  z-index:1;overflow:hidden;
}
.hero-left{flex:1;max-width:680px;z-index:2}
.hero-right{
  position:absolute;right:48px;top:50%;transform:translateY(-50%);
  width:440px;z-index:1;
}

.glitch-wrap{margin-bottom:10px}
.glitch-tag{
  font-family:'Share Tech Mono',monospace;font-size:12px;
  color:var(--neon);letter-spacing:.2em;text-transform:uppercase;
  opacity:0;animation:fadeUp .5s ease forwards .3s;
}

.hero-name{
  font-family:'Orbitron',sans-serif;
  font-size:clamp(42px,7vw,96px);
  font-weight:900;
  line-height:.95;
  letter-spacing:-.02em;
  margin:16px 0 8px;
  opacity:0;animation:fadeUp .7s ease forwards .5s;
}
.hero-name .line1{
  display:block;
  background:linear-gradient(90deg,#fff 0%,var(--blue) 50%,var(--neon) 100%);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
}
.hero-name .line2{
  display:block;
  color:var(--pink);
  -webkit-text-fill-color:var(--pink);
  filter:drop-shadow(0 0 30px var(--pink));
  animation:nameGlow 2s ease-in-out infinite;
}
@keyframes nameGlow{
  0%,100%{filter:drop-shadow(0 0 30px var(--pink))}
  50%{filter:drop-shadow(0 0 60px var(--pink)) drop-shadow(0 0 100px rgba(255,45,120,.4))}
}

/* GLITCH TEXT */
.glitch{
  position:relative;
  font-family:'Orbitron',sans-serif;
  font-size:clamp(42px,7vw,96px);
  font-weight:900;
  color:#fff;
}
.glitch::before,.glitch::after{
  content:attr(data-text);
  position:absolute;top:0;left:0;
  width:100%;height:100%;
}
.glitch::before{
  color:var(--pink);
  animation:glitch1 4s infinite;
  clip-path:polygon(0 0,100% 0,100% 35%,0 35%);
}
.glitch::after{
  color:var(--neon);
  animation:glitch2 4s infinite;
  clip-path:polygon(0 65%,100% 65%,100% 100%,0 100%);
}
@keyframes glitch1{
  0%,90%,100%{transform:translate(0)}
  92%{transform:translate(-4px,2px)}
  94%{transform:translate(4px,-2px)}
  96%{transform:translate(-2px,0)}
  98%{transform:translate(2px,1px)}
}
@keyframes glitch2{
  0%,88%,100%{transform:translate(0)}
  90%{transform:translate(4px,-2px)}
  93%{transform:translate(-4px,2px)}
  97%{transform:translate(3px,0)}
}

.hero-desc{
  font-family:'Share Tech Mono',monospace;
  font-size:14px;color:rgba(224,224,240,.7);
  line-height:1.8;margin:24px 0 40px;max-width:480px;
  opacity:0;animation:fadeUp .7s ease forwards .9s;
}
.hero-desc .hi{color:var(--neon)}.hero-desc .hot{color:var(--pink)}

.hero-btns{
  display:flex;gap:16px;flex-wrap:wrap;
  opacity:0;animation:fadeUp .7s ease forwards 1.1s;
}
.btn-neon{
  display:inline-flex;align-items:center;gap:10px;
  background:transparent;
  border:2px solid var(--neon);
  color:var(--neon);
  font-family:'Orbitron',monospace;font-size:12px;font-weight:700;
  padding:14px 28px;text-decoration:none;letter-spacing:.1em;
  cursor:pointer;
  position:relative;overflow:hidden;
  transition:all .3s;
  text-transform:uppercase;
}
.btn-neon::before{
  content:'';position:absolute;inset:0;
  background:var(--neon);
  transform:translateX(-100%) skewX(-15deg);
  transition:transform .3s ease;
  z-index:-1;
}
.btn-neon:hover::before{transform:translateX(0) skewX(-15deg)}
.btn-neon:hover{color:#000;box-shadow:0 0 40px rgba(0,255,231,.5)}

.btn-pink{
  display:inline-flex;align-items:center;gap:10px;
  background:var(--pink);border:2px solid var(--pink);
  color:#fff;font-family:'Orbitron',monospace;font-size:12px;font-weight:700;
  padding:14px 28px;text-decoration:none;letter-spacing:.1em;
  cursor:pointer;transition:all .3s;text-transform:uppercase;
}
.btn-pink:hover{background:transparent;color:var(--pink);box-shadow:0 0 40px rgba(255,45,120,.5)}

/* ── ASTRONAUT ── */
.astronaut-wrap{
  opacity:0;animation:fadeLeft .8s ease forwards 1.4s;
  transform-origin:center;
}
.astronaut-svg{
  width:100%;
  animation:float 4s ease-in-out infinite;
  filter:drop-shadow(0 20px 60px rgba(0,255,231,.25));
}
@keyframes float{
  0%,100%{transform:translateY(0) rotate(-2deg)}
  50%{transform:translateY(-20px) rotate(2deg)}
}

/* ── SECTION COMMONS ── */
section{position:relative;z-index:1;padding:100px 48px}
.sec-label{
  font-family:'Share Tech Mono',monospace;font-size:11px;
  color:var(--neon);letter-spacing:.25em;text-transform:uppercase;
  margin-bottom:12px;display:flex;align-items:center;gap:12px;
}
.sec-label::before{content:'▶';font-size:8px}
.sec-title{
  font-family:'Orbitron',sans-serif;
  font-size:clamp(32px,5vw,56px);font-weight:900;
  letter-spacing:-.02em;margin-bottom:60px;
  line-height:1.1;
}
.highlight{color:var(--neon)}
.highlight-pink{color:var(--pink)}

/* ── ABOUT ── */
.about-grid{display:grid;grid-template-columns:1fr 1fr;gap:60px;align-items:start}
.about-text p{
  font-family:'Share Tech Mono',monospace;font-size:13px;
  color:rgba(224,224,240,.6);line-height:2;margin-bottom:16px;
}
.about-text p b{color:var(--neon)}
.about-text p em{color:var(--pink);font-style:normal}

/* Robot */
.robot-scene{position:relative;display:flex;justify-content:center;align-items:center}
.robot-svg{width:280px;animation:robotBob 2s ease-in-out infinite}
@keyframes robotBob{0%,100%{transform:translateY(0)}50%{transform:translateY(-12px)}}
.robot-glow{
  position:absolute;bottom:-20px;left:50%;transform:translateX(-50%);
  width:200px;height:30px;
  background:radial-gradient(ellipse,rgba(0,255,231,.3) 0%,transparent 70%);
  animation:shadowPulse 2s ease-in-out infinite;
}
@keyframes shadowPulse{
  0%,100%{opacity:.5;transform:translateX(-50%) scaleX(1)}
  50%{opacity:1;transform:translateX(-50%) scaleX(.7)}
}
.speech{
  position:absolute;top:10px;right:-20px;
  background:rgba(0,255,231,.1);
  border:1px solid var(--neon);
  padding:12px 18px;border-radius:12px 12px 12px 0;
  font-family:'Share Tech Mono',monospace;font-size:12px;
  color:var(--neon);white-space:nowrap;
  animation:speechBounce 3s ease-in-out infinite;
  z-index:10;
}
.speech::after{
  content:'';position:absolute;bottom:-10px;left:0;
  border:5px solid transparent;
  border-top-color:var(--neon);border-right-color:var(--neon);
}
@keyframes speechBounce{0%,100%{transform:translateY(0)}50%{transform:translateY(-6px)}}

/* ── SKILLS ── */
.skills-outer{
  background:rgba(0,255,231,.02);border:1px solid rgba(0,255,231,.07);
  padding:48px;position:relative;overflow:hidden;
}
.skills-outer::before{
  content:'SKILLS';
  position:absolute;right:-20px;top:50%;transform:translateY(-50%) rotate(90deg);
  font-family:'Orbitron',sans-serif;font-size:80px;font-weight:900;
  color:rgba(0,255,231,.03);letter-spacing:.2em;pointer-events:none;
  white-space:nowrap;
}
.skill-rows{display:flex;flex-direction:column;gap:20px}
.skill-row{display:flex;align-items:center;gap:20px}
.skill-icon-wrap{
  width:52px;height:52px;flex-shrink:0;
  display:flex;align-items:center;justify-content:center;
  border:1px solid rgba(0,255,231,.2);
  background:rgba(0,255,231,.05);
  font-size:24px;
  transition:all .3s;
  cursor:pointer;
}
.skill-icon-wrap:hover{
  border-color:var(--neon);
  background:rgba(0,255,231,.1);
  transform:scale(1.1) rotate(5deg);
  box-shadow:0 0 20px rgba(0,255,231,.3);
}
.skill-info{flex:1;min-width:0}
.skill-name{
  font-family:'Orbitron',sans-serif;font-size:13px;font-weight:700;
  color:var(--text);margin-bottom:8px;
  display:flex;justify-content:space-between;align-items:center;
}
.skill-pct{color:var(--neon);font-size:12px;flex-shrink:0}
.skill-bar{height:4px;background:rgba(255,255,255,.06);border-radius:2px;overflow:hidden}

/* FIX: skill bars now use width set by JS, not CSS scaleX */
.skill-fill{
  height:100%;border-radius:2px;
  background:linear-gradient(90deg,var(--neon),var(--blue));
  width:0%; /* start at 0, JS animates to target */
  transition:width 1.2s cubic-bezier(.25,.46,.45,.94);
}
.skill-fill.pink{background:linear-gradient(90deg,var(--pink),var(--purple))}
.skill-fill.gold{background:linear-gradient(90deg,var(--gold),var(--pink))}

/* ── BUILDING ── */
.build-grid{display:grid;grid-template-columns:1fr 1fr;gap:24px}
.build-card{
  border:1px solid rgba(0,255,231,.12);
  background:rgba(0,255,231,.02);
  padding:36px;position:relative;overflow:hidden;
  transition:all .3s;cursor:pointer;
}
.build-card::before{
  content:'';position:absolute;inset:0;
  background:linear-gradient(135deg,rgba(0,255,231,.07) 0%,transparent 60%);
  opacity:0;transition:opacity .3s;
}
.build-card:hover::before{opacity:1}
.build-card:hover{
  border-color:rgba(0,255,231,.4);
  transform:translateY(-6px);
  box-shadow:0 20px 60px rgba(0,0,0,.5),0 0 0 1px rgba(0,255,231,.08),inset 0 1px 0 rgba(0,255,231,.1);
}
.build-card .emoji{
  font-size:44px;display:block;margin-bottom:20px;
  animation:emojiFloat 3s ease-in-out infinite;
}
@keyframes emojiFloat{
  0%,100%{transform:translateY(0) rotate(0deg)}
  50%{transform:translateY(-8px) rotate(5deg)}
}
.build-status{
  font-family:'Share Tech Mono',monospace;font-size:10px;letter-spacing:.2em;
  padding:4px 10px;border-radius:20px;display:inline-block;margin-bottom:16px;
}
.status-live{color:#00ff88;border:1px solid rgba(0,255,136,.3);background:rgba(0,255,136,.08)}
.status-wip{color:var(--gold);border:1px solid rgba(255,215,0,.3);background:rgba(255,215,0,.06)}
.build-title{font-family:'Orbitron',sans-serif;font-size:18px;font-weight:700;margin-bottom:12px;color:var(--text)}
.build-desc{font-family:'Share Tech Mono',monospace;font-size:12px;color:var(--dim);line-height:1.8;margin-bottom:20px}
.prog-bar{height:6px;background:rgba(255,255,255,.06);border-radius:3px;overflow:hidden;position:relative}
.prog-fill{
  height:100%;border-radius:3px;
  background:linear-gradient(90deg,var(--neon),var(--blue),var(--pink));
  background-size:200%;
  animation:progMove 3s linear infinite;
}
@keyframes progMove{0%{background-position:0%}100%{background-position:200%}}
.prog-label{
  display:flex;justify-content:space-between;
  font-family:'Share Tech Mono',monospace;font-size:11px;
  color:var(--dim);margin-top:8px;
}

/* ── PROJECTS ── */
.proj-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:20px}
.proj-card{
  background:rgba(255,255,255,.02);
  border:1px solid rgba(255,255,255,.06);
  padding:32px;position:relative;overflow:hidden;
  transition:all .3s;cursor:pointer;
}
.proj-card::after{
  content:'';position:absolute;
  top:-100%;left:-100%;width:300%;height:300%;
  background:conic-gradient(from 0deg,transparent,rgba(0,255,231,.05),transparent);
  animation:rotateShine 8s linear infinite;
  pointer-events:none;
}
.proj-card:hover{
  border-color:rgba(0,255,231,.3);
  transform:translateY(-8px) scale(1.01);
  box-shadow:0 30px 80px rgba(0,0,0,.6),0 0 30px rgba(0,255,231,.1);
}
@keyframes rotateShine{from{transform:rotate(0deg)}to{transform:rotate(360deg)}}
.proj-tag-row{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:16px}
.ptag{
  font-family:'Share Tech Mono',monospace;font-size:10px;
  padding:3px 10px;border-radius:2px;letter-spacing:.05em;
}
.ptag-n{color:var(--neon);border:1px solid rgba(0,255,231,.25);background:rgba(0,255,231,.05)}
.ptag-p{color:var(--pink);border:1px solid rgba(255,45,120,.25);background:rgba(255,45,120,.05)}
.ptag-g{color:var(--gold);border:1px solid rgba(255,215,0,.25);background:rgba(255,215,0,.05)}
.proj-title{font-family:'Orbitron',sans-serif;font-size:20px;font-weight:700;color:var(--text);margin-bottom:12px}
.proj-desc{font-family:'Share Tech Mono',monospace;font-size:12px;color:var(--dim);line-height:1.8;margin-bottom:24px}
.proj-link{
  font-family:'Orbitron',monospace;font-size:11px;font-weight:700;
  color:var(--neon);text-decoration:none;letter-spacing:.1em;
  display:inline-flex;align-items:center;gap:8px;
  transition:gap .2s;
  cursor:pointer;
}
.proj-link:hover{gap:14px}

/* ── CONNECT ── */
.connect-scene{
  display:grid;grid-template-columns:1fr 1fr;gap:60px;align-items:center;
}
.connect-links{display:flex;flex-direction:column;gap:16px}
.link-card{
  display:flex;align-items:center;gap:20px;
  padding:20px 28px;
  border:1px solid rgba(255,255,255,.06);
  background:rgba(255,255,255,.02);
  text-decoration:none;
  transition:all .25s;cursor:pointer;
  position:relative;overflow:hidden;
}
.link-card::before{
  content:'';position:absolute;left:0;top:0;bottom:0;width:3px;
  background:var(--neon);transform:scaleY(0);transition:transform .3s;
}
.link-card:hover::before{transform:scaleY(1)}
.link-card:hover{
  border-color:rgba(0,255,231,.25);
  background:rgba(0,255,231,.04);
  transform:translateX(8px);
}
.link-icon{font-size:26px;flex-shrink:0}
.link-info .link-name{font-family:'Orbitron',sans-serif;font-size:14px;font-weight:700;color:var(--text);display:block;margin-bottom:2px}
.link-info .link-sub{font-family:'Share Tech Mono',monospace;font-size:11px;color:var(--dim)}
.link-arrow{margin-left:auto;color:var(--dim);font-size:16px;transition:all .2s}
.link-card:hover .link-arrow{color:var(--neon);transform:translate(4px,-4px)}

/* Coding character */
.coder-svg{width:100%;animation:coderBob 3s ease-in-out infinite}
@keyframes coderBob{0%,100%{transform:translateY(0)}50%{transform:translateY(-10px)}}

/* ── FOOTER ── */
footer{
  position:relative;z-index:1;
  border-top:1px solid rgba(0,255,231,.08);
  padding:48px;text-align:center;
}
.footer-ascii{
  font-family:'Share Tech Mono',monospace;
  font-size:10px;color:rgba(0,255,231,.2);
  line-height:1.4;letter-spacing:.05em;
  margin-bottom:24px;
  animation:asciiGlow 4s ease-in-out infinite;
  overflow:hidden;white-space:nowrap;
  text-overflow:ellipsis;
}
@keyframes asciiGlow{0%,100%{color:rgba(0,255,231,.2)}50%{color:rgba(0,255,231,.4)}}
.footer-text{font-family:'Orbitron',monospace;font-size:13px;font-weight:700;color:var(--neon);letter-spacing:.15em;margin-bottom:8px}
.footer-sub{font-family:'Share Tech Mono',monospace;font-size:11px;color:var(--dim)}

/* ── SCROLL INDICATOR ── */
.scroll-hint{
  position:absolute;bottom:32px;left:50%;transform:translateX(-50%);
  display:flex;flex-direction:column;align-items:center;gap:8px;
  opacity:0;animation:fadeUp .6s ease forwards 1.6s;z-index:2;
}
.scroll-hint span{font-family:'Share Tech Mono',monospace;font-size:10px;color:var(--dim);letter-spacing:.2em}
.scroll-line{width:1px;height:50px;background:linear-gradient(to bottom,var(--neon),transparent);animation:lineScroll 2s ease-in-out infinite}
@keyframes lineScroll{0%,100%{opacity:1;transform:scaleY(1)}50%{opacity:.3;transform:scaleY(.4)}}

/* ── REVEAL ── */
.reveal{opacity:0;transform:translateY(40px);transition:opacity .7s ease,transform .7s ease}
.reveal.visible{opacity:1;transform:translateY(0)}

/* ── ANIMS ── */
@keyframes fadeUp{from{opacity:0;transform:translateY(24px)}to{opacity:1;transform:translateY(0)}}
@keyframes fadeLeft{from{opacity:0;transform:translateX(30px)}to{opacity:1;transform:translateX(0)}}

/* ── SCAN LINES ── */
.scanlines{
  position:fixed;inset:0;z-index:999;pointer-events:none;
  background:repeating-linear-gradient(
    0deg,transparent,transparent 2px,
    rgba(0,0,0,.08) 2px,rgba(0,0,0,.08) 4px
  );
  opacity:.4;
}

/* ── CORNER DECORATIONS ── */
.corner-tl,.corner-br{
  position:fixed;width:80px;height:80px;
  border-color:rgba(0,255,231,.3);
  border-style:solid;
  z-index:100;pointer-events:none;
}
.corner-tl{top:80px;left:20px;border-width:2px 0 0 2px;border-radius:4px 0 0 0}
.corner-br{bottom:20px;right:20px;border-width:0 2px 2px 0;border-radius:0 0 4px 0}

/* Responsive */
@media(max-width:1000px){
  .hero{padding:100px 24px 80px}
  .hero-right{display:none}
  section{padding:80px 24px}
  .about-grid,.build-grid,.connect-scene{grid-template-columns:1fr}
  nav{padding:16px 24px}
  .nav-links{display:none}
  footer{padding:32px 24px}
  .footer-ascii{font-size:8px}
}
@media(max-width:600px){
  .proj-grid{grid-template-columns:1fr}
  .speech{display:none}
}
</style>
</head>
<body>

<div class="scanlines"></div>
<div class="corner-tl"></div>
<div class="corner-br"></div>

<!-- Custom cursor -->
<div id="cur"><canvas id="curCanvas" width="60" height="60"></canvas></div>

<!-- Starfield -->
<canvas id="stars"></canvas>

<!-- NAV -->
<nav>
  <div class="nav-logo">⟨ CodewithSaket /⟩</div>
  <div class="nav-links">
    <a href="#about">// about</a>
    <a href="#skills">// stack</a>
    <a href="#building">// building</a>
    <a href="#work">// work</a>
    <a href="#connect">// connect</a>
  </div>
  <div class="status-pill"><div class="status-dot"></div>open to collab</div>
</nav>

<!-- ═══ HERO ═══ -->
<section class="hero" id="home">
  <div class="hero-left">
    <div class="glitch-wrap">
      <div class="glitch-tag">[ SYSTEM ONLINE ] // DEVELOPER PROFILE LOADED</div>
    </div>

    <h1 class="hero-name">
      <span class="line1">SAKET</span>
      <span class="line2 glitch" data-text="RAJ">RAJ</span>
    </h1>

    <p class="hero-desc">
      <span class="hi">Full-Stack Dreamer.</span> Front-End Engineer from <span class="hot">Purnea, Bihar 🇮🇳</span><br/>
      Crafting pixel-perfect UIs by day, learning MERN by night.<br/>
      One commit at a time — shipping the future. 🚀
    </p>

    <div class="hero-btns">
      <a href="https://github.com/CodewithSaket" target="_blank" class="btn-neon">
        <svg width="16" height="16" fill="currentColor" viewBox="0 0 24 24"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub ↗
      </a>
      <a href="https://www.linkedin.com/in/-saket-raj/" target="_blank" class="btn-pink">💼 LinkedIn ↗</a>
    </div>
  </div>

  <!-- ASTRONAUT -->
  <div class="hero-right">
    <div class="astronaut-wrap">
      <svg class="astronaut-svg" viewBox="0 0 400 500" xmlns="http://www.w3.org/2000/svg">
        <g>
          <circle cx="30" cy="60" r="2" fill="#00ffe7" opacity=".6"><animate attributeName="opacity" values=".6;0;.6" dur="2s" repeatCount="indefinite"/></circle>
          <circle cx="370" cy="100" r="1.5" fill="#ff2d78" opacity=".8"><animate attributeName="opacity" values=".8;0;.8" dur="1.5s" begin=".5s" repeatCount="indefinite"/></circle>
          <circle cx="360" cy="380" r="2" fill="#ffd700" opacity=".7"><animate attributeName="opacity" values=".7;0;.7" dur="2.5s" begin="1s" repeatCount="indefinite"/></circle>
          <circle cx="20" cy="400" r="1" fill="#a855f7" opacity=".9"><animate attributeName="opacity" values=".9;0;.9" dur="1.8s" begin=".3s" repeatCount="indefinite"/></circle>
          <circle cx="200" cy="20" r="2.5" fill="#38bdf8" opacity=".5"><animate attributeName="opacity" values=".5;1;.5" dur="3s" repeatCount="indefinite"/></circle>
        </g>
        <!-- Jetpack exhaust -->
        <g opacity=".7">
          <ellipse cx="160" cy="390" rx="12" ry="8" fill="#00ffe7"><animate attributeName="ry" values="8;14;8" dur=".4s" repeatCount="indefinite"/><animate attributeName="opacity" values=".7;.3;.7" dur=".4s" repeatCount="indefinite"/></ellipse>
          <ellipse cx="240" cy="390" rx="12" ry="8" fill="#00ffe7"><animate attributeName="ry" values="8;14;8" dur=".4s" begin=".2s" repeatCount="indefinite"/><animate attributeName="opacity" values=".7;.3;.7" dur=".4s" begin=".2s" repeatCount="indefinite"/></ellipse>
          <ellipse cx="160" cy="405" rx="7" ry="18" fill="rgba(0,255,231,.4)"><animate attributeName="ry" values="18;28;18" dur=".3s" repeatCount="indefinite"/></ellipse>
          <ellipse cx="240" cy="405" rx="7" ry="18" fill="rgba(255,45,120,.4)"><animate attributeName="ry" values="18;28;18" dur=".3s" begin=".15s" repeatCount="indefinite"/></ellipse>
        </g>
        <!-- Jetpack body -->
        <rect x="140" y="300" width="40" height="60" rx="8" fill="#1a1a2e" stroke="#00ffe7" stroke-width="1.5"/>
        <rect x="220" y="300" width="40" height="60" rx="8" fill="#1a1a2e" stroke="#00ffe7" stroke-width="1.5"/>
        <rect x="155" y="270" width="90" height="90" rx="10" fill="#0d0d1a" stroke="rgba(0,255,231,.3)" stroke-width="1"/>
        <circle cx="170" cy="295" r="5" fill="#00ffe7"><animate attributeName="fill" values="#00ffe7;#fff;#00ffe7" dur=".8s" repeatCount="indefinite"/></circle>
        <circle cx="230" cy="295" r="5" fill="#ff2d78"><animate attributeName="fill" values="#ff2d78;#fff;#ff2d78" dur=".8s" begin=".4s" repeatCount="indefinite"/></circle>
        <!-- Suit body -->
        <ellipse cx="200" cy="260" rx="65" ry="80" fill="#e8e8f0"/>
        <ellipse cx="200" cy="260" rx="60" ry="75" fill="#d0d0e8"/>
        <!-- Chest panel -->
        <rect x="175" y="230" width="50" height="35" rx="6" fill="#1a1a2e" stroke="#00ffe7" stroke-width="1.5"/>
        <rect x="180" y="235" width="40" height="25" rx="4" fill="#050508"/>
        <text x="200" y="252" text-anchor="middle" font-family="'Share Tech Mono',monospace" font-size="8" fill="#00ffe7">SAKET.exe</text>
        <!-- Arms -->
        <ellipse cx="130" cy="270" rx="22" ry="45" fill="#d0d0e8" transform="rotate(-15 130 270)"/>
        <ellipse cx="118" cy="310" rx="16" ry="16" fill="#e8e8f0"/>
        <g>
          <ellipse cx="270" cy="250" rx="22" ry="45" fill="#d0d0e8" transform="rotate(15 270 250)">
            <animateTransform attributeName="transform" type="rotate" values="15 270 250;25 270 250;15 270 250" dur="1.5s" repeatCount="indefinite"/>
          </ellipse>
          <ellipse cx="285" cy="288" rx="16" ry="16" fill="#e8e8f0">
            <animateTransform attributeName="transform" type="rotate" values="0 285 288;10 285 288;0 285 288" dur="1.5s" repeatCount="indefinite"/>
          </ellipse>
        </g>
        <!-- Legs -->
        <ellipse cx="175" cy="355" rx="22" ry="45" fill="#c8c8e0" transform="rotate(-5 175 355)"/>
        <ellipse cx="225" cy="355" rx="22" ry="45" fill="#c8c8e0" transform="rotate(5 225 355)"/>
        <ellipse cx="170" cy="392" rx="24" ry="12" fill="#2d2d4a"/>
        <ellipse cx="230" cy="392" rx="24" ry="12" fill="#2d2d4a"/>
        <!-- Helmet -->
        <ellipse cx="200" cy="160" rx="72" ry="76" fill="#c8d8f8"/>
        <ellipse cx="200" cy="160" rx="68" ry="72" fill="#ddeeff"/>
        <ellipse cx="200" cy="162" rx="52" ry="54" fill="#050520"/>
        <ellipse cx="200" cy="162" rx="48" ry="50" fill="#0a0a30"/>
        <ellipse cx="188" cy="148" rx="16" ry="22" fill="rgba(255,255,255,.06)" transform="rotate(-15 188 148)"/>
        <path d="M178 140 Q182 134 188 138" stroke="rgba(255,255,255,.3)" stroke-width="2" fill="none" stroke-linecap="round"/>
        <!-- Eyes -->
        <ellipse cx="182" cy="155" rx="8" ry="9" fill="#00ffe7" opacity=".9">
          <animate attributeName="ry" values="9;2;9" dur="4s" begin="2s" repeatCount="indefinite"/>
        </ellipse>
        <ellipse cx="218" cy="155" rx="8" ry="9" fill="#00ffe7" opacity=".9">
          <animate attributeName="ry" values="9;2;9" dur="4s" begin="2s" repeatCount="indefinite"/>
        </ellipse>
        <ellipse cx="184" cy="157" rx="4" ry="5" fill="#002a25"/>
        <ellipse cx="220" cy="157" rx="4" ry="5" fill="#002a25"/>
        <circle cx="186" cy="153" r="2" fill="rgba(255,255,255,.5)"/>
        <circle cx="222" cy="153" r="2" fill="rgba(255,255,255,.5)"/>
        <path d="M190 170 Q200 178 210 170" stroke="rgba(0,255,231,.5)" stroke-width="2" fill="none" stroke-linecap="round"/>
        <!-- Helmet ring & antenna -->
        <ellipse cx="200" cy="100" rx="72" ry="16" fill="none" stroke="rgba(0,255,231,.4)" stroke-width="2"/>
        <line x1="200" y1="88" x2="200" y2="60" stroke="#d0d0e8" stroke-width="3" stroke-linecap="round"/>
        <circle cx="200" cy="55" r="8" fill="#ff2d78">
          <animate attributeName="r" values="8;12;8" dur="1s" repeatCount="indefinite"/>
          <animate attributeName="fill" values="#ff2d78;#ffd700;#ff2d78" dur="1s" repeatCount="indefinite"/>
        </circle>
        <ellipse cx="200" cy="160" rx="72" ry="76" fill="none" stroke="rgba(0,255,231,.2)" stroke-width="3">
          <animate attributeName="stroke-opacity" values=".2;.6;.2" dur="2s" repeatCount="indefinite"/>
        </ellipse>
        <!-- Floating code -->
        <text x="50" y="140" font-family="'Share Tech Mono',monospace" font-size="10" fill="rgba(0,255,231,.35)" transform="rotate(-20 50 140)">
          &lt;React/&gt;<animate attributeName="opacity" values=".35;.7;.35" dur="3s" repeatCount="indefinite"/>
        </text>
        <text x="300" y="200" font-family="'Share Tech Mono',monospace" font-size="10" fill="rgba(255,45,120,.4)" transform="rotate(15 300 200)">
          npm run dev<animate attributeName="opacity" values=".4;.8;.4" dur="2.5s" begin=".5s" repeatCount="indefinite"/>
        </text>
        <text x="40" y="320" font-family="'Share Tech Mono',monospace" font-size="9" fill="rgba(255,215,0,.3)">
          git push 🚀<animate attributeName="opacity" values=".3;.6;.3" dur="3.5s" begin="1s" repeatCount="indefinite"/>
        </text>
      </svg>
    </div>
  </div>

  <div class="scroll-hint">
    <span>SCROLL</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- ═══ ABOUT ═══ -->
<section id="about">
  <div class="sec-label reveal">PROFILE</div>
  <div class="sec-title reveal">About <span class="highlight">Me</span></div>

  <div class="about-grid">
    <div class="about-text reveal">
      <p>Hey! I'm <b>Saket Raj</b> — a passionate <b>Front-End Developer</b> from <b>Purnea, Bihar 🇮🇳</b>. I write code that lives at the intersection of clean design and solid engineering.</p>
      <p>Currently deep-diving into <b>Full Stack Development</b> via the <em>MERN Stack</em> — MongoDB, Express, React, and Node.js. Every project is a lesson; every bug is a boss level.</p>
      <p>I'm always up for <b>collaboration</b>, open-source contributions, or that collab that turns into something legendary. If you're building something cool — <em>let's talk.</em> 🔥</p>
      <p>When not coding: plotting my next project, exploring tech rabbit holes, and dreaming in JavaScript. <b>Working from home</b> and loving every minute. 🏠</p>
    </div>

    <div class="robot-scene reveal" style="position:relative">
      <div class="speech">console.log("Let's build! 🚀")</div>
      <svg class="robot-svg" viewBox="0 0 280 340" xmlns="http://www.w3.org/2000/svg">
        <ellipse cx="140" cy="330" rx="70" ry="10" fill="rgba(0,255,231,.15)"/>
        <rect x="70" y="150" width="140" height="130" rx="18" fill="#0f0f1a" stroke="#00ffe7" stroke-width="2"/>
        <rect x="70" y="150" width="140" height="130" rx="18" fill="none" stroke="rgba(0,255,231,.2)" stroke-width="6"/>
        <rect x="90" y="168" width="100" height="70" rx="8" fill="#050510" stroke="rgba(0,255,231,.3)" stroke-width="1"/>
        <circle cx="108" cy="185" r="7" fill="#ff2d78"><animate attributeName="opacity" values="1;.3;1" dur=".8s" repeatCount="indefinite"/></circle>
        <circle cx="130" cy="185" r="7" fill="#ffd700"><animate attributeName="opacity" values="1;.3;1" dur=".8s" begin=".27s" repeatCount="indefinite"/></circle>
        <circle cx="152" cy="185" r="7" fill="#00ffe7"><animate attributeName="opacity" values="1;.3;1" dur=".8s" begin=".54s" repeatCount="indefinite"/></circle>
        <rect x="90" y="200" width="100" height="30" rx="4" fill="#050508"/>
        <text x="140" y="220" text-anchor="middle" font-family="'Share Tech Mono',monospace" font-size="9" fill="#00ffe7">
          SAKET.DEV<animate attributeName="fill" values="#00ffe7;#ff2d78;#ffd700;#00ffe7" dur="3s" repeatCount="indefinite"/>
        </text>
        <rect x="30" y="155" width="38" height="100" rx="14" fill="#0f0f1a" stroke="#00ffe7" stroke-width="1.5"/>
        <circle cx="49" cy="265" r="14" fill="#1a1a2e" stroke="#00ffe7" stroke-width="1.5"/>
        <g>
          <rect x="212" y="145" width="38" height="100" rx="14" fill="#0f0f1a" stroke="#ff2d78" stroke-width="1.5">
            <animateTransform attributeName="transform" type="rotate" values="-5 231 165;10 231 165;-5 231 165" dur="1.2s" repeatCount="indefinite"/>
          </rect>
          <circle cx="231" cy="255" r="14" fill="#1a1a2e" stroke="#ff2d78" stroke-width="1.5">
            <animateTransform attributeName="transform" type="rotate" values="-5 231 165;10 231 165;-5 231 165" dur="1.2s" repeatCount="indefinite"/>
          </circle>
        </g>
        <rect x="90" y="278" width="38" height="55" rx="10" fill="#0f0f1a" stroke="#00ffe7" stroke-width="1.5"/>
        <rect x="152" y="278" width="38" height="55" rx="10" fill="#0f0f1a" stroke="#00ffe7" stroke-width="1.5"/>
        <rect x="82" y="328" width="52" height="14" rx="7" fill="#1a1a2e" stroke="rgba(0,255,231,.4)" stroke-width="1"/>
        <rect x="146" y="328" width="52" height="14" rx="7" fill="#1a1a2e" stroke="rgba(0,255,231,.4)" stroke-width="1"/>
        <rect x="122" y="118" width="36" height="34" rx="6" fill="#0d0d18" stroke="rgba(0,255,231,.3)" stroke-width="1"/>
        <rect x="70" y="40" width="140" height="84" rx="20" fill="#0f0f1a" stroke="#00ffe7" stroke-width="2"/>
        <rect x="70" y="40" width="140" height="84" rx="20" fill="none" stroke="rgba(0,255,231,.2)" stroke-width="8"/>
        <rect x="88" y="56" width="42" height="32" rx="8" fill="#050508" stroke="#00ffe7" stroke-width="1.5"/>
        <rect x="150" y="56" width="42" height="32" rx="8" fill="#050508" stroke="#00ffe7" stroke-width="1.5"/>
        <ellipse cx="109" cy="72" rx="14" ry="11" fill="#00ffe7" opacity=".9">
          <animate attributeName="ry" values="11;4;11" dur="3.5s" begin="1s" repeatCount="indefinite"/>
        </ellipse>
        <ellipse cx="171" cy="72" rx="14" ry="11" fill="#00ffe7" opacity=".9">
          <animate attributeName="ry" values="11;4;11" dur="3.5s" begin="1s" repeatCount="indefinite"/>
        </ellipse>
        <ellipse cx="109" cy="72" rx="7" ry="7" fill="#003330"/>
        <ellipse cx="171" cy="72" rx="7" ry="7" fill="#003330"/>
        <circle cx="112" cy="69" r="3" fill="rgba(255,255,255,.5)"/>
        <circle cx="174" cy="69" r="3" fill="rgba(255,255,255,.5)"/>
        <rect x="100" y="100" width="80" height="14" rx="7" fill="#050508" stroke="rgba(0,255,231,.3)" stroke-width="1"/>
        <rect x="103" y="103" width="18" height="8" rx="3" fill="#00ffe7" opacity=".8">
          <animate attributeName="width" values="18;12;18" dur=".5s" repeatCount="indefinite"/>
        </rect>
        <rect x="125" y="103" width="18" height="8" rx="3" fill="#ff2d78" opacity=".7">
          <animate attributeName="width" values="18;24;18" dur=".5s" begin=".25s" repeatCount="indefinite"/>
        </rect>
        <rect x="147" y="103" width="18" height="8" rx="3" fill="#ffd700" opacity=".6">
          <animate attributeName="width" values="18;10;18" dur=".5s" begin=".1s" repeatCount="indefinite"/>
        </rect>
        <rect x="169" y="103" width="8" height="8" rx="3" fill="#a855f7" opacity=".8"/>
        <line x1="140" y1="40" x2="140" y2="14" stroke="#d0d0e8" stroke-width="3" stroke-linecap="round"/>
        <circle cx="140" cy="10" r="7" fill="#ff2d78">
          <animate attributeName="r" values="7;10;7" dur="1.2s" repeatCount="indefinite"/>
        </circle>
        <circle cx="72" cy="100" r="5" fill="#00ffe7" opacity=".5"/>
        <circle cx="208" cy="100" r="5" fill="#00ffe7" opacity=".5"/>
      </svg>
      <div class="robot-glow"></div>
    </div>
  </div>
</section>

<!-- ═══ SKILLS ═══ -->
<section id="skills" style="background:rgba(0,255,231,.01)">
  <div class="sec-label reveal">CAPABILITIES</div>
  <div class="sec-title reveal">Tech <span class="highlight-pink">Stack</span></div>

  <div class="skills-outer reveal" id="skillsBox">
    <div class="skill-rows">
      <div class="skill-row">
        <div class="skill-icon-wrap">🌐</div>
        <div class="skill-info">
          <div class="skill-name">HTML5 <span class="skill-pct">92%</span></div>
          <div class="skill-bar"><div class="skill-fill" data-width="92"></div></div>
        </div>
      </div>
      <div class="skill-row">
        <div class="skill-icon-wrap">🎨</div>
        <div class="skill-info">
          <div class="skill-name">CSS3 / Animations <span class="skill-pct">88%</span></div>
          <div class="skill-bar"><div class="skill-fill pink" data-width="88"></div></div>
        </div>
      </div>
      <div class="skill-row">
        <div class="skill-icon-wrap">⚡</div>
        <div class="skill-info">
          <div class="skill-name">JavaScript (ES6+) <span class="skill-pct">80%</span></div>
          <div class="skill-bar"><div class="skill-fill gold" data-width="80"></div></div>
        </div>
      </div>
      <div class="skill-row">
        <div class="skill-icon-wrap">⚛️</div>
        <div class="skill-info">
          <div class="skill-name">React.js <span class="skill-pct">72%</span></div>
          <div class="skill-bar"><div class="skill-fill" data-width="72"></div></div>
        </div>
      </div>
      <div class="skill-row">
        <div class="skill-icon-wrap">🟢</div>
        <div class="skill-info">
          <div class="skill-name">Node.js / Express <span class="skill-pct">55%</span></div>
          <div class="skill-bar"><div class="skill-fill pink" data-width="55"></div></div>
        </div>
      </div>
      <div class="skill-row">
        <div class="skill-icon-wrap">🍃</div>
        <div class="skill-info">
          <div class="skill-name">MongoDB <span class="skill-pct">50%</span></div>
          <div class="skill-bar"><div class="skill-fill gold" data-width="50"></div></div>
        </div>
      </div>
      <div class="skill-row">
        <div class="skill-icon-wrap">🐍</div>
        <div class="skill-info">
          <div class="skill-name">Python <span class="skill-pct">45%</span></div>
          <div class="skill-bar"><div class="skill-fill" data-width="45"></div></div>
        </div>
      </div>
      <div class="skill-row">
        <div class="skill-icon-wrap">🐙</div>
        <div class="skill-info">
          <div class="skill-name">Git &amp; GitHub <span class="skill-pct">85%</span></div>
          <div class="skill-bar"><div class="skill-fill pink" data-width="85"></div></div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ═══ BUILDING ═══ -->
<section id="building">
  <div class="sec-label reveal">WIP</div>
  <div class="sec-title reveal">Currently <span class="highlight">Building</span></div>

  <div class="build-grid">
    <div class="build-card reveal">
      <span class="emoji">🛒</span>
      <div class="build-status status-live">🔴 ACTIVE BUILD</div>
      <div class="build-title">E-Commerce Platform</div>
      <div class="build-desc">Full-featured React shopping app with product listings, cart, checkout flow, user auth. MERN integration in progress. The one that'll make recruits DM. 💥</div>
      <div class="prog-bar"><div class="prog-fill" style="width:65%"></div></div>
      <div class="prog-label"><span>progress</span><span>65%</span></div>
    </div>
    <div class="build-card reveal">
      <span class="emoji" style="animation-delay:.5s">🌐</span>
      <div class="build-status status-wip">🟡 LEARNING</div>
      <div class="build-title">MERN Mastery Track</div>
      <div class="build-desc">Methodically working through MongoDB, Express, React, Node.js. Building real projects at each step. No tutorials without implementation — building to learn. 🔥</div>
      <div class="prog-bar"><div class="prog-fill" style="width:48%"></div></div>
      <div class="prog-label"><span>progress</span><span>48%</span></div>
    </div>
  </div>
</section>

<!-- ═══ WORK ═══ -->
<section id="work">
  <div class="sec-label reveal">PORTFOLIO</div>
  <div class="sec-title reveal"><span class="highlight-pink">Selected</span> Work</div>

  <div class="proj-grid">
    <div class="proj-card reveal">
      <div class="proj-tag-row"><span class="ptag ptag-n">HTML</span><span class="ptag ptag-g">CSS</span><span class="ptag ptag-p">JS</span></div>
      <div class="proj-title">⚡ To-Do List App</div>
      <div class="proj-desc">Minimal, elegant task manager. Clean UI, smooth interactions, local persistence. Proof that fundamentals done right are always impressive.</div>
      <a href="https://github.com/CodewithSaket/To-Do-List" target="_blank" class="proj-link">View Repo →</a>
    </div>
    <div class="proj-card reveal">
      <div class="proj-tag-row"><span class="ptag ptag-n">React</span><span class="ptag ptag-g">Node</span><span class="ptag ptag-p">MongoDB</span></div>
      <div class="proj-title">🛒 E-Commerce UI</div>
      <div class="proj-desc">React-powered shopping experience. Component-based architecture, responsive layout, smooth UX. In active development — watch this space. 🚀</div>
      <a href="https://github.com/CodewithSaket" target="_blank" class="proj-link">Follow Progress →</a>
    </div>
    <div class="proj-card reveal">
      <div class="proj-tag-row"><span class="ptag ptag-g">11 Repos</span><span class="ptag ptag-p">Open Source</span></div>
      <div class="proj-title">🗂 All Repositories</div>
      <div class="proj-desc">11 repositories and counting — experiments, clones, originals, and everything in between. Every commit represents a skill upgraded.</div>
      <a href="https://github.com/CodewithSaket?tab=repositories" target="_blank" class="proj-link">Browse All →</a>
    </div>
  </div>
</section>

<!-- ═══ CONNECT ═══ -->
<section id="connect">
  <div class="sec-label reveal">SOCIALS</div>
  <div class="sec-title reveal">Let's <span class="highlight">Connect</span></div>

  <div class="connect-scene">
    <div class="connect-links reveal">
      <a href="https://github.com/CodewithSaket" target="_blank" class="link-card">
        <div class="link-icon">🐙</div>
        <div class="link-info"><span class="link-name">GitHub</span><span class="link-sub">@CodewithSaket</span></div>
        <div class="link-arrow">↗</div>
      </a>
      <a href="https://www.linkedin.com/in/-saket-raj/" target="_blank" class="link-card">
        <div class="link-icon">💼</div>
        <div class="link-info"><span class="link-name">LinkedIn</span><span class="link-sub">in/-saket-raj</span></div>
        <div class="link-arrow">↗</div>
      </a>
      <a href="https://www.instagram.com/_sakettomar/" target="_blank" class="link-card">
        <div class="link-icon">📸</div>
        <div class="link-info"><span class="link-name">Instagram</span><span class="link-sub">@_sakettomar</span></div>
        <div class="link-arrow">↗</div>
      </a>
      <a href="mailto:saketraj@example.com" class="link-card">
        <div class="link-icon">✉️</div>
        <div class="link-info"><span class="link-name">Email</span><span class="link-sub">Drop a message</span></div>
        <div class="link-arrow">↗</div>
      </a>
    </div>

    <div class="reveal" style="display:flex;justify-content:center;align-items:center">
      <svg class="coder-svg" viewBox="0 0 300 340" xmlns="http://www.w3.org/2000/svg">
        <rect x="20" y="270" width="260" height="8" rx="4" fill="#0f0f1a" stroke="rgba(0,255,231,.3)" stroke-width="1"/>
        <ellipse cx="150" cy="278" rx="130" ry="10" fill="rgba(0,255,231,.05)"/>
        <rect x="60" y="130" width="180" height="130" rx="10" fill="#050510" stroke="#00ffe7" stroke-width="2"/>
        <rect x="65" y="135" width="170" height="120" rx="7" fill="#020208"/>
        <rect x="60" y="130" width="180" height="130" rx="10" fill="none" stroke="rgba(0,255,231,.15)" stroke-width="8"/>
        <text x="74" y="154" font-family="'Share Tech Mono',monospace" font-size="9" fill="rgba(255,45,120,.8)">&lt;div className="hero"&gt;</text>
        <text x="80" y="167" font-family="'Share Tech Mono',monospace" font-size="9" fill="rgba(0,255,231,.7)">  &lt;h1&gt;Saket Raj&lt;/h1&gt;</text>
        <text x="80" y="180" font-family="'Share Tech Mono',monospace" font-size="9" fill="rgba(168,85,247,.8)">  &lt;p&gt;Full Stack Dev&lt;/p&gt;</text>
        <text x="74" y="193" font-family="'Share Tech Mono',monospace" font-size="9" fill="rgba(255,45,120,.8)">&lt;/div&gt;</text>
        <text x="74" y="208" font-family="'Share Tech Mono',monospace" font-size="9" fill="rgba(255,215,0,.6)">// building the future 🚀</text>
        <rect x="74" y="214" width="6" height="11" fill="#00ffe7" rx="1">
          <animate attributeName="opacity" values="1;0;1" dur=".8s" repeatCount="indefinite"/>
        </rect>
        <rect x="65" y="135" width="170" height="2" fill="rgba(0,255,231,.08)" opacity=".5">
          <animate attributeName="y" values="135;255;135" dur="3s" repeatCount="indefinite"/>
        </rect>
        <rect x="135" y="260" width="30" height="12" rx="3" fill="#1a1a2e" stroke="rgba(0,255,231,.2)" stroke-width="1"/>
        <rect x="120" y="270" width="60" height="6" rx="3" fill="#1a1a2e" stroke="rgba(0,255,231,.2)" stroke-width="1"/>
        <rect x="80" y="285" width="140" height="30" rx="6" fill="#0f0f1a" stroke="rgba(0,255,231,.3)" stroke-width="1.5"/>
        <g fill="rgba(0,255,231,.25)">
          <rect x="86" y="290" width="12" height="8" rx="2"/>
          <rect x="101" y="290" width="12" height="8" rx="2"/>
          <rect x="116" y="290" width="12" height="8" rx="2"/>
          <rect x="131" y="290" width="12" height="8" rx="2"/>
          <rect x="146" y="290" width="12" height="8" rx="2"/>
          <rect x="161" y="290" width="12" height="8" rx="2"/>
          <rect x="176" y="290" width="12" height="8" rx="2"/>
          <rect x="191" y="290" width="12" height="8" rx="2"/>
          <rect x="100" y="301" width="100" height="8" rx="2" fill="rgba(0,255,231,.15)"/>
        </g>
        <!-- Person -->
        <ellipse cx="60" cy="220" rx="30" ry="40" fill="#1a1a2e" stroke="rgba(255,45,120,.4)" stroke-width="1"/>
        <circle cx="60" cy="165" r="28" fill="#f5c5a3"/>
        <ellipse cx="60" cy="148" rx="28" ry="12" fill="#2d1810"/>
        <rect x="32" y="148" width="12" height="18" rx="6" fill="#2d1810"/>
        <rect x="56" y="136" width="8" height="16" rx="4" fill="#3d2018"/>
        <circle cx="50" cy="168" r="4" fill="#1a0a00"/>
        <circle cx="70" cy="168" r="4" fill="#1a0a00"/>
        <circle cx="51" cy="166" r="1.5" fill="white"/>
        <circle cx="71" cy="166" r="1.5" fill="white"/>
        <path d="M47 163 Q50 160 53 163" stroke="#333" stroke-width="1.5" fill="none"/>
        <path d="M67 163 Q70 160 73 163" stroke="#333" stroke-width="1.5" fill="none"/>
        <path d="M53 178 Q60 184 67 178" stroke="#c0906a" stroke-width="2" fill="none" stroke-linecap="round"/>
        <line x1="40" y1="200" x2="95" y2="285" stroke="#f5c5a3" stroke-width="10" stroke-linecap="round"/>
        <line x1="80" y1="200" x2="130" y2="285" stroke="#f5c5a3" stroke-width="10" stroke-linecap="round">
          <animateTransform attributeName="transform" type="rotate" values="-3 80 200;3 80 200;-3 80 200" dur=".4s" repeatCount="indefinite"/>
        </line>
        <!-- Coffee -->
        <rect x="10" y="260" width="28" height="22" rx="4" fill="#3d2018" stroke="rgba(255,215,0,.4)" stroke-width="1"/>
        <rect x="10" y="260" width="28" height="8" rx="3" fill="#5d3020"/>
        <path d="M18 256 Q15 248 18 240" stroke="rgba(255,255,255,.2)" stroke-width="2" fill="none" stroke-linecap="round">
          <animate attributeName="opacity" values=".2;.6;.2" dur="2s" repeatCount="indefinite"/>
        </path>
        <path d="M25 254 Q22 244 25 236" stroke="rgba(255,255,255,.15)" stroke-width="2" fill="none" stroke-linecap="round">
          <animate attributeName="opacity" values=".15;.5;.15" dur="2.5s" begin=".5s" repeatCount="indefinite"/>
        </path>
        <text x="16" y="275" font-family="'Share Tech Mono',monospace" font-size="7" fill="rgba(255,215,0,.6)">☕</text>
      </svg>
    </div>
  </div>
</section>

<!-- ═══ FOOTER ═══ -->
<footer>
  <div class="footer-ascii">
█  CODE WITH SAKET  ·  SAKET RAJ  ·  PURNEA, BIHAR  ·  MERN STACK  ·  2025  █
  </div>
  <div class="footer-text">⟨ KEEP BUILDING · KEEP SHIPPING · NEVER STOP LEARNING /⟩</div>
  <div class="footer-sub">Made with ❤️ + ☕ + 🎧 by Saket Raj · CodewithSaket</div>
</footer>

<script>
// ══ STARS ══
const sc = document.getElementById('stars');
const sctx = sc.getContext('2d');
function resizeStars(){sc.width=window.innerWidth;sc.height=window.innerHeight;}
resizeStars();
window.addEventListener('resize',resizeStars);

const stars=Array.from({length:200},()=>({
  x:Math.random()*sc.width,y:Math.random()*sc.height,
  r:Math.random()*1.8+.2,speed:Math.random()*.3+.05,
  opacity:Math.random(),opSpeed:Math.random()*.01+.003,opDir:1,
  color:['#00ffe7','#ff2d78','#ffd700','#a855f7','#ffffff'][Math.floor(Math.random()*5)]
}));

function animStars(){
  sctx.clearRect(0,0,sc.width,sc.height);
  stars.forEach(s=>{
    s.opacity+=s.opSpeed*s.opDir;
    if(s.opacity>=1||s.opacity<=0)s.opDir*=-1;
    sctx.beginPath();
    sctx.arc(s.x,s.y,s.r,0,Math.PI*2);
    sctx.fillStyle=s.color;
    sctx.globalAlpha=s.opacity*.7;
    sctx.fill();
    sctx.globalAlpha=1;
  });
  requestAnimationFrame(animStars);
}
animStars();

// ══ CUSTOM CURSOR ══
const curCanvas=document.getElementById('curCanvas');
const curCtx=curCanvas.getContext('2d');
const curDiv=document.getElementById('cur');
const particles=[];
let cursorReady=false;

document.addEventListener('mousemove',e=>{
  if(!cursorReady){
    cursorReady=true;
    curDiv.classList.add('active');
    document.body.classList.add('cursor-ready');
  }
  curDiv.style.left=(e.clientX-30)+'px';
  curDiv.style.top=(e.clientY-30)+'px';
  for(let i=0;i<3;i++){
    particles.push({
      x:30,y:30,
      vx:(Math.random()-.5)*4,vy:(Math.random()-.5)*4,
      life:1,decay:Math.random()*.04+.02,
      r:Math.random()*3+1,
      color:['#00ffe7','#ff2d78','#ffd700','#a855f7'][Math.floor(Math.random()*4)]
    });
  }
});

function animCursor(){
  curCtx.clearRect(0,0,60,60);
  curCtx.beginPath();
  curCtx.arc(30,30,5,0,Math.PI*2);
  curCtx.fillStyle='#00ffe7';
  curCtx.shadowColor='#00ffe7';
  curCtx.shadowBlur=12;
  curCtx.fill();
  curCtx.shadowBlur=0;
  curCtx.beginPath();
  curCtx.arc(30,30,14,0,Math.PI*2);
  curCtx.strokeStyle='rgba(0,255,231,.4)';
  curCtx.lineWidth=1;
  curCtx.stroke();
  particles.forEach((p,i)=>{
    p.x+=p.vx;p.y+=p.vy;p.life-=p.decay;
    if(p.life<=0){particles.splice(i,1);return;}
    curCtx.beginPath();
    curCtx.arc(p.x,p.y,p.r*p.life,0,Math.PI*2);
    curCtx.fillStyle=p.color;
    curCtx.globalAlpha=p.life;
    curCtx.fill();
    curCtx.globalAlpha=1;
  });
  requestAnimationFrame(animCursor);
}
animCursor();

// ══ SCROLL REVEAL ══
const reveals=document.querySelectorAll('.reveal');
const revObs=new IntersectionObserver(entries=>{
  entries.forEach((e,idx)=>{
    if(e.isIntersecting){
      setTimeout(()=>e.target.classList.add('visible'),(idx%5)*100);
    }
  });
},{threshold:.08});
reveals.forEach(r=>revObs.observe(r));

// ══ SKILL BARS — fixed: use width%, not scaleX ══
const skillBox=document.getElementById('skillsBox');
let skillsAnimated=false;

function animateSkills(){
  if(skillsAnimated)return;
  skillsAnimated=true;
  document.querySelectorAll('.skill-fill').forEach((el,i)=>{
    const target=el.dataset.width||'0';
    setTimeout(()=>{
      el.style.width=target+'%';
    },i*80);
  });
}

const skillObs=new IntersectionObserver(entries=>{
  if(entries[0].isIntersecting){
    animateSkills();
    skillObs.disconnect();
  }
},{threshold:.2});
skillObs.observe(skillBox);

// Also trigger if already in view on load
window.addEventListener('load',()=>{
  const rect=skillBox.getBoundingClientRect();
  if(rect.top<window.innerHeight)animateSkills();
});

// ══ CLICK EXPLOSION ══
document.addEventListener('click',e=>{
  for(let i=0;i<20;i++){
    const p=document.createElement('div');
    const angle=(i/20)*Math.PI*2;
    const vel=Math.random()*80+40;
    const color=['#00ffe7','#ff2d78','#ffd700','#a855f7','#38bdf8'][Math.floor(Math.random()*5)];
    p.style.cssText=`
      position:fixed;left:${e.clientX}px;top:${e.clientY}px;
      width:${Math.random()*5+2}px;height:${Math.random()*5+2}px;
      background:${color};border-radius:50%;
      pointer-events:none;z-index:9000;
      transition:all .6s cubic-bezier(.25,.46,.45,.94);
      box-shadow:0 0 6px ${color};
    `;
    document.body.appendChild(p);
    requestAnimationFrame(()=>{
      p.style.transform=`translate(${Math.cos(angle)*vel}px,${Math.sin(angle)*vel}px)`;
      p.style.opacity='0';
    });
    setTimeout(()=>p.remove(),700);
  }
});

// ══ CURSOR HOVER EFFECTS ══
document.querySelectorAll('a,button,.skill-icon-wrap,.build-card,.proj-card,.link-card').forEach(el=>{
  el.addEventListener('mouseenter',()=>{
    curCanvas.style.transform='scale(1.8)';
    curCanvas.style.filter='hue-rotate(180deg)';
  });
  el.addEventListener('mouseleave',()=>{
    curCanvas.style.transform='scale(1)';
    curCanvas.style.filter='none';
  });
});
</script>
</body>
</html>
