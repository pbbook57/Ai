<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="utf-8">
<title>Phiếu bầu Ban chấp hành công đoàn</title>
<style>
  body {
    font-family: "Segoe UI", sans-serif;
    background: #f7f9fc;
    text-align: center;
    margin: 40px;
  }
  h2 {
    color: #0066cc;
    margin-bottom: 20px;
  }
  table {
    margin: 0 auto;
    border-collapse: collapse;
    width: 70%;
    background: white;
    box-shadow: 0 2px 6px rgba(0,0,0,0.2);
  }
  th, td {
    border: 1px solid #ccc;
    padding: 12px;
    font-size: 18px;
  }
  th {
    background-color: #eaf2ff;
  }
  button {
    padding: 6px 14px;
    margin: 2px;
    border: none;
    border-radius: 6px;
    color: white;
    cursor: pointer;
    font-size: 16px;
  }
  .plus {
    background: #28a745;
  }
  .plus:hover {
    background: #1e7e34;
  }
  .minus {
    background: #dc3545;
  }
  .minus:hover {
    background: #a71d2a;
  }
  #reset {
    background: #ff9900;
    margin-top: 20px;
  }
  #reset:hover {
    background: #cc7a00;
  }
</style>
</head>
<body>
<h2>🗳️ Phiếu bầu Ban chấp hành công đoàn</h2>

<table>
  <tr><th>Họ và tên</th><th>Số phiếu</th><th>Thao tác</th></tr>
  <tr><td>Hoàng Thị Lan Anh</td><td id="lananh">0</td>
      <td>
        <button class="plus" onclick="vote('lananh',1)">+1</button>
        <button class="minus" onclick="vote('lananh',-1)">-1</button>
      </td></tr>
  <tr><td>Phạm Thị Hà</td><td id="ha">0</td>
      <td>
        <button class="plus" onclick="vote('ha',1)">+1</button>
        <button class="minus" onclick="vote('ha',-1)">-1</button>
      </td></tr>
  <tr><td>Trịnh Trung Hiếu</td><td id="hieu">0</td>
      <td>
        <button class="plus" onclick="vote('hieu',1)">+1</button>
        <button class="minus" onclick="vote('hieu',-1)">-1</button>
      </td></tr>
  <tr><td>Kim Ngọc Huệ</td><td id="hue">0</td>
      <td>
        <button class="plus" onclick="vote('hue',1)">+1</button>
        <button class="minus" onclick="vote('hue',-1)">-1</button>
      </td></tr>
  <tr><td>Hà Văn Nam</td><td id="nam">0</td>
      <td>
        <button class="plus" onclick="vote('nam',1)">+1</button>
        <button class="minus" onclick="vote('nam',-1)">-1</button>
      </td></tr>
  <tr><td>Lê Xuân Thành</td><td id="thanh">0</td>
      <td>
        <button class="plus" onclick="vote('thanh',1)">+1</button>
        <button class="minus" onclick="vote('thanh',-1)">-1</button>
      </td></tr>
</table>

<button id="reset" onclick="resetVotes()">🔄 Đặt lại tất cả về 0</button>

<script>
function vote(id, value) {
  let cell = document.getElementById(id);
  let count = parseInt(cell.textContent);
  count += value;
  if (count < 0) count = 0; // không cho âm
  cell.textContent = count;
}

function resetVotes() {
  document.querySelectorAll("td[id]").forEach(cell => cell.textContent = 0);
}
</script>

</body>
</html>
