<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ClipAI Studio — Gerador de Videoclipe Automático</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{background:#0a0a0a;color:#fff;font-family:'Inter',sans-serif;min-height:100vh}

#setup{padding:24px;max-width:700px;margin:0 auto}
.logo{font-family:'Bebas Neue',sans-serif;font-size:32px;letter-spacing:3px;color:#fff;margin-bottom:4px}
.logo span{color:#e63946}
.sub{font-size:12px;color:#666;margin-bottom:24px;letter-spacing:1px;text-transform:uppercase}

.field-group{margin-bottom:16px}
.field-group label{font-size:11px;color:#888;text-transform:uppercase;letter-spacing:1px;display:block;margin-bottom:6px}
textarea,input,select{width:100%;background:#141414;border:1px solid #222;color:#fff;padding:10px 12px;border-radius:6px;font-size:13px;font-family:'Inter',sans-serif;resize:vertical;outline:none;transition:border 0.2s}
textarea:focus,input:focus,select:focus{border-color:#e63946}
textarea{min-height:120px}

.row2{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px}

.key-note{background:#141414;border:1px solid #1e1e1e;border-left:3px solid #e63946;padding:10px 14px;border-radius:0 6px 6px 0;font-size:12px;color:#888;margin-bottom:20px;line-height:1.6}
.key-note strong{color:#e63946}
.key-note a{color:#e63946;text-decoration:none}
.key-note a:hover{text-decoration:underline}

.btn-gen{width:100%;padding:14px;background:#e63946;color:#fff;border:none;border-radius:8px;font-size:15px;font-family:'Bebas Neue',sans-serif;letter-spacing:2px;cursor:pointer;transition:opacity 0.2s;margin-top:4px}
.btn-gen:hover{opacity:0.85}
.btn-gen:disabled{opacity:0.4;cursor:not-allowed}

#loading{display:none;padding:60px 24px;text-align:center;max-width:500px;margin:0 auto}
.load-title{font-family:'Bebas Neue',sans-serif;font-size:24px;letter-spacing:3px;color:#e63946;margin-bottom:8px}
.load-msg{font-size:13px;color:#666;margin-bottom:24px;min-height:20px}
.prog-wrap{background:#1a1a1a;border-radius:999px;height:4px;overflow:hidden;max-width:300px;margin:0 auto 20px}
.prog-fill{height:100%;background:#e63946;border-radius:999px;transition:width 0.5s}
.steps-list{display:flex;flex-direction:column;gap:10px;max-width:300px;margin:0 auto;text-align:left}
.step-item{display:flex;align-items:center;gap:10px;font-size:12px;color:#444;transition:color 0.3s}
.step-item.done{color:#4caf50}
.step-item.active{color:#fff}
.step-dot{width:8px;height:8px;border-radius:50%;background:#333;flex-shrink:0;transition:background 0.3s}
.step-item.done .step-dot{background:#4caf50}
.step-item.active .step-dot{background:#e63946;box-shadow:0 0 8px #e63946}

#error-box{display:none;padding:24px;max-width:700px;margin:0 auto}
.err-card{background:#1a0a0a;border:1px solid #e63946;border-radius:8px;padding:24px}
.err-title{font-family:'Bebas Neue',sans-serif;font-size:20px;color:#e63946;margin-bottom:8px}
.err-msg{font-size:13px;color:#888;line-height:1.6;margin-bottom:16px}
.btn-back{background:transparent;border:1px solid #333;color:#888;padding:9px 18px;border-radius:6px;font-size:13px;cursor:pointer;font-family:'Inter',sans-serif}
.btn-back:hover{border-color:#fff;color:#fff}

#player-wrap{display:none}

.video-stage{position:relative;width:100%;background:#000;overflow:hidden;aspect-ratio:16/9}
.video-stage video{width:100%;height:100%;object-fit:cover;display:block}
.video-overlay{position:absolute;inset:0;pointer-events:none}
.vinheta{position:absolute;inset:0;background:radial-gradient(ellipse at center,transparent 40%,rgba(0,0,0,0.75) 100%)}
.lyric-display{position:absolute;bottom:60px;left:0;right:0;text-align:center;padding:0 40px}
.lyric-line{font-family:'Bebas Neue',sans-serif;font-size:clamp(18px,4vw,38px);letter-spacing:2px;color:#fff;text-shadow:0 2px 20px rgba(0,0,0,0.9),0 0 40px rgba(230,57,70,0.5);line-height:1.2;opacity:0;transform:translateY(12px);transition:all 0.4s ease;pointer-events:none;margin-bottom:4px}
.lyric-line.visible{opacity:1;transform:translateY(0)}
.lyric-line.fade{opacity:0;transform:translateY(-8px)}
.prog-bar-wrap{position:absolute;bottom:0;left:0;right:0;height:3px;background:rgba(255,255,255,0.1)}
.prog-bar-fill{height:100%;background:#e63946;width:0%;transition:width 0.1s linear}
.hud-top{position:absolute;top:0;left:0;right:0;padding:16px 20px;display:flex;justify-content:space-between;align-items:center;background:linear-gradient(to bottom,rgba(0,0,0,0.7),transparent)}
.hud-title{font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:2px;color:rgba(255,255,255,0.7)}
.hud-badge{font-size:10px;color:#e63946;border:1px solid #e63946;padding:2px 8px;border-radius:999px;letter-spacing:1px}

.controls{background:#111;padding:14px 20px;display:flex;align-items:center;gap:12px;border-bottom:1px solid #1a1a1a}
.ctrl-btn{background:transparent;border:1px solid #2a2a2a;color:#aaa;width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:13px;transition:all 0.15s;flex-shrink:0}
.ctrl-btn:hover{border-color:#e63946;color:#fff}
.ctrl-btn.play-btn{width:44px;height:44px;background:#e63946;border-color:#e63946;color:#fff;font-size:16px}
.ctrl-btn.play-btn:hover{background:#c62d39}
.time-display{font-size:12px;color:#666;font-variant-numeric:tabular-nums;flex-shrink:0;min-width:70px}
.vol-wrap{display:flex;align-items:center;gap:8px;margin-left:auto}
input[type=range]{-webkit-appearance:none;height:3px;background:#2a2a2a;border-radius:999px;outline:none;width:80px;cursor:pointer}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:13px;height:13px;border-radius:50%;background:#e63946;cursor:pointer}

.info-panel{background:#0d0d0d;padding:14px 20px;border-bottom:1px solid #1a1a1a}
.info-row{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px}
.info-label{font-size:10px;color:#555;text-transform:uppercase;letter-spacing:1px}
.clip-counter{font-size:12px;color:#888}
.clip-counter span{color:#e63946;font-weight:600}
.action-row{display:flex;gap:8px;flex-wrap:wrap}
.act-btn{display:flex;align-items:center;gap:6px;padding:8px 13px;border-radius:6px;font-size:12px;cursor:pointer;border:1px solid #2a2a2a;background:transparent;color:#888;transition:all 0.15s;font-family:'Inter',sans-serif}
.act-btn:hover{border-color:#e63946;color:#fff}
.act-btn.primary{background:#e63946;border-color:#e63946;color:#fff}
.act-btn.primary:hover{background:#c62d39}

.clips-preview{background:#0d0d0d;padding:14px 20px;border-bottom:1px solid #1a1a1a}
.clips-grid{display:flex;gap:8px;overflow-x:auto;padding-bottom:6px}
.clips-grid::-webkit-scrollbar{height:3px}
.clips-grid::-webkit-scrollbar-thumb{background:#333;border-radius:999px}
.clip-thumb{width:80px;flex-shrink:0;cursor:pointer;border-radius:5px;overflow:hidden;border:2px solid transparent;transition:border 0.15s}
.clip-thumb.active{border-color:#e63946}
.clip-thumb-img{width:100%;height:50px;object-fit:cover;display:block;background:#1a1a1a}
.clip-icon{width:100%;height:50px;background:#1a1a1a;display:flex;align-items:center;justify-content:center;font-size:20px}
.clip-label{font-size:9px;color:#555;text-align:center;padding:3px 2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}

.lyrics-panel{background:#0d0d0d;padding:14px 20px;max-height:200px;overflow-y:auto}
.lyrics-panel::-webkit-scrollbar{width:3px}
.lyrics-panel::-webkit-scrollbar-thumb{background:#333;border-radius:999px}
.lyric-item{padding:6px 0 6px 14px;font-size:13px;color:#444;border-left:2px solid transparent;cursor:pointer;transition:all 0.15s;line-height:1.5}
.lyric-item.current{color:#fff;border-left-color:#e63946}
.lyric-item:hover{color:#888}
</style>
</head>
<body>

<!-- ═══ SETUP ═══ -->
<div id="setup">
  <div class="logo">CLIP<span>AI</span> STUDIO</div>
  <div class="sub">Gerador automático de videoclipe com IA</div>

  <div class="key-note">
    <strong>Como funciona:</strong> A IA cria a letra completa → busca vídeos reais no Pixabay → monta o videoclipe automaticamente com a letra sincronizada na tela, estilo clipe profissional. Cole a letra no <strong>Suno Pro</strong> e o vídeo no <strong>CapCut Pro</strong> para finalizar.
  </div>

  <div class="field-group">
    <label>Tema / ideia da música</label>
    <textarea id="tema" placeholder="Ex: música trap sobre superar dificuldades e nunca desistir dos sonhos..."></textarea>
  </div>

  <div class="row2">
    <div class="field-group">
      <label>Gênero musical</label>
      <select id="genero">
        <option>Trap / Hip-hop</option>
        <option>Pop</option>
        <option>R&B / Soul</option>
        <option>Lo-fi</option>
        <option>Eletrônica / EDM</option>
        <option>Gospel / Inspiracional</option>
        <option>Funk carioca</option>
        <option>Sertanejo universitário</option>
        <option>Rock alternativo</option>
        <option>Phonk</option>
      </select>
    </div>
    <div class="field-group">
      <label>Idioma da letra</label>
      <select id="idioma">
        <option>Português (BR)</option>
        <option>Inglês</option>
        <option>Espanhol</option>
      </select>
    </div>
  </div>

  <div class="row3">
    <div class="field-group">
      <label>Mood / Tom</label>
      <select id="mood">
        <option>Motivacional</option>
        <option>Melancólico</option>
        <option>Energético</option>
        <option>Romântico</option>
        <option>Espiritual</option>
        <option>Festa</option>
        <option>Agressivo</option>
        <option>Suave / Chill</option>
      </select>
    </div>
    <div class="field-group">
      <label>Duração do clipe</label>
      <select id="duracao">
        <option value="60">~1 minuto</option>
        <option value="120" selected>~2 minutos</option>
        <option value="180">~3 minutos</option>
      </select>
    </div>
    <div class="field-group">
      <label>Pixabay API Key</label>
      <input type="text" id="pxkey" placeholder="Cole sua key aqui">
    </div>
  </div>

  <div class="key-note">
    <strong>API Key gratuita do Pixabay:</strong> acesse <a href="https://pixabay.com/api/docs/" target="_blank">pixabay.com/api/docs</a> → crie uma conta → copie sua key e cole acima. Sem key, o clipe usa vídeos de demonstração.
  </div>

  <button class="btn-gen" id="btn-gerar" onclick="iniciar()">▶ GERAR VIDEOCLIPE AUTOMÁTICO</button>
</div>

<!-- ═══ LOADING ═══ -->
<div id="loading">
  <div class="load-title">GERANDO CLIPE</div>
  <div class="load-msg" id="load-msg">Iniciando...</div>
  <div class="prog-wrap"><div class="prog-fill" id="prog-fill" style="width:0%"></div></div>
  <div class="steps-list" id="steps-list"></div>
</div>

<!-- ═══ ERRO ═══ -->
<div id="error-box">
  <div class="err-card">
    <div class="err-title">⚠ Erro na geração</div>
    <div class="err-msg" id="err-msg-text"></div>
    <button class="btn-back" onclick="voltarSetup()">← Tentar novamente</button>
  </div>
</div>

<!-- ═══ PLAYER ═══ -->
<div id="player-wrap">
  <div class="video-stage" id="video-stage">
    <video id="main-video" muted playsinline preload="auto"></video>
    <div class="video-overlay">
      <div class="vinheta"></div>
      <div class="hud-top">
        <div class="hud-title" id="hud-title">CLIPAI STUDIO</div>
        <div class="hud-badge">AUTO CLIP</div>
      </div>
      <div class="lyric-display">
        <div class="lyric-line" id="lyric-a"></div>
        <div class="lyric-line" id="lyric-b"></div>
      </div>
      <div class="prog-bar-wrap"><div class="prog-bar-fill" id="main-prog"></div></div>
    </div>
  </div>

  <div class="controls">
    <button class="ctrl-btn" onclick="prevClip()" title="Cena anterior">&#9664;&#9664;</button>
    <button class="ctrl-btn play-btn" id="play-btn" onclick="togglePlay()">&#9654;</button>
    <button class="ctrl-btn" onclick="nextClip()" title="Próxima cena">&#9654;&#9654;</button>
    <span class="time-display" id="time-disp">0:00 / 0:00</span>
    <div class="vol-wrap">
      <span style="font-size:14px">🔊</span>
      <input type="range" min="0" max="1" step="0.05" value="0" id="vol-slider" oninput="setVol(this.value)">
    </div>
  </div>

  <div class="info-panel">
    <div class="info-row">
      <span class="info-label">Cena atual</span>
      <span class="clip-counter">cena <span id="clip-num">1</span> de <span id="clip-total">0</span></span>
    </div>
    <div class="action-row">
      <button class="act-btn primary" onclick="voltarSetup()">↺ Novo clipe</button>
      <button class="act-btn" onclick="copiarLetra()">📋 Copiar letra</button>
      <button class="act-btn" onclick="copiarPromptSuno()">🎵 Prompt Suno Pro</button>
      <button class="act-btn" onclick="window.open('https://pixabay.com/videos/','_blank')">🎬 Pixabay</button>
      <button class="act-btn" onclick="window.open('https://suno.com/create','_blank')">🎧 Abrir Suno</button>
      <button class="act-btn" onclick="window.open('https://www.capcut.com','_blank')">✂️ Abrir CapCut</button>
    </div>
  </div>

  <div class="clips-preview">
    <div class="info-label" style="margin-bottom:10px">Cenas do clipe</div>
    <div class="clips-grid" id="clips-grid"></div>
  </div>

  <div class="lyrics-panel">
    <div class="info-label" style="margin-bottom:10px">Letra completa</div>
    <div id="lyrics-list"></div>
  </div>
</div>

<script>
// ─── ESTADO GLOBAL ──────────────────────────────────────────────────
const ANTHROPIC_KEY = ''; // deixe vazio — a API é chamada via proxy do Claude.ai
let clips = [];
let lyrics = [];
let clipDur = 8;
let currentClip = 0;
let playing = false;
let ticker = null;
let totalSecs = 0;
let elapsed = 0;
let sunoPrompt = '';
let letraCompleta = '';

const DEMO_URLS = [
  'https://cdn.pixabay.com/video/2016/09/08/5093-182757895_medium.mp4',
  'https://cdn.pixabay.com/video/2020/07/30/46018-447089985_medium.mp4',
  'https://cdn.pixabay.com/video/2019/12/16/30225-380773517_medium.mp4',
  'https://cdn.pixabay.com/video/2020/05/19/39733-422077809_medium.mp4',
  'https://cdn.pixabay.com/video/2016/01/05/1882-150699075_medium.mp4',
  'https://cdn.pixabay.com/video/2021/09/28/90800-621012099_medium.mp4',
  'https://cdn.pixabay.com/video/2020/04/06/35362-410012175_medium.mp4',
  'https://cdn.pixabay.com/video/2019/05/08/23597-335427135_medium.mp4',
];

// ─── UI ─────────────────────────────────────────────────────────────
function setStage(s) {
  ['setup','loading','error-box','player-wrap'].forEach(id => {
    document.getElementById(id).style.display = (id === s) ? 'block' : 'none';
  });
}

const STEPS = [
  'Gerando letra com IA',
  'Criando prompt para o Suno Pro',
  'Buscando vídeos no Pixabay',
  'Carregando clipes de vídeo',
  'Montando timeline',
  'Sincronizando letra com o clipe'
];
let stepState = [];

function initSteps() {
  stepState = STEPS.map(() => 'pending');
  document.getElementById('steps-list').innerHTML = STEPS.map((s,i) =>
    `<div class="step-item" id="st${i}"><div class="step-dot"></div><span>${s}</span></div>`
  ).join('');
}

function setStep(i, state, msg) {
  stepState[i] = state;
  const el = document.getElementById('st'+i);
  if (el) el.className = 'step-item ' + (state==='done'?'done':state==='active'?'active':'');
  if (msg) document.getElementById('load-msg').textContent = msg;
  const done = stepState.filter(s => s==='done').length;
  document.getElementById('prog-fill').style.width = (done / STEPS.length * 100) + '%';
}

function mostrarErro(msg) {
  setStage('error-box');
  document.getElementById('err-msg-text').textContent = msg;
}

function voltarSetup() {
  pausePlay();
  setStage('setup');
}

// ─── INICIAR ─────────────────────────────────────────────────────────
async function iniciar() {
  const tema = document.getElementById('tema').value.trim() || 'música motivacional sobre superar desafios e nunca desistir';
  const genero = document.getElementById('genero').value;
  const idioma = document.getElementById('idioma').value;
  const mood = document.getElementById('mood').value;
  const durSecs = parseInt(document.getElementById('duracao').value);
  const pxKey = document.getElementById('pxkey').value.trim();

  setStage('loading');
  initSteps();
  clips=[]; lyrics=[]; currentClip=0; elapsed=0;
  totalSecs = durSecs;
  clipDur = 8;

  // ── PASSO 0+1: Gerar letra e prompt via IA ──
  setStep(0, 'active', 'Pedindo à IA para compor a música...');
  setStep(1, 'active');

  const numLinhas = Math.ceil(durSecs / 4);

  const promptIA = `Você é um compositor profissional de músicas para videoclipes.

DADOS DO PROJETO:
- Tema: ${tema}
- Gênero: ${genero}
- Idioma: ${idioma}
- Mood: ${mood}
- Duração: ${durSecs} segundos

Responda SOMENTE com JSON válido, sem markdown, sem texto fora do JSON:

{
  "titulo": "título criativo da música",
  "letra": [
    {"linha": "frase curta da música"},
    {"linha": "outra frase"}
  ],
  "suno_prompt": "style prompt técnico em inglês para Suno Pro, máximo 80 palavras, com gênero, BPM, instrumentos, mood e referências de artistas",
  "pixabay_terms": ["term1 english","term2 english","term3 english","term4 english","term5 english","term6 english","term7 english","term8 english"]
}

A letra deve ter exatamente ${numLinhas} linhas curtas (máximo 6 palavras cada), sem marcadores como [Verso] ou [Refrão], prontas para aparecer na tela uma a uma como um clipe profissional.`;

  let titulo = tema, pixTerms = [], letra = [];

  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{ role: 'user', content: promptIA }]
      })
    });
    if (!res.ok) throw new Error('Erro na API: ' + res.status + '. Verifique sua conexão.');
    const data = await res.json();
    const raw = data.content.map(b => b.text || '').join('').trim();
    const clean = raw.replace(/```json|```/g, '').trim();
    const json = JSON.parse(clean);
    titulo = json.titulo || tema;
    letra = json.letra || [];
    sunoPrompt = json.suno_prompt || '';
    pixTerms = json.pixabay_terms || [];
    letraCompleta = letra.map(l => l.linha).join('\n');
  } catch(e) {
    mostrarErro('Erro ao gerar letra com IA: ' + e.message);
    return;
  }

  setStep(0, 'done');
  setStep(1, 'done', 'Letra e prompt do Suno criados!');

  // ── PASSO 2: Buscar vídeos no Pixabay ──
  setStep(2, 'active', 'Buscando vídeos no Pixabay...');

  const numClips = Math.ceil(totalSecs / clipDur);
  const fetchedClips = [];

  if (pxKey) {
    const allTerms = [...(pixTerms.length ? pixTerms : []), 'city night', 'forest nature', 'ocean waves', 'mountains sky', 'rain street', 'fire light'];
    for (let i = 0; i < Math.min(allTerms.length, numClips); i++) {
      try {
        const r = await fetch(`https://pixabay.com/api/videos/?key=${pxKey}&q=${encodeURIComponent(allTerms[i])}&video_type=film&per_page=5&min_width=1280`);
        if (r.ok) {
          const d = await r.json();
          if (d.hits && d.hits.length > 0) {
            const hit = d.hits[Math.floor(Math.random() * Math.min(3, d.hits.length))];
            const vid = hit.videos.medium || hit.videos.small || hit.videos.tiny;
            if (vid && vid.url) {
              fetchedClips.push({ url: vid.url, thumb: '', tag: allTerms[i] });
            }
          }
        }
      } catch(e2) { /* continua */ }
      await new Promise(r => setTimeout(r, 150));
    }
  }

  // Completar com demos se precisar
  while (fetchedClips.length < numClips) {
    const idx = fetchedClips.length % DEMO_URLS.length;
    const tag = pixTerms[fetchedClips.length % pixTerms.length] || 'demo';
    fetchedClips.push({ url: DEMO_URLS[idx], thumb: '', tag });
  }

  clips = fetchedClips.slice(0, numClips);
  setStep(2, 'done', clips.length + ' vídeos prontos!');

  // ── PASSO 3: Pré-carregar primeiro clipe ──
  setStep(3, 'active', 'Carregando primeiro clipe...');
  await preloadVideo(clips[0].url);
  setStep(3, 'done');

  // ── PASSO 4+5: Timeline e sincronização ──
  setStep(4, 'active', 'Montando timeline...');
  setStep(5, 'active', 'Sincronizando letra...');

  const linhas = letra.map(l => l.linha).filter(Boolean);
  const secsPerLine = totalSecs / linhas.length;
  lyrics = linhas.map((linha, i) => ({
    text: linha,
    start: i * secsPerLine,
    end: (i + 1) * secsPerLine - 0.3
  }));

  setStep(4, 'done');
  setStep(5, 'done', 'Tudo pronto! Iniciando clipe...');

  await new Promise(r => setTimeout(r, 600));
  renderPlayer(titulo);
}

// ─── PLAYER ─────────────────────────────────────────────────────────
function preloadVideo(url) {
  return new Promise(res => {
    const v = document.getElementById('main-video');
    v.src = url;
    v.oncanplay = () => res();
    v.onerror = () => res();
    setTimeout(res, 4000);
  });
}

function renderPlayer(titulo) {
  document.getElementById('hud-title').textContent = titulo.toUpperCase();
  document.getElementById('clip-total').textContent = clips.length;

  // Grid de cenas
  const grid = document.getElementById('clips-grid');
  grid.innerHTML = '';
  clips.forEach((c, i) => {
    const div = document.createElement('div');
    div.className = 'clip-thumb' + (i===0?' active':'');
    div.id = 'cthumb' + i;
    div.onclick = () => jumpToClip(i);
    div.innerHTML = `<div class="clip-icon">🎬</div><div class="clip-label">${c.tag}</div>`;
    grid.appendChild(div);
  });

  // Lista de letras
  const llist = document.getElementById('lyrics-list');
  llist.innerHTML = '';
  lyrics.forEach((l, i) => {
    const div = document.createElement('div');
    div.className = 'lyric-item';
    div.id = 'll' + i;
    div.textContent = l.text;
    div.onclick = () => { elapsed = l.start; updateLyrics(); };
    llist.appendChild(div);
  });

  setStage('player-wrap');
  loadClip(0);
  setTimeout(() => startPlay(), 500);
}

function loadClip(idx) {
  if (idx < 0 || idx >= clips.length) return;
  currentClip = idx;
  document.getElementById('clip-num').textContent = idx + 1;
  document.querySelectorAll('.clip-thumb').forEach((el, i) => {
    el.classList.toggle('active', i === idx);
  });
  const v = document.getElementById('main-video');
  v.src = clips[idx].url;
  v.loop = true;
  v.muted = true;
  if (playing) v.play().catch(() => {});
}

function jumpToClip(idx) {
  elapsed = idx * clipDur;
  loadClip(idx);
  if (!playing) startPlay();
}

function togglePlay() {
  playing ? pausePlay() : startPlay();
}

function startPlay() {
  document.getElementById('main-video').play().catch(() => {});
  playing = true;
  document.getElementById('play-btn').innerHTML = '&#9646;&#9646;';
  if (ticker) clearInterval(ticker);
  ticker = setInterval(tick, 100);
}

function pausePlay() {
  document.getElementById('main-video').pause();
  playing = false;
  document.getElementById('play-btn').innerHTML = '&#9654;';
  if (ticker) { clearInterval(ticker); ticker = null; }
}

function tick() {
  elapsed += 0.1;
  if (elapsed >= totalSecs) { elapsed = 0; loadClip(0); }
  const clipIdx = Math.floor(elapsed / clipDur);
  if (clipIdx !== currentClip && clipIdx < clips.length) loadClip(clipIdx);
  updateLyrics();
  updateProgress();
}

function updateLyrics() {
  const cur = lyrics.find(l => elapsed >= l.start && elapsed < l.end);
  const la = document.getElementById('lyric-a');
  if (cur) {
    la.textContent = cur.text;
    la.classList.add('visible');
    la.classList.remove('fade');
  } else {
    la.classList.remove('visible');
    la.classList.add('fade');
  }
  lyrics.forEach((l, i) => {
    const el = document.getElementById('ll'+i);
    if (el) el.classList.toggle('current', elapsed >= l.start && elapsed < l.end);
  });
  const curEl = document.querySelector('.lyric-item.current');
  if (curEl) curEl.scrollIntoView({ block: 'nearest', behavior: 'smooth' });
}

function updateProgress() {
  const pct = (elapsed / totalSecs * 100).toFixed(1);
  document.getElementById('main-prog').style.width = pct + '%';
  document.getElementById('time-disp').textContent = fmt(elapsed) + ' / ' + fmt(totalSecs);
}

function fmt(s) {
  const m = Math.floor(s/60), sec = Math.floor(s%60);
  return m + ':' + (sec < 10 ? '0' : '') + sec;
}

function prevClip() { elapsed = Math.max(0, currentClip-1) * clipDur; loadClip(Math.max(0, currentClip-1)); }
function nextClip() { const n = Math.min(clips.length-1, currentClip+1); elapsed = n * clipDur; loadClip(n); }

function setVol(v) {
  const vid = document.getElementById('main-video');
  vid.muted = false;
  vid.volume = parseFloat(v);
}

function copiarLetra() {
  copiarTexto(letraCompleta, 'Letra copiada! Cole no Suno Pro.');
}

function copiarPromptSuno() {
  copiarTexto(sunoPrompt, 'Prompt do Suno copiado!');
}

function copiarTexto(texto, msg) {
  navigator.clipboard.writeText(texto)
    .then(() => alert(msg))
    .catch(() => {
      const ta = document.createElement('textarea');
      ta.value = texto;
      document.body.appendChild(ta);
      ta.select();
      document.execCommand('copy');
      document.body.removeChild(ta);
      alert(msg);
    });
}
</script>
</body>
</html>
