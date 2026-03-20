# Sanchez-Calculator[index.html](https://github.com/user-attachments/files/26149415/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#8B0000">
<title>Sanchez Junk & Haul — Pro Calculator</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Barlow:wght@300;400;500;600;700&family=Barlow+Condensed:wght@500;600;700&display=swap" rel="stylesheet">
<style>
/* ── RESET ───────────────────────────────────────────────────── */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
html{scroll-behavior:smooth;}
body{font-family:'Barlow',sans-serif;min-height:100vh;transition:background 0.3s,color 0.3s;-webkit-tap-highlight-color:transparent;}

/* ── THEMES ──────────────────────────────────────────────────── */
body.light{
  --bg:#f2efe9;--bg2:#e8e4dc;--surface:#ffffff;--surface2:#f7f4f0;--surface3:#ede9e2;
  --border:rgba(0,0,0,0.09);--border2:rgba(0,0,0,0.05);
  --text:#18140f;--text2:#5c5650;--text3:#9c9690;
  --red:#8B0000;--red2:#a50000;--red-bg:rgba(139,0,0,0.07);--red-border:rgba(139,0,0,0.2);
  --green:#1a6600;--green-bg:rgba(26,102,0,0.08);
  --amber:#7a4a00;--amber-bg:rgba(180,120,0,0.09);
  --danger:#c0392b;--danger-bg:rgba(192,57,43,0.08);
  --shadow:0 2px 12px rgba(0,0,0,0.08);--shadow-lg:0 8px 32px rgba(0,0,0,0.12);
}
body.dark{
  --bg:#0f0d0b;--bg2:#1a1714;--surface:#211e1a;--surface2:#2a2622;--surface3:#332f2a;
  --border:rgba(255,255,255,0.08);--border2:rgba(255,255,255,0.04);
  --text:#f0ece6;--text2:#a09890;--text3:#605850;
  --red:#c0392b;--red2:#e04030;--red-bg:rgba(192,57,43,0.12);--red-border:rgba(192,57,43,0.3);
  --green:#4caf50;--green-bg:rgba(76,175,80,0.1);
  --amber:#e6a020;--amber-bg:rgba(230,160,32,0.1);
  --danger:#e05040;--danger-bg:rgba(224,80,64,0.1);
  --shadow:0 2px 12px rgba(0,0,0,0.4);--shadow-lg:0 8px 32px rgba(0,0,0,0.5);
}

/* ── LOGIN SCREEN ────────────────────────────────────────────── */
#loginScreen{
  position:fixed;inset:0;z-index:9999;
  display:flex;align-items:center;justify-content:center;
  background:var(--bg);
  animation:fadeIn 0.4s ease;
}
.login-box{
  width:100%;max-width:380px;padding:0 20px;
  display:flex;flex-direction:column;align-items:center;gap:0;
}
.login-logo{
  font-family:'Bebas Neue',sans-serif;
  font-size:52px;letter-spacing:0.04em;color:var(--red);
  line-height:1;margin-bottom:4px;text-align:center;
}
.login-sub{
  font-size:11px;font-weight:600;letter-spacing:0.18em;text-transform:uppercase;
  color:var(--text3);margin-bottom:40px;text-align:center;
}
.login-label{font-size:12px;font-weight:600;color:var(--text2);letter-spacing:0.06em;text-transform:uppercase;margin-bottom:6px;align-self:flex-start;}
.login-input{
  width:100%;padding:14px 16px;font-size:16px;font-family:'Barlow',sans-serif;
  background:var(--surface);border:1.5px solid var(--border);border-radius:10px;
  color:var(--text);outline:none;margin-bottom:12px;transition:border 0.2s;
}
.login-input:focus{border-color:var(--red);}
.login-btn{
  width:100%;padding:15px;font-size:15px;font-weight:700;font-family:'Barlow',sans-serif;
  letter-spacing:0.06em;text-transform:uppercase;
  background:var(--red);color:#fff;border:none;border-radius:10px;
  cursor:pointer;transition:opacity 0.15s;margin-top:4px;
}
.login-btn:hover{opacity:0.9;}
.login-err{font-size:12px;color:var(--danger);margin-top:8px;text-align:center;min-height:16px;}

/* ── APP WRAPPER ─────────────────────────────────────────────── */
#app{display:none;min-height:100vh;background:var(--bg);}

/* ── HEADER ──────────────────────────────────────────────────── */
.header{
  background:var(--red);padding:0 20px;
  display:flex;align-items:center;justify-content:space-between;
  position:sticky;top:0;z-index:100;height:58px;
  box-shadow:0 2px 16px rgba(139,0,0,0.35);
}
.header-left{display:flex;align-items:baseline;gap:10px;}
.header-logo{font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:0.06em;color:#fff;}
.header-tagline{font-size:10px;font-weight:500;color:rgba(255,255,255,0.55);letter-spacing:0.1em;text-transform:uppercase;}
.header-right{display:flex;align-items:center;gap:10px;}
.dark-toggle{
  background:rgba(255,255,255,0.15);border:none;border-radius:20px;
  padding:6px 12px;color:#fff;font-size:13px;cursor:pointer;font-family:'Barlow',sans-serif;
  font-weight:500;transition:background 0.2s;
}
.dark-toggle:hover{background:rgba(255,255,255,0.25);}
.logout-btn{
  background:rgba(255,255,255,0.12);border:1px solid rgba(255,255,255,0.2);
  border-radius:8px;padding:5px 10px;color:rgba(255,255,255,0.7);
  font-size:11px;cursor:pointer;font-family:'Barlow',sans-serif;font-weight:500;
  transition:all 0.2s;
}
.logout-btn:hover{background:rgba(255,255,255,0.2);color:#fff;}

/* ── TABS ────────────────────────────────────────────────────── */
.tabs{
  display:flex;background:var(--surface);
  border-bottom:1.5px solid var(--border2);
  overflow-x:auto;-webkit-overflow-scrolling:touch;
}
.tabs::-webkit-scrollbar{display:none;}
.tab{
  flex:1;min-width:80px;padding:14px 8px;text-align:center;
  font-size:12px;font-weight:600;letter-spacing:0.05em;text-transform:uppercase;
  color:var(--text3);cursor:pointer;border:none;background:none;
  font-family:'Barlow',sans-serif;border-bottom:2.5px solid transparent;
  transition:all 0.2s;white-space:nowrap;
}
.tab.active{color:var(--red);border-bottom-color:var(--red);}
.tab:hover:not(.active){color:var(--text2);}

/* ── PANELS ──────────────────────────────────────────────────── */
.panel{display:none;padding:20px;max-width:780px;margin:0 auto;}
.panel.active{display:block;}

/* ── SECTION ─────────────────────────────────────────────────── */
.section{margin-bottom:20px;}
.slabel{
  font-size:10px;font-weight:700;color:var(--text3);
  letter-spacing:0.14em;text-transform:uppercase;margin-bottom:10px;
  display:flex;align-items:center;gap:6px;
}
.slabel::after{content:'';flex:1;height:1px;background:var(--border2);}

/* ── TRAILER INFO BANNER ─────────────────────────────────────── */
.trailer-banner{
  background:var(--red-bg);border:1px solid var(--red-border);border-radius:10px;
  padding:10px 14px;margin-bottom:20px;
  display:flex;align-items:center;gap:10px;
}
.trailer-banner-icon{font-size:20px;}
.trailer-banner-text{font-size:12px;color:var(--text2);line-height:1.5;}
.trailer-banner-text strong{color:var(--red);font-weight:700;}

/* ── LOAD SIZE ───────────────────────────────────────────────── */
.load-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;}
@media(max-width:480px){.load-grid{grid-template-columns:repeat(2,1fr);}}
.load-btn{
  border:1.5px solid var(--border);border-radius:12px;padding:12px 6px;
  text-align:center;cursor:pointer;background:var(--surface);
  transition:all 0.2s;position:relative;overflow:hidden;
}
.load-btn::before{
  content:'';position:absolute;inset:0;background:var(--red);
  opacity:0;transition:opacity 0.2s;
}
.load-btn:hover::before{opacity:0.04;}
.load-btn.active{border-color:var(--red);background:var(--red-bg);}
.load-btn.active .lb-pct{opacity:1;}
.lb-name{font-size:13px;font-weight:700;color:var(--text);font-family:'Barlow Condensed',sans-serif;letter-spacing:0.02em;}
.lb-price{font-size:10px;color:var(--text2);margin-top:3px;font-weight:500;}
.lb-vol{font-size:9px;color:var(--text3);margin-top:2px;}
.lb-pct{
  display:inline-block;margin-top:4px;font-size:9px;font-weight:700;
  background:var(--red);color:#fff;border-radius:20px;padding:1px 6px;
  opacity:0;transition:opacity 0.2s;
}

/* ── MATERIAL GRID ───────────────────────────────────────────── */
.mat-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;}
@media(max-width:380px){.mat-grid{grid-template-columns:repeat(2,1fr);}}
.mat-btn{
  border:1.5px solid var(--border);border-radius:10px;padding:9px 6px;
  text-align:center;cursor:pointer;background:var(--surface);
  font-size:11px;font-weight:600;color:var(--text2);
  transition:all 0.2s;line-height:1.3;
}
.mat-btn:hover{border-color:var(--red);color:var(--text);}
.mat-btn.active{border-color:var(--red);background:var(--red-bg);color:var(--text);}
.mat-weight{font-size:9px;color:var(--text3);margin-top:2px;font-weight:400;}

/* ── WEIGHT ROW ──────────────────────────────────────────────── */
.weight-row{display:flex;align-items:center;gap:10px;margin-top:10px;flex-wrap:wrap;}
.weight-row input{width:110px;}
.dump-tag{
  display:inline-flex;align-items:center;gap:4px;
  font-size:11px;font-weight:600;background:var(--amber-bg);
  color:var(--amber);border-radius:20px;padding:4px 10px;
  border:1px solid rgba(180,120,0,0.2);
}
.wt-hint{font-size:11px;color:var(--text3);}

/* ── FORM FIELDS ─────────────────────────────────────────────── */
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.grid3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;}
@media(max-width:400px){.grid3{grid-template-columns:1fr 1fr;}}
.field{display:flex;flex-direction:column;gap:5px;}
.field label{font-size:11px;font-weight:600;color:var(--text2);letter-spacing:0.04em;}
.field input,.field select,.field textarea{
  border:1.5px solid var(--border);border-radius:10px;
  padding:10px 12px;font-size:15px;background:var(--surface);color:var(--text);
  width:100%;font-family:'Barlow',sans-serif;-webkit-appearance:none;
  transition:border 0.2s,box-shadow 0.2s;
}
.field textarea{resize:vertical;min-height:72px;font-size:14px;line-height:1.5;}
.field input:focus,.field select:focus,.field textarea:focus{
  outline:none;border-color:var(--red);box-shadow:0 0 0 3px rgba(139,0,0,0.1);
}
.field-hint{font-size:10px;color:var(--text3);margin-top:2px;}

/* ── DIVIDER ─────────────────────────────────────────────────── */
.divider{border:none;border-top:1.5px solid var(--border2);margin:20px 0;}

/* ── RESULT CARD ─────────────────────────────────────────────── */
.result-card{
  background:var(--surface);border:1.5px solid var(--border);
  border-radius:16px;padding:18px;box-shadow:var(--shadow);
}
.result-row{
  display:flex;justify-content:space-between;align-items:center;
  padding:6px 0;font-size:13px;border-bottom:1px solid var(--border2);
}
.result-row:last-of-type{border-bottom:none;}
.r-label{color:var(--text2);font-weight:500;}
.r-val{font-weight:700;color:var(--text);}
.r-val.neg{color:var(--danger);}
.result-total{
  display:flex;justify-content:space-between;align-items:center;
  padding:14px 0 0;border-top:2px solid var(--border);margin-top:8px;
}
.rt-label{font-size:15px;font-weight:700;color:var(--text);}
.rt-val{
  font-family:'Bebas Neue',sans-serif;font-size:38px;letter-spacing:0.02em;
  line-height:1;
}
.rt-val.pos{color:var(--green);}
.rt-val.neg{color:var(--danger);}

/* ── MARGIN BAR ──────────────────────────────────────────────── */
.bar-wrap{margin-top:14px;}
.bar-meta{display:flex;justify-content:space-between;font-size:11px;margin-bottom:6px;}
.bar-meta span:first-child{color:var(--text2);font-weight:600;}
.bar-meta span:last-child{font-weight:700;color:var(--text);}
.bar-track{height:8px;background:var(--surface3);border-radius:4px;overflow:hidden;}
.bar-fill{height:100%;border-radius:4px;transition:width 0.4s cubic-bezier(.4,0,.2,1),background 0.4s;}
.bar-ends{display:flex;justify-content:space-between;font-size:10px;color:var(--text3);margin-top:4px;}

/* ── TIME CARD ───────────────────────────────────────────────── */
.time-card{
  background:var(--surface);border:1.5px solid var(--border);
  border-radius:16px;padding:18px;margin-top:12px;box-shadow:var(--shadow);
}
.time-top{display:flex;justify-content:space-between;align-items:flex-start;gap:10px;}
.time-lbl{font-size:11px;font-weight:600;color:var(--text2);letter-spacing:0.04em;text-transform:uppercase;margin-bottom:4px;}
.time-val{font-family:'Bebas Neue',sans-serif;font-size:34px;letter-spacing:0.02em;line-height:1;color:var(--text);}
.time-sub{font-size:11px;color:var(--text3);margin-top:3px;}
.badge{font-size:11px;padding:5px 12px;border-radius:20px;font-weight:700;letter-spacing:0.04em;white-space:nowrap;}
.badge.green{background:var(--green-bg);color:var(--green);}
.badge.amber{background:var(--amber-bg);color:var(--amber);}
.badge.red{background:var(--danger-bg);color:var(--danger);}
.time-note{font-size:12px;color:var(--text2);margin-top:12px;line-height:1.6;padding:10px 12px;background:var(--surface2);border-radius:8px;}

/* ── SAVE CARD ───────────────────────────────────────────────── */
.save-card{
  background:var(--surface2);border:1.5px solid var(--border);
  border-radius:16px;padding:18px;margin-top:12px;
}

/* ── BUTTONS ─────────────────────────────────────────────────── */
.btn-primary{
  width:100%;margin-top:14px;padding:15px;border:none;border-radius:12px;
  background:var(--red);color:#fff;font-size:14px;font-weight:700;
  font-family:'Barlow',sans-serif;letter-spacing:0.08em;text-transform:uppercase;
  cursor:pointer;transition:all 0.2s;box-shadow:0 4px 14px rgba(139,0,0,0.3);
}
.btn-primary:hover{opacity:0.9;transform:translateY(-1px);}
.btn-primary:active{transform:translateY(0);opacity:0.85;}
.btn-secondary{
  width:100%;margin-top:10px;padding:13px;
  border:1.5px solid var(--border);border-radius:12px;
  background:var(--surface);color:var(--text2);font-size:13px;font-weight:600;
  font-family:'Barlow',sans-serif;letter-spacing:0.04em;cursor:pointer;transition:all 0.2s;
}
.btn-secondary:hover{border-color:var(--red);color:var(--red);}
.btn-secondary.success{color:var(--green);border-color:var(--green);}
.btn-ghost{
  width:100%;margin-top:8px;padding:12px;
  border:1.5px dashed var(--red-border);border-radius:12px;
  background:transparent;color:var(--red);font-size:12px;font-weight:600;
  font-family:'Barlow',sans-serif;letter-spacing:0.06em;text-transform:uppercase;
  cursor:pointer;transition:all 0.2s;
}
.btn-ghost:hover{background:var(--red-bg);}

/* ── STATS GRID ──────────────────────────────────────────────── */
.stats-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-bottom:20px;}
@media(min-width:600px){.stats-grid{grid-template-columns:repeat(4,1fr);}}
.stat-card{
  background:var(--surface);border:1.5px solid var(--border);
  border-radius:12px;padding:14px;box-shadow:var(--shadow);
}
.stat-lbl{font-size:10px;font-weight:700;color:var(--text3);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:6px;}
.stat-val{font-family:'Bebas Neue',sans-serif;font-size:28px;color:var(--text);letter-spacing:0.02em;}
.stat-sub{font-size:10px;color:var(--text3);margin-top:2px;}

/* ── MONTH FILTER ────────────────────────────────────────────── */
.month-row{display:flex;align-items:center;gap:12px;margin-bottom:14px;}
.month-row select{
  border:1.5px solid var(--border);border-radius:10px;padding:9px 12px;
  font-size:14px;background:var(--surface);color:var(--text);
  font-family:'Barlow',sans-serif;-webkit-appearance:none;flex:1;
}

/* ── JOB CARDS ───────────────────────────────────────────────── */
.job-list{display:flex;flex-direction:column;gap:10px;}
.job-card{
  background:var(--surface);border:1.5px solid var(--border);
  border-radius:14px;padding:16px;box-shadow:var(--shadow);
  transition:box-shadow 0.2s;
}
.job-card:hover{box-shadow:var(--shadow-lg);}
.job-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:8px;}
.job-name{font-size:16px;font-weight:700;color:var(--text);font-family:'Barlow Condensed',sans-serif;letter-spacing:0.02em;}
.job-date{font-size:11px;color:var(--text3);font-weight:500;}
.job-row{display:flex;flex-wrap:wrap;gap:8px;font-size:12px;color:var(--text2);margin-bottom:5px;align-items:center;}
.job-profit{font-weight:700;}
.job-profit.pos{color:var(--green);}
.job-profit.neg{color:var(--danger);}
.pill{font-size:10px;padding:3px 9px;border-radius:20px;font-weight:700;}
.pill.green{background:var(--green-bg);color:var(--green);}
.pill.amber{background:var(--amber-bg);color:var(--amber);}
.pill.red{background:var(--danger-bg);color:var(--danger);}
.job-notes{font-size:12px;color:var(--text3);margin-top:6px;font-style:italic;line-height:1.5;padding:8px;background:var(--surface2);border-radius:8px;}
.job-actions{display:flex;gap:10px;margin-top:10px;}
.job-del{font-size:11px;color:var(--text3);background:none;border:none;cursor:pointer;font-family:'Barlow',sans-serif;font-weight:600;padding:4px 8px;border-radius:6px;transition:all 0.15s;}
.job-del:hover{color:var(--danger);background:var(--danger-bg);}
.job-quote-btn{font-size:11px;color:var(--red);background:var(--red-bg);border:none;cursor:pointer;font-family:'Barlow',sans-serif;font-weight:600;padding:4px 10px;border-radius:6px;transition:all 0.15s;}
.job-quote-btn:hover{opacity:0.8;}

/* ── QUOTE GENERATOR ─────────────────────────────────────────── */
.quote-card{
  background:var(--surface);border:1.5px solid var(--border);
  border-radius:16px;padding:20px;box-shadow:var(--shadow);margin-bottom:16px;
}
.quote-preview{
  background:var(--surface2);border:1.5px solid var(--border);
  border-radius:12px;padding:16px;font-size:13px;line-height:1.8;
  color:var(--text);white-space:pre-wrap;font-family:'Barlow',sans-serif;
  margin-top:14px;
}
.quote-preview strong{color:var(--red);font-weight:700;}

/* ── EMPTY STATE ─────────────────────────────────────────────── */
.empty{text-align:center;padding:48px 20px;color:var(--text3);}
.empty-icon{font-size:40px;margin-bottom:12px;}
.empty strong{display:block;font-size:16px;color:var(--text2);margin-bottom:6px;font-family:'Barlow Condensed',sans-serif;letter-spacing:0.04em;}

/* ── ANIMATIONS ──────────────────────────────────────────────── */
@keyframes fadeIn{from{opacity:0;transform:translateY(10px);}to{opacity:1;transform:translateY(0);}}
@keyframes slideUp{from{opacity:0;transform:translateY(20px);}to{opacity:1;transform:translateY(0);}}
.panel.active{animation:slideUp 0.3s ease;}

/* ── DESKTOP ENHANCEMENTS ────────────────────────────────────── */
@media(min-width:640px){
  .panel{padding:28px 32px;}
  .load-grid{grid-template-columns:repeat(4,1fr);}
  .mat-grid{grid-template-columns:repeat(6,1fr);}
}
</style>
</head>
<body class="light">

<!-- ── LOGIN SCREEN ─────────────────────────────────────────── -->
<div id="loginScreen">
  <div class="login-box">
    <div class="login-logo">Sanchez</div>
    <div class="login-sub">Junk &amp; Haul Co. · Pro Tools</div>
    <div class="login-label">Password</div>
    <input class="login-input" type="password" id="loginInput" placeholder="Enter password" autocomplete="current-password">
    <button class="login-btn" onclick="doLogin()">Enter</button>
    <div class="login-err" id="loginErr"></div>
  </div>
</div>

<!-- ── APP ──────────────────────────────────────────────────── -->
<div id="app">

  <div class="header">
    <div class="header-left">
      <span class="header-logo">Sanchez J&amp;H</span>
      <span class="header-tagline">Pro Tools</span>
    </div>
    <div class="header-right">
      <button class="dark-toggle" onclick="toggleDark()" id="darkBtn">🌙 Dark</button>
      <button class="logout-btn" onclick="doLogout()">Lock</button>
    </div>
  </div>

  <div class="tabs">
    <button class="tab active" onclick="switchTab('calc')">Calculator</button>
    <button class="tab" onclick="switchTab('quote')">Quote Gen</button>
    <button class="tab" onclick="switchTab('history')">History</button>
  </div>

  <!-- ═══════════════════════════════════════════════════════════
       CALCULATOR TAB
  ════════════════════════════════════════════════════════════ -->
  <div class="panel active" id="panel-calc">

    <div class="trailer-banner">
      <div class="trailer-banner-icon">🚛</div>
      <div class="trailer-banner-text">
        <strong>5×8 Utility Trailer</strong> — 40 sq ft bed · ~2.5–3.5 cu yd capacity · Max load ~1,500 lbs
      </div>
    </div>

    <div class="section">
      <div class="slabel">Load size</div>
      <div class="load-grid">
        <div class="load-btn active" data-price="125" data-idx="0" onclick="selectLoad(this)">
          <div class="lb-name">Quarter</div>
          <div class="lb-price">$100–150</div>
          <div class="lb-vol">~0.5–1 cu yd</div>
          <div class="lb-pct">25%</div>
        </div>
        <div class="load-btn" data-price="225" data-idx="1" onclick="selectLoad(this)">
          <div class="lb-name">Half</div>
          <div class="lb-price">$175–275</div>
          <div class="lb-vol">~1–1.5 cu yd</div>
          <div class="lb-pct">50%</div>
        </div>
        <div class="load-btn" data-price="350" data-idx="2" onclick="selectLoad(this)">
          <div class="lb-name">Three-Qtr</div>
          <div class="lb-price">$300–400</div>
          <div class="lb-vol">~1.5–2.5 cu yd</div>
          <div class="lb-pct">75%</div>
        </div>
        <div class="load-btn" data-price="475" data-idx="3" onclick="selectLoad(this)">
          <div class="lb-name">Full</div>
          <div class="lb-price">$450–525</div>
          <div class="lb-vol">~2.5–3.5 cu yd</div>
          <div class="lb-pct">100%</div>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="slabel">Material type</div>
      <div class="mat-grid">
        <div class="mat-btn active" data-type="Mixed / general" data-weight="600" onclick="selectMat(this)">
          Mixed<div class="mat-weight">~600 lbs</div>
        </div>
        <div class="mat-btn" data-type="Furniture" data-weight="450" onclick="selectMat(this)">
          Furniture<div class="mat-weight">~450 lbs</div>
        </div>
        <div class="mat-btn" data-type="Appliances" data-weight="700" onclick="selectMat(this)">
          Appliances<div class="mat-weight">~700 lbs</div>
        </div>
        <div class="mat-btn" data-type="Construction debris" data-weight="1100" onclick="selectMat(this)">
          C&amp;D<div class="mat-weight">~1,100 lbs</div>
        </div>
        <div class="mat-btn" data-type="Yard waste" data-weight="400" onclick="selectMat(this)">
          Yard waste<div class="mat-weight">~400 lbs</div>
        </div>
        <div class="mat-btn" data-type="Electronics" data-weight="300" onclick="selectMat(this)">
          Electronics<div class="mat-weight">~300 lbs</div>
        </div>
      </div>
      <div class="weight-row">
        <span class="wt-hint">Est. weight:</span>
        <input type="number" id="weightInput" value="600" inputmode="numeric" oninput="onWeightChange()" style="width:110px;">
        <span class="wt-hint">lbs</span>
        <div class="dump-tag" id="dumpTag">⚡ $60 · 0–1,000 lbs</div>
      </div>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="slabel">Revenue</div>
      <div class="grid2">
        <div class="field">
          <label>Quoted price ($)</label>
          <input type="number" id="quotedPrice" value="125" inputmode="decimal" oninput="calc()">
        </div>
        <div class="field">
          <label>Tip ($)</label>
          <input type="number" id="tipAmt" value="0" inputmode="decimal" oninput="calc()">
        </div>
      </div>
    </div>

    <div class="section">
      <div class="slabel">Costs</div>
      <div class="grid2" style="margin-bottom:12px;">
        <div class="field">
          <label>Dump fee ($)</label>
          <input type="number" id="dumpFee" value="60" inputmode="decimal" oninput="calc()">
          <div class="field-hint">Taylor non-resident rate · auto-fills</div>
        </div>
        <div class="field">
          <label>Miles (round trip)</label>
          <input type="number" id="miles" value="20" inputmode="decimal" oninput="calc()">
        </div>
      </div>
      <div class="grid3" style="margin-bottom:12px;">
        <div class="field">
          <label>Helpers</label>
          <input type="number" id="helpers" value="0" min="0" inputmode="numeric" oninput="calc()">
        </div>
        <div class="field">
          <label>Helper hrs</label>
          <input type="number" id="helperHrs" value="2" inputmode="decimal" oninput="calc()">
        </div>
        <div class="field">
          <label>Rate ($/hr)</label>
          <input type="number" id="helperRate" value="20" inputmode="decimal" oninput="calc()">
        </div>
      </div>
      <div class="grid3">
        <div class="field">
          <label>MPG</label>
          <input type="number" id="mpg" value="16" inputmode="decimal" oninput="calc()">
        </div>
        <div class="field">
          <label>Gas ($/gal)</label>
          <input type="number" id="gasPrice" value="3.50" step="0.01" inputmode="decimal" oninput="calc()">
        </div>
        <div class="field">
          <label>Insurance ($)</label>
          <input type="number" id="insurance" value="3" step="0.50" inputmode="decimal" oninput="calc()">
        </div>
      </div>
    </div>

    <div class="section">
      <div class="slabel">Your time</div>
      <div class="grid2">
        <div class="field">
          <label>Your hours on job</label>
          <input type="number" id="yourHrs" value="1.5" step="0.5" inputmode="decimal" oninput="calc()">
        </div>
        <div class="field">
          <label>Target rate ($/hr)</label>
          <input type="number" id="targetRate" value="125" inputmode="decimal" oninput="calc()">
        </div>
      </div>
    </div>

    <div class="divider"></div>

    <!-- RESULTS -->
    <div class="result-card">
      <div class="result-row"><span class="r-label">Quoted price</span><span class="r-val" id="r-quoted">$125</span></div>
      <div class="result-row"><span class="r-label">Tip</span><span class="r-val" id="r-tip">$0</span></div>
      <div class="result-row"><span class="r-label">Dump fee</span><span class="r-val neg" id="r-dump">−$60</span></div>
      <div class="result-row"><span class="r-label">Fuel</span><span class="r-val neg" id="r-fuel">−$4</span></div>
      <div class="result-row"><span class="r-label">Helper labor</span><span class="r-val neg" id="r-labor">−$0</span></div>
      <div class="result-row"><span class="r-label">Insurance</span><span class="r-val neg" id="r-ins">−$3</span></div>
      <div class="result-total">
        <span class="rt-label">Company profit</span>
        <span class="rt-val pos" id="r-profit">$58</span>
      </div>
      <div class="bar-wrap">
        <div class="bar-meta">
          <span>Profit margin</span>
          <span id="r-margin-pct">46%</span>
        </div>
        <div class="bar-track"><div class="bar-fill" id="marginBar" style="width:46%;background:#1a6600;"></div></div>
        <div class="bar-ends"><span>0%</span><span>50%</span><span>100%</span></div>
      </div>
    </div>

    <div class="time-card">
      <div class="time-top">
        <div>
          <div class="time-lbl">Your effective hourly rate</div>
          <div class="time-val" id="t-rate">$83/hr</div>
          <div class="time-sub" id="t-target">Target: $125/hr</div>
        </div>
        <div class="badge amber" id="t-badge">Close</div>
      </div>
      <div class="time-note" id="t-note">To hit $125/hr in 1.5 hrs, charge at least $191.</div>
    </div>

    <div class="save-card">
      <div class="slabel">Save this job</div>
      <div class="grid2" style="margin-bottom:12px;">
        <div class="field">
          <label>Customer name</label>
          <input type="text" id="customerName" placeholder="e.g. John Smith">
        </div>
        <div class="field">
          <label>Date</label>
          <input type="date" id="jobDate">
        </div>
      </div>
      <div class="field">
        <label>Notes</label>
        <textarea id="jobNotes" placeholder="e.g. 2-bed cleanout, Downriver, basement carry-out, quick job"></textarea>
      </div>
      <button class="btn-primary" id="saveBtn" onclick="saveJob()">💾 Save to job history</button>
    </div>

    <button class="btn-ghost" onclick="clearJob()">✕ Clear / New Job</button>
    <button class="btn-secondary" id="copyBtn" onclick="copyInvoiceFly()">📋 Copy for Invoice Fly</button>

  </div><!-- end panel-calc -->

  <!-- ═══════════════════════════════════════════════════════════
       QUOTE GENERATOR TAB
  ════════════════════════════════════════════════════════════ -->
  <div class="panel" id="panel-quote">

    <div class="quote-card">
      <div class="slabel">Quote details</div>
      <div class="grid2" style="margin-bottom:12px;">
        <div class="field">
          <label>Customer name</label>
          <input type="text" id="q-name" placeholder="e.g. Lisa">
        </div>
        <div class="field">
          <label>Job address / area</label>
          <input type="text" id="q-address" placeholder="e.g. Flat Rock">
        </div>
      </div>
      <div class="grid2" style="margin-bottom:12px;">
        <div class="field">
          <label>Quote amount ($)</label>
          <input type="number" id="q-price" value="0" inputmode="decimal" oninput="buildQuote()">
        </div>
        <div class="field">
          <label>Load size</label>
          <select id="q-load" onchange="buildQuote()">
            <option value="quarter">Quarter load (~25%)</option>
            <option value="half">Half load (~50%)</option>
            <option value="threequarter">Three-quarter load (~75%)</option>
            <option value="full">Full load (100%)</option>
          </select>
        </div>
      </div>
      <div class="field" style="margin-bottom:12px;">
        <label>Items / description</label>
        <textarea id="q-items" placeholder="e.g. 2 oak display cabinets, miscellaneous furniture" oninput="buildQuote()"></textarea>
      </div>
      <div class="grid2" style="margin-bottom:12px;">
        <div class="field">
          <label>Pickup location</label>
          <select id="q-location" onchange="buildQuote()">
            <option value="garage">Garage</option>
            <option value="basement">Basement (stair carry-out)</option>
            <option value="curbside">Curbside / outside</option>
            <option value="firstfloor">First floor</option>
            <option value="secondfloor">Second floor</option>
            <option value="attic">Attic</option>
          </select>
        </div>
        <div class="field">
          <label>Quote valid for (days)</label>
          <input type="number" id="q-days" value="7" inputmode="numeric" oninput="buildQuote()">
        </div>
      </div>
      <div class="field">
        <label>Additional notes (optional)</label>
        <input type="text" id="q-notes" placeholder="e.g. Kevin will help move to garage first" oninput="buildQuote()">
      </div>
    </div>

    <div class="slabel">Quote preview</div>
    <div class="quote-preview" id="quotePreview">Fill in the fields above to generate your quote.</div>

    <button class="btn-primary" onclick="copyQuote()">📱 Copy quote to send</button>
    <button class="btn-secondary" id="quoteCopyBtn2" onclick="copyQuoteEmail()">📧 Copy as email version</button>

  </div><!-- end panel-quote -->

  <!-- ═══════════════════════════════════════════════════════════
       HISTORY TAB
  ════════════════════════════════════════════════════════════ -->
  <div class="panel" id="panel-history">

    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-lbl">Jobs</div>
        <div class="stat-val" id="s-jobs">0</div>
        <div class="stat-sub">this month</div>
      </div>
      <div class="stat-card">
        <div class="stat-lbl">Revenue</div>
        <div class="stat-val" id="s-revenue">$0</div>
        <div class="stat-sub">total charged</div>
      </div>
      <div class="stat-card">
        <div class="stat-lbl">Profit</div>
        <div class="stat-val" id="s-profit">$0</div>
        <div class="stat-sub">after costs</div>
      </div>
      <div class="stat-card">
        <div class="stat-lbl">Avg margin</div>
        <div class="stat-val" id="s-margin">—</div>
        <div class="stat-sub">profit %</div>
      </div>
    </div>

    <div class="month-row">
      <span style="font-size:12px;color:var(--text2);font-weight:600;">Month:</span>
      <select id="monthFilter" onchange="renderHistory()"></select>
    </div>

    <div class="job-list" id="jobList">
      <div class="empty">
        <div class="empty-icon">📋</div>
        <strong>No jobs yet</strong>
        Save a job from the Calculator tab and it'll show up here.
      </div>
    </div>

  </div><!-- end panel-history -->

</div><!-- end app -->

<script>
// ═══════════════════════════════════════════════════════════════
// AUTH
// ═══════════════════════════════════════════════════════════════
const PW = btoa('Micosanch422!');
const SESSION_KEY = 'sjh_auth';

function doLogin() {
  const val = document.getElementById('loginInput').value;
  if (btoa(val) === PW) {
    sessionStorage.setItem(SESSION_KEY, '1');
    document.getElementById('loginScreen').style.display = 'none';
    document.getElementById('app').style.display = 'block';
    initApp();
  } else {
    document.getElementById('loginErr').textContent = 'Incorrect password. Try again.';
    document.getElementById('loginInput').value = '';
    document.getElementById('loginInput').focus();
  }
}

function doLogout() {
  sessionStorage.removeItem(SESSION_KEY);
  document.getElementById('loginScreen').style.display = 'flex';
  document.getElementById('app').style.display = 'none';
  document.getElementById('loginInput').value = '';
  document.getElementById('loginErr').textContent = '';
}

document.getElementById('loginInput').addEventListener('keydown', e => {
  if (e.key === 'Enter') doLogin();
});

// Check if already logged in this session
if (sessionStorage.getItem(SESSION_KEY) === '1') {
  document.getElementById('loginScreen').style.display = 'none';
  document.getElementById('app').style.display = 'block';
}

// ═══════════════════════════════════════════════════════════════
// THEME
// ═══════════════════════════════════════════════════════════════
function toggleDark() {
  const isDark = document.body.classList.toggle('dark');
  document.body.classList.toggle('light', !isDark);
  document.getElementById('darkBtn').textContent = isDark ? '☀️ Light' : '🌙 Dark';
  localStorage.setItem('sjh_theme', isDark ? 'dark' : 'light');
}

function loadTheme() {
  const t = localStorage.getItem('sjh_theme') || 'light';
  document.body.className = t;
  document.getElementById('darkBtn').textContent = t === 'dark' ? '☀️ Light' : '🌙 Dark';
}

// ═══════════════════════════════════════════════════════════════
// TAYLOR NON-RESIDENT DUMP TIERS
// ═══════════════════════════════════════════════════════════════
const TIERS = [
  { max: 1000,  fee: 60,  label: '0–1,000 lbs' },
  { max: 2000,  fee: 95,  label: '1,001–2,000 lbs' },
  { max: 3000,  fee: 125, label: '2,001–3,000 lbs' },
  { max: 4000,  fee: 155, label: '3,001–4,000 lbs' },
  { max: 5000,  fee: 185, label: '4,001–5,000 lbs' },
  { max: 6000,  fee: 215, label: '5,001–6,000 lbs' },
  { max: 7000,  fee: 245, label: '6,001–7,000 lbs' },
  { max: 8000,  fee: 275, label: '7,001–8,000 lbs' },
  { max: 9000,  fee: 305, label: '8,001–9,000 lbs' },
  { max: 10000, fee: 335, label: '9,001–10,000 lbs' },
];

function lookupDump(lbs) {
  for (const t of TIERS) { if (lbs <= t.max) return t; }
  return TIERS[TIERS.length - 1];
}

// ═══════════════════════════════════════════════════════════════
// STORAGE
// ═══════════════════════════════════════════════════════════════
const JOBS_KEY = 'sjh_jobs_v2';
let jobs = [];

function loadJobs() {
  try {
    const d = localStorage.getItem(JOBS_KEY);
    if (d) jobs = JSON.parse(d);
  } catch(e) { jobs = []; }
}

function saveJobs() {
  try { localStorage.setItem(JOBS_KEY, JSON.stringify(jobs)); } catch(e) {}
}

// ═══════════════════════════════════════════════════════════════
// TABS
// ═══════════════════════════════════════════════════════════════
function switchTab(t) {
  document.querySelectorAll('.tab').forEach(el => el.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(el => el.classList.remove('active'));
  const idx = { calc: 0, quote: 1, history: 2 };
  document.querySelectorAll('.tab')[idx[t]].classList.add('active');
  document.getElementById('panel-' + t).classList.add('active');
  if (t === 'history') { populateMonthFilter(); renderHistory(); }
  if (t === 'quote') buildQuote();
}

// ═══════════════════════════════════════════════════════════════
// LOAD & MATERIAL SELECTORS
// ═══════════════════════════════════════════════════════════════
function selectLoad(el) {
  document.querySelectorAll('.load-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('quotedPrice').value = el.dataset.price;
  calc();
}

function selectMat(el) {
  document.querySelectorAll('.mat-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('weightInput').value = el.dataset.weight;
  onWeightChange();
}

function onWeightChange() {
  const lbs = parseFloat(document.getElementById('weightInput').value) || 0;
  const tier = lookupDump(lbs);
  document.getElementById('dumpFee').value = tier.fee;
  document.getElementById('dumpTag').textContent = `⚡ $${tier.fee} · ${tier.label}`;
  calc();
}

// ═══════════════════════════════════════════════════════════════
// CORE CALCULATION
// ═══════════════════════════════════════════════════════════════
function getVals() {
  const n = id => parseFloat(document.getElementById(id).value) || 0;
  const quoted    = n('quotedPrice');
  const tip       = n('tipAmt');
  const dump      = n('dumpFee');
  const miles     = n('miles');
  const mpg       = n('mpg') || 16;
  const gas       = n('gasPrice') || 3.50;
  const helpers   = n('helpers');
  const helperHrs = n('helperHrs');
  const helperRate= n('helperRate');
  const ins       = n('insurance');
  const yourHrs   = n('yourHrs') || 1;
  const targetRate= n('targetRate') || 125;

  const fuel    = (miles / mpg) * gas;
  const labor   = helpers * helperHrs * helperRate;
  const revenue = quoted + tip;
  const costs   = dump + fuel + labor + ins;
  const profit  = revenue - costs;
  const margin  = revenue > 0 ? Math.round((profit / revenue) * 100) : 0;
  const effRate = yourHrs > 0 ? Math.round(revenue / yourHrs) : 0;
  const minCharge = Math.round((targetRate * yourHrs) + costs);

  return { quoted, tip, dump, fuel, labor, ins, yourHrs, targetRate,
           revenue, costs, profit, margin, effRate, minCharge, miles, mpg, gas };
}

function fmt(n, neg = false) {
  return (neg ? '−$' : '$') + Math.abs(Math.round(n)).toLocaleString();
}

function calc() {
  const v = getVals();

  document.getElementById('r-quoted').textContent = fmt(v.quoted);
  document.getElementById('r-tip').textContent    = fmt(v.tip);
  document.getElementById('r-dump').textContent   = fmt(v.dump, true);
  document.getElementById('r-fuel').textContent   = fmt(v.fuel, true);
  document.getElementById('r-labor').textContent  = fmt(v.labor, true);
  document.getElementById('r-ins').textContent    = fmt(v.ins, true);

  const pe = document.getElementById('r-profit');
  pe.textContent = (v.profit >= 0 ? '$' : '−$') + Math.abs(Math.round(v.profit)).toLocaleString();
  pe.className = 'rt-val ' + (v.profit >= 0 ? 'pos' : 'neg');

  document.getElementById('r-margin-pct').textContent = v.margin + '%';
  const barColor = v.margin >= 40 ? '#1a6600' : v.margin >= 20 ? '#885500' : '#c0392b';
  const bar = document.getElementById('marginBar');
  bar.style.width = Math.max(0, Math.min(100, v.margin)) + '%';
  bar.style.background = barColor;

  document.getElementById('t-rate').textContent   = '$' + v.effRate + '/hr';
  document.getElementById('t-target').textContent = 'Target: $' + v.targetRate + '/hr';

  const badge = document.getElementById('t-badge');
  const note  = document.getElementById('t-note');

  if (v.effRate >= v.targetRate) {
    badge.textContent = '✓ On target'; badge.className = 'badge green';
    note.textContent  = "You're hitting your hourly goal on this job. Great work! 💪";
  } else if (v.effRate >= v.targetRate * 0.75) {
    badge.textContent = 'Close'; badge.className = 'badge amber';
    note.textContent  = `To hit $${v.targetRate}/hr in ${v.yourHrs} hrs, you need to charge at least $${v.minCharge}.`;
  } else {
    badge.textContent = 'Below target'; badge.className = 'badge red';
    note.textContent  = `To hit $${v.targetRate}/hr in ${v.yourHrs} hrs, you need to charge at least $${v.minCharge}.`;
  }
}

// ═══════════════════════════════════════════════════════════════
// SAVE & CLEAR JOB
// ═══════════════════════════════════════════════════════════════
function saveJob() {
  const v        = getVals();
  const customer = document.getElementById('customerName').value.trim() || 'Unnamed customer';
  const date     = document.getElementById('jobDate').value || new Date().toISOString().split('T')[0];
  const notes    = document.getElementById('jobNotes').value.trim();
  const mat      = document.querySelector('.mat-btn.active')?.dataset.type || 'Mixed';
  const size     = document.querySelector('.load-btn.active .lb-name')?.textContent || 'Quarter';
  const weight   = document.getElementById('weightInput').value;

  const job = { id: Date.now(), customer, date, notes, mat, size, weight, ...v };
  jobs.unshift(job);
  saveJobs();

  const btn = document.getElementById('saveBtn');
  btn.textContent = '✓ Saved!';
  btn.style.background = '#1a6600';
  setTimeout(() => { btn.textContent = '💾 Save to job history'; btn.style.background = ''; }, 2000);
  populateMonthFilter();
}

function clearJob() {
  document.getElementById('customerName').value = '';
  document.getElementById('jobNotes').value     = '';
  document.getElementById('quotedPrice').value  = 125;
  document.getElementById('tipAmt').value       = 0;
  document.getElementById('miles').value        = 20;
  document.getElementById('helpers').value      = 0;
  document.getElementById('helperHrs').value    = 2;
  document.getElementById('weightInput').value  = 600;
  document.getElementById('jobDate').value      = new Date().toISOString().split('T')[0];
  document.querySelectorAll('.load-btn').forEach((b, i) => b.classList.toggle('active', i === 0));
  document.querySelectorAll('.mat-btn').forEach((b, i) => b.classList.toggle('active', i === 0));
  onWeightChange();
}

function deleteJob(id) {
  if (!confirm('Delete this job? This cannot be undone.')) return;
  jobs = jobs.filter(j => j.id !== id);
  saveJobs();
  populateMonthFilter();
  renderHistory();
}

// ═══════════════════════════════════════════════════════════════
// COPY FOR INVOICE FLY
// ═══════════════════════════════════════════════════════════════
function copyInvoiceFly() {
  const v        = getVals();
  const mat      = document.querySelector('.mat-btn.active')?.dataset.type || 'Mixed';
  const size     = document.querySelector('.load-btn.active .lb-name')?.textContent || 'Quarter';
  const weight   = document.getElementById('weightInput').value;
  const customer = document.getElementById('customerName').value.trim() || 'Customer';
  const notes    = document.getElementById('jobNotes').value.trim();

  const text = [
    'SANCHEZ JUNK & HAUL CO.',
    `Customer: ${customer}`,
    notes ? `Job: ${notes}` : '',
    `Load: ${size} | Material: ${mat} | Est. ${parseInt(weight).toLocaleString()} lbs`,
    `Charged: $${v.quoted}${v.tip > 0 ? ` + $${v.tip} tip` : ''}`,
    `Dump: $${Math.round(v.dump)} | Fuel: $${Math.round(v.fuel)} | Labor: $${Math.round(v.labor)}`,
    `Net profit: $${Math.round(v.profit)} (${v.margin}% margin)`,
    '—',
    'ESTIMATE DISCLAIMER',
    'Final pricing may vary based on actual volume, weight, and accessibility. Price adjusts if scope changes upon arrival. Payment due upon completion.',
    '—',
    '📞 734-741-3104 | Remove · Refresh · Reclaim'
  ].filter(Boolean).join('\n');

  navigator.clipboard.writeText(text).then(() => {
    const btn = document.getElementById('copyBtn');
    btn.textContent = '✓ Copied!'; btn.classList.add('success');
    setTimeout(() => { btn.textContent = '📋 Copy for Invoice Fly'; btn.classList.remove('success'); }, 2000);
  }).catch(() => {
    alert('Copy failed. Please copy manually.');
  });
}

// ═══════════════════════════════════════════════════════════════
// QUOTE GENERATOR
// ═══════════════════════════════════════════════════════════════
const LOCATION_LABELS = {
  garage:      'garage (ground level)',
  basement:    'basement (stair carry-out)',
  curbside:    'curbside / outside',
  firstfloor:  'first floor',
  secondfloor: 'second floor',
  attic:       'attic'
};

const LOAD_LABELS = {
  quarter:      'quarter load (~25% of trailer)',
  half:         'half load (~50% of trailer)',
  threequarter: 'three-quarter load (~75% of trailer)',
  full:         'full load (trailer at capacity)'
};

function buildQuote() {
  const name     = document.getElementById('q-name').value.trim() || 'Hi';
  const address  = document.getElementById('q-address').value.trim();
  const price    = parseFloat(document.getElementById('q-price').value) || 0;
  const load     = document.getElementById('q-load').value;
  const items    = document.getElementById('q-items').value.trim();
  const location = document.getElementById('q-location').value;
  const days     = parseInt(document.getElementById('q-days').value) || 7;
  const notes    = document.getElementById('q-notes').value.trim();

  const today = new Date();
  const expiry = new Date(today.getTime() + days * 24 * 60 * 60 * 1000);
  const expiryStr = expiry.toLocaleDateString('en-US', { month: 'long', day: 'numeric', year: 'numeric' });

  const greeting = name !== 'Hi' ? `Hi ${name}!` : 'Hi!';
  const addrLine = address ? ` at ${address}` : '';
  const itemLine = items ? `Items: ${items}` : '';
  const noteLine = notes ? `Note: ${notes}` : '';

  const text = [
    `${greeting} This is Mico with Sanchez Junk & Haul Co.`,
    '',
    `Here's your quote for junk removal${addrLine}:`,
    '',
    itemLine,
    `Pickup location: ${LOCATION_LABELS[location]}`,
    `Estimated load: ${LOAD_LABELS[load]}`,
    '',
    `💰 Quote: $${price.toFixed(0)}`,
    `Includes: loading, hauling, and full disposal.`,
    '',
    notes ? `📌 ${noteLine}` : '',
    `This quote is valid until ${expiryStr}.`,
    '',
    'To confirm, just reply to this message or give me a call.',
    '',
    '—',
    'Sanchez Junk & Haul Co.',
    '📞 734-741-3104',
    'Remove · Refresh · Reclaim'
  ].filter(l => l !== undefined && l !== null && !(typeof l === 'string' && l === '' && false)).join('\n');

  // Clean up multiple blank lines
  const clean = text.replace(/\n{3,}/g, '\n\n').trim();
  document.getElementById('quotePreview').textContent = clean;
}

function copyQuote() {
  const text = document.getElementById('quotePreview').textContent;
  if (!text || text === 'Fill in the fields above to generate your quote.') {
    alert('Fill in the quote details first.'); return;
  }
  navigator.clipboard.writeText(text).then(() => {
    const btn = document.querySelector('#panel-quote .btn-primary');
    btn.textContent = '✓ Copied! Ready to text or paste.';
    setTimeout(() => { btn.textContent = '📱 Copy quote to send'; }, 2500);
  }).catch(() => alert('Copy failed.'));
}

function copyQuoteEmail() {
  const name    = document.getElementById('q-name').value.trim() || 'there';
  const price   = parseFloat(document.getElementById('q-price').value) || 0;
  const address = document.getElementById('q-address').value.trim();
  const items   = document.getElementById('q-items').value.trim();
  const location= document.getElementById('q-location').value;
  const load    = document.getElementById('q-load').value;
  const days    = parseInt(document.getElementById('q-days').value) || 7;
  const notes   = document.getElementById('q-notes').value.trim();

  const expiry = new Date(Date.now() + days * 24*60*60*1000);
  const expiryStr = expiry.toLocaleDateString('en-US',{month:'long',day:'numeric',year:'numeric'});

  const subject = `Junk Removal Quote — Sanchez Junk & Haul Co.`;
  const body = [
    `Dear ${name},`,
    '',
    `Thank you for reaching out to Sanchez Junk & Haul Co. Please find your junk removal estimate below.`,
    '',
    '──────────────────────────────',
    'ESTIMATE DETAILS',
    '──────────────────────────────',
    address ? `Location: ${address}` : '',
    items   ? `Items: ${items}` : '',
    `Pickup area: ${LOCATION_LABELS[location]}`,
    `Estimated load: ${LOAD_LABELS[load]}`,
    notes   ? `Additional notes: ${notes}` : '',
    '',
    `TOTAL ESTIMATE: $${price.toFixed(0)}`,
    '(Includes loading, hauling & full disposal)',
    '',
    `This estimate is valid until ${expiryStr}.`,
    '',
    '──────────────────────────────',
    'DISCLAIMER',
    '──────────────────────────────',
    'Final pricing may vary depending on actual volume, weight, accessibility, and any additional items not included in the original quote. Sanchez Junk & Haul Co. reserves the right to adjust the final invoice if the scope of work changes upon arrival. Payment is due upon completion of service.',
    '',
    'To confirm this estimate, please reply to this email or call/text us directly.',
    '',
    'Best regards,',
    'Mico Sanchez',
    'Sanchez Junk & Haul Co.',
    '📞 734-741-3104',
    'Remove · Refresh · Reclaim'
  ].filter(Boolean).join('\n').replace(/\n{3,}/g,'\n\n');

  navigator.clipboard.writeText(`Subject: ${subject}\n\n${body}`).then(() => {
    const btn = document.getElementById('quoteCopyBtn2');
    btn.textContent = '✓ Email version copied!'; btn.classList.add('success');
    setTimeout(() => { btn.textContent = '📧 Copy as email version'; btn.classList.remove('success'); }, 2500);
  }).catch(() => alert('Copy failed.'));
}

// ═══════════════════════════════════════════════════════════════
// HISTORY
// ═══════════════════════════════════════════════════════════════
function populateMonthFilter() {
  const sel  = document.getElementById('monthFilter');
  const now  = new Date().toISOString().substring(0, 7);
  const months = [...new Set(jobs.map(j => j.date.substring(0, 7)))].sort().reverse();
  if (!months.includes(now)) months.unshift(now);
  const cur = sel.value || now;
  sel.innerHTML = months.map(m => {
    const [y, mo] = m.split('-');
    const lbl = new Date(y, mo - 1).toLocaleString('default', { month: 'long', year: 'numeric' });
    return `<option value="${m}"${m === cur ? ' selected' : ''}>${lbl}</option>`;
  }).join('');
}

function renderHistory() {
  const month    = document.getElementById('monthFilter').value;
  const filtered = jobs.filter(j => j.date.startsWith(month));
  const totRev   = filtered.reduce((a, j) => a + (j.revenue  || 0), 0);
  const totProfit= filtered.reduce((a, j) => a + (j.profit   || 0), 0);
  const avgMargin= filtered.length
    ? Math.round(filtered.reduce((a, j) => a + (j.margin || 0), 0) / filtered.length)
    : null;

  document.getElementById('s-jobs').textContent    = filtered.length;
  document.getElementById('s-revenue').textContent = '$' + Math.round(totRev).toLocaleString();
  document.getElementById('s-profit').textContent  = '$' + Math.round(totProfit).toLocaleString();
  document.getElementById('s-margin').textContent  = avgMargin !== null ? avgMargin + '%' : '—';

  const list = document.getElementById('jobList');
  if (!filtered.length) {
    list.innerHTML = `<div class="empty"><div class="empty-icon">📋</div><strong>No jobs this month</strong>Saved jobs will appear here.</div>`;
    return;
  }

  list.innerHTML = filtered.map(j => {
    const pc  = j.margin >= 40 ? 'green' : j.margin >= 20 ? 'amber' : 'red';
    const d   = new Date(j.date + 'T12:00:00');
    const ds  = d.toLocaleDateString('en-US', { month: 'short', day: 'numeric' });
    return `<div class="job-card">
      <div class="job-top">
        <span class="job-name">${escHtml(j.customer)}</span>
        <span class="job-date">${ds}</span>
      </div>
      <div class="job-row">
        <span>${escHtml(j.size)} load · ${escHtml(j.mat)} · ${parseInt(j.weight).toLocaleString()} lbs</span>
      </div>
      <div class="job-row">
        <span class="job-profit ${j.profit >= 0 ? 'pos' : 'neg'}">
          $${Math.round(Math.abs(j.profit)).toLocaleString()} ${j.profit >= 0 ? 'profit' : 'loss'}
        </span>
        <span class="pill ${pc}">${j.margin}% margin</span>
      </div>
      <div class="job-row">
        <span>Charged $${Math.round(j.revenue).toLocaleString()}</span>
        <span>Costs $${Math.round(j.costs).toLocaleString()}</span>
        <span>Your rate: $${j.effRate}/hr</span>
      </div>
      ${j.notes ? `<div class="job-notes">${escHtml(j.notes)}</div>` : ''}
      <div class="job-actions">
        <button class="job-del" onclick="deleteJob(${j.id})">Delete</button>
      </div>
    </div>`;
  }).join('');
}

function escHtml(str) {
  return String(str)
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/"/g, '&quot;');
}

// ═══════════════════════════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════════════════════════
function initApp() {
  loadTheme();
  loadJobs();
  document.getElementById('jobDate').value = new Date().toISOString().split('T')[0];
  onWeightChange();
  populateMonthFilter();
  buildQuote();
}

// Run on page load
loadTheme();
if (sessionStorage.getItem(SESSION_KEY) === '1') {
  initApp();
}
</script>
</body>
</html>
