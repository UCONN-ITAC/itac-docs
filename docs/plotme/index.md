---
hide:
  - toc
  - navigation
---

# PlotME — Plot My Energy

Upload ITAC assessment CSV data and build interactive, publication-ready graphs. All Plotly controls are enabled. The **Download PNG** toolbar button always exports in light mode regardless of your current theme.

**Features:** multi-series line, scatter & histogram · dual Y-axis · datetime auto-detection · linear data transforms · moving average · trend lines · log scale

---

<div id="plotme" style="max-width: 1100px; margin: 20px auto; font-size: 0.95em;">

<!-- ══════════════ STEP 1: UPLOAD ══════════════ -->
<div style="margin-bottom: 18px; padding: 20px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 8px; background: var(--md-code-bg-color);">
  <h3 style="margin-top: 0;">Step 1: Upload CSV File</h3>
  <div style="display: flex; align-items: center; gap: 14px; flex-wrap: wrap;">
    <label for="pmFile" style="display: inline-block; padding: 10px 22px; background: #4051b5; color: white; border-radius: 4px; cursor: pointer; font-weight: 500; white-space: nowrap;">
      Choose CSV File
    </label>
    <input type="file" id="pmFile" accept=".csv" style="display: none;">
    <span id="pmFileName" style="color: var(--md-default-fg-color--light);">No file chosen</span>
  </div>
  <div id="pmPreview" style="display: none; margin-top: 16px;"></div>
</div>

<!-- ══════════════ STEP 2: CHART TYPE ══════════════ -->
<div id="pmStep2" style="display: none; margin-bottom: 18px; padding: 20px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 8px; background: var(--md-code-bg-color);">
  <h3 style="margin-top: 0;">Step 2: Select Chart Type</h3>
  <div style="display: flex; gap: 12px; flex-wrap: wrap;">
    <button id="pmBtnLine"      onclick="pmSelectType('line')"      style="padding: 14px 22px; border: 2px solid var(--md-default-fg-color--lightest); border-radius: 6px; background: transparent; color: var(--md-default-fg-color); cursor: pointer; font-size: 0.95em; flex: 1; min-width: 120px;">📈 Line</button>
    <button id="pmBtnScatter"   onclick="pmSelectType('scatter')"   style="padding: 14px 22px; border: 2px solid var(--md-default-fg-color--lightest); border-radius: 6px; background: transparent; color: var(--md-default-fg-color); cursor: pointer; font-size: 0.95em; flex: 1; min-width: 120px;">● Scatter</button>
    <button id="pmBtnHistogram" onclick="pmSelectType('histogram')" style="padding: 14px 22px; border: 2px solid var(--md-default-fg-color--lightest); border-radius: 6px; background: transparent; color: var(--md-default-fg-color); cursor: pointer; font-size: 0.95em; flex: 1; min-width: 120px;">▬ Histogram</button>
  </div>
</div>

<!-- ══════════════ STEP 3: CONFIGURE ══════════════ -->
<div id="pmStep3" style="display: none; margin-bottom: 18px; padding: 20px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 8px; background: var(--md-code-bg-color);">
  <h3 style="margin-top: 0;">Step 3: Configure Columns</h3>
  <div id="pmConfigInner"></div>
  <button onclick="pmPlot()" style="margin-top: 18px; padding: 12px 30px; background: #4051b5; color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 1em; font-weight: 500;">Generate Chart</button>
</div>

<!-- ══════════════ STEP 4: CHART ══════════════ -->
<div id="pmStep4" style="display: none; margin-bottom: 18px; padding: 20px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 8px; background: var(--md-code-bg-color);">
  <h3 style="margin-top: 0;">Step 4: Chart</h3>
  <div id="pmPlotDiv" style="height: 520px; width: 100%;"></div>
</div>

<!-- ══════════════ STEP 5: CUSTOMIZE ══════════════ -->
<div id="pmStep5" style="display: none; padding: 20px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 8px; background: var(--md-code-bg-color);">
  <h3 style="margin-top: 0;">Step 5: Customize</h3>
  <div id="pmCustomize"></div>
  <button onclick="pmPlot()" style="margin-top: 18px; padding: 10px 26px; background: #4051b5; color: white; border: none; border-radius: 4px; cursor: pointer; font-weight: 500;">Update Chart</button>
</div>

</div><!-- /#plotme -->

<script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>
<script>
(function () {
'use strict';

// ─── PALETTE ─────────────────────────────────────────────────────────────────
const PM_COLORS = ['#4051b5','#4caf50','#f44336','#ff9800','#9c27b0','#00bcd4','#795548','#e91e63','#607d8b','#8bc34a'];

// ─── STATE ───────────────────────────────────────────────────────────────────
const pm = {
  headers: [], rows: [], colTypes: [],
  chartType: '',
  title: '', xLabel: '', yLabel: '', y2Label: '',
  xScale: 'linear', yScale: 'linear', y2Scale: 'linear',
  histnorm: '', histBarmode: 'overlay',
};

let ySeriesIdCounter    = 0;
let histSeriesIdCounter = 0;

// ─── THEME COLORS ────────────────────────────────────────────────────────────
function isDarkMode() {
  const scheme = document.documentElement.getAttribute('data-md-color-scheme')
              || document.body.getAttribute('data-md-color-scheme') || '';
  return scheme === 'slate';
}

function getPlotColors() {
  if (isDarkMode()) {
    return {
      fg:   'rgba(255,255,255,0.87)',
      fgL:  'rgba(255,255,255,0.54)',
      bg:   'rgba(0,0,0,0)',
      grid: 'rgba(255,255,255,0.12)',
    };
  }
  return {
    fg:   '#222222',
    fgL:  '#666666',
    bg:   'rgba(0,0,0,0)',
    grid: 'rgba(0,0,0,0.10)',
  };
}

const LIGHT = {
  fg: '#222222', bg: '#ffffff', grid: 'rgba(0,0,0,0.10)',
  zeroLine: 'rgba(0,0,0,0.20)',
};

// Watch for dark/light mode toggle and update chart colors live
const pmThemeObserver = new MutationObserver(function () {
  const plotDiv = document.getElementById('pmPlotDiv');
  if (!plotDiv._fullLayout) return;
  const c = getPlotColors();
  try {
    Plotly.relayout('pmPlotDiv', {
      paper_bgcolor: c.bg, plot_bgcolor: c.bg,
      'font.color':         c.fg,
      'xaxis.color':        c.fg,  'xaxis.gridcolor':  c.grid,
      'yaxis.color':        c.fg,  'yaxis.gridcolor':  c.grid,
      'yaxis2.color':       c.fg,  'yaxis2.gridcolor': c.grid,
      'legend.bgcolor':     c.bg,  'legend.bordercolor': c.grid,
      'legend.font.color':  c.fg,
    });
  } catch (_) {}
});
pmThemeObserver.observe(document.documentElement, { attributes: true, attributeFilter: ['data-md-color-scheme'] });
pmThemeObserver.observe(document.body, { attributes: true, attributeFilter: ['data-md-color-scheme'] });

// ─── HELPERS ─────────────────────────────────────────────────────────────────
function iStyle(extra) {
  return 'width:100%;padding:7px 8px;border:1px solid var(--md-default-fg-color--lightest);border-radius:4px;background:var(--md-default-bg-color);color:var(--md-default-fg-color);box-sizing:border-box;' + (extra || '');
}

function makeColOptions(selectedIdx) {
  return pm.headers.map((h, i) =>
    `<option value="${i}" ${i === selectedIdx ? 'selected' : ''}>[${pm.colTypes[i][0].toUpperCase()}] ${h}</option>`
  ).join('');
}

// ─── DATETIME NORMALIZATION ──────────────────────────────────────────────────
// Converts any common date format to YYYY-MM-DDTHH:MM:SS for Plotly
function toPlotlyDate(v) {
  if (!v) return null;
  v = String(v).trim();

  // Already ISO: YYYY-MM-DDTHH... or YYYY-MM-DD HH...
  if (/^\d{4}-\d{2}-\d{2}T/.test(v)) return v;
  if (/^\d{4}-\d{2}-\d{2} \d{2}:/.test(v)) return v.replace(' ', 'T');
  if (/^\d{4}-\d{2}-\d{2}$/.test(v)) return v + 'T00:00:00';

  // MM/DD/YYYY HH:MM:SS  (most common ITAC logger format)
  const mdy = v.match(/^(\d{1,2})\/(\d{1,2})\/(\d{4})(?:[T ](\d{2}):(\d{2})(?::(\d{2}))?)?/);
  if (mdy) {
    const [, mo, dy, yr, hh = '00', mm = '00', ss = '00'] = mdy;
    return `${yr}-${mo.padStart(2,'0')}-${dy.padStart(2,'0')}T${hh}:${mm}:${ss}`;
  }

  // YYYY/MM/DD ...
  const ymd = v.match(/^(\d{4})\/(\d{2})\/(\d{2})(?:[T ](\d{2}):(\d{2})(?::(\d{2}))?)?/);
  if (ymd) {
    const [, yr, mo, dy, hh = '00', mm = '00', ss = '00'] = ymd;
    return `${yr}-${mo}-${dy}T${hh}:${mm}:${ss}`;
  }

  // Fallback: JS Date (handles many RFC/HTTP formats)
  const d = new Date(v);
  if (!isNaN(d)) return d.toISOString().slice(0, 19);

  return v; // pass through and let Plotly complain
}

function isDatetimeLike(v) {
  if (/^\d{4}-\d{2}-\d{2}[T ]/.test(v)) return true;
  if (/^\d{1,2}\/\d{1,2}\/\d{4}/.test(v)) return true;
  if (/^\d{4}\/\d{2}\/\d{2}/.test(v)) return true;
  return false;
}

// ─── DATA HELPERS ─────────────────────────────────────────────────────────────
function getColValues(ci, forceNumeric) {
  const isNum = pm.colTypes[ci] === 'numeric';
  const isDT  = pm.colTypes[ci] === 'datetime';
  return pm.rows.map(r => {
    const v = (r[ci] ?? '').trim();
    if (forceNumeric || isNum) return parseFloat(v);
    if (isDT) return toPlotlyDate(v);
    return v;
  });
}

function applyTransform(vals, scale, offset) {
  const s = isFinite(scale)  ? scale  : 1;
  const o = isFinite(offset) ? offset : 0;
  if (s === 1 && o === 0) return vals;
  return vals.map(v => (typeof v === 'number' && !isNaN(v)) ? v * s + o : v);
}

function movingAverage(arr, win) {
  const half = Math.floor(win / 2);
  return arr.map((_, i) => {
    const s = Math.max(0, i - half), e = Math.min(arr.length, s + win);
    const sl = arr.slice(s, e).filter(v => typeof v === 'number' && !isNaN(v));
    return sl.length ? sl.reduce((a, b) => a + b, 0) / sl.length : NaN;
  });
}

function linearRegression(xArr, yArr) {
  let n = 0, sx = 0, sy = 0, sxy = 0, sx2 = 0;
  for (let i = 0; i < xArr.length; i++) {
    const x = xArr[i], y = yArr[i];
    if (!isFinite(x) || !isFinite(y)) continue;
    sx += x; sy += y; sxy += x * y; sx2 += x * x; n++;
  }
  if (n < 2) return null;
  const m = (n * sxy - sx * sy) / (n * sx2 - sx * sx);
  const b = (sy - m * sx) / n;
  return { m, b };
}

// ─── STEP 1: FILE LOAD ───────────────────────────────────────────────────────
document.getElementById('pmFile').addEventListener('change', function () {
  if (!this.files[0]) return;
  document.getElementById('pmFileName').textContent = this.files[0].name;
  const reader = new FileReader();
  reader.onload = e => pmParseCSV(e.target.result);
  reader.readAsText(this.files[0]);
});

function parseCSVLine(line) {
  const result = []; let cur = '', inQ = false;
  for (let i = 0; i < line.length; i++) {
    const c = line[i];
    if (c === '"') {
      if (inQ && line[i + 1] === '"') { cur += '"'; i++; }
      else inQ = !inQ;
    } else if (c === ',' && !inQ) {
      result.push(cur.trim()); cur = '';
    } else cur += c;
  }
  result.push(cur.trim());
  return result;
}

function pmParseCSV(text) {
  const lines = text.split(/\r?\n/).filter(l => l.trim());
  if (lines.length < 2) { alert('CSV needs at least a header row and one data row.'); return; }

  pm.headers = parseCSVLine(lines[0]);
  pm.rows    = lines.slice(1).map(parseCSVLine);

  pm.colTypes = pm.headers.map((_, ci) => {
    const vals = pm.rows.map(r => (r[ci] ?? '').trim()).filter(v => v !== '');
    if (!vals.length) return 'string';
    const numOk = vals.filter(v => !isNaN(parseFloat(v)) && isFinite(+v)).length;
    if (numOk / vals.length >= 0.8) return 'numeric';
    // Use pattern-based detection — more reliable than Date.parse across browsers/formats
    const dtOk = vals.filter(isDatetimeLike).length;
    if (dtOk / vals.length >= 0.8) return 'datetime';
    return 'string';
  });

  renderPreview();
  document.getElementById('pmStep2').style.display = 'block';
  ['pmStep3','pmStep4','pmStep5'].forEach(id => document.getElementById(id).style.display = 'none');
  ySeriesIdCounter = histSeriesIdCounter = 0;
}

function colStats(ci) {
  const vals = pm.rows.map(r => parseFloat(r[ci])).filter(v => !isNaN(v));
  if (!vals.length) return '';
  const mn = Math.min(...vals), mx = Math.max(...vals);
  const avg = vals.reduce((a, b) => a + b, 0) / vals.length;
  const std = Math.sqrt(vals.reduce((a, b) => a + (b - avg) ** 2, 0) / vals.length);
  return `min ${mn.toPrecision(4)} · max ${mx.toPrecision(4)} · avg ${avg.toPrecision(4)} · σ ${std.toPrecision(3)}`;
}

function renderPreview() {
  const maxCols = Math.min(pm.headers.length, 8);
  const maxRows = Math.min(pm.rows.length, 6);
  const badge = t => {
    const c = t === 'numeric' ? '#4caf50' : t === 'datetime' ? '#4051b5' : '#ff9800';
    return `<span style="font-size:0.75em;font-weight:400;color:${c};">${t}</span>`;
  };
  let html = `<p style="margin:0 0 10px;font-size:0.9em;color:var(--md-default-fg-color--light);">
    <strong>${pm.rows.length}</strong> rows &times; <strong>${pm.headers.length}</strong> columns.
    ${pm.headers.length > 8 ? '&nbsp;Showing first 8.' : ''}
  </p><div style="overflow-x:auto;"><table style="border-collapse:collapse;width:100%;font-size:0.83em;"><thead><tr>`;
  for (let ci = 0; ci < maxCols; ci++) {
    html += `<th style="padding:6px 10px;text-align:left;border-bottom:2px solid var(--md-default-fg-color--lightest);white-space:nowrap;">
      ${pm.headers[ci]}<br>${badge(pm.colTypes[ci])}
      ${pm.colTypes[ci] === 'numeric' ? `<br><span style="font-size:0.72em;color:var(--md-default-fg-color--light);font-weight:400;">${colStats(ci)}</span>` : ''}
    </th>`;
  }
  html += '</tr></thead><tbody>';
  for (let ri = 0; ri < maxRows; ri++) {
    html += '<tr>';
    for (let ci = 0; ci < maxCols; ci++) {
      html += `<td style="padding:5px 10px;border-bottom:1px solid var(--md-default-fg-color--lightest);white-space:nowrap;max-width:180px;overflow:hidden;text-overflow:ellipsis;">${(pm.rows[ri] ?? [])[ci] ?? ''}</td>`;
    }
    html += '</tr>';
  }
  html += '</tbody></table></div>';
  if (pm.rows.length > maxRows) html += `<p style="margin:6px 0 0;font-size:0.8em;color:var(--md-default-fg-color--light);">&hellip; and ${pm.rows.length - maxRows} more rows</p>`;
  const preview = document.getElementById('pmPreview');
  preview.innerHTML = html;
  preview.style.display = 'block';
}

// ─── STEP 2: CHART TYPE ───────────────────────────────────────────────────────
window.pmSelectType = function (type) {
  pm.chartType = type;
  ['line','scatter','histogram'].forEach(t => {
    const btn = document.getElementById('pmBtn' + t.charAt(0).toUpperCase() + t.slice(1));
    btn.style.borderColor = t === type ? '#4051b5' : 'var(--md-default-fg-color--lightest)';
    btn.style.background  = t === type ? 'rgba(64,81,181,0.10)' : 'transparent';
  });
  renderConfig();
  document.getElementById('pmStep3').style.display = 'block';
  document.getElementById('pmStep4').style.display = 'none';
  document.getElementById('pmStep5').style.display = 'none';
};

// ─── STEP 3: CONFIG ───────────────────────────────────────────────────────────
function renderConfig() {
  const inner = document.getElementById('pmConfigInner');
  if (pm.chartType === 'histogram') renderHistConfig(inner);
  else                               renderXYConfig(inner);
}

// Shared transform sub-row injected into every series card
function transformRow(scaleId, offsetId) {
  const si = iStyle('width:72px;');
  return `
    <div style="display:flex;gap:20px;margin-top:10px;padding-top:10px;border-top:1px solid var(--md-default-fg-color--lightest);align-items:center;flex-wrap:wrap;">
      <label style="font-size:0.85em;display:flex;align-items:center;gap:6px;">
        Scale &times;
        <input type="number" id="${scaleId}" value="1" step="any" style="${si}">
      </label>
      <label style="font-size:0.85em;display:flex;align-items:center;gap:6px;">
        Offset +
        <input type="number" id="${offsetId}" value="0" step="any" style="${si}">
      </label>
      <span style="font-size:0.78em;color:var(--md-default-fg-color--light);">result = (raw &times; scale) + offset</span>
    </div>`;
}

function renderXYConfig(inner) {
  const dtIdx   = pm.colTypes.findIndex(t => t === 'datetime');
  const defaultX = dtIdx >= 0 ? dtIdx : 0;
  inner.innerHTML = `
    <p style="margin:0 0 14px;font-size:0.9em;color:var(--md-default-fg-color--light);">
      Choose an X column, then add one or more Y series. Assign each to the left (Y1) or right (Y2) axis.
    </p>
    <div style="margin-bottom:14px;">
      <label style="display:block;margin-bottom:4px;font-weight:500;">X Axis Column</label>
      <select id="pmXCol" style="${iStyle()}max-width:320px;">${makeColOptions(defaultX)}</select>
    </div>
    <div>
      <strong>Y Series</strong>
      <div id="pmYSeriesContainer" style="margin-top:10px;"></div>
      <button onclick="pmAddYSeries()" style="margin-top:8px;padding:8px 16px;background:#4caf50;color:white;border:none;border-radius:4px;cursor:pointer;">+ Add Series</button>
    </div>`;
  pmAddYSeries();
}

window.pmAddYSeries = function () {
  const id    = ySeriesIdCounter++;
  const color = PM_COLORS[id % PM_COLORS.length];
  const xVal  = parseInt((document.getElementById('pmXCol') || {}).value || '0');
  const defY  = pm.headers.findIndex((_, i) => i !== xVal && pm.colTypes[i] === 'numeric');
  const defaultY = defY >= 0 ? defY : (xVal === 0 ? Math.min(1, pm.headers.length - 1) : 0);

  const div = document.createElement('div');
  div.id = `pmYS_${id}`;
  div.style.cssText = 'padding:12px;margin-bottom:8px;border:1px solid var(--md-default-fg-color--lightest);border-radius:6px;background:var(--md-default-bg-color);';
  div.innerHTML = `
    <div style="display:grid;grid-template-columns:2fr 2fr 1fr 1fr auto;gap:10px;align-items:end;flex-wrap:wrap;">
      <div>
        <label style="display:block;margin-bottom:4px;font-size:0.85em;font-weight:500;">Column</label>
        <select id="pmYCol_${id}" style="${iStyle()}">${makeColOptions(defaultY)}</select>
      </div>
      <div>
        <label style="display:block;margin-bottom:4px;font-size:0.85em;font-weight:500;">Label Override</label>
        <input type="text" id="pmYLabel_${id}" placeholder="(column name)" style="${iStyle()}">
      </div>
      <div>
        <label style="display:block;margin-bottom:4px;font-size:0.85em;font-weight:500;">Axis</label>
        <select id="pmYAxis_${id}" style="${iStyle()}">
          <option value="y">Left Y1</option>
          <option value="y2">Right Y2</option>
        </select>
      </div>
      <div>
        <label style="display:block;margin-bottom:4px;font-size:0.85em;font-weight:500;">Color</label>
        <input type="color" id="pmYColor_${id}" value="${color}" style="width:100%;height:36px;padding:2px 3px;border:1px solid var(--md-default-fg-color--lightest);border-radius:4px;cursor:pointer;box-sizing:border-box;">
      </div>
      <div style="align-self:end;">
        <button onclick="document.getElementById('pmYS_${id}').remove()" style="padding:8px 10px;background:#d32f2f;color:white;border:none;border-radius:4px;cursor:pointer;">✕</button>
      </div>
    </div>
    ${transformRow('pmScale_' + id, 'pmOffset_' + id)}`;
  document.getElementById('pmYSeriesContainer').appendChild(div);
};

function renderHistConfig(inner) {
  inner.innerHTML = `
    <p style="margin:0 0 14px;font-size:0.9em;color:var(--md-default-fg-color--light);">
      Add one or more columns to plot as histograms. They will be overlaid on the same axes.
    </p>
    <div id="pmHistContainer" style="margin-top:8px;"></div>
    <button onclick="pmAddHistSeries()" style="margin-top:8px;padding:8px 16px;background:#4caf50;color:white;border:none;border-radius:4px;cursor:pointer;">+ Add Column</button>`;
  pmAddHistSeries();
}

window.pmAddHistSeries = function () {
  const id      = histSeriesIdCounter++;
  const color   = PM_COLORS[id % PM_COLORS.length];
  const defNum  = pm.colTypes.findIndex(t => t === 'numeric');
  const defaultCol = defNum >= 0 ? defNum : 0;

  const div = document.createElement('div');
  div.id = `pmHS_${id}`;
  div.style.cssText = 'padding:12px;margin-bottom:8px;border:1px solid var(--md-default-fg-color--lightest);border-radius:6px;background:var(--md-default-bg-color);';
  div.innerHTML = `
    <div style="display:grid;grid-template-columns:2fr 2fr 1fr 1fr auto;gap:10px;align-items:end;">
      <div>
        <label style="display:block;margin-bottom:4px;font-size:0.85em;font-weight:500;">Column</label>
        <select id="pmHCol_${id}" style="${iStyle()}">${makeColOptions(defaultCol)}</select>
      </div>
      <div>
        <label style="display:block;margin-bottom:4px;font-size:0.85em;font-weight:500;">Label Override</label>
        <input type="text" id="pmHLabel_${id}" placeholder="(column name)" style="${iStyle()}">
      </div>
      <div>
        <label style="display:block;margin-bottom:4px;font-size:0.85em;font-weight:500;">Bins</label>
        <input type="number" id="pmHBins_${id}" value="30" min="1" max="500" style="${iStyle()}">
      </div>
      <div>
        <label style="display:block;margin-bottom:4px;font-size:0.85em;font-weight:500;">Color</label>
        <input type="color" id="pmHColor_${id}" value="${color}" style="width:100%;height:36px;padding:2px 3px;border:1px solid var(--md-default-fg-color--lightest);border-radius:4px;cursor:pointer;box-sizing:border-box;">
      </div>
      <div style="align-self:end;">
        <button onclick="document.getElementById('pmHS_${id}').remove()" style="padding:8px 10px;background:#d32f2f;color:white;border:none;border-radius:4px;cursor:pointer;">✕</button>
      </div>
    </div>
    ${transformRow('pmHScale_' + id, 'pmHOffset_' + id)}`;
  document.getElementById('pmHistContainer').appendChild(div);
};

// ─── STEP 4: PLOT ────────────────────────────────────────────────────────────
window.pmPlot = function () {
  const c = getPlotColors();

  const axisBase = {
    gridcolor: c.grid,
    color:     c.fg,
    zeroline:  false,
    linecolor: c.grid,
  };

  const baseLayout = {
    paper_bgcolor: c.bg,
    plot_bgcolor:  c.bg,
    font:    { color: c.fg, family: 'inherit', size: 13 },
    margin:  { t: 60, b: 60, l: 70, r: 50 },
    hovermode: 'closest',
    title:   { text: pm.title, font: { size: 16 } },
    legend:  { bgcolor: 'rgba(0,0,0,0)', bordercolor: c.grid, borderwidth: 1, font: { color: c.fg } },
  };

  let traces = [], layout = { ...baseLayout };

  if (pm.chartType === 'histogram') {
    const serEls = [...document.querySelectorAll('[id^="pmHS_"]')];
    if (!serEls.length) { alert('Add at least one column.'); return; }

    serEls.forEach(el => {
      const id     = el.id.replace('pmHS_', '');
      const ci     = parseInt(document.getElementById(`pmHCol_${id}`).value);
      const lbl    = document.getElementById(`pmHLabel_${id}`).value.trim();
      const nbins  = parseInt(document.getElementById(`pmHBins_${id}`).value) || 30;
      const color  = document.getElementById(`pmHColor_${id}`).value;
      const scale  = parseFloat(document.getElementById(`pmHScale_${id}`)?.value) || 1;
      const offset = parseFloat(document.getElementById(`pmHOffset_${id}`)?.value) || 0;
      let vals = getColValues(ci, true).filter(v => !isNaN(v));
      vals = applyTransform(vals, scale, offset);
      traces.push({
        x: vals, type: 'histogram', nbinsx: nbins,
        name: lbl || pm.headers[ci],
        histnorm: pm.histnorm, opacity: 0.75,
        marker: { color, line: { color: 'white', width: 0.5 } },
      });
    });

    layout = {
      ...layout,
      barmode: pm.histBarmode,
      xaxis: { ...axisBase, title: pm.xLabel || '', type: pm.xScale === 'log' ? 'log' : '-' },
      yaxis: { ...axisBase, title: pm.yLabel || (pm.histnorm === 'probability density' ? 'Probability Density' : 'Count'), type: pm.yScale === 'log' ? 'log' : '-' },
    };

  } else {
    const serEls = [...document.querySelectorAll('[id^="pmYS_"]')];
    if (!serEls.length) { alert('Add at least one Y series.'); return; }

    const xCi   = parseInt(document.getElementById('pmXCol').value);
    // For datetime X: pass ISO strings (not forceNumeric); for numeric X: parse as float
    const xVals = getColValues(xCi, pm.colTypes[xCi] === 'numeric');
    let hasY2   = false;

    serEls.forEach(el => {
      const id     = el.id.replace('pmYS_', '');
      const yCi    = parseInt(document.getElementById(`pmYCol_${id}`).value);
      const lbl    = document.getElementById(`pmYLabel_${id}`).value.trim();
      const axis   = document.getElementById(`pmYAxis_${id}`).value;
      const color  = document.getElementById(`pmYColor_${id}`).value;
      const scale  = parseFloat(document.getElementById(`pmScale_${id}`)?.value);
      const offset = parseFloat(document.getElementById(`pmOffset_${id}`)?.value);
      const name   = lbl || pm.headers[yCi];
      let yVals    = getColValues(yCi, true);
      yVals = applyTransform(yVals, scale, offset);
      const mode = pm.chartType === 'line' ? 'lines' : 'markers';
      if (axis === 'y2') hasY2 = true;

      traces.push({
        x: xVals, y: yVals, type: 'scatter', mode,
        name, yaxis: axis,
        line:   { color, width: 2 },
        marker: { color, size: 5 },
      });

      // Moving average (values read from customize panel if it exists)
      const maWin = parseInt(document.getElementById(`pmMA_${id}`)?.value) || 0;
      if (maWin > 1) {
        traces.push({
          x: xVals, y: movingAverage(yVals, maWin), type: 'scatter', mode: 'lines',
          name: `${name} (MA-${maWin})`, yaxis: axis,
          line: { color, width: 2, dash: 'dash' },
        });
      }

      // Trend line (numeric X only)
      if (document.getElementById(`pmTrend_${id}`)?.checked && pm.colTypes[xCi] === 'numeric') {
        const xNum = xVals.map(Number);
        const reg  = linearRegression(xNum, yVals);
        if (reg) {
          const { m, b } = reg;
          const fin = xNum.filter(v => isFinite(v));
          const x0 = Math.min(...fin), x1 = Math.max(...fin);
          traces.push({
            x: [x0, x1], y: [m * x0 + b, m * x1 + b], type: 'scatter', mode: 'lines',
            name: `${name} trend (m=${m.toPrecision(3)})`, yaxis: axis,
            line: { color, width: 1.5, dash: 'dot' },
          });
        }
      }
    });

    const xTitle = pm.xLabel || pm.headers[xCi] || '';
    const xType  = pm.colTypes[xCi] === 'datetime' ? 'date'
                 : pm.xScale === 'log' ? 'log' : '-';

    layout = {
      ...layout,
      hovermode: 'x unified',
      xaxis: { ...axisBase, title: xTitle, type: xType },
      yaxis: { ...axisBase, title: pm.yLabel || '', type: pm.yScale === 'log' ? 'log' : '-' },
    };

    if (hasY2) {
      layout.margin.r = 80;
      layout.yaxis2   = { ...axisBase, title: pm.y2Label || '', type: pm.y2Scale === 'log' ? 'log' : '-', overlaying: 'y', side: 'right' };
    }
  }

  // Custom download button: relayout to explicit light colors, capture, then restore theme
  const downloadBtn = {
    name:  'Download PNG',
    title: 'Download as PNG (light mode)',
    icon:  Plotly.Icons.camera,
    click: async function (gd) {
      await Plotly.relayout(gd, {
        paper_bgcolor: LIGHT.bg, plot_bgcolor: LIGHT.bg,
        'font.color':         LIGHT.fg,
        'xaxis.color':        LIGHT.fg,  'xaxis.gridcolor':  LIGHT.grid,
        'yaxis.color':        LIGHT.fg,  'yaxis.gridcolor':  LIGHT.grid,
        'yaxis2.color':       LIGHT.fg,  'yaxis2.gridcolor': LIGHT.grid,
        'legend.bgcolor':     LIGHT.bg,  'legend.bordercolor': LIGHT.grid,
        'legend.font.color':  LIGHT.fg,
      });
      await Plotly.downloadImage(gd, {
        format: 'png', scale: 2,
        filename: (pm.title || 'plotme-chart').replace(/[^a-z0-9_-]/gi, '_'),
      });
      // Restore theme colors
      const rc = getPlotColors();
      await Plotly.relayout(gd, {
        paper_bgcolor: rc.bg, plot_bgcolor: rc.bg,
        'font.color':         rc.fg,
        'xaxis.color':        rc.fg,  'xaxis.gridcolor':  rc.grid,
        'yaxis.color':        rc.fg,  'yaxis.gridcolor':  rc.grid,
        'yaxis2.color':       rc.fg,  'yaxis2.gridcolor': rc.grid,
        'legend.bgcolor':     'rgba(0,0,0,0)', 'legend.bordercolor': rc.grid,
        'legend.font.color':  rc.fg,
      });
    },
  };

  const config = {
    responsive: true, scrollZoom: true, displayModeBar: true,
    modeBarButtonsToRemove: ['toImage'],
    modeBarButtonsToAdd:    [downloadBtn],
  };

  document.getElementById('pmStep4').style.display = 'block';
  Plotly.newPlot('pmPlotDiv', traces, layout, config);

  renderCustomize();
  document.getElementById('pmStep5').style.display = 'block';
  document.getElementById('pmStep4').scrollIntoView({ behavior: 'smooth', block: 'start' });
};

// ─── STEP 5: CUSTOMIZE ───────────────────────────────────────────────────────
function renderCustomize() {
  const cont   = document.getElementById('pmCustomize');
  const isHist = pm.chartType === 'histogram';
  const isXY   = !isHist;

  const inp = (id, val, ph, oninput) =>
    `<input type="text" id="${id}" value="${val || ''}" placeholder="${ph}" style="${iStyle()}" oninput="${oninput}">`;

  const sel = (id, val, opts, onchange) =>
    `<select id="${id}" style="${iStyle()}" onchange="${onchange}">${opts.map(([v, l]) =>
      `<option value="${v}" ${v === val ? 'selected' : ''}>${l}</option>`).join('')}</select>`;

  const scaleOpts = [['linear','Linear'],['log','Log']];

  // Per-series MA + trend controls — read current values before overwriting DOM
  let seriesHTML = '';
  if (isXY) {
    const serEls = [...document.querySelectorAll('[id^="pmYS_"]')];
    seriesHTML = serEls.map(el => {
      const id   = el.id.replace('pmYS_', '');
      const ci   = parseInt(document.getElementById(`pmYCol_${id}`).value);
      const name = document.getElementById(`pmYLabel_${id}`).value.trim() || pm.headers[ci];
      const maV  = document.getElementById(`pmMA_${id}`)?.value ?? '0';
      const trV  = document.getElementById(`pmTrend_${id}`)?.checked ?? false;
      return `
        <div style="padding:10px 0;border-bottom:1px solid var(--md-default-fg-color--lightest);">
          <strong style="font-size:0.88em;">${name}</strong>
          <div style="display:flex;gap:24px;flex-wrap:wrap;margin-top:8px;align-items:center;">
            <label style="font-size:0.85em;display:flex;align-items:center;gap:6px;">
              Moving avg window
              <input type="number" id="pmMA_${id}" value="${maV}" min="0" max="999"
                style="width:64px;padding:5px;border:1px solid var(--md-default-fg-color--lightest);border-radius:4px;background:var(--md-default-bg-color);color:var(--md-default-fg-color);">
              <span style="color:var(--md-default-fg-color--light);">(0 = off)</span>
            </label>
            <label style="font-size:0.85em;display:flex;align-items:center;gap:6px;cursor:pointer;">
              <input type="checkbox" id="pmTrend_${id}" ${trV ? 'checked' : ''}>
              Show trend line
            </label>
          </div>
        </div>`;
    }).join('');
    if (seriesHTML) seriesHTML = `
      <div style="margin-bottom:16px;">
        <strong style="font-size:0.9em;">Per-Series Options</strong>
        ${seriesHTML}
      </div>`;
  }

  const histExtra = isHist ? `
    <div style="display:flex;gap:16px;flex-wrap:wrap;margin-bottom:16px;align-items:center;">
      <label style="font-size:0.9em;font-weight:500;display:flex;align-items:center;gap:8px;">
        Normalization:
        ${sel('pmOptHistnorm', pm.histnorm, [['','Count'],['probability density','Probability Density']], 'pm.histnorm=this.value')}
      </label>
      <label style="font-size:0.9em;font-weight:500;display:flex;align-items:center;gap:8px;">
        Bar mode:
        ${sel('pmOptHistBarmode', pm.histBarmode, [['overlay','Overlay'],['stack','Stacked'],['group','Grouped']], 'pm.histBarmode=this.value')}
      </label>
    </div>` : '';

  cont.innerHTML = `
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-bottom:16px;">
      <div>
        <label style="display:block;margin-bottom:4px;font-weight:500;font-size:0.9em;">Chart Title</label>
        ${inp('pmOptTitle', pm.title, '(optional)', 'pm.title=this.value')}
      </div>
      <div>
        <label style="display:block;margin-bottom:4px;font-weight:500;font-size:0.9em;">X Axis Label</label>
        ${inp('pmOptXLabel', pm.xLabel, '(auto from column)', 'pm.xLabel=this.value')}
      </div>
      <div>
        <label style="display:block;margin-bottom:4px;font-weight:500;font-size:0.9em;">${isHist ? 'Y Axis Label' : 'Y1 (Left) Axis Label'}</label>
        ${inp('pmOptYLabel', pm.yLabel, '(auto)', 'pm.yLabel=this.value')}
      </div>
      ${isXY ? `<div>
        <label style="display:block;margin-bottom:4px;font-weight:500;font-size:0.9em;">Y2 (Right) Axis Label</label>
        ${inp('pmOptY2Label', pm.y2Label, '(if Y2 used)', 'pm.y2Label=this.value')}
      </div>` : '<div></div>'}
    </div>
    <div style="display:flex;gap:20px;flex-wrap:wrap;margin-bottom:16px;align-items:center;">
      <label style="font-size:0.9em;font-weight:500;display:flex;align-items:center;gap:8px;">X Scale: ${sel('pmOptXScale', pm.xScale, scaleOpts, 'pm.xScale=this.value')}</label>
      <label style="font-size:0.9em;font-weight:500;display:flex;align-items:center;gap:8px;">Y1 Scale: ${sel('pmOptY1Scale', pm.yScale, scaleOpts, 'pm.yScale=this.value')}</label>
      ${isXY ? `<label style="font-size:0.9em;font-weight:500;display:flex;align-items:center;gap:8px;">Y2 Scale: ${sel('pmOptY2Scale', pm.y2Scale, scaleOpts, 'pm.y2Scale=this.value')}</label>` : ''}
    </div>
    ${histExtra}
    ${seriesHTML}`;
}

})();
</script>
