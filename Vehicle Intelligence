main.py
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vehicle Inventory Intelligence</title>
    <style>
        :root {
            --bg: #0f172a;
            --card: #1e293b;
            --border: #334155;
            --text: #e2e8f0;
            --muted: #94a3b8;
            --red: #ef4444;
            --green: #22c55e;
            --yellow: #eab308;
            --blue: #3b82f6;
            --accent: #e94560;
        }
        * { margin:0; padding:0; box-sizing:border-box; }
        body { font-family: system-ui, -apple-system, sans-serif; background:var(--bg); color:var(--text); line-height:1.6; }

        /* Layout */
        .header { background:var(--card); border-bottom:2px solid var(--accent); padding:16px 24px; display:flex; justify-content:space-between; align-items:center; position:sticky; top:0; z-index:50; }
        .header h1 { font-size:18px; }
        .header span { color:var(--muted); font-size:12px; text-transform:uppercase; letter-spacing:2px; }
        .container { max-width:1200px; margin:0 auto; padding:24px; }

        /* Buttons */
        .btn { padding:12px 28px; border:none; border-radius:8px; font-size:14px; font-weight:700; cursor:pointer; font-family:inherit; transition:all .2s; }
        .btn-primary { background:var(--accent); color:#fff; }
        .btn-primary:hover { opacity:.9; transform:translateY(-1px); }
        .btn-outline { background:transparent; color:var(--text); border:1px solid var(--border); }
        .btn-outline:hover { border-color:var(--muted); }
        .btn-green { background:rgba(34,197,94,.15); color:var(--green); border:1px solid rgba(34,197,94,.3); }
        .btn-bar { display:flex; gap:12px; justify-content:center; margin:24px 0; flex-wrap:wrap; }

        /* Form */
        .grid2 { display:grid; grid-template-columns:1fr 1fr; gap:20px; }
        .card { background:var(--card); border:1px solid var(--border); border-radius:12px; padding:24px; margin-bottom:20px; }
        .card h3 { font-size:15px; margin-bottom:16px; padding-bottom:12px; border-bottom:1px solid var(--border); display:flex; align-items:center; gap:10px; }
        .fields { display:grid; grid-template-columns:1fr 1fr; gap:12px; }
        .field { display:flex; flex-direction:column; gap:4px; }
        .field.full { grid-column:1/-1; }
        .field label { font-size:11px; font-weight:600; color:var(--muted); text-transform:uppercase; letter-spacing:.5px; }
        .field input, .field select, .field textarea {
            padding:10px 14px; background:#0f172a; border:1px solid var(--border); border-radius:8px;
            color:var(--text); font-size:14px; font-family:inherit; outline:none; transition:border .2s;
        }
        .field input:focus, .field select:focus, .field textarea:focus { border-color:var(--accent); }
        .field textarea { resize:vertical; min-height:60px; }
        .field select { appearance:none; cursor:pointer; }

        /* Report */
        #report { display:none; }
        #report.show { display:block; }
        .kpis { display:grid; grid-template-columns:repeat(4,1fr); gap:12px; margin-bottom:20px; }
        .kpi { background:var(--card); border:1px solid var(--border); border-radius:10px; padding:16px; text-align:center; }
        .kpi .label { font-size:11px; text-transform:uppercase; color:var(--muted); letter-spacing:1px; }
        .kpi .value { font-size:24px; font-weight:700; margin:4px 0; }
        .kpi .sub { font-size:11px; color:var(--muted); }
        .green { color:var(--green); }
        .red { color:var(--red); }
        .yellow { color:var(--yellow); }
        .blue { color:var(--blue); }

        .section { background:var(--card); border:1px solid var(--border); border-radius:12px; margin-bottom:20px; overflow:hidden; }
        .section-head { padding:20px 24px; border-bottom:1px solid var(--border); display:flex; align-items:center; gap:12px; }
        .section-num { width:32px; height:32px; background:linear-gradient(135deg,var(--accent),var(--blue)); border-radius:8px; display:flex; align-items:center; justify-content:center; font-weight:700; font-size:14px; flex-shrink:0; }
        .section-title { font-size:16px; font-weight:700; }
        .section-body { padding:24px; }
        .section-body p { font-size:14px; color:var(--muted); margin-bottom:10px; }
        .section-body strong { color:var(--text); }

        /* Probability bars */
        .prob { display:flex; align-items:center; gap:12px; margin:10px 0; }
        .prob-label { width:80px; font-size:13px; font-weight:600; }
        .prob-track { flex:1; height:26px; background:#0f172a; border-radius:6px; overflow:hidden; }
        .prob-fill { height:100%; border-radius:6px; display:flex; align-items:center; padding-left:10px; font-size:12px; font-weight:700; transition:width 1s ease; }

        /* Table */
        table { width:100%; border-collapse:collapse; margin:12px 0; font-size:13px; }
        th { background:#0f172a; padding:10px 12px; text-align:left; font-size:11px; text-transform:uppercase; color:var(--muted); letter-spacing:.5px; }
        td { padding:10px 12px; border-bottom:1px solid var(--border); }

        /* Callout */
        .callout { padding:16px 20px; border-radius:10px; margin:14px 0; border-left:4px solid; }
        .callout-red { background:rgba(239,68,68,.08); border-color:var(--red); }
        .callout-green { background:rgba(34,197,94,.08); border-color:var(--green); }
        .callout-blue { background:rgba(59,130,246,.08); border-color:var(--blue); }
        .callout-yellow { background:rgba(234,179,8,.08); border-color:var(--yellow); }
        .callout h4 { font-size:13px; text-transform:uppercase; letter-spacing:.5px; margin-bottom:6px; }
        .callout p, .callout li { font-size:13px; color:var(--muted); }
        .callout ul { margin:6px 0 0 18px; }

        /* Recommendation box */
        .rec-box { background:#0f172a; border:2px solid var(--accent); border-radius:10px; padding:20px; text-align:center; margin:16px 0; }
        .rec-box .action { font-size:22px; font-weight:700; color:var(--accent); }
        .rec-box .detail { font-size:15px; margin-top:4px; }
        .rec-box .sub { font-size:12px; color:var(--muted); margin-top:6px; }

        /* Exit cards */
        .exit-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:12px; margin:14px 0; }
        .exit-card { background:#0f172a; border:1px solid var(--border); border-radius:10px; padding:16px; text-align:center; }
        .exit-card.best { border-color:var(--green); box-shadow:0 0 15px rgba(34,197,94,.1); }
        .exit-card h4 { font-size:12px; text-transform:uppercase; letter-spacing:1px; color:var(--muted); margin-bottom:8px; }
        .exit-card .g { font-size:20px; font-weight:700; }
        .exit-card .t { font-size:12px; color:var(--muted); margin-top:4px; }
        .best-label { display:inline-block; background:var(--green); color:#000; padding:2px 8px; border-radius:4px; font-size:10px; font-weight:700; text-transform:uppercase; margin-bottom:6px; }

        /* Action items */
        .action-item { background:#0f172a; border:1px solid var(--border); border-radius:10px; padding:16px 20px; margin:10px 0; display:flex; gap:14px; }
        .action-item .num { width:28px; height:28px; background:linear-gradient(135deg,var(--accent),var(--blue)); border-radius:6px; display:flex; align-items:center; justify-content:center; font-weight:700; font-size:13px; flex-shrink:0; }
        .action-item h4 { font-size:14px; margin-bottom:4px; }
        .action-item p { font-size:12px; color:var(--muted); }
        .timing-badge { display:inline-block; padding:2px 8px; background:rgba(233,69,96,.15); color:var(--accent); border-radius:4px; font-size:10px; font-weight:600; text-transform:uppercase; margin-bottom:6px; }

        /* Confidence */
        .conf-bar { display:flex; align-items:center; gap:12px; margin:12px 0; }
        .conf-track { flex:1; height:8px; background:#0f172a; border-radius:4px; overflow:hidden; }
        .conf-fill { height:100%; border-radius:4px; }

        /* Badge */
        .badge { display:inline-block; padding:3px 10px; border-radius:12px; font-size:11px; font-weight:600; }
        .badge-green { background:rgba(34,197,94,.15); color:var(--green); }
        .badge-yellow { background:rgba(234,179,8,.15); color:var(--yellow); }
        .badge-red { background:rgba(239,68,68,.15); color:var(--red); }

        /* Responsive */
        @media(max-width:900px) { .grid2,.fields,.exit-grid { grid-template-columns:1fr; } .kpis { grid-template-columns:1fr 1fr; } }
        @media(max-width:600px) { .kpis { grid-template-columns:1fr; } .container { padding:12px; } }
        @media print {
            .header,.btn-bar,#form { display:none!important; }
            body { background:#fff; color:#000; }
            .card,.section,.kpi,.callout,.action-item,.exit-card,.rec-box { background:#fff; border-color:#ddd; }
            .section-body p,.callout p,.callout li,.action-item p,.kpi .sub { color:#333; }
        }

        /* Loading */
        .loading { display:none; position:fixed; inset:0; background:rgba(15,23,42,.95); z-index:100; justify-content:center; align-items:center; flex-direction:column; gap:16px; }
        .loading.show { display:flex; }
        .spinner { width:48px; height:48px; border:4px solid var(--border); border-top-color:var(--accent); border-radius:50%; animation:spin .8s linear infinite; }
        @keyframes spin { to { transform:rotate(360deg); } }

        /* Saved vehicles */
        .saved-list { margin:20px 0; }
        .saved-item { background:var(--card); border:1px solid var(--border); border-radius:8px; padding:14px 20px; margin:8px 0; display:flex; justify-content:space-between; align-items:center; cursor:pointer; transition:border .2s; }
        .saved-item:hover { border-color:var(--accent); }
        .saved-item .info { font-weight:600; }
        .saved-item .meta { font-size:12px; color:var(--muted); }
        .saved-item .actions { display:flex; gap:8px; }
        .saved-item .actions button { padding:6px 14px; font-size:12px; }
    </style>
</head>
<body>

<div class="header">
    <div>
        <h1>🚗 Vehicle Inventory Intelligence</h1>
        <span>Dealership Analytics Platform</span>
    </div>
    <div style="display:flex;gap:8px;">
        <button class="btn btn-outline" onclick="showForm()" id="btnForm">New Analysis</button>
        <button class="btn btn-outline" onclick="showSaved()" id="btnSaved">Saved (0)</button>
        <button class="btn btn-outline" onclick="window.print()">Print</button>
    </div>
</div>

<div class="loading" id="loading">
    <div class="spinner"></div>
    <div style="color:var(--muted);">Generating Intelligence Report...</div>
</div>

<div class="container">

<!-- FORM -->
<div id="form">
    <div class="btn-bar" style="margin-top:0;">
        <button class="btn btn-green" onclick="loadSample()">▶ Load Sample (2021 Camry SE)</button>
        <button class="btn btn-outline" onclick="clearForm()">Clear</button>
    </div>

    <div class="grid2">
        <!-- Vehicle Details -->
        <div class="card">
            <h3>🚗 Vehicle Details</h3>
            <div class="fields">
                <div class="field"><label>Year</label><input type="number" id="year" placeholder="2021"></div>
                <div class="field"><label>Make</label><input id="make" placeholder="Toyota"></div>
                <div class="field"><label>Model</label><input id="model" placeholder="Camry"></div>
                <div class="field"><label>Trim</label><input id="trim" placeholder="SE"></div>
                <div class="field"><label>Mileage</label><input type="number" id="mileage" placeholder="41850"></div>
                <div class="field"><label>Ext / Int Color</label><input id="color" placeholder="White / Black"></div>
                <div class="field full"><label>Equipment / Packages</label><textarea id="equipment" placeholder="SE Convenience Package, BSM, Apple CarPlay..."></textarea></div>
            </div>
        </div>

        <!-- Financial -->
        <div class="card">
            <h3>💰 Financial Data</h3>
            <div class="fields">
                <div class="field"><label>Acquisition Cost</label><input type="number" id="acqCost" placeholder="19400"></div>
                <div class="field"><label>Recon Cost</label><input type="number" id="reconCost" placeholder="850"></div>
                <div class="field"><label>Current List Price</label><input type="number" id="listPrice" placeholder="23495"></div>
                <div class="field"><label>Floorplan Rate %</label><input type="number" id="fpRate" placeholder="7.25" step="0.25"></div>
                <div class="field"><label>Wholesale Exit Price</label><input type="number" id="wholesalePrice" placeholder="20300"></div>
                <div class="field"><label>Min Acceptable Gross</label><input type="number" id="minGross" placeholder="2000"></div>
            </div>
        </div>

        <!-- Inventory -->
        <div class="card">
            <h3>📊 Inventory Status</h3>
            <div class="fields">
                <div class="field"><label>Days in Inventory</label><input type="number" id="daysInv" placeholder="52"></div>
                <div class="field"><label>Price Changes to Date</label><input type="number" id="priceChanges" placeholder="1"></div>
                <div class="field full"><label>Days Since Last Price Change</label><input type="number" id="daysSinceChange" placeholder="18"></div>
            </div>
        </div>

        <!-- Market -->
        <div class="card">
            <h3>🌐 Market Context</h3>
            <div class="fields">
                <div class="field"><label>Comp Low</label><input type="number" id="compLow" placeholder="22300"></div>
                <div class="field"><label>Comp High</label><input type="number" id="compHigh" placeholder="23900"></div>
                <div class="field"><label>Competing Units</label><input type="number" id="compUnits" placeholder="17"></div>
                <div class="field"><label>Demand Signal</label>
                    <select id="demand"><option value="moderate">Moderate</option><option value="high">High</option><option value="soft">Soft</option></select>
                </div>
                <div class="field full"><label>Seasonal Notes</label><textarea id="seasonal" placeholder="Any timing factors..."></textarea></div>
            </div>
        </div>
    </div>

    <!-- Activity Signals -->
    <div class="card">
        <h3>📡 Dealer Activity Signals</h3>
        <div class="fields" style="grid-template-columns:repeat(3,1fr);">
            <div class="field"><label>Views (7d)</label><input type="number" id="v7" placeholder="28"></div>
            <div class="field"><label>Views (30d)</label><input type="number" id="v30" placeholder="134"></div>
            <div class="field"><label>Leads (7d)</label><input type="number" id="l7" placeholder="3"></div>
            <div class="field"><label>Leads (30d)</label><input type="number" id="l30" placeholder="11"></div>
            <div class="field"><label>Test Drives (7d)</label><input type="number" id="td7" placeholder="1"></div>
            <div class="field"><label>Test Drives (30d)</label><input type="number" id="td30" placeholder="4"></div>
            <div class="field full"><label>Sales Notes / Objections</label><textarea id="notes" placeholder="Price resistance vs newer models..."></textarea></div>
        </div>
    </div>

    <div class="btn-bar">
        <button class="btn btn-primary" onclick="generate()" style="padding:16px 48px;font-size:16px;">⚡ Generate Intelligence Report</button>
    </div>
</div>

<!-- SAVED VEHICLES -->
<div id="savedPanel" style="display:none;">
    <h2 style="margin-bottom:12px;">Saved Vehicles</h2>
    <p style="color:var(--muted);font-size:13px;margin-bottom:16px;">Click any vehicle to load it into the form. Data is stored in your browser.</p>
    <div id="savedList" class="saved-list"></div>
    <div class="btn-bar"><button class="btn btn-outline" onclick="showForm()">← Back to Form</button></div>
</div>

<!-- REPORT -->
<div id="report"></div>

</div>

<script>
// ============================================================
// STORAGE (localStorage — no backend needed)
// ============================================================
function getSaved() { return JSON.parse(localStorage.getItem('vi_vehicles') || '[]'); }
function setSaved(arr) { localStorage.setItem('vi_vehicles', JSON.stringify(arr)); updateSavedCount(); }
function updateSavedCount() { document.getElementById('btnSaved').textContent = `Saved (${getSaved().length})`; }
updateSavedCount();

// ============================================================
// FORM HELPERS
// ============================================================
const $ = id => document.getElementById(id);
const val = id => $(id).value.trim();
const num = id => parseFloat($(id).value) || 0;

function loadSample() {
    $('year').value='2021'; $('make').value='Toyota'; $('model').value='Camry'; $('trim').value='SE';
    $('mileage').value='41850'; $('color').value='White / Black';
    $('equipment').value='SE Convenience Package, Blind Spot Monitor, Power Driver Seat, Apple CarPlay';
    $('acqCost').value='19400'; $('reconCost').value='850'; $('listPrice').value='23495';
    $('fpRate').value='7.25'; $('wholesalePrice').value='20300'; $('minGross').value='2000';
    $('daysInv').value='52'; $('priceChanges').value='1'; $('daysSinceChange').value='18';
    $('compLow').value='22300'; $('compHigh').value='23900'; $('compUnits').value='17';
    $('demand').value='moderate'; $('seasonal').value='Neutral; steady year-round demand, mild compression from newer model incentives';
    $('v7').value='28'; $('v30').value='134'; $('l7').value='3'; $('l30').value='11';
    $('td7').value='1'; $('td30').value='4'; $('notes').value='Price resistance versus newer 2023 models; customers asking for $500–$1,000 flexibility';
}

function clearForm() {
    document.querySelectorAll('#form input, #form textarea, #form select').forEach(el => {
        if(el.tagName==='SELECT') el.selectedIndex=0; else el.value='';
    });
}

function collectData() {
    return {
        year:val('year'), make:val('make'), model:val('model'), trim:val('trim'),
        mileage:num('mileage'), color:val('color'), equipment:val('equipment'),
        acqCost:num('acqCost'), reconCost:num('reconCost'), listPrice:num('listPrice'),
        fpRate:num('fpRate'), wholesalePrice:num('wholesalePrice'), minGross:num('minGross'),
        daysInv:num('daysInv'), priceChanges:num('priceChanges'), daysSinceChange:num('daysSinceChange'),
        compLow:num('compLow'), compHigh:num('compHigh'), compUnits:num('compUnits'),
        demand:val('demand'), seasonal:val('seasonal'),
        v7:num('v7'), v30:num('v30'), l7:num('l7'), l30:num('l30'),
        td7:num('td7'), td30:num('td30'), notes:val('notes')
    };
}

function loadData(d) {
    $('year').value=d.year; $('make').value=d.make; $('model').value=d.model; $('trim').value=d.trim;
    $('mileage').value=d.mileage; $('color').value=d.color; $('equipment').value=d.equipment;
    $('acqCost').value=d.acqCost; $('reconCost').value=d.reconCost; $('listPrice').value=d.listPrice;
    $('fpRate').value=d.fpRate; $('wholesalePrice').value=d.wholesalePrice; $('minGross').value=d.minGross;
    $('daysInv').value=d.daysInv; $('priceChanges').value=d.priceChanges; $('daysSinceChange').value=d.daysSinceChange;
    $('compLow').value=d.compLow; $('compHigh').value=d.compHigh; $('compUnits').value=d.compUnits;
    $('demand').value=d.demand; $('seasonal').value=d.seasonal;
    $('v7').value=d.v7; $('v30').value=d.v30; $('l7').value=d.l7; $('l30').value=d.l30;
    $('td7').value=d.td7; $('td30').value=d.td30; $('notes').value=d.notes;
}

// ============================================================
// NAVIGATION
// ============================================================
function showForm() {
    $('form').style.display='block'; $('report').className=''; $('savedPanel').style.display='none';
    window.scrollTo({top:0,behavior:'smooth'});
}
function showSaved() {
    $('form').style.display='none'; $('report').className=''; $('savedPanel').style.display='block';
    renderSavedList();
    window.scrollTo({top:0,behavior:'smooth'});
}

function renderSavedList() {
    const list = getSaved();
    if(list.length===0) {
        $('savedList').innerHTML = '<p style="color:var(--muted);text-align:center;padding:40px;">No saved vehicles yet. Generate a report and it auto-saves.</p>';
        return;
    }
    $('savedList').innerHTML = list.map((v,i) => `
        <div class="saved-item">
            <div>
                <div class="info">${v.year} ${v.make} ${v.model} ${v.trim}</div>
                <div class="meta">${v.mileage.toLocaleString()} mi · ${v.color} · ${v.daysInv} days · $${v.listPrice.toLocaleString()}</div>
            </div>
            <div class="actions">
                <button class="btn btn-outline" onclick="loadVehicle(${i})">Load</button>
                <button class="btn btn-outline" style="color:var(--red);border-color:var(--red);" onclick="deleteVehicle(${i})">✕</button>
            </div>
        </div>
    `).join('');
}

function loadVehicle(i) {
    loadData(getSaved()[i]);
    showForm();
}
function deleteVehicle(i) {
    const list = getSaved(); list.splice(i,1); setSaved(list); renderSavedList();
}

// ============================================================
// ANALYSIS ENGINE
// ============================================================
function analyze(d) {
    const a = {};

    // Financials
    a.invested = d.acqCost + d.reconCost;
    a.gross = d.listPrice - a.invested;
    a.dailyFP = (a.invested * (d.fpRate/100)) / 365;
    a.fpAccrued = a.dailyFP * d.daysInv;
    a.netGross = a.gross - a.fpAccrued;
    a.whNet = d.wholesalePrice - a.invested - a.fpAccrued;

    // Market
    const range = d.compHigh - d.compLow;
    a.mktPos = range > 0 ? (d.listPrice - d.compLow) / range : 0.5;
    a.mktLabel = a.mktPos>.75?'Top Quartile — Overpriced Risk':a.mktPos>.5?'Above Mid-Market':a.mktPos>.25?'Mid-Market':'Value Position';

    // Engagement
    const avgWeekly = d.v30/4.3;
    a.viewTrend = avgWeekly>0 ? ((d.v7-avgWeekly)/avgWeekly*100) : 0;
    a.viewTrendLabel = a.viewTrend>10?'Accelerating':a.viewTrend>-10?'Stable':'Declining';
    a.l2v = d.v30>0?(d.l30/d.v30*100):0;
    a.td2l = d.l30>0?(d.td30/d.l30*100):0;
    a.engScore = d.l7*3 + d.td7*10 + d.v7*0.2;

    // Probability model
    const dm = d.demand==='high'?1.2:d.demand==='soft'?0.75:1.0;
    const cf = d.compUnits<=5?1.3:d.compUnits<=10?1.1:d.compUnits<=20?0.9:0.7;
    const af = d.daysInv<=20?1.2:d.daysInv<=40?1.0:d.daysInv<=60?0.85:d.daysInv<=90?0.65:0.45;
    const ef = a.engScore>25?1.2:a.engScore>12?1.0:a.engScore>5?0.8:0.6;
    const pf = a.mktPos>.8?.7:a.mktPos>.6?.85:a.mktPos>.4?1.0:a.mktPos>.2?1.15:1.25;

    const clamp = (v,lo,hi) => Math.max(lo,Math.min(hi,v));
    a.p30 = clamp(.35*dm*cf*af*ef*pf,.05,.95);
    a.p60 = clamp(.55*dm*cf*(af*1.1)*ef*pf,.10,.97);
    a.p90 = clamp(.72*dm*cf*(af*1.15)*ef*pf,.20,.98);

    // Aging
    a.zone = d.daysInv<=30?'HEALTHY':d.daysInv<=60?'AT-RISK':'DANGER';

    // Erosion table
    a.erosion = [0,30,60,90].map(add => {
        const tot = d.daysInv + add;
        const fp = a.dailyFP * tot;
        const gs = a.gross - fp;
        return { add, tot, fp, gs, rLow: gs-1000, rHigh: gs-500 };
    });

    // Irrationality day
    a.irrDay = d.daysInv;
    for(let day=d.daysInv; day<=d.daysInv+150; day++) {
        const fp = a.dailyFP*day;
        const ret = (a.gross-fp)-750;
        const pr = clamp(a.p30*Math.pow(.98,day-d.daysInv),.05,.95);
        if(ret*pr < Math.max(d.wholesalePrice-a.invested-fp, a.whNet) || ret<0) { a.irrDay=day; break; }
        a.irrDay=day;
    }
    a.daysLeft = Math.max(0, a.irrDay - d.daysInv);

    // Pricing
    const optPrice = range>0 ? d.compLow + range*0.45 : d.listPrice;
    const diff = d.listPrice - optPrice;

    if(a.mktPos>.65 && d.daysInv>30) {
        a.priceAction='REDUCE';
        a.cut = Math.max(300, Math.min(Math.round(diff/100)*100, Math.round(a.gross*.35/100)*100));
    } else if(a.mktPos<.25 && d.daysInv<20 && a.engScore>20) {
        a.priceAction='INCREASE';
        a.cut = Math.min(Math.round(Math.abs(diff)*.5/100)*100, 800);
    } else if(a.mktPos>.55 && d.daysInv>45) {
        a.priceAction='REDUCE';
        a.cut = Math.max(300, Math.round(diff*.7/100)*100);
    } else {
        a.priceAction='HOLD';
        a.cut=0;
    }
    a.newPrice = a.priceAction==='INCREASE' ? d.listPrice+a.cut : d.listPrice-a.cut;
    a.txLow = a.newPrice-1000;
    a.txHigh = a.newPrice-500;
    a.gLow = a.txLow - a.invested;
    a.gHigh = a.txHigh - a.invested;

    // Elasticity
    a.elast = d.compUnits>15?'HIGH':d.compUnits>8?'MODERATE-HIGH':d.compUnits>4?'MODERATE':'LOW';

    // Exit path
    const retAvg = (a.gLow+a.gHigh)/2 - a.dailyFP*20;
    a.bestExit = (retAvg*a.p30 > a.whNet && a.gLow > d.minGross*.5) ? 'RETAIL' : a.whNet > -500 ? 'WHOLESALE' : 'RETAIL';
    a.reassessDay = d.daysInv + 14;

    // Confidence
    const dp = [d.v30,d.l30,d.compLow,d.compUnits,d.wholesalePrice].filter(v=>v>0).length/5;
    a.conf = dp>.8?'HIGH':dp>.5?'MEDIUM':'LOW';
    a.confPct = dp>.8 ? 80+Math.round(dp*15) : dp>.5 ? 50+Math.round(dp*20) : 20+Math.round(dp*30);

    return a;
}

// ============================================================
// FORMAT HELPERS
// ============================================================
const fm = n => n<0 ? '-$'+Math.abs(Math.round(n)).toLocaleString() : '$'+Math.round(n).toLocaleString();
const fp = n => Math.round(n*100)+'%';
const fn = n => Math.round(n).toLocaleString();

// ============================================================
// GENERATE REPORT
// ============================================================
function generate() {
    const d = collectData();
    if(!d.year||!d.make||!d.model||!d.acqCost||!d.listPrice) { alert('Please fill in Year, Make, Model, Acquisition Cost, and List Price.'); return; }

    // Save vehicle
    const saved = getSaved();
    const exists = saved.findIndex(v => v.year===d.year && v.make===d.make && v.model===d.model && v.trim===d.trim && v.mileage===d.mileage);
    if(exists>=0) saved[exists]=d; else saved.unshift(d);
    if(saved.length>50) saved.pop();
    setSaved(saved);

    // Show loading
    $('loading').classList.add('show');

    setTimeout(() => {
        const a = analyze(d);
        renderReport(d, a);
        $('loading').classList.remove('show');
        $('form').style.display='none';
        $('report').className='show';
        window.scrollTo({top:0,behavior:'smooth'});
    }, 1800);
}

// ============================================================
// RENDER REPORT
// ============================================================
function renderReport(d, a) {
    const title = `${d.year} ${d.make} ${d.model} ${d.trim}`;
    const zBadge = a.zone==='HEALTHY'?'badge-green':a.zone==='AT-RISK'?'badge-yellow':'badge-red';
    const gColor = a.netGross>d.minGross?'green':a.netGross>0?'yellow':'red';
    const p30c = a.p30>.5?'var(--green)':a.p30>.3?'var(--yellow)':'var(--red)';
    const p60c = a.p60>.6?'var(--green)':a.p60>.4?'var(--yellow)':'var(--red)';
    const p90c = a.p90>.7?'var(--green)':a.p90>.5?'var(--yellow)':'var(--red)';

    $('report').innerHTML = `
    <div class="btn-bar" style="justify-content:space-between;">
        <button class="btn btn-outline" onclick="showForm()">← Back to Form</button>
        <button class="btn btn-outline" onclick="window.print()">🖨 Print</button>
    </div>

    <!-- Header -->
    <div class="card" style="display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:16px;">
        <div>
            <h2 style="font-size:24px;">${title}</h2>
            <div style="display:flex;gap:20px;flex-wrap:wrap;margin-top:8px;">
                <span><span style="color:var(--muted);font-size:11px;">MILEAGE</span><br><strong>${fn(d.mileage)} mi</strong></span>
                <span><span style="color:var(--muted);font-size:11px;">COLOR</span><br><strong>${d.color}</strong></span>
                <span><span style="color:var(--muted);font-size:11px;">DAYS IN STOCK</span><br><strong>${d.daysInv}</strong></span>
                <span><span style="color:var(--muted);font-size:11px;">AGING</span><br><span class="badge ${zBadge}">${a.zone}</span></span>
            </div>
        </div>
    </div>

    <!-- KPIs -->
    <div class="kpis">
        <div class="kpi"><div class="label">Total Invested</div><div class="value blue">${fm(a.invested)}</div><div class="sub">Acq ${fm(d.acqCost)} + Recon ${fm(d.reconCost)}</div></div>
        <div class="kpi"><div class="label">Net Gross (at sticker)</div><div class="value ${gColor}">${fm(Math.round(a.netGross))}</div><div class="sub">After ${fm(Math.round(a.fpAccrued))} floorplan</div></div>
        <div class="kpi"><div class="label">Daily Floorplan</div><div class="value red">$${a.dailyFP.toFixed(2)}</div><div class="sub">${fm(Math.round(a.fpAccrued))} accrued</div></div>
        <div class="kpi"><div class="label">Wholesale Exit</div><div class="value ${a.whNet>=0?'yellow':'red'}">${fm(Math.round(a.whNet))}</div><div class="sub">Net after all costs</div></div>
    </div>

    <!-- 1. Sale Probability -->
    <div class="section"><div class="section-head"><div class="section-num">1</div><div class="section-title">Multi-Horizon Sale Probability</div></div><div class="section-body">
        <div class="prob"><div class="prob-label">30 Days</div><div class="prob-track"><div class="prob-fill" style="width:${Math.round(a.p30*100)}%;background:${p30c};">${fp(a.p30)}</div></div></div>
        <div class="prob"><div class="prob-label">60 Days</div><div class="prob-track"><div class="prob-fill" style="width:${Math.round(a.p60*100)}%;background:${p60c};">${fp(a.p60)}</div></div></div>
        <div class="prob"><div class="prob-label">90 Days</div><div class="prob-track"><div class="prob-fill" style="width:${Math.round(a.p90*100)}%;background:${p90c};">${fp(a.p90)}</div></div></div>
        <div class="callout callout-blue"><h4>Key Drivers</h4><ul>
            <li><strong>Market position:</strong> ${Math.round(a.mktPos*100)}th percentile — ${a.mktLabel}.</li>
            <li><strong>Engagement:</strong> Views ${a.viewTrendLabel.toLowerCase()} (${a.viewTrend>0?'+':''}${Math.round(a.viewTrend)}% WoW). Lead-to-view: ${a.l2v.toFixed(1)}%. TD-to-lead: ${a.td2l.toFixed(0)}%.</li>
            <li><strong>Competition:</strong> ${d.compUnits} units — ${d.compUnits>15?'heavy supply pressure':d.compUnits>8?'moderate competition':'limited competition'}.</li>
            <li><strong>Demand:</strong> ${d.demand.charAt(0).toUpperCase()+d.demand.slice(1)}. ${d.seasonal||'No seasonal factors noted.'}</li>
        </ul></div>
    </div></div>

    <!-- 2. Aging -->
    <div class="section"><div class="section-head"><div class="section-num">2</div><div class="section-title">Inventory Velocity & Aging Risk</div></div><div class="section-body">
        <p>Current zone: <span class="badge ${zBadge}">${a.zone}</span> ${d.daysInv>40?'— This vehicle is overdue for its segment. Target: 30–40 days.':''}</p>
        <table><thead><tr><th>Scenario</th><th>+Days</th><th>Total</th><th>Floorplan</th><th>Gross @Sticker</th><th>Realistic Gross</th></tr></thead><tbody>
        ${a.erosion.map((r,i) => `<tr><td>${i===0?'<strong>Today</strong>':'+'+r.add+' days'}</td><td>${r.add}</td><td>${r.tot}</td><td>${fm(Math.round(r.fp))}</td><td>${fm(Math.round(r.gs))}</td><td>${fm(Math.round(r.rLow))} – ${fm(Math.round(r.rHigh))}</td></tr>`).join('')}
        </tbody></table>
        <div class="callout callout-red"><h4>Irrationality Threshold: Day ${a.irrDay}</h4><p>You have <strong>${a.daysLeft} days</strong> before holding becomes economically irrational vs. wholesale. Beyond day ${a.irrDay}, probability-weighted retail falls below wholesale.</p></div>
    </div></div>

    <!-- 3. Pricing -->
    <div class="section"><div class="section-head"><div class="section-num">3</div><div class="section-title">Pricing Strategy</div></div><div class="section-body">
        <div class="rec-box">
            <div class="action">${a.priceAction==='REDUCE'?'↓ REDUCE BY '+fm(a.cut):a.priceAction==='INCREASE'?'↑ INCREASE BY '+fm(a.cut):'● HOLD CURRENT PRICE'}</div>
            <div class="detail">${a.priceAction!=='HOLD'?'New Price: <strong>'+fm(a.newPrice)+'</strong> (from '+fm(d.listPrice)+')':'Maintain at <strong>'+fm(d.listPrice)+'</strong>'}</div>
            <div class="sub">${a.priceAction==='REDUCE'?'Execute today. Not Friday. Today.':''}</div>
        </div>
        ${a.priceAction==='REDUCE'?`<p>At the <strong>${Math.round(a.mktPos*100)}th percentile</strong> of the ${fm(d.compLow)}–${fm(d.compHigh)} range with ${d.compUnits} competing units, you're priced above where mileage and age justify. ${fm(a.cut)} repositions to mid-market with negotiation room for your team.</p>
        <p>Expected transaction: <strong>${fm(a.txLow)} – ${fm(a.txHigh)}</strong>. Expected gross: <strong>${fm(a.gLow)} – ${fm(a.gHigh)}</strong> before floorplan.</p>`:''}
        <div class="callout callout-blue"><h4>Price Elasticity: ${a.elast}</h4><p>${d.compUnits>12?`${d.compUnits} competing units means buyers run filtered price searches. A reduction likely moves you into a lower search bracket. Expect view uptick within 72 hours.`:'Limited competition gives you pricing flexibility. Attributes matter more than marginal price differences.'}</p></div>
    </div></div>

    <!-- 4. Exit Path -->
    <div class="section"><div class="section-head"><div class="section-num">4</div><div class="section-title">Optimal Exit Path</div></div><div class="section-body">
        <div class="exit-grid">
            <div class="exit-card ${a.bestExit==='RETAIL'?'best':''}">
                ${a.bestExit==='RETAIL'?'<div class="best-label">Recommended</div>':''}
                <h4>Retail</h4>
                <div class="g green">${fm(a.gLow)} – ${fm(a.gHigh)}</div>
                <div class="t">${a.priceAction!=='HOLD'?'12–25 days':'20–40 days'} · ${fp(a.p30)}–${fp(a.p60)}</div>
            </div>
            <div class="exit-card ${a.bestExit==='WHOLESALE'?'best':''}">
                ${a.bestExit==='WHOLESALE'?'<div class="best-label">Recommended</div>':''}
                <h4>Wholesale</h4>
                <div class="g ${a.whNet>=0?'yellow':'red'}">${fm(Math.round(a.whNet))}</div>
                <div class="t">3–7 days · ~95%</div>
            </div>
            <div class="exit-card">
                <h4>Dealer Trade</h4>
                <div class="g" style="color:var(--muted);">$0 – $300</div>
                <div class="t">7–21 days · Low prob</div>
            </div>
        </div>
        <div class="callout callout-yellow"><h4>Decision Trigger: Day ${a.reassessDay}</h4><p>If fewer than 2 test drives by day ${a.reassessDay}, move to wholesale immediately. No extensions.</p></div>
    </div></div>

    <!-- 5. Action Plan -->
    <div class="section"><div class="section-head"><div class="section-num">5</div><div class="section-title">Dealer Action Plan — This Week</div></div><div class="section-body">
        <div class="action-item"><div class="num">1</div><div>
            <div class="timing-badge">TODAY</div>
            <h4>${a.priceAction==='REDUCE'?'Execute the '+fm(a.cut)+' price reduction':a.priceAction==='INCREASE'?'Increase price by '+fm(a.cut):'Hold price — monitor 7 days'}</h4>
            <p>${a.priceAction==='REDUCE'?'Reposition to mid-market and trigger platform re-indexing. Every day costs $'+a.dailyFP.toFixed(2)+' in floorplan.':'Maintain current positioning and track engagement.'}</p>
        </div></div>
        <div class="action-item"><div class="num">2</div><div>
            <div class="timing-badge">TODAY</div>
            <h4>Audit and upgrade the listing</h4>
            <p>30+ photos, video walkaround, rewrite description with value narrative. Verify all feature filters toggled on. ${d.equipment?'Highlight: '+d.equipment:''}</p>
        </div></div>
        ${d.l30>0?`<div class="action-item"><div class="num">3</div><div>
            <div class="timing-badge">BY WEDNESDAY</div>
            <h4>Re-engage all ${d.l30} leads from the past 30 days</h4>
            <p>Personal phone calls first, then text, then email. ${a.priceAction==='REDUCE'?'"We just adjusted the price — wanted you to hear it first."':'"Following up — are you still in the market?"'} The ${d.l7} leads from last 7 days get called within 4 hours.</p>
        </div></div>`:''}
        <div class="action-item"><div class="num">${d.l30>0?'4':'3'}</div><div>
            <div class="timing-badge">TOMORROW AM</div>
            <h4>Brief sales team with negotiation framework</h4>
            <p>Sticker: ${fm(a.newPrice)}. Hard floor: ${fm(Math.max(a.newPrice-500, a.invested+d.minGross))}. ${d.notes?'Objection talk-track: address "'+d.notes+'" directly.':''} Don't lead with concessions.</p>
        </div></div>
        <div class="action-item"><div class="num">${d.l30>0?'5':'4'}</div><div>
            <div class="timing-badge">NOW</div>
            <h4>Set wholesale decision date: Day ${a.reassessDay}</h4>
            <p>Calendar it. If &lt;2 test drives by then, wholesale at next auction. No extensions. Current wholesale net: ${fm(Math.round(a.whNet))}.</p>
        </div></div>
    </div></div>

    <!-- 6. Risk & Confidence -->
    <div class="section"><div class="section-head"><div class="section-num">6</div><div class="section-title">Risk & Confidence</div></div><div class="section-body">
        <h3 style="font-size:14px;margin-bottom:10px;">Risk Factors</h3>
        ${d.seasonal&&d.seasonal.toLowerCase().includes('compression')?'<div class="callout callout-red"><h4>Model Year Compression</h4><p>Newer model incentives pulling price ceiling down. External risk — respond with speed.</p></div>':''}
        ${d.daysInv>45?'<div class="callout callout-yellow"><h4>Stale Listing</h4><p>At '+d.daysInv+' days, many buyers have seen and passed. You\'re fishing in a depleted pond.</p></div>':''}
        ${d.compUnits>12?'<div class="callout callout-yellow"><h4>Heavy Competition</h4><p>'+d.compUnits+' units in market. If a competitor liquidates 3+, supply shock requires immediate action.</p></div>':''}
        ${a.viewTrend<-15?'<div class="callout callout-red"><h4>Declining Views</h4><p>Down '+Math.abs(Math.round(a.viewTrend))+'% WoW. Listing is losing search relevance.</p></div>':''}
        ${d.notes&&d.notes.toLowerCase().includes('price')?'<div class="callout callout-yellow"><h4>Price Resistance Reported</h4><p>Sales team confirms buyer pushback. Supports the case for repricing.</p></div>':''}

        <h3 style="font-size:14px;margin:20px 0 10px;">What Would Change This Recommendation</h3>
        <ul style="margin-left:20px;color:var(--muted);font-size:13px;">
            ${d.wholesalePrice?'<li>Wholesale drops below '+fm(d.wholesalePrice-500)+' — exit immediately.</li>':''}
            <li>Competitor liquidates 3+ similar units — cut deeper or wholesale.</li>
            <li>Leads spike to 5+ post-reprice — hold firmer, market supports more.</li>
            ${a.priceAction==='REDUCE'?'<li>Zero test drives 14 days after cut — wholesale, no debate.</li>':''}
        </ul>

        <h3 style="font-size:14px;margin:20px 0 10px;">Confidence Level</h3>
        <div class="conf-bar">
            <strong>${a.conf}</strong>
            <div class="conf-track"><div class="conf-fill" style="width:${a.confPct}%;background:${a.conf==='HIGH'?'var(--green)':a.conf==='MEDIUM'?'var(--yellow)':'var(--red)'};"></div></div>
            <span style="font-size:13px;">${a.confPct}%</span>
        </div>
        <p style="font-size:13px;">${a.conf==='HIGH'?'Well-understood segment with clear data. Math is straightforward. High certainty.':a.conf==='MEDIUM'?'Adequate data for directional recommendations. Some inputs missing.':'Limited data. Gather more comps and engagement metrics.'}</p>
    </div></div>

    <div style="text-align:center;padding:20px;font-size:12px;color:var(--muted);border-top:1px solid var(--border);margin-top:20px;">
        Report generated ${new Date().toLocaleString()} · Vehicle Inventory Intelligence System · All projections based on stated inputs
    </div>`;
}
</script>
</body>
</html>
