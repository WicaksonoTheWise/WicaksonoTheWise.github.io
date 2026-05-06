<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aisy Converter 📏</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg:      #FFF7ED;
      --surface: #FFFFFF;
      --primary: #FF6B35;
      --accent:  #FFD166;
      --dark:    #1A1A2E;
      --muted:   #9B8FA0;
      --border:  #F0E4D7;
    }
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      background: var(--bg);
      font-family: 'Syne', sans-serif;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 24px;
      overflow-x: hidden;
    }
    /* Decorative blobs */
    body::before, body::after {
      content: '';
      position: fixed;
      border-radius: 50%;
      filter: blur(80px);
      opacity: 0.35;
      pointer-events: none;
      z-index: 0;
    }
    body::before {
      width: 420px; height: 420px;
      background: var(--primary);
      top: -120px; right: -100px;
    }
    body::after {
      width: 320px; height: 320px;
      background: var(--accent);
      bottom: -80px; left: -80px;
    }
    .card {
      position: relative;
      z-index: 1;
      background: var(--surface);
      border: 2px solid var(--border);
      border-radius: 28px;
      padding: 48px 44px 44px;
      max-width: 480px;
      width: 100%;
      box-shadow: 8px 8px 0px var(--dark);
    }
    /* Header */
    .badge {
      display: inline-block;
      background: var(--accent);
      color: var(--dark);
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      padding: 4px 12px;
      border-radius: 100px;
      margin-bottom: 14px;
    }
    h1 {
      font-size: clamp(28px, 6vw, 36px);
      font-weight: 800;
      color: var(--dark);
      line-height: 1.15;
      margin-bottom: 6px;
    }
    h1 span { color: var(--primary); }
    .subtitle {
      font-size: 13px;
      color: var(--muted);
      font-family: 'DM Mono', monospace;
      margin-bottom: 36px;
    }
    .subtitle b { color: var(--primary); }
    /* Input group */
    .input-group {
      position: relative;
      margin-bottom: 20px;
    }
    .input-group label {
      display: block;
      font-size: 12px;
      font-weight: 700;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 8px;
    }
    .input-row {
      display: flex;
      gap: 10px;
      align-items: stretch;
    }
    input[type="number"] {
      flex: 1;
      border: 2px solid var(--border);
      border-radius: 14px;
      padding: 14px 18px;
      font-size: 20px;
      font-family: 'DM Mono', monospace;
      font-weight: 500;
      color: var(--dark);
      background: var(--bg);
      outline: none;
      transition: border-color 0.2s, box-shadow 0.2s;
      -moz-appearance: textfield;
    }
    input[type="number"]::-webkit-inner-spin-button,
    input[type="number"]::-webkit-outer-spin-button { -webkit-appearance: none; }
    input[type="number"]:focus {
      border-color: var(--primary);
      box-shadow: 4px 4px 0px var(--primary);
    }
    .unit-tag {
      display: flex;
      align-items: center;
      padding: 0 18px;
      background: var(--dark);
      color: var(--accent);
      font-family: 'DM Mono', monospace;
      font-size: 14px;
      font-weight: 500;
      border-radius: 14px;
      white-space: nowrap;
    }
    /* Convert button */
    .btn {
      width: 100%;
      padding: 16px;
      background: var(--primary);
      color: #fff;
      border: 2px solid var(--dark);
      border-radius: 14px;
      font-family: 'Syne', sans-serif;
      font-size: 16px;
      font-weight: 800;
      letter-spacing: 0.04em;
      cursor: pointer;
      box-shadow: 4px 4px 0px var(--dark);
      transition: transform 0.12s, box-shadow 0.12s;
      margin-bottom: 28px;
    }
    .btn:hover { transform: translate(-2px,-2px); box-shadow: 6px 6px 0px var(--dark); }
    .btn:active { transform: translate(2px,2px); box-shadow: 2px 2px 0px var(--dark); }
    /* Result box */
    .result-box {
      background: var(--dark);
      border-radius: 18px;
      padding: 28px 24px;
      text-align: center;
      min-height: 130px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      position: relative;
      overflow: hidden;
      transition: all 0.3s ease;
    }
    .result-box::before {
      content: '';
      position: absolute;
      inset: 0;
      background: repeating-linear-gradient(
        45deg,
        transparent,
        transparent 10px,
        rgba(255,255,255,0.015) 10px,
        rgba(255,255,255,0.015) 20px
      );
    }
    .result-label {
      font-size: 11px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--muted);
      font-family: 'DM Mono', monospace;
      margin-bottom: 10px;
    }
    .result-value {
      font-size: clamp(32px, 8vw, 48px);
      font-weight: 800;
      color: var(--accent);
      line-height: 1;
      transition: all 0.4s cubic-bezier(0.34,1.56,0.64,1);
    }
    .result-unit {
      font-size: 14px;
      color: rgba(255,255,255,0.5);
      font-family: 'DM Mono', monospace;
      margin-top: 8px;
    }
    .result-emoji {
      font-size: 28px;
      margin-top: 10px;
      display: block;
      transition: transform 0.3s ease;
    }
    /* Pop animation */
    @keyframes pop {
      0%   { transform: scale(0.85); opacity: 0; }
      70%  { transform: scale(1.08); }
      100% { transform: scale(1);   opacity: 1; }
    }
    .pop { animation: pop 0.4s cubic-bezier(0.34,1.56,0.64,1) forwards; }
    /* Fun fact strip */
    .fun-facts {
      margin-top: 20px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }
    .fact-chip {
      background: var(--bg);
      border: 1.5px solid var(--border);
      border-radius: 12px;
      padding: 12px 14px;
      font-size: 11px;
      color: var(--dark);
      font-family: 'DM Mono', monospace;
    }
    .fact-chip b { display: block; font-size: 16px; font-family: 'Syne', sans-serif; margin-bottom: 2px; }
    /* Footer */
    footer {
      margin-top: 24px;
      font-size: 11px;
      color: var(--muted);
      font-family: 'DM Mono', monospace;
      text-align: center;
      z-index: 1;
    }
    /* Shake on invalid */
    @keyframes shake {
      0%,100% { transform: translateX(0); }
      20%     { transform: translateX(-8px); }
      40%     { transform: translateX(8px); }
      60%     { transform: translateX(-6px); }
      80%     { transform: translateX(6px); }
    }
    .shake { animation: shake 0.4s ease; }
    /* Responsive */
    @media(max-width: 520px) {
      .card { padding: 32px 24px 28px; }
      .fun-facts { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

<div class="card">
  <span class="badge">✨ Satuan Eksklusif Exponent</span>
  <h1 id="cardTitle">CM → <span>Aisy</span></h1>
  <p class="subtitle">1 Aisy = <b>144.7 cm</b> tinggi badan Aisy</p>

  <div style="display:flex;justify-content:flex-end;margin-bottom:12px;">
    <button onclick="toggleMode()" id="modeBtn" style="
      background:transparent;
      border:2px solid var(--border);
      border-radius:100px;
      padding:6px 16px;
      font-family:'Syne',sans-serif;
      font-size:12px;
      font-weight:700;
      color:var(--muted);
      cursor:pointer;
      transition:all 0.2s;
    " onmouseover="this.style.borderColor='var(--primary)';this.style.color='var(--primary)'"
       onmouseout="this.style.borderColor='var(--border)';this.style.color='var(--muted)'">
      ⇄ Balik ke Aisy → CM
    </button>
  </div>

  <div class="input-group">
    <label id="inputLabel">Masukkan Panjang</label>
    <div class="input-row">
      <input type="number" id="cmInput" placeholder="misal: 170" min="0" step="any" />
      <span class="unit-tag" id="unitTag">cm</span>
    </div>
  </div>

  <button class="btn" id="convertBtn" onclick="convert()">🔁 Konversi ke Aisy!</button>

  <div class="result-box" id="resultBox">
    <p class="result-label">Hasil Konversi</p>
    <div class="result-value" id="resultValue">—</div>
    <div class="result-unit" id="resultUnit">masukkan nilai dulu ya 👆</div>
    <div style="display:flex;align-items:center;justify-content:center;gap:10px;margin-top:10px;">
      <span class="result-emoji" id="resultEmoji" style="margin-top:0;">📏</span>
      <span id="resultTag" style="display:none;font-family:'Syne',sans-serif;font-size:13px;font-weight:700;color:var(--dark);background:var(--accent);padding:4px 12px;border-radius:100px;white-space:nowrap;"></span>
    </div>
  </div>

  <div class="fun-facts" id="funFacts" style="display:none">
    <div class="fact-chip">
      <b id="factAisy">—</b> Aisy
    </div>
    <div class="fact-chip">
      <b id="factCm">—</b> cm input
    </div>
    <div class="fact-chip">
      <b id="factMeter">—</b> meter
    </div>
    <div class="fact-chip">
      <b id="factSisa">—</b> cm sisa
    </div>
  </div>
</div>

<footer>Dibuat oleh Biro Exponent HMDM FMIPA UI 2026</footer>

<script>
  const AISY = 144.7; // cm per 1 Aisy

  function getEmoji(aisy) {
    if (aisy < 0.5)  return '🐭';
    if (aisy < 1)    return '🐱';
    if (aisy < 1.5)  return '🙋';   // sekitar 1 Aisy
    if (aisy < 2)    return '🦒';
    if (aisy < 5)    return '🏠';
    if (aisy < 10)   return '🌴';
    if (aisy < 50)   return '🗼';
    if (aisy < 300)  return '🏔️';
    return '🌍';
  }

  function getLabel(aisy) {
    if (aisy < 0.95)                      return 'Kurcaci gila';
    if (aisy >= 0.95 && aisy <= 1.05)     return 'Ini mah aisy';
    if (aisy > 1.05 && aisy <= 1.1)       return 'tertantang secara vertikal';
    if (aisy > 1.1  && aisy <= 1.2)       return 'Normal';
    if (aisy > 1.2  && aisy <= 1.24)      return 'Cukup tinggi';
    if (aisy > 1.24 && aisy <= 1,5)       return 'Inimah Ezra';
    if (aisy > 1.5)                       return 'Inimah boong gila';
    return null; // tidak ada label untuk range lainnya
  }

  function convert() {
    const inp = document.getElementById('cmInput');
    const val = parseFloat(inp.value);
    const isCm2Aisy = mode === 'cm2aisy';

    if (isNaN(val) || val < 0) {
      inp.classList.remove('shake');
      void inp.offsetWidth; // reflow
      inp.classList.add('shake');
      document.getElementById('resultValue').textContent = '❌';
      document.getElementById('resultUnit').textContent = 'Input tidak valid!';
      document.getElementById('resultEmoji').textContent = '😅';
      document.getElementById('funFacts').style.display = 'none';
      return;
    }

    // Hitung nilai sesuai mode
    const aisy = isCm2Aisy ? val / AISY : val;
    const cm   = isCm2Aisy ? val        : val * AISY;

    const aisyStr = aisy < 0.01
      ? aisy.toFixed(6)
      : aisy < 1
      ? aisy.toFixed(4)
      : aisy.toFixed(3);

    const cmStr = cm.toFixed(2);

    const resultVal  = document.getElementById('resultValue');
    const resultUnit = document.getElementById('resultUnit');
    const resultEmoji= document.getElementById('resultEmoji');

    resultVal.textContent  = isCm2Aisy ? aisyStr : cmStr;
    resultUnit.textContent = isCm2Aisy ? 'Aisy'  : 'cm';
    resultEmoji.textContent = getEmoji(aisy);

    // Tampilkan label kontekstual di samping emoji
    const tag = document.getElementById('resultTag');
    const label = getLabel(aisy);
    if (label) {
      tag.textContent = label;
      tag.style.display = 'inline-block';
      tag.style.animation = 'none';
      void tag.offsetWidth;
      tag.style.animation = 'pop 0.4s cubic-bezier(0.34,1.56,0.64,1) forwards';
    } else {
      tag.style.display = 'none';
    }

    // Pop animation
    resultVal.classList.remove('pop');
    void resultVal.offsetWidth;
    resultVal.classList.add('pop');

    // Fun facts
    const bulat = Math.floor(aisy);
    const sisa  = (cm - bulat * AISY).toFixed(1);
    document.getElementById('factAisy').textContent  = aisyStr;
    document.getElementById('factCm').textContent    = cm.toFixed(2);
    document.getElementById('factMeter').textContent = (cm / 100).toFixed(2);
    document.getElementById('factSisa').textContent  = parseFloat(sisa) >= 0 ? sisa : 0;

    document.getElementById('funFacts').style.display = 'grid';
  }

  // Mode: 'cm2aisy' atau 'aisy2cm'
  let mode = 'cm2aisy';

  function toggleMode() {
    mode = (mode === 'cm2aisy') ? 'aisy2cm' : 'cm2aisy';
    const isCm2Aisy = mode === 'cm2aisy';

    document.getElementById('cardTitle').innerHTML  = isCm2Aisy ? 'CM → <span>Aisy</span>' : '<span>Aisy</span> → CM';
    document.getElementById('unitTag').textContent  = isCm2Aisy ? 'cm' : 'Aisy';
    document.getElementById('inputLabel').textContent = isCm2Aisy ? 'Masukkan Panjang' : 'Masukkan nilai Aisy';
    document.getElementById('convertBtn').textContent = isCm2Aisy ? '🔁 Konversi ke Aisy!' : '🔁 Konversi ke CM!';
    document.getElementById('modeBtn').textContent  = isCm2Aisy ? '⇄ Balik ke Aisy → CM' : '⇄ Balik ke CM → Aisy';
    document.getElementById('cmInput').placeholder  = isCm2Aisy ? 'misal: 170' : 'misal: 1.17';
    document.getElementById('cmInput').value = '';

    // Reset hasil
    document.getElementById('resultValue').textContent = '—';
    document.getElementById('resultUnit').textContent  = isCm2Aisy ? 'masukkan nilai dulu ya 👆' : 'masukkan nilai dulu ya 👆';
    document.getElementById('resultEmoji').textContent = '📏';
    document.getElementById('resultTag').style.display = 'none';
    document.getElementById('funFacts').style.display  = 'none';
  }

  // Enter key support
  document.getElementById('cmInput').addEventListener('keydown', e => {
    if (e.key === 'Enter') convert();
  });
</script>

<!-- ═══════════════════════════════════════════════════════════════
     SEKSI: Mengapa Satuan Aisy Itu Penting — versi static info
     ═══════════════════════════════════════════════════════════════ -->
<style>
  .latar-card {
    position: relative;
    z-index: 1;
    background: var(--dark);
    border: 2px solid rgba(255,255,255,0.08);
    border-radius: 28px;
    padding: 40px 44px;
    max-width: 480px;
    width: 100%;
    margin-top: 20px;
    box-shadow: 8px 8px 0px var(--primary);
  }

  .latar-title {
    font-size: clamp(18px, 5vw, 24px);
    font-weight: 800;
    color: #fff;
    margin-bottom: 20px;
    line-height: 1.2;
  }
  .latar-title span { color: var(--accent); }

  .latar-divider {
    height: 2px;
    background: linear-gradient(90deg, var(--primary), transparent);
    border-radius: 2px;
    margin-bottom: 24px;
  }

  .latar-body {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .latar-block {
    display: flex;
    gap: 14px;
    align-items: flex-start;
  }

  .latar-icon {
    font-size: 24px;
    flex-shrink: 0;
    margin-top: 2px;
    line-height: 1;
  }

  .latar-text h3 {
    font-size: 13px;
    font-weight: 800;
    color: var(--accent);
    letter-spacing: 0.06em;
    text-transform: uppercase;
    margin-bottom: 5px;
  }

  .latar-text p {
    font-size: 13px;
    font-family: 'DM Mono', monospace;
    color: rgba(255,255,255,0.7);
    line-height: 1.75;
  }

  .latar-text p b {
    color: #fff;
    font-family: 'Syne', sans-serif;
  }

  .latar-quote {
    margin-top: 8px;
    padding: 16px 20px;
    background: rgba(255,209,102,0.08);
    border-left: 3px solid var(--accent);
    border-radius: 0 12px 12px 0;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    font-style: italic;
    color: var(--accent);
    line-height: 1.7;
  }

  @media(max-width: 520px) {
    .latar-card { padding: 28px 22px; }
  }
</style>

<div class="latar-card">
  <h2 class="latar-title">Mengapa Satuan <span>Aisy</span> Itu Penting?</h2>
  <div class="latar-divider"></div>

  <div class="latar-body">
    <div class="latar-block">
      <div class="latar-icon">📐</div>
      <div class="latar-text">
        <h3>LATAR BELAKANG</h3>
        <p>Pada suatu hari yang biasa, muncul pertanyaan besar: <b>"seberapa panjang itu sebenarnya?"</b> Meter terasa terlalu abstrak untuk keseharian di Matek. Kaki dan inci terlalu kolonial. Maka lahirlah satuan BARU BANGET <b>Aisy</b> yang berdasarkan tinggi badan Aisy yang tepatnya <b>144,7 cm</b> cocok sebagai sebuah referensi nyata, manusiawi, dan bisa dibayangin langsung (lihat aja orangnya).</p>
      </div>
    </div>
    <div class="latar-block">
      <div class="latar-icon">🧠</div>
      <div class="latar-text">
        <h3>Lebih Masuk Akal aja</h3>
        <p>Kalau ada yang bilang pohon itu <b>"3 meter"</b>, kamu harus mikir dulu. Tapi kalau ada yang bilang pohon itu <b>"2 Aisy"</b>, kamu langsung bisa bayangin: itu dua kali tingginya Aisy, terus mikir "cukup tinggi, tapi masih bisa diajak foto bareng."</p>
      </div>
    </div>
    <div class="latar-block">
      <div class="latar-icon">🌍</div>
      <div class="latar-text">
        <h3>Satuan yang dibuat dari Iblis MATEK</h3>
        <p>Berbeda dari meter yang diciptakan berdasarkan keliling bumi (siapa yang relate?), satuan Aisy diciptakan berdasarkan seseorang yang <b>nyata, dikenal, dan bisa dijumpai langsung</b>.</p>
      </div>
    </div>
    <div class="latar-block">
      <div class="latar-icon">📊</div>
      <div class="latar-text">
        <h3>Skala yang Lebih Relevan</h3>
        <p>Sebagian besar benda di kehidupan sehari-hari berada di rentang <b>0,01 hingga 10 Aisy</b> — dari pulpen sampai gedung bertingkat. Satuan ini ternyata pas banget untuk mendeskripsikan dunia di sekitar kita tanpa harus pakai notasi ilmiah. Meter overrated bro.</p>
      </div>
    </div>
    <div class="latar-quote">
      Ayo normalisasi penggunaan Aisy sekarang juga.
    </div>
  </div>
</div>
</body>
</html>
