# comparison26<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>電気代比較</title>
<style>
/* ============================================================
   CSS変数・テーマ
   ============================================================ */
:root {
  --bg:         #f0f4f8;
  --panel:      #dde6ef;
  --card:       #ffffff;
  --text:       #1e2532;
  --subtext:    #5a6475;
  --accent:     #1a5276;
  --accent-lt:  #2980b9;
  --border:     #c8d6e0;
  --tab-h:      56px;
  --radius:     10px;
  --shadow:     0 2px 10px rgba(0,0,0,0.08);

  /* 機種カラー */
  --c1: #2e5b88; --c1l: #7aaace;
  --c2: #1e6b45; --c2l: #68b88e;
  --c3: #8b2500; --c3l: #d4826a;
  --c4: #5b2d8e; --c4l: #a98dcb;
  --c5: #7a5500; --c5l: #d4aa4a;
}
[data-theme="gray"] {
  --bg:#f5f6f7; --panel:#e4e7ea; --accent:#3d4a5c; --accent-lt:#5a6d82; --border:#cdd3d9;
}
[data-theme="green"] {
  --bg:#f0f5f1; --panel:#d8eadc; --accent:#1a5c30; --accent-lt:#2e8b57; --border:#b8d8c0;
}

/* ============================================================
   リセット・ベース
   ============================================================ */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html, body { height: 100%; }
body {
  font-family: -apple-system, 'Helvetica Neue', Arial, 'Hiragino Sans', Meiryo, sans-serif;
  background: var(--bg);
  color: var(--text);
  font-size: 16px;
  line-height: 1.5;
  -webkit-tap-highlight-color: transparent;
}

/* ============================================================
   タブナビゲーション
   ============================================================ */
.tab-nav {
  display: flex;
  background: var(--card);
  border-bottom: 2px solid var(--border);
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: var(--shadow);
}
.tab-btn {
  flex: 1;
  height: var(--tab-h);
  border: none;
  background: none;
  font-size: 1rem;
  font-weight: 600;
  color: var(--subtext);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  border-bottom: 3px solid transparent;
  transition: color 0.2s, border-color 0.2s;
  -webkit-appearance: none;
}
.tab-btn.active {
  color: var(--accent);
  border-bottom-color: var(--accent);
}
.tab-btn:active { opacity: 0.7; }

/* ============================================================
   タブコンテンツ
   ============================================================ */
.tab-content { display: none; padding: 20px 16px 40px; max-width: 900px; margin: 0 auto; }
.tab-content.active { display: block; }

/* ============================================================
   セクションタイトル
   ============================================================ */
.sec-title {
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  color: var(--accent);
  text-transform: uppercase;
  margin-bottom: 10px;
  padding-bottom: 6px;
  border-bottom: 1px solid var(--border);
}

/* ============================================================
   設定タブ
   ============================================================ */
.settings-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 14px;
}
@media (max-width: 540px) { .settings-grid { grid-template-columns: 1fr; } }

.setting-card {
  background: var(--card);
  border-radius: var(--radius);
  padding: 16px;
  border: 1px solid var(--border);
  box-shadow: var(--shadow);
}
.setting-card.full { grid-column: 1 / -1; }

.setting-label {
  display: block;
  font-size: 0.82rem;
  font-weight: 700;
  color: var(--subtext);
  margin-bottom: 10px;
}
.setting-label span {
  font-weight: 800;
  color: var(--accent);
  font-size: 1rem;
}

/* セレクト・テキスト入力 */
select, input[type="text"] {
  width: 100%;
  padding: 12px 14px;
  border: 1.5px solid var(--border);
  border-radius: 8px;
  font-size: 1rem;
  background: #fff;
  color: var(--text);
  -webkit-appearance: none;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%235a6475' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 14px center;
}
input[type="text"] {
  background-image: none;
}
select:focus, input[type="text"]:focus {
  outline: none;
  border-color: var(--accent-lt);
}

/* スライダー */
input[type="range"] {
  width: 100%;
  -webkit-appearance: none;
  height: 6px;
  border-radius: 3px;
  background: var(--border);
  outline: none;
  margin-top: 4px;
}
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 26px;
  height: 26px;
  border-radius: 50%;
  background: var(--accent);
  cursor: pointer;
  box-shadow: 0 2px 6px rgba(0,0,0,0.2);
}

/* 季節ボタン */
.season-row { display: flex; gap: 8px; }
.season-btn { flex: 1; }
.season-btn input[type="checkbox"] { display: none; }
.season-btn span {
  display: block;
  text-align: center;
  padding: 12px 4px;
  border: 1.5px solid var(--border);
  border-radius: 8px;
  font-size: 0.95rem;
  font-weight: 600;
  background: #f8f9fa;
  cursor: pointer;
  transition: background 0.15s, color 0.15s;
  user-select: none;
}
.season-btn input:checked + span {
  background: var(--accent);
  color: #fff;
  border-color: var(--accent);
}

/* ============================================================
   比較タブ：入力エリア
   ============================================================ */
.years-card {
  background: var(--card);
  border-radius: var(--radius);
  padding: 16px 18px;
  border: 1px solid var(--border);
  box-shadow: var(--shadow);
  margin-bottom: 16px;
}
.years-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  margin-bottom: 10px;
}
.years-label { font-size: 0.9rem; font-weight: 700; }
.years-value { font-size: 1.6rem; font-weight: 800; color: var(--accent); }

.aircon-block {
  background: var(--card);
  border-radius: var(--radius);
  padding: 16px;
  margin-bottom: 12px;
  border: 1px solid var(--border);
  box-shadow: var(--shadow);
}
.aircon-block-title {
  font-size: 0.88rem;
  font-weight: 700;
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  gap: 8px;
}
.color-dot {
  width: 14px; height: 14px;
  border-radius: 4px;
  flex-shrink: 0;
}
.input-row { display: flex; gap: 10px; }
.input-cell { flex: 1; }
.input-cell label {
  display: block;
  font-size: 0.76rem;
  font-weight: 600;
  color: var(--subtext);
  margin-bottom: 5px;
}
input[type="number"] {
  width: 100%;
  padding: 12px 10px;
  border: 1.5px solid var(--border);
  border-radius: 8px;
  font-size: 1rem;
  background: #fff;
  color: var(--text);
  -webkit-appearance: none;
}
input[type="number"]:focus { outline: none; border-color: var(--accent-lt); }

/* ============================================================
   詳細オプション利用中バッジ
   ============================================================ */
.options-badge {
  display: none;
  align-items: center;
  gap: 6px;
  background: #fff8e1;
  border: 1px solid #f9a825;
  border-radius: 20px;
  padding: 5px 12px;
  font-size: 0.8rem;
  font-weight: 700;
  color: #7a5900;
  margin-bottom: 14px;
}
.options-badge.visible { display: flex; }

/* 警告バナー */
.warning-banner {
  display: none;
  background: #fff3f3;
  border: 1px solid #e74c3c;
  border-radius: 8px;
  padding: 10px 14px;
  font-size: 0.85rem;
  color: #922b21;
  margin-bottom: 14px;
}
.warning-banner.visible { display: block; }

/* ============================================================
   グラフエリア
   ============================================================ */
.result-card {
  background: var(--card);
  border-radius: var(--radius);
  padding: 20px 16px;
  border: 1px solid var(--border);
  box-shadow: var(--shadow);
  margin-top: 16px;
}
.result-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}
.result-title { font-size: 0.95rem; font-weight: 700; }

/* 全画面ボタン */
.btn-fullscreen {
  background: var(--accent);
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 8px 14px;
  font-size: 0.82rem;
  font-weight: 700;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 5px;
}
.btn-fullscreen:active { opacity: 0.8; }

/* 棒グラフ */
.chart-row { margin-bottom: 18px; }
.chart-model-label {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 5px;
  gap: 8px;
}
.chart-model-name {
  display: flex;
  align-items: center;
  gap: 7px;
  font-size: 0.88rem;
  font-weight: 700;
}
.chart-total {
  font-size: 0.9rem;
  font-weight: 800;
  color: var(--accent);
  white-space: nowrap;
}
.chart-bars { display: flex; flex-direction: column; gap: 5px; }
.chart-bar-row { display: flex; align-items: center; gap: 8px; }
.chart-bar-row-label {
  font-size: 0.72rem;
  color: var(--subtext);
  width: 48px;
  text-align: right;
  flex-shrink: 0;
}
.chart-bar-track {
  flex: 1;
  height: 20px;
  background: #edf0f3;
  border-radius: 5px;
  overflow: hidden;
}
.chart-bar-fill {
  height: 100%;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding-right: 7px;
  font-size: 0.68rem;
  color: #fff;
  font-weight: 700;
  white-space: nowrap;
  transition: width 0.4s ease;
  min-width: 0;
}

/* 凡例 */
.chart-legend {
  display: flex;
  gap: 16px;
  justify-content: flex-end;
  margin-top: 10px;
  font-size: 0.78rem;
  color: var(--subtext);
}
.legend-item { display: flex; align-items: center; gap: 5px; }
.legend-box { width: 14px; height: 14px; border-radius: 3px; flex-shrink: 0; }

/* サマリー */
.summary-card {
  background: var(--panel);
  border-radius: var(--radius);
  padding: 16px;
  margin-top: 16px;
}
.summary-row {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  padding: 8px 0;
  border-bottom: 1px dotted var(--border);
  gap: 8px;
}
.summary-row:last-child { border-bottom: none; }
.summary-model { font-size: 0.9rem; font-weight: 700; }
.summary-detail { font-size: 0.75rem; color: var(--subtext); margin-top: 2px; }
.summary-cost { font-size: 1rem; font-weight: 800; color: var(--accent); white-space: nowrap; }

.diff-card {
  background: #eafaf1;
  border: 1px solid #a9dfbf;
  border-radius: var(--radius);
  padding: 14px 16px;
  margin-top: 12px;
  font-size: 0.9rem;
}
.diff-amount { font-size: 1.2rem; font-weight: 800; color: #1a7a3c; }

/* ============================================================
   全画面グラフビュー
   ============================================================ */
#fullscreenView {
  display: none;
  position: fixed;
  inset: 0;
  background: var(--card);
  z-index: 200;
  overflow-y: auto;
  padding: 0;
}
#fullscreenView.active { display: block; }

.fullscreen-header {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 14px 16px;
  border-bottom: 1px solid var(--border);
  background: var(--card);
  position: sticky;
  top: 0;
  z-index: 10;
}
.btn-back {
  background: none;
  border: 1.5px solid var(--border);
  border-radius: 8px;
  padding: 8px 14px;
  font-size: 0.88rem;
  font-weight: 700;
  cursor: pointer;
  color: var(--text);
  display: flex;
  align-items: center;
  gap: 5px;
}
.btn-back:active { opacity: 0.7; }
.fullscreen-title { font-size: 1rem; font-weight: 700; }

.fullscreen-body { padding: 20px 16px 40px; max-width: 900px; margin: 0 auto; }

/* ============================================================
   空状態
   ============================================================ */
.empty-state {
  text-align: center;
  padding: 40px 20px;
  color: var(--subtext);
}
.empty-state p { font-size: 0.9rem; margin-top: 8px; }

/* ============================================================
   機種カラークラス
   ============================================================ */
.bg-c1 { background: var(--c1); }
.bg-c2 { background: var(--c2); }
.bg-c3 { background: var(--c3); }
.bg-c4 { background: var(--c4); }
.bg-c5 { background: var(--c5); }
.bglt-c1 { background: var(--c1l); }
.bglt-c2 { background: var(--c2l); }
.bglt-c3 { background: var(--c3l); }
.bglt-c4 { background: var(--c4l); }
.bglt-c5 { background: var(--c5l); }
</style>
</head>
<body>

<!-- タブナビ -->
<nav class="tab-nav">
  <button class="tab-btn active" onclick="switchTab('compare')" id="tab-compare">
    📊 比較
  </button>
  <button class="tab-btn" onclick="switchTab('settings')" id="tab-settings">
    ⚙️ 設定
  </button>
</nav>

<!-- ========== 設定タブ ========== -->
<div class="tab-content active" id="content-settings" style="display:none;">
  <div style="margin-bottom:16px;">
    <div class="sec-title">表示・比較設定</div>
  </div>

  <div class="settings-grid">

    <div class="setting-card">
      <label class="setting-label">比較機種数</label>
      <select id="deviceCount" onchange="onSettingChange()">
        <option value="2" selected>2機種</option>
        <option value="3">3機種</option>
        <option value="4">4機種</option>
        <option value="5">5機種</option>
      </select>
    </div>

    <div class="setting-card">
      <label class="setting-label">カラーテーマ</label>
      <select id="themeSelect" onchange="changeTheme(this.value); onSettingChange()">
        <option value="">標準（ブルー）</option>
        <option value="gray">スマートグレー</option>
        <option value="green">アースグリーン</option>
      </select>
    </div>

    <div class="setting-card full">
      <label class="setting-label">使用シーズン（複数選択可）</label>
      <div class="season-row">
        <label class="season-btn"><input type="checkbox" id="season_sp" onchange="onSettingChange()"><span>春</span></label>
        <label class="season-btn"><input type="checkbox" id="season_su" checked onchange="onSettingChange()"><span>夏</span></label>
        <label class="season-btn"><input type="checkbox" id="season_au" onchange="onSettingChange()"><span>秋</span></label>
        <label class="season-btn"><input type="checkbox" id="season_wi" checked onchange="onSettingChange()"><span>冬</span></label>
      </div>
    </div>

    <div class="setting-card full">
      <label class="setting-label">1日の使用時間：<span id="hoursDisplay">8</span> 時間</label>
      <input type="range" id="useHours" min="1" max="24" value="8" oninput="updateHoursText()">
    </div>

    <div class="setting-card">
      <label class="setting-label">建物の構造</label>
      <select id="buildingStructure" onchange="onSettingChange()">
        <option value="1.15">木造住宅</option>
        <option value="1.0">鉄筋コンクリート（RC）</option>
        <option value="0.95" selected>マンション</option>
      </select>
    </div>

    <div class="setting-card">
      <label class="setting-label">設置の向き（メモ）</label>
      <input type="text" id="placementDirection" placeholder="例：南向き、西日あり" oninput="onSettingChange()">
    </div>

  </div>

  <div style="margin-top:20px; display:flex; gap:12px; justify-content:center; flex-wrap:wrap;">
    <button class="btn-fullscreen" style="display:inline-flex;" onclick="switchTab('compare')">
      比較画面へ →
    </button>
    <button onclick="resetSettings()" style="display:inline-flex; align-items:center; gap:5px; background:#fff; color:#922b21; border:1.5px solid #e74c3c; border-radius:8px; padding:8px 14px; font-size:0.82rem; font-weight:700; cursor:pointer;">
      🔄 詳細オプションをリセット
    </button>
  </div>
</div>

<!-- ========== 比較タブ ========== -->
<div class="tab-content" id="content-compare" style="display:none;">

  <!-- 詳細オプション利用中バッジ -->
  <div class="options-badge" id="optionsBadge">
    ⚙ 詳細オプション利用中
  </div>

  <!-- 警告バナー -->
  <div class="warning-banner" id="warningBanner"></div>

  <!-- 使用期間スライダー -->
  <div class="years-card">
    <div class="years-header">
      <span class="years-label">使用期間</span>
      <span class="years-value" id="yearsDisplay">10年</span>
    </div>
    <input type="range" id="yearsRange" min="1" max="15" value="10" oninput="calculate()">
  </div>

  <!-- 機種入力 -->
  <div id="airconInputsContainer"></div>

  <!-- 結果グラフ -->
  <div class="result-card">
    <div class="result-header">
      <span class="result-title" id="resultTitle">10年間のコスト比較</span>
      <button class="btn-fullscreen" onclick="openFullscreen()">⛶ 全画面</button>
    </div>
    <div id="chartContainer">
      <div class="empty-state">
        <p>機種の情報を入力すると<br>グラフが表示されます</p>
      </div>
    </div>
    <div class="chart-legend" id="chartLegend" style="display:none;">
      <div class="legend-item"><div class="legend-box" style="background:#7aaace;"></div>本体料金</div>
      <div class="legend-item"><div class="legend-box" style="background:#1c3d5e;"></div>電気代累計</div>
    </div>
  </div>

  <!-- サマリー -->
  <div id="summaryContainer"></div>

</div>

<!-- ========== 全画面グラフビュー ========== -->
<div id="fullscreenView">
  <div class="fullscreen-header">
    <button class="btn-back" onclick="closeFullscreen()">← 戻る</button>
    <span class="fullscreen-title" id="fullscreenTitle">コスト比較</span>
  </div>
  <div class="fullscreen-body">
    <div id="fullscreenChartContainer"></div>
    <div class="chart-legend" style="margin-top:16px;">
      <div class="legend-item"><div class="legend-box" style="background:#7aaace;"></div>本体料金</div>
      <div class="legend-item"><div class="legend-box" style="background:#1c3d5e;"></div>電気代累計</div>
    </div>
    <div id="fullscreenSummary"></div>
  </div>
</div>

<script>
/* ============================================================
   状態管理
   ============================================================ */
const inputStore = {};

// デフォルト設定値（これと比較して変化があれば「詳細オプション利用中」）
const DEFAULTS = {
  deviceCount: '2',
  season_sp: false,
  season_su: true,
  season_au: false,
  season_wi: true,
  useHours: '8',
  buildingStructure: '0.95',
  placementDirection: '',
  themeSelect: ''
};

/* ============================================================
   タブ切り替え
   ============================================================ */
function switchTab(tab) {
  // 比較タブに戻るとき機種数変更を反映
  if (tab === 'compare') {
    rebuildAirconInputs();
    calculate();
  }

  document.getElementById('content-compare').style.display  = tab === 'compare'  ? 'block' : 'none';
  document.getElementById('content-settings').style.display = tab === 'settings' ? 'block' : 'none';
  document.getElementById('tab-compare').classList.toggle('active',  tab === 'compare');
  document.getElementById('tab-settings').classList.toggle('active', tab === 'settings');
}

/* ============================================================
   テーマ切り替え
   ============================================================ */
function changeTheme(val) {
  document.body.setAttribute('data-theme', val);
}

/* ============================================================
   時間スライダーのテキスト連動
   ============================================================ */
function updateHoursText() {
  document.getElementById('hoursDisplay').innerText = document.getElementById('useHours').value;
  onSettingChange();
}

/* ============================================================
   詳細オプション変更検知
   ============================================================ */
function onSettingChange() {
  const badge = document.getElementById('optionsBadge');
  const changed =
    document.getElementById('deviceCount').value        !== DEFAULTS.deviceCount ||
    document.getElementById('season_sp').checked        !== DEFAULTS.season_sp   ||
    document.getElementById('season_su').checked        !== DEFAULTS.season_su   ||
    document.getElementById('season_au').checked        !== DEFAULTS.season_au   ||
    document.getElementById('season_wi').checked        !== DEFAULTS.season_wi   ||
    document.getElementById('useHours').value           !== DEFAULTS.useHours    ||
    document.getElementById('buildingStructure').value  !== DEFAULTS.buildingStructure ||
    document.getElementById('placementDirection').value !== DEFAULTS.placementDirection ||
    document.getElementById('themeSelect').value        !== DEFAULTS.themeSelect;

  badge.classList.toggle('visible', changed);
  calculate();
}

/* ============================================================
   機種入力ブロック再構築（入力値を保持）
   ============================================================ */
function saveInputs() {
  const blocks = document.querySelectorAll('.aircon-block');
  blocks.forEach((_, i) => {
    const m = document.getElementById(`model_${i}`);
    const p = document.getElementById(`price_${i}`);
    const e = document.getElementById(`elec_${i}`);
    if (m) inputStore[`model_${i}`] = m.value;
    if (p) inputStore[`price_${i}`] = p.value;
    if (e) inputStore[`elec_${i}`]  = e.value;
  });
}

function rebuildAirconInputs() {
  saveInputs();
  const count = parseInt(document.getElementById('deviceCount').value);
  const container = document.getElementById('airconInputsContainer');
  container.innerHTML = '';

  const colorNames = ['深青', '深緑', '深赤', '深紫', '深金'];

  for (let i = 0; i < count; i++) {
    const sm = inputStore[`model_${i}`] ?? '';
    const sp = inputStore[`price_${i}`] ?? '';
    const se = inputStore[`elec_${i}`]  ?? '';

    const div = document.createElement('div');
    div.className = 'aircon-block';
    div.innerHTML = `
      <div class="aircon-block-title">
        <span class="color-dot bg-c${i+1}"></span>
        機種 ${i+1}
      </div>
      <div class="input-row" style="margin-bottom:10px;">
        <div class="input-cell">
          <label>型番・名称</label>
          <input type="text" id="model_${i}" value="${sm}" placeholder="例：AN226" oninput="calculate()">
        </div>
      </div>
      <div class="input-row">
        <div class="input-cell">
          <label>本体料金（円）</label>
          <input type="number" id="price_${i}" value="${sp}" placeholder="例：120000" inputmode="numeric" oninput="calculate()">
        </div>
        <div class="input-cell">
          <label>年間電気代（円）*必須</label>
          <input type="number" id="elec_${i}" value="${se}" placeholder="例：18000" inputmode="numeric" oninput="calculate()">
        </div>
      </div>
    `;
    container.appendChild(div);
  }
}

/* ============================================================
   計算ロジック
   ============================================================ */

// 季節ごとの負荷係数（日本平均気温ベース）
const SEASON_LOAD = { sp: 0.6, su: 1.3, au: 0.7, wi: 1.2 };
const SEASON_MONTHS = 3; // 各季節 3ヶ月

function isUsingCustomSettings() {
  return document.getElementById('optionsBadge').classList.contains('visible');
}

function calculate() {
  const count = parseInt(document.getElementById('deviceCount').value);
  const years = parseInt(document.getElementById('yearsRange').value);

  document.getElementById('yearsDisplay').innerText = years + '年';
  document.getElementById('resultTitle').innerText  = `${years}年間のコスト比較`;

  const useCustom = isUsingCustomSettings();

  // 補正係数計算
  let modifier = 1.0;
  let warnings = [];

  if (useCustom) {
    const useHours = parseFloat(document.getElementById('useHours').value);
    const structure = parseFloat(document.getElementById('buildingStructure').value);

    // 季節補正
    let seasonMod = 0;
    let checkedCount = 0;
    ['sp','su','au','wi'].forEach(s => {
      if (document.getElementById(`season_${s}`).checked) {
        seasonMod += SEASON_LOAD[s] * (SEASON_MONTHS / 12);
        checkedCount++;
      }
    });

    if (checkedCount === 0) {
      warnings.push('使用シーズンが選択されていません。');
      seasonMod = 1.0;
    }

    // 時間補正（家庭平均8時間基準）
    const hoursMod = useHours / 8;

    modifier = seasonMod * hoursMod * structure;
  }

  // 各機種データ取得・計算
  let results = [];
  let errs = [];

  for (let i = 0; i < count; i++) {
    const model    = (document.getElementById(`model_${i}`)?.value.trim()) || `機種 ${i+1}`;
    const priceRaw = document.getElementById(`price_${i}`)?.value ?? '';
    const elecRaw  = document.getElementById(`elec_${i}`)?.value  ?? '';

    if (elecRaw === '') { errs.push(`機種 ${i+1}：年間電気代が未入力`); continue; }
    if (priceRaw === '' || parseInt(priceRaw) === 0) { errs.push(`機種 ${i+1}：本体料金が未入力または0円`); continue; }

    const price = parseInt(priceRaw);
    const elec  = parseInt(elecRaw);
    const adjustedElec = Math.round(elec * modifier);
    const totalElec    = adjustedElec * years;
    const totalCost    = price + totalElec;

    results.push({ index: i, model, price, totalElec, totalCost });
  }

  // 警告表示
  const warnEl = document.getElementById('warningBanner');
  const allWarnings = [...warnings, ...errs];
  if (allWarnings.length > 0) {
    warnEl.textContent = '⚠ ' + allWarnings.join(' / ');
    warnEl.classList.add('visible');
  } else {
    warnEl.classList.remove('visible');
  }

  // グラフ描画
  renderChart(results, years);
}

/* ============================================================
   グラフ・サマリー描画
   ============================================================ */
function buildChartHTML(results, years) {
  if (results.length === 0) return { chart: '', summary: '' };

  const maxCost = Math.max(...results.map(r => r.totalCost), 1);
  const minCost = Math.min(...results.map(r => r.totalCost));
  const maxItem = results.reduce((a, b) => a.totalCost > b.totalCost ? a : b);
  const minItem = results.reduce((a, b) => a.totalCost < b.totalCost ? a : b);

  let chartHtml = '';
  let summaryHtml = '';

  results.forEach(res => {
    const ci = res.index + 1;
    const pw = Math.max((res.price / maxCost) * 100, 0).toFixed(1);
    const ew = Math.max((res.totalElec / maxCost) * 100, 0).toFixed(1);
    const pLabel = parseFloat(pw) > 14 ? res.price.toLocaleString() + '円' : '';
    const eLabel = parseFloat(ew) > 14 ? res.totalElec.toLocaleString() + '円' : '';

    chartHtml += `
      <div class="chart-row">
        <div class="chart-model-label">
          <div class="chart-model-name">
            <span class="color-dot bg-c${ci}"></span>
            ${res.model}
          </div>
          <span class="chart-total">${res.totalCost.toLocaleString()}円</span>
        </div>
        <div class="chart-bars">
          <div class="chart-bar-row">
            <div class="chart-bar-row-label">本体</div>
            <div class="chart-bar-track">
              <div class="chart-bar-fill bglt-c${ci}" style="width:${pw}%">${pLabel}</div>
            </div>
          </div>
          <div class="chart-bar-row">
            <div class="chart-bar-row-label">電気代</div>
            <div class="chart-bar-track">
              <div class="chart-bar-fill bg-c${ci}" style="width:${ew}%">${eLabel}</div>
            </div>
          </div>
        </div>
      </div>
    `;

    summaryHtml += `
      <div class="summary-row">
        <div>
          <div class="summary-model">${res.model}</div>
          <div class="summary-detail">本体 ${res.price.toLocaleString()}円 ＋ 電気代 ${res.totalElec.toLocaleString()}円</div>
        </div>
        <div class="summary-cost">${res.totalCost.toLocaleString()}円</div>
      </div>
    `;
  });

  // 差額カード
  let diffHtml = '';
  if (results.length >= 2) {
    const diff = maxItem.totalCost - minItem.totalCost;
    diffHtml = `
      <div class="diff-card">
        <div style="font-size:0.82rem; color:#2e7d52; margin-bottom:4px;">
          ${years}年間で最も安い <strong>${minItem.model}</strong> と 最も高い <strong>${maxItem.model}</strong> の差額
        </div>
        <div class="diff-amount">${diff.toLocaleString()}円</div>
      </div>
    `;
  }

  return { chart: chartHtml, summary: summaryHtml, diff: diffHtml };
}

function renderChart(results, years) {
  const chartContainer   = document.getElementById('chartContainer');
  const summaryContainer = document.getElementById('summaryContainer');
  const legendEl         = document.getElementById('chartLegend');

  if (results.length === 0) {
    chartContainer.innerHTML = `<div class="empty-state"><p>機種の情報を入力すると<br>グラフが表示されます</p></div>`;
    summaryContainer.innerHTML = '';
    legendEl.style.display = 'none';
    return;
  }

  const { chart, summary, diff } = buildChartHTML(results, years);
  chartContainer.innerHTML = chart;
  legendEl.style.display = 'flex';

  summaryContainer.innerHTML = `
    <div class="summary-card" style="margin-top:16px;">
      ${summary}
    </div>
    ${diff}
  `;
}

/* ============================================================
   全画面グラフ
   ============================================================ */
function openFullscreen() {
  const count = parseInt(document.getElementById('deviceCount').value);
  const years = parseInt(document.getElementById('yearsRange').value);

  // 現在の results を再計算
  const modifier = getCurrentModifier();
  let results = [];
  for (let i = 0; i < count; i++) {
    const model    = (document.getElementById(`model_${i}`)?.value.trim()) || `機種 ${i+1}`;
    const priceRaw = document.getElementById(`price_${i}`)?.value ?? '';
    const elecRaw  = document.getElementById(`elec_${i}`)?.value  ?? '';
    if (elecRaw === '' || priceRaw === '' || parseInt(priceRaw) === 0) continue;
    const price = parseInt(priceRaw);
    const elec  = parseInt(elecRaw);
    const totalElec = Math.round(elec * modifier) * years;
    const totalCost = price + totalElec;
    results.push({ index: i, model, price, totalElec, totalCost });
  }

  document.getElementById('fullscreenTitle').innerText = `${years}年間のコスト比較`;

  const { chart, summary, diff } = buildChartHTML(results, years);
  document.getElementById('fullscreenChartContainer').innerHTML = chart || '<div class="empty-state"><p>データがありません</p></div>';
  document.getElementById('fullscreenSummary').innerHTML = `
    <div class="summary-card" style="margin-top:16px;">${summary}</div>
    ${diff || ''}
  `;

  document.getElementById('fullscreenView').classList.add('active');
  document.body.style.overflow = 'hidden';
}

function closeFullscreen() {
  document.getElementById('fullscreenView').classList.remove('active');
  document.body.style.overflow = '';
}

function getCurrentModifier() {
  if (!isUsingCustomSettings()) return 1.0;
  const useHours = parseFloat(document.getElementById('useHours').value);
  const structure = parseFloat(document.getElementById('buildingStructure').value);
  let seasonMod = 0;
  ['sp','su','au','wi'].forEach(s => {
    if (document.getElementById(`season_${s}`).checked) {
      seasonMod += SEASON_LOAD[s] * (SEASON_MONTHS / 12);
    }
  });
  if (seasonMod === 0) seasonMod = 1.0;
  return seasonMod * (useHours / 8) * structure;
}

/* ============================================================
   詳細オプションリセット
   ============================================================ */
function resetSettings() {
  document.getElementById('deviceCount').value       = DEFAULTS.deviceCount;
  document.getElementById('season_sp').checked       = DEFAULTS.season_sp;
  document.getElementById('season_su').checked       = DEFAULTS.season_su;
  document.getElementById('season_au').checked       = DEFAULTS.season_au;
  document.getElementById('season_wi').checked       = DEFAULTS.season_wi;
  document.getElementById('useHours').value          = DEFAULTS.useHours;
  document.getElementById('hoursDisplay').innerText  = DEFAULTS.useHours;
  document.getElementById('buildingStructure').value = DEFAULTS.buildingStructure;
  document.getElementById('placementDirection').value = DEFAULTS.placementDirection;
  document.getElementById('themeSelect').value       = DEFAULTS.themeSelect;
  changeTheme('');
  onSettingChange();
  rebuildAirconInputs();
}

/* ============================================================
   初期化
   ============================================================ */
window.addEventListener('DOMContentLoaded', () => {
  rebuildAirconInputs();
  switchTab('compare');
});
</script>
</body>
</html>
