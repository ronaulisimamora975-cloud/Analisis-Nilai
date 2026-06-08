# Analisis-Nilai
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Analisis Pretest Posttest</title>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #f4f6f9; color: #2d3748; min-height: 100vh; padding: 20px; }
  .container { max-width: 960px; margin: 0 auto; }
  .header { background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%); color: white; border-radius: 12px; padding: 24px 28px; margin-bottom: 20px; }
  .header h1 { font-size: 22px; font-weight: 600; margin-bottom: 4px; }
  .header p { font-size: 13px; opacity: 0.85; }
  .card { background: #fff; border-radius: 12px; border: 1px solid #e2e8f0; padding: 20px 24px; margin-bottom: 16px; }
  .card-title { font-size: 13px; font-weight: 600; color: #64748b; text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 14px; }
  .row2 { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  .row4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; }
  label { font-size: 12px; color: #64748b; display: block; margin-bottom: 4px; font-weight: 500; }
  input[type=text], input[type=number] { width: 100%; padding: 8px 10px; border: 1px solid #e2e8f0; border-radius: 8px; font-size: 13px; color: #2d3748; background: #f8fafc; transition: border-color 0.2s; outline: none; }
  input:focus { border-color: #4f46e5; background: #fff; }
  .metric { background: #f8fafc; border-radius: 8px; padding: 14px 16px; border: 1px solid #e2e8f0; }
  .metric-label { font-size: 11px; color: #94a3b8; margin-bottom: 4px; font-weight: 500; text-transform: uppercase; letter-spacing: 0.04em; }
  .metric-value { font-size: 24px; font-weight: 700; color: #1e293b; }
  .metric-sub { font-size: 11px; color: #94a3b8; margin-top: 2px; }
  table { width: 100%; border-collapse: collapse; font-size: 13px; }
  th { font-weight: 600; color: #64748b; padding: 10px 12px; border-bottom: 2px solid #e2e8f0; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.04em; background: #f8fafc; }
  td { padding: 8px 12px; border-bottom: 1px solid #f1f5f9; color: #374151; vertical-align: middle; }
  tr:last-child td { border-bottom: none; }
  tr:hover td { background: #fafafa; }
  .btn { padding: 9px 18px; border-radius: 8px; font-size: 13px; font-weight: 500; cursor: pointer; border: none; transition: all 0.15s; }
  .btn-primary { background: #4f46e5; color: white; }
  .btn-primary:hover { background: #4338ca; }
  .btn-secondary { background: #f1f5f9; color: #374151; border: 1px solid #e2e8f0; }
  .btn-secondary:hover { background: #e2e8f0; }
  .btn-danger { background: transparent; border: none; color: #cbd5e1; cursor: pointer; font-size: 16px; padding: 2px 6px; border-radius: 4px; }
  .btn-danger:hover { color: #ef4444; background: #fef2f2; }
  .btn-analyze { background: linear-gradient(135deg, #4f46e5, #7c3aed); color: white; padding: 11px 28px; font-size: 14px; font-weight: 600; border-radius: 8px; border: none; cursor: pointer; transition: opacity 0.15s; }
  .btn-analyze:hover { opacity: 0.9; }
  .badge { display: inline-block; padding: 3px 10px; border-radius: 20px; font-size: 11px; font-weight: 600; }
  .badge-high { background: #dcfce7; color: #166534; }
  .badge-mid { background: #fef9c3; color: #854d0e; }
  .badge-low { background: #fee2e2; color: #991b1b; }
  .badge-tuntas { background: #dbeafe; color: #1e40af; }
  .badge-belum { background: #fce7f3; color: #9d174d; }
  .tabs { display: flex; gap: 4px; border-bottom: 2px solid #e2e8f0; margin-bottom: 16px; }
  .tab { padding: 8px 16px; font-size: 13px; font-weight: 500; cursor: pointer; border: none; background: transparent; color: #64748b; border-bottom: 2px solid transparent; margin-bottom: -2px; transition: all 0.15s; }
  .tab.active { color: #4f46e5; border-bottom-color: #4f46e5; }
  .tab:hover { color: #4f46e5; }
  .hidden { display: none; }
  .bar-bg { background: #e2e8f0; border-radius: 4px; height: 10px; overflow: hidden; margin: 4px 0; }
  .bar-fill { height: 100%; border-radius: 4px; transition: width 0.5s ease; }
  .note { font-size: 12px; color: #64748b; background: #f0f4ff; border-left: 3px solid #4f46e5; border-radius: 0 6px 6px 0; padding: 10px 14px; margin-top: 14px; }
  .flex-between { display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 8px; }
  .result-hidden { display: none; }
  .ideal-row { display: flex; align-items: center; gap: 8px; font-size: 13px; color: #64748b; }
  .ideal-row input { width: 70px; display: inline-block; }
  @media (max-width: 600px) {
    .row2, .row4 { grid-template-columns: 1fr 1fr; }
    .row4 { grid-template-columns: 1fr 1fr; }
    body { padding: 10px; }
  }
</style>
</head>
<body>
<div class="container">

  <div class="header">
    <h1>📊 Analisis Nilai Pretest &amp; Posttest</h1>
    <p>Hitung N-Gain, efektivitas pembelajaran, dan statistik kelas secara otomatis</p>
  </div>

  <!-- Pengaturan -->
  <div class="card">
    <div class="flex-between">
      <span class="card-title" style="margin-bottom:0">⚙️ Pengaturan</span>
      <div class="ideal-row">Skor Ideal: <input type="number" id="ideal" value="100" min="1" style="width:70px"></div>
    </div>
    <div style="height:12px"></div>
    <div class="row2">
      <div>
        <label>Nama Kelas / Mata Pelajaran</label>
        <input type="text" id="class-name" placeholder="Contoh: Biologi Kelas X-A">
      </div>
      <div>
        <label>KKM / Nilai Minimum Kelulusan</label>
        <input type="number" id="kkm" value="70" min="0" max="100">
      </div>
    </div>
  </div>

  <!-- Input Data -->
  <div class="card">
    <div class="flex-between" style="margin-bottom:14px">
      <span class="card-title" style="margin-bottom:0">📝 Data Nilai Siswa</span>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn btn-secondary" onclick="addRow()">+ Tambah Siswa</button>
        <button class="btn btn-secondary" onclick="importSample()">📋 Contoh Data</button>
        <button class="btn btn-secondary" onclick="clearAll()">🗑 Hapus Semua</button>
      </div>
    </div>
    <div style="overflow-x:auto">
      <table>
        <thead>
          <tr>
            <th style="width:36px">#</th>
            <th>Nama Siswa</th>
            <th style="width:110px">Pretest</th>
            <th style="width:110px">Posttest</th>
            <th style="width:90px">N-Gain</th>
            <th style="width:90px">Kategori</th>
            <th style="width:36px"></th>
          </tr>
        </thead>
        <tbody id="table-body"></tbody>
      </table>
    </div>
    <div style="margin-top:16px;display:flex;align-items:center;gap:12px">
      <button class="btn-analyze" onclick="analyze()">🔍 Analisis Otomatis</button>
      <span style="font-size:12px;color:#94a3b8" id="row-count"></span>
    </div>
  </div>

  <!-- Hasil Analisis -->
  <div id="result-section" class="result-hidden">

    <div style="margin-bottom:16px">
      <div class="card-title" style="padding:0 0 8px">📈 Ringkasan Statistik</div>
      <div class="row4" id="summary-cards"></div>
    </div>

    <div class="card">
      <div class="tabs">
        <button class="tab active" onclick="showTab('ngain')">Distribusi N-Gain</button>
        <button class="tab" onclick="showTab('compare')">Perbandingan Nilai</button>
        <button class="tab" onclick="showTab('ketuntasan')">Ketuntasan Belajar</button>
      </div>
      <div id="tab-ngain"></div>
      <div id="tab-compare" class="hidden"></div>
      <div id="tab-ketuntasan" class="hidden"></div>
    </div>

    <div class="card">
      <div class="flex-between" style="margin-bottom:14px">
        <span class="card-title" style="margin-bottom:0">📋 Tabel Hasil Lengkap</span>
        <button class="btn btn-secondary" onclick="exportCSV()">⬇ Ekspor CSV</button>
      </div>
      <div style="overflow-x:auto">
        <table>
          <thead>
            <tr>
              <th>#</th><th>Nama Siswa</th><th>Pretest</th><th>Posttest</th>
              <th>Selisih</th><th>N-Gain</th><th>Kategori</th><th>Ketuntasan</th>
            </tr>
          </thead>
          <tbody id="result-body"></tbody>
        </table>
      </div>
    </div>

    <div class="card">
      <div class="card-title">📝 Interpretasi Hasil</div>
      <div id="interpretasi" style="font-size:14px;line-height:1.8;color:#374151"></div>
    </div>

  </div>
</div>

<script>
var rows = [], rowId = 0;

function addRow(name, pre, post) {
  rowId++;
  rows.push({ id: rowId, name: name || '', pre: pre !== undefined ? pre : '', post: post !== undefined ? post : '' });
  renderTable();
}

function removeRow(id) {
  rows = rows.filter(function(r){ return r.id !== id; });
  renderTable();
}

function clearAll() {
  if (confirm('Hapus semua data?')) { rows = []; rowId = 0; renderTable(); document.getElementById('result-section').style.display = 'none'; }
}

function calcNGain(pre, post, ideal) {
  if (pre >= ideal) return null;
  return (post - pre) / (ideal - pre);
}

function catLabel(g) {
  if (g === null) return '—';
  if (g >= 0.7) return 'Tinggi';
  if (g >= 0.3) return 'Sedang';
  return 'Rendah';
}

function renderTable() {
  var ideal = parseFloat(document.getElementById('ideal').value) || 100;
  var tbody = document.getElementById('table-body');
  tbody.innerHTML = '';
  rows.forEach(function(r, i) {
    var pre = parseFloat(r.pre), post = parseFloat(r.post);
    var g = (!isNaN(pre) && !isNaN(post)) ? calcNGain(pre, post, ideal) : null;
    var cat = catLabel(g);
    var badge = cat === 'Tinggi' ? 'badge-high' : cat === 'Sedang' ? 'badge-mid' : cat === 'Rendah' ? 'badge-low' : '';
    var gStr = g !== null ? g.toFixed(3) : '—';
    var gColor = cat === 'Tinggi' ? '#166534' : cat === 'Sedang' ? '#854d0e' : cat === 'Rendah' ? '#991b1b' : '#94a3b8';
    tbody.innerHTML += '<tr>' +
      '<td style="color:#94a3b8">' + (i+1) + '</td>' +
      '<td><input type="text" value="' + escHtml(r.name) + '" placeholder="Nama siswa" onchange="upd(' + r.id + ',\'name\',this.value)"></td>' +
      '<td><input type="number" value="' + r.pre + '" placeholder="0-' + ideal + '" min="0" max="' + ideal + '" oninput="upd(' + r.id + ',\'pre\',this.value)"></td>' +
      '<td><input type="number" value="' + r.post + '" placeholder="0-' + ideal + '" min="0" max="' + ideal + '" oninput="upd(' + r.id + ',\'post\',this.value)"></td>' +
      '<td style="font-weight:600;color:' + gColor + '">' + gStr + '</td>' +
      '<td>' + (badge ? '<span class="badge ' + badge + '">' + cat + '</span>' : '—') + '</td>' +
      '<td><button class="btn-danger" onclick="removeRow(' + r.id + ')" title="Hapus">×</button></td>' +
      '</tr>';
  });
  document.getElementById('row-count').textContent = rows.length + ' siswa terdaftar';
}

function escHtml(s) { return String(s).replace(/&/g,'&amp;').replace(/"/g,'&quot;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

function upd(id, field, val) {
  var r = rows.find(function(x){ return x.id === id; });
  if (r) { r[field] = val; renderTable(); }
}

function avg(arr) { return arr.length ? arr.reduce(function(a,b){ return a+b; }, 0) / arr.length : 0; }

function importSample() {
  var samples = [
    ['Andi Pratama',45,78],['Budi Santoso',52,85],['Citra Dewi',38,72],
    ['Dani Kurniawan',60,88],['Eka Rahayu',55,91],['Fajar Nugraha',42,65],
    ['Gina Lestari',48,83],['Hendra Wijaya',35,70],['Indah Permata',65,95],['Joko Susanto',40,75]
  ];
  rows = []; rowId = 0;
  samples.forEach(function(s){ addRow(s[0], s[1], s[2]); });
}

function analyze() {
  var ideal = parseFloat(document.getElementById('ideal').value) || 100;
  var kkm = parseFloat(document.getElementById('kkm').value) || 70;
  var valid = rows.filter(function(r){ return r.name && !isNaN(parseFloat(r.pre)) && !isNaN(parseFloat(r.post)); });
  if (valid.length < 2) { alert('Masukkan minimal 2 data siswa yang lengkap.'); return; }

  var data = valid.map(function(r) {
    var pre = parseFloat(r.pre), post = parseFloat(r.post);
    var g = calcNGain(pre, post, ideal);
    return { name: r.name, pre: pre, post: post, gain: g, cat: catLabel(g) };
  });

  var pres = data.map(function(d){ return d.pre; });
  var posts = data.map(function(d){ return d.post; });
  var gains = data.filter(function(d){ return d.gain !== null; }).map(function(d){ return d.gain; });
  var avgPre = avg(pres), avgPost = avg(posts), avgGain = avg(gains);
  var tinggi = data.filter(function(d){ return d.cat === 'Tinggi'; }).length;
  var sedang = data.filter(function(d){ return d.cat === 'Sedang'; }).length;
  var rendah = data.filter(function(d){ return d.cat === 'Rendah'; }).length;
  var tuntasPre = pres.filter(function(v){ return v >= kkm; }).length;
  var tuntasPost = posts.filter(function(v){ return v >= kkm; }).length;

  var effLabel = avgGain >= 0.7 ? 'Tinggi' : avgGain >= 0.3 ? 'Sedang' : 'Rendah';
  var effColor = avgGain >= 0.7 ? '#166534' : avgGain >= 0.3 ? '#854d0e' : '#991b1b';

  document.getElementById('result-section').style.display = 'block';

  document.getElementById('summary-cards').innerHTML =
    mkMetric('Rata-rata Pretest', avgPre.toFixed(1), pres.length + ' siswa', '') +
    mkMetric('Rata-rata Posttest', avgPost.toFixed(1), '+' + (avgPost-avgPre).toFixed(1) + ' peningkatan', '') +
    mkMetric('N-Gain Rata-rata', avgGain.toFixed(3), 'Kategori: ' + effLabel, effColor) +
    mkMetric('Ketuntasan Posttest', Math.round(tuntasPost/data.length*100) + '%', tuntasPost + ' dari ' + data.length + ' siswa', '');

  renderTabNGain(tinggi, sedang, rendah, data.length);
  renderTabCompare(avgPre, avgPost, pres, posts, ideal);
  renderTabKetuntasan(tuntasPre, tuntasPost, data.length, kkm);
  renderResultTable(data, kkm);
  renderInterpretasi(data, avgPre, avgPost, avgGain, effLabel, tinggi, sedang, rendah, tuntasPre, tuntasPost);

  document.getElementById('result-section').scrollIntoView({ behavior: 'smooth' });
}

function mkMetric(label, val, sub, color) {
  return '<div class="metric"><div class="metric-label">' + label + '</div>' +
    '<div class="metric-value"' + (color ? ' style="color:' + color + '"' : '') + '>' + val + '</div>' +
    '<div class="metric-sub">' + sub + '</div></div>';
}

function bar(pct, color) {
  return '<div class="bar-bg"><div class="bar-fill" style="width:' + pct + '%;background:' + color + '"></div></div>';
}

function renderTabNGain(t, s, r, total) {
  var el = document.getElementById('tab-ngain');
  var items = [
    { label: 'Tinggi (g ≥ 0.7)', count: t, color: '#22c55e' },
    { label: 'Sedang (0.3 ≤ g < 0.7)', count: s, color: '#f59e0b' },
    { label: 'Rendah (g < 0.3)', count: r, color: '#ef4444' }
  ];
  el.innerHTML = items.map(function(b) {
    var pct = total > 0 ? Math.round(b.count/total*100) : 0;
    return '<div style="margin-bottom:16px">' +
      '<div style="display:flex;justify-content:space-between;font-size:13px;margin-bottom:4px">' +
      '<span>' + b.label + '</span>' +
      '<span style="font-weight:600;color:' + b.color + '">' + b.count + ' siswa (' + pct + '%)</span></div>' +
      bar(pct, b.color) + '</div>';
  }).join('') +
  '<div class="note"><strong>Rumus N-Gain (Hake, 1999):</strong> g = (Skor Posttest – Skor Pretest) / (Skor Ideal – Skor Pretest)</div>';
}

function renderTabCompare(avgPre, avgPost, pres, posts, ideal) {
  var el = document.getElementById('tab-compare');
  el.innerHTML = '<div style="margin-bottom:16px">' +
    '<p style="font-size:13px;color:#64748b;margin-bottom:10px">Rata-rata kelas:</p>' +
    '<div style="display:flex;gap:20px">' +
    '<div style="flex:1"><div style="font-size:12px;color:#3b82f6;margin-bottom:3px;font-weight:600">Pretest</div>' + bar(Math.round(avgPre/ideal*100), '#3b82f6') + '<div style="font-size:15px;font-weight:700;margin-top:3px">' + avgPre.toFixed(1) + '</div></div>' +
    '<div style="flex:1"><div style="font-size:12px;color:#22c55e;margin-bottom:3px;font-weight:600">Posttest</div>' + bar(Math.round(avgPost/ideal*100), '#22c55e') + '<div style="font-size:15px;font-weight:700;margin-top:3px">' + avgPost.toFixed(1) + '</div></div>' +
    '</div></div>' +
    '<div class="row4">' +
    mkMetric('Pre Tertinggi', Math.max.apply(null,pres), '','') +
    mkMetric('Pre Terendah', Math.min.apply(null,pres), '','') +
    mkMetric('Post Tertinggi', Math.max.apply(null,posts), '','') +
    mkMetric('Post Terendah', Math.min.apply(null,posts), '','') + '</div>';
}

function renderTabKetuntasan(tpre, tpost, total, kkm) {
  var el = document.getElementById('tab-ketuntasan');
  var pPre = Math.round(tpre/total*100), pPost = Math.round(tpost/total*100);
  el.innerHTML = '<p style="font-size:13px;color:#64748b;margin-bottom:14px">KKM: <strong>' + kkm + '</strong></p>' +
    '<div style="margin-bottom:16px"><div style="display:flex;justify-content:space-between;font-size:13px;margin-bottom:4px"><span>Ketuntasan Pretest</span><span style="font-weight:600">' + tpre + '/' + total + ' (' + pPre + '%)</span></div>' + bar(pPre, '#3b82f6') + '</div>' +
    '<div style="margin-bottom:16px"><div style="display:flex;justify-content:space-between;font-size:13px;margin-bottom:4px"><span>Ketuntasan Posttest</span><span style="font-weight:600;color:#22c55e">' + tpost + '/' + total + ' (' + pPost + '%)</span></div>' + bar(pPost, '#22c55e') + '</div>' +
    '<div class="note">Peningkatan ketuntasan: <strong>+' + (pPost-pPre) + '%</strong> (' + (tpost-tpre) + ' siswa bertambah mencapai KKM)</div>';
}

function renderResultTable(data, kkm) {
  var tbody = document.getElementById('result-body');
  tbody.innerHTML = data.map(function(d, i) {
    var diff = d.post - d.pre;
    var gStr = d.gain !== null ? d.gain.toFixed(3) : '—';
    var catBadge = d.cat === 'Tinggi' ? 'badge-high' : d.cat === 'Sedang' ? 'badge-mid' : 'badge-low';
    var tClass = d.post >= kkm ? 'badge-tuntas' : 'badge-belum';
    var tLabel = d.post >= kkm ? '✓ Tuntas' : '✗ Belum';
    return '<tr><td style="color:#94a3b8">' + (i+1) + '</td><td>' + escHtml(d.name) + '</td><td>' + d.pre + '</td><td>' + d.post + '</td>' +
      '<td style="font-weight:600;color:' + (diff >= 0 ? '#166534' : '#991b1b') + '">' + (diff >= 0 ? '+' : '') + diff + '</td>' +
      '<td style="font-weight:600">' + gStr + '</td>' +
      '<td><span class="badge ' + catBadge + '">' + d.cat + '</span></td>' +
      '<td><span class="badge ' + tClass + '">' + tLabel + '</span></td></tr>';
  }).join('');
}

function renderInterpretasi(data, avgPre, avgPost, avgGain, effLabel, tinggi, sedang, rendah, tpre, tpost) {
  var kls = document.getElementById('class-name').value || 'kelas ini';
  document.getElementById('interpretasi').innerHTML =
    '<p style="margin-bottom:8px">Berdasarkan analisis terhadap <strong>' + data.length + ' siswa</strong> pada ' + escHtml(kls) + ', diperoleh rata-rata pretest <strong>' + avgPre.toFixed(1) + '</strong> dan posttest <strong>' + avgPost.toFixed(1) + '</strong> dengan peningkatan sebesar <strong>' + (avgPost-avgPre).toFixed(1) + ' poin</strong>.</p>' +
    '<p style="margin-bottom:8px">Nilai N-Gain rata-rata sebesar <strong>' + avgGain.toFixed(3) + '</strong> menunjukkan efektivitas pembelajaran tergolong <strong>' + effLabel + '</strong> berdasarkan kriteria Hake (1999).</p>' +
    '<p style="margin-bottom:8px">Distribusi N-Gain: <strong>' + tinggi + ' siswa</strong> kategori Tinggi, <strong>' + sedang + ' siswa</strong> kategori Sedang, dan <strong>' + rendah + ' siswa</strong> kategori Rendah.</p>' +
    '<p>Ketuntasan belajar meningkat dari <strong>' + tpre + ' siswa</strong> pada pretest menjadi <strong>' + tpost + ' siswa</strong> pada posttest. ' +
    (tpost === data.length ? 'Seluruh siswa telah mencapai ketuntasan belajar.' : 'Masih terdapat <strong>' + (data.length-tpost) + ' siswa</strong> yang belum mencapai KKM dan perlu mendapat perhatian khusus.') + '</p>';
}

function exportCSV() {
  var headers = ['No','Nama Siswa','Pretest','Posttest','Selisih','N-Gain','Kategori N-Gain','Ketuntasan'];
  var csvRows = [headers.join(',')];
  document.querySelectorAll('#result-body tr').forEach(function(tr) {
    var cells = Array.from(tr.querySelectorAll('td')).map(function(td){ return '"' + td.textContent.trim().replace(/"/g,'""') + '"'; });
    csvRows.push(cells.join(','));
  });
  var blob = new Blob([csvRows.join('\n')], { type: 'text/csv;charset=utf-8;' });
  var a = document.createElement('a'); a.href = URL.createObjectURL(blob);
  a.download = 'analisis_pretest_posttest.csv'; a.click();
}

function showTab(name) {
  ['ngain','compare','ketuntasan'].forEach(function(t){
    document.getElementById('tab-' + t).classList.toggle('hidden', t !== name);
  });
  document.querySelectorAll('.tab').forEach(function(btn, i){
    btn.classList.toggle('active', ['ngain','compare','ketuntasan'][i] === name);
  });
}

importSample();
</script>
</body>
</html>
