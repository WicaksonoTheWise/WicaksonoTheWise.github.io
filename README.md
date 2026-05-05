<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aisy Converter 📏</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet" />
  <style>
    :root{
      --bg:      #FFF7ED;
      --surface: #FFFFFF;
      --primary: #FF6B35;
      --accent:  #FFD166;
      --dark:    #1A1A2E;
      --muted:   #9B8FA0;
      --border:  #F0E4D7;}
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
  <h1>CM → <span>Aisy</span></h1>
  <p class="subtitle">1 Aisy = <b>144.7 cm</b> tinggi badan Aisy</p>
  <div class="input-group">
    <label>Masukkan Panjang</label>
    <div class="input-row">
      <input type="number" id="cmInput" placeholder="misal: 170" min="0" step="any" />
      <span class="unit-tag">cm</span>
    </div>
  </div>
  <button class="btn" onclick="convert()">🔁 Konversi ke Aisy!</button>

  <div class="result-box" id="resultBox">
    <p class="result-label">Hasil Konversi</p>
    <div class="result-value" id="resultValue">—</div>
    <div class="result-unit" id="resultUnit">masukkan nilai dulu ya 👆</div>
    <span class="result-emoji" id="resultEmoji">📏</span>
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

  function convert() {
    const inp = document.getElementById('cmInput');
    const val = parseFloat(inp.value);

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

    const aisy = val / AISY;

    // Format: kalau bilangan besar tampilkan 2 desimal, kecil 4 desimal
    const aisyStr = aisy < 0.01
      ? aisy.toFixed(6)
      : aisy < 1
      ? aisy.toFixed(4)
      : aisy.toFixed(3);

    const resultVal  = document.getElementById('resultValue');
    const resultUnit = document.getElementById('resultUnit');
    const resultEmoji= document.getElementById('resultEmoji');

    resultVal.textContent  = aisyStr;
    resultUnit.textContent = 'Aisy';
    resultEmoji.textContent = getEmoji(aisy);

    // Pop animation
    resultVal.classList.remove('pop');
    void resultVal.offsetWidth;
    resultVal.classList.add('pop');

    // Fun facts
    const bulat = Math.floor(aisy);
    const sisa  = (val - bulat * AISY).toFixed(1);
    document.getElementById('factAisy').textContent  = aisyStr;
    document.getElementById('factCm').textContent    = val.toLocaleString('id-ID');
    document.getElementById('factMeter').textContent = (val / 100).toFixed(2);
    document.getElementById('factSisa').textContent  = sisa >= 0 ? sisa : 0;

    document.getElementById('funFacts').style.display = 'grid';
  }

  // Enter key support
  document.getElementById('cmInput').addEventListener('keydown', e => {
    if (e.key === 'Enter') convert();
  });
</script>
</body>
</html>
