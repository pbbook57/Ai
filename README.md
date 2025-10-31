<html lang="vi">
<head>
<meta charset="utf-8">
<title>Phiếu bầu (2 thẻ, lưu & tính % theo phiếu hợp lệ)</title>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<style>
  :root { --brand:#0066cc; --green:#28a745; --green2:#1e7e34; --red:#dc3545; --red2:#a71d2a; --amber:#ff9900; --amber2:#cc7a00; }
  body { font-family:"Segoe UI",system-ui,-apple-system,sans-serif; background:#f7f9fc; margin:32px; }
  h1{ color:var(--brand); text-align:center; margin-bottom:8px }
  .tabs { max-width:1100px; margin:0 auto; background:#fff; border-radius:14px; box-shadow:0 8px 24px rgba(0,0,0,.08); overflow:hidden; }
  .tab-bar { display:flex; border-bottom:1px solid #e6eaf0; background:#f2f6ff }
  .tab-btn { flex:1; padding:14px 10px; text-align:center; cursor:pointer; font-weight:600; color:#334; }
  .tab-btn.active { background:#fff; color:var(--brand); border-bottom:3px solid var(--brand); }
  .panel { display:none; padding:18px; }
  .panel.active { display:block; }
  table { width:100%; border-collapse:collapse; background:#fff; }
  th, td { border:1px solid #d9dfe7; padding:10px 12px; font-size:16px; }
  th { background:#eaf2ff; text-align:left; }
  .actions { white-space:nowrap; }
  button { padding:6px 12px; margin:2px; border:none; border-radius:8px; color:#fff; cursor:pointer; font-size:15px; }
  .plus { background:var(--green); } .plus:hover{ background:var(--green2); }
  .minus{ background:var(--red); } .minus:hover{ background:var(--red2); }
  .reset{ background:var(--amber); } .reset:hover{ background:var(--amber2); }
  .btn-ghost { background:#708090; } .btn-ghost:hover{ filter:brightness(.9); }
  .header { display:flex; align-items:center; justify-content:space-between; gap:12px; margin-bottom:12px; flex-wrap:wrap; }
  .title { font-size:18px; font-weight:700; color:#223; }
  .util { display:flex; flex-wrap:wrap; gap:8px; }
  .stats { display:grid; grid-template-columns:repeat(3, minmax(180px,1fr)); gap:10px; margin:10px 0 14px; }
  .stat { background:#f7fbff; border:1px solid #e1e8f0; border-radius:10px; padding:8px 10px; }
  .stat label { display:block; font-size:13px; color:#334; margin-bottom:4px; }
  .stat input { width:100%; padding:8px; font-size:15px; border:1px solid #cfd8e3; border-radius:8px; }
  .summary { font-size:14px; color:#444; margin:6px 0 12px; }
  .right { text-align:right; }
  .muted { color:#667; font-size:14px; }
</style>
</head>
<body>
<h1>🗳️ Phiếu bầu (2 thẻ, lưu & tính %)</h1>

<div class="tabs" id="tabs">
  <div class="tab-bar">
    <div class="tab-btn active" data-tab="bch">Ban chấp hành Công đoàn</div>
    <div class="tab-btn" data-tab="db">Đại biểu</div>
  </div>

  <!-- ===== THẺ 1: BCH CÔNG ĐOÀN ===== -->
  <div class="panel active" id="panel-bch">
    <div class="header">
      <div class="title">Phiếu bầu Ban chấp hành Công đoàn</div>
      <div class="util">
        <button class="reset" onclick="resetVotes('#panel-bch')">🔄 Đặt lại về 0</button>
        <button class="btn-ghost" onclick="saveAll()">💾 Lưu ngay</button>
        <button class="btn-ghost" onclick="exportCSV('#panel-bch','BCH_Cong_doan.csv')">📥 Xuất CSV</button>
        <button class="btn-ghost" onclick="clearSaved()">🧹 Xóa dữ liệu lưu</button>
      </div>
    </div>

    <!-- Nhập thống kê -->
    <div class="stats">
      <div class="stat"><label for="bch_issued">Số phiếu phát ra</label><input id="bch_issued" type="number" min="0" value="0"></div>
      <div class="stat"><label for="bch_collected">Số phiếu thu về</label><input id="bch_collected" type="number" min="0" value="0"></div>
      <div class="stat"><label for="bch_valid">Số phiếu hợp lệ</label><input id="bch_valid" type="number" min="0" value="0"></div>
    </div>
    <div class="summary" id="bch_summary" aria-live="polite"></div>

    <table>
      <tr><th>Họ và tên</th><th class="right">Số phiếu</th><th class="right">% (trên hợp lệ)</th><th class="actions">Thao tác</th></tr>
      <tr><td>Hoàng Thị Lan Anh</td><td id="bch_lananh" class="right">0</td><td id="bch_lananh_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('bch_lananh',1)">+1</button><button class="minus" onclick="vote('bch_lananh',-1)">-1</button></td></tr>
      <tr><td>Phạm Thị Hà</td><td id="bch_ha" class="right">0</td><td id="bch_ha_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('bch_ha',1)">+1</button><button class="minus" onclick="vote('bch_ha',-1)">-1</button></td></tr>
      <tr><td>Trịnh Trung Hiếu</td><td id="bch_hieu" class="right">0</td><td id="bch_hieu_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('bch_hieu',1)">+1</button><button class="minus" onclick="vote('bch_hieu',-1)">-1</button></td></tr>
      <tr><td>Kim Ngọc Huệ</td><td id="bch_hue" class="right">0</td><td id="bch_hue_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('bch_hue',1)">+1</button><button class="minus" onclick="vote('bch_hue',-1)">-1</button></td></tr>
      <tr><td>Hà Văn Nam</td><td id="bch_nam" class="right">0</td><td id="bch_nam_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('bch_nam',1)">+1</button><button class="minus" onclick="vote('bch_nam',-1)">-1</button></td></tr>
      <tr><td>Lê Xuân Thành</td><td id="bch_thanh" class="right">0</td><td id="bch_thanh_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('bch_thanh',1)">+1</button><button class="minus" onclick="vote('bch_thanh',-1)">-1</button></td></tr>
    </table>
    <p class="muted">*Tỷ lệ được tính theo số phiếu hợp lệ của thẻ này.</p>
  </div>

  <!-- ===== THẺ 2: ĐẠI BIỂU ===== -->
  <div class="panel" id="panel-db">
    <div class="header">
      <div class="title">Phiếu bầu Đại biểu</div>
      <div class="util">
        <button class="reset" onclick="resetVotes('#panel-db')">🔄 Đặt lại về 0</button>
        <button class="btn-ghost" onclick="saveAll()">💾 Lưu ngay</button>
        <button class="btn-ghost" onclick="exportCSV('#panel-db','Dai_bieu.csv')">📥 Xuất CSV</button>
        <button class="btn-ghost" onclick="clearSaved()">🧹 Xóa dữ liệu lưu</button>
      </div>
    </div>

    <div class="stats">
      <div class="stat"><label for="db_issued">Số phiếu phát ra</label><input id="db_issued" type="number" min="0" value="0"></div>
      <div class="stat"><label for="db_collected">Số phiếu thu về</label><input id="db_collected" type="number" min="0" value="0"></div>
      <div class="stat"><label for="db_valid">Số phiếu hợp lệ</label><input id="db_valid" type="number" min="0" value="0"></div>
    </div>
    <div class="summary" id="db_summary" aria-live="polite"></div>

    <table>
      <tr><th>Họ và tên</th><th class="right">Số phiếu</th><th class="right">% (trên hợp lệ)</th><th class="actions">Thao tác</th></tr>
      <tr><td>Trần Thị Thanh Hà</td><td id="db_ha1" class="right">0</td><td id="db_ha1_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_ha1',1)">+1</button><button class="minus" onclick="vote('db_ha1',-1)">-1</button></td></tr>
      <tr><td>Hoàng Thị Lan Anh</td><td id="db_lananh" class="right">0</td><td id="db_lananh_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_lananh',1)">+1</button><button class="minus" onclick="vote('db_lananh',-1)">-1</button></td></tr>
      <tr><td>Nguyễn Thành Đạt</td><td id="db_dat" class="right">0</td><td id="db_dat_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_dat',1)">+1</button><button class="minus" onclick="vote('db_dat',-1)">-1</button></td></tr>
      <tr><td>Phạm Thị Hà</td><td id="db_ha2" class="right">0</td><td id="db_ha2_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_ha2',1)">+1</button><button class="minus" onclick="vote('db_ha2',-1)">-1</button></td></tr>
      <tr><td>Vũ Thị Thanh Hà</td><td id="db_ha3" class="right">0</td><td id="db_ha3_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_ha3',1)">+1</button><button class="minus" onclick="vote('db_ha3',-1)">-1</button></td></tr>
      <tr><td>Dương Thị Hạnh</td><td id="db_hanh" class="right">0</td><td id="db_hanh_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_hanh',1)">+1</button><button class="minus" onclick="vote('db_hanh',-1)">-1</button></td></tr>
      <tr><td>Trịnh Trung Hiếu</td><td id="db_hieu" class="right">0</td><td id="db_hieu_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_hieu',1)">+1</button><button class="minus" onclick="vote('db_hieu',-1)">-1</button></td></tr>
      <tr><td>Kim Ngọc Huệ</td><td id="db_hue" class="right">0</td><td id="db_hue_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_hue',1)">+1</button><button class="minus" onclick="vote('db_hue',-1)">-1</button></td></tr>
      <tr><td>Nguyễn Thị Cẩm Hương</td><td id="db_huong" class="right">0</td><td id="db_huong_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_huong',1)">+1</button><button class="minus" onclick="vote('db_huong',-1)">-1</button></td></tr>
      <tr><td>Hà Văn Nam</td><td id="db_nam" class="right">0</td><td id="db_nam_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_nam',1)">+1</button><button class="minus" onclick="vote('db_nam',-1)">-1</button></td></tr>
      <tr><td>Lê Thị Thúy Nga</td><td id="db_nga" class="right">0</td><td id="db_nga_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_nga',1)">+1</button><button class="minus" onclick="vote('db_nga',-1)">-1</button></td></tr>
      <tr><td>Lê Xuân Thành</td><td id="db_thanh" class="right">0</td><td id="db_thanh_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_thanh',1)">+1</button><button class="minus" onclick="vote('db_thanh',-1)">-1</button></td></tr>
      <tr><td>Nguyễn Thị Thanh Tú</td><td id="db_tu" class="right">0</td><td id="db_tu_pct" class="right">0%</td><td class="actions"><button class="plus" onclick="vote('db_tu',1)">+1</button><button class="minus" onclick="vote('db_tu',-1)">-1</button></td></tr>
    </table>
    <p class="muted">*Tỷ lệ được tính theo số phiếu hợp lệ của thẻ này.</p>
  </div>
</div>

<script>
  const STORAGE_KEY = 'phieubau_votes_v2';

  // ==== Tabs ====
  document.querySelectorAll('.tab-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
      document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
      btn.classList.add('active');
      document.getElementById('panel-'+btn.dataset.tab).classList.add('active');
    });
  });

  // ==== Helpers ====
  function fmtPct(x){ return (isFinite(x) ? x.toFixed(2) : '0.00') + '%'; }

  function recalcPanel(panelSelector){
    // đọc số phiếu hợp lệ của panel
    const validInput = document.querySelector(panelSelector+' input[id$="_valid"]');
    const valid = Math.max(0, parseInt(validInput.value||'0',10));
    // cập nhật từng dòng %
    document.querySelectorAll(panelSelector+' td[id$="_pct"]').forEach(pctCell=>{
      const idBase = pctCell.id.replace('_pct','');
      const voteCell = document.getElementById(idBase);
      const votes = parseInt(voteCell.textContent||'0',10);
      const pct = (valid>0) ? (votes/valid*100) : 0;
      pctCell.textContent = fmtPct(pct);
    });
    // tóm tắt: thu về, hợp lệ, không hợp lệ, tỷ lệ tham gia
    const issued = Math.max(0, parseInt(document.querySelector(panelSelector+' input[id$="_issued"]').value||'0',10));
    const collected = Math.max(0, parseInt(document.querySelector(panelSelector+' input[id$="_collected"]').value||'0',10));
    const invalid = Math.max(0, collected - valid);
    const turnout = (issued>0) ? (collected/issued*100) : 0;
    const sumEl = document.querySelector(panelSelector+' .summary');
    sumEl.textContent = `Phát ra: ${issued} • Thu về: ${collected} • Hợp lệ: ${valid} • Không hợp lệ: ${invalid} • Tỷ lệ tham gia: ${fmtPct(turnout).replace('%','%')}`;
  }

  function recalcAll(){
    recalcPanel('#panel-bch');
    recalcPanel('#panel-db');
  }

  // ==== Vote ====
  function vote(id, delta){
    const cell = document.getElementById(id);
    let v = parseInt(cell.textContent||'0',10) + delta;
    if (v < 0) v = 0;
    cell.textContent = v;
    recalcAll();
    saveAll();
  }

  // ==== Reset theo panel ====
  function resetVotes(panelSelector){
    document.querySelectorAll(panelSelector+' td[id]').forEach(td=>{
      // chỉ đặt lại ô Số phiếu, không đụng ô % (sẽ tính lại)
      if(!td.id.endsWith('_pct')) td.textContent = 0;
    });
    // đặt 3 input về 0
    document.querySelectorAll(panelSelector+' input[type="number"]').forEach(inp=> inp.value = 0);
    recalcPanel(panelSelector);
    saveAll();
  }

  // ==== LƯU / TẢI ====
  function saveAll(){
    const data = {};
    // các ô đếm phiếu
    document.querySelectorAll('td[id]').forEach(td=>{
      data[td.id] = td.textContent;
    });
    // các input tổng hợp
    document.querySelectorAll('input[type="number"]').forEach(inp=>{
      data[inp.id] = inp.value;
    });
    localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
  }

  function loadAll(){
    try{
      const data = JSON.parse(localStorage.getItem(STORAGE_KEY) || '{}');
      Object.keys(data).forEach(id=>{
        const el = document.getElementById(id);
        if(el){
          if(el.tagName === 'INPUT') el.value = data[id];
          else el.textContent = data[id];
        }
      });
    }catch(e){}
    recalcAll();
  }

  function clearSaved(){
    localStorage.removeItem(STORAGE_KEY);
    alert('Đã xóa dữ liệu lưu trong trình duyệt.');
  }

  // ==== Xuất CSV ====
  function exportCSV(panelSelector, filename){
    const rows = Array.from(document.querySelectorAll(panelSelector+' table tr')).slice(1);
    // header
    const lines = [['Ho va ten','So phieu','Ty le (%)']];
    rows.forEach(tr=>{
      const tds = tr.querySelectorAll('td');
      if (tds.length >= 3){
        const name = tds[0].textContent.replace(/\s+/g,' ').trim();
        const count = tds[1].textContent.trim();
        const pct = tds[2].textContent.replace('%','').trim();
        lines.push([name, count, pct]);
      }
    });
    // phần tóm tắt
    const issued = document.querySelector(panelSelector+' input[id$="_issued"]').value;
    const collected = document.querySelector(panelSelector+' input[id$="_collected"]').value;
    const valid = document.querySelector(panelSelector+' input[id$="_valid"]').value;
    lines.push([]);
    lines.push(['Tong ket','Phat ra','Thu ve','Hop le']);
    lines.push(['', issued, collected, valid]);

    const csv = lines.map(r=>r.map(x=>`"${String(x).replace(/"/g,'""')}"`).join(',')).join('\r\n');
    const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = filename;
    a.click();
    URL.revokeObjectURL(a.href);
  }

  // ==== Lắng nghe thay đổi input để tính lại & lưu ====
  document.querySelectorAll('input[type="number"]').forEach(inp=>{
    inp.addEventListener('input', ()=>{ recalcAll(); saveAll(); });
  });

  // Khởi động
  loadAll();
</script>
</body>
</html>
