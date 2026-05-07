<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Seta Lab — Hub de Ferramentas</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,400&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0c0b10;
  --bg2:#13111c;
  --bg3:#1a1726;
  --bg4:#221f30;
  --surface:#1e1b2b;
  --border:rgba(138,92,246,.14);
  --border-m:rgba(138,92,246,.28);
  --purple:#8B5CF6;
  --purple-l:#a78bfa;
  --purple-d:#6d28d9;
  --purple-glow:rgba(139,92,246,.18);
  --text:#f0ede8;
  --text-2:#b0adb8;
  --text-3:#6e6b7a;
  --accent:#c4b5fd;
  --green:#22c55e;
  --green-bg:rgba(34,197,94,.08);
  --red:#f87171;
  --red-bg:rgba(248,113,113,.08);
  --amber:#fbbf24;
  --r:10px;
  --r2:14px;
  --sidebar-w:220px;
}

body{background:var(--bg);color:var(--text);font-family:'DM Sans',sans-serif;font-size:14px;line-height:1.6;min-height:100vh;overflow-x:hidden}

/* GRAIN */
body::before{content:'';position:fixed;inset:0;background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");pointer-events:none;z-index:0;opacity:.6}

/* LAYOUT */
.app{display:flex;min-height:100vh;position:relative;z-index:1}

/* SIDEBAR */
.sidebar{
  width:var(--sidebar-w);
  min-height:100vh;
  background:var(--bg2);
  border-right:1px solid var(--border);
  display:flex;
  flex-direction:column;
  position:fixed;
  left:0;top:0;bottom:0;
  z-index:50;
  transition:transform .3s ease;
}

.sidebar-logo{
  padding:20px 18px 0;
  display:flex;
  align-items:center;
  gap:10px;
  margin-bottom:28px;
}
.sidebar-logo img{width:32px;height:32px;object-fit:contain}
.sidebar-logo-text{font-family:'Syne',sans-serif;font-size:13px;font-weight:700;color:var(--purple-l);letter-spacing:-.01em}
.sidebar-logo-sub{font-size:10px;color:var(--text-3);font-weight:400}

.sidebar-section-label{
  font-size:9px;
  font-weight:700;
  letter-spacing:.12em;
  text-transform:uppercase;
  color:var(--text-3);
  padding:0 18px;
  margin-bottom:6px;
  margin-top:4px;
}

.nav-item{
  display:flex;
  align-items:center;
  gap:10px;
  padding:9px 18px;
  border-radius:0;
  cursor:pointer;
  color:var(--text-3);
  font-size:13px;
  font-weight:500;
  transition:all .15s;
  position:relative;
  margin:1px 8px;
  border-radius:8px;
}
.nav-item:hover{color:var(--text);background:var(--bg3)}
.nav-item.active{
  color:var(--purple-l);
  background:var(--purple-glow);
}
.nav-item.active::before{
  content:'';
  position:absolute;
  left:-8px;top:6px;bottom:6px;
  width:3px;
  background:var(--purple);
  border-radius:0 3px 3px 0;
}
.nav-icon{width:16px;height:16px;flex-shrink:0;opacity:.7}
.nav-item.active .nav-icon{opacity:1}

.sidebar-footer{
  margin-top:auto;
  padding:16px 18px;
  border-top:1px solid var(--border);
}
.credit{font-size:10px;color:var(--text-3);line-height:1.5}
.credit strong{color:var(--text-2);font-weight:500}

/* MAIN */
.main{
  margin-left:var(--sidebar-w);
  flex:1;
  display:flex;
  flex-direction:column;
  min-height:100vh;
}

/* TOPBAR */
.topbar{
  height:54px;
  background:var(--bg2);
  border-bottom:1px solid var(--border);
  display:flex;
  align-items:center;
  justify-content:space-between;
  padding:0 24px;
  position:sticky;
  top:0;
  z-index:40;
}
.topbar-title{font-family:'Syne',sans-serif;font-size:14px;font-weight:700;color:var(--text)}
.topbar-right{display:flex;align-items:center;gap:12px}
.credit-badge{
  font-size:11px;
  color:var(--text-3);
  font-style:italic;
}
.credit-badge strong{color:var(--purple-l);font-style:normal;font-weight:600}

/* CONTENT */
.content{flex:1;padding:24px;max-width:820px;width:100%}

/* PAGES */
.page{display:none;animation:fadeIn .25s ease}
.page.active{display:block}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}

/* PAGE HEADER */
.page-header{margin-bottom:24px}
.page-tag{
  display:inline-flex;
  align-items:center;
  gap:6px;
  font-size:10px;
  font-weight:700;
  letter-spacing:.12em;
  text-transform:uppercase;
  color:var(--purple-l);
  background:var(--purple-glow);
  border:1px solid var(--border-m);
  border-radius:99px;
  padding:3px 10px;
  margin-bottom:10px;
}
.page-title{font-family:'Syne',sans-serif;font-size:22px;font-weight:800;color:var(--text);line-height:1.2;margin-bottom:6px}
.page-desc{font-size:13px;color:var(--text-3);max-width:520px;line-height:1.6}

/* CARD */
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r2);padding:20px;margin-bottom:14px}
.card-title{font-family:'Syne',sans-serif;font-size:11px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--purple-l);margin-bottom:16px;display:flex;align-items:center;gap:8px}
.card-title::after{content:'';flex:1;height:1px;background:var(--border)}

/* FORM */
.field{margin-bottom:14px}
.field:last-child{margin-bottom:0}
label{display:block;font-size:12px;font-weight:500;color:var(--text-2);margin-bottom:5px}
label .hint{color:var(--text-3);font-weight:400;margin-left:4px}
input[type=text],input[type=number],textarea,select{
  width:100%;
  background:var(--bg3);
  border:1px solid var(--border);
  border-radius:var(--r);
  padding:9px 12px;
  color:var(--text);
  font-family:'DM Sans',sans-serif;
  font-size:13px;
  outline:none;
  transition:border-color .2s,background .2s;
  resize:vertical;
}
input::placeholder,textarea::placeholder{color:#3d3a4e}
input:focus,textarea:focus,select:focus{border-color:rgba(139,92,246,.5);background:#1c1929}
select option{background:var(--bg3)}
textarea{min-height:68px;line-height:1.6}

/* TYPE GRID */
.type-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.type-btn{
  background:var(--bg3);
  border:1px solid var(--border);
  border-radius:var(--r);
  padding:12px 8px;
  text-align:center;
  cursor:pointer;
  color:var(--text-3);
  font-size:12px;
  font-weight:500;
  transition:all .15s;
}
.type-btn .icon{font-size:20px;display:block;margin-bottom:5px}
.type-btn:hover{border-color:var(--border-m);color:var(--text)}
.type-btn.selected{border-color:var(--purple);background:var(--purple-glow);color:var(--purple-l)}

/* CHIPS */
.chip-group{display:flex;flex-wrap:wrap;gap:6px}
.chip{
  padding:4px 12px;
  border-radius:99px;
  border:1px solid var(--border);
  font-size:12px;
  color:var(--text-3);
  cursor:pointer;
  transition:all .15s;
  background:var(--bg3);
}
.chip:hover{color:var(--text);border-color:var(--border-m)}
.chip.selected{border-color:var(--purple);color:var(--purple-l);background:var(--purple-glow)}

/* STEPS PILLS */
.steps{display:flex;gap:6px;margin-bottom:20px;flex-wrap:wrap}
.step-pill{
  display:flex;align-items:center;gap:5px;
  font-size:11px;font-weight:500;
  color:var(--text-3);
  padding:4px 10px;
  border-radius:99px;
  border:1px solid var(--border);
  transition:all .2s;
}
.step-pill.active{color:var(--purple-l);border-color:var(--border-m);background:var(--purple-glow)}
.step-pill.done{color:var(--green);border-color:rgba(34,197,94,.3);background:rgba(34,197,94,.06)}
.step-pill .num{width:16px;height:16px;border-radius:50%;background:currentColor;color:var(--bg);display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:800}

/* BUTTONS */
.btn-row{display:flex;gap:8px;margin-top:20px;justify-content:flex-end}
.btn{padding:9px 20px;border-radius:var(--r);border:none;font-family:'DM Sans',sans-serif;font-size:13px;font-weight:600;cursor:pointer;transition:all .15s}
.btn-outline{background:transparent;border:1px solid var(--border);color:var(--text-3)}
.btn-outline:hover{border-color:var(--border-m);color:var(--text)}
.btn-primary{background:var(--purple);color:#fff}
.btn-primary:hover{background:var(--purple-d);transform:translateY(-1px);box-shadow:0 6px 20px rgba(139,92,246,.3)}

/* RESULT CARD */
.result-card{
  background:var(--surface);
  border:1px solid var(--border-m);
  border-radius:var(--r2);
  padding:20px;
  display:none;
  animation:fadeIn .35s ease;
}
.result-card.show{display:block}
.result-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;flex-wrap:wrap;gap:8px}
.result-title{font-family:'Syne',sans-serif;font-size:12px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--purple-l)}
.copy-btn{
  display:flex;align-items:center;gap:5px;
  padding:6px 14px;
  border-radius:var(--r);
  background:var(--purple);color:#fff;border:none;
  font-family:'DM Sans',sans-serif;font-size:12px;font-weight:700;
  cursor:pointer;transition:all .15s;
}
.copy-btn:hover{background:var(--purple-d);transform:translateY(-1px)}
.copy-btn.copied{background:var(--green)}
pre#prompt-output{
  background:var(--bg3);
  border:1px solid var(--border);
  border-radius:var(--r);
  padding:14px;
  font-size:12px;line-height:1.75;
  color:var(--text-2);
  white-space:pre-wrap;word-break:break-word;
  max-height:420px;overflow-y:auto;
  font-family:'DM Sans',sans-serif;
}
pre#prompt-output::-webkit-scrollbar{width:4px}
pre#prompt-output::-webkit-scrollbar-thumb{background:var(--bg4);border-radius:4px}
.reset-row{text-align:center;margin-top:12px}
.reset-btn{background:none;border:none;color:var(--text-3);font-size:12px;cursor:pointer;text-decoration:underline;font-family:'DM Sans',sans-serif}
.reset-btn:hover{color:var(--text)}

/* CS AREA */
.client-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:8px;margin-bottom:4px}
.cbtn{
  background:var(--bg3);border:1px solid var(--border);border-radius:var(--r);
  padding:9px 12px;font-size:12px;font-weight:500;color:var(--text-3);
  cursor:pointer;text-align:left;transition:all .15s;
}
.cbtn:hover{border-color:var(--border-m);color:var(--text)}
.cbtn.sel{border:1.5px solid var(--purple);background:var(--purple-glow);color:var(--purple-l)}

.tipo-row{display:flex;gap:8px;flex-wrap:wrap}
.tbtn{
  flex:1;min-width:130px;padding:9px 12px;font-size:12px;
  border:1px solid var(--border);border-radius:var(--r);
  background:var(--bg3);color:var(--text-3);cursor:pointer;
  text-align:center;transition:all .15s;position:relative;
}
.tbtn:hover{border-color:var(--border-m);color:var(--text)}
.tbtn.sel{border:1.5px solid var(--purple);background:var(--purple-glow);color:var(--purple-l)}
.tbtn.sel::after{content:'✓';position:absolute;top:4px;right:7px;font-size:9px;color:var(--purple-l)}

.section-block{background:var(--bg3);border:1px solid var(--border);border-radius:var(--r2);padding:16px;margin-bottom:10px}
.block-title{font-size:11px;font-weight:700;color:var(--purple-l);text-transform:uppercase;letter-spacing:.07em;margin-bottom:12px;padding-bottom:8px;border-bottom:1px solid var(--border)}
.nrow{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px}
.nrow label{display:block;font-size:11px;color:var(--text-3);margin-bottom:4px}
.context-blocks{display:flex;flex-direction:column;gap:10px}
.cs-result-card{background:var(--surface);border:1px solid var(--border-m);border-radius:var(--r2);padding:20px;display:none;animation:fadeIn .3s ease;margin-top:14px}
.cs-result-card.show{display:block}
.instructions-box{background:var(--purple-glow);border:1px solid var(--border-m);border-radius:var(--r);padding:12px 14px;margin-bottom:14px}
.instructions-box p{font-size:12px;color:var(--accent);line-height:1.7;margin-bottom:4px}
.instructions-box p:last-child{margin-bottom:0}
.open-btn{
  display:inline-block;margin-top:8px;
  padding:6px 14px;font-size:12px;font-weight:600;
  background:var(--purple);color:#fff;border:none;border-radius:var(--r);
  cursor:pointer;text-decoration:none;transition:background .15s;
}
.open-btn:hover{background:var(--purple-d)}
.prompt-box{
  font-size:12px;color:var(--text-2);line-height:1.7;
  white-space:pre-wrap;background:var(--bg3);border-radius:var(--r);
  padding:14px;font-family:'DM Sans',sans-serif;
  max-height:360px;overflow-y:auto;
}
.prompt-box::-webkit-scrollbar{width:4px}
.prompt-box::-webkit-scrollbar-thumb{background:var(--bg4);border-radius:4px}

/* PAINEL */
.pr-bar{height:5px;background:var(--border);border-radius:3px;margin-bottom:6px;overflow:hidden}
.pr-fill{height:100%;background:linear-gradient(90deg,var(--purple),var(--purple-l));border-radius:3px;transition:width .4s ease}
.pr-sub{font-size:12px;color:var(--text-3);margin-bottom:20px}
.plist{display:flex;flex-direction:column;gap:6px}
.pitem{
  display:flex;justify-content:space-between;align-items:center;
  padding:10px 14px;background:var(--bg3);border:1px solid var(--border);border-radius:var(--r);font-size:13px;
}
.piname{color:var(--text);font-weight:500}
.sdone{font-size:11px;color:var(--green);background:var(--green-bg);border:1px solid rgba(34,197,94,.2);padding:3px 10px;border-radius:99px}
.spend{font-size:11px;color:var(--amber);background:rgba(251,191,36,.08);border:1px solid rgba(251,191,36,.2);padding:3px 10px;border-radius:99px}

/* SOCIAL AREA */
.social-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r2);padding:20px;margin-bottom:14px}
.metric-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:8px}
.mc{background:var(--bg3);border:1px solid var(--border);border-radius:var(--r);padding:14px}
.mc-label{font-size:11px;color:var(--text-3);margin-bottom:6px}
.mc-value{font-size:24px;font-weight:700;font-family:'Syne',sans-serif;color:var(--text);letter-spacing:-.02em;margin-bottom:4px}
.mc-delta{font-size:11px}
.up{color:var(--green)}.down{color:var(--red)}.neutral{color:var(--text-3)}
.post-list{display:flex;flex-direction:column}
.post-item{display:flex;justify-content:space-between;align-items:center;padding:10px 0;border-bottom:1px solid var(--border)}
.post-item:last-child{border-bottom:none}
.post-thumb{width:32px;height:32px;border-radius:6px;background:var(--bg4);display:flex;align-items:center;justify-content:center;font-size:14px;flex-shrink:0}
.post-meta{display:flex;align-items:center;gap:8px}
.post-title-txt{font-size:12px;font-weight:500;color:var(--text);margin-bottom:1px}
.post-date{font-size:10px;color:var(--text-3)}
.post-stats{display:flex;gap:16px;flex-shrink:0}
.ps-val{font-size:13px;font-weight:600;color:var(--text);text-align:right}
.ps-lbl{font-size:10px;color:var(--text-3);text-align:right}
.ibox{border-radius:var(--r);padding:12px 14px;margin-bottom:8px}
.ibox.gr{background:rgba(34,197,94,.07);border:1px solid rgba(34,197,94,.2)}
.ibox.gr p{color:#86efac;font-size:12px;line-height:1.6}
.ibox.pu{background:var(--purple-glow);border:1px solid var(--border-m)}
.ibox.pu p{color:var(--purple-l);font-size:12px;line-height:1.6}

/* MANAGE */
.mgmt-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r2);padding:20px;margin-bottom:12px}
.mgmt-card h3{font-size:12px;font-weight:600;color:var(--text);margin-bottom:12px}
.add-row{display:flex;gap:8px}
.add-row input{flex:1}
.add-btn{padding:9px 16px;font-size:12px;font-weight:600;background:var(--purple);border:none;border-radius:var(--r);color:#fff;cursor:pointer;white-space:nowrap;transition:background .15s}
.add-btn:hover{background:var(--purple-d)}
.cm-list{display:flex;flex-direction:column;gap:6px;margin-top:10px}
.cm-item{display:flex;justify-content:space-between;align-items:center;padding:9px 12px;background:var(--bg3);border-radius:var(--r);font-size:12px}
.cm-name{color:var(--text);font-weight:500}
.rm-btn{font-size:10px;padding:3px 9px;border-radius:99px;background:var(--red-bg);color:var(--red);border:1px solid rgba(248,113,113,.2);cursor:pointer}
.rm-btn:hover{opacity:.75}
.empty-state{font-size:12px;color:var(--text-3);text-align:center;padding:16px}

/* SOCIAL TABS */
.stabs{display:flex;gap:6px;margin-bottom:20px}
.stab{padding:7px 14px;font-size:12px;color:var(--text-3);cursor:pointer;border-bottom:2px solid transparent;transition:all .15s}
.stab:hover{color:var(--text)}
.stab.active{color:var(--purple-l);border-bottom-color:var(--purple);font-weight:500}
.spane{display:none}.spane.active{display:block}

/* SLABEL */
.slabel{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.1em;color:var(--text-3);margin:16px 0 8px}

/* PERIOD BADGE */
.period-badge{font-size:11px;color:var(--text-2);background:var(--bg3);border:1px solid var(--border);border-radius:var(--r);padding:5px 12px}
.report-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:20px;flex-wrap:wrap;gap:10px}
.client-name-h{font-family:'Syne',sans-serif;font-size:22px;font-weight:800;color:var(--text);letter-spacing:-.02em}
.client-sub-h{font-size:12px;color:var(--text-3);margin-top:3px}
.edit-toggle{font-size:11px;padding:5px 12px;border-radius:var(--r);border:1px solid var(--border-m);background:transparent;color:var(--purple-l);cursor:pointer;transition:all .15s}
.edit-toggle:hover{background:var(--purple-glow)}
.edit-toggle.on{background:var(--purple);border-color:var(--purple);color:#fff}
.client-sel-bar{display:flex;align-items:center;gap:10px;margin-bottom:16px;flex-wrap:wrap}
.client-sel-bar label{font-size:11px;color:var(--text-3)}
.client-sel-bar select{background:var(--bg3);border:1px solid var(--border);border-radius:var(--r);padding:6px 10px;font-size:12px;color:var(--text);outline:none;font-family:inherit}
.client-sel-bar select:focus{border-color:var(--purple-l)}
.edit-panel{display:none}
.esec{background:var(--bg3);border:1px solid var(--border);border-radius:var(--r2);padding:16px;margin-bottom:10px}
.esec h3{font-size:10px;font-weight:700;color:var(--purple-l);text-transform:uppercase;letter-spacing:.07em;margin-bottom:12px;padding-bottom:8px;border-bottom:1px solid var(--border)}
.egrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(170px,1fr));gap:8px;margin-bottom:4px}
.ef label{display:block;font-size:11px;color:var(--text-3);margin-bottom:4px}
.prev-section{background:rgba(139,92,246,.06);border:1px solid var(--border-m);border-radius:var(--r);padding:12px;margin-top:10px}
.prev-section-title{font-size:10px;color:var(--purple-l);font-weight:700;margin-bottom:8px;text-transform:uppercase;letter-spacing:.05em}
.prev-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:8px}
.first-period-note{background:rgba(34,197,94,.07);border:1px solid rgba(34,197,94,.2);border-radius:var(--r);padding:8px 12px;margin-top:8px}
.first-period-note p{font-size:11px;color:#86efac}
.peb{background:var(--bg4);border-radius:var(--r);padding:10px;margin-bottom:8px}
.peb-num{font-size:10px;color:var(--purple-l);font-weight:700;margin-bottom:8px}
.peg{display:grid;grid-template-columns:2fr 1fr 1fr 1fr 1fr;gap:7px}
.save-btn{width:100%;padding:11px;font-size:13px;font-weight:700;background:var(--purple);border:none;border-radius:var(--r);color:#fff;cursor:pointer;transition:background .15s;margin-top:8px}
.save-btn:hover{background:var(--purple-d)}
.save-btn.saved{background:rgba(34,197,94,.7)}
.checkbox-row{display:flex;align-items:center;gap:7px;margin-bottom:12px}
.checkbox-row input{width:14px;height:14px;accent-color:var(--purple);cursor:pointer}
.checkbox-row label{font-size:12px;color:var(--text-2);cursor:pointer}
.empty-report{text-align:center;padding:40px 20px;color:var(--text-3);font-size:13px;line-height:1.8}

/* MOBILE HAMBURGER */
.hamburger{display:none;background:none;border:none;cursor:pointer;padding:4px;color:var(--text-2)}
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:49}

@media(max-width:700px){
  .sidebar{transform:translateX(-100%)}
  .sidebar.open{transform:translateX(0)}
  .main{margin-left:0}
  .hamburger{display:flex}
  .overlay.show{display:block}
  .type-grid{grid-template-columns:1fr 1fr}
  .nrow{grid-template-columns:1fr 1fr}
  .peg{grid-template-columns:1fr 1fr}
  .btn-row{flex-direction:column-reverse}
  .btn{width:100%;text-align:center}
}
</style>
</head>
<body>
<div class="overlay" id="overlay" onclick="closeSidebar()"></div>
<div class="app">

<!-- SIDEBAR -->
<nav class="sidebar" id="sidebar">
  <div class="sidebar-logo">
    <img src="data:image/png;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/4gHYSUNDX1BST0ZJTEUAAQEAAAHIAAAAAAQwAABtbnRyUkdCIFhZWiAH4AABAAEAAAAAAABhY3NwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAA9tYAAQAAAADTLQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAlkZXNjAAAA8AAAACRyWFlaAAABFAAAABRnWFlaAAABKAAAABRiWFlaAAABPAAAABR3dHB0AAABUAAAABRyVFJDAAABZAAAAChnVFJDAAABZAAAAChiVFJDAAABZAAAAChjcHJ0AAABjAAAADxtbHVjAAAAAAAAAAEAAAAMZW5VUwAAAAgAAAAcAHMAUgBHAEJYWVogAAAAAAAAb6IAADj1AAADkFhZWiAAAAAAAABimQAAt4UAABjaWFlaIAAAAAAAACSgAAAPhAAAts9YWVogAAAAAAAA9tYAAQAAAADTLXBhcmEAAAAAAAQAAAACZmYAAPKnAAANWQAAE9AAAApbAAAAAAAAAABtbHVjAAAAAAAAAAEAAAAMZW5VUwAAACAAAAAcAEcAbwBvAGcAbABlACAASQBuAGMALgAgADIAMAAxADb/2wBDAAUDBAQEAwUEBAQFBQUGBwwIBwcHBw8LCwkMEQ8SEhEPERETFhwXExQaFRERGCEYGh0dHx8fExciJCIeJBweHx7/2wBDAQUFBQcGBw4ICA4eFBEUHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh7/wAARCAfQB9ADASIAAhEBAxEB/8QAHAABAAIDAQEBAAAAAAAAAAAAAAYHBAUIAwIB/8QAWRABAAEDAgICCgwLBwEGBAcBAAECAwQFEQYHEjETIUFRYXGBobGyFBciMjZUcnORlMHRFTNCUlZ0kpPC0uIjQ1NVYqKzgiRFY4Ph8AgWJmQlNDVEhKPxRv/EABwBAQACAwEBAQAAAAAAAAAAAAAEBQIDBgcBCP/EAEARAQABAgMDBwkGBwEBAAMBAAABAgMEBREGITESQVFxgZHRExQyMzVhobHBFiJSU3LhFSNCQ5Ki8GKCJdLi8f/aAAwDAQACEQMRAD8A4yAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/2Q==" alt="Seta Lab"/>
    <div>
      <div class="sidebar-logo-text">Seta Lab</div>
      <div class="sidebar-logo-sub">Hub de Ferramentas</div>
    </div>
  </div>

  <div class="sidebar-section-label">Ferramentas</div>

  <div class="nav-item active" id="nav-copy" onclick="switchPage('copy')">
    <svg class="nav-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 20h9M16.5 3.5a2.121 2.121 0 013 3L7 19l-4 1 1-4 12.5-12.5z"/></svg>
    Criação de Copy
  </div>

  <div class="nav-item" id="nav-cs" onclick="switchPage('cs')">
    <svg class="nav-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
    Área do CS
  </div>

  <div class="nav-item" id="nav-social" onclick="switchPage('social')">
    <svg class="nav-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg>
    Social Media
  </div>

  <div class="sidebar-section-label" style="margin-top:16px">Configurações</div>

  <div class="nav-item" id="nav-clientes" onclick="switchPage('clientes')">
    <svg class="nav-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 00-3-3.87M16 3.13a4 4 0 010 7.75"/></svg>
    Clientes
  </div>

  <div class="sidebar-footer">
    <div class="credit">Criado por<br><strong>Daniel Markel</strong></div>
  </div>
</nav>

<!-- MAIN -->
<div class="main">
  <div class="topbar">
    <div style="display:flex;align-items:center;gap:12px">
      <button class="hamburger" onclick="openSidebar()">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="3" y1="6" x2="21" y2="6"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="3" y1="18" x2="21" y2="18"/></svg>
      </button>
      <div class="topbar-title" id="topbar-title">Criação de Copy</div>
    </div>
    <div class="topbar-right">
      <div class="credit-badge">por <strong>Daniel Markel</strong></div>
    </div>
  </div>

  <div class="content">

    <!-- ==================== PAGE: COPY ==================== -->
    <div class="page active" id="page-copy">
      <div class="page-header">
        <div class="page-tag">✍️ Copy</div>
        <div class="page-title">Gerador de Copy</div>
        <div class="page-desc">Preencha o briefing e receba um prompt pronto para colar no ChatGPT ou Claude.</div>
      </div>

      <div class="steps">
        <div class="step-pill active" id="cpill-1"><span class="num">1</span> Tipo</div>
        <div class="step-pill" id="cpill-2"><span class="num">2</span> Restaurante</div>
        <div class="step-pill" id="cpill-3"><span class="num">3</span> Produto</div>
        <div class="step-pill" id="cpill-4"><span class="num">4</span> Público</div>
      </div>

      <!-- Step 1 -->
      <div class="card" id="cstep-1">
        <div class="card-title">Tipo de criativo</div>
        <div class="type-grid">
          <div class="type-btn" data-val="video" onclick="selectType(this)"><span class="icon">🎬</span>Vídeo</div>
          <div class="type-btn" data-val="estatico" onclick="selectType(this)"><span class="icon">🖼️</span>Estático</div>
          <div class="type-btn" data-val="ambos" onclick="selectType(this)"><span class="icon">✨</span>Os dois</div>
        </div>
        <div class="btn-row"><button class="btn btn-primary" onclick="cGoTo(2)">Próximo →</button></div>
      </div>

      <!-- Step 2 -->
      <div class="card" id="cstep-2" style="display:none">
        <div class="card-title">Sobre o restaurante</div>
        <div class="field"><label>Nome do restaurante <span class="hint">*</span></label><input type="text" id="cnome" placeholder="Ex: Lanche dos Guri"/></div>
        <div class="field"><label>Cidade e estado <span class="hint">*</span></label><input type="text" id="ccidade" placeholder="Ex: Palhoça - SC"/></div>
        <div class="field"><label>Contexto local ou cultural <span class="hint">opcional</span></label><textarea id="clocal" rows="2" placeholder="Ex: time de futebol local, gíria da cidade, clima..."></textarea></div>
        <div class="btn-row">
          <button class="btn btn-outline" onclick="cGoTo(1)">← Voltar</button>
          <button class="btn btn-primary" onclick="cGoTo(3)">Próximo →</button>
        </div>
      </div>

      <!-- Step 3 -->
      <div class="card" id="cstep-3" style="display:none">
        <div class="card-title">Produto & oferta</div>
        <div class="field"><label>Produto ou prato <span class="hint">*</span></label><input type="text" id="cproduto" placeholder="Ex: Banheirinha de Cheddar"/></div>
        <div class="field"><label>Descrição do produto <span class="hint">recomendado</span></label><textarea id="cdesc" rows="3" placeholder="Cole a descrição completa do produto..."></textarea></div>
        <div class="field"><label>Promoção ou diferencial <span class="hint">opcional</span></label><textarea id="cpromo" rows="2" placeholder="Ex: A partir de R$ 73,99, serve mais de 4 pessoas..."></textarea></div>
        <div class="field"><label>Objetivo do criativo</label>
          <select id="cobj">
            <option value="gerar pedidos">Gerar pedidos / vendas</option>
            <option value="divulgar lançamento">Divulgar lançamento</option>
            <option value="promoção relâmpago">Promoção relâmpago</option>
            <option value="reforçar a marca">Reforçar a marca</option>
          </select>
        </div>
        <div class="btn-row">
          <button class="btn btn-outline" onclick="cGoTo(2)">← Voltar</button>
          <button class="btn btn-primary" onclick="cGoTo(4)">Próximo →</button>
        </div>
      </div>

      <!-- Step 4 -->
      <div class="card" id="cstep-4" style="display:none">
        <div class="card-title">Público & tom</div>
        <div class="field"><label>Público-alvo <span class="hint">*</span></label><input type="text" id="cpublico" placeholder="Ex: jovens, famílias, trabalhadores da região..."/></div>
        <div class="field"><label>Tom de linguagem</label>
          <div class="chip-group" id="cton-chips">
            <div class="chip" onclick="selectChip(this)">Descontraído</div>
            <div class="chip" onclick="selectChip(this)">Irônico</div>
            <div class="chip" onclick="selectChip(this)">Popular</div>
            <div class="chip" onclick="selectChip(this)">Premium</div>
            <div class="chip" onclick="selectChip(this)">Urgente</div>
            <div class="chip" onclick="selectChip(this)">Emotivo</div>
            <div class="chip" onclick="selectChip(this)">Divertido</div>
          </div>
        </div>
        <div class="field" style="margin-top:8px"><label>Outro tom <span class="hint">opcional</span></label><input type="text" id="ctom-custom" placeholder="Ex: linguagem de boteco, estilo jovem..."/></div>
        <div class="btn-row">
          <button class="btn btn-outline" onclick="cGoTo(3)">← Voltar</button>
          <button class="btn btn-primary" onclick="generateCopy()">⚡ Gerar prompt</button>
        </div>
      </div>

      <!-- Result -->
      <div class="result-card" id="copy-result">
        <div class="result-header">
          <div class="result-title">✅ Prompt gerado</div>
          <button class="copy-btn" id="copyBtnCopy" onclick="copyText('prompt-output','copyBtnCopy')">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1"/></svg>
            Copiar
          </button>
        </div>
        <pre id="prompt-output"></pre>
        <div class="reset-row"><button class="reset-btn" onclick="resetCopy()">↩ Novo prompt</button></div>
      </div>
    </div>

    <!-- ==================== PAGE: CS ==================== -->
    <div class="page" id="page-cs">
      <div class="page-header">
        <div class="page-tag">💬 CS</div>
        <div class="page-title">Central do CS</div>
        <div class="page-desc">Gere mensagens de WhatsApp personalizadas para cada cliente com contexto real.</div>
      </div>

      <div class="slabel">1. Selecione o cliente</div>
      <div class="client-grid" id="cs-cgrid"></div>

      <div class="slabel" style="margin-top:16px">2. Áreas de melhoria</div>
      <div class="tipo-row">
        <div class="tbtn" id="cs-t-trafego" onclick="csToggleTipo('trafego')">Tráfego pago</div>
        <div class="tbtn" id="cs-t-social" onclick="csToggleTipo('social')">Social media</div>
        <div class="tbtn" id="cs-t-cardapio" onclick="csToggleTipo('cardapio')">Cardápio / operação</div>
      </div>

      <div class="slabel" style="margin-top:16px">3. Contexto</div>
      <div class="context-blocks" id="cs-context-blocks"></div>

      <button class="btn btn-primary" style="width:100%;margin-top:4px" onclick="csGerar()">⚡ Gerar prompt para o Claude</button>

      <div class="cs-result-card" id="cs-result">
        <div class="instructions-box">
          <p><strong>Prompt gerado!</strong> Siga os passos:</p>
          <p>1. Clique em "Copiar prompt" &nbsp;2. Abra o Claude.ai &nbsp;3. Cole e envie &nbsp;4. Copie a mensagem e envie ao cliente</p>
          <a class="open-btn" href="https://claude.ai" target="_blank">Abrir Claude.ai</a>
        </div>
        <div class="result-header" style="margin-top:12px">
          <div class="result-title" id="cs-result-title">Prompt gerado</div>
          <button class="copy-btn" id="cs-copy-btn" onclick="copyText('cs-prompt-text','cs-copy-btn')">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1"/></svg>
            Copiar
          </button>
        </div>
        <div class="prompt-box" id="cs-prompt-text"></div>
      </div>

      <!-- Painel -->
      <div style="margin-top:28px">
        <div class="slabel">Progresso de hoje</div>
        <div class="pr-bar"><div class="pr-fill" id="cs-prfill" style="width:0%"></div></div>
        <div class="pr-sub" id="cs-prsub">0 de 0 clientes contatados</div>
        <div class="plist" id="cs-plist"></div>
      </div>
    </div>

    <!-- ==================== PAGE: SOCIAL ==================== -->
    <div class="page" id="page-social">
      <div class="page-header">
        <div class="page-tag">📊 Social</div>
        <div class="page-title">Relatórios Social Media</div>
        <div class="page-desc">Preencha e visualize relatórios mensais e quinzenais para cada cliente.</div>
      </div>

      <div class="stabs">
        <div class="stab active" id="stab-mensal" onclick="switchSocialTab('mensal')">Mensal</div>
        <div class="stab" id="stab-quinzenal" onclick="switchSocialTab('quinzenal')">Quinzenal</div>
      </div>

      <!-- Mensal -->
      <div class="spane active" id="spane-mensal">
        <div class="client-sel-bar">
          <label>Cliente:</label>
          <select id="sel-mensal" onchange="renderMensal()"></select>
          <button class="edit-toggle" id="editToggleM" onclick="toggleEditM()">Editar</button>
        </div>
        <div id="view-mensal"></div>
        <div class="edit-panel" id="edit-mensal">
          <div class="esec">
            <h3>Identificação</h3>
            <div class="egrid"><div class="ef"><label>Período</label><input type="text" id="ePerM" placeholder="Abril 2025"></div></div>
            <div class="checkbox-row"><input type="checkbox" id="ePrimMes"><label for="ePrimMes">Primeiro mês — não comparar com anterior</label></div>
          </div>
          <div class="esec">
            <h3>Métricas atuais</h3>
            <div class="egrid">
              <div class="ef"><label>Alcance total</label><input type="text" id="eAlcM" placeholder="48.2k"></div>
              <div class="ef"><label>Impressões</label><input type="text" id="eImpM" placeholder="112k"></div>
              <div class="ef"><label>Novos seguidores</label><input type="text" id="eSegM" placeholder="+342"></div>
              <div class="ef"><label>Taxa de engajamento</label><input type="text" id="eEngM" placeholder="4,7%"></div>
              <div class="ef"><label>Publicações</label><input type="text" id="ePubM" placeholder="18"></div>
              <div class="ef"><label>Cliques no perfil</label><input type="text" id="eCliM" placeholder="1.240"></div>
            </div>
            <div class="prev-section" id="prevSecM">
              <div class="prev-section-title">Mês anterior</div>
              <div class="prev-grid">
                <div class="ef"><label>Alcance ant.</label><input type="text" id="ePAlcM" placeholder="40k"></div>
                <div class="ef"><label>Impressões ant.</label><input type="text" id="ePImpM" placeholder="100k"></div>
                <div class="ef"><label>Seguidores ant.</label><input type="text" id="ePSegM" placeholder="+275"></div>
                <div class="ef"><label>Engajamento ant.</label><input type="text" id="ePEngM" placeholder="4,1%"></div>
                <div class="ef"><label>Cliques ant.</label><input type="text" id="ePCliM" placeholder="1.130"></div>
              </div>
            </div>
            <div class="first-period-note" id="firstNoteM" style="display:none"><p>Primeiro período — variações não serão exibidas.</p></div>
          </div>
          <div class="esec"><h3>Top 3 publicações</h3><div id="ePostsM"></div></div>
          <div class="esec">
            <h3>Análise</h3>
            <div style="display:flex;flex-direction:column;gap:10px">
              <div class="ef"><label>O que funcionou</label><textarea id="eDestM" placeholder="Ex: Os Reels com bastidores geraram 52% do engajamento..."></textarea></div>
              <div class="ef"><label>Foco para o próximo mês</label><textarea id="eProxM" placeholder="Ex: Aumentar frequência de Reels para 3x por semana..."></textarea></div>
            </div>
          </div>
          <button class="save-btn" id="saveM" onclick="saveMensal()">Salvar relatório mensal</button>
        </div>
      </div>

      <!-- Quinzenal -->
      <div class="spane" id="spane-quinzenal">
        <div class="client-sel-bar">
          <label>Cliente:</label>
          <select id="sel-quinzenal" onchange="renderQuinzenal()"></select>
          <button class="edit-toggle" id="editToggleQ" onclick="toggleEditQ()">Editar</button>
        </div>
        <div id="view-quinzenal"></div>
        <div class="edit-panel" id="edit-quinzenal">
          <div class="esec">
            <h3>Identificação</h3>
            <div class="egrid"><div class="ef"><label>Período</label><input type="text" id="ePerQ" placeholder="1–15 Abril 2025"></div></div>
            <div class="checkbox-row"><input type="checkbox" id="ePrimQ"><label for="ePrimQ">Primeira quinzena — não comparar com anterior</label></div>
          </div>
          <div class="esec">
            <h3>Métricas atuais</h3>
            <div class="egrid">
              <div class="ef"><label>Alcance</label><input type="text" id="eAlcQ" placeholder="22k"></div>
              <div class="ef"><label>Impressões</label><input type="text" id="eImpQ" placeholder="54k"></div>
              <div class="ef"><label>Novos seguidores</label><input type="text" id="eSegQ" placeholder="+156"></div>
              <div class="ef"><label>Taxa de engajamento</label><input type="text" id="eEngQ" placeholder="4,5%"></div>
              <div class="ef"><label>Publicações</label><input type="text" id="ePubQ" placeholder="9"></div>
              <div class="ef"><label>Cliques no perfil</label><input type="text" id="eCliQ" placeholder="580"></div>
            </div>
            <div class="prev-section" id="prevSecQ">
              <div class="prev-section-title">Quinzena anterior</div>
              <div class="prev-grid">
                <div class="ef"><label>Alcance ant.</label><input type="text" id="ePAlcQ" placeholder="19k"></div>
                <div class="ef"><label>Impressões ant.</label><input type="text" id="ePImpQ" placeholder="48k"></div>
                <div class="ef"><label>Seguidores ant.</label><input type="text" id="ePSegQ" placeholder="+130"></div>
                <div class="ef"><label>Engajamento ant.</label><input type="text" id="ePEngQ" placeholder="4,1%"></div>
                <div class="ef"><label>Cliques ant.</label><input type="text" id="ePCliQ" placeholder="510"></div>
              </div>
            </div>
            <div class="first-period-note" id="firstNoteQ" style="display:none"><p>Primeira quinzena — variações não serão exibidas.</p></div>
          </div>
          <div class="esec">
            <h3>Análise</h3>
            <div style="display:flex;flex-direction:column;gap:10px">
              <div class="ef"><label>Destaque da quinzena</label><textarea id="eDestQ" placeholder="Ex: O Reel do novo prato atingiu 8.200 visualizações..."></textarea></div>
              <div class="ef"><label>Próximo passo</label><textarea id="eProxQ" placeholder="Ex: Vamos testar novo criativo focado no combo duplo..."></textarea></div>
            </div>
          </div>
          <button class="save-btn" id="saveQ" onclick="saveQuinzenal()">Salvar relatório quinzenal</button>
        </div>
      </div>
    </div>

    <!-- ==================== PAGE: CLIENTES ==================== -->
    <div class="page" id="page-clientes">
      <div class="page-header">
        <div class="page-tag">👥 Clientes</div>
        <div class="page-title">Gestão de Clientes</div>
        <div class="page-desc">Adicione ou remova clientes da lista compartilhada entre todas as ferramentas.</div>
      </div>
      <div class="mgmt-card">
        <h3>Adicionar cliente</h3>
        <div class="add-row">
          <input type="text" id="iNewClient" placeholder="Nome do restaurante">
          <button class="add-btn" onclick="addClient()">Adicionar</button>
        </div>
      </div>
      <div class="mgmt-card">
        <h3>Clientes ativos</h3>
        <div class="cm-list" id="cmList"></div>
      </div>
    </div>

  </div><!-- /content -->
</div><!-- /main -->
</div><!-- /app -->

<script>
// ===================== STATE =====================
var DEFAULT_CLIENTS=['Divino Mineiro','Hebrom','Lanche dos Guri','Fogo no Disco','Pizzaria Campeã','Cafezinho','Imperial / Atillio','Forno Napoletano','El Patron','Hamburgueria Goiana','Johnys','Parmegiamo','Quentinhas','Restaurante Grill','Varanda Beer','Costelito'];
var clients=JSON.parse(localStorage.getItem('sl_clients')||'null')||DEFAULT_CLIENTS.slice();

function saveClients(){localStorage.setItem('sl_clients',JSON.stringify(clients));}
function storeKey(t,c){return 'sl_'+t+'_'+encodeURIComponent(c);}
function saveData(t,c,d){try{localStorage.setItem(storeKey(t,c),JSON.stringify(d));}catch(e){}}
function loadData(t,c){try{var d=localStorage.getItem(storeKey(t,c));return d?JSON.parse(d):null;}catch(e){return null;}}
function gv(id){var el=document.getElementById(id);return el?el.value.trim():'';}
function sv(id,v){var el=document.getElementById(id);if(el)el.value=v||'';}
function gc(id){var el=document.getElementById(id);return el?el.checked:false;}
function sc(id,v){var el=document.getElementById(id);if(el)el.checked=!!v;}

// ===================== SIDEBAR =====================
var currentPage='copy';
var pageTitles={copy:'Criação de Copy',cs:'Área do CS',social:'Social Media',clientes:'Clientes'};

function switchPage(p){
  currentPage=p;
  document.querySelectorAll('.nav-item').forEach(function(el){el.classList.remove('active');});
  document.getElementById('nav-'+p).classList.add('active');
  document.querySelectorAll('.page').forEach(function(el){el.classList.remove('active');});
  document.getElementById('page-'+p).classList.add('active');
  document.getElementById('topbar-title').textContent=pageTitles[p];
  if(p==='cs'){renderCSGrid();renderCSPainel();}
  if(p==='social'){populateSocialSelects();renderMensal();renderQuinzenal();}
  if(p==='clientes'){renderManage();}
  closeSidebar();
}

function openSidebar(){document.getElementById('sidebar').classList.add('open');document.getElementById('overlay').classList.add('show');}
function closeSidebar(){document.getElementById('sidebar').classList.remove('open');document.getElementById('overlay').classList.remove('show');}

// ===================== COPY PAGE =====================
var cSelectedType='',cSelectedTon='';

function selectType(el){
  document.querySelectorAll('.type-btn').forEach(function(b){b.classList.remove('selected');});
  el.classList.add('selected');cSelectedType=el.dataset.val;
}
function selectChip(el){
  el.classList.toggle('selected');
  cSelectedTon=[...document.querySelectorAll('#cton-chips .chip.selected')].map(c=>c.textContent).join(', ');
}

function cGoTo(step){
  if(step===2&&!cSelectedType){alert('Selecione o tipo de criativo.');return;}
  if(step===3&&(!gv('cnome')||!gv('ccidade'))){alert('Preencha nome e cidade.');return;}
  if(step===4&&!gv('cproduto')){alert('Informe o produto.');return;}
  for(var i=1;i<=4;i++){
    var card=document.getElementById('cstep-'+i);
    if(card)card.style.display=(i===step)?'block':'none';
    var pill=document.getElementById('cpill-'+i);
    if(pill){
      pill.classList.remove('active','done');
      if(i<step)pill.classList.add('done');
      if(i===step)pill.classList.add('active');
    }
  }
  window.scrollTo({top:0,behavior:'smooth'});
}

function generateCopy(){
  if(!gv('cpublico')){alert('Informe o público-alvo.');return;}
  var nome=gv('cnome'),cidade=gv('ccidade'),local=gv('clocal');
  var produto=gv('cproduto'),desc=gv('cdesc'),promo=gv('cpromo'),obj=gv('cobj');
  var publico=gv('cpublico'),tomCustom=gv('ctom-custom');
  var tom=[cSelectedTon,tomCustom].filter(Boolean).join(' + ')||'Descontraído';
  var tipoLabel={video:'criativo em vídeo',estatico:'criativo estático',ambos:'criativo em vídeo E criativo estático'}[cSelectedType]||'criativo';
  var instrucoes='';
  if(cSelectedType==='video'||cSelectedType==='ambos'){
    instrucoes+=`\n\n## CRIATIVO EM VÍDEO\nCrie copy completa com 3 partes:\n\n**1. GANCHO (3–5s)** — Uma frase curta e impactante que pare o scroll. Conexão local/emocional. NÃO use clichês.\n\n**2. DESENVOLVIMENTO** — Máx. 2–3 frases. Apresenta o produto e destaca o diferencial.\n\n**3. CTA** — Use exatamente: "Clique em 'Pedir agora' e [receba/experimente/garanta] [produto] na porta da sua casa."\n\nEntregue as 3 partes separadas e numeradas. Após entregar, pergunte se o usuário quer ajustar alguma parte.`;
  }
  if(cSelectedType==='estatico'||cSelectedType==='ambos'){
    instrucoes+=`\n\n## CRIATIVO ESTÁTICO\nCrie hierarquia de textos para imagem (feed/stories):\n\n1. **HEADLINE** — Frase principal de maior destaque\n2. **SUBHEADLINE** — Complemento ou detalhe da oferta\n3. **TEXTO DE APOIO** — Preço, prazo, condições (se houver)\n4. **CTA VISUAL** — Botão ou chamada de ação\n5. **ORIENTAÇÕES PARA O DESIGNER** — Posicionamento do produto, como destacar a promoção, hierarquia visual`;
  }
  var prompt=`Você é um especialista em copywriting para tráfego pago de restaurantes. Crie ${tipoLabel} com base nas informações abaixo.\n\n---\nRESTAURANTE: ${nome}\nCIDADE / ESTADO: ${cidade}${local?'\nCONTEXTO LOCAL: '+local:''}\nPRODUTO: ${produto}${desc?'\nDESCRIÇÃO: '+desc:''}${promo?'\nPROMOÇÃO / DIFERENCIAL: '+promo:''}\nOBJETIVO: ${obj}\nPÚBLICO-ALVO: ${publico}\nTOM: ${tom}\n---${instrucoes}\n\nREGRAS:\n- Nunca use clichês como "venha nos visitar" ou "qualidade incomparável"\n- Adapte o tom ao perfil do restaurante e público\n- Entregue copies prontas para uso, sem rascunho\n- Após entregar, pergunte se quer ajustes`;

  document.querySelectorAll('.card[id^=cstep-]').forEach(function(c){c.style.display='none';});
  document.querySelectorAll('.step-pill').forEach(function(p){p.classList.remove('active');p.classList.add('done');});
  document.getElementById('prompt-output').textContent=prompt;
  var rc=document.getElementById('copy-result');rc.classList.add('show');
  rc.scrollIntoView({behavior:'smooth',block:'start'});
}

function resetCopy(){
  cSelectedType='';cSelectedTon='';
  document.querySelectorAll('.type-btn').forEach(function(b){b.classList.remove('selected');});
  document.querySelectorAll('.chip').forEach(function(c){c.classList.remove('selected');});
  ['cnome','ccidade','clocal','cproduto','cdesc','cpromo','cpublico','ctom-custom'].forEach(function(id){sv(id,'');});
  document.getElementById('cobj').selectedIndex=0;
  document.getElementById('copy-result').classList.remove('show');
  document.querySelectorAll('.step-pill').forEach(function(p,i){p.classList.remove('active','done');if(i===0)p.classList.add('active');});
  cGoTo(1);
}

// ===================== CS PAGE =====================
var csSelClient=null,csSelTipos=[],csDone={};
var CS_TIPOS={
  trafego:{label:'Tráfego pago',fields:[
    {id:'cs-trafego-acao',label:'O que foi feito no tráfego?',type:'textarea',ph:'Ex: ajustamos o criativo principal, nova campanha de conversão...'},
    {id:'cs-trafego-resultado',label:'Resultado gerado',type:'textarea',ph:'Ex: ROAS subiu, mais pedidos via delivery...'},
    {id:'cs-trafego-inv',label:'Investido (R$)',type:'number',ph:'168'},
    {id:'cs-trafego-ret',label:'Retorno (R$)',type:'number',ph:'688'},
    {id:'cs-trafego-meta',label:'Meta (R$)',type:'number',ph:'1750'}
  ]},
  social:{label:'Social media',fields:[
    {id:'cs-social-acao',label:'O que foi feito no social?',type:'textarea',ph:'Ex: publicamos 3 reels de bastidores...'},
    {id:'cs-social-resultado',label:'Resultado gerado',type:'textarea',ph:'Ex: alcance aumentou 18%, 87 novos seguidores...'}
  ]},
  cardapio:{label:'Cardápio / operação',fields:[
    {id:'cs-cardapio-acao',label:'O que foi feito?',type:'textarea',ph:'Ex: criamos o monte seu combinho, ajustamos margem...'},
    {id:'cs-cardapio-resultado',label:'Resultado gerado',type:'textarea',ph:'Ex: ticket médio subiu, menos desperdício...'}
  ]}
};

function renderCSGrid(){
  var g=document.getElementById('cs-cgrid');g.innerHTML='';
  if(clients.length===0){g.innerHTML='<div class="empty-state">Nenhum cliente. Adicione na aba Clientes.</div>';return;}
  clients.forEach(function(c){
    var d=document.createElement('div');
    d.className='cbtn'+(csSelClient===c?' sel':'');
    d.textContent=c;
    d.onclick=function(){csSelClient=c;renderCSGrid();renderCSPainel();};
    g.appendChild(d);
  });
}

function csToggleTipo(t){
  var idx=csSelTipos.indexOf(t);
  if(idx>-1)csSelTipos.splice(idx,1);else csSelTipos.push(t);
  document.getElementById('cs-t-'+t).classList.toggle('sel',csSelTipos.indexOf(t)>-1);
  renderCSContext();
}

function renderCSContext(){
  var container=document.getElementById('cs-context-blocks');
  var order=['trafego','social','cardapio'];
  var active=order.filter(function(t){return csSelTipos.indexOf(t)>-1;});
  if(active.length===0){container.innerHTML='';return;}
  var existing={};
  container.querySelectorAll('.section-block[data-tipo]').forEach(function(el){existing[el.dataset.tipo]=el;});
  container.innerHTML='';
  active.forEach(function(t){
    if(existing[t]){container.appendChild(existing[t]);return;}
    var cfg=CS_TIPOS[t];
    var block=document.createElement('div');
    block.className='section-block';block.dataset.tipo=t;
    var html='<div class="block-title">'+cfg.label+'</div>';
    var numF=cfg.fields.filter(function(f){return f.type==='number';});
    var txtF=cfg.fields.filter(function(f){return f.type==='textarea';});
    txtF.forEach(function(f){html+='<div class="field"><label>'+f.label+'</label><textarea id="'+f.id+'" placeholder="'+f.ph+'"></textarea></div>';});
    if(numF.length>0){
      html+='<div class="field"><label>Dados (opcional)</label><div class="nrow">';
      numF.forEach(function(f){html+='<div><label>'+f.label+'</label><input type="number" id="'+f.id+'" placeholder="'+f.ph+'"></div>';});
      html+='</div></div>';
    }
    block.innerHTML=html;container.appendChild(block);
  });
  var pb=document.getElementById('cs-prox-block');
  if(!pb){
    pb=document.createElement('div');pb.className='section-block';pb.id='cs-prox-block';
    pb.innerHTML='<div class="field" style="margin:0"><label>Próximo passo <span class="hint">opcional</span></label><input type="text" id="cs-proximo" placeholder="Ex: vamos testar novo criativo focado no combo duplo"></div>';
  }
  container.appendChild(pb);
}

function csGerar(){
  if(!csSelClient){alert('Selecione um cliente.');return;}
  if(csSelTipos.length===0){alert('Selecione ao menos uma área.');return;}
  var labels={trafego:'Tráfego pago',social:'Social media',cardapio:'Cardápio / operação'};
  var order=['trafego','social','cardapio'];
  var areas=csSelTipos.map(function(t){return labels[t];}).join(', ');
  var partes='';
  order.filter(function(t){return csSelTipos.indexOf(t)>-1;}).forEach(function(t){
    var cfg=CS_TIPOS[t];
    partes+='\n\n## '+labels[t]+'\n';
    cfg.fields.filter(function(f){return f.type==='textarea';}).forEach(function(f){
      var v=gv(f.id);if(v)partes+='- '+f.label+': '+v+'\n';
    });
    if(t==='trafego'){
      var inv=gv('cs-trafego-inv'),ret=gv('cs-trafego-ret'),meta=gv('cs-trafego-meta');
      if(inv&&ret)partes+='- Investido: R$'+inv+' | Retorno: R$'+ret+(meta?' | Meta: R$'+meta:'')+'\n';
    }
  });
  var prox=gv('cs-proximo');
  var prompt='Você é o assistente de comunicação da Seta Lab. Redija uma mensagem de WhatsApp para o cliente "'+csSelClient+'" sobre melhorias recentes nas áreas de: '+areas+'.\n\nDiretrizes:\n- Tom caloroso, direto e próximo — como parceiro de negócio\n- Linguagem simples, sem jargão técnico\n- Integre as áreas numa narrativa coesa, sem separar por tópico\n- Máximo 5 parágrafos curtos\n- No máximo 2 emojis\n- Comece direto com a principal novidade\n'+partes+(prox?'\n- Próximo passo: '+prox+'\n':'')+'\nEscreva apenas a mensagem final, sem introdução nem aspas.';
  csDone[csSelClient]=true;
  document.getElementById('cs-result-title').textContent='Prompt para '+csSelClient;
  document.getElementById('cs-prompt-text').textContent=prompt;
  document.getElementById('cs-result').classList.add('show');
  document.getElementById('cs-result').scrollIntoView({behavior:'smooth',block:'start'});
  renderCSPainel();
}

function renderCSPainel(){
  var n=Object.keys(csDone).filter(function(k){return csDone[k];}).length;
  var total=clients.length;
  var pct=total>0?Math.round(n/total*100):0;
  document.getElementById('cs-prfill').style.width=pct+'%';
  document.getElementById('cs-prsub').textContent=n+' de '+total+' clientes contatados hoje';
  var l=document.getElementById('cs-plist');l.innerHTML='';
  clients.forEach(function(c){
    var d=document.createElement('div');d.className='pitem';
    d.innerHTML='<span class="piname">'+c+'</span><span class="'+(csDone[c]?'sdone':'spend')+'">'+(csDone[c]?'Enviado':'Pendente')+'</span>';
    l.appendChild(d);
  });
}

// ===================== SOCIAL PAGE =====================
var editMensal=false,editQuinzenal=false;

function populateSocialSelects(){
  ['sel-mensal','sel-quinzenal'].forEach(function(sid){
    var sel=document.getElementById(sid);
    var prev=sel.value;
    sel.innerHTML='';
    clients.forEach(function(c){var o=document.createElement('option');o.value=c;o.textContent=c;sel.appendChild(o);});
    if(prev&&clients.indexOf(prev)>-1)sel.value=prev;
  });
}

function switchSocialTab(t){
  ['mensal','quinzenal'].forEach(function(x){
    document.getElementById('stab-'+x).classList.toggle('active',x===t);
    document.getElementById('spane-'+x).classList.toggle('active',x===t);
  });
}

function calcDelta(curr,prev){
  var c=parseFloat(String(curr).replace(/[^0-9.,]/g,'').replace(',','.'));
  var p=parseFloat(String(prev).replace(/[^0-9.,]/g,'').replace(',','.'));
  if(isNaN(c)||isNaN(p)||p===0)return null;
  var pct=((c-p)/Math.abs(p)*100);
  return {text:(pct>=0?'+':'')+pct.toFixed(1)+'%',cls:pct>=0?'up':'down'};
}

function mcHTML(label,val,prev,isPrim){
  var delta=(!isPrim&&prev)?calcDelta(val,prev):null;
  var dHtml=delta?('<span class="'+delta.cls+'">'+delta.text+'</span>'):'<span class="neutral">—</span>';
  return '<div class="mc"><div class="mc-label">'+label+'</div><div class="mc-value">'+(val||'—')+'</div><div class="mc-delta">'+dHtml+'</div></div>';
}

var EMOJIS=['🍝','🍔','🌮','🍕','🥩','☕','🍗','🥗'];
function renderPosts(posts){
  if(!posts||!posts.filter(function(p){return p.titulo;}).length)return '<div style="font-size:12px;color:var(--text-3);padding:8px 0">Nenhuma publicação cadastrada.</div>';
  return posts.filter(function(p){return p.titulo;}).map(function(p,i){
    return '<div class="post-item"><div class="post-meta"><div class="post-thumb">'+EMOJIS[i%EMOJIS.length]+'</div><div><div class="post-title-txt">'+p.titulo+'</div><div class="post-date">'+(p.data||'')+(p.tipo?' · '+p.tipo:'')+'</div></div></div><div class="post-stats"><div><div class="ps-val">'+(p.alcance||'—')+'</div><div class="ps-lbl">alcance</div></div><div><div class="ps-val">'+(p.engaj||'—')+'</div><div class="ps-lbl">engaj.</div></div></div></div>';
  }).join('');
}

function renderMensal(){
  var c=document.getElementById('sel-mensal').value;
  if(!c)return;
  var d=loadData('mensal',c)||{};
  var el=document.getElementById('view-mensal');
  if(!d.periodo){el.innerHTML='<div class="empty-report">Nenhum relatório para <strong>'+c+'</strong>.<br>Clique em <strong>Editar</strong> para preencher.</div>';return;}
  var ip=d.primeiro;
  el.innerHTML=
    '<div class="report-header"><div><div class="client-name-h">'+c+'</div><div class="client-sub-h">Relatório mensal · Instagram</div></div><div class="period-badge">'+d.periodo+'</div></div>'+
    '<div class="slabel">Visão geral</div>'+
    '<div class="metric-grid">'+mcHTML('Alcance total',d.alcance,d.palcance,ip)+mcHTML('Impressões',d.impressoes,d.pimpressoes,ip)+mcHTML('Novos seguidores',d.seguidores,d.pseguidores,ip)+mcHTML('Engajamento',d.engaj,d.pengaj,ip)+mcHTML('Publicações',d.pubs,null,true)+mcHTML('Cliques no perfil',d.cliques,d.pcliques,ip)+'</div>'+
    '<div class="slabel">Top publicações</div>'+
    '<div class="card" style="padding:16px"><div class="post-list">'+renderPosts(d.posts)+'</div></div>'+
    '<div class="slabel">Análise</div>'+
    '<div class="ibox gr"><p><strong>O que funcionou:</strong> '+(d.destaque||'—')+'</p></div>'+
    '<div class="ibox pu"><p><strong>Foco próximo mês:</strong> '+(d.proximo||'—')+'</p></div>';
}

function renderQuinzenal(){
  var c=document.getElementById('sel-quinzenal').value;
  if(!c)return;
  var d=loadData('quinzenal',c)||{};
  var el=document.getElementById('view-quinzenal');
  if(!d.periodo){el.innerHTML='<div class="empty-report">Nenhum relatório para <strong>'+c+'</strong>.<br>Clique em <strong>Editar</strong> para preencher.</div>';return;}
  var ip=d.primeiro;
  el.innerHTML=
    '<div class="report-header"><div><div class="client-name-h">'+c+'</div><div class="client-sub-h">Relatório quinzenal · Instagram</div></div><div class="period-badge">'+d.periodo+'</div></div>'+
    '<div class="slabel">Visão geral</div>'+
    '<div class="metric-grid">'+mcHTML('Alcance',d.alcance,d.palcance,ip)+mcHTML('Impressões',d.impressoes,d.pimpressoes,ip)+mcHTML('Novos seguidores',d.seguidores,d.pseguidores,ip)+mcHTML('Engajamento',d.engaj,d.pengaj,ip)+mcHTML('Publicações',d.pubs,null,true)+mcHTML('Cliques no perfil',d.cliques,d.pcliques,ip)+'</div>'+
    '<div class="slabel">Destaque da quinzena</div>'+
    '<div class="ibox gr"><p>'+(d.destaque||'—')+'</p></div>'+
    '<div class="slabel">Próximo passo</div>'+
    '<div class="ibox pu"><p>'+(d.proximo||'—')+'</p></div>';
}

function toggleEditM(){
  editMensal=!editMensal;
  var btn=document.getElementById('editToggleM');
  btn.textContent=editMensal?'Visualizar':'Editar';btn.classList.toggle('on',editMensal);
  document.getElementById('view-mensal').style.display=editMensal?'none':'block';
  document.getElementById('edit-mensal').style.display=editMensal?'block':'none';
  if(editMensal)fillEditMensal();
}

function toggleEditQ(){
  editQuinzenal=!editQuinzenal;
  var btn=document.getElementById('editToggleQ');
  btn.textContent=editQuinzenal?'Visualizar':'Editar';btn.classList.toggle('on',editQuinzenal);
  document.getElementById('view-quinzenal').style.display=editQuinzenal?'none':'block';
  document.getElementById('edit-quinzenal').style.display=editQuinzenal?'block':'none';
  if(editQuinzenal)fillEditQuinzenal();
}

function togglePrevSec(t,ip){
  var ps=document.getElementById('prevSec'+t),fn=document.getElementById('firstNote'+t);
  if(ps)ps.style.display=ip?'none':'block';if(fn)fn.style.display=ip?'block':'none';
}

document.getElementById('ePrimMes').addEventListener('change',function(){togglePrevSec('M',this.checked);});
document.getElementById('ePrimQ').addEventListener('change',function(){togglePrevSec('Q',this.checked);});

function fillEditMensal(){
  var c=document.getElementById('sel-mensal').value;
  var d=loadData('mensal',c)||{};
  sv('ePerM',d.periodo);sc('ePrimMes',d.primeiro);
  sv('eAlcM',d.alcance);sv('eImpM',d.impressoes);sv('eSegM',d.seguidores);
  sv('eEngM',d.engaj);sv('ePubM',d.pubs);sv('eCliM',d.cliques);
  sv('ePAlcM',d.palcance);sv('ePImpM',d.pimpressoes);sv('ePSegM',d.pseguidores);
  sv('ePEngM',d.pengaj);sv('ePCliM',d.pcliques);
  sv('eDestM',d.destaque);sv('eProxM',d.proximo);
  togglePrevSec('M',d.primeiro);
  var posts=d.posts||[{},{},{}];
  var cont=document.getElementById('ePostsM');cont.innerHTML='';
  for(var i=0;i<3;i++){
    var p=posts[i]||{};
    var b=document.createElement('div');b.className='peb';
    b.innerHTML='<div class="peb-num">Publicação '+(i+1)+'</div><div class="peg"><div class="ef"><label>Título</label><input type="text" id="eP'+i+'T" value="'+(p.titulo||'')+'" placeholder="Nome do post"></div><div class="ef"><label>Data</label><input type="text" id="eP'+i+'D" value="'+(p.data||'')+'" placeholder="12 abr"></div><div class="ef"><label>Tipo</label><input type="text" id="eP'+i+'Tp" value="'+(p.tipo||'')+'" placeholder="Reel"></div><div class="ef"><label>Alcance</label><input type="text" id="eP'+i+'A" value="'+(p.alcance||'')+'" placeholder="8.4k"></div><div class="ef"><label>Engaj.</label><input type="text" id="eP'+i+'E" value="'+(p.engaj||'')+'" placeholder="6,2%"></div></div>';
    cont.appendChild(b);
  }
}

function fillEditQuinzenal(){
  var c=document.getElementById('sel-quinzenal').value;
  var d=loadData('quinzenal',c)||{};
  sv('ePerQ',d.periodo);sc('ePrimQ',d.primeiro);
  sv('eAlcQ',d.alcance);sv('eImpQ',d.impressoes);sv('eSegQ',d.seguidores);
  sv('eEngQ',d.engaj);sv('ePubQ',d.pubs);sv('eCliQ',d.cliques);
  sv('ePAlcQ',d.palcance);sv('ePImpQ',d.pimpressoes);sv('ePSegQ',d.pseguidores);
  sv('ePEngQ',d.pengaj);sv('ePCliQ',d.pcliques);
  sv('eDestQ',d.destaque);sv('eProxQ',d.proximo);
  togglePrevSec('Q',d.primeiro);
}

function saveMensal(){
  var c=document.getElementById('sel-mensal').value;
  var posts=[];
  for(var i=0;i<3;i++)posts.push({titulo:gv('eP'+i+'T'),data:gv('eP'+i+'D'),tipo:gv('eP'+i+'Tp'),alcance:gv('eP'+i+'A'),engaj:gv('eP'+i+'E')});
  saveData('mensal',c,{periodo:gv('ePerM'),primeiro:gc('ePrimMes'),alcance:gv('eAlcM'),impressoes:gv('eImpM'),seguidores:gv('eSegM'),engaj:gv('eEngM'),pubs:gv('ePubM'),cliques:gv('eCliM'),palcance:gv('ePAlcM'),pimpressoes:gv('ePImpM'),pseguidores:gv('ePSegM'),pengaj:gv('ePEngM'),pcliques:gv('ePCliM'),destaque:gv('eDestM'),proximo:gv('eProxM'),posts:posts});
  renderMensal();
  var btn=document.getElementById('saveM');btn.textContent='Salvo!';btn.classList.add('saved');
  setTimeout(function(){btn.textContent='Salvar relatório mensal';btn.classList.remove('saved');},2000);
}

function saveQuinzenal(){
  var c=document.getElementById('sel-quinzenal').value;
  saveData('quinzenal',c,{periodo:gv('ePerQ'),primeiro:gc('ePrimQ'),alcance:gv('eAlcQ'),impressoes:gv('eImpQ'),seguidores:gv('eSegQ'),engaj:gv('eEngQ'),pubs:gv('ePubQ'),cliques:gv('eCliQ'),palcance:gv('ePAlcQ'),pimpressoes:gv('ePImpQ'),pseguidores:gv('ePSegQ'),pengaj:gv('ePEngQ'),pcliques:gv('ePCliQ'),destaque:gv('eDestQ'),proximo:gv('eProxQ')});
  renderQuinzenal();
  var btn=document.getElementById('saveQ');btn.textContent='Salvo!';btn.classList.add('saved');
  setTimeout(function(){btn.textContent='Salvar relatório quinzenal';btn.classList.remove('saved');},2000);
}

// ===================== CLIENTS =====================
function renderManage(){
  var l=document.getElementById('cmList');l.innerHTML='';
  if(clients.length===0){l.innerHTML='<div class="empty-state">Nenhum cliente cadastrado.</div>';return;}
  clients.forEach(function(c,i){
    var d=document.createElement('div');d.className='cm-item';
    d.innerHTML='<span class="cm-name">'+c+'</span><button class="rm-btn">Remover</button>';
    d.querySelector('.rm-btn').addEventListener('click',function(){removeClient(i);});
    l.appendChild(d);
  });
}

function addClient(){
  var v=document.getElementById('iNewClient').value.trim();
  if(!v)return;
  if(clients.indexOf(v)>-1){alert('Cliente já existe.');return;}
  clients.push(v);saveClients();
  document.getElementById('iNewClient').value='';
  renderManage();renderCSGrid();populateSocialSelects();
}

function removeClient(i){
  if(!confirm('Remover "'+clients[i]+'"?'))return;
  if(csSelClient===clients[i])csSelClient=null;
  clients.splice(i,1);saveClients();
  renderManage();renderCSGrid();populateSocialSelects();
}

document.getElementById('iNewClient').addEventListener('keydown',function(e){if(e.key==='Enter')addClient();});

// ===================== COPY UTILS =====================
function copyText(sourceId,btnId){
  var el=document.getElementById(sourceId);
  var text=el.tagName==='PRE'?el.textContent:el.textContent;
  navigator.clipboard.writeText(text).then(function(){
    var btn=document.getElementById(btnId);
    btn.classList.add('copied');
    btn.innerHTML='<svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="20 6 9 17 4 12"/></svg> Copiado!';
    setTimeout(function(){
      btn.classList.remove('copied');
      btn.innerHTML='<svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1"/></svg> Copiar';
    },2500);
  });
}

// ===================== INIT =====================
populateSocialSelects();
renderMensal();
renderQuinzenal();
renderCSGrid();
renderCSPainel();
</script>
</body>
</html>
