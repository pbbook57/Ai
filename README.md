# Ai
Trang web khoa học
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Một ngày bình thường của em</title>
<style>
  body {
    margin: 0;
    font-family: "Segoe UI", sans-serif;
    background: url('https://images.unsplash.com/photo-1527774269336-6b94b8f299d2?auto=format&fit=crop&w=1920&q=80') no-repeat center center fixed;
    background-size: cover;
    color: #fff;
    text-align: center;
    overflow-x: hidden;
  }

  .overlay {
    background: rgba(0,0,0,0.6);
    position: fixed;
    inset: 0;
    z-index: 0;
  }

  h1 {
    font-size: 1.8em;
    color: #00ffff;
    margin-top: 10px;
    text-shadow: 0 0 10px #00ffff;
  }

  .game-container {
    position: relative;
    z-index: 1;
    padding: 10px;
  }

  .character {
    width: 80px;
    margin: 10px auto;
    animation: float 2s infinite alternate;
  }

  @keyframes float {
    from { transform: translateY(0); }
    to { transform: translateY(-10px); }
  }

  .activity-box {
    background: rgba(20,20,20,0.85);
    border: 2px solid #0ff;
    border-radius: 15px;
    padding: 15px;
    margin: 15px auto;
    width: 90%;
    box-shadow: 0 0 20px #0ff;
  }

  .buttons button {
    margin: 10px;
    padding: 10px 20px;
    border: none;
    border-radius: 10px;
    font-size: 1em;
    color: #fff;
    cursor: pointer;
    box-shadow: 0 4px 0 #333;
    transition: all 0.2s;
  }

  .buttons button:hover {
    transform: scale(1.1);
  }

  .yes { background: linear-gradient(145deg,#00ffaa,#0077ff); }
  .no { background: linear-gradient(145deg,#ff0077,#ff7700); }

  .result-box {
    background: rgba(30,30,30,0.85);
    border-radius: 15px;
    padding: 15px;
    width: 90%;
    margin: 20px auto;
    box-shadow: 0 0 15px #ff00ff;
  }

  .robot {
    position: fixed;
    bottom: 20px;
    right: 10px;
    width: 100px;
  }

  .speech {
    position: fixed;
    bottom: 130px;
    right: 20px;
    background: rgba(255,255,255,0.9);
    color: #000;
    border-radius: 15px;
    padding: 10px;
    max-width: 60%;
    box-shadow: 0 0 10px #fff;
  }

  .flower {
    font-size: 3em;
    margin: 10px;
  }

  .start-btn, .restart-btn {
    background: linear-gradient(145deg,#00ffff,#ff00ff);
    padding: 12px 25px;
    font-size: 1.2em;
    border: none;
    border-radius: 12px;
    color: #fff;
    box-shadow: 0 4px 0 #333;
    cursor: pointer;
  }

</style>
</head>
<body>
<div class="overlay"></div>
<div class="game-container">
  <h1>🌙 Một ngày bình thường của em 🌞</h1>
  <div id="game"></div>
  <div id="result"></div>
</div>

<img src="https://cdn-icons-png.flaticon.com/512/4712/4712100.png" class="robot" id="robot" style="display:none;">
<div class="speech" id="speech" style="display:none;"></div>

<script>
const data = [
  {time:"6h00", activity:"Thức dậy, kiểm tra điện thoại ngay khi vừa mở mắt", eval:"Chưa tốt", comment:"Dễ gây mỏi mắt và phụ thuộc thói quen.", type:"Tiêu cực", score:4},
  {time:"6h30", activity:"Ăn sáng, vừa ăn vừa xem YouTube/TikTok", eval:"Chưa tốt", comment:"Giảm tập trung khi ăn uống.", type:"Tiêu cực", score:3},
  {time:"7h00", activity:"Đi học, trên xe buýt/xem điện thoại", eval:"Chưa tốt", comment:"Nguy hiểm khi tham gia giao thông.", type:"Tiêu cực", score:4},
  {time:"7h30-11h30", activity:"Học trên lớp, thỉnh thoảng dùng điện thoại để nhắn tin", eval:"Chưa tốt", comment:"Giảm hiệu quả học tập.", type:"Tiêu cực", score:4},
  {time:"11h30", activity:"Về nhà, ăn trưa, vừa ăn vừa chơi game", eval:"Chưa tốt", comment:"Tạo thói quen xấu dùng điện thoại mọi lúc.", type:"Tiêu cực", score:3},
  {time:"12h00-13h30", activity:"Ngủ trưa, nhưng dùng điện thoại đến khi ngủ gật", eval:"Chưa tốt", comment:"Giảm chất lượng giấc ngủ.", type:"Tiêu cực", score:4},
  {time:"13h30-17h00", activity:"Học thêm trực tuyến, nhưng vừa học vừa lướt mạng xã hội", eval:"Chưa tốt", comment:"Mất tập trung, hiệu quả học thấp.", type:"Tiêu cực", score:4},
  {time:"17h00-18h00", activity:"Chơi thể thao cùng bạn bè", eval:"Tốt", comment:"Giúp rèn luyện sức khỏe.", type:"Tích cực", score:1},
  {time:"18h00-19h00", activity:"Ăn tối cùng gia đình, trò chuyện trực tiếp", eval:"Tốt", comment:"Gắn kết gia đình.", type:"Tích cực", score:1},
  {time:"19h00-21h30", activity:"Làm bài tập, tra cứu tài liệu online", eval:"Tốt (nếu hợp lý)", comment:"Internet hỗ trợ học tập nếu dùng đúng.", type:"Tích cực/Tiêu cực", score:2},
  {time:"21h30", activity:"Xem phim/YouTube trước khi ngủ", eval:"Chưa tốt", comment:"Ảnh sáng xanh ảnh hưởng giấc ngủ.", type:"Tiêu cực", score:4},
  {time:"7h10", activity:"Trò chuyện trực tiếp với bạn cùng bàn trước giờ vào lớp", eval:"Tốt", comment:"Tăng kỹ năng giao tiếp.", type:"Tích cực", score:1},
  {time:"10h00", activity:"Tra cứu thông tin học tập trên điện thoại khi được giáo viên cho phép", eval:"Tốt", comment:"Sử dụng đúng mục đích học tập.", type:"Tích cực", score:1},
  {time:"15h00", activity:"Tham gia CLB sở thích tại trường", eval:"Tốt", comment:"Phát triển năng khiếu.", type:"Tích cực", score:1},
  {time:"16h30", activity:"Ngồi quán trà sữa, dùng điện thoại suốt buổi", eval:"Chưa tốt", comment:"Giảm tương tác trực tiếp với bạn bè.", type:"Tiêu cực", score:3},
  {time:"17h30", activity:"Chơi game online hơn 1 tiếng", eval:"Chưa tốt", comment:"Dễ nghiện, giảm vận động.", type:"Tiêu cực", score:4},
  {time:"18h30", activity:"Phụ giúp bố mẹ việc nhà", eval:"Tốt", comment:"Tăng kỹ năng sống.", type:"Tích cực", score:1},
  {time:"20h00", activity:"Học nhóm trực tuyến qua Zoom/Google Meet", eval:"Tốt", comment:"Tận dụng công nghệ đúng cách.", type:"Tích cực/Tiêu cực", score:2},
  {time:"20h45", activity:"Chat với bạn bè về chủ đề ngoài học tập", eval:"Chưa tốt", comment:"Dễ kéo dài thời gian online.", type:"Tiêu cực", score:3},
  {time:"22h00", activity:"Lướt mạng xã hội để 'cập nhật tin tức'", eval:"Chưa tốt", comment:"Dễ bị cuốn vào thông tin không cần thiết.", type:"Tiêu cực", score:4}
];

let current = 0;
let totalScore = 0;

const gameDiv = document.getElementById('game');
const resultDiv = document.getElementById('result');
const speech = document.getElementById('speech');
const robot = document.getElementById('robot');

function startGame() {
  current = 0;
  totalScore = 0;
  resultDiv.innerHTML = "";
  robot.style.display = 'none';
  speech.style.display = 'none';
  showActivity();
}

function showActivity() {
  if (current >= data.length) { endGame(); return; }

  const act = data[current];
  gameDiv.innerHTML = `
    <img class="character" src="https://cdn-icons-png.flaticon.com/512/8212/8212731.png">
    <div class="activity-box">
      <h2>${act.time}</h2>
      <p>${act.activity}</p>
      <div class="buttons">
        <button class="yes" onclick="choose(true)">Có</button>
        <button class="no" onclick="choose(false)">Không</button>
      </div>
    </div>
  `;
}

function choose(answer) {
  const act = data[current];
  let score = 0;
  if (act.eval.startsWith("Chưa tốt")) {
    score = answer ? act.score : 1;
  } else if (act.eval.startsWith("Tốt")) {
    if (act.eval.includes("nếu")) score = answer ? 2 : 1;
    else score = answer ? 1 : 3;
  } else if (act.type.includes("Tích cực/Tiêu cực")) {
    score = answer ? 2 : 1;
  }

  totalScore += score;

  const flower = (act.eval.startsWith("Tốt")) ? "🌸" : "🥀";
  const msg = `${act.eval}: ${act.comment}`;
  gameDiv.innerHTML = `
    <div class="activity-box">
      <h2>${act.time}</h2>
      <p>${act.activity}</p>
      <div class="flower">${flower}</div>
      <p><b>Đánh giá:</b> ${act.eval}</p>
      <p><b>Nhận xét:</b> ${act.comment}</p>
    </div>
    <button class="start-btn" onclick="next()">Tiếp tục</button>
  `;

  robot.style.display = 'block';
  speech.style.display = 'block';
  speech.textContent = msg;
}

function next() {
  current++;
  showActivity();
}

function endGame() {
  const avg = (totalScore / data.length).toFixed(1);
  let level = "", color = "";
  if (avg < 2) { level="Nguy cơ thấp"; color="#00ff99"; }
  else if (avg < 3) { level="Nguy cơ trung bình"; color="#ffff00"; }
  else if (avg < 4) { level="Nguy cơ cao"; color="#ff8800"; }
  else { level="Nguy cơ rất cao"; color="#ff0044"; }

  resultDiv.innerHTML = `
    <div class="result-box" style="border:3px solid ${color}; box-shadow:0 0 15px ${color}">
      <h2>Kết quả cuối ngày</h2>
      <p>Điểm trung bình: <b>${avg}</b></p>
      <p>Mức nguy cơ: <b style="color:${color}">${level}</b></p>
      <p>${level==="Nguy cơ thấp"?"Tốt lắm! Em đang dùng điện thoại rất hợp lí."
          :level==="Nguy cơ trung bình"?"Cần điều chỉnh thời gian dùng điện thoại hợp lí hơn."
          :level==="Nguy cơ cao"?"Hãy giảm thời gian dùng điện thoại, chú ý học tập và vận động."
          :"Cảnh báo! Em đang sử dụng điện thoại quá nhiều, cần thay đổi ngay!"}</p>
      <button class="restart-btn" onclick="startGame()">Bắt đầu lại</button>
    </div>
  `;
  gameDiv.innerHTML = "";
  robot.style.display = 'none';
  speech.style.display = 'none';
}

gameDiv.innerHTML = `<button class="start-btn" onclick="startGame()">Bắt đầu trò chơi</button>`;
</script>
</body>
</html>
