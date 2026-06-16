<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Bacalaureat · Română</title>
<style>
  :root {
    --bg: #f7f5f2;
    --surface: #ffffff;
    --border: #e2ddd8;
    --text: #1a1916;
    --muted: #8a8580;
    --accent: #2d5a3d;
    --accent-soft: #e8f0eb;
    --red: #c0392b;
    --red-soft: #fdf0ee;
    --radius: 12px;
    --shadow: 0 2px 16px rgba(0,0,0,0.07);
  }
  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
  body {
    font-family: -apple-system, 'SF Pro Text', 'Helvetica Neue', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    padding: 0 0 80px;
  }
  header {
    position: sticky; top: 0; z-index: 50;
    background: rgba(247,245,242,0.94);
    backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    padding: 14px 20px;
    display: flex; align-items: center; justify-content: space-between;
  }
  header h1 { font-size: 15px; font-weight: 600; letter-spacing: -0.2px; }
  header span { font-size: 13px; color: var(--muted); }

  .view { display: none; padding: 20px; max-width: 600px; margin: 0 auto; }
  .view.active { display: block; }

  nav {
    position: fixed; bottom: 0; left: 0; right: 0; z-index: 50;
    background: rgba(247,245,242,0.96);
    backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
    border-top: 1px solid var(--border);
    display: flex;
  }
  nav button {
    flex: 1; background: none; border: none;
    padding: 10px 4px 14px; font-size: 10px; color: var(--muted);
    cursor: pointer; display: flex; flex-direction: column; align-items: center; gap: 3px;
    font-family: inherit; transition: color 0.15s;
  }
  nav button svg { width: 22px; height: 22px; }
  nav button.active { color: var(--accent); }

  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: 24px; margin-bottom: 16px;
  }
  .q-number {
    display: inline-block; font-size: 11px; font-weight: 700;
    letter-spacing: 0.5px; color: var(--accent); background: var(--accent-soft);
    border-radius: 6px; padding: 2px 8px; margin-bottom: 12px;
  }
  .q-text { font-size: 17px; font-weight: 500; line-height: 1.5; letter-spacing: -0.2px; }
  .placeholder-text { color: var(--muted); font-size: 15px; text-align: center; padding: 40px 0; }

  .btn {
    display: inline-flex; align-items: center; justify-content: center;
    gap: 7px; border: none; border-radius: 10px;
    font-family: inherit; font-size: 15px; font-weight: 600;
    cursor: pointer; padding: 13px 20px;
    transition: opacity 0.1s, transform 0.1s;
  }
  .btn:active { opacity: 0.75; transform: scale(0.97); }
  .btn-primary { background: var(--accent); color: #fff; width: 100%; }
  .btn-secondary { background: var(--border); color: var(--text); }
  .btn-ghost { background: none; color: var(--accent); padding: 0; font-weight: 500; }
  .btn-sm { font-size: 13px; padding: 9px 14px; border-radius: 8px; }
  .btn-row { display: flex; gap: 10px; margin-top: 16px; }
  .btn-row .btn { flex: 1; }

  .answer-section { margin-top: 20px; border-top: 1px solid var(--border); padding-top: 20px; animation: fadeIn 0.25s ease; }
  .answer-label { font-size: 11px; font-weight: 700; letter-spacing: 0.8px; text-transform: uppercase; color: var(--muted); margin-bottom: 12px; }

  .img-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 8px; margin-bottom: 12px; }
  .img-grid img { width: 100%; border-radius: 8px; border: 1px solid var(--border); cursor: pointer; display: block; }
  .img-wrapper { position: relative; }
  .img-del-btn {
    position: absolute; top: 4px; right: 4px;
    background: rgba(0,0,0,0.55); border: none; border-radius: 50%;
    width: 26px; height: 26px; display: flex; align-items: center; justify-content: center;
    cursor: pointer; padding: 0;
  }
  .img-del-btn svg { width: 13px; height: 13px; fill: #fff; }

  .upload-zone {
    border: 1.5px dashed var(--border); border-radius: 10px;
    padding: 20px; text-align: center; cursor: pointer;
    color: var(--muted); font-size: 13px;
    transition: border-color 0.15s, background 0.15s;
  }
  .upload-zone:hover, .upload-zone.drag-over { border-color: var(--accent); background: var(--accent-soft); }

  /* storage warning */
  .storage-bar-wrap { margin-bottom: 12px; }
  .storage-bar-bg { background: var(--border); border-radius: 4px; height: 4px; }
  .storage-bar-fill { height: 4px; border-radius: 4px; background: var(--accent); transition: width 0.3s; }
  .storage-bar-fill.warn { background: #e67e22; }
  .storage-bar-fill.danger { background: var(--red); }
  .storage-label { font-size: 11px; color: var(--muted); margin-top: 4px; }

  .q-list-item {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 10px; padding: 14px 16px; margin-bottom: 10px;
    display: flex; align-items: flex-start; gap: 12px;
    cursor: pointer; transition: background 0.1s;
  }
  .q-list-item:active { background: var(--border); }
  .q-list-item .num { font-size: 11px; font-weight: 700; color: var(--accent); background: var(--accent-soft); border-radius: 5px; padding: 2px 6px; flex-shrink: 0; margin-top: 2px; }
  .q-list-item .has-img { margin-left: auto; flex-shrink: 0; color: var(--accent); margin-top: 2px; }
  .q-list-item p { font-size: 14px; line-height: 1.4; flex: 1; }

  .search-wrap { position: relative; margin-bottom: 16px; }
  .search-wrap svg { position: absolute; left: 12px; top: 50%; transform: translateY(-50%); width: 16px; height: 16px; color: var(--muted); pointer-events: none; }
  input[type="search"], input[type="text"], textarea {
    width: 100%; background: var(--surface); border: 1px solid var(--border);
    border-radius: 10px; font-family: inherit; font-size: 15px; color: var(--text);
    padding: 11px 14px; outline: none; -webkit-appearance: none; appearance: none;
  }
  input[type="search"] { padding-left: 38px; }
  input:focus, textarea:focus { border-color: var(--accent); box-shadow: 0 0 0 3px var(--accent-soft); }
  textarea { resize: vertical; min-height: 100px; line-height: 1.5; }

  .edit-label { font-size: 12px; font-weight: 600; color: var(--muted); margin-bottom: 6px; letter-spacing: 0.3px; }
  .edit-field { margin-bottom: 18px; }

  #lightbox { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.9); z-index: 200; align-items: center; justify-content: center; }
  #lightbox.open { display: flex; }
  #lightbox img { max-width: 95vw; max-height: 90vh; border-radius: 8px; object-fit: contain; }
  #lightboxClose { position: absolute; top: 16px; right: 16px; background: rgba(255,255,255,0.15); border: none; border-radius: 50%; width: 36px; height: 36px; display: flex; align-items: center; justify-content: center; cursor: pointer; color: #fff; }

  #toast { position: fixed; bottom: 90px; left: 50%; transform: translateX(-50%) translateY(10px); background: var(--text); color: #fff; font-size: 14px; padding: 10px 20px; border-radius: 20px; opacity: 0; transition: opacity 0.2s, transform 0.2s; pointer-events: none; white-space: nowrap; z-index: 100; }
  #toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

  .hidden { display: none !important; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes shuffle { 0% { opacity: 1; transform: scale(1); } 40% { opacity: 0; transform: scale(0.95); } 100% { opacity: 1; transform: scale(1); } }
  .shuffle-anim { animation: shuffle 0.3s ease; }

  /* compress warning modal */
  .modal-overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.5); z-index: 300; align-items: flex-end; justify-content: center; }
  .modal-overlay.open { display: flex; }
  .modal-sheet { background: var(--surface); border-radius: 16px 16px 0 0; padding: 24px 20px 36px; width: 100%; max-width: 600px; }
  .modal-title { font-size: 16px; font-weight: 600; margin-bottom: 8px; }
  .modal-body { font-size: 14px; color: var(--muted); line-height: 1.5; margin-bottom: 20px; }
  .modal-sheet .btn { margin-top: 8px; }
</style>
</head>
<body>

<header>
  <h1>Română · BAC</h1>
  <span id="headerSub">96 întrebări</span>
</header>

<div id="viewRandom" class="view active">
  <div class="card" id="randomCard">
    <div class="placeholder-text">Apasă Aleatorie pentru o întrebare</div>
  </div>
  <button class="btn btn-primary" onclick="pickRandom()">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M16 3h5v5M14 10l7-7M8 21H3v-5M10 14l-7 7"/><path d="M21 16v5h-5M14 14l7 7M3 8V3h5M10 10 3 3"/></svg>
    Aleatorie
  </button>
</div>

<div id="viewList" class="view">
  <div class="search-wrap">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
    <input type="search" id="searchInput" placeholder="Caută întrebare…" oninput="filterList(this.value)" autocomplete="off" spellcheck="false">
  </div>
  <div id="qList"></div>
</div>

<div id="viewEdit" class="view">
  <div class="card">
    <div class="q-number" id="editBadge">—</div>
    <div class="edit-field">
      <div class="edit-label">Întrebare</div>
      <textarea id="editText" rows="4"></textarea>
    </div>
    <div class="btn-row">
      <button class="btn btn-secondary btn-sm" onclick="cancelEdit()">Anulează</button>
      <button class="btn btn-primary btn-sm" onclick="saveEdit()">Salvează</button>
    </div>
  </div>
  <div style="margin-top:8px;text-align:center;">
    <button class="btn btn-ghost btn-sm" onclick="showView('viewList')">← Înapoi la listă</button>
  </div>
</div>

<nav>
  <button class="active" onclick="showView('viewRandom')" id="navRandom">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M16 3h5v5M14 10l7-7M8 21H3v-5M10 14l-7 7"/><path d="M21 16v5h-5M14 14l7 7M3 8V3h5M10 10 3 3"/></svg>
    Aleatorie
  </button>
  <button onclick="showView('viewList')" id="navList">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="8" y1="6" x2="21" y2="6"/><line x1="8" y1="12" x2="21" y2="12"/><line x1="8" y1="18" x2="21" y2="18"/><line x1="3" y1="6" x2="3.01" y2="6"/><line x1="3" y1="12" x2="3.01" y2="12"/><line x1="3" y1="18" x2="3.01" y2="18"/></svg>
    Toate
  </button>
</nav>

<div id="lightbox">
  <button id="lightboxClose" onclick="closeLightbox()">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" width="20" height="20"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
  </button>
  <img id="lightboxImg" src="" alt="">
</div>

<div id="toast"></div>
<input type="file" id="fileInput" accept="image/*" multiple style="display:none" onchange="handleFileInput(event)">

<!-- Storage full modal -->
<div class="modal-overlay" id="storageModal">
  <div class="modal-sheet">
    <div class="modal-title">⚠️ Spațiu aproape plin</div>
    <div class="modal-body" id="storageModalBody">localStorage-ul Safari este aproape plin. Șterge câteva poze pentru a elibera spațiu.</div>
    <button class="btn btn-secondary" style="width:100%" onclick="closeStorageModal()">OK</button>
  </div>
</div>

<script>
// ══════════════════════════════════════════════════════
//  QUESTIONS DATA
// ══════════════════════════════════════════════════════
const QUESTIONS_DEFAULT = [
  "Cine este Mihai Eminescu în literatura română și ce reprezintă poemul romantic Luceafărul în opera sa?",
  "Comentează două scene relevante pt romanul realist Ion de Liviu Rebreanu.",
  "Comentează două secvențe relevante din prima strofă și a doua strofă din poezia simbolistă Plumb de George Bacovia.",
  "Care sunt două trăsături ale realismului de tip balzacian prezente în romanul Enigma Otiliei de George Călinescu?",
  "Care este conflictul principal din familia Moromete în primul volum al romanului Moromeții de Marin Preda?",
  "Explică pe scurt titlul poeziei moderniste Eu nu strivesc corola de minuni a lumii de Lucian Blaga.",
  "Comentează două scene relevante din comedia O scrisoare pierdută de I.L. Caragiale.",
  "Care este tema operei în poemul Luceafărul de Mihai Eminescu?",
  "Cum este construit imaginarul artistic în poezia Flori de mucigai de Tudor Arghezi?",
  "Care sunt două trăsături ale basmului cult prezente în Povestea lui Harap-Alb?",
  "Modalități de caracterizare în Ultima noapte de dragoste, întâia noapte de război?",
  "Comentează două secvențe relevante din poemul Riga Crypto și lapona Enigel.",
  "Care sunt cele două conflicte majore care macină personajul Ghiță în Moara cu noroc?",
  "Explică pe scurt titlul poeziei Leoaică tânără, iubirea.",
  "Cine este Marin Sorescu în literatura română și ce rol are parabola dramatică Iona?",
  "Care este tema operei în romanul Baltagul de Mihail Sadoveanu?",
  "Comentează două scene relevante din romanul Ion de Liviu Rebreanu.",
  "Care sunt două trăsături ale curentului literar în Eu nu strivesc corola de minuni a lumii?",
  "a) Cum asigură cuvintele bătrânei simetria compozițională în Moara cu noroc? b) Modalități de caracterizare în nuvelă.",
  "Explică pe scurt titlul poeziei Flori de mucigai.",
  "Comentează două scene relevante din Povestea lui Harap-Alb.",
  "Care este conflictul principal în piesa de teatru Iona?",
  "Care este tema operei în poezia Plumb?",
  "Explică pe scurt titlul inițial comparativ cu cel actual în Enigma Otiliei.",
  "Cum este construit imaginarul artistic în Riga Crypto și lapona Enigel?",
  "Cine este Mihail Sadoveanu în literatura română?",
  "Comentează două scene relevante din Moromeții.",
  "Care sunt două trăsături ale curentului literar în Ultima noapte de dragoste, întâia noapte de război?",
  "Perspectiva narativă în Baltagul. Modalități de caracterizare în Baltagul.",
  "Explică pe scurt titlul operei Povestea lui Harap-Alb. Statut Harap-Alb.",
  "Care este conflictul principal care determină destinul protagonistului din Ion?",
  "Care este tema operei în Ultima noapte de dragoste, întâia noapte de război? Statut Ștefan Gheorghidiu.",
  "Comentează două secvențe relevante din Luceafărul.",
  "Explică pe scurt titlul nuvelei Moara cu noroc. Statut Ghiță.",
  "Care sunt două trăsături ale curentului literar în O scrisoare pierdută?",
  "Cine este Nichita Stănescu în peisajul literar românesc?",
  "Cum subliniază descrierea străzii Antim simetria compozițională în Enigma Otiliei?",
  "Explică pe scurt titlul romanului Moromeții. Statut Ilie Moromete.",
  "Comentează două scene relevante din Ultima noapte de dragoste, întâia noapte de război.",
  "Care sunt două trăsături ale curentului literar în Leoaică tânără, iubirea?",
  "Care este conflictul din O scrisoare pierdută? Statut Tipătescu.",
  "Explică pe scurt titlul poeziei Plumb.",
  "Comentează două scene relevante din Enigma Otiliei.",
  "Cine este Ion Creangă în literatura română? Modalități de caracterizare Harap-Alb.",
  "Cum se oglindește destinul personajului în Iona? Statut Iona.",
  "Explică pe scurt titlul poemului Luceafărul.",
  "Comentează două secvențe relevante din Eu nu strivesc corola de minuni a lumii.",
  "Care sunt două trăsături ale realismului în Ion? Statut Ion.",
  "Explică pe scurt titlul Ultima noapte de dragoste, întâia noapte de război. Statut Ștefan Gheorghidiu.",
  "Cine este Ioan Slavici în literatura română?",
  "Comentează două scene relevante din Moara cu noroc.",
  "Care sunt două trăsături simboliste în Plumb?",
  "Explică pe scurt titlul Baltagul. Statut Vitoria.",
  "Cum se schimbă percepția timpului în Moromeții?",
  "Comentează două secvențe relevante din Flori de mucigai.",
  "Care este conflictul principal din Enigma Otiliei?",
  "Care este tema operei în Iona?",
  "Explică pe scurt titlul romanului Ion.",
  "Cine este Tudor Arghezi în literatura română?",
  "Comentează două scene relevante din Baltagul.",
  "Care sunt două trăsături ale curentului literar în Iona?",
  "Două trăsături ale comediei în O scrisoare pierdută.",
  "Explică pe scurt titlul operei Riga Crypto și lapona Enigel.",
  "Cine este George Călinescu?",
  "Comentează două secvențe relevante din Leoaică tânără, iubirea.",
  "Care sunt două trăsături romantice în Luceafărul?",
  "Care este conflictul principal din Baltagul?",
  "Care este tema operei în Moromeții?",
  "Explică pe scurt titlul operei O scrisoare pierdută.",
  "Cine este Liviu Rebreanu în istoria literaturii române?",
  "Comentează două scene relevante din Iona.",
  "Care sunt două trăsături realiste în Moromeții?",
  "Care este conflictul principal în Povestea lui Harap-Alb?",
  "Care este tema în Eu nu strivesc corola de minuni a lumii?",
  "Cine este Camil Petrescu în literatura română?",
  "Care sunt două trăsături moderniste în Flori de mucigai?",
  "Care este tema operei în Riga Crypto și lapona Enigel?",
  "Cum se trece de la dezechilibru la final fericit în Harap-Alb?",
  "Cine este Marin Preda în literatura română?",
  "Care este conflictul principal al lui Ștefan Gheorghidiu?",
  "Care este tema operei în O scrisoare pierdută?",
  "Care sunt două trăsături tradiționaliste în Baltagul?",
  "Cine este George Bacovia în literatura română?",
  "Care sunt două trăsături moderniste în Riga Crypto și lapona Enigel?",
  "Cum este construit imaginarul artistic în Plumb?",
  "Cine este Lucian Blaga în literatura română?",
  "Cum este construit imaginarul artistic în Eu nu strivesc corola de minuni a lumii?",
  "Cine este Ion Barbu în literatura română?",
  "Cum este construit imaginarul artistic în Leoaică tânără, iubirea?",
  "Cine este I.L. Caragiale în literatura română?",
  "Cum explicăm perspectiva narativă la S2?",
  "Cum explicăm expresivitatea la S2?",
  "Cum explicăm didascaliile la S2?",
  "Cum explicăm modalități de caracterizare la S2?",
  "Relații de simetrie în Flori de mucigai.",
  "Relații de simetrie în Riga Crypto și lapona Enigel."
];

// ══════════════════════════════════════════════════════
//  STORAGE — localStorage with image compression
// ══════════════════════════════════════════════════════
const LS_QUESTIONS = 'bac_questions';
const LS_IMAGES    = 'bac_images';   // JSON: { "0": ["dataUrl",...], "5": [...], ... }

function loadQuestions() {
  try {
    const raw = localStorage.getItem(LS_QUESTIONS);
    if (raw) {
      const arr = JSON.parse(raw);
      if (Array.isArray(arr) && arr.length === QUESTIONS_DEFAULT.length) return arr;
    }
  } catch(e) {}
  return [...QUESTIONS_DEFAULT];
}

function saveQuestions(arr) {
  try { localStorage.setItem(LS_QUESTIONS, JSON.stringify(arr)); } catch(e) { showStorageFull(); }
}

function loadImages() {
  try {
    const raw = localStorage.getItem(LS_IMAGES);
    return raw ? JSON.parse(raw) : {};
  } catch(e) { return {}; }
}

function saveImages(imgMap) {
  try {
    localStorage.setItem(LS_IMAGES, JSON.stringify(imgMap));
    return true;
  } catch(e) {
    showStorageFull();
    return false;
  }
}

function storageUsedKB() {
  let total = 0;
  for (let k in localStorage) {
    if (localStorage.hasOwnProperty(k)) total += localStorage[k].length * 2;
  }
  return Math.round(total / 1024);
}

function showStorageFull() {
  const used = storageUsedKB();
  document.getElementById('storageModalBody').textContent =
    `Spațiul local este plin (${used} KB folosiți din ~5120 KB). Șterge câteva poze pentru a face loc.`;
  document.getElementById('storageModal').classList.add('open');
}
function closeStorageModal() {
  document.getElementById('storageModal').classList.remove('open');
}

// ══════════════════════════════════════════════════════
//  IMAGE COMPRESSION before saving
// ══════════════════════════════════════════════════════
function compressImage(dataUrl, maxW, maxH, quality) {
  return new Promise(resolve => {
    const img = new Image();
    img.onload = () => {
      let w = img.width, h = img.height;
      if (w > maxW) { h = h * maxW / w; w = maxW; }
      if (h > maxH) { w = w * maxH / h; h = maxH; }
      const canvas = document.createElement('canvas');
      canvas.width = Math.round(w); canvas.height = Math.round(h);
      canvas.getContext('2d').drawImage(img, 0, 0, canvas.width, canvas.height);
      resolve(canvas.toDataURL('image/jpeg', quality));
    };
    img.src = dataUrl;
  });
}

// ══════════════════════════════════════════════════════
//  STATE
// ══════════════════════════════════════════════════════
let questions = loadQuestions();
let imgMap    = loadImages();   // { "idx": ["dataUrl", ...] }
let currentIdx   = null;
let showingAnswer = false;
let editingIdx   = null;
let uploadTargetIdx = null;

// ══════════════════════════════════════════════════════
//  VIEWS
// ══════════════════════════════════════════════════════
function showView(id) {
  document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  document.querySelectorAll('nav button').forEach(b => b.classList.remove('active'));
  if (id === 'viewRandom') document.getElementById('navRandom').classList.add('active');
  if (id === 'viewList')   { document.getElementById('navList').classList.add('active'); renderList(); }
}

// ══════════════════════════════════════════════════════
//  RANDOM
// ══════════════════════════════════════════════════════
function pickRandom() {
  currentIdx = Math.floor(Math.random() * questions.length);
  showingAnswer = false;
  renderRandomCard(true);
}

function renderRandomCard(animate) {
  const card = document.getElementById('randomCard');
  if (animate) { card.classList.add('shuffle-anim'); setTimeout(() => card.classList.remove('shuffle-anim'), 350); }

  if (currentIdx === null) {
    card.innerHTML = '<div class="placeholder-text">Apasă Aleatorie pentru o întrebare</div>';
    return;
  }

  const idx = currentIdx;
  const q   = questions[idx];
  const imgs = imgMap[idx] || [];

  let html = `<div class="q-number">#${idx + 1}</div><div class="q-text">${escHtml(q)}</div>`;

  if (!showingAnswer) {
    html += `<div class="btn-row">
      <button class="btn btn-secondary btn-sm" onclick="openEdit(${idx})">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
        Editează
      </button>
      <button class="btn btn-primary btn-sm" onclick="revealAnswer()">
        Răspuns
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/></svg>
      </button>
    </div>`;
  } else {
    html += `<div class="answer-section"><div class="answer-label">Răspuns / Poze</div>`;

    if (imgs.length > 0) {
      html += `<div class="img-grid">`;
      imgs.forEach((src, i) => {
        html += `<div class="img-wrapper">
          <img src="${src}" onclick="openLightbox('${src}')" loading="lazy">
          <button class="img-del-btn" onclick="deleteImg(${idx},${i})">
            <svg viewBox="0 0 24 24"><path d="M18 6L6 18M6 6l12 12"/></svg>
          </button>
        </div>`;
      });
      html += `</div>`;
    } else {
      html += `<p style="color:var(--muted);font-size:14px;margin-bottom:12px;">Nicio poză atașată încă.</p>`;
    }

    // storage bar
    const usedKB = storageUsedKB();
    const maxKB  = 5120;
    const pct    = Math.min(100, Math.round(usedKB / maxKB * 100));
    const barCls = pct > 85 ? 'danger' : pct > 65 ? 'warn' : '';
    html += `<div class="storage-bar-wrap">
      <div class="storage-bar-bg"><div class="storage-bar-fill ${barCls}" style="width:${pct}%"></div></div>
      <div class="storage-label">Stocare locală: ${usedKB} KB / ~5120 KB</div>
    </div>`;

    html += `
      <div class="upload-zone" onclick="triggerUpload(${idx})">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" style="display:block;margin:0 auto 6px"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
        Adaugă poze
      </div>
      <div class="btn-row">
        <button class="btn btn-secondary btn-sm" onclick="openEdit(${idx})">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
          Editează
        </button>
      </div>
    </div>`;
  }

  card.innerHTML = html;
}

function revealAnswer() { showingAnswer = true; renderRandomCard(false); }

// ══════════════════════════════════════════════════════
//  LIST
// ══════════════════════════════════════════════════════
function renderList() {
  const container = document.getElementById('qList');
  container.innerHTML = '';
  const filter = document.getElementById('searchInput').value.toLowerCase();
  let count = 0;

  for (let i = 0; i < questions.length; i++) {
    if (filter && !questions[i].toLowerCase().includes(filter)) continue;
    count++;
    const hasImg = (imgMap[i] || []).length > 0;
    const item = document.createElement('div');
    item.className = 'q-list-item';
    item.innerHTML = `
      <span class="num">${i + 1}</span>
      <p>${escHtml(questions[i])}</p>
      ${hasImg ? `<svg class="has-img" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>` : ''}
    `;
    item.addEventListener('click', () => { currentIdx = i; showingAnswer = false; showView('viewRandom'); renderRandomCard(false); });
    container.appendChild(item);
  }

  if (count === 0) container.innerHTML = '<div class="placeholder-text">Nicio întrebare găsită.</div>';
}

function filterList(v) { renderList(); }

// ══════════════════════════════════════════════════════
//  EDIT
// ══════════════════════════════════════════════════════
function openEdit(idx) {
  editingIdx = idx;
  document.getElementById('editBadge').textContent = `#${idx + 1}`;
  document.getElementById('editText').value = questions[idx];
  showView('viewEdit');
}

function saveEdit() {
  if (editingIdx === null) return;
  const newText = document.getElementById('editText').value.trim();
  if (!newText) { showToast('Întrebarea nu poate fi goală'); return; }
  questions[editingIdx] = newText;
  saveQuestions(questions);
  showToast('Salvat ✓');
  const prev = editingIdx; editingIdx = null;
  currentIdx = prev; showingAnswer = false;
  showView('viewRandom'); renderRandomCard(false);
}

function cancelEdit() {
  if (currentIdx !== null) showView('viewRandom');
  else showView('viewList');
}

// ══════════════════════════════════════════════════════
//  IMAGES
// ══════════════════════════════════════════════════════
function triggerUpload(idx) {
  uploadTargetIdx = idx;
  document.getElementById('fileInput').click();
}

async function handleFileInput(e) {
  const files = Array.from(e.target.files);
  e.target.value = '';
  if (!files.length) return;
  await processFiles(files, uploadTargetIdx);
}

async function processFiles(files, idx) {
  let added = 0;
  for (const file of files) {
    if (!file.type.startsWith('image/')) continue;
    const raw = await fileToDataUrl(file);
    // compress: max 1200×1200, quality 0.75
    const compressed = await compressImage(raw, 1200, 1200, 0.75);
    if (!imgMap[idx]) imgMap[idx] = [];
    imgMap[idx].push(compressed);
    added++;
  }
  if (!saveImages(imgMap)) {
    // rollback last additions on failure
    imgMap[idx].splice(imgMap[idx].length - added, added);
  } else {
    showToast(`${added} poză${added > 1 ? 'uri' : ''} adăugată ✓`);
    if (currentIdx === idx) renderRandomCard(false);
  }
}

function fileToDataUrl(file) {
  return new Promise(resolve => {
    const r = new FileReader();
    r.onload = e => resolve(e.target.result);
    r.readAsDataURL(file);
  });
}

function deleteImg(qIdx, imgIdx) {
  if (!imgMap[qIdx]) return;
  imgMap[qIdx].splice(imgIdx, 1);
  if (imgMap[qIdx].length === 0) delete imgMap[qIdx];
  saveImages(imgMap);
  showToast('Poză ștearsă');
  if (currentIdx === qIdx) renderRandomCard(false);
}

// ══════════════════════════════════════════════════════
//  LIGHTBOX
// ══════════════════════════════════════════════════════
function openLightbox(src) {
  document.getElementById('lightboxImg').src = src;
  document.getElementById('lightbox').classList.add('open');
}
function closeLightbox() { document.getElementById('lightbox').classList.remove('open'); }
document.getElementById('lightbox').addEventListener('click', function(e) { if (e.target === this) closeLightbox(); });

// ══════════════════════════════════════════════════════
//  TOAST
// ══════════════════════════════════════════════════════
let _toastTimer;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  clearTimeout(_toastTimer);
  _toastTimer = setTimeout(() => t.classList.remove('show'), 2200);
}

function escHtml(s) {
  return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

// init header
document.getElementById('headerSub').textContent = `${questions.length} întrebări`;
</script>
</body>
</html>
