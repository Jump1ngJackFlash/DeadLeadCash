<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Dead Lead Cash Recovery Calculator</title>
  <style>
    :root {
      --bg: #0b1220;
      --panel: #111a2e;
      --text: #e9eefc;
      --muted: #a9b6d6;
      --border: rgba(233, 238, 252, 0.14);
      --accent: #7aa2ff;
      --warn: #ffd27a;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial;
      background: var(--bg);
      color: var(--text);
      padding: 32px 16px;
    }
    .wrap { max-width: 920px; margin: 0 auto; }
    h1 { font-size: 28px; margin-bottom: 8px; }
    p.sub { color: var(--muted); margin-bottom: 20px; }
    .grid { display: grid; gap: 16px; }
    @media (min-width: 860px) { .grid { grid-template-columns: 1.1fr 0.9fr; } }
    .card {
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 18px;
    }
    label { font-size: 13px; color: var(--muted); display: block; margin-bottom: 6px; }
    input, select {
      width: 100%;
      padding: 12px;
      border-radius: 12px;
      border: 1px solid var(--border);
      background: #0a1020;
      color: var(--text);
    }
    .row { display: grid; gap: 12px; margin-bottom: 14px; }
    @media (min-width: 540px) { .row.two { grid-template-columns: 1fr 1fr; } }
    .kpiBox {
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 14px;
      margin-bottom: 12px;
    }
    .kpiTitle { font-size: 12px; color: var(--muted); }
    .kpiValue { font-size: 22px; font-weight: 700; }
    .kpiRange { font-size: 13px; color: var(--muted); }
    .punch {
      border-left: 3px solid var(--warn);
      padding: 10px 12px;
      background: rgba(255,210,122,0.08);
      border-radius: 12px;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <div class="wrap">
    <h1>Dead Lead Cash Recovery Calculator</h1>
    <p class="sub">Estimate how much business value you are losing by not re-contacting existing leads.</p>

    <div class="grid">
      <div class="card">
        <h2>Inputs</h2>
        <div class="row two">
          <div>
            <label>Leads not contacted recently</label>
            <input id="leads" type="number" value="1000" />
          </div>
          <div>
            <label>Days since last contact</label>
            <input id="days" type="number" value="3" />
          </div>
        </div>
        <div class="row two">
          <div>
            <label>Lead quality</label>
            <select id="quality">
              <option value="old">1+ Year Old (3–4%)</option>
              <option value="mid" selected>3-Day Old (10–12%)</option>
              <option value="fresh">Fresh Google Ads (50%)</option>
            </select>
          </div>
          <div>
            <label>Business value per appointment ($)</label>
            <input id="value" type="number" value="300" />
          </div>
        </div>
      </div>

      <div class="card">
        <h2>Outputs</h2>
        <div class="kpiBox">
          <div class="kpiTitle">Missed appointments</div>
          <div class="kpiValue" id="apptExp">0</div>
          <div class="kpiRange" id="apptRange">Low 0 | High 0</div>
        </div>
        <div class="kpiBox">
          <div class="kpiTitle">Missed business value</div>
          <div class="kpiValue" id="valueExp">$0</div>
          <div class="kpiRange" id="valueRange">Low $0 | High $0</div>
        </div>
        <div class="punch" id="punch">Not contacting these leads is costing you $0.</div>
      </div>
    </div>
  </div>

  <script>
    const rates = {
      old: [0.03, 0.035, 0.04],
      mid: [0.10, 0.11, 0.12],
      fresh: [0.5, 0.5, 0.5]
    };

    const leads = document.getElementById('leads');
    const quality = document.getElementById('quality');
    const value = document.getElementById('value');
    const apptExp = document.getElementById('apptExp');
    const apptRange = document.getElementById('apptRange');
    const valueExp = document.getElementById('valueExp');
    const valueRange = document.getElementById('valueRange');
    const punch = document.getElementById('punch');

    function money(n) {
      return '$' + Math.round(n).toLocaleString();
    }

    function calc() {
      const l = Number(leads.value) || 0;
      const v = Number(value.value) || 0;
      const [lo, ex, hi] = rates[quality.value];

      const aLo = l * lo;
      const aEx = l * ex;
      const aHi = l * hi;

      const vLo = aLo * v;
      const vEx = aEx * v;
      const vHi = aHi * v;

      apptExp.textContent = Math.round(aEx);
      apptRange.textContent = `Low ${Math.round(aLo)} | High ${Math.round(aHi)}`;
      valueExp.textContent = money(vEx);
      valueRange.textContent = `Low ${money(vLo)} | High ${money(vHi)}`;
      punch.textContent = `Not contacting these leads is costing you about ${money(vEx)} in business value.`;
    }

    [leads, quality, value].forEach(el => el.addEventListener('input', calc));
    calc();
  </script>
</body>
</html>
