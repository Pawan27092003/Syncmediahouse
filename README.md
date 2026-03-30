<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sync Media House — We Create. We Grow. We Sync.</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@300;400;500;600&family=Playfair+Display:ital,wght@1,400;1,600&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
[data-theme="dark"]{--bg:#080808;--deep:#0D0D0D;--card:#111111;--border:#1E1E1E;--white:#F5F5F0;--muted:#6B6B6B;--nav-bg:rgba(8,8,8,.94);--stroke:rgba(245,245,240,.25);--hero-desc:rgba(245,245,240,.55);--ob:rgba(245,245,240,.2);--oc:rgba(245,245,240,.5);--gl:rgba(255,255,255,.018);--no:.5}
[data-theme="light"]{--bg:#F7F4EF;--deep:#EEEAE3;--card:#FFFFFF;--border:#E0D8CE;--white:#1A1714;--muted:#7A7268;--nav-bg:rgba(247,244,239,.95);--stroke:rgba(26,23,20,.22);--hero-desc:rgba(26,23,20,.6);--ob:rgba(26,23,20,.2);--oc:rgba(26,23,20,.6);--gl:rgba(0,0,0,.04);--no:.2}
:root{--gold:#E8B84B;--accent:#FF4D2E;--wa:#25D366;--display:'Bebas Neue',sans-serif;--body:'Outfit',sans-serif;--serif:'Playfair Display',Georgia,serif}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--white);font-family:var(--body);font-weight:300;overflow-x:hidden;cursor:none;transition:background .4s,color .4s}
body::after{content:'';position:fixed;inset:0;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.04'/%3E%3C/svg%3E");pointer-events:none;z-index:9000;opacity:var(--no);transition:opacity .4s}

/* CURSOR */
#cur{position:fixed;width:8px;height:8px;background:var(--gold);border-radius:50%;pointer-events:none;z-index:9999;transform:translate(-50%,-50%);transition:width .25s,height .25s}
#cur-ring{position:fixed;width:36px;height:36px;border:1px solid rgba(232,184,75,.4);border-radius:50%;pointer-events:none;z-index:9998;transform:translate(-50%,-50%);transition:width .35s,height .35s}

/* LOADER */
#loader{position:fixed;inset:0;background:var(--bg);z-index:8999;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:24px;transition:opacity .8s .2s,visibility .8s .2s}
#loader.done{opacity:0;visibility:hidden;pointer-events:none}
.loader-text{font-family:var(--display);font-size:clamp(2rem,8vw,7rem);letter-spacing:.05em;color:var(--white);overflow:hidden;text-align:center}
.loader-text span{display:inline-block;animation:lSlide .6s cubic-bezier(.16,1,.3,1) both}
.loader-text span:nth-child(2){animation-delay:.08s}
.loader-text span:nth-child(3){animation-delay:.16s}
.lbar-wrap{width:min(200px,60vw);height:1px;background:var(--border)}
.lbar{height:1px;background:var(--gold);width:0;animation:lBarAnim 1.8s cubic-bezier(.4,0,.2,1) forwards}
@keyframes lSlide{from{transform:translateY(110%)}to{transform:translateY(0)}}
@keyframes lBarAnim{to{width:100%}}

/* FLOATING WHATSAPP */
#wa-float{position:fixed;bottom:24px;right:20px;z-index:600;width:56px;height:56px;background:var(--wa);border-radius:50%;display:flex;align-items:center;justify-content:center;box-shadow:0 4px 24px rgba(37,211,102,.4);text-decoration:none;transition:transform .3s;animation:waPulse 3s ease-in-out infinite}
#wa-float:hover{transform:scale(1.1)}
#wa-float svg{width:26px;height:26px;fill:white}
.wa-tip{position:absolute;right:64px;white-space:nowrap;background:var(--card);color:var(--white);font-size:.7rem;padding:7px 12px;border:1px solid var(--border);opacity:0;pointer-events:none;transition:opacity .3s;font-family:var(--body)}
#wa-float:hover .wa-tip{opacity:1}
@keyframes waPulse{0%,100%{box-shadow:0 4px 24px rgba(37,211,102,.4)}50%{box-shadow:0 4px 36px rgba(37,211,102,.6)}}

/* THEME TOGGLE */
#tt{position:fixed;top:50%;transform:translateY(-50%);right:0;z-index:600;width:36px;height:80px;background:var(--card);border:1px solid var(--border);border-right:none;border-radius:8px 0 0 8px;cursor:pointer;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;padding:10px 8px;transition:background .3s}
#tt:hover{border-color:var(--gold)}
#tt .tt-icon{font-size:1rem;line-height:1;transition:opacity .3s}
#tt .tt-label{font-size:.45rem;letter-spacing:.1em;text-transform:uppercase;color:var(--muted);writing-mode:vertical-rl;transform:rotate(180deg)}
[data-theme="dark"] #tt .sun{opacity:.4}
[data-theme="dark"] #tt .moon{opacity:1}
[data-theme="light"] #tt .sun{opacity:1}
[data-theme="light"] #tt .moon{opacity:.3}

/* NAV */
nav{position:fixed;top:0;left:0;right:0;z-index:500;display:flex;justify-content:space-between;align-items:center;padding:18px 56px;transition:background .4s,border-color .4s;border-bottom:1px solid transparent}
nav.scrolled{background:var(--nav-bg);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);border-color:var(--border)}
.nav-brand{text-decoration:none;display:flex;flex-direction:column;gap:1px}
.nav-brand-top{font-family:var(--display);font-size:1.35rem;letter-spacing:.08em;color:var(--white);line-height:1}
.nav-brand-sub{font-size:.5rem;letter-spacing:.25em;text-transform:uppercase;color:var(--gold)}
.nav-links{display:flex;gap:28px;list-style:none}
.nav-links a{font-size:.68rem;letter-spacing:.14em;text-transform:uppercase;color:var(--muted);text-decoration:none;position:relative;transition:color .3s}
.nav-links a::after{content:'';position:absolute;bottom:-4px;left:0;width:0;height:1px;background:var(--gold);transition:width .4s cubic-bezier(.4,0,.2,1)}
.nav-links a:hover{color:var(--white)}
.nav-links a:hover::after{width:100%}
.nav-right{display:flex;align-items:center;gap:10px}
.nav-wa{display:flex;align-items:center;gap:7px;padding:8px 18px;background:var(--wa);color:#fff;font-size:.66rem;font-weight:500;letter-spacing:.08em;text-transform:uppercase;text-decoration:none;transition:opacity .3s;white-space:nowrap}
.nav-wa:hover{opacity:.88}
.nav-wa svg{width:13px;height:13px;fill:white;flex-shrink:0}
/* Hamburger */
.ham{display:none;flex-direction:column;gap:5px;cursor:pointer;padding:4px;background:none;border:none}
.ham span{display:block;width:22px;height:1.5px;background:var(--white);transition:transform .35s,opacity .35s}
.ham.open span:nth-child(1){transform:translateY(6.5px) rotate(45deg)}
.ham.open span:nth-child(2){opacity:0}
.ham.open span:nth-child(3){transform:translateY(-6.5px) rotate(-45deg)}
/* Mobile Menu */
.mob-menu{position:fixed;inset:0;background:var(--bg);z-index:490;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:32px;transform:translateY(-100%);transition:transform .45s cubic-bezier(.4,0,.2,1);pointer-events:none}
.mob-menu.open{transform:translateY(0);pointer-events:all}
.mob-menu a{font-family:var(--display);font-size:clamp(2rem,9vw,3.5rem);letter-spacing:.06em;color:var(--white);text-decoration:none;transition:color .3s}
.mob-menu a:hover{color:var(--gold)}
.mob-wa{display:flex!important;align-items:center;gap:10px;background:var(--wa)!important;color:white!important;padding:14px 32px;border-radius:4px;font-size:1.1rem!important;letter-spacing:.05em!important}
.mob-wa svg{width:20px;height:20px;fill:white}

/* HERO */
.hero{min-height:100svh;display:flex;flex-direction:column;justify-content:flex-end;padding:0 56px 90px;position:relative;overflow:hidden}
.hero-bg{position:absolute;inset:0;background:radial-gradient(ellipse 80% 60% at 70% 40%,rgba(232,184,75,.07) 0%,transparent 70%),radial-gradient(ellipse 50% 40% at 20% 80%,rgba(255,77,46,.05) 0%,transparent 60%);pointer-events:none}
[data-theme="light"] .hero-bg{background:radial-gradient(ellipse 80% 60% at 70% 40%,rgba(232,184,75,.13) 0%,transparent 70%),radial-gradient(ellipse 50% 40% at 20% 80%,rgba(255,77,46,.08) 0%,transparent 60%)}
.hero-grid{position:absolute;inset:0;background-image:linear-gradient(var(--gl) 1px,transparent 1px),linear-gradient(90deg,var(--gl) 1px,transparent 1px);background-size:80px 80px;pointer-events:none}
.hero-label{font-size:.62rem;letter-spacing:.28em;text-transform:uppercase;color:var(--gold);margin-bottom:24px;opacity:0;animation:fadeUp .7s .5s both}
.hero-title{font-family:var(--display);font-size:clamp(3.5rem,12vw,14rem);letter-spacing:.02em;line-height:.92;opacity:0;animation:fadeUp .8s .7s both}
.hero-title-line2{display:block;color:transparent;-webkit-text-stroke:1px var(--stroke);font-size:clamp(2.8rem,10vw,12rem)}
.hero-title em{font-family:var(--serif);font-style:italic;font-size:clamp(1.2rem,3.5vw,4rem);color:var(--gold);display:block;font-weight:400;letter-spacing:.02em;margin-top:6px;-webkit-text-stroke:0}
.hero-bottom{display:flex;justify-content:space-between;align-items:flex-end;margin-top:48px;opacity:0;animation:fadeUp .8s 1s both;gap:28px;flex-wrap:wrap}
.hero-desc{max-width:400px;font-size:.95rem;color:var(--hero-desc);line-height:1.8}
.hero-ctas{display:flex;flex-direction:column;gap:10px;align-items:flex-end;flex-shrink:0}
.btn-gold{display:inline-flex;align-items:center;gap:10px;padding:14px 34px;background:var(--gold);color:#080808;font-family:var(--body);font-size:.73rem;font-weight:600;letter-spacing:.11em;text-transform:uppercase;text-decoration:none;position:relative;overflow:hidden;transition:transform .2s;cursor:pointer;border:none;white-space:nowrap}
.btn-gold::before{content:'';position:absolute;inset:0;background:var(--accent);transform:translateX(-101%);transition:transform .45s cubic-bezier(.4,0,.2,1)}
.btn-gold:hover{transform:translateY(-2px)}
.btn-gold:hover::before{transform:translateX(0)}
.btn-gold span{position:relative;z-index:1}
.btn-wa{display:inline-flex;align-items:center;gap:9px;padding:13px 30px;background:var(--wa);color:#fff;font-family:var(--body);font-size:.73rem;font-weight:600;letter-spacing:.09em;text-transform:uppercase;text-decoration:none;transition:transform .2s,box-shadow .2s;white-space:nowrap}
.btn-wa svg{width:15px;height:15px;fill:white;flex-shrink:0}
.btn-wa:hover{transform:translateY(-2px);box-shadow:0 6px 24px rgba(37,211,102,.35)}
.btn-outline{display:inline-flex;align-items:center;gap:9px;padding:13px 28px;border:1px solid var(--ob);font-size:.7rem;letter-spacing:.1em;text-transform:uppercase;color:var(--oc);text-decoration:none;transition:border-color .3s,color .3s;white-space:nowrap}
.btn-outline:hover{border-color:var(--white);color:var(--white)}
.scroll-ind{position:absolute;bottom:28px;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;align-items:center;gap:8px;opacity:0;animation:fadeIn 1s 1.8s both}
.scroll-ind span{font-size:.55rem;letter-spacing:.22em;text-transform:uppercase;color:var(--muted)}
.scroll-wheel{width:20px;height:32px;border:1px solid var(--ob);border-radius:10px;display:flex;justify-content:center;padding-top:5px}
.scroll-dot{width:3px;height:5px;background:var(--gold);border-radius:2px;animation:sDot 2s ease-in-out infinite}
@keyframes sDot{0%{transform:translateY(0);opacity:1}100%{transform:translateY(12px);opacity:0}}

/* TICKER */
.ticker{background:var(--gold);padding:12px 0;overflow:hidden;white-space:nowrap}
.ticker-track{display:inline-flex;animation:tick 22s linear infinite}
.ti{font-family:var(--display);font-size:.95rem;letter-spacing:.1em;color:#080808;padding:0 32px}
.td{color:var(--accent);margin-right:32px}
@keyframes tick{from{transform:translateX(0)}to{transform:translateX(-50%)}}

/* SECTIONS */
section{padding:100px 56px;position:relative}
.ey{display:flex;align-items:center;gap:14px;margin-bottom:18px}
.ey-line{width:28px;height:1px;background:var(--gold)}
.ey-text{font-size:.58rem;letter-spacing:.26em;text-transform:uppercase;color:var(--gold)}
.sec-title{font-family:var(--display);font-size:clamp(2rem,4.5vw,4.5rem);letter-spacing:.04em;line-height:1.05;margin-bottom:14px}
.sec-sub{font-size:.9rem;color:var(--muted);line-height:1.8;max-width:540px}

/* ABOUT */
.about-inner{display:grid;grid-template-columns:1fr 1fr;gap:68px;align-items:start;margin-top:60px}
.about-stmt{font-family:var(--serif);font-style:italic;font-size:clamp(1.2rem,2vw,1.8rem);color:var(--white);line-height:1.6;margin-bottom:24px;opacity:.88}
.about-stmt strong{color:var(--gold);font-weight:400}
.about-body{font-size:.88rem;color:var(--muted);line-height:1.9;margin-bottom:16px}
.about-ctas{display:flex;gap:12px;margin-top:32px;flex-wrap:wrap}
.about-stats{display:grid;grid-template-columns:1fr 1fr;gap:2px}
.astat{background:var(--card);padding:28px 22px;position:relative;overflow:hidden;transition:background .3s}
.astat::before{content:'';position:absolute;top:0;left:0;width:2px;height:0;background:var(--gold);transition:height .6s cubic-bezier(.4,0,.2,1)}
.astat:hover::before{height:100%}
.astat-num{font-family:var(--display);font-size:2.8rem;color:var(--white);line-height:1}
.astat-num sup{font-size:1.2rem;vertical-align:super;color:var(--gold)}
.astat-label{font-size:.62rem;letter-spacing:.14em;text-transform:uppercase;color:var(--muted);margin-top:6px}

/* SERVICES */
.svc-bg{background:var(--deep)}
.svc-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:2px;margin-top:60px}
.svc-card{background:var(--card);padding:40px 28px;position:relative;overflow:hidden;cursor:pointer;transition:background .4s}
.svc-card::after{content:'';position:absolute;inset:0;background:linear-gradient(135deg,var(--gold) 0%,var(--accent) 100%);opacity:0;transition:opacity .5s}
.svc-card:hover::after{opacity:1}
.svc-card:hover .sc-num,.svc-card:hover .sc-title,.svc-card:hover .sc-desc,.svc-card:hover .sc-icon{color:#080808}
.svc-card:hover .sc-feat li{color:rgba(8,8,8,.7);border-color:rgba(8,8,8,.12)}
.sc-num{font-family:var(--display);font-size:3.2rem;color:var(--border);line-height:1;margin-bottom:24px;position:relative;z-index:1;transition:color .4s}
.sc-icon{font-size:1.7rem;margin-bottom:14px;position:relative;z-index:1;transition:color .4s;color:var(--gold)}
.sc-title{font-family:var(--display);font-size:1.5rem;letter-spacing:.04em;line-height:1.1;margin-bottom:12px;position:relative;z-index:1;transition:color .4s}
.sc-desc{font-size:.78rem;color:var(--muted);line-height:1.8;position:relative;z-index:1;transition:color .4s}
.sc-feat{list-style:none;margin-top:16px;position:relative;z-index:1}
.sc-feat li{font-size:.7rem;color:var(--muted);padding:5px 0;border-bottom:1px solid var(--border);letter-spacing:.03em;transition:color .4s,border-color .4s}

/* GALLERY */
.gallery-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:3px;margin-top:60px}
.gal-item{position:relative;overflow:hidden;background:var(--card);cursor:pointer}
.gal-item:nth-child(1){grid-column:1/3;aspect-ratio:16/9}
.gal-item:nth-child(2){aspect-ratio:4/5}
.gal-item:nth-child(3){aspect-ratio:1}
.gal-item:nth-child(4){aspect-ratio:1}
.gal-item:nth-child(5){grid-column:2/4;aspect-ratio:16/8}
.gal-item:nth-child(6){aspect-ratio:4/3}
.gal-img{width:100%;height:100%;object-fit:cover;display:block;transition:transform .7s cubic-bezier(.4,0,.2,1),filter .5s}
.gal-item:hover .gal-img{transform:scale(1.07);filter:brightness(.7)}
.gal-ov{position:absolute;inset:0;background:linear-gradient(to top,rgba(0,0,0,.75) 0%,transparent 55%);opacity:0;transition:opacity .4s;display:flex;align-items:flex-end;padding:20px}
.gal-item:hover .gal-ov{opacity:1}
.gal-label{font-family:var(--display);font-size:1rem;color:white;letter-spacing:.06em}

/* PROCESS */
.proc-bg{background:var(--deep)}
.proc-steps{display:grid;grid-template-columns:repeat(5,1fr);gap:0;margin-top:64px;position:relative}
.proc-steps::before{content:'';position:absolute;top:24px;left:calc(10% + 26px);right:calc(10% + 26px);height:1px;background:var(--border)}
.proc-step{display:flex;flex-direction:column;align-items:center;text-align:center;padding:0 14px;position:relative}
.ps-c{width:48px;height:48px;border:1px solid var(--border);border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:var(--display);font-size:1rem;color:var(--muted);margin-bottom:20px;position:relative;z-index:1;background:var(--deep);transition:border-color .3s,color .3s,background .3s}
.proc-step:hover .ps-c{border-color:var(--gold);color:var(--gold);background:var(--card)}
.ps-title{font-family:var(--display);font-size:.95rem;letter-spacing:.06em;margin-bottom:8px}
.ps-desc{font-size:.72rem;color:var(--muted);line-height:1.7}

/* PORTFOLIO */
.port-grid{margin-top:60px;display:grid;grid-template-columns:1fr 1fr;gap:3px}
.port-item{position:relative;overflow:hidden;background:var(--card);aspect-ratio:16/10;display:flex;align-items:flex-end;cursor:pointer;text-decoration:none}
.port-item.wide{grid-column:1/-1;aspect-ratio:21/9}
.port-img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;display:block;transition:transform .7s cubic-bezier(.4,0,.2,1),filter .5s}
.port-item:hover .port-img{transform:scale(1.06);filter:brightness(.6)}
.port-ov{position:absolute;inset:0;background:linear-gradient(to top,rgba(0,0,0,.88) 0%,rgba(0,0,0,.08) 60%,transparent 100%);z-index:1}
.port-content{position:relative;z-index:2;padding:28px 32px;width:100%}
.port-cat{font-size:.56rem;letter-spacing:.22em;text-transform:uppercase;color:var(--gold);margin-bottom:7px}
.port-title{font-family:var(--display);font-size:clamp(1.3rem,2.5vw,2.4rem);letter-spacing:.04em;line-height:1.1;color:#fff}
.port-arr{position:absolute;top:24px;right:24px;z-index:2;width:40px;height:40px;border:1px solid rgba(255,255,255,.2);border-radius:50%;display:flex;align-items:center;justify-content:center;color:rgba(255,255,255,.4);transition:all .4s;transform:rotate(-45deg)}
.port-item:hover .port-arr{background:var(--gold);border-color:var(--gold);color:#080808;transform:rotate(0deg)}

/* INSTAGRAM */
.ig-sec{background:var(--deep);text-align:center}
.ig-sec .ey{justify-content:center}
.ig-sec .sec-title{text-align:center}
.ig-handle{font-family:var(--serif);font-style:italic;font-size:clamp(1.2rem,2.6vw,2.2rem);color:var(--gold);margin-top:8px;margin-bottom:40px;display:block;text-decoration:none;transition:color .3s}
.ig-handle:hover{color:var(--accent)}
.ig-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:3px;margin-bottom:40px}
.ig-tile{aspect-ratio:1;position:relative;overflow:hidden;cursor:pointer;background:var(--card)}
.ig-tile img{width:100%;height:100%;object-fit:cover;display:block;transition:transform .5s,filter .4s}
.ig-tile:hover img{transform:scale(1.1);filter:brightness(.65)}
.ig-tile-ov{position:absolute;inset:0;background:rgba(232,184,75,0);display:flex;align-items:center;justify-content:center;transition:background .4s}
.ig-tile:hover .ig-tile-ov{background:rgba(232,184,75,.18)}
.ig-btn{display:inline-flex;align-items:center;gap:10px;padding:15px 40px;background:transparent;border:1px solid var(--gold);color:var(--gold);font-family:var(--body);font-size:.76rem;font-weight:500;letter-spacing:.11em;text-transform:uppercase;text-decoration:none;position:relative;overflow:hidden;transition:color .4s}
.ig-btn::before{content:'';position:absolute;inset:0;background:var(--gold);transform:scaleX(0);transform-origin:left;transition:transform .45s cubic-bezier(.4,0,.2,1)}
.ig-btn:hover{color:#080808}
.ig-btn:hover::before{transform:scaleX(1)}
.ig-btn span{position:relative;z-index:1}

/* WHY */
.why-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:2px;margin-top:60px}
.why-card{background:var(--card);padding:40px 28px;position:relative;overflow:hidden;transition:background .3s}
.why-card::before{content:'';position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--gold),var(--accent));transform:scaleX(0);transform-origin:left;transition:transform .5s cubic-bezier(.4,0,.2,1)}
.why-card:hover::before{transform:scaleX(1)}
.wc-icon{width:44px;height:44px;border:1px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:1.2rem;margin-bottom:20px;transition:border-color .3s}
.why-card:hover .wc-icon{border-color:var(--gold)}
.wc-title{font-family:var(--display);font-size:1.3rem;letter-spacing:.05em;margin-bottom:10px}
.wc-desc{font-size:.8rem;color:var(--muted);line-height:1.85}

/* TESTIMONIALS */
.testi-bg{background:var(--deep)}
.testi-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:2px;margin-top:60px}
.testi-card{background:var(--card);padding:36px 28px;transition:background .3s}
.testi-stars{display:flex;gap:2px;margin-bottom:16px}
.star{color:var(--gold);font-size:.82rem}
.testi-q{font-size:2.2rem;color:var(--gold);line-height:.5;margin-bottom:18px;font-family:Georgia,serif}
.testi-txt{font-size:.84rem;color:var(--muted);line-height:1.9;margin-bottom:22px;font-style:italic}
.testi-author{font-size:.65rem;letter-spacing:.12em;text-transform:uppercase;color:var(--gold)}
.testi-role{font-size:.63rem;color:var(--muted);margin-top:3px}

/* CONTACT */
.contact-inner{display:grid;grid-template-columns:1fr 1fr;gap:68px;align-items:start;margin-top:60px}
.contact-big{font-family:var(--display);font-size:clamp(2rem,5.5vw,5.5rem);letter-spacing:.04em;line-height:.95;margin-bottom:24px}
.contact-big em{font-family:var(--serif);font-style:italic;color:var(--gold);font-size:clamp(1.2rem,3.2vw,3.2rem);display:block;letter-spacing:.02em}
.ci-list{display:flex;flex-direction:column;gap:0;margin-top:36px}
.ci{display:flex;align-items:center;gap:14px;padding:14px 0;border-bottom:1px solid var(--border);text-decoration:none;transition:border-color .3s}
.ci:hover{border-color:var(--gold)}
.ci-icon{width:36px;height:36px;border:1px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:.9rem;flex-shrink:0;color:var(--gold);transition:border-color .3s,background .3s}
.ci:hover .ci-icon{border-color:var(--gold);background:rgba(232,184,75,.08)}
.ci-lbl{font-size:.56rem;letter-spacing:.16em;text-transform:uppercase;color:var(--muted);margin-bottom:2px}
.ci-val{font-size:.86rem;color:var(--white)}
.wa-big-btn{display:flex;align-items:center;gap:12px;background:var(--wa);color:#fff;padding:16px 24px;text-decoration:none;margin-top:28px;transition:transform .2s,box-shadow .2s;font-family:var(--body)}
.wa-big-btn:hover{transform:translateY(-2px);box-shadow:0 8px 28px rgba(37,211,102,.3)}
.wa-big-btn svg{width:20px;height:20px;fill:white;flex-shrink:0}
.wa-big-btn-txt{display:flex;flex-direction:column;gap:2px}
.wa-big-btn-t{font-size:.75rem;font-weight:600;letter-spacing:.08em;text-transform:uppercase}
.wa-big-btn-s{font-size:.68rem;opacity:.8}
/* Form */
.fg{margin-bottom:22px}
.fl{display:block;font-size:.58rem;letter-spacing:.18em;text-transform:uppercase;color:var(--muted);margin-bottom:8px}
.fi,.fs,.ft{width:100%;background:var(--card);border:1px solid var(--border);padding:12px 14px;font-family:var(--body);font-size:.86rem;color:var(--white);outline:none;transition:border-color .3s;resize:none;-webkit-appearance:none;appearance:none;border-radius:0}
.fi:focus,.fs:focus,.ft:focus{border-color:var(--gold)}
.fi::placeholder,.ft::placeholder{color:var(--muted)}
.fs{color:var(--muted);cursor:pointer}
.fs option{background:var(--card);color:var(--white)}
.ft{min-height:85px}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:14px}
.btn-submit{width:100%;display:flex;align-items:center;justify-content:center;gap:10px;padding:15px;background:var(--wa);color:#fff;border:none;font-family:var(--body);font-size:.76rem;font-weight:600;letter-spacing:.11em;text-transform:uppercase;cursor:pointer;transition:transform .2s,box-shadow .2s}
.btn-submit:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(37,211,102,.3)}
.btn-submit svg{width:17px;height:17px;fill:white;flex-shrink:0}
.form-note{font-size:.68rem;color:var(--muted);margin-top:10px;line-height:1.6}
#form-success{display:none;background:rgba(37,211,102,.1);border:1px solid var(--wa);padding:20px;margin-bottom:20px;text-align:center}
.fs-icon{font-size:1.8rem;margin-bottom:6px}
.fs-title{font-family:var(--display);font-size:1.3rem;color:var(--wa);letter-spacing:.04em}
.fs-sub{font-size:.78rem;color:var(--muted);margin-top:4px}

/* FOOTER */
footer{background:var(--deep);padding:68px 56px 36px;border-top:1px solid var(--border)}
.footer-top{display:grid;grid-template-columns:2fr 1fr 1fr 1fr;gap:48px;margin-bottom:48px}
.fb-name{font-family:var(--display);font-size:1.8rem;letter-spacing:.06em;margin-bottom:7px}
.fb-sub{font-size:.55rem;letter-spacing:.22em;text-transform:uppercase;color:var(--gold);margin-bottom:16px}
.fb-tag{font-size:.8rem;color:var(--muted);line-height:1.8;max-width:250px}
.fc-title{font-size:.58rem;letter-spacing:.18em;text-transform:uppercase;color:var(--gold);margin-bottom:20px}
.fc ul{list-style:none;display:flex;flex-direction:column;gap:10px}
.fc ul a{font-size:.78rem;color:var(--muted);text-decoration:none;transition:color .3s}
.fc ul a:hover{color:var(--white)}
.footer-bottom{display:flex;justify-content:space-between;align-items:center;padding-top:32px;border-top:1px solid var(--border);flex-wrap:wrap;gap:14px}
.footer-copy{font-size:.65rem;color:var(--muted)}
.footer-social{display:flex;gap:10px}
.si{width:34px;height:34px;border:1px solid var(--border);display:flex;align-items:center;justify-content:center;color:var(--muted);text-decoration:none;transition:border-color .3s,color .3s}
.si:hover{border-color:var(--gold);color:var(--gold)}

/* ANIMATIONS */
@keyframes fadeUp{from{opacity:0;transform:translateY(40px)}to{opacity:1;transform:translateY(0)}}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
.rev{opacity:0;transform:translateY(30px);transition:opacity .7s,transform .7s}
.rev.vis{opacity:1;transform:none}
.revL{opacity:0;transform:translateX(-30px);transition:opacity .7s,transform .7s}
.revL.vis{opacity:1;transform:none}

/* RESPONSIVE */
@media(max-width:1100px){.svc-grid{grid-template-columns:repeat(2,1fr)}.footer-top{grid-template-columns:1fr 1fr;gap:32px}}
@media(max-width:900px){
  nav{padding:16px 18px}
  .nav-links,.nav-wa{display:none}
  .ham{display:flex}
  #tt{display:none}
  section{padding:68px 18px}
  .hero{padding:0 18px 76px}
  .hero-title{font-size:clamp(2.8rem,13vw,7rem)}
  .hero-title-line2{font-size:clamp(2.2rem,11vw,6rem)}
  .hero-bottom{flex-direction:column;align-items:flex-start;gap:24px;margin-top:32px}
  .hero-ctas{align-items:stretch;width:100%}
  .hero-ctas a{justify-content:center}
  .about-inner{grid-template-columns:1fr;gap:40px}
  .about-ctas{flex-direction:column}
  .about-ctas a{justify-content:center}
  .about-stats{grid-template-columns:1fr 1fr}
  .svc-grid{grid-template-columns:1fr 1fr}
  .gallery-grid{grid-template-columns:1fr 1fr}
  .gal-item:nth-child(1){grid-column:1/3}
  .gal-item:nth-child(5){grid-column:1/3}
  .proc-steps{grid-template-columns:1fr 1fr;gap:24px}
  .proc-steps::before{display:none}
  .port-grid{grid-template-columns:1fr}
  .port-item.wide{grid-column:auto;aspect-ratio:16/10}
  .contact-inner{grid-template-columns:1fr;gap:40px}
  .why-grid{grid-template-columns:1fr 1fr}
  .testi-grid{grid-template-columns:1fr}
  .ig-grid{grid-template-columns:repeat(3,1fr)}
  .footer-top{grid-template-columns:1fr 1fr;gap:24px}
  footer{padding:48px 18px 28px}
  .footer-bottom{flex-direction:column;align-items:flex-start}
  .form-row{grid-template-columns:1fr}
}
@media(max-width:600px){
  .svc-grid{grid-template-columns:1fr}
  .why-grid{grid-template-columns:1fr}
  .gallery-grid{grid-template-columns:1fr}
  .gal-item:nth-child(1),.gal-item:nth-child(5){grid-column:auto;aspect-ratio:16/10}
  .ig-grid{grid-template-columns:repeat(2,1fr)}
  .footer-top{grid-template-columns:1fr}
  .proc-steps{grid-template-columns:1fr}
  body{cursor:auto}
  #cur,#cur-ring{display:none}
}
</style>
</head>
<body>
<div id="cur"></div>
<div id="cur-ring"></div>

<!-- LOADER -->
<div id="loader">
  <div class="loader-text"><span>SYNC</span>&nbsp;<span>MEDIA</span>&nbsp;<span>HOUSE</span></div>
  <div class="lbar-wrap"><div class="lbar"></div></div>
</div>

<!-- FLOATING WHATSAPP -->
<a id="wa-float" href="https://wa.me/919289113520?text=Hi%20Sync%20Media%20House!%20I%27d%20like%20to%20enquire%20about%20your%20services." target="_blank" rel="noopener" aria-label="WhatsApp">
  <span class="wa-tip">Chat with us →</span>
  <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
</a>

<!-- THEME TOGGLE SIDEBAR -->
<button id="tt" aria-label="Toggle theme" title="Toggle light/dark mode">
  <span class="tt-icon sun">☀️</span>
  <span class="tt-icon moon">🌙</span>
  <span class="tt-label">Theme</span>
</button>

<!-- MOBILE MENU -->
<div class="mob-menu" id="mobMenu">
  <a href="#about" class="mob-link">About</a>
  <a href="#services" class="mob-link">Services</a>
  <a href="#gallery" class="mob-link">Gallery</a>
  <a href="#work" class="mob-link">Portfolio</a>
  <a href="#contact" class="mob-link">Contact</a>
  <a href="https://wa.me/919289113520?text=Hi!%20I%20want%20to%20discuss%20a%20project." target="_blank" class="mob-wa">
    <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
    WhatsApp Us
  </a>
  <!-- Mobile theme toggle in menu -->
  <button onclick="toggleTheme()" style="background:none;border:1px solid var(--border);color:var(--white);font-family:var(--display);font-size:1rem;letter-spacing:.06em;padding:10px 24px;cursor:pointer;margin-top:8px" id="mob-theme-btn">☀️ LIGHT MODE</button>
</div>

<!-- NAV -->
<nav id="mainNav">
  <a href="#" class="nav-brand"><span class="nav-brand-top">SYNC MEDIA</span><span class="nav-brand-sub">Creative House</span></a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#gallery">Gallery</a></li>
    <li><a href="#work">Portfolio</a></li>
    <li><a href="#instagram">Instagram</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="nav-right">
    <a href="https://wa.me/919289113520?text=Hi%20Sync%20Media%20House!%20I%27d%20like%20a%20quote." target="_blank" class="nav-wa">
      <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      WhatsApp Us
    </a>
    <button class="ham" id="ham" aria-label="Menu"><span></span><span></span><span></span></button>
  </div>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <div class="hero-grid"></div>
  <p class="hero-label">📍 India — Full-Service Creative Agency</p>
  <h1 class="hero-title">SYNC<span class="hero-title-line2">MEDIA</span><em>House.</em></h1>
  <div class="hero-bottom">
    <p class="hero-desc">We capture stories, craft reels, edit videos, and build websites that make your brand impossible to ignore. From shoots to screens — we do it all.</p>
    <div class="hero-ctas">
      <a href="#services" class="btn-gold"><span>Explore Services</span><span>→</span></a>
      <a href="https://wa.me/919289113520?text=Hi!%20I%20saw%20your%20portfolio%20and%20want%20to%20discuss%20a%20project." target="_blank" class="btn-wa"><svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>WhatsApp Us</a>
      <a href="https://www.instagram.com/syncmediahousee/" target="_blank" class="btn-outline">@syncmediahousee ↗</a>
    </div>
  </div>
  <div class="scroll-ind"><span>Scroll</span><div class="scroll-wheel"><div class="scroll-dot"></div></div></div>
</section>

<!-- TICKER -->
<div class="ticker"><div class="ticker-track"><span class="ti">PHOTO SHOOTS</span><span class="td">✦</span><span class="ti">REELS & SHORT VIDEO</span><span class="td">✦</span><span class="ti">VIDEO EDITING</span><span class="td">✦</span><span class="ti">WEB DEVELOPMENT</span><span class="td">✦</span><span class="ti">SOCIAL MEDIA</span><span class="td">✦</span><span class="ti">BRAND GROWTH</span><span class="td">✦</span><span class="ti">PHOTO SHOOTS</span><span class="td">✦</span><span class="ti">REELS & SHORT VIDEO</span><span class="td">✦</span><span class="ti">VIDEO EDITING</span><span class="td">✦</span><span class="ti">WEB DEVELOPMENT</span><span class="td">✦</span><span class="ti">SOCIAL MEDIA</span><span class="td">✦</span><span class="ti">BRAND GROWTH</span><span class="td">✦</span></div></div>

<!-- ABOUT -->
<section id="about">
  <div class="ey rev"><div class="ey-line"></div><span class="ey-text">Who We Are</span></div>
  <h2 class="sec-title rev">We Are Sync<br>Media House</h2>
  <div class="about-inner">
    <div class="revL">
      <p class="about-stmt">A creative powerhouse built to help <strong>Indian businesses</strong> stand out, grow online, and connect with their audience.</p>
      <p class="about-body">Sync Media House is a full-service creative agency specializing in photography, videography, short-form reels, video editing, and web development. We don't just create content — we craft strategies that drive real results.</p>
      <p class="about-body">Whether you're a startup building your online presence or an established brand leveling up visuals, we bring the skills, tools, and creative energy to make it happen.</p>
      <div class="about-ctas">
        <a href="https://wa.me/919289113520?text=Hi%20Sync%20Media%20House!%20I%27d%20like%20to%20know%20more." target="_blank" class="btn-wa"><svg viewBox="0 0 24 24" width="14" height="14" fill="white"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>Chat on WhatsApp</a>
        <a href="#contact" class="btn-gold"><span>Get a Quote</span><span>→</span></a>
      </div>
    </div>
    <div class="about-stats rev">
      <div class="astat"><div class="astat-num"><span class="cu" data-t="50">0</span><sup>+</sup></div><div class="astat-label">Projects Done</div></div>
      <div class="astat"><div class="astat-num"><span class="cu" data-t="30">0</span><sup>+</sup></div><div class="astat-label">Happy Clients</div></div>
      <div class="astat"><div class="astat-num"><span class="cu" data-t="100">0</span><sup>%</sup></div><div class="astat-label">Satisfaction</div></div>
      <div class="astat"><div class="astat-num"><span class="cu" data-t="3">0</span><sup>+</sup></div><div class="astat-label">Years Active</div></div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section id="services" class="svc-bg">
  <div class="ey rev"><div class="ey-line"></div><span class="ey-text">What We Do</span></div>
  <h2 class="sec-title rev">Our Core Services</h2>
  <p class="sec-sub rev">Every service is built around one goal: making your brand grow faster and look better doing it.</p>
  <div class="svc-grid">
    <div class="svc-card rev" onclick="waEnq('Photo & Video Shoots')"><div class="sc-num">01</div><div class="sc-icon">📸</div><div class="sc-title">PHOTO & VIDEO SHOOTS</div><div class="sc-desc">Professional shoots for products, events, portraits & brand campaigns that stop the scroll.</div><ul class="sc-feat"><li>Product Photography</li><li>Event Coverage</li><li>Brand Campaigns</li><li>Portrait Sessions</li></ul></div>
    <div class="svc-card rev" onclick="waEnq('Reels & Short Video')"><div class="sc-num">02</div><div class="sc-icon">🎬</div><div class="sc-title">REELS & SHORT VIDEO</div><div class="sc-desc">Viral-ready reels & short-form content for Instagram & YouTube — built to grow your following.</div><ul class="sc-feat"><li>Instagram Reels</li><li>YouTube Shorts</li><li>Trending Formats</li><li>Content Strategy</li></ul></div>
    <div class="svc-card rev" onclick="waEnq('Video Editing')"><div class="sc-num">03</div><div class="sc-icon">✂️</div><div class="sc-title">VIDEO EDITING</div><div class="sc-desc">Raw footage to polished masterpiece — color grading, motion graphics, transitions & sound.</div><ul class="sc-feat"><li>Color Grading</li><li>Motion Graphics</li><li>Transitions & FX</li><li>Sound Design</li></ul></div>
    <div class="svc-card rev" onclick="waEnq('Web Development')"><div class="sc-num">04</div><div class="sc-icon">💻</div><div class="sc-title">WEB DEVELOPMENT</div><div class="sc-desc">Fast, beautiful, conversion-focused websites that turn visitors into paying customers.</div><ul class="sc-feat"><li>Custom Websites</li><li>E-Commerce Stores</li><li>Landing Pages</li><li>SEO Optimized</li></ul></div>
  </div>
</section>

<!-- GALLERY -->
<section id="gallery">
  <div class="ey rev"><div class="ey-line"></div><span class="ey-text">Our Shoots</span></div>
  <h2 class="sec-title rev">Behind the Lens</h2>
  <p class="sec-sub rev">A glimpse into the visual stories we've crafted for brands across India.</p>
  <div class="gallery-grid">
    <div class="gal-item rev"><img class="gal-img" src="https://images.unsplash.com/photo-1492691527719-9d1e07e534b4?w=900&q=80&auto=format&fit=crop" alt="Brand Shoot" loading="lazy"><div class="gal-ov"><span class="gal-label">Brand Shoot</span></div></div>
    <div class="gal-item rev"><img class="gal-img" src="https://images.unsplash.com/photo-1471341971476-ae15ff5dd4ea?w=600&q=80&auto=format&fit=crop" alt="Product Photography" loading="lazy"><div class="gal-ov"><span class="gal-label">Product Photography</span></div></div>
    <div class="gal-item rev"><img class="gal-img" src="https://images.unsplash.com/photo-1574717024653-61fd2cf4d44d?w=600&q=80&auto=format&fit=crop" alt="Video Production" loading="lazy"><div class="gal-ov"><span class="gal-label">Video Production</span></div></div>
    <div class="gal-item rev"><img class="gal-img" src="https://images.unsplash.com/photo-1603190287605-e6ade32fa852?w=600&q=80&auto=format&fit=crop" alt="Studio Shoot" loading="lazy"><div class="gal-ov"><span class="gal-label">Studio Shoot</span></div></div>
    <div class="gal-item rev"><img class="gal-img" src="https://images.unsplash.com/photo-1559028012-481c04fa702d?w=900&q=80&auto=format&fit=crop" alt="Reel Production" loading="lazy"><div class="gal-ov"><span class="gal-label">Reel Production</span></div></div>
    <div class="gal-item rev"><img class="gal-img" src="https://images.unsplash.com/photo-1542744173-8e7e53415bb0?w=600&q=80&auto=format&fit=crop" alt="Corporate Shoot" loading="lazy"><div class="gal-ov"><span class="gal-label">Corporate Shoot</span></div></div>
  </div>
</section>

<!-- PROCESS -->
<section class="proc-bg">
  <div class="ey rev"><div class="ey-line"></div><span class="ey-text">How We Work</span></div>
  <h2 class="sec-title rev">Our Simple Process</h2>
  <div class="proc-steps">
    <div class="proc-step rev"><div class="ps-c">01</div><div class="ps-title">DISCOVER</div><div class="ps-desc">Free consultation to understand your brand, goals & vision.</div></div>
    <div class="proc-step rev"><div class="ps-c">02</div><div class="ps-title">PLAN</div><div class="ps-desc">We craft a tailored creative plan around your business goals.</div></div>
    <div class="proc-step rev"><div class="ps-c">03</div><div class="ps-title">CREATE</div><div class="ps-desc">Shoot, edit, design, or build — bringing your vision to life.</div></div>
    <div class="proc-step rev"><div class="ps-c">04</div><div class="ps-title">REFINE</div><div class="ps-desc">Review, revise & polish until you're fully satisfied.</div></div>
    <div class="proc-step rev"><div class="ps-c">05</div><div class="ps-title">LAUNCH</div><div class="ps-desc">Deliver, go live, and track performance together.</div></div>
  </div>
</section>

<!-- PORTFOLIO -->
<section id="work">
  <div class="ey rev"><div class="ey-line"></div><span class="ey-text">Our Work</span></div>
  <h2 class="sec-title rev">Recent Projects</h2>
  <div class="port-grid">
    <div class="port-item wide rev" onclick="waEnq('Hotel Golden Petals style shoot')">
      <img class="port-img" src="https://images.unsplash.com/photo-1551882547-ff40c63fe5fa?w=1400&q=80&auto=format&fit=crop" alt="Hotel Golden Petals">
      <div class="port-ov"></div>
      <div class="port-content"><div class="port-cat">Photography & Videography</div><div class="port-title">Hotel Golden Petals — Brand Shoot</div></div>
      <div class="port-arr"><svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M7 17L17 7M7 7h10v10"/></svg></div>
    </div>
    <div class="port-item rev" onclick="waEnq('Social Media Reels')">
      <img class="port-img" src="https://images.unsplash.com/photo-1611162616305-c69b3037c431?w=800&q=80&auto=format&fit=crop" alt="Reels Campaign">
      <div class="port-ov"></div>
      <div class="port-content"><div class="port-cat">Reels & Short Video</div><div class="port-title">Social Media Campaign</div></div>
      <div class="port-arr"><svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M7 17L17 7M7 7h10v10"/></svg></div>
    </div>
    <div class="port-item rev" onclick="waEnq('Web Development')">
      <img class="port-img" src="https://images.unsplash.com/photo-1467232004584-a241de8bcf5d?w=800&q=80&auto=format&fit=crop" alt="Web Development">
      <div class="port-ov"></div>
      <div class="port-content"><div class="port-cat">Web Development</div><div class="port-title">Business Website Build</div></div>
      <div class="port-arr"><svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M7 17L17 7M7 7h10v10"/></svg></div>
    </div>
  </div>
</section>

<!-- INSTAGRAM -->
<section id="instagram" class="ig-sec">
  <div class="ey"><div class="ey-line"></div><span class="ey-text">Follow Our Work</span></div>
  <h2 class="sec-title rev">We're on Instagram</h2>
  <a class="ig-handle rev" href="https://www.instagram.com/syncmediahousee/" target="_blank" rel="noopener">@syncmediahousee</a>
  <div class="ig-grid rev">
    <div class="ig-tile" onclick="window.open('https://www.instagram.com/syncmediahousee/','_blank')"><img src="https://images.unsplash.com/photo-1492691527719-9d1e07e534b4?w=400&q=75&auto=format&fit=crop" alt="ig" loading="lazy"><div class="ig-tile-ov"></div></div>
    <div class="ig-tile" onclick="window.open('https://www.instagram.com/syncmediahousee/','_blank')"><img src="https://images.unsplash.com/photo-1611162616305-c69b3037c431?w=400&q=75&auto=format&fit=crop" alt="ig" loading="lazy"><div class="ig-tile-ov"></div></div>
    <div class="ig-tile" onclick="window.open('https://www.instagram.com/syncmediahousee/','_blank')"><img src="https://images.unsplash.com/photo-1574717024653-61fd2cf4d44d?w=400&q=75&auto=format&fit=crop" alt="ig" loading="lazy"><div class="ig-tile-ov"></div></div>
    <div class="ig-tile" onclick="window.open('https://www.instagram.com/syncmediahousee/','_blank')"><img src="https://images.unsplash.com/photo-1551882547-ff40c63fe5fa?w=400&q=75&auto=format&fit=crop" alt="ig" loading="lazy"><div class="ig-tile-ov"></div></div>
    <div class="ig-tile" onclick="window.open('https://www.instagram.com/syncmediahousee/','_blank')"><img src="https://images.unsplash.com/photo-1467232004584-a241de8bcf5d?w=400&q=75&auto=format&fit=crop" alt="ig" loading="lazy"><div class="ig-tile-ov"></div></div>
    <div class="ig-tile" onclick="window.open('https://www.instagram.com/syncmediahousee/','_blank')"><img src="https://images.unsplash.com/photo-1603190287605-e6ade32fa852?w=400&q=75&auto=format&fit=crop" alt="ig" loading="lazy"><div class="ig-tile-ov"></div></div>
  </div>
  <a href="https://www.instagram.com/syncmediahousee/" target="_blank" rel="noopener" class="ig-btn">
    <svg viewBox="0 0 24 24" width="15" height="15" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg>
    <span>Follow @syncmediahousee</span>
  </a>
</section>

<!-- WHY CHOOSE US -->
<section>
  <div class="ey rev"><div class="ey-line"></div><span class="ey-text">Why Choose Us</span></div>
  <h2 class="sec-title rev">Why Sync Media House?</h2>
  <div class="why-grid">
    <div class="why-card rev"><div class="wc-icon">⚡</div><div class="wc-title">FAST DELIVERY</div><div class="wc-desc">Time is money. Our workflow ensures fast turnaround without compromising on quality.</div></div>
    <div class="why-card rev"><div class="wc-icon">🎯</div><div class="wc-title">RESULTS FOCUSED</div><div class="wc-desc">Every piece of content is built with a goal — more followers, leads, and sales.</div></div>
    <div class="why-card rev"><div class="wc-icon">✨</div><div class="wc-title">PREMIUM QUALITY</div><div class="wc-desc">Professional-grade equipment and software. No shortcuts. Your brand deserves the best.</div></div>
    <div class="why-card rev"><div class="wc-icon">🤝</div><div class="wc-title">DEDICATED SUPPORT</div><div class="wc-desc">We're with you from concept to launch. WhatsApp us anytime — we respond fast.</div></div>
    <div class="why-card rev"><div class="wc-icon">💡</div><div class="wc-title">CREATIVE STRATEGY</div><div class="wc-desc">We don't just execute — we ideate. Trend-aware creative concepts keep you ahead.</div></div>
    <div class="why-card rev"><div class="wc-icon">📈</div><div class="wc-title">BUSINESS GROWTH</div><div class="wc-desc">From brand awareness to conversions, our content helps businesses grow consistently.</div></div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testi-bg">
  <div class="ey rev"><div class="ey-line"></div><span class="ey-text">Client Love</span></div>
  <h2 class="sec-title rev">What Clients Say</h2>
  <div class="testi-grid">
    <div class="testi-card rev"><div class="testi-stars"><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span></div><div class="testi-q">"</div><div class="testi-txt">Sync Media House transformed our hotel's digital presence. The brand shoot for Hotel Golden Petals was beyond expectations — stunning, professional, and on time.</div><div class="testi-author">Rajesh Sharma</div><div class="testi-role">Owner, Hotel Golden Petals</div></div>
    <div class="testi-card rev"><div class="testi-stars"><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span></div><div class="testi-q">"</div><div class="testi-txt">The reels they made went viral within days. Their understanding of trends is unmatched. Our Instagram following grew 3x in two months. Highly recommend!</div><div class="testi-author">Priya Mehta</div><div class="testi-role">Founder, Fashion Brand</div></div>
    <div class="testi-card rev"><div class="testi-stars"><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span></div><div class="testi-q">"</div><div class="testi-txt">Got our website built by Sync Media House — fast, clean, and exactly what we needed. The team is responsive and genuinely cares about results. 10/10!</div><div class="testi-author">Amit Verma</div><div class="testi-role">Director, Consulting Firm</div></div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="ey rev"><div class="ey-line"></div><span class="ey-text">Get In Touch</span></div>
  <div class="contact-inner">
    <div class="revL">
      <h2 class="contact-big">LET'S CREATE<em>something great.</em></h2>
      <p style="font-size:.86rem;color:var(--muted);line-height:1.8">Ready to level up your brand? Fill the form or WhatsApp us directly — we reply within minutes!</p>
      <div class="ci-list">
        <a href="https://www.instagram.com/syncmediahousee/" target="_blank" class="ci"><div class="ci-icon"><svg viewBox="0 0 24 24" width="15" height="15" fill="var(--gold)"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg></div><div><div class="ci-lbl">Instagram</div><div class="ci-val">@syncmediahousee</div></div></a>
        <a href="https://wa.me/919289113520" target="_blank" class="ci"><div class="ci-icon"><svg viewBox="0 0 24 24" width="15" height="15" fill="var(--wa)"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg></div><div><div class="ci-lbl">WhatsApp Business</div><div class="ci-val">+91 92891 13520</div></div></a>
        <a href="tel:+919289113520" class="ci"><div class="ci-icon">📞</div><div><div class="ci-lbl">Call Us</div><div class="ci-val">+91 92891 13520</div></div></a>
        <div class="ci" style="cursor:default"><div class="ci-icon">📍</div><div><div class="ci-lbl">Location</div><div class="ci-val">India</div></div></div>
      </div>
      <a href="https://wa.me/919289113520?text=Hi%20Sync%20Media%20House!%20I%27d%20like%20to%20get%20started." target="_blank" class="wa-big-btn">
        <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
        <div class="wa-big-btn-txt"><span class="wa-big-btn-t">Chat on WhatsApp Business</span><span class="wa-big-btn-s">+91 92891 13520 · Reply within minutes</span></div>
      </a>
    </div>
    <div class="rev">
      <div id="form-success"><div class="fs-icon">✅</div><div class="fs-title">SENT TO WHATSAPP!</div><div class="fs-sub">WhatsApp is opening with your message. We'll reply within minutes!</div></div>
      <div class="form-row">
        <div class="fg"><label class="fl">Your Name *</label><input type="text" class="fi" id="fn" placeholder="Full Name"></div>
        <div class="fg"><label class="fl">Phone / WhatsApp *</label><input type="tel" class="fi" id="fp" placeholder="+91 00000 00000"></div>
      </div>
      <div class="fg"><label class="fl">Business Name</label><input type="text" class="fi" id="fb" placeholder="Your Business / Brand Name"></div>
      <div class="fg"><label class="fl">Service Required *</label>
        <select class="fs" id="fsvc"><option value="" disabled selected>Select a service...</option><option>Photo / Video Shoot</option><option>Instagram Reels</option><option>Video Editing</option><option>Web Development</option><option>Full Package (All Services)</option><option>Social Media Management</option><option>Something Else</option></select>
      </div>
      <div class="fg"><label class="fl">Budget Range</label>
        <select class="fs" id="fbg"><option value="" disabled selected>Approximate budget...</option><option>Under ₹5,000</option><option>₹5,000 – ₹15,000</option><option>₹15,000 – ₹30,000</option><option>₹30,000 – ₹50,000</option><option>₹50,000+</option><option>Let's discuss</option></select>
      </div>
      <div class="fg"><label class="fl">Project Details</label><textarea class="ft" id="fm" placeholder="Tell us about your project, goals, timeline..."></textarea></div>
      <button class="btn-submit" onclick="sendWA()">
        <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
        Send via WhatsApp
      </button>
      <p class="form-note">Clicking "Send via WhatsApp" opens WhatsApp with your enquiry pre-filled — directly to our business number <strong>+91 92891 13520</strong>. We reply within minutes!</p>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-top">
    <div>
      <div class="fb-name">SYNC MEDIA</div>
      <div class="fb-sub">Creative House</div>
      <div class="fb-tag">We create visual stories that help Indian businesses grow, connect, and thrive in the digital age.</div>
      <a href="https://wa.me/919289113520" target="_blank" style="display:inline-flex;align-items:center;gap:7px;margin-top:18px;color:var(--wa);text-decoration:none;font-size:.78rem;font-weight:500"><svg viewBox="0 0 24 24" width="14" height="14" fill="var(--wa)"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>+91 92891 13520</a>
    </div>
    <div class="fc"><div class="fc-title">Services</div><ul><li><a href="#services">Photo & Video Shoots</a></li><li><a href="#services">Reels & Short Video</a></li><li><a href="#services">Video Editing</a></li><li><a href="#services">Web Development</a></li></ul></div>
    <div class="fc"><div class="fc-title">Company</div><ul><li><a href="#about">About Us</a></li><li><a href="#gallery">Gallery</a></li><li><a href="#work">Portfolio</a></li><li><a href="#contact">Contact</a></li></ul></div>
    <div class="fc"><div class="fc-title">Connect</div><ul><li><a href="https://www.instagram.com/syncmediahousee/" target="_blank">Instagram</a></li><li><a href="https://wa.me/919289113520" target="_blank">WhatsApp</a></li><li><a href="tel:+919289113520">Call Us</a></li><li><a href="#contact">Free Quote</a></li></ul></div>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2026 Sync Media House. All rights reserved. Crafted with ✦ in India.</div>
    <div class="footer-social">
      <a href="https://www.instagram.com/syncmediahousee/" target="_blank" class="si" aria-label="Instagram"><svg viewBox="0 0 24 24" width="15" height="15" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg></a>
      <a href="https://wa.me/919289113520" target="_blank" class="si" aria-label="WhatsApp"><svg viewBox="0 0 24 24" width="15" height="15" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg></a>
    </div>
  </div>
</footer>

<script>
const WA='919289113520';

// LOADER
window.addEventListener('load',()=>setTimeout(()=>document.getElementById('loader').classList.add('done'),2000));

// CURSOR
const cur=document.getElementById('cur'),ring=document.getElementById('cur-ring');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cur.style.left=mx+'px';cur.style.top=my+'px'});
(function loop(){rx+=(mx-rx)*.1;ry+=(my-ry)*.1;ring.style.left=rx+'px';ring.style.top=ry+'px';requestAnimationFrame(loop)})();
document.querySelectorAll('a,button,.svc-card,.port-item,.gal-item,.ig-tile').forEach(el=>{
  el.addEventListener('mouseenter',()=>{cur.style.width='18px';cur.style.height='18px';ring.style.width='58px';ring.style.height='58px'});
  el.addEventListener('mouseleave',()=>{cur.style.width='8px';cur.style.height='8px';ring.style.width='36px';ring.style.height='36px'});
});

// THEME
const html=document.documentElement;
function toggleTheme(){
  const t=html.getAttribute('data-theme')==='dark'?'light':'dark';
  html.setAttribute('data-theme',t);
  localStorage.setItem('smh-theme',t);
  const btn=document.getElementById('mob-theme-btn');
  if(btn)btn.textContent=t==='dark'?'☀️ LIGHT MODE':'🌙 DARK MODE';
}
// Init theme
const saved=localStorage.getItem('smh-theme')||'dark';
html.setAttribute('data-theme',saved);
const mobBtn=document.getElementById('mob-theme-btn');
if(mobBtn)mobBtn.textContent=saved==='dark'?'☀️ LIGHT MODE':'🌙 DARK MODE';
document.getElementById('tt').addEventListener('click',toggleTheme);

// HAMBURGER
const ham=document.getElementById('ham'),mob=document.getElementById('mobMenu');
ham.addEventListener('click',()=>{ham.classList.toggle('open');mob.classList.toggle('open');document.body.style.overflow=mob.classList.contains('open')?'hidden':''});
mob.querySelectorAll('.mob-link').forEach(a=>a.addEventListener('click',()=>{ham.classList.remove('open');mob.classList.remove('open');document.body.style.overflow=''}));

// NAV SCROLL
const nav=document.getElementById('mainNav');
window.addEventListener('scroll',()=>nav.classList.toggle('scrolled',window.scrollY>50));

// REVEAL
const obs=new IntersectionObserver(entries=>{
  entries.forEach((e,i)=>{if(e.isIntersecting){setTimeout(()=>e.target.classList.add('vis'),i*65);obs.unobserve(e.target)}});
},{threshold:.07});
document.querySelectorAll('.rev,.revL').forEach(el=>obs.observe(el));

// COUNTUP
function countup(el){
  const t=+el.dataset.t,d=1600,s=performance.now();
  (function tick(now){const p=Math.min((now-s)/d,1),e2=1-Math.pow(1-p,3);el.textContent=Math.round(e2*t);if(p<1)requestAnimationFrame(tick)})(performance.now());
}
new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting&&!e.target.dataset.done){e.target.querySelectorAll('.cu').forEach(countup);e.target.dataset.done=1}});
},{threshold:.3}).observe(document.querySelector('.about-stats'));

// STAGGER
['svc-card','why-card','testi-card','proc-step','gal-item'].forEach(cls=>{
  document.querySelectorAll('.'+cls).forEach((c,i)=>c.style.transitionDelay=(i*.08)+'s');
});

// SEND VIA WHATSAPP
function sendWA(){
  const name=document.getElementById('fn').value.trim();
  const phone=document.getElementById('fp').value.trim();
  const biz=document.getElementById('fb').value.trim();
  const svc=document.getElementById('fsvc').value;
  const budget=document.getElementById('fbg').value;
  const msg=document.getElementById('fm').value.trim();
  if(!name){alert('Please enter your name.');document.getElementById('fn').focus();return}
  if(!phone){alert('Please enter your phone number.');document.getElementById('fp').focus();return}
  if(!svc){alert('Please select a service.');document.getElementById('fsvc').focus();return}
  const text=`Hi Sync Media House! 👋\n\n*New Enquiry from Portfolio Website*\n\n📋 *Name:* ${name}\n📱 *Phone:* ${phone}${biz?'\n🏢 *Business:* '+biz:''}\n🎯 *Service:* ${svc}${budget?'\n💰 *Budget:* '+budget:''}${msg?'\n📝 *Details:* '+msg:''}\n\nI found you through your portfolio and I'm interested in working with you!`;
  window.open('https://wa.me/'+WA+'?text='+encodeURIComponent(text),'_blank');
  document.getElementById('form-success').style.display='block';
  document.getElementById('form-success').scrollIntoView({behavior:'smooth',block:'nearest'});
}

// SERVICE CARD WHATSAPP
function waEnq(svc){
  const text='Hi Sync Media House! 👋 I\'m interested in your *'+svc+'* service. Can we discuss further?';
  window.open('https://wa.me/'+WA+'?text='+encodeURIComponent(text),'_blank');
}
</script>
</body>
</html>
