<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Client Payment Tracker 2026–2031</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:ital,wght@0,400;0,500;1,400&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #080b10;
  --surface: #0f1219;
  --surface2: #161b26;
  --surface3: #1c2233;
  --border: #1a2035;
  --border2: #222b40;
  --text: #dde4f0;
  --text2: #8896b3;
  --muted: #4a5672;
  --accent: #3d8ef5;
  --accent2: #6c4ff0;
  --paid: #23d07a;
  --paid-bg: rgba(35,208,122,.1);
  --paid-border: rgba(35,208,122,.22);
  --pending: #f5a623;
  --pending-bg: rgba(245,166,35,.1);
  --pending-border: rgba(245,166,35,.22);
  --pastdue: #f54040;
  --pastdue-bg: rgba(245,64,64,.1);
  --pastdue-border: rgba(245,64,64,.22);
  --lapsed: #5a6680;
  --lapsed-bg: rgba(90,102,128,.1);
  --lapsed-border: rgba(90,102,128,.22);
  --r: 10px;
}
*{box-sizing:border-box;margin:0;padding:0}
body{background:var(--bg);color:var(--text);font-family:'DM Mono',monospace;min-height:100vh;overflow-x:hidden}
body::before{content:'';position:fixed;inset:0;background-image:radial-gradient(ellipse 80% 50% at 20% -10%,rgba(61,142,245,.06),transparent),radial-gradient(ellipse 60% 40% at 80% 110%,rgba(108,79,240,.05),transparent),linear-gradient(rgba(61,142,245,.018) 1px,transparent 1px),linear-gradient(90deg,rgba(61,142,245,.018) 1px,transparent 1px);background-size:100% 100%,100% 100%,36px 36px,36px 36px;pointer-events:none;z-index:0}
.wrap{max-width:1500px;margin:0 auto;padding:0 28px 80px;position:relative;z-index:1}

header{padding:44px 0 28px;border-bottom:1px solid var(--border);margin-bottom:28px;display:flex;align-items:flex-end;justify-content:space-between;flex-wrap:wrap;gap:16px}
.brand h1{font-family:'Syne',sans-serif;font-size:clamp(20px,3.5vw,34px);font-weight:800;letter-spacing:-.4px;line-height:1}
.brand h1 em{font-style:normal;background:linear-gradient(125deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.brand p{color:var(--muted);font-size:11px;margin-top:8px;text-transform:uppercase;letter-spacing:.1em}
.hdr-right{display:flex;align-items:center;gap:10px;flex-wrap:wrap}
.live-badge{display:flex;align-items:center;gap:6px;background:var(--paid-bg);border:1px solid var(--paid-border);border-radius:20px;padding:5px 12px;font-size:10px;color:var(--paid);letter-spacing:.08em;text-transform:uppercase}
.live-dot{width:6px;height:6px;border-radius:50%;background:var(--paid);animation:blink 2s ease-in-out infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.25}}
.btn{background:var(--surface2);border:1px solid var(--border2);color:var(--text2);padding:8px 15px;border-radius:8px;font-family:'DM Mono',monospace;font-size:11px;cursor:pointer;transition:all .18s;letter-spacing:.05em;text-transform:uppercase}
.btn:hover{border-color:var(--accent);color:var(--accent)}

.stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(145px,1fr));gap:11px;margin-bottom:28px}
.stat{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:18px 20px 14px;position:relative;overflow:hidden;transition:transform .18s}
.stat:hover{transform:translateY(-2px)}
.stat::after{content:'';position:absolute;bottom:0;left:0;right:0;height:2px}
.s-total::after{background:linear-gradient(90deg,var(--accent),var(--accent2))}
.s-paid::after{background:var(--paid)}
.s-pending::after{background:var(--pending)}
.s-pastdue::after{background:var(--pastdue)}
.s-lapsed::after{background:var(--lapsed)}
.s-void::after{background:var(--muted)}
.stat-lbl{font-size:9.5px;text-transform:uppercase;letter-spacing:.1em;color:var(--muted);margin-bottom:10px}
.stat-val{font-family:'Syne',sans-serif;font-size:38px;font-weight:800;line-height:1}
.s-total .stat-val{color:var(--text)}
.s-paid .stat-val{color:var(--paid)}
.s-pending .stat-val{color:var(--pending)}
.s-pastdue .stat-val{color:var(--pastdue)}
.s-lapsed .stat-val{color:var(--lapsed)}
.s-void .stat-val{color:var(--muted)}
.stat-sub{font-size:10px;color:var(--muted);margin-top:6px}

.controls{display:flex;align-items:center;gap:10px;margin-bottom:20px;flex-wrap:wrap}
.tabs{display:flex;background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:3px;gap:2px}
.tab{padding:6px 14px;border-radius:6px;border:none;background:transparent;color:var(--muted);font-family:'DM Mono',monospace;font-size:11px;cursor:pointer;transition:all .18s;letter-spacing:.03em}
.tab.on{background:var(--surface3);color:var(--text);border:1px solid var(--border2)}
.tab:hover:not(.on){color:var(--text)}
.inp{background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:8px 13px;font-family:'DM Mono',monospace;font-size:11px;color:var(--text);outline:none;transition:border-color .18s;cursor:pointer}
.inp:focus{border-color:var(--accent)}
input.inp::placeholder{color:var(--muted)}
input.inp{min-width:190px}

.tbl-wrap{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);overflow:hidden;overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:11.5px}
thead{background:var(--surface2);border-bottom:1px solid var(--border2);position:sticky;top:0;z-index:10}
th{padding:11px 13px;text-align:left;font-size:9.5px;text-transform:uppercase;letter-spacing:.1em;color:var(--muted);white-space:nowrap;font-weight:500;cursor:pointer;user-select:none;transition:color .18s}
th:hover{color:var(--text)}
th.asc::after{content:' ↑';color:var(--accent)}
th.desc::after{content:' ↓';color:var(--accent)}
td{padding:10px 13px;border-bottom:1px solid var(--border);vertical-align:middle}
tr:last-child td{border-bottom:none}
tbody tr:hover td{background:rgba(61,142,245,.025)}

.cn{font-family:'Syne',sans-serif;font-weight:600;font-size:12.5px;color:var(--text);white-space:nowrap}
.cpol{font-size:9.5px;color:var(--muted);margin-top:2px}
.plan-badge{display:inline-block;padding:2px 8px;border-radius:4px;font-size:9px;letter-spacing:.05em;text-transform:uppercase;border:1px solid var(--border2);color:var(--text2);background:var(--surface2);white-space:nowrap}
.pg{border-color:rgba(61,142,245,.3);color:var(--accent);background:rgba(61,142,245,.08)}
.pge{border-color:rgba(108,79,240,.3);color:#a07af5;background:rgba(108,79,240,.08)}
.pc{border-color:rgba(245,166,35,.3);color:var(--pending);background:rgba(245,166,35,.08)}
.freq-badge{display:inline-block;padding:2px 7px;border-radius:4px;font-size:9px;letter-spacing:.04em;text-transform:uppercase;color:var(--muted);background:var(--surface3);border:1px solid var(--border2)}
.pill{display:inline-flex;align-items:center;gap:5px;padding:3px 9px;border-radius:20px;font-size:9.5px;font-weight:500;letter-spacing:.05em;text-transform:uppercase}
.pill-dot{width:5px;height:5px;border-radius:50%;flex-shrink:0}
.pill.active{background:var(--paid-bg);color:var(--paid);border:1px solid var(--paid-border)}
.pill.active .pill-dot{background:var(--paid)}
.pill.void{background:var(--lapsed-bg);color:var(--lapsed);border:1px solid var(--lapsed-border)}
.pill.void .pill-dot{background:var(--lapsed)}
.amt{font-size:12px;color:var(--text)}
.amt-s{font-size:9.5px;color:var(--muted);margin-top:2px}
.comm{font-size:10.5px;color:var(--text2)}

.mrow{display:flex;gap:3px;min-width:220px}
.mc{width:17px;height:17px;border-radius:3px;display:flex;align-items:center;justify-content:center;font-size:7.5px;font-weight:600;position:relative;cursor:default;flex-shrink:0;border:1px solid transparent;transition:transform .12s}
.mc:hover{transform:scale(1.4);z-index:5}
.mc:hover::after{content:attr(data-tip);position:absolute;bottom:calc(100%+5px);left:50%;transform:translateX(-50%);background:var(--surface3);border:1px solid var(--border2);border-radius:5px;padding:3px 7px;font-size:9px;white-space:nowrap;z-index:100;pointer-events:none}
.mc.paid{background:var(--paid-bg);color:var(--paid);border-color:var(--paid-border)}
.mc.pending{background:var(--pending-bg);color:var(--pending);border-color:var(--pending-border)}
.mc.pastdue{background:var(--pastdue-bg);color:var(--pastdue);border-color:var(--pastdue-border)}
.mc.lapsed{background:var(--lapsed-bg);color:var(--lapsed);border-color:var(--lapsed-border)}
.mc.empty{background:var(--surface2);border-color:var(--border);color:var(--muted)}

.sumrow td{background:var(--surface2);border-top:2px solid var(--border2);border-bottom:none!important;font-size:10px;color:var(--muted);padding:10px 13px}
.no-data{text-align:center!important;padding:50px!important;color:var(--muted)!important}
.state-box{text-align:center;padding:70px 24px}
.spinner{width:30px;height:30px;border:2px solid var(--border2);border-top-color:var(--accent);border-radius:50%;animation:spin .75s linear infinite;margin:0 auto 14px}
@keyframes spin{to{transform:rotate(360deg)}}

footer{margin-top:36px;padding-top:18px;border-top:1px solid var(--border);display:flex;justify-content:space-between;align-items:center;color:var(--muted);font-size:10px;text-transform:uppercase;letter-spacing:.08em;flex-wrap:wrap;gap:8px}
footer b{color:var(--text2)}

.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.72);z-index:200;display:none;align-items:center;justify-content:center;backdrop-filter:blur(6px)}
.modal-bg.open{display:flex}
.modal{background:var(--surface);border:1px solid var(--border2);border-radius:14px;padding:32px;max-width:680px;width:92%;max-height:88vh;overflow-y:auto;position:relative;animation:mopen .22s ease}
@keyframes mopen{from{transform:scale(.94);opacity:0}to{transform:scale(1);opacity:1}}
.modal-x{position:absolute;top:16px;right:18px;background:none;border:none;color:var(--muted);font-size:20px;cursor:pointer;transition:color .18s;line-height:1;font-family:monospace}
.modal-x:hover{color:var(--text)}
.modal h2{font-family:'Syne',sans-serif;font-size:20px;font-weight:800;margin-bottom:4px}
.modal-meta{font-size:10.5px;color:var(--muted);margin-bottom:24px;letter-spacing:.04em}
.mgrid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:24px}
.mfield{background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:12px 14px}
.mf-lbl{font-size:9px;text-transform:uppercase;letter-spacing:.1em;color:var(--muted);margin-bottom:5px}
.mf-val{font-size:13px;color:var(--text)}
.ym-title{font-size:9.5px;text-transform:uppercase;letter-spacing:.1em;color:var(--muted);margin-bottom:10px}
.ym-row{display:flex;align-items:center;gap:10px;margin-bottom:6px}
.ym-yr{font-size:10px;color:var(--muted);width:30px;flex-shrink:0}
.ym-cells{display:flex;gap:3px}
.ymc{width:21px;height:21px;border-radius:4px;font-size:8px;display:flex;align-items:center;justify-content:center;border:1px solid transparent;cursor:default;font-weight:600}
.ymc.paid{background:var(--paid-bg);color:var(--paid);border-color:var(--paid-border)}
.ymc.pending{background:var(--pending-bg);color:var(--pending);border-color:var(--pending-border)}
.ymc.pastdue{background:var(--pastdue-bg);color:var(--pastdue);border-color:var(--pastdue-border)}
.ymc.lapsed{background:var(--lapsed-bg);color:var(--lapsed);border-color:var(--lapsed-border)}
.ymc.empty{background:var(--surface3);border-color:var(--border);color:var(--muted)}

/* Month legend below table */
.legend{display:flex;gap:14px;margin-top:14px;flex-wrap:wrap}
.leg{display:flex;align-items:center;gap:5px;font-size:10px;color:var(--muted)}
.leg-dot{width:10px;height:10px;border-radius:2px}

@media(max-width:700px){.mgrid{grid-template-columns:1fr}.controls{flex-direction:column;align-items:stretch}input.inp{min-width:unset}}
</style>
</head>
<body>
<div class="wrap">

<header>
  <div class="brand">
    <h1>📊 <em>Client Payment</em> Tracker</h1>
    <p>Insurance Premium Monitoring &nbsp;·&nbsp; 22 Clients &nbsp;·&nbsp; 2026–2031</p>
  </div>
  <div class="hdr-right">
    <div class="live-badge"><div class="live-dot"></div>Live Data</div>
    <button class="btn" id="syncBtn" onclick="syncSheet()">↻ Sync Sheet</button>
    <button class="btn" onclick="exportCSV()">⬇ Export CSV</button>
  </div>
</header>

<div class="stats">
  <div class="stat s-total"><div class="stat-lbl">Total Clients</div><div class="stat-val">22</div><div class="stat-sub">all policies</div></div>
  <div class="stat s-paid"><div class="stat-lbl">✅ Active</div><div class="stat-val" id="sActive">21</div><div class="stat-sub">policies</div></div>
  <div class="stat s-pending"><div class="stat-lbl">⏳ Pending</div><div class="stat-val" id="sPending">0</div><div class="stat-sub">month payments</div></div>
  <div class="stat s-pastdue"><div class="stat-lbl">🔴 Past Due</div><div class="stat-val" id="sPastdue">0</div><div class="stat-sub">month payments</div></div>
  <div class="stat s-lapsed"><div class="stat-lbl">⬜ Lapsed</div><div class="stat-val" id="sLapsed">0</div><div class="stat-sub">month payments</div></div>
  <div class="stat s-void"><div class="stat-lbl">❌ Void</div><div class="stat-val" id="sVoid">1</div><div class="stat-sub">policies</div></div>
</div>

<div class="controls">
  <div class="tabs" id="yearTabs"></div>
  <input class="inp" type="text" id="searchBox" placeholder="Search name / policy…" oninput="render()">
  <select class="inp" id="planSel" onchange="render()">
    <option value="">All plans</option>
    <option>ST Gregory</option>
    <option>ST George</option>
    <option>St Claire</option>
  </select>
  <select class="inp" id="freqSel" onchange="render()">
    <option value="">All frequencies</option>
    <option>Monthly</option>
    <option>Quarterly</option>
    <option>Annual</option>
  </select>
  <select class="inp" id="statusSel" onchange="render()">
    <option value="">All statuses</option>
    <option>Active</option>
    <option>VOID</option>
  </select>
</div>

<div class="tbl-wrap" id="tblWrap">
  <div class="state-box"><div class="spinner"></div><p style="color:var(--muted)">Loading…</p></div>
</div>

<div class="legend">
  <div class="leg"><div class="leg-dot" style="background:var(--paid-bg);border:1px solid var(--paid-border)"></div><span style="color:var(--paid)">Paid</span></div>
  <div class="leg"><div class="leg-dot" style="background:var(--pending-bg);border:1px solid var(--pending-border)"></div><span style="color:var(--pending)">Pending</span></div>
  <div class="leg"><div class="leg-dot" style="background:var(--pastdue-bg);border:1px solid var(--pastdue-border)"></div><span style="color:var(--pastdue)">Past Due</span></div>
  <div class="leg"><div class="leg-dot" style="background:var(--lapsed-bg);border:1px solid var(--lapsed-border)"></div><span style="color:var(--lapsed)">Lapsed</span></div>
  <div class="leg"><div class="leg-dot" style="background:var(--surface2);border:1px solid var(--border)"></div><span>Not set</span></div>
</div>

<footer>
  <span>Insurance Premium Tracker &nbsp;·&nbsp; Year: <b id="footerYear">2026</b></span>
  <span>Last synced: <b id="lastSync">—</b></span>
</footer>
</div>

<!-- MODAL -->
<div class="modal-bg" id="modalBg" onclick="closeModal(event)">
  <div class="modal" id="modal">
    <button class="modal-x" onclick="closeModal()">✕</button>
    <h2 id="mName"></h2>
    <div class="modal-meta" id="mMeta"></div>
    <div class="mgrid" id="mGrid"></div>
    <div class="ym-title">Payment Timeline — all years</div>
    <div id="mYears"></div>
  </div>
</div>

<script>
const CLIENTS = [
  {id:1,name:'ILAGAN, Kimberly Jane',policy:'L26967488I',plan:'ST Gregory',freq:'Monthly',dob:'Jun 28, 1994',age:31,cost:57000,premium:1100,commission:342,net:758,activated:'Apr 10, 2026',status:'Active'},
  {id:2,name:'BABATID, Mcjohn Velasco',policy:'L26967489I',plan:'ST Gregory',freq:'Monthly',dob:'Nov 17, 1991',age:34,cost:57000,premium:1100,commission:342,net:758,activated:'Apr 10, 2026',status:'Active'},
  {id:3,name:'VERDIDA, Junjun Mabanag',policy:'L26967491I',plan:'ST Gregory',freq:'Monthly',dob:'Sep 14, 1981',age:44,cost:57000,premium:1100,commission:342,net:758,activated:'Apr 10, 2026',status:'Active'},
  {id:4,name:'VERDIDA, Jhayne Marie',policy:'L26967492I',plan:'ST Gregory',freq:'Monthly',dob:'Aug 11, 2007',age:18,cost:57000,premium:1100,commission:342,net:758,activated:'Apr 10, 2026',status:'Active'},
  {id:5,name:'BABATID, Jayann Olivares',policy:'L26967493I',plan:'ST Gregory',freq:'Monthly',dob:'Oct 29, 1986',age:39,cost:57000,premium:1100,commission:342,net:758,activated:'Apr 10, 2026',status:'Active'},
  {id:6,name:'KING, Romie Lloyd Cabrera',policy:'L26967494I',plan:'ST George',freq:'Monthly',dob:'Jul 29, 1991',age:34,cost:53000,premium:1000,commission:318,net:682,activated:'Apr 10, 2026',status:'Active'},
  {id:7,name:'LABUCA, Gerardo',policy:'L26967499I',plan:'ST Gregory',freq:'Monthly',dob:'Jul 3, 1970',age:55,cost:57000,premium:1100,commission:342,net:758,activated:'Apr 10, 2026',status:'Active'},
  {id:8,name:'LABUCA, Sally',policy:'L26967500I',plan:'ST Gregory',freq:'Monthly',dob:'Apr 6, 1970',age:56,cost:57000,premium:1100,commission:342,net:758,activated:'Apr 10, 2026',status:'Active'},
  {id:9,name:'LABUCA, Sage',policy:'L26967497I',plan:'ST Gregory',freq:'Monthly',dob:'Sep 14, 1999',age:26,cost:57000,premium:1100,commission:342,net:758,activated:'Apr 10, 2026',status:'Active'},
  {id:10,name:'CALAGO, Eulie Neil',policy:'L26967496I',plan:'ST George',freq:'Monthly',dob:'Apr 30, 1996',age:30,cost:53000,premium:1000,commission:0,net:0,activated:'Apr 10, 2026',status:'VOID'},
  {id:11,name:'CALAGO, Shiela Mae',policy:'L26967495I',plan:'ST George',freq:'Monthly',dob:'Oct 23, 1988',age:37,cost:53000,premium:1000,commission:318,net:682,activated:'Apr 10, 2026',status:'Active'},
  {id:12,name:'CALAGO, Gemma',policy:'L26967490I',plan:'ST Gregory',freq:'Annual',dob:'Apr 27, 1970',age:56,cost:57000,premium:11400,commission:4104,net:7296,activated:'Apr 10, 2026',status:'Active'},
  {id:13,name:'RIVERA, Erna Patrimonio',policy:'L26967559I',plan:'ST Gregory',freq:'Quarterly',dob:'Oct 29, 1965',age:60,cost:57000,premium:3135,commission:1026,net:2109,activated:'May 8, 2026',status:'Active'},
  {id:14,name:'AMAD, Regine Millor',policy:'L26967553I',plan:'ST Gregory',freq:'Monthly',dob:'May 9, 1996',age:30,cost:57000,premium:1100,commission:342,net:758,activated:'May 8, 2026',status:'Active'},
  {id:15,name:'RIVERA, Joselito Pelayo',policy:'L26967558I',plan:'ST Gregory',freq:'Quarterly',dob:'Aug 27, 1961',age:64,cost:57000,premium:3135,commission:1026,net:2109,activated:'May 8, 2026',status:'Active'},
  {id:16,name:'ENRIQUEZ, Fraulein Anova',policy:'L26967557I',plan:'St Claire',freq:'Quarterly',dob:'Jul 7, 1995',age:30,cost:98500,premium:5420,commission:1773,net:3647,activated:'May 8, 2026',status:'Active'},
  {id:17,name:'CALAGO, Jackie Neil Montaner',policy:'L26967551I',plan:'ST Gregory',freq:'Monthly',dob:'Mar 29, 1999',age:27,cost:57000,premium:1100,commission:342,net:758,activated:'May 8, 2026',status:'Active'},
  {id:18,name:'BABATID, Anita Olivares',policy:'L26967555I',plan:'ST Gregory',freq:'Monthly',dob:'Apr 17, 1967',age:59,cost:57000,premium:1100,commission:342,net:758,activated:'May 8, 2026',status:'Active'},
  {id:19,name:'TAN, Racheal Sheena Suhuri',policy:'L26967552I',plan:'ST Gregory',freq:'Monthly',dob:'Oct 3, 1994',age:31,cost:57000,premium:1100,commission:342,net:758,activated:'May 8, 2026',status:'Active'},
  {id:20,name:'RIVERA, Kith Jhuniel Patrimonio',policy:'L26967556I',plan:'ST Gregory',freq:'Quarterly',dob:'Dec 16, 1990',age:35,cost:98500,premium:5420,commission:1773,net:3647,activated:'May 8, 2026',status:'Active'},
  {id:21,name:'AMAD, Resurrrecion Catira',policy:'L26967560I',plan:'ST Gregory',freq:'Monthly',dob:'Mar 28, 1970',age:56,cost:57000,premium:1100,commission:342,net:758,activated:'May 8, 2026',status:'Active'},
  {id:22,name:'GERALDO, Herbert Sanglitan',policy:'L26967555I',plan:'ST Gregory',freq:'Monthly',dob:'Oct 5, 1998',age:27,cost:57000,premium:1100,commission:342,net:758,activated:'May 8, 2026',status:'Active'},
];

const MONTHS = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
const YEARS  = [2026,2027,2028,2029,2030,2031];
const SHEET_ID = '15mhNWjxg07pEgvwoGkWOnNFt5UEpDhAerV4Q1PUnmQM';

// payments[clientId][year][monthIdx] = 'paid'|'pending'|'pastdue'|'lapsed'|''
let P = {};
CLIENTS.forEach(c => {
  P[c.id] = {};
  YEARS.forEach(y => { P[c.id][y] = Array(12).fill(''); });
});

let activeYear = 2026;
let sortCol = 'id', sortDir = 1;

function buildTabs() {
  document.getElementById('yearTabs').innerHTML = YEARS.map(y =>
    `<button class="tab${y===activeYear?' on':''}" onclick="setYear(${y})">${y}</button>`
  ).join('');
}

function setYear(y) {
  activeYear = y;
  document.getElementById('footerYear').textContent = y;
  buildTabs(); render();
}

function sc(v) {
  if (!v) return 'empty';
  const s = v.toLowerCase().trim();
  if (s==='paid') return 'paid';
  if (s==='pending') return 'pending';
  if (s.includes('past')||s.includes('due')) return 'pastdue';
  if (s==='lapsed') return 'lapsed';
  return 'empty';
}

function planCls(p) {
  const s = (p||'').toLowerCase();
  if (s.includes('gregory')) return 'pg';
  if (s.includes('george'))  return 'pge';
  if (s.includes('claire'))  return 'pc';
  return '';
}

function peso(n) {
  return '₱' + Number(n).toLocaleString('en-PH',{minimumFractionDigits:2,maximumFractionDigits:2});
}

function updateStats() {
  let pending=0, pastdue=0, lapsed=0;
  CLIENTS.forEach(c => {
    (P[c.id]?.[activeYear]||[]).forEach(v => {
      const s = sc(v);
      if (s==='pending') pending++;
      else if (s==='pastdue') pastdue++;
      else if (s==='lapsed') lapsed++;
    });
  });
  document.getElementById('sActive').textContent  = CLIENTS.filter(c=>c.status==='Active').length;
  document.getElementById('sPending').textContent  = pending;
  document.getElementById('sPastdue').textContent  = pastdue;
  document.getElementById('sLapsed').textContent   = lapsed;
  document.getElementById('sVoid').textContent     = CLIENTS.filter(c=>c.status==='VOID').length;
}

function render() {
  updateStats();
  const q  = document.getElementById('searchBox').value.toLowerCase();
  const pF = document.getElementById('planSel').value;
  const fF = document.getElementById('freqSel').value;
  const sF = document.getElementById('statusSel').value;

  let rows = CLIENTS.filter(c =>
    (!q  || c.name.toLowerCase().includes(q) || c.policy.toLowerCase().includes(q)) &&
    (!pF || c.plan === pF) &&
    (!fF || c.freq === fF) &&
    (!sF || c.status === sF)
  );

  rows.sort((a,b) => {
    let va = a[sortCol], vb = b[sortCol];
    if (typeof va==='string') { va=va.toLowerCase(); vb=vb.toLowerCase(); }
    return va<vb ? -sortDir : va>vb ? sortDir : 0;
  });

  if (!rows.length) {
    document.getElementById('tblWrap').innerHTML = `<table><thead><tr>${hdrs()}</tr></thead><tbody><tr><td colspan="9" class="no-data">No clients found</td></tr></tbody></table>`;
    return;
  }

  document.getElementById('tblWrap').innerHTML = `<table>
    <thead><tr>${hdrs()}</tr></thead>
    <tbody>${rows.map(c=>row(c)).join('')}${sumRow(rows)}</tbody>
  </table>`;
}

function hdrs() {
  const cols = [
    ['id','#'],['name','Client Name'],['plan','Plan'],['freq','Freq'],
    ['premium','Premium'],['net','Net Prem.'],['commission','Commission'],['status','Status'],
    ['months','Payments — ' + MONTHS.map(m=>m[0]).join(' ')]
  ];
  return cols.map(([k,l]) => {
    const c = sortCol===k ? (sortDir>0?'asc':'desc') : '';
    return `<th class="${c}" onclick="sort('${k}')">${l}</th>`;
  }).join('');
}

function row(c) {
  const yr = P[c.id]?.[activeYear] || Array(12).fill('');
  const mCells = yr.map((v,i) => {
    const cls = sc(v);
    const lbl = v ? v[0].toUpperCase() : '';
    return `<div class="mc ${cls}" data-tip="${MONTHS[i]}: ${v||'—'}">${lbl}</div>`;
  }).join('');

  const pill = c.status==='VOID'
    ? `<span class="pill void"><span class="pill-dot"></span>Void</span>`
    : `<span class="pill active"><span class="pill-dot"></span>Active</span>`;

  return `<tr onclick="openModal(${c.id})" style="cursor:pointer">
    <td style="color:var(--muted);font-size:10px">${c.id}</td>
    <td><div class="cn">${c.name}</div><div class="cpol">${c.policy}</div></td>
    <td><span class="plan-badge ${planCls(c.plan)}">${c.plan}</span></td>
    <td><span class="freq-badge">${c.freq}</span></td>
    <td><div class="amt">${peso(c.premium)}</div><div class="amt-s">${c.freq}</div></td>
    <td><div class="comm">${peso(c.net)}</div></td>
    <td><div class="comm">${peso(c.commission)}</div></td>
    <td>${pill}</td>
    <td><div class="mrow">${mCells}</div></td>
  </tr>`;
}

function sumRow(rows) {
  const yr = activeYear;
  const counts = Array(12).fill(null).map(()=>({paid:0,pending:0,pastdue:0,lapsed:0}));
  rows.forEach(c => (P[c.id]?.[yr]||[]).forEach((v,i)=>{const s=sc(v);if(s in counts[i])counts[i][s]++;}));
  const mSums = counts.map(m => {
    const p = [];
    if (m.paid)    p.push(`<span style="color:var(--paid)">${m.paid}✓</span>`);
    if (m.pending) p.push(`<span style="color:var(--pending)">${m.pending}⏳</span>`);
    if (m.pastdue) p.push(`<span style="color:var(--pastdue)">${m.pastdue}!</span>`);
    if (m.lapsed)  p.push(`<span style="color:var(--lapsed)">${m.lapsed}⬜</span>`);
    return `<div style="display:inline-flex;flex-direction:column;align-items:center;gap:1px;width:19px;font-size:7.5px">${p.join('')||'<span>—</span>'}</div>`;
  }).join('');
  const totP = rows.filter(r=>r.status!=='VOID').reduce((a,c)=>a+c.premium,0);
  const totN = rows.filter(r=>r.status!=='VOID').reduce((a,c)=>a+c.net,0);
  const totC = rows.filter(r=>r.status!=='VOID').reduce((a,c)=>a+c.commission,0);
  return `<tr class="sumrow">
    <td>—</td>
    <td style="font-family:'Syne',sans-serif;font-weight:700;color:var(--text2)">TOTAL (${rows.length} clients)</td>
    <td></td><td></td>
    <td style="color:var(--text2)">${peso(totP)}</td>
    <td style="color:var(--text2)">${peso(totN)}</td>
    <td style="color:var(--text2)">${peso(totC)}</td>
    <td></td>
    <td><div style="display:flex;gap:3px">${mSums}</div></td>
  </tr>`;
}

function sort(col) {
  sortCol===col ? sortDir*=-1 : (sortCol=col,sortDir=1);
  render();
}

// ── MODAL ──
function openModal(id) {
  const c = CLIENTS.find(x=>x.id===id);
  if (!c) return;
  document.getElementById('mName').textContent = c.name;
  document.getElementById('mMeta').textContent = `${c.policy} · ${c.plan} · ${c.freq} · Activated ${c.activated}`;
  document.getElementById('mGrid').innerHTML = [
    ['Date of Birth',c.dob], ['Age',c.age+' yrs'],
    ['Policy Cost',peso(c.cost)], ['Premium',peso(c.premium)+' / '+c.freq],
    ['Net Premium',peso(c.net)], ['Commission',peso(c.commission)],
    ['Status',c.status], ['Activated',c.activated],
  ].map(([l,v])=>`<div class="mfield"><div class="mf-lbl">${l}</div><div class="mf-val">${v}</div></div>`).join('');
  document.getElementById('mYears').innerHTML = YEARS.map(y => {
    const yr = P[c.id]?.[y]||Array(12).fill('');
    const cells = yr.map((v,i)=>`<div class="ymc ${sc(v)}" title="${MONTHS[i]}: ${v||'—'}">${MONTHS[i][0]}</div>`).join('');
    return `<div class="ym-row"><div class="ym-yr">${y}</div><div class="ym-cells">${cells}</div></div>`;
  }).join('');
  document.getElementById('modalBg').classList.add('open');
}

function closeModal(e) {
  if (!e || e.target===document.getElementById('modalBg'))
    document.getElementById('modalBg').classList.remove('open');
}

// ── SYNC FROM GOOGLE SHEET ──
async function syncSheet() {
  const btn = document.getElementById('syncBtn');
  const orig = btn.textContent;
  btn.textContent = '↻ Syncing…'; btn.style.color = 'var(--accent)';
  try {
    for (const year of YEARS) {
      const url = `https://docs.google.com/spreadsheets/d/${SHEET_ID}/gviz/tq?tqx=out:json&sheet=${year}`;
      const res = await fetch(url);
      const txt = await res.text();
      const m = txt.match(/google\.visualization\.Query\.setResponse\(([\s\S]*?)\);\s*$/);
      if (!m) continue;
      const gviz = JSON.parse(m[1]);
      const rows = gviz.table?.rows || [];
      rows.forEach(row => {
        if (!row.c) return;
        const nameCel = row.c[1]?.v || row.c[0]?.v || '';
        const nameStr = String(nameCel).trim().toUpperCase();
        const client = CLIENTS.find(c => {
          const parts = c.name.toUpperCase().split(',');
          return nameStr.includes(parts[0].trim()) || c.name.toUpperCase() === nameStr;
        });
        if (!client) return;
        MONTHS.forEach((mn, mi) => {
          const cell = row.c[mi + 2];
          if (cell && cell.v !== null && cell.v !== undefined) {
            const val = String(cell.v).trim().toLowerCase();
            if (['paid','pending','past due','pastdue','lapsed'].some(s=>val.includes(s.replace(' ','')||s))) {
              if (!P[client.id]) P[client.id] = {};
              if (!P[client.id][year]) P[client.id][year] = Array(12).fill('');
              P[client.id][year][mi] = val.includes('past')||val.includes('due') ? 'pastdue' : val;
            }
          }
        });
      });
    }
    document.getElementById('lastSync').textContent = new Date().toLocaleString('en-PH');
    btn.textContent = '✓ Synced'; btn.style.color = 'var(--paid)';
    setTimeout(() => { btn.textContent = orig; btn.style.color = ''; }, 2500);
    render();
  } catch(err) {
    btn.textContent = '⚠ Sheet Offline'; btn.style.color = 'var(--pending)';
    setTimeout(() => { btn.textContent = orig; btn.style.color = ''; }, 3000);
    toast('Make sure the Google Sheet is set to <b>"Anyone with the link → Viewer"</b> to enable live sync.', 'var(--pending-border)');
  }
}

function toast(msg, border='var(--border2)') {
  const el = document.createElement('div');
  el.style = `position:fixed;bottom:24px;right:24px;background:var(--surface2);border:1px solid ${border};color:var(--text2);border-radius:10px;padding:14px 18px;font-size:11.5px;max-width:340px;z-index:999;line-height:1.5`;
  el.innerHTML = msg;
  document.body.appendChild(el);
  setTimeout(() => el.remove(), 6000);
}

function exportCSV() {
  const yr = activeYear;
  const hdr = ['#','Name','Policy','Plan','Freq','DOB','Age','Cost','Premium','Net','Commission','Status',...MONTHS.map(m=>m+' '+yr)];
  const body = CLIENTS.map(c => {
    const mths = (P[c.id]?.[yr]||Array(12).fill('')).map(v=>v||'');
    return [c.id,`"${c.name}"`,c.policy,c.plan,c.freq,`"${c.dob}"`,c.age,c.cost,c.premium,c.net,c.commission,c.status,...mths].join(',');
  });
  const blob = new Blob([[hdr.join(','),...body].join('\n')], {type:'text/csv'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = `payment-tracker-${yr}.csv`;
  a.click();
}

document.addEventListener('keydown', e => { if (e.key==='Escape') closeModal(); });

// Init
buildTabs();
render();
document.getElementById('lastSync').textContent = new Date().toLocaleString('en-PH');
setTimeout(syncSheet, 1000);
</script>
</body>
</html>
