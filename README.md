<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="utf-8">
<title>Phiếu bầu (2 thẻ)</title>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<style>
  :root { --brand:#0066cc; --green:#28a745; --green2:#1e7e34; --red:#dc3545; --red2:#a71d2a; --amber:#ff9900; --amber2:#cc7a00; }
  body { font-family:"Segoe UI",system-ui,-apple-system,sans-serif; background:#f7f9fc; margin:32px; }
  h1{ color:var(--brand); text-align:center; margin-bottom:8px }
  .tabs { max-width:1000px; margin:0 auto; background:#fff; border-radius:14px; box-shadow:0 8px 24px rgba(0,0,0,.08); overflow:hidden; }
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
  .reset{ background:var(--amber); margin-top:10px } .reset:hover{ background:var(--amber2); }
  .header { display:flex; align-items:center; justify-content:space-between; gap:12px; margin-bottom:10px; }
  .title { font-size:18px; font-weight:700; color:#223; }
</style>
</head>
<body>
<h1>🗳️ Phiếu bầu (2 thẻ)</h1>

<div class="tabs" id="tabs">
  <div class="tab-bar">
    <div class="tab-btn active" data-tab="bch">Ban chấp hành Công đoàn</div>
    <div class="tab-btn" data-tab="db">Đại biểu</div>
  </div>

  <!-- THẺ 1: Ban chấp hành Công đoàn -->
  <div class="panel active" id="panel-bch">
    <div class="header">
      <div class="title">Phiếu bầu Ban chấp hành Công đoàn</div>
      <button class="reset" onclick="resetVotes('#panel-bch')">🔄 Đặt lại về 0 (thẻ này)</button>
    </div>
    <table>
      <tr><th>Họ và tên</th><th>Số phiếu</th><th class="actions">Thao tác</th></tr>
      <tr><td>Hoàng Thị Lan Anh</td><td id="bch_lananh">0</td><td class="actions"><button class="plus" onclick="vote('bch_lananh',1)">+1</button><button class="minus" onclick="vote('bch_lananh',-1)">-1</button></td></tr>
      <tr><td>Phạm Thị Hà</td><td id="bch_ha">0</td><td class="actions"><button class="plus" onclick="vote('bch_ha',1)">+1</button><button class="minus" onclick="vote('bch_ha',-1)">-1</button></td></tr>
      <tr><td>Trịnh Trung Hiếu</td><td id="bch_hieu">0</td><td class="actions"><button class="plus" onclick="vote('bch_hieu',1)">+1</button><button class="minus" onclick="vote('bch_hieu',-1)">-1</button></td></tr>
      <tr><td>Kim Ngọc Huệ</td><td id="bch_hue">0</td><td class="actions"><button class="plus" onclick="vote('bch_hue',1)">+1</button><button class="minus" onclick="vote('bch_hue',-1)">-1</button></td></tr>
      <tr><td>Hà Văn Nam</td><td id="bch_nam">0</td><td class="actions"><button class="plus" onclick="vote('bch_nam',1)">+1</button><button class="minus" onclick="vote('bch_nam',-1)">-1</button></td></tr>
      <tr><td>Lê Xuân Thành</td><td id="bch_thanh">0</td><td class="actions"><button class="plus" onclick="vote('bch_thanh',1)">+1</button><button class="minus" onclick="vote('bch_thanh',-1)">-1</button></td></tr>
    </table>
  </div>

  <!-- THẺ 2: Đại biểu -->
  <div class="panel" id="panel-db">
    <div class="header">
      <div class="title">Phiếu bầu Đại biểu</div>
      <button class="reset" onclick="resetVotes('#panel-db')">🔄 Đặt lại về 0 (thẻ này)</button>
    </div>
    <table>
      <tr><th>Họ và tên</th><th>Số phiếu</th><th class="actions">Thao tác</th></tr>
      <tr><td>Trần Thị Thanh Hà</td><td id="db_ha1">0</td><td class="actions"><button class="plus" onclick="vote('db_ha1',1)">+1</button><button class="minus" onclick="vote('db_ha1',-1)">-1</button></td></tr>
      <tr><td>Hoàng Thị Lan Anh</td><td id="db_lananh">0</td><td class="actions"><button class="plus" onclick="vote('db_lananh',1)">+1</button><button class="minus" onclick="vote('db_lananh',-1)">-1</button></td></tr>
      <tr><td>Nguyễn Thành Đạt</td><td id="db_dat">0</td><td class="actions"><button class="plus" onclick="vote('db_dat',1)">+1</button><button class="minus" onclick="vote('db_dat',-1)">-1</button></td></tr>
      <tr><td>Phạm Thị Hà</td><td id="db_ha2">0</td><td class="actions"><button class="plus" onclick="vote('db_ha2',1)">+1</button><button class="minus" onclick="vote('db_ha2',-1)">-1</button></td></tr>
      <tr><td>Vũ Thị Thanh Hà</td><td id="db_ha3">0</td><td class="actions"><button class="plus" onclick="vote('db_ha3',1)">+1</button><button class="minus" onclick="vote('db_ha3',-1)">-1</button></td></tr>
      <tr><td>Dương Thị Hạnh</td><td id="db_hanh">0</td><td class="actions"><button class="plus" onclick="vote('db_hanh',1)">+1</button><button class="minus" onclick="vote('db_hanh',-1)">-1</button></td></tr>
      <tr><td>Trịnh Trung Hiếu</td><td id="db_hieu">0</td><td class="actions"><button class="plus" onclick="vote('db_hieu',1)">+1</button><button class="minus" onclick="vote('db_hieu',-1)">-1</button></td></tr>
      <tr><td>Kim Ngọc Huệ</td><td id="db_hue">0</td><td class="actions"><button class="plus" onclick="vote('db_hue',1)">+1</button><button class="minus" onclick="vote('db_hue',-1)">-1</button></td></tr>
      <tr><td>Nguyễn Thị Cẩm Hương</td><td id="db_huong">0</td><td class="actions"><button class="plus" onclick="vote('db_huong',1)">+1</button><button class="minus" onclick="vote('db_huong',-1)">-1</button></td></tr>
      <tr><td>Hà Văn Nam</td><td id="db_nam">0</td><td class="actions"><button class="plus" onclick="vote('db_nam',1)">+1</button><button class="minus" onclick="vote('db_nam',-1)">-1</button></td></tr>
      <tr><td>Lê Thị Thúy Nga</td><td id="db_nga">0</td><td class="actions"><button class="plus" onclick="vote('db_nga',1)">+1</button><button class="minus" onclick="vote('db_nga',-1)">-1</button></td></tr>
      <tr><td>Lê Xuân Thành</td><td id="db_thanh">0</td><td class="actions"><button class="plus" onclick="vote('db_thanh',1)">+1</button><button class="minus" onclick="vote('db_thanh',-1)">-1</button></td></tr>
      <tr><td>Nguyễn Thị Thanh Tú</td><td id="db_tu">0</td><td class="actions"><button class="plus" onclick="vote('db_tu',1)">+1</button><button class="minus" onclick="vote('db_tu',-1)">-1</button></td></tr>
    </table>
  </div>
</div>

<script>
  // Chuyển thẻ
  document.querySelectorAll('.tab-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
      document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
      btn.classList.add('active');
      const key = btn.getAttribute('data-tab');
      document.getElementById('panel-'+key).classList.add('active');
    });
  });

  // Cộng/trừ phiếu
  function vote(id, delta){
    const cell = document.getElementById(id);
    let v = parseInt(cell.textContent||'0',10) + delta;
    if (v < 0) v = 0; // không cho âm
    cell.textContent = v;
  }

  // Đặt lại trong từng thẻ (selector là panel)
  function resetVotes(panelSelector){
    document.querySelectorAll(panelSelector+' td[id]').forEach(td=> td.textContent = 0);
  }
</script>
</body>
</html>
