<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no">
<title>RevMaster</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Barlow:wght@400;500;600;700&family=Barlow+Condensed:wght@600;700&display=swap" rel="stylesheet">
<style>
:root{--bg:#080810;--bg2:#0e0e1a;--bg3:#14141f;--card:#12121c;--card2:#1a1a28;--border:#22223a;--border2:#2e2e4a;--orange:#ff6200;--orange2:#ff8c00;--red:#e63946;--green:#2dbd6e;--gold:#f5c842;--blue:#38b6ff;--purple:#a855f7;--text:#e8e8f0;--text2:#7878a0;--text3:#3a3a55;}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;overflow:hidden}
body{background:var(--bg);color:var(--text);font-family:'Barlow',sans-serif;display:flex;flex-direction:column;overflow:hidden}
body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(rgba(255,98,0,0.04) 1px,transparent 1px),linear-gradient(90deg,rgba(255,98,0,0.04) 1px,transparent 1px);background-size:40px 40px;pointer-events:none;z-index:0}
.hdr{position:relative;z-index:10;background:rgba(8,8,16,0.95);border-bottom:1px solid var(--border);padding:10px 14px;display:flex;align-items:center;justify-content:space-between;flex-shrink:0}
.hdr-logo{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:3px;background:linear-gradient(90deg,var(--orange),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.hdr-right{display:flex;align-items:center;gap:8px}
.money-pill{display:flex;align-items:center;gap:5px;background:var(--card2);border:1px solid var(--border2);border-radius:20px;padding:6px 11px}
.money-label{font-size:10px;color:var(--gold);font-weight:700}
.money-amt{font-family:'Bebas Neue',sans-serif;font-size:18px;color:var(--gold)}
.money-amt.bump{animation:mBump .4s ease}
@keyframes mBump{0%,100%{transform:scale(1)}50%{transform:scale(1.18)}}
.stats-pill{display:flex;align-items:center;gap:4px;background:var(--card);border:1px solid var(--border);border-radius:20px;padding:6px 10px;font-size:11px;color:var(--text2);font-weight:600}
.scroll-area{flex:1;overflow-y:auto;overflow-x:hidden;position:relative;z-index:1;-webkit-overflow-scrolling:touch;scrollbar-width:none}
.scroll-area::-webkit-scrollbar{display:none}
.tab{display:none;padding:14px 14px 100px}
.tab.active{display:block;animation:fslide .25s ease}
@keyframes fslide{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.bottom-nav{position:relative;z-index:10;display:flex;background:rgba(8,8,16,0.97);border-top:1px solid var(--border);flex-shrink:0;padding-bottom:env(safe-area-inset-bottom,0px)}
.nav-btn{flex:1;display:flex;flex-direction:column;align-items:center;gap:2px;padding:9px 4px 8px;background:none;border:none;cursor:pointer;color:var(--text3);transition:color .2s;font-family:'Barlow',sans-serif}
.nav-btn.active{color:var(--orange)}
.nav-btn svg{width:20px;height:20px;stroke-width:1.8}
.nav-btn span{font-size:9px;font-weight:700;text-transform:uppercase;letter-spacing:.8px}
.nav-dot{width:4px;height:4px;border-radius:50%;background:var(--orange);margin-bottom:-4px;margin-top:2px;opacity:0;transition:opacity .2s}
.nav-btn.active .nav-dot{opacity:1}
.sec-title{font-family:'Bebas Neue',sans-serif;font-size:30px;letter-spacing:3px;line-height:1;margin-bottom:2px}
.sec-sub{color:var(--text2);font-size:12px;font-weight:500;margin-bottom:14px}
.filter-bar{display:flex;gap:6px;overflow-x:auto;padding-bottom:2px;margin-bottom:14px;scrollbar-width:none}
.filter-bar::-webkit-scrollbar{display:none}
.chip{flex-shrink:0;background:var(--card);border:1px solid var(--border);border-radius:20px;padding:5px 13px;font-size:11px;font-weight:700;cursor:pointer;color:var(--text2);transition:all .15s;font-family:'Barlow Condensed',sans-serif}
.chip.active{background:var(--orange);border-color:var(--orange);color:#fff}
.car-grid{display:grid;grid-template-columns:1fr;gap:10px}
@media(min-width:520px){.car-grid{grid-template-columns:1fr 1fr}}
.car-card{background:var(--card);border:1px solid var(--border);border-radius:16px;overflow:hidden;transition:transform .15s}
.car-card:active{transform:scale(.98)}
.car-banner{height:88px;display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden}
.car-banner::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,transparent 50%,var(--card))}
.car-emoji{font-size:50px;position:relative;z-index:1;filter:drop-shadow(0 6px 20px rgba(0,0,0,.6));transition:transform .3s}
.car-card:hover .car-emoji{transform:scale(1.08) rotate(-3deg)}
.t1{background:linear-gradient(135deg,#0d1b33,#1a3060)}
.t2{background:linear-gradient(135deg,#2d0d0d,#5c1a1a)}
.t3{background:linear-gradient(135deg,#0d2d1a,#1a5c30)}
.t4{background:linear-gradient(135deg,#2d2200,#5c4800);position:relative}
.t4::before{content:'';position:absolute;inset:0;z-index:0;background:linear-gradient(105deg,transparent 40%,rgba(245,200,66,.15) 50%,transparent 60%);animation:shim 3s infinite}
@keyframes shim{0%{transform:translateX(-100%)}100%{transform:translateX(200%)}}
.car-body{padding:11px 13px 13px}
.car-name{font-weight:700;font-size:14px;line-height:1.25;margin-bottom:2px}
.car-eng{font-size:10px;color:var(--text3);font-weight:600;margin-bottom:4px;font-family:'Barlow Condensed',sans-serif}
.car-desc{font-size:11px;color:var(--text3);font-style:italic;margin-bottom:9px}
.stat-row{display:grid;grid-template-columns:repeat(4,1fr);gap:4px;margin-bottom:10px}
.stat-box{background:var(--bg2);border-radius:8px;padding:6px 4px;text-align:center;border:1px solid var(--border)}
.stat-lbl{font-size:7px;text-transform:uppercase;letter-spacing:.8px;color:var(--text3);font-weight:700;margin-bottom:2px}
.stat-val{font-family:'Bebas Neue',sans-serif;font-size:16px;color:var(--orange)}
.stat-unit{font-size:7px;color:var(--text3)}
.car-footer{display:flex;align-items:center;justify-content:space-between;gap:8px}
.car-price{font-family:'Bebas Neue',sans-serif;font-size:20px;color:var(--gold);letter-spacing:1px}
.dt-badge{display:inline-block;font-size:9px;font-weight:800;padding:2px 8px;border-radius:10px;letter-spacing:1px;font-family:'Barlow Condensed',sans-serif}
.dt-RWD{background:rgba(230,57,70,.18);color:#ff6b75;border:1px solid rgba(230,57,70,.35)}
.dt-AWD{background:rgba(45,189,110,.18);color:#4fe08a;border:1px solid rgba(45,189,110,.35)}
.dt-FWD{background:rgba(56,182,255,.18);color:#6fd3ff;border:1px solid rgba(56,182,255,.35)}
.owned-tag,.mod-tag,.eng-tag{font-size:9px;font-weight:800;padding:2px 8px;border-radius:10px;font-family:'Barlow Condensed',sans-serif}
.owned-tag{background:rgba(255,98,0,.15);color:var(--orange);border:1px solid rgba(255,98,0,.3)}
.mod-tag{background:rgba(168,85,247,.18);color:#c084fc;border:1px solid rgba(168,85,247,.3)}
.eng-tag{background:rgba(245,200,66,.15);color:var(--gold);border:1px solid rgba(245,200,66,.3)}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:5px;padding:9px 18px;border-radius:10px;border:none;font-family:'Barlow',sans-serif;font-weight:700;font-size:13px;cursor:pointer;transition:all .15s;white-space:nowrap}
.btn:active{transform:scale(.96)}
.btn:disabled{opacity:.35;cursor:not-allowed;transform:none!important}
.btn-primary{background:var(--orange);color:#fff}
.btn-primary:hover:not(:disabled){background:var(--orange2)}
.btn-sec{background:var(--card2);color:var(--text);border:1px solid var(--border2)}
.btn-danger{background:rgba(230,57,70,.18);color:#ff7783;border:1px solid rgba(230,57,70,.35)}
.btn-ghost{background:rgba(255,98,0,.12);color:var(--orange);border:1px solid rgba(255,98,0,.3)}
.btn-gold{background:rgba(245,200,66,.15);color:var(--gold);border:1px solid rgba(245,200,66,.35)}
.btn-purple{background:var(--purple);color:#fff}
.btn-full{width:100%}
.btn-lg{padding:14px 24px;font-size:15px;border-radius:12px}
.gar-actions{display:grid;grid-template-columns:1fr 1fr;gap:6px;padding:0 13px 13px}
.empty{text-align:center;padding:60px 20px;display:flex;flex-direction:column;align-items:center;gap:10px}
.empty-icon{font-size:56px;opacity:.3}
.empty h3{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:2px;color:var(--text2)}
.empty p{color:var(--text3);font-size:13px}
.picker-box{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:13px;margin-bottom:12px}
.picker-box label{font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text2);font-weight:700;display:block;margin-bottom:7px}
.sel{width:100%;background:var(--bg2);border:1px solid var(--border2);border-radius:9px;color:var(--text);padding:10px 32px 10px 12px;font-family:'Barlow',sans-serif;font-size:13px;appearance:none;-webkit-appearance:none;cursor:pointer;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%237878a0' stroke-width='2'%3E%3Cpath d='M6 9l6 6 6-6'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 12px center}
.sel option{background:var(--bg2);color:var(--text)}
.ws-stabs{display:flex;gap:4px;margin-bottom:12px;background:var(--card);border:1px solid var(--border);border-radius:12px;padding:4px}
.ws-stab{flex:1;padding:8px 4px;text-align:center;border-radius:9px;cursor:pointer;font-size:10px;font-weight:800;text-transform:uppercase;letter-spacing:.8px;color:var(--text2);transition:all .15s;font-family:'Barlow Condensed',sans-serif;border:none;background:none}
.ws-stab.active{background:var(--orange);color:#fff}
.perf-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:13px;margin-bottom:12px}
.perf-title{font-family:'Bebas Neue',sans-serif;font-size:15px;letter-spacing:2px;color:var(--orange);margin-bottom:10px}
.pgrid{display:grid;grid-template-columns:repeat(4,1fr);gap:6px}
.pi{background:var(--bg2);border:1px solid var(--border);border-radius:9px;padding:9px 5px;text-align:center}
.pi-val{font-family:'Bebas Neue',sans-serif;font-size:20px;color:var(--orange)}
.pi-lbl{font-size:8px;text-transform:uppercase;letter-spacing:.8px;color:var(--text3);font-weight:700}
.pi-d{font-size:9px;margin-top:1px}
.score-bar-wrap{margin-top:11px}
.score-bar-lbl{display:flex;justify-content:space-between;font-size:11px;color:var(--text2);font-weight:600;margin-bottom:5px}
.score-bar-track{height:7px;background:var(--bg2);border-radius:4px;overflow:hidden;border:1px solid var(--border)}
.score-bar-fill{height:100%;border-radius:4px;background:linear-gradient(90deg,var(--orange),var(--gold));transition:width .5s cubic-bezier(.34,1.56,.64,1)}
.eng-bar{display:flex;align-items:center;gap:8px;background:var(--bg2);border:1px solid var(--border);border-radius:9px;padding:8px 11px;margin-top:10px}
.eng-bar-name{font-size:11px;font-weight:700}
.eng-bar-sub{font-size:10px;color:var(--text3)}
.section-box{background:var(--card);border:1px solid var(--border);border-radius:12px;overflow:hidden;margin-bottom:10px}
.section-hdr{padding:10px 13px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:8px}
.section-hdr-icon{font-size:15px}
.section-hdr h3{font-weight:700;font-size:13px;flex:1}
.section-hdr-note{font-size:10px;color:var(--green);font-weight:600}
.section-hdr-step{font-size:10px;color:var(--orange);font-weight:700;font-family:'Barlow Condensed',sans-serif}
.opts{padding:8px;display:flex;flex-direction:column;gap:5px}
.opt{display:flex;align-items:center;gap:10px;padding:9px 11px;background:var(--bg2);border-radius:9px;border:1.5px solid transparent;cursor:pointer;transition:all .15s}
.opt:active{transform:scale(.98)}
.opt.sel-opt{border-color:var(--orange);background:rgba(255,98,0,.07)}
.opt.sel-build{border-color:var(--purple);background:rgba(168,85,247,.07)}
.opt-check{width:16px;height:16px;border-radius:50%;border:2px solid var(--border2);display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all .15s;font-size:9px;font-weight:900;color:#fff}
.opt.sel-opt .opt-check{background:var(--orange);border-color:var(--orange)}
.opt.sel-build .opt-check{background:var(--purple);border-color:var(--purple)}
.opt-info{flex:1;min-width:0}
.opt-name{font-weight:700;font-size:12px;line-height:1.2}
.opt-desc{font-size:10px;color:var(--text2);margin-top:1px}
.opt-cost{font-family:'Barlow Condensed',sans-serif;font-weight:700;font-size:13px;text-align:right;flex-shrink:0;min-width:58px}
.c-free{color:var(--green)}
.c-paid{color:var(--gold)}
.c-instd{color:var(--text3)}
.cost-box{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:13px;margin-bottom:12px}
.cost-box-title{font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text2);font-weight:700;margin-bottom:9px}
.cost-line{display:flex;justify-content:space-between;font-size:12px;color:var(--text2);margin-bottom:5px}
.cost-total{display:flex;justify-content:space-between;font-size:14px;font-weight:700;color:var(--gold);border-top:1px solid var(--border);padding-top:9px;margin-top:5px}
.warn{font-size:11px;color:var(--red);margin-top:8px}
.swap-card{background:var(--card);border:1.5px solid var(--border);border-radius:12px;padding:12px 13px;margin-bottom:8px;cursor:pointer;transition:all .15s}
.swap-card:active{transform:scale(.98)}
.swap-card.sw-inst{border-color:var(--gold);background:rgba(245,200,66,.05);cursor:default}
.swap-head{display:flex;align-items:flex-start;justify-content:space-between;gap:8px;margin-bottom:7px}
.swap-name{font-weight:700;font-size:13px;line-height:1.2}
.swap-type{font-size:9px;font-weight:800;padding:2px 8px;border-radius:8px;background:rgba(168,85,247,.18);color:#c084fc;border:1px solid rgba(168,85,247,.3);font-family:'Barlow Condensed',sans-serif;flex-shrink:0}
.swap-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:5px;margin-bottom:7px}
.sw-stat{background:var(--bg2);border:1px solid var(--border);border-radius:7px;padding:6px 4px;text-align:center}
.sw-stat-lbl{font-size:7px;text-transform:uppercase;letter-spacing:.8px;color:var(--text3);font-weight:700;margin-bottom:2px}
.sw-stat-val{font-family:'Bebas Neue',sans-serif;font-size:17px;color:var(--orange)}
.swap-foot{display:flex;align-items:center;justify-content:space-between;gap:8px}
.swap-foot-desc{font-size:10px;color:var(--text3);font-style:italic;flex:1}
.swap-price{font-family:'Bebas Neue',sans-serif;font-size:18px;color:var(--gold);letter-spacing:1px}
.bld-preview{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:13px;margin-bottom:12px}
.bld-preview-title{font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:2px;color:var(--purple);margin-bottom:8px}
.bld-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;margin-bottom:10px}
.bld-stat{background:var(--bg2);border:1px solid var(--border);border-radius:9px;padding:9px 6px;text-align:center}
.bld-stat-val{font-family:'Bebas Neue',sans-serif;font-size:24px;color:var(--purple)}
.bld-stat-lbl{font-size:8px;text-transform:uppercase;letter-spacing:.8px;color:var(--text3);font-weight:700}
.bld-name{font-size:11px;color:var(--text2);text-align:center;margin-bottom:8px;font-weight:600}
.race-type-grid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-bottom:13px}
.rtype{background:var(--card);border:1.5px solid var(--border);border-radius:12px;padding:13px 10px;text-align:center;cursor:pointer;transition:all .15s}
.rtype:active{transform:scale(.97)}
.rtype.rsel{border-color:var(--orange);background:rgba(255,98,0,.09)}
.rtype-icon{font-size:26px;margin-bottom:5px}
.rtype-name{font-weight:700;font-size:12px;margin-bottom:3px}
.rtype-desc{font-size:10px;color:var(--text2)}
.diff-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:5px;margin-bottom:13px}
.diff{background:var(--card);border:1.5px solid var(--border);border-radius:10px;padding:10px 3px;text-align:center;cursor:pointer;transition:all .15s}
.diff:active{transform:scale(.97)}
.diff.dsel{border-color:var(--orange);background:rgba(255,98,0,.09)}
.diff-name{font-weight:800;font-size:11px;font-family:'Barlow Condensed',sans-serif;letter-spacing:.5px}
.diff-prize{font-size:9px;color:var(--gold);margin-top:3px}
.odds-box{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:13px;margin-bottom:13px}
.odds-title{font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text2);font-weight:700;margin-bottom:10px}
.odds-scores{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-bottom:10px}
.odds-score-item{background:var(--bg2);border:1px solid var(--border);border-radius:9px;padding:9px;text-align:center}
.odds-score-lbl{font-size:9px;text-transform:uppercase;letter-spacing:.8px;color:var(--text3);font-weight:700;margin-bottom:3px}
.odds-score-val{font-family:'Bebas Neue',sans-serif;font-size:24px}
.win-wrap{display:flex;align-items:center;gap:8px}
.win-lbl{font-size:11px;color:var(--text2);font-weight:600;white-space:nowrap}
.win-track{flex:1;height:8px;background:var(--bg2);border-radius:4px;overflow:hidden;border:1px solid var(--border)}
.win-fill{height:100%;border-radius:4px;transition:width .5s ease}
.win-pct{font-family:'Bebas Neue',sans-serif;font-size:20px;min-width:44px;text-align:right}
.overlay{display:none;position:fixed;inset:0;z-index:500;align-items:center;justify-content:center;padding:20px}
.overlay.show{display:flex}
#raceAnim{background:rgba(8,8,16,.97);flex-direction:column;align-items:center;justify-content:center;gap:18px}
.race-title{font-family:'Bebas Neue',sans-serif;font-size:36px;letter-spacing:6px;background:linear-gradient(90deg,var(--orange),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;text-align:center}
.race-sub{font-size:13px;color:var(--text2);font-weight:600;text-align:center}
.race-track{width:min(420px,100%);height:90px;background:var(--card2);border-radius:12px;position:relative;overflow:hidden;border:1px solid var(--border2)}
.road-lines{position:absolute;top:50%;left:0;right:0;height:2px;background:repeating-linear-gradient(90deg,var(--border2) 0,var(--border2) 18px,transparent 18px,transparent 30px);transform:translateY(-50%);animation:road .3s linear infinite}
@keyframes road{from{background-position:0 0}to{background-position:-30px 0}}
.car-p{position:absolute;top:16%;font-size:34px;left:-8%;filter:drop-shadow(0 0 10px rgba(255,98,0,.7))}
.car-o{position:absolute;bottom:14%;font-size:28px;left:-8%;opacity:.65}
.car-p.go{animation:cDrive 2.0s cubic-bezier(.18,0,.82,1) forwards}
.car-o.go{animation:cDrive 2.0s cubic-bezier(.25,0,.92,1) forwards}
@keyframes cDrive{from{left:-8%}to{left:108%}}
.cd-num{font-family:'Bebas Neue',sans-serif;font-size:90px;color:var(--orange);letter-spacing:2px;animation:cdpop .4s cubic-bezier(.34,1.56,.64,1)}
.cd-num.go{color:var(--green)}
@keyframes cdpop{from{transform:scale(.3);opacity:0}to{transform:scale(1);opacity:1}}
#raceResult{background:rgba(8,8,16,.96);align-items:center;justify-content:center}
.result-card{background:var(--card2);border:1px solid var(--border2);border-radius:24px;padding:28px 22px;width:min(380px,100%);text-align:center;animation:popup .5s cubic-bezier(.34,1.56,.64,1)}
@keyframes popup{from{transform:scale(.6);opacity:0}to{transform:scale(1);opacity:1}}
.res-emoji{font-size:60px;margin-bottom:8px}
.res-verdict{font-family:'Bebas Neue',sans-serif;font-size:46px;letter-spacing:4px;margin-bottom:4px}
.res-verdict.win{color:var(--green)}
.res-verdict.lose{color:var(--red)}
.res-sub{color:var(--text2);font-size:13px;margin-bottom:14px}
.res-prize{font-family:'Bebas Neue',sans-serif;font-size:38px;color:var(--gold);letter-spacing:2px;margin-bottom:4px}
.res-prize-lbl{font-size:10px;color:var(--text3);font-weight:700;margin-bottom:14px}
.res-stats{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-bottom:16px}
.rs-item{background:var(--bg2);border:1px solid var(--border);border-radius:9px;padding:9px}
.rs-lbl{font-size:9px;text-transform:uppercase;letter-spacing:.8px;color:var(--text3);font-weight:700;margin-bottom:3px}
.rs-val{font-family:'Bebas Neue',sans-serif;font-size:22px}
.modal-wrap{display:none;position:fixed;inset:0;z-index:600;background:rgba(8,8,16,.88);align-items:flex-end;justify-content:center;padding:0 12px 12px}
.modal-wrap.show{display:flex}
.modal{background:var(--bg3);border:1px solid var(--border2);border-radius:20px;width:100%;max-width:440px;padding:22px;animation:slideup .3s ease}
@keyframes slideup{from{transform:translateY(80px);opacity:0}to{transform:translateY(0);opacity:1}}
.modal-title{font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:2px;margin-bottom:4px}
.modal-body{color:var(--text2);font-size:13px;line-height:1.6;margin-bottom:18px}
.modal-body strong{color:var(--text)}
.modal-btns{display:flex;gap:8px}
.modal-btns .btn{flex:1}
.notif{position:fixed;top:72px;left:50%;transform:translateX(-50%);z-index:700;background:var(--card2);border:1px solid var(--border2);border-radius:20px;padding:9px 18px;font-size:13px;font-weight:600;white-space:nowrap;pointer-events:none;animation:npop 2.8s forwards}
@keyframes npop{0%{opacity:0;top:80px}12%{opacity:1;top:72px}75%{opacity:1;top:72px}100%{opacity:0;top:72px}}
.flex-sb{display:flex;align-items:center;justify-content:space-between}
.label{font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text2);font-weight:700;display:block;margin-bottom:7px}
</style>
</head>
<body>
<header class="hdr">
  <div class="hdr-logo">&#9889; REVMASTER</div>
  <div class="hdr-right">
    <div class="stats-pill">&#127937; <span id="hdrRecord">0-0</span></div>
    <div class="money-pill"><span class="money-label">$</span><span class="money-amt" id="moneyDisp">25,000</span></div>
  </div>
</header>
<div class="scroll-area">
  <div id="tab-garage" class="tab active">
    <div class="sec-title">MY GARAGE</div>
    <div class="sec-sub" id="garSub">0 cars owned</div>
    <div class="car-grid" id="garGrid"></div>
  </div>
  <div id="tab-market" class="tab">
    <div class="sec-title">MARKETPLACE</div>
    <div class="sec-sub">Buy cars to grow your collection</div>
    <div class="filter-bar">
      <div class="chip active" onclick="setFilter(this,'all')">All</div>
      <div class="chip" onclick="setFilter(this,'FWD')">FWD</div>
      <div class="chip" onclick="setFilter(this,'RWD')">RWD</div>
      <div class="chip" onclick="setFilter(this,'AWD')">AWD</div>
      <div class="chip" onclick="setFilter(this,'t1')">Budget</div>
      <div class="chip" onclick="setFilter(this,'t2')">Sport</div>
      <div class="chip" onclick="setFilter(this,'t3')">Performance</div>
      <div class="chip" onclick="setFilter(this,'t4')">Exotic</div>
    </div>
    <div class="car-grid" id="mktGrid"></div>
  </div>
  <div id="tab-workshop" class="tab">
    <div class="sec-title">WORKSHOP</div>
    <div class="sec-sub">Tune, swap, or build your engine</div>
    <div class="picker-box">
      <label>Select Car</label>
      <select class="sel" id="wsCar" onchange="wsLoad()">
        <option value="">&#8212; Choose from your garage &#8212;</option>
      </select>
    </div>
    <div id="wsContent" style="display:none"></div>
  </div>
  <div id="tab-race" class="tab">
    <div class="sec-title">RACE</div>
    <div class="sec-sub">Simulate races to earn prize money</div>
    <div class="picker-box">
      <label>Race Car</label>
      <select class="sel" id="raceCar" onchange="racePreview()">
        <option value="">&#8212; Choose your car &#8212;</option>
      </select>
    </div>
    <div id="raceCarPreview" style="display:none;margin-bottom:12px"></div>
    <span class="label">Race Type</span>
    <div class="race-type-grid">
      <div class="rtype rsel" data-type="drag" onclick="selRType(this)"><div class="rtype-icon">&#127958;&#65039;</div><div class="rtype-name">Drag Race</div><div class="rtype-desc">HP + AWD advantage</div></div>
      <div class="rtype" data-type="circuit" onclick="selRType(this)"><div class="rtype-icon">&#128260;</div><div class="rtype-name">Circuit</div><div class="rtype-desc">Balance + RWD bonus</div></div>
      <div class="rtype" data-type="street" onclick="selRType(this)"><div class="rtype-icon">&#127751;</div><div class="rtype-name">Street Sprint</div><div class="rtype-desc">0-60 focused</div></div>
      <div class="rtype" data-type="hill" onclick="selRType(this)"><div class="rtype-icon">&#9968;&#65039;</div><div class="rtype-name">Hill Climb</div><div class="rtype-desc">AWD dominates</div></div>
    </div>
    <span class="label">Difficulty</span>
    <div class="diff-grid">
      <div class="diff dsel" data-diff="amateur" onclick="selDiff(this)"><div class="diff-name" style="color:var(--blue)">Amateur</div><div class="diff-prize">$2K-5K</div></div>
      <div class="diff" data-diff="pro" onclick="selDiff(this)"><div class="diff-name" style="color:var(--green)">Pro</div><div class="diff-prize">$8K-15K</div></div>
      <div class="diff" data-diff="elite" onclick="selDiff(this)"><div class="diff-name" style="color:var(--orange)">Elite</div><div class="diff-prize">$20K-40K</div></div>
      <div class="diff" data-diff="legend" onclick="selDiff(this)"><div class="diff-name" style="color:var(--red)">Legend</div><div class="diff-prize">$50K-100K</div></div>
    </div>
    <div id="oddsBox" class="odds-box" style="display:none"><div class="odds-title">Race Preview</div><div id="oddsContent"></div></div>
    <button class="btn btn-primary btn-full btn-lg" id="raceBtn" onclick="startRace()" disabled>&#127937; &nbsp;RACE NOW</button>
  </div>
</div>
<nav class="bottom-nav">
  <button class="nav-btn active" onclick="goTab('garage',this)"><div class="nav-dot"></div><svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><rect x="1" y="3" width="22" height="18" rx="2"/><path d="M1 9h22M9 21V9"/></svg><span>Garage</span></button>
  <button class="nav-btn" onclick="goTab('market',this)"><div class="nav-dot"></div><svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 001.99 1.61h9.72a2 2 0 001.99-1.61L23 6H6"/></svg><span>Market</span></button>
  <button class="nav-btn" onclick="goTab('workshop',this)"><div class="nav-dot"></div><svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><path d="M14.7 6.3a1 1 0 000 1.4l1.6 1.6a1 1 0 001.4 0l3.77-3.77a6 6 0 01-7.94 7.94l-6.91 6.91a2.12 2.12 0 01-3-3l6.91-6.91a6 6 0 017.94-7.94l-3.76 3.76z"/></svg><span>Workshop</span></button>
  <button class="nav-btn" onclick="goTab('race',this)"><div class="nav-dot"></div><svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><polygon points="5 3 19 12 5 21 5 3"/></svg><span>Race</span></button>
</nav>
<div class="overlay" id="raceAnim" style="flex-direction:column">
  <div class="cd-num" id="cdNum">3</div>
  <div class="race-title">RACE IN PROGRESS</div>
  <div class="race-sub" id="animCarName"></div>
  <div class="race-track"><div class="road-lines"></div><div class="car-p" id="animP">&#127958;&#65039;</div><div class="car-o" id="animO">&#128663;</div></div>
  <div style="color:var(--text3);font-size:12px;font-weight:600;letter-spacing:1px">SIMULATING RACE...</div>
</div>
<div class="overlay" id="raceResult"><div class="result-card" id="resultCard"></div></div>
<div class="modal-wrap" id="buyModal"><div class="modal"><div class="modal-title" id="buyTitle">BUY CAR?</div><div class="modal-body" id="buyBody"></div><div class="modal-btns"><button class="btn btn-sec" onclick="closeModal('buyModal')">Cancel</button><button class="btn btn-primary" onclick="confirmBuy()">&#128179; Purchase</button></div></div></div>
<div class="modal-wrap" id="sellModal"><div class="modal"><div class="modal-title" id="sellTitle">SELL CAR?</div><div class="modal-body" id="sellBody"></div><div class="modal-btns"><button class="btn btn-sec" onclick="closeModal('sellModal')">Keep It</button><button class="btn btn-danger" onclick="confirmSell()">&#128181; Sell</button></div></div></div>
<div class="modal-wrap" id="swapModal"><div class="modal"><div class="modal-title" id="swapTitle">INSTALL ENGINE?</div><div class="modal-body" id="swapBody"></div><div class="modal-btns"><button class="btn btn-sec" onclick="closeModal('swapModal')">Cancel</button><button class="btn btn-gold" onclick="confirmSwap()">&#128295; Install</button></div></div></div>
<script>
// ============================================================
// DATA
// ============================================================
var CARS = [
  {id:'civicsi',  name:'2023 Honda Civic Si',           price:20000,  hp:200, wt:2950, ewt:250, dt:'FWD',tier:1,eng:'1.5L VTEC Turbo I4',       em:'&#128663;',desc:'Sport compact, rev-happy VTEC'},
  {id:'miata',    name:'2023 Mazda MX-5 Miata',         price:26900,  hp:181, wt:2341, ewt:220, dt:'RWD',tier:1,eng:'2.0L SKYACTIV-G I4',        em:'&#127958;',desc:'Lightweight legend, sublime balance'},
  {id:'gr86',     name:'2023 Toyota GR86',              price:28400,  hp:228, wt:2822, ewt:265, dt:'RWD',tier:1,eng:'2.4L FA24 Boxer-4',         em:'&#127958;',desc:"Driver's car with flat-four soul"},
  {id:'wrx',      name:'2023 Subaru WRX',               price:31095,  hp:271, wt:3264, ewt:280, dt:'AWD',tier:1,eng:'2.4L FA24F Turbo Boxer-4',  em:'&#128663;',desc:'Rally-bred AWD all-weather beast'},
  {id:'typeR',    name:'2023 Honda Civic Type R',       price:44990,  hp:315, wt:3117, ewt:260, dt:'FWD',tier:1,eng:'2.0L K20C1 VTEC Turbo',     em:'&#128663;',desc:'FWD perfected, Nurburgring slayer'},
  {id:'golfR',    name:'2023 Volkswagen Golf R',        price:44640,  hp:315, wt:3310, ewt:275, dt:'AWD',tier:1,eng:'2.0L EA888 TSI Turbo I4',   em:'&#128663;',desc:'Subtle sleeper with 4MOTION AWD'},
  {id:'mustangGT',name:'2023 Ford Mustang GT',          price:41595,  hp:450, wt:3705, ewt:445, dt:'RWD',tier:2,eng:'5.0L Coyote V8',            em:'&#127958;',desc:'American muscle, V8 anthem'},
  {id:'camaroSS', name:'2023 Chevrolet Camaro SS',      price:43495,  hp:455, wt:3653, ewt:440, dt:'RWD',tier:2,eng:'6.2L LT1 V8',              em:'&#127958;',desc:'Classic muscle, modern engineering'},
  {id:'supra',    name:'2023 Toyota GR Supra 3.0',      price:56180,  hp:382, wt:3400, ewt:390, dt:'RWD',tier:2,eng:'3.0L BMW B58 Turbo I6',    em:'&#127958;',desc:'Legendary nameplate, BMW muscle'},
  {id:'rs3',      name:'2023 Audi RS3 Sedan',           price:58900,  hp:401, wt:3748, ewt:360, dt:'AWD',tier:2,eng:'2.5L TFSI Turbo 5-cyl',    em:'&#128663;',desc:'AWD rocket, iconic 5-pot sound'},
  {id:'m3',       name:'2023 BMW M3 Competition',       price:74900,  hp:503, wt:3858, ewt:420, dt:'RWD',tier:2,eng:'3.0L S58 Twin-Turbo I6',   em:'&#127958;',desc:'The benchmark sport sedan'},
  {id:'gt500',    name:'2023 Ford Shelby GT500',        price:79095,  hp:760, wt:4225, ewt:550, dt:'RWD',tier:3,eng:'5.2L Predator SC V8',       em:'&#127958;',desc:'Most powerful street Mustang ever'},
  {id:'hellcat',  name:'2023 Dodge Challenger Hellcat', price:71895,  hp:717, wt:4449, ewt:540, dt:'RWD',tier:3,eng:'6.2L HEMI SC V8',           em:'&#127958;',desc:'Supercharged American brute'},
  {id:'z06',      name:'2023 Chevrolet Corvette Z06',   price:106395, hp:670, wt:3366, ewt:430, dt:'RWD',tier:3,eng:'5.5L LT6 Flat-Plane V8',   em:'&#127958;',desc:'Ferrari-killer from Kentucky'},
  {id:'gtr',      name:'2023 Nissan GT-R Premium',      price:113540, hp:565, wt:3822, ewt:480, dt:'AWD',tier:3,eng:'3.8L VR38DETT TT V6',      em:'&#127958;',desc:'Godzilla, the god of grip'},
  {id:'911s',     name:'2023 Porsche 911 Carrera S',    price:115000, hp:443, wt:3307, ewt:380, dt:'RWD',tier:3,eng:'3.0L Twin-Turbo Flat-6',   em:'&#127958;',desc:'Rear-engine perfection, 60 years on'},
  {id:'amggt63',  name:'2023 Mercedes-AMG GT 63 S',     price:163000, hp:630, wt:4717, ewt:510, dt:'AWD',tier:3,eng:'4.0L M177 Biturbo V8',     em:'&#127958;',desc:'Four-door GT, no compromises'},
  {id:'huracan',  name:'2023 Lamborghini Huracan',      price:241321, hp:631, wt:3135, ewt:440, dt:'RWD',tier:4,eng:'5.2L NA V10',               em:'&#127958;',desc:'Naturally aspirated V10 masterpiece'},
  {id:'gt3rs',    name:'2023 Porsche 911 GT3 RS',       price:238700, hp:518, wt:3153, ewt:370, dt:'RWD',tier:4,eng:'4.0L NA Flat-6',            em:'&#127958;',desc:'Nurburgring-tuned track weapon'},
  {id:'720s',     name:'2023 McLaren 720S',             price:299000, hp:710, wt:2937, ewt:450, dt:'RWD',tier:4,eng:'4.0L M840T Twin-T V8',     em:'&#127958;',desc:'Carbon fiber art on wheels'},
  {id:'chiron',   name:'2023 Bugatti Chiron Sport',     price:3300000,hp:1479,wt:4398, ewt:900, dt:'AWD',tier:4,eng:'8.0L Quad-Turbo W16',      em:'&#127958;',desc:'The absolute pinnacle of speed'}
];

var TUNE_KEYS = ['intake','exhaust','forced','internals','ecu','weight','drivetrain'];

var TGRPS = {
  intake:    {label:'Air Intake',       icon:'&#128168;', opts:[
    {id:'stock',  name:'Stock Intake',         cost:0,    hpM:1.00, desc:'Factory air intake system'},
    {id:'cold',   name:'Cold Air Intake',       cost:350,  hpM:1.03, desc:'+3% HP, improved throttle'},
    {id:'ram',    name:'Performance Ram Air',   cost:850,  hpM:1.06, desc:'+6% HP, pressurized feed'}
  ]},
  exhaust:   {label:'Exhaust System',   icon:'&#128293;', opts:[
    {id:'stock',  name:'Stock Exhaust',         cost:0,    hpM:1.00, desc:'Factory, emissions compliant'},
    {id:'catback',name:'Cat-Back Exhaust',       cost:1200, hpM:1.04, desc:'+4% HP, aggressive note'},
    {id:'race',   name:'Full Race System',       cost:2800, hpM:1.08, desc:'+8% HP, straight-pipe power'}
  ]},
  forced:    {label:'Boost Kit',        icon:'&#127754;', opts:[
    {id:'none',   name:'No Boost Kit',           cost:0,    hpB:0,   desc:'Stock or builder induction'},
    {id:'turbo',  name:'Bolt-On Turbo Kit',       cost:3800, hpB:55,  desc:'+55 HP stacks with built engine'},
    {id:'twin',   name:'Twin Turbo Kit',           cost:8500, hpB:130, desc:'+130 HP serious power'},
    {id:'super',  name:'Supercharger Kit',         cost:6800, hpB:90,  desc:'+90 HP instant response'}
  ]},
  internals: {label:'Engine Internals', icon:'&#9881;',   opts:[
    {id:'stock',  name:'Stock Internals',          cost:0,    desc:'Factory pistons rods crank'},
    {id:'forged', name:'Forged Pistons + Rods',     cost:3500, desc:'Handles boost longer life'},
    {id:'race',   name:'Full Race Build',             cost:8500, desc:'Race-spec everything max strength'}
  ]},
  ecu:       {label:'ECU / Tune',       icon:'&#128187;', opts:[
    {id:'stock',  name:'Stock ECU',                 cost:0,    hpM:1.00, desc:'Factory maps'},
    {id:'s1',     name:'Stage 1 Tune',               cost:600,  hpM:1.05, desc:'+5% HP optimized maps'},
    {id:'s2',     name:'Stage 2 Tune',               cost:1400, hpM:1.10, desc:'+10% HP aggressive timing'},
    {id:'rtune',  name:'Full Race Tune',              cost:2600, hpM:1.16, desc:'+16% HP race fuel required'}
  ]},
  weight:    {label:'Weight Reduction',  icon:'&#9878;',  opts:[
    {id:'stock',  name:'Stock Weight',               cost:0,     wtL:0,   desc:'All factory components'},
    {id:'wheels', name:'Forged Alloy Wheels',         cost:1800,  wtL:45,  desc:'-45 lbs lighter unsprung mass'},
    {id:'strip',  name:'Interior Strip + Delete',      cost:4500,  wtL:135, desc:'-135 lbs stripped cabin'},
    {id:'carbon', name:'Full Carbon Package',          cost:13500, wtL:270, desc:'-270 lbs CF hood roof trunk'}
  ]},
  drivetrain:{label:'Drivetrain Upgrade',icon:'&#128297;',opts:[
    {id:'keep',   name:'Stock Drivetrain',            cost:0,    desc:'No drivetrain changes'},
    {id:'lsd',    name:'Limited Slip Diff',            cost:2200, desc:'Better traction quicker exits'},
    {id:'awd',    name:'AWD Conversion Kit',           cost:16000,desc:'Full AWD ultimate grip'}
  ]}
};

var SWAPS = [
  {id:'k20c1', name:'Honda K20C1 Type R',      hp:315, ewt:255, wtd:-5,  cost:5800,  type:'I4 2.0L VTEC Turbo',   desc:'FWD king light and potent'},
  {id:'2jz',   name:'Toyota 2JZ-GTE',           hp:321, ewt:480, wtd:60,  cost:9200,  type:'I6 3.0L Twin Turbo',   desc:'Legend of the tuner world'},
  {id:'4b11t', name:'Mitsubishi 4B11T Evo X',   hp:291, ewt:310, wtd:30,  cost:4800,  type:'I4 2.0L Turbo DOHC',  desc:'Evo X engine light and fast'},
  {id:'ej257', name:'Subaru EJ257 STi',          hp:305, ewt:370, wtd:40,  cost:5200,  type:'Boxer-4 2.5L Turbo',  desc:'Rally heritage AWD-ready'},
  {id:'b58',   name:'BMW B58 Inline-6',          hp:382, ewt:420, wtd:60,  cost:8800,  type:'I6 3.0L Turbo DOHC',  desc:'Smooth strong very tuneable'},
  {id:'rb26',  name:'Nissan RB26DETT',           hp:280, ewt:500, wtd:90,  cost:9500,  type:'I6 2.6L Twin Turbo',  desc:'Skyline GT-R legend in iron'},
  {id:'s54',   name:'BMW S54 E46 M3',            hp:333, ewt:400, wtd:30,  cost:8200,  type:'I6 3.2L NA DOHC',     desc:'High-rev screamer pure driver'},
  {id:'coyote',name:'Ford Coyote 5.0 V8',        hp:435, ewt:445, wtd:55,  cost:7200,  type:'V8 5.0L DOHC',        desc:'Modern pony car powerplant'},
  {id:'ls3',   name:'Chevy LS3 V8',              hp:430, ewt:465, wtd:60,  cost:6800,  type:'V8 6.2L OHV',         desc:'American torque bulletproof'},
  {id:'lt1v8', name:'Chevy LT1 V8',              hp:455, ewt:455, wtd:55,  cost:7800,  type:'V8 6.2L OHV DI',      desc:'LS successor direct injection'},
  {id:'m156',  name:'Mercedes M156 V8',           hp:451, ewt:490, wtd:80,  cost:10500, type:'V8 6.2L NA DOHC',    desc:'AMG naturally aspirated monster'},
  {id:'vr38',  name:'Nissan VR38DETT GT-R',       hp:565, ewt:580, wtd:130, cost:14500, type:'V6 3.8L Twin Turbo', desc:'Godzilla engine pure grip'},
  {id:'lfav10',name:'Lexus LFA 1LR V10',          hp:562, ewt:460, wtd:80,  cost:22000, type:'V10 4.8L NA DOHC',   desc:'Carbon V10 F1-derived masterpiece'},
  {id:'w16',   name:'Bugatti W16 Quad-Turbo',     hp:1479,ewt:900, wtd:350, cost:95000, type:'W16 8.0L Quad Turbo',desc:'Absolute insanity go all-in'}
];

var EB_BLOCK = [
  {id:'i4',   name:'Inline-4',       baseHp:155, ewt:230, cost:1200,  icon:'&#9889;',  desc:'Light great turbo platform'},
  {id:'i6',   name:'Inline-6',       baseHp:220, ewt:375, cost:2800,  icon:'&#128309;',desc:'Silky smooth naturally balanced'},
  {id:'v6',   name:'V6',             baseHp:210, ewt:360, cost:2200,  icon:'&#128256;',desc:'Compact wide torque band'},
  {id:'v8sb', name:'V8 Small Block', baseHp:320, ewt:445, cost:4500,  icon:'&#128308;',desc:'Classic American torque'},
  {id:'v8bb', name:'V8 Big Block',   baseHp:420, ewt:560, cost:7500,  icon:'&#127825;',desc:'Heavy but massive displacement'},
  {id:'v10',  name:'V10',            baseHp:510, ewt:640, cost:15000, icon:'&#128995;',desc:'Exotic screaming powerplant'},
  {id:'v12',  name:'V12',            baseHp:600, ewt:740, cost:28000, icon:'&#11088;', desc:'Ultimate silky smooth power'}
];
var EB_DISP = {
  i4:  [{id:'1.6',lbl:'1.6L',m:0.85,c:0},{id:'2.0',lbl:'2.0L',m:1.00,c:500},{id:'2.3',lbl:'2.3L',m:1.12,c:900},{id:'2.5',lbl:'2.5L',m:1.22,c:1400}],
  i6:  [{id:'2.5',lbl:'2.5L',m:0.88,c:0},{id:'3.0',lbl:'3.0L',m:1.00,c:600},{id:'3.5',lbl:'3.5L',m:1.12,c:1200},{id:'4.0',lbl:'4.0L',m:1.25,c:2200}],
  v6:  [{id:'2.5',lbl:'2.5L',m:0.88,c:0},{id:'3.0',lbl:'3.0L',m:1.00,c:600},{id:'3.5',lbl:'3.5L',m:1.12,c:1200},{id:'3.8',lbl:'3.8L',m:1.22,c:1800}],
  v8sb:[{id:'5.0',lbl:'5.0L',m:1.00,c:0},{id:'5.3',lbl:'5.3L',m:1.06,c:800},{id:'5.7',lbl:'5.7L',m:1.14,c:1600},{id:'6.2',lbl:'6.2L',m:1.26,c:2800}],
  v8bb:[{id:'6.0',lbl:'6.0L',m:0.92,c:0},{id:'6.6',lbl:'6.6L',m:1.00,c:1000},{id:'7.0',lbl:'7.0L',m:1.12,c:2200},{id:'7.4',lbl:'7.4L',m:1.22,c:3500}],
  v10: [{id:'5.2',lbl:'5.2L',m:0.94,c:0},{id:'5.7',lbl:'5.7L',m:1.00,c:1200},{id:'6.0',lbl:'6.0L',m:1.07,c:2500},{id:'8.0',lbl:'8.0L',m:1.35,c:6000}],
  v12: [{id:'5.5',lbl:'5.5L',m:0.94,c:0},{id:'6.0',lbl:'6.0L',m:1.00,c:2000},{id:'6.5',lbl:'6.5L',m:1.07,c:4000},{id:'6.75',lbl:'6.75L',m:1.12,c:6000}]
};
var EB_HEAD = [
  {id:'ohv', name:'OHV Pushrod',m:0.86,c:0,    desc:'Low-RPM torque proven design'},
  {id:'sohc',name:'SOHC',       m:0.94,c:800,  desc:'Balanced power and efficiency'},
  {id:'dohc',name:'DOHC',       m:1.00,c:1800, desc:'High-revving peak power best HP/L'}
];
var EB_FI = [
  {id:'na',   name:'Naturally Aspirated',hpB:0,   c:0,    desc:'Pure linear power no lag'},
  {id:'turbo',name:'Single Turbo',       hpB:75,  c:3800, desc:'+75 HP spool then surge'},
  {id:'twin', name:'Twin Turbo',          hpB:160, c:8500, desc:'+160 HP wide powerband'},
  {id:'super',name:'Supercharged',        hpB:110, c:7200, desc:'+110 HP instant throttle'},
  {id:'quad', name:'Quad Turbo',          hpB:300, c:19000,desc:'+300 HP maximum insanity'}
];
var EB_TUNE = [
  {id:'street',name:'Street Tune',m:1.00,c:0,    desc:'Safe reliable daily driveable'},
  {id:'sport', name:'Sport Tune', m:1.06,c:800,  desc:'+6% HP optimized fuel maps'},
  {id:'race',  name:'Race Tune',  m:1.14,c:2000, desc:'+14% HP aggressive timing'},
  {id:'dyno',  name:'Dyno Tune',  m:1.20,c:4500, desc:'+20% HP session on the dyno'}
];

var DIFF = {
  amateur:{min:48, max:82,  prize:[2000,5000],   range:'$2,000-$5,000'},
  pro:    {min:88, max:148, prize:[8000,15000],  range:'$8,000-$15,000'},
  elite:  {min:162,max:245, prize:[20000,40000], range:'$20,000-$40,000'},
  legend: {min:280,max:485, prize:[50000,100000],range:'$50,000-$100,000'}
};

// ============================================================
// STATE
// ============================================================
var G = {
  money:25000,garage:[],wins:0,losses:0,
  buyPend:null,sellPend:null,swapPend:null,
  wsIdx:null,wsTab:'tune',
  wsM:null,wsB:null,
  raceIdx:null,raceType:'drag',raceDiff:'amateur'
};

function defMods(){
  return {intake:'stock',exhaust:'stock',forced:'none',internals:'stock',ecu:'stock',weight:'stock',drivetrain:'keep',
          engType:'stock',swapId:null,bBlock:'i4',bDisp:'2.0',bHead:'dohc',bFi:'na',bTune:'street',bPaid:0};
}

// ============================================================
// PHYSICS
// ============================================================
function calc60(hp,wt,dt){
  var f=dt==='AWD'?0.87:dt==='FWD'?1.05:1.00;
  return Math.max(1.8,0.65*Math.pow(wt/hp,0.85)*f);
}
function builtHp(m){
  var blk=EB_BLOCK.find(function(b){return b.id===m.bBlock;});
  var opts=EB_DISP[m.bBlock]||[];
  var disp=opts.find(function(d){return d.id===m.bDisp;});
  var head=EB_HEAD.find(function(h){return h.id===m.bHead;});
  var fi=EB_FI.find(function(f){return f.id===m.bFi;});
  var tune=EB_TUNE.find(function(t){return t.id===m.bTune;});
  if(!blk||!disp||!head||!fi||!tune)return 200;
  return Math.round((blk.baseHp*disp.m*head.m+fi.hpB)*tune.m);
}
function builtCost(m){
  var blk=EB_BLOCK.find(function(b){return b.id===m.bBlock;})||{cost:0};
  var opts=EB_DISP[m.bBlock]||[];
  var disp=opts.find(function(d){return d.id===m.bDisp;})||{c:0};
  var head=EB_HEAD.find(function(h){return h.id===m.bHead;})||{c:0};
  var fi=EB_FI.find(function(f){return f.id===m.bFi;})||{c:0};
  var tune=EB_TUNE.find(function(t){return t.id===m.bTune;})||{c:0};
  return blk.cost+disp.c+head.c+fi.c+tune.c;
}
function builtName(m){
  var blk=EB_BLOCK.find(function(b){return b.id===m.bBlock;})||{name:'Engine'};
  var opts=EB_DISP[m.bBlock]||[];
  var disp=opts.find(function(d){return d.id===m.bDisp;})||{lbl:''};
  var fi=EB_FI.find(function(f){return f.id===m.bFi;})||{name:'NA',id:'na'};
  return 'Custom '+disp.lbl+' '+blk.name+(fi.id!=='na'?' '+fi.name:'');
}
function builtEwt(m){
  var blk=EB_BLOCK.find(function(b){return b.id===m.bBlock;})||{ewt:300};
  return blk.ewt;
}
function calcPerf(car){
  var m=car.mods||defMods();
  var baseHp=car.hp,ewtDelta=0;
  if(m.engType==='swap'&&m.swapId){
    var sw=SWAPS.find(function(s){return s.id===m.swapId;});
    if(sw){baseHp=sw.hp;ewtDelta=sw.wtd;}
  } else if(m.engType==='built'){
    baseHp=builtHp(m);ewtDelta=builtEwt(m)-car.ewt;
  }
  var hp=baseHp;
  var ig=TGRPS.intake.opts.find(function(o){return o.id===m.intake;});
  var eg=TGRPS.exhaust.opts.find(function(o){return o.id===m.exhaust;});
  var fg=TGRPS.forced.opts.find(function(o){return o.id===m.forced;});
  var ug=TGRPS.ecu.opts.find(function(o){return o.id===m.ecu;});
  if(ig&&ig.hpM)hp*=ig.hpM;
  if(eg&&eg.hpM)hp*=eg.hpM;
  if(fg&&fg.hpB)hp+=fg.hpB;
  if(ug&&ug.hpM)hp*=ug.hpM;
  hp=Math.round(hp);
  var wg=TGRPS.weight.opts.find(function(o){return o.id===m.weight;})||{wtL:0};
  var carWt=Math.max(1500,Math.round(car.wt+ewtDelta-wg.wtL));
  var eDT=car.dt;
  if(m.drivetrain==='awd')eDT='AWD';
  var lsd=m.drivetrain==='lsd'?1.04:1.0;
  var z60=parseFloat(calc60(hp,carWt,eDT).toFixed(1));
  var score=Math.round(((hp*0.38)+((1/z60)*185))*lsd);
  return {hp:hp,wt:carWt,z60:z60,score:score,eDT:eDT};
}
function raceScore(car,type){
  var p=calcPerf(car),dt=p.eDT,s;
  if(type==='drag')         s=((p.hp*0.46)+((1/p.z60)*150))*(dt==='AWD'?1.09:dt==='FWD'?0.87:1.00);
  else if(type==='circuit') s=((p.hp*0.34)+((1/p.z60)*195))*(dt==='RWD'?1.07:dt==='FWD'?0.85:1.02);
  else if(type==='street')  s=((p.hp*0.30)+((1/p.z60)*215))*(dt==='AWD'?1.05:dt==='FWD'?0.90:1.00);
  else                      s=((p.hp*0.35)+((1/p.z60)*175))*(dt==='AWD'?1.15:dt==='FWD'?0.82:0.93);
  return Math.round(s);
}
function engLabel(car){
  var m=car.mods||defMods();
  if(m.engType==='swap'&&m.swapId){var sw=SWAPS.find(function(s){return s.id===m.swapId;});return sw?sw.name:'Swapped';}
  if(m.engType==='built')return builtName(m);
  return car.eng;
}

// ============================================================
// HELPERS
// ============================================================
function fmt(n){if(n>=1e6)return '$'+(n/1e6).toFixed(2)+'M';return '$'+Math.round(n).toLocaleString();}
function updateMoney(anim){
  var el=document.getElementById('moneyDisp');
  el.textContent=fmt(G.money).replace('$','');
  if(anim){el.classList.remove('bump');void el.offsetWidth;el.classList.add('bump');}
}
function updateRecord(){document.getElementById('hdrRecord').textContent=G.wins+'-'+G.losses;}
function notif(msg,color){
  var el=document.createElement('div');
  el.className='notif';el.style.color=color||'var(--text)';el.innerHTML=msg;
  document.body.appendChild(el);
  setTimeout(function(){el.remove();},2900);
}
function openModal(id){document.getElementById(id).classList.add('show');}
function closeModal(id){document.getElementById(id).classList.remove('show');}
document.querySelectorAll('.modal-wrap').forEach(function(m){
  m.addEventListener('click',function(e){if(e.target===m)closeModal(m.id);});
});

// ============================================================
// EVENT DELEGATION — eliminates all onclick string-arg escaping
// ============================================================
document.addEventListener('click', function(e) {
  var el = e.target.closest('[data-action]');
  if(!el) return;
  var action = el.dataset.action;
  var id     = el.dataset.id;
  var key    = el.dataset.key;
  var val    = el.dataset.val;
  var idx    = el.dataset.idx !== undefined ? parseInt(el.dataset.idx) : null;

  if(action==='buy')       promptBuy(id);
  if(action==='sell')      promptSell(idx);
  if(action==='workshop')  goWorkshop(idx);
  if(action==='swap')      promptSwap(id);
  if(action==='revert')    wsRevertStock();
  if(action==='tune-sel')  wsSelUpg(key, val);
  if(action==='build-sel') wsBuildSel(key, val);
  if(action==='ws-tab')    wsSelTab(val);
});

// ============================================================
// TAB NAV
// ============================================================
function goTab(name,btn){
  document.querySelectorAll('.tab').forEach(function(t){t.classList.remove('active');});
  document.querySelectorAll('.nav-btn').forEach(function(b){b.classList.remove('active');});
  document.getElementById('tab-'+name).classList.add('active');
  btn.classList.add('active');
  document.querySelector('.scroll-area').scrollTop=0;
  if(name==='garage')   renderGarage();
  if(name==='market')   renderMarket();
  if(name==='workshop'){wsRefreshDrop();if(G.wsIdx!==null)wsLoad();}
  if(name==='race')    {raceRefreshDrop();racePreview();}
}

// ============================================================
// MARKET
// ============================================================
var mktFilter='all';
function setFilter(el,f){
  document.querySelectorAll('.filter-bar .chip').forEach(function(c){c.classList.remove('active');});
  el.classList.add('active');mktFilter=f;renderMarket();
}
function renderMarket(){
  var cars=CARS.slice();
  if(mktFilter==='FWD'||mktFilter==='RWD'||mktFilter==='AWD')
    cars=cars.filter(function(c){return c.dt===mktFilter;});
  else if(['t1','t2','t3','t4'].indexOf(mktFilter)>=0)
    cars=cars.filter(function(c){return c.tier===parseInt(mktFilter[1]);});
  var ownedIds=G.garage.map(function(c){return c.id;});
  var grid=document.getElementById('mktGrid');
  if(!cars.length){
    grid.innerHTML='<div class="empty"><div class="empty-icon">&#128269;</div><h3>NO CARS</h3><p>Try a different filter</p></div>';
    return;
  }
  var html='';
  cars.forEach(function(car){
    var owned=ownedIds.indexOf(car.id)>=0;
    var canAfford=G.money>=car.price;
    var z60=parseFloat(calc60(car.hp,car.wt,car.dt).toFixed(1));
    html+='<div class="car-card">';
    html+='<div class="car-banner t'+car.tier+'"><div class="car-emoji">'+car.em+'</div></div>';
    html+='<div class="car-body">';
    html+='<div class="car-name">'+car.name+'</div>';
    html+='<div class="car-eng">'+car.eng+'</div>';
    html+='<div class="car-desc">'+car.desc+'</div>';
    html+='<div class="stat-row">';
    html+='<div class="stat-box"><div class="stat-lbl">HP</div><div class="stat-val">'+car.hp+'</div><div class="stat-unit">bhp</div></div>';
    html+='<div class="stat-box"><div class="stat-lbl">0-60</div><div class="stat-val">'+z60+'</div><div class="stat-unit">sec</div></div>';
    html+='<div class="stat-box"><div class="stat-lbl">Weight</div><div class="stat-val" style="font-size:12px;margin-top:3px">'+(car.wt/1000).toFixed(1)+'k</div><div class="stat-unit">lbs</div></div>';
    html+='<div class="stat-box"><div class="stat-lbl">Drive</div><div class="stat-val" style="font-size:13px;margin-top:2px">'+car.dt+'</div></div>';
    html+='</div>';
    html+='<div class="car-footer">';
    html+='<div><div class="car-price">'+fmt(car.price)+'</div><span class="dt-badge dt-'+car.dt+'">'+car.dt+'</span></div>';
    if(owned){
      html+='<span class="owned-tag">&#10003; OWNED</span>';
    } else if(canAfford){
      html+='<button class="btn btn-primary" data-action="buy" data-id="'+car.id+'">&#128179; Buy</button>';
    } else {
      html+='<button class="btn btn-primary" disabled>No funds</button>';
    }
    html+='</div></div></div>';
  });
  grid.innerHTML=html;
}
function promptBuy(id){
  var car=CARS.find(function(c){return c.id===id;});
  if(!car)return;
  G.buyPend=id;
  var z60=parseFloat(calc60(car.hp,car.wt,car.dt).toFixed(1));
  document.getElementById('buyTitle').textContent='Buy '+car.name+'?';
  document.getElementById('buyBody').innerHTML='<strong>'+car.name+'</strong><br>'+car.eng+'<br><br>&#128176; Price: <strong>'+fmt(car.price)+'</strong><br>&#9889; HP: <strong>'+car.hp+'</strong> | 0-60: <strong>'+z60+'s</strong><br>&#9878; Weight: <strong>'+car.wt.toLocaleString()+' lbs</strong> | Drive: <strong>'+car.dt+'</strong><br><br>Balance after: <strong>'+fmt(G.money-car.price)+'</strong>';
  openModal('buyModal');
}
function confirmBuy(){
  var car=CARS.find(function(c){return c.id===G.buyPend;});
  if(!car||G.money<car.price)return;
  G.money-=car.price;
  var entry=Object.assign({},car,{mods:defMods(),purchasePrice:car.price,gid:Date.now()});
  G.garage.push(entry);
  updateMoney(true);closeModal('buyModal');
  notif('&#127958; Bought '+car.name+'!','var(--green)');
  renderMarket();wsRefreshDrop();raceRefreshDrop();
}

// ============================================================
// GARAGE
// ============================================================
function renderGarage(){
  var grid=document.getElementById('garGrid');
  var n=G.garage.length;
  document.getElementById('garSub').textContent=n+' car'+(n!==1?'s':'')+' owned';
  if(!n){
    grid.innerHTML='<div class="empty"><div class="empty-icon">&#127937;</div><h3>EMPTY GARAGE</h3><p>Buy a car from the Marketplace</p></div>';
    return;
  }
  var html='';
  G.garage.forEach(function(car,idx){
    var p=calcPerf(car);
    var sv=Math.round(car.purchasePrice*0.70);
    var dm=defMods();
    var hasMods=TUNE_KEYS.some(function(k){return car.mods[k]!==dm[k];});
    var hasEng=car.mods.engType!=='stock';
    html+='<div class="car-card">';
    html+='<div class="car-banner t'+car.tier+'"><div class="car-emoji">'+car.em+'</div></div>';
    html+='<div class="car-body">';
    html+='<div class="flex-sb" style="margin-bottom:3px">';
    html+='<div class="car-name">'+car.name+'</div>';
    html+='<div style="display:flex;gap:4px">';
    if(hasEng) html+='<span class="eng-tag">&#128297; ENG</span>';
    if(hasMods) html+='<span class="mod-tag">&#128295; MOD</span>';
    html+='</div></div>';
    html+='<div class="car-eng">'+engLabel(car)+'</div>';
    html+='<div class="stat-row" style="margin-top:8px">';
    html+='<div class="stat-box"><div class="stat-lbl">HP</div><div class="stat-val">'+p.hp+'</div><div class="stat-unit">bhp</div></div>';
    html+='<div class="stat-box"><div class="stat-lbl">0-60</div><div class="stat-val">'+p.z60+'</div><div class="stat-unit">sec</div></div>';
    html+='<div class="stat-box"><div class="stat-lbl">Weight</div><div class="stat-val" style="font-size:12px;margin-top:3px">'+(p.wt/1000).toFixed(1)+'k</div><div class="stat-unit">lbs</div></div>';
    html+='<div class="stat-box"><div class="stat-lbl">Score</div><div class="stat-val">'+p.score+'</div><div class="stat-unit">pts</div></div>';
    html+='</div>';
    html+='<div class="flex-sb" style="margin-top:8px">';
    html+='<span class="dt-badge dt-'+p.eDT+'">'+p.eDT+'</span>';
    html+='<span style="font-size:11px;color:var(--text2)">Sell: <strong style="color:var(--gold)">'+fmt(sv)+'</strong></span>';
    html+='</div></div>';
    html+='<div class="gar-actions">';
    html+='<button class="btn btn-ghost" data-action="workshop" data-idx="'+idx+'">&#128295; Workshop</button>';
    html+='<button class="btn btn-danger" data-action="sell" data-idx="'+idx+'">&#128181; Sell</button>';
    html+='</div></div>';
  });
  grid.innerHTML=html;
}
function goWorkshop(idx){
  G.wsIdx=idx;G.wsTab='tune';
  document.querySelectorAll('.tab').forEach(function(t){t.classList.remove('active');});
  document.querySelectorAll('.nav-btn').forEach(function(b){b.classList.remove('active');});
  document.getElementById('tab-workshop').classList.add('active');
  document.querySelectorAll('.nav-btn')[2].classList.add('active');
  document.querySelector('.scroll-area').scrollTop=0;
  wsRefreshDrop();wsLoad();
}
function promptSell(idx){
  var car=G.garage[idx];if(!car)return;
  var sv=Math.round(car.purchasePrice*0.70);G.sellPend=idx;
  document.getElementById('sellTitle').textContent='Sell '+car.name+'?';
  document.getElementById('sellBody').innerHTML='Receive <strong>'+fmt(sv)+'</strong> (70%).<br>All mods and engines will be lost.<br><br>New balance: <strong>'+fmt(G.money+sv)+'</strong>';
  openModal('sellModal');
}
function confirmSell(){
  var idx=G.sellPend;
  if(idx===null||idx===undefined||!G.garage[idx])return;
  var car=G.garage[idx];var sv=Math.round(car.purchasePrice*0.70);
  G.money+=sv;G.garage.splice(idx,1);
  if(G.wsIdx===idx)G.wsIdx=null; else if(G.wsIdx!==null&&G.wsIdx>idx)G.wsIdx--;
  if(G.raceIdx===idx)G.raceIdx=null; else if(G.raceIdx!==null&&G.raceIdx>idx)G.raceIdx--;
  updateMoney(true);closeModal('sellModal');
  notif('&#128181; Sold '+car.name+' for '+fmt(sv),'var(--gold)');
  renderGarage();renderMarket();wsRefreshDrop();raceRefreshDrop();
  if(G.wsIdx===null)document.getElementById('wsContent').style.display='none';
}

// ============================================================
// WORKSHOP
// ============================================================
function wsRefreshDrop(){
  var sel=document.getElementById('wsCar');
  var html='<option value="">&#8212; Choose from your garage &#8212;</option>';
  G.garage.forEach(function(c,i){
    html+='<option value="'+i+'"'+(i===G.wsIdx?' selected':'')+'>'+c.name+'</option>';
  });
  sel.innerHTML=html;
}
function wsLoad(){
  var sel=document.getElementById('wsCar');
  var v=sel.value;
  var idx=v!==''?parseInt(v):null;
  G.wsIdx=idx;
  var cont=document.getElementById('wsContent');
  if(idx===null||!G.garage[idx]){cont.style.display='none';return;}
  G.wsM=Object.assign({},G.garage[idx].mods);
  G.wsB={block:G.garage[idx].mods.bBlock||'i4',disp:G.garage[idx].mods.bDisp||'2.0',
         head:G.garage[idx].mods.bHead||'dohc',fi:G.garage[idx].mods.bFi||'na',
         tune:G.garage[idx].mods.bTune||'street'};
  cont.style.display='block';
  wsRender();
}
function wsSelTab(t){G.wsTab=t;wsRender();}

function wsRender(){
  var idx=G.wsIdx;var car=G.garage[idx];if(!car)return;
  var p=calcPerf(Object.assign({},car,{mods:G.wsM}));
  var pb=calcPerf(Object.assign({},car,{mods:defMods()}));
  var MAX=600;
  var el=engLabel(Object.assign({},car,{mods:G.wsM}));
  var html='';

  // Perf card
  html+='<div class="perf-card">';
  html+='<div class="perf-title">PERFORMANCE</div>';
  html+='<div class="pgrid">';
  html+=piH(p.hp,'HP',p.hp-pb.hp,false);
  html+=piH(p.z60+'s','0-60',parseFloat((p.z60-pb.z60).toFixed(1)),true);
  html+=piH((p.wt/1000).toFixed(1)+'k','Wt lbs',p.wt-pb.wt,true);
  html+=piH(p.score,'Score',0,false);
  html+='</div>';
  html+='<div class="score-bar-wrap">';
  html+='<div class="score-bar-lbl"><span>Performance Rating</span><span>'+p.score+' pts</span></div>';
  html+='<div class="score-bar-track"><div class="score-bar-fill" style="width:'+Math.min(100,p.score/MAX*100).toFixed(1)+'%"></div></div>';
  html+='</div>';
  html+='<div class="eng-bar"><span style="font-size:14px">&#128297;</span><div><div class="eng-bar-name">'+el+'</div><div class="eng-bar-sub">'+G.wsM.engType+' engine &middot; '+p.eDT+'</div></div></div>';
  html+='</div>';

  // Sub-tabs using data-action
  html+='<div class="ws-stabs">';
  html+='<button class="ws-stab'+(G.wsTab==='tune'?' active':'')+'" data-action="ws-tab" data-val="tune">&#128295; Tune</button>';
  html+='<button class="ws-stab'+(G.wsTab==='swap'?' active':'')+'" data-action="ws-tab" data-val="swap">&#128260; Swap Engine</button>';
  html+='<button class="ws-stab'+(G.wsTab==='build'?' active':'')+'" data-action="ws-tab" data-val="build">&#9881; Build Engine</button>';
  html+='</div>';

  if(G.wsTab==='tune')       html+=wsTune(car);
  else if(G.wsTab==='swap')  html+=wsSwap(car);
  else if(G.wsTab==='build') html+=wsBuild(car);

  html+='<div style="height:12px"></div>';
  document.getElementById('wsContent').innerHTML=html;
}

function piH(val,lbl,delta,lessIsBetter){
  var h='<div class="pi"><div class="pi-val">'+val+'</div><div class="pi-lbl">'+lbl+'</div>';
  if(delta!==0&&delta!==undefined&&delta!==null){
    var pos=lessIsBetter?delta<0:delta>0;
    h+='<div class="pi-d" style="color:'+(pos?'var(--green)':'var(--red)')+'">'+(delta>=0?'+':'')+delta+'</div>';
  }
  return h+'</div>';
}

// ---- TUNE ----
function wsTune(car){
  var m=G.wsM,html='';
  TUNE_KEYS.forEach(function(key){
    var grp=TGRPS[key];
    html+='<div class="section-box"><div class="section-hdr"><span class="section-hdr-icon">'+grp.icon+'</span><h3>'+grp.label+'</h3>';
    if(key==='weight')html+='<span class="section-hdr-note">Affects 0-60!</span>';
    html+='</div><div class="opts">';
    grp.opts.forEach(function(opt){
      var isSel=m[key]===opt.id;
      var isInstd=car.mods[key]===opt.id;
      var cost=isInstd?0:(opt.cost||0);
      var costTxt=isInstd?'INSTALLED':cost===0?'FREE':fmt(cost);
      var cc=isInstd?'c-instd':cost===0?'c-free':'c-paid';
      var nm=opt.name;
      if(opt.wtL&&opt.wtL>0)nm+=' <span style="color:var(--green);font-size:10px">-'+opt.wtL+'lbs</span>';
      if(opt.hpB&&opt.hpB>0)nm+=' <span style="color:var(--orange);font-size:10px">+'+opt.hpB+'hp</span>';
      html+='<div class="opt'+(isSel?' sel-opt':'')+'" data-action="tune-sel" data-key="'+key+'" data-val="'+opt.id+'">';
      html+='<div class="opt-check">'+(isSel?'&#10003;':'')+'</div>';
      html+='<div class="opt-info"><div class="opt-name">'+nm+'</div><div class="opt-desc">'+opt.desc+'</div></div>';
      html+='<div class="opt-cost '+cc+'">'+costTxt+'</div>';
      html+='</div>';
    });
    html+='</div></div>';
  });
  var total=0,breakdown='';
  TUNE_KEYS.forEach(function(key){
    if(m[key]!==car.mods[key]){
      var opt=TGRPS[key].opts.find(function(o){return o.id===m[key];});
      if(opt&&opt.cost){total+=opt.cost;breakdown+='<div class="cost-line"><span>'+opt.name+'</span><span>'+fmt(opt.cost)+'</span></div>';}
    }
  });
  var canAfford=G.money>=total;
  html+='<div class="cost-box"><div class="cost-box-title">Upgrade Cost</div>';
  html+=breakdown||'<div style="font-size:12px;color:var(--text3);margin-bottom:6px">No pending changes</div>';
  if(total>0)html+='<div class="cost-total"><span>Total</span><span>'+fmt(total)+'</span></div>';
  if(total>0&&!canAfford)html+='<div class="warn">&#9888; Need '+fmt(total-G.money)+' more</div>';
  html+='</div>';
  html+='<button class="btn btn-primary btn-full btn-lg" onclick="wsApplyTune()"'+(!total||!canAfford?' disabled':'')+'>'+(!total?'&#10003; No Changes':'&#128295; Apply Tune &#8212; '+fmt(total))+'</button>';
  return html;
}
function wsSelUpg(key,id){if(G.wsM)G.wsM[key]=id;wsRender();}
function wsApplyTune(){
  var idx=G.wsIdx;if(idx===null||!G.garage[idx])return;
  var car=G.garage[idx],m=G.wsM,total=0;
  TUNE_KEYS.forEach(function(key){
    if(m[key]!==car.mods[key]){var opt=TGRPS[key].opts.find(function(o){return o.id===m[key];});if(opt&&opt.cost)total+=opt.cost;}
  });
  if(G.money<total){notif('&#9888; Not enough money!','var(--red)');return;}
  G.money-=total;
  TUNE_KEYS.forEach(function(k){G.garage[idx].mods[k]=m[k];});
  G.wsM=Object.assign({},G.garage[idx].mods);
  updateMoney(total>0);notif('&#9989; Upgrades applied!','var(--green)');wsRender();
}

// ---- SWAP ----
function wsSwap(car){
  var m=G.wsM,html='';
  html+='<div class="section-box" style="margin-bottom:12px">';
  html+='<div class="section-hdr"><span class="section-hdr-icon">&#128260;</span><h3>Currently Installed</h3></div>';
  html+='<div style="padding:12px">';
  html+='<div style="font-weight:700;font-size:13px">'+engLabel(Object.assign({},car,{mods:m}))+'</div>';
  html+='<div style="font-size:11px;color:var(--text2);margin-top:3px">'+(m.engType==='stock'?'Stock engine &mdash; tap a swap below':'Swapped &mdash; tap another to replace')+'</div>';
  if(m.engType!=='stock')html+='<button class="btn btn-danger btn-full" style="margin-top:10px" data-action="revert">&#8617; Revert to Stock</button>';
  html+='</div></div>';
  SWAPS.forEach(function(sw){
    var isInst=m.engType==='swap'&&m.swapId===sw.id;
    var canAfford=G.money>=sw.cost;
    var wtCol=sw.wtd<=0?'var(--green)':'var(--red)';
    html+='<div class="swap-card'+(isInst?' sw-inst':'')+'">';
    html+='<div class="swap-head">';
    html+='<div><div class="swap-name">'+sw.name+'</div><span class="swap-type">'+sw.type+'</span></div>';
    html+='<div style="text-align:right;flex-shrink:0">';
    if(isInst)html+='<span class="owned-tag">&#10003; INSTALLED</span>';
    else html+='<div class="swap-price">'+fmt(sw.cost)+'</div>';
    html+='</div></div>';
    html+='<div class="swap-stats">';
    html+='<div class="sw-stat"><div class="sw-stat-lbl">HP</div><div class="sw-stat-val">'+sw.hp+'</div></div>';
    html+='<div class="sw-stat"><div class="sw-stat-lbl">Eng Wt</div><div class="sw-stat-val" style="font-size:13px;margin-top:2px">'+sw.ewt+'</div></div>';
    html+='<div class="sw-stat"><div class="sw-stat-lbl">Car &#916;Wt</div><div class="sw-stat-val" style="font-size:13px;margin-top:2px;color:'+wtCol+'">'+(sw.wtd>=0?'+':'')+sw.wtd+'</div></div>';
    html+='</div>';
    html+='<div class="swap-foot"><div class="swap-foot-desc">'+sw.desc+'</div>';
    if(!isInst)html+='<button class="btn btn-gold" data-action="swap" data-id="'+sw.id+'"'+(canAfford?'':' disabled')+'>'+(canAfford?'Install':'No funds')+'</button>';
    html+='</div></div>';
  });
  return html;
}
function promptSwap(id){
  var sw=SWAPS.find(function(s){return s.id===id;});if(!sw)return;
  G.swapPend=id;
  document.getElementById('swapTitle').textContent='Install '+sw.name+'?';
  document.getElementById('swapBody').innerHTML='<strong>'+sw.name+'</strong><br>'+sw.type+'<br><br>&#9889; HP: <strong>'+sw.hp+'</strong><br>&#9878; Car weight change: <strong>'+(sw.wtd>=0?'+':'')+sw.wtd+' lbs</strong><br>&#128176; Cost: <strong>'+fmt(sw.cost)+'</strong><br><br>Current engine removed. Tune mods still apply.<br><br>Balance after: <strong>'+fmt(G.money-sw.cost)+'</strong>';
  openModal('swapModal');
}
function confirmSwap(){
  var idx=G.wsIdx;if(idx===null||!G.garage[idx])return;
  var sw=SWAPS.find(function(s){return s.id===G.swapPend;});if(!sw)return;
  if(G.money<sw.cost){notif('&#9888; Not enough money!','var(--red)');closeModal('swapModal');return;}
  G.money-=sw.cost;
  G.garage[idx].mods.engType='swap';G.garage[idx].mods.swapId=sw.id;
  G.wsM.engType='swap';G.wsM.swapId=sw.id;
  updateMoney(true);closeModal('swapModal');
  notif('&#128297; Installed '+sw.name+'!','var(--gold)');wsRender();
}
function wsRevertStock(){
  var idx=G.wsIdx;if(idx===null||!G.garage[idx])return;
  G.garage[idx].mods.engType='stock';G.garage[idx].mods.swapId=null;
  G.wsM.engType='stock';G.wsM.swapId=null;
  notif('&#8617; Reverted to stock engine','var(--text2)');wsRender();
}

// ---- BUILD ----
function wsBuild(car){
  var pb=G.wsB;
  var dOpts=EB_DISP[pb.block]||[];
  if(!dOpts.find(function(d){return d.id===pb.disp;}))pb.disp=dOpts[0]?dOpts[0].id:'2.0';
  var bm={bBlock:pb.block,bDisp:pb.disp,bHead:pb.head,bFi:pb.fi,bTune:pb.tune};
  var bHp=builtHp(bm);
  var bEwt=builtEwt(bm);
  var bWtD=bEwt-car.ewt;
  var bWg=TGRPS.weight.opts.find(function(o){return o.id===G.wsM.weight;})||{wtL:0};
  var bWt=Math.max(1500,car.wt+bWtD-bWg.wtL);
  var bDT=G.wsM.drivetrain==='awd'?'AWD':car.dt;
  var bZ60=parseFloat(calc60(bHp,bWt,bDT).toFixed(1));
  var bCostNew=builtCost(bm);
  var bCostPaid=car.mods.engType==='built'?(car.mods.bPaid||0):0;
  var bDue=Math.max(0,bCostNew-bCostPaid);
  var canAfford=G.money>=bDue;

  var html='<div class="bld-preview">';
  html+='<div class="bld-preview-title">ENGINE PREVIEW</div>';
  html+='<div class="bld-name">'+builtName(bm)+'</div>';
  html+='<div class="bld-stats">';
  html+='<div class="bld-stat"><div class="bld-stat-val">'+bHp+'</div><div class="bld-stat-lbl">HP Output</div></div>';
  html+='<div class="bld-stat"><div class="bld-stat-val">'+bZ60+'s</div><div class="bld-stat-lbl">Est. 0-60</div></div>';
  html+='<div class="bld-stat"><div class="bld-stat-val" style="font-size:16px;margin-top:3px;color:'+(bWtD<=0?'var(--green)':'var(--red)')+'">'+( bWtD>=0?'+':'')+bWtD+'</div><div class="bld-stat-lbl">Wt &#916; lbs</div></div>';
  html+='</div>';
  html+='<div class="cost-line" style="margin-top:4px"><span>Build Cost</span><span style="color:var(--gold);font-weight:700">'+fmt(bCostNew)+'</span></div>';
  if(bCostPaid>0)html+='<div class="cost-line"><span>Already paid</span><span style="color:var(--green)">-'+fmt(bCostPaid)+'</span></div>';
  html+='<div class="cost-total"><span>Amount Due</span><span>'+fmt(bDue)+'</span></div>';
  if(!canAfford&&bDue>0)html+='<div class="warn">&#9888; Need '+fmt(bDue-G.money)+' more</div>';
  html+='</div>';

  html+=bSection('&#128297;','Engine Block','STEP 1',EB_BLOCK,'block',pb.block,function(b){return b.icon+' '+b.name+' <span style="font-size:10px;color:var(--text2)">('+b.ewt+'lbs)</span>';},function(b){return b.desc;},function(b){return b.cost;});
  html+=bSection('&#128208;','Displacement','STEP 2',dOpts,'disp',pb.disp,function(d){return d.lbl;},function(d){return 'x'+d.m+' HP mult';},function(d){return d.c;});
  html+=bSection('&#128309;','Cylinder Head','STEP 3',EB_HEAD,'head',pb.head,function(h){return h.name;},function(h){return h.desc;},function(h){return h.c;});
  html+=bSection('&#127754;','Forced Induction','STEP 4',EB_FI,'fi',pb.fi,function(f){return f.name+(f.hpB>0?' <span style="color:var(--orange);font-size:10px">+'+f.hpB+'hp</span>':'');},function(f){return f.desc;},function(f){return f.c;});
  html+=bSection('&#128187;','Engine Tune','STEP 5',EB_TUNE,'tune',pb.tune,function(t){return t.name+' <span style="color:var(--orange);font-size:10px">x'+t.m+'</span>';},function(t){return t.desc;},function(t){return t.c;});

  html+='<button class="btn btn-purple btn-full btn-lg" onclick="wsInstallBuild()"'+(!canAfford&&bDue>0?' disabled':'')+'>&#9881; Install Built Engine'+(bDue>0?' &#8212; '+fmt(bDue):'')+'</button>';
  if(car.mods.engType==='built')html+='<button class="btn btn-danger btn-full" style="margin-top:6px" data-action="revert">&#8617; Revert to Stock</button>';
  return html;
}

function bSection(icon,label,step,items,field,curVal,nameFn,descFn,costFn){
  var html='<div class="section-box"><div class="section-hdr"><span class="section-hdr-icon">'+icon+'</span><h3>'+label+'</h3><span class="section-hdr-step">'+step+'</span></div><div class="opts">';
  items.forEach(function(item){
    var sel=curVal===item.id;
    var cost=costFn(item);
    html+='<div class="opt'+(sel?' sel-build':'')+'" data-action="build-sel" data-key="'+field+'" data-val="'+item.id+'">';
    html+='<div class="opt-check">'+(sel?'&#10003;':'')+'</div>';
    html+='<div class="opt-info"><div class="opt-name">'+nameFn(item)+'</div><div class="opt-desc">'+descFn(item)+'</div></div>';
    html+='<div class="opt-cost '+(cost===0?'c-free':'c-paid')+'">'+(cost===0?'FREE':fmt(cost))+'</div>';
    html+='</div>';
  });
  return html+'</div></div>';
}
function wsBuildSel(field,val){
  if(!G.wsB)return;
  G.wsB[field]=val;
  if(field==='block'){
    var opts=EB_DISP[val]||[];
    if(!opts.find(function(d){return d.id===G.wsB.disp;}))G.wsB.disp=opts[0]?opts[0].id:'2.0';
  }
  wsRender();
}
function wsInstallBuild(){
  var idx=G.wsIdx;if(idx===null||!G.garage[idx])return;
  var car=G.garage[idx],pb=G.wsB;
  var bm={bBlock:pb.block,bDisp:pb.disp,bHead:pb.head,bFi:pb.fi,bTune:pb.tune};
  var bCostNew=builtCost(bm);
  var bCostPaid=car.mods.engType==='built'?(car.mods.bPaid||0):0;
  var due=Math.max(0,bCostNew-bCostPaid);
  if(G.money<due){notif('&#9888; Not enough money!','var(--red)');return;}
  G.money-=due;
  Object.assign(G.garage[idx].mods,{engType:'built',swapId:null,bBlock:pb.block,bDisp:pb.disp,bHead:pb.head,bFi:pb.fi,bTune:pb.tune,bPaid:bCostNew});
  G.wsM=Object.assign({},G.garage[idx].mods);
  updateMoney(due>0);notif('&#9881; Custom engine installed!','var(--purple)');wsRender();
}

// ============================================================
// RACE
// ============================================================
function raceRefreshDrop(){
  var sel=document.getElementById('raceCar');
  var html='<option value="">&#8212; Choose your car &#8212;</option>';
  G.garage.forEach(function(c,i){html+='<option value="'+i+'"'+(i===G.raceIdx?' selected':'')+'>'+c.name+'</option>';});
  sel.innerHTML=html;
}
function selRType(el){
  document.querySelectorAll('.rtype').forEach(function(b){b.classList.remove('rsel');});
  el.classList.add('rsel');G.raceType=el.dataset.type;racePreview();
}
function selDiff(el){
  document.querySelectorAll('.diff').forEach(function(b){b.classList.remove('dsel');});
  el.classList.add('dsel');G.raceDiff=el.dataset.diff;racePreview();
}
function racePreview(){
  var sel=document.getElementById('raceCar');
  var v=sel.value;
  var idx=v!==''?parseInt(v):null;
  G.raceIdx=idx;
  var rBtn=document.getElementById('raceBtn');
  var prevBox=document.getElementById('raceCarPreview');
  var oddsBox=document.getElementById('oddsBox');
  if(idx===null||!G.garage[idx]){prevBox.style.display='none';oddsBox.style.display='none';rBtn.disabled=true;return;}
  var car=G.garage[idx];
  var p=calcPerf(car);
  var rs=raceScore(car,G.raceType);
  var d=DIFF[G.raceDiff];
  var avg=(d.min+d.max)/2;
  var wPct=Math.round((1/(1+Math.exp(-(rs-avg)/26)))*100);
  var wCol=wPct>60?'var(--green)':wPct>40?'var(--orange)':'var(--red)';
  prevBox.style.display='block';
  var ph='<div class="perf-card" style="margin-bottom:0"><div class="perf-title" style="font-size:12px;margin-bottom:8px">'+car.name+'</div><div class="pgrid">';
  ph+=piH(p.hp,'HP',0,false);ph+=piH(p.z60+'s','0-60',0,false);ph+=piH((p.wt/1000).toFixed(1)+'k','Wt lbs',0,false);ph+=piH(p.score,'Score',0,false);
  ph+='</div></div>';
  prevBox.innerHTML=ph;
  oddsBox.style.display='block';
  var oh='<div class="odds-scores"><div class="odds-score-item"><div class="odds-score-lbl">Your Score</div><div class="odds-score-val" style="color:var(--orange)">'+rs+'</div></div><div class="odds-score-item"><div class="odds-score-lbl">Avg Opponent</div><div class="odds-score-val" style="color:var(--red)">'+Math.round(avg)+'</div></div></div>';
  oh+='<div class="win-wrap"><div class="win-lbl">Win Chance</div><div class="win-track"><div class="win-fill" style="width:'+wPct+'%;background:'+wCol+'"></div></div><div class="win-pct" style="color:'+wCol+'">'+wPct+'%</div></div>';
  oh+='<div style="margin-top:8px;font-size:10px;color:var(--text3);font-weight:600">PRIZE RANGE: '+d.range+'</div>';
  document.getElementById('oddsContent').innerHTML=oh;
  rBtn.disabled=false;
}
function startRace(){
  var idx=G.raceIdx;if(idx===null||!G.garage[idx])return;
  var car=G.garage[idx];
  document.getElementById('raceBtn').disabled=true;
  document.getElementById('animCarName').textContent=car.name+' \u2014 '+G.raceType.toUpperCase();
  var anim=document.getElementById('raceAnim');
  var cdEl=document.getElementById('cdNum');
  var pEl=document.getElementById('animP');
  var oEl=document.getElementById('animO');
  pEl.classList.remove('go');oEl.classList.remove('go');
  pEl.style.left='-8%';oEl.style.left='-8%';
  cdEl.className='cd-num';cdEl.innerHTML='3';
  anim.classList.add('show');
  var count=3;
  function tick(){
    cdEl.className='cd-num';void cdEl.offsetWidth;cdEl.className='cd-num';
    cdEl.innerHTML=count>0?count:'GO!';
    if(count===0)cdEl.classList.add('go');
    if(count>0){count--;setTimeout(tick,700);}
    else{
      pEl.classList.add('go');oEl.classList.add('go');
      setTimeout(function(){
        anim.classList.remove('show');
        document.getElementById('raceBtn').disabled=false;
        doRaceResult(car);
      },2100);
    }
  }
  tick();
}
function doRaceResult(car){
  var rs=raceScore(car,G.raceType);
  var d=DIFF[G.raceDiff];
  var opp=d.min+Math.random()*(d.max-d.min);
  var wc=1/(1+Math.exp(-(rs-opp)/26));
  var won=Math.random()<wc;
  var prize=won
    ?Math.round(d.prize[0]+Math.random()*(d.prize[1]-d.prize[0]))
    :Math.round(d.prize[0]*0.05+Math.random()*d.prize[0]*0.08);
  G.money+=prize;won?G.wins++:G.losses++;
  updateMoney(true);updateRecord();
  var wcPct=Math.round(wc*100);
  var wCol=wcPct>60?'var(--green)':wcPct>40?'var(--orange)':'var(--red)';
  var rh='<div class="res-emoji">'+(won?'&#127942;':'&#128168;')+'</div>';
  rh+='<div class="res-verdict '+(won?'win':'lose')+'">'+(won?'VICTORY!':'DEFEAT')+'</div>';
  rh+='<div class="res-sub">'+(won?'You crossed the line first!':'The opponent edged you out.')+'</div>';
  rh+='<div class="res-prize">+'+fmt(prize)+'</div>';
  rh+='<div class="res-prize-lbl">'+(won?'PRIZE WINNINGS':'CONSOLATION PAY')+'</div>';
  rh+='<div class="res-stats">';
  rh+='<div class="rs-item"><div class="rs-lbl">Your Score</div><div class="rs-val" style="color:var(--orange)">'+rs+'</div></div>';
  rh+='<div class="rs-item"><div class="rs-lbl">Opponent</div><div class="rs-val" style="color:var(--red)">'+Math.round(opp)+'</div></div>';
  rh+='<div class="rs-item"><div class="rs-lbl">Win Chance</div><div class="rs-val" style="color:'+wCol+'">'+wcPct+'%</div></div>';
  rh+='<div class="rs-item"><div class="rs-lbl">Record</div><div class="rs-val" style="font-size:15px">'+G.wins+'W/'+G.losses+'L</div></div>';
  rh+='</div><button class="btn btn-primary btn-full" onclick="closeRaceResult()">Continue Racing</button>';
  document.getElementById('resultCard').innerHTML=rh;
  document.getElementById('raceResult').classList.add('show');
}
function closeRaceResult(){document.getElementById('raceResult').classList.remove('show');racePreview();}

// ============================================================
// INIT
// ============================================================
updateMoney();updateRecord();renderGarage();renderMarket();
</script>
</body>
</html>