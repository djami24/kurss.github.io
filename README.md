<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dollar kursi — Markaziy bank</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600;700&family=Manrope:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #0d211c;
    --panel: #133429;
    --panel-2: #163d2f;
    --line: #244a3c;
    --gold: #cda349;
    --gold-dim: #8a7139;
    --cream: #f1ece0;
    --mint: #6fb79a;
    --red: #d9705a;
    --green: #6fbf8a;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background: radial-gradient(ellipse at top, #123528 0%, var(--bg) 55%, #081712 100%);
    color: var(--cream);
    font-family: 'Manrope', sans-serif;
    min-height:100vh;
    padding: 40px 20px 60px;
  }
  .wrap{ max-width: 760px; margin: 0 auto; }

  .eyebrow{
    font-family:'IBM Plex Mono', monospace;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    font-size: 11.5px;
    color: var(--gold);
    text-align:center;
    margin-bottom: 10px;
  }
  h1{
    text-align:center;
    font-size: clamp(24px, 4.5vw, 34px);
    font-weight: 800;
    margin: 0 0 6px;
    letter-spacing: -0.01em;
  }
  .subtitle{
    text-align:center;
    color: #a9c3b6;
    font-size: 14px;
    margin-bottom: 34px;
  }

  /* ---- split-flap board ---- */
  .board{
    background: linear-gradient(180deg, var(--panel-2), var(--panel));
    border: 1px solid var(--line);
    border-radius: 18px;
    padding: 30px 24px 24px;
    box-shadow: 0 30px 60px -25px rgba(0,0,0,0.6), inset 0 1px 0 rgba(255,255,255,0.03);
    position: relative;
    overflow:hidden;
  }
  .board::before{
    content:"";
    position:absolute; inset:0;
    background: repeating-linear-gradient(180deg, rgba(0,0,0,0.12) 0px, rgba(0,0,0,0.12) 1px, transparent 1px, transparent 44px);
    pointer-events:none;
  }
  .board-top{
    display:flex; justify-content: space-between; align-items:center;
    font-family:'IBM Plex Mono', monospace;
    font-size: 12px;
    color: #85a696;
    margin-bottom: 18px;
    position: relative;
    z-index:1;
  }
  .board-top .code{ color: var(--gold); font-weight:600; letter-spacing: 0.08em;}
  .flap-row{
    display:flex;
    justify-content:center;
    align-items:baseline;
    gap: 6px;
    position:relative;
    z-index:1;
  }
  .flap-digit{
    font-family:'IBM Plex Mono', monospace;
    font-weight:700;
    font-size: clamp(38px, 9vw, 64px);
    background: #0b1f18;
    border: 1px solid #2b5645;
    border-radius: 8px;
    padding: 6px 4px;
    min-width: 0.85em;
    text-align:center;
    color: var(--cream);
    box-shadow: inset 0 -2px 6px rgba(0,0,0,0.5), inset 0 2px 0 rgba(255,255,255,0.04);
  }
  .flap-digit.dim{ color:#5a7c6d; background:#0a1c16; }
  .flap-sep{
    font-family:'IBM Plex Mono', monospace;
    font-weight:700;
    font-size: clamp(38px, 9vw, 64px);
    color: #4a7062;
    padding: 6px 0;
  }
  .flap-unit{
    font-family:'IBM Plex Mono', monospace;
    font-size: 15px;
    color: #85a696;
    align-self:center;
    margin-left: 8px;
  }
  @keyframes flapIn{
    0%{ transform: rotateX(90deg); opacity:0.2; }
    100%{ transform: rotateX(0deg); opacity:1; }
  }
  .flap-digit{ animation: flapIn 0.5s ease; transform-origin: 50% 50%; }

  .board-bottom{
    display:flex; justify-content:space-between; align-items:center;
    margin-top: 20px;
    position:relative; z-index:1;
    font-family:'IBM Plex Mono', monospace;
    font-size: 12.5px;
    color: #85a696;
  }
  .diff{ font-weight:600; }
  .diff.up{ color: var(--green); }
  .diff.down{ color: var(--red); }
  .diff.flat{ color: #85a696; }

  .status-line{
    text-align:center;
    font-size: 12px;
    color: #7a9686;
    margin-top: 14px;
    min-height: 16px;
  }
  .status-line a{ color: var(--gold); text-decoration:none; }
  .status-line a:hover{ text-decoration:underline; }

  /* ---- calculator ---- */
  .calc{
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 18px;
    padding: 26px 24px;
    margin-top: 22px;
  }
  .calc h2{
    font-size: 14px;
    text-transform: uppercase;
    letter-spacing: 0.14em;
    color: var(--gold);
    margin: 0 0 18px;
    font-weight:700;
  }
  .row{
    display:flex;
    align-items:center;
    gap: 12px;
    background: #0d251d;
    border: 1px solid var(--line);
    border-radius: 12px;
    padding: 12px 16px;
    margin-bottom: 12px;
  }
  .row label{
    font-family:'IBM Plex Mono', monospace;
    font-size: 13px;
    color: var(--mint);
    width: 62px;
    flex-shrink:0;
  }
  .row input{
    background: transparent;
    border: none;
    outline: none;
    color: var(--cream);
    font-family:'IBM Plex Mono', monospace;
    font-size: 19px;
    font-weight: 600;
    width: 100%;
    text-align: right;
  }
  .row input::placeholder{ color:#4a6a5c; }
  .swap-btn{
    display:flex;
    justify-content:center;
    margin: -4px 0 10px;
  }
  .swap-btn button{
    background: var(--panel-2);
    border: 1px solid var(--line);
    color: var(--gold);
    width: 34px; height:34px;
    border-radius: 50%;
    cursor:pointer;
    font-size:16px;
    display:flex; align-items:center; justify-content:center;
    transition: transform 0.2s ease, background 0.2s ease;
  }
  .swap-btn button:hover{ background:#1c4636; transform: rotate(180deg); }

  .manual-toggle{
    text-align:center;
    margin-top: 16px;
  }
  .manual-toggle button{
    background:none;
    border: none;
    color: #7a9686;
    font-size: 12px;
    font-family:'IBM Plex Mono', monospace;
    cursor:pointer;
    text-decoration: underline;
    text-underline-offset: 3px;
  }
  .manual-row{
    display:none;
    margin-top: 14px;
  }
  .manual-row.show{ display:flex; }

  footer{
    text-align:center;
    margin-top: 30px;
    font-size: 11.5px;
    color: #5e7c6d;
    line-height:1.6;
  }
  footer a{ color: var(--gold); }

  @media (max-width: 480px){
    .flap-digit{ padding: 5px 2px; }
    .row label{ width: 50px; font-size:12px; }
    .row input{ font-size: 16px; }
  }
</style>
</head>
<body>
<div class="wrap">
  <div class="eyebrow">O'zbekiston Respublikasi Markaziy banki</div>
  <h1>AQSH dollari kursi</h1>
  <div class="subtitle">Rasmiy kurs — real vaqt rejimida CBU.uz orqali</div>

  <div class="board">
    <div class="board-top">
      <span class="code">USD / UZS</span>
      <span id="rateDate">— .— .—</span>
    </div>
    <div class="flap-row" id="flapRow">
      <span class="flap-digit dim">—</span>
      <span class="flap-digit dim">—</span>
      <span class="flap-digit dim">—</span>
      <span class="flap-digit dim">—</span>
      <span class="flap-digit dim">—</span>
      <span class="flap-unit">so'm</span>
    </div>
    <div class="board-bottom">
      <span>1 AQSH dollari uchun</span>
      <span class="diff flat" id="diffLabel">o'zgarish yo'q</span>
    </div>
  </div>

  <div class="status-line" id="statusLine">Kurs yuklanmoqda…</div>

  <div class="calc">
    <h2>Kalkulyator</h2>
    <div class="row">
      <label>USD</label>
      <input type="text" inputmode="decimal" id="usdInput" placeholder="0" value="1">
    </div>
    <div class="swap-btn"><button id="swapBtn" title="Aylantirish">⇅</button></div>
    <div class="row">
      <label>UZS</label>
      <input type="text" inputmode="decimal" id="uzsInput" placeholder="0">
    </div>

    <div class="manual-toggle">
      <button id="manualToggle">Kursni qo'lda kiritish</button>
    </div>
    <div class="row manual-row" id="manualRow">
      <label>Kurs</label>
      <input type="text" inputmode="decimal" id="manualRate" placeholder="masalan: 12750">
    </div>
  </div>

  <footer>
    Manba: <a href="https://cbu.uz" target="_blank" rel="noopener">cbu.uz</a> — O'zbekiston Respublikasi Markaziy banki rasmiy sayti.<br>
    Ushbu kurs faqat statistik/hisob-kitob maqsadlarida beriladi, bank sotib olish yoki sotish majburiyatini bildirmaydi.
  </footer>
</div>

<script>
let currentRate = null;
let manualMode = false;

const flapRow = document.getElementById('flapRow');
const rateDate = document.getElementById('rateDate');
const diffLabel = document.getElementById('diffLabel');
const statusLine = document.getElementById('statusLine');
const usdInput = document.getElementById('usdInput');
const uzsInput = document.getElementById('uzsInput');
const manualRate = document.getElementById('manualRate');
const manualToggle = document.getElementById('manualToggle');
const manualRow = document.getElementById('manualRow');
const swapBtn = document.getElementById('swapBtn');

let lastEdited = 'usd';

function renderFlap(rateValue){
  const rounded = Math.round(rateValue);
  const digits = String(rounded).padStart(5, '0').split('');
  flapRow.innerHTML = '';
  digits.forEach((d, i) => {
    const span = document.createElement('span');
    span.className = 'flap-digit';
    span.style.animationDelay = (i * 0.06) + 's';
    span.textContent = d;
    flapRow.appendChild(span);
  });
  const unit = document.createElement('span');
  unit.className = 'flap-unit';
  unit.textContent = "so'm";
  flapRow.appendChild(unit);
}

function formatDateUZ(dateStr){
  try{
    const d = new Date(dateStr);
    if(isNaN(d)) return dateStr;
    const months = ['yan','fev','mar','apr','may','iyun','iyul','avg','sen','okt','noy','dek'];
    return d.getDate() + '-' + months[d.getMonth()] + ', ' + d.getFullYear();
  }catch(e){ return dateStr; }
}

function setDiff(diffValue){
  const d = parseFloat(diffValue);
  if(isNaN(d) || d === 0){
    diffLabel.textContent = "o'zgarish yo'q";
    diffLabel.className = 'diff flat';
  } else if(d > 0){
    diffLabel.textContent = '▲ +' + d.toFixed(2) + " so'm";
    diffLabel.className = 'diff up';
  } else {
    diffLabel.textContent = '▼ ' + d.toFixed(2) + " so'm";
    diffLabel.className = 'diff down';
  }
}

function recalc(){
  const rate = manualMode ? parseFloat(manualRate.value) : currentRate;
  if(!rate || isNaN(rate)) return;
  if(lastEdited === 'usd'){
    const usd = parseFloat(usdInput.value.replace(/[, ]/g,''));
    if(!isNaN(usd)){
      uzsInput.value = Math.round(usd * rate).toLocaleString('ru-RU');
    } else {
      uzsInput.value = '';
    }
  } else {
    const uzs = parseFloat(uzsInput.value.replace(/[, ]/g,''));
    if(!isNaN(uzs)){
      usdInput.value = (uzs / rate).toFixed(2);
    } else {
      usdInput.value = '';
    }
  }
}

usdInput.addEventListener('input', () => { lastEdited = 'usd'; recalc(); });
uzsInput.addEventListener('input', () => { lastEdited = 'uzs'; recalc(); });
manualRate.addEventListener('input', () => { recalc(); });

swapBtn.addEventListener('click', () => {
  lastEdited = (lastEdited === 'usd') ? 'uzs' : 'usd';
  const tmp = usdInput.value;
  usdInput.value = uzsInput.value;
  uzsInput.value = tmp;
  recalc();
});

manualToggle.addEventListener('click', () => {
  manualMode = !manualMode;
  manualRow.classList.toggle('show', manualMode);
  manualToggle.textContent = manualMode ? "Rasmiy kursga qaytish" : "Kursni qo'lda kiritish";
  if(manualMode && currentRate){
    manualRate.value = currentRate;
  }
  recalc();
});

async function fetchRate(){
  statusLine.textContent = 'Kurs yuklanmoqda…';
  try{
    const res = await fetch('https://cbu.uz/uz/arkhiv-kursov-valyut/json/USD/');
    if(!res.ok) throw new Error('network');
    const data = await res.json();
    const item = Array.isArray(data) ? data[0] : data;
    const rate = parseFloat(item.Rate ?? item.rate);
    const diff = item.Diff ?? item.diff;
    const date = item.Date ?? item.date;
    if(!rate || isNaN(rate)) throw new Error('parse');

    currentRate = rate;
    renderFlap(rate);
    rateDate.textContent = formatDateUZ(date);
    setDiff(diff);
    statusLine.innerHTML = 'Yangilandi: rasmiy manba — <a href="https://cbu.uz" target="_blank" rel="noopener">cbu.uz</a>';
    if(!manualMode) recalc();
  }catch(err){
    statusLine.textContent = "Kursni avtomatik yuklab bo'lmadi — pastda qo'lda kiriting.";
    manualMode = true;
    manualRow.classList.add('show');
    manualToggle.textContent = "Rasmiy kursga qaytish";
    flapRow.querySelectorAll('.flap-digit').forEach(d => d.classList.add('dim'));
  }
}

usdInput.value = '1';
fetchRate();
</script>
</body>
</html>
