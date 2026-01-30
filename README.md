<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>みゃくみゃくじ</title>

<meta name="description" content="12の「脈」から、今日のあなたに流れている運をひとつ授ける、1日1回のwebおみくじ。">

<style>
  body {
    font-family: -apple-system, BlinkMacSystemFont, sans-serif;
    text-align: center;
    padding: 30px 15px;
    background: linear-gradient(180deg, #ffffff, #f2f7f4);
    color: #333;
  }

  h1 {
    font-size: 26px;
    color: #1f6f5c;
    letter-spacing: 0.08em;
    margin-bottom: 10px;
  }

  .intro {
    font-size: 16px;
    color: #555;
    margin-bottom: 25px;
  }

  button {
    font-size: 18px;
    padding: 14px 30px;
    border-radius: 999px;
    border: none;
    background: linear-gradient(135deg, #1f6f5c, #2a9d8f);
    color: #fff;
    box-shadow: 0 6px 14px rgba(0,0,0,0.15);
    cursor: pointer;
  }

  button:active {
    transform: scale(0.96);
  }

  .result {
    margin: 35px auto 0;
    padding: 22px 20px;
    max-width: 420px;
    background: #ffffff;
    border-radius: 18px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.06);
  }

  .shuffle {
    font-size: 16px;
    color: #999;
  }

  .name {
    font-size: 22px;
    font-weight: bold;
    margin-top: 10px;
    color: #1f6f5c;
  }

  .desc {
    margin-top: 12px;
    font-size: 16px;
    line-height: 1.7;
  }

  .thanks {
    margin-top: 20px;
    font-size: 14px;
    color: #777;
  }

  footer {
    margin-top: 50px;
    font-size: 12px;
    color: #999;
    line-height: 1.8;
  }
</style>
</head>

<body>

<h1>みゃくみゃくじ</h1>

<div class="intro">
  12の「脈」から、今日のあなたに流れている運をひとつ授けます。
</div>

<button onclick="draw()">くじを引く</button>

<div class="result">
  <div id="status" class="shuffle"></div>
  <div id="name" class="name"></div>
  <div id="desc" class="desc"></div>
  <div id="thanks" class="thanks"></div>
</div>

<footer>
  © 2026 みゃくみゃくじ<br>
  ※ 本コンテンツは個人制作の占いコンテンツです。<br>
  ※ 本コンテンツは特定の団体・キャラクターとは関係ありません。
</footer>

<script>
const omikuji = [
  { name: "金脈（きんみゃく）", desc: "金運が良い、富の源泉を見つける" },
  { name: "人脈（じんみゃく）", desc: "素敵なご縁に恵まれる、助け合える仲間ができる" },
  { name: "脈々（みゃくみゃく）", desc: "大切な伝統や想いを受け継ぎ、次へ繋げる" },
  { name: "脈拍（みゃくはく）", desc: "心身ともに健康で、リズムが安定している" },
  { name: "脈絡（みゃくらく）", desc: "物事の筋道が見え、賢明な判断ができる" },
  { name: "山脈（さんみゃく）", desc: "大きな志を持ち、さらなる高みへ到達できる" },
  { name: "水脈（すいみゃく）", desc: "知恵やアイデアが枯れることなく湧き出し続ける" },
  { name: "気脈（きみゃく）", desc: "周囲の人と心が通じ合い、最高の連携が取れる" },
  { name: "地脈（ちみゃく）", desc: "場所や環境のエネルギーを味方につけ、安定する" },
  { name: "鉱脈（こうみゃく）", desc: "自分の中に眠っていた新しい才能や宝を発見する" },
  { name: "脈あり（みゃくあり）", desc: "期待していたことに光が差し、願いが叶う兆し" },
  { name: "ミャクミャク", desc: "変化を楽しみながら、生命力あふれる未来を切り拓く" }
];

function draw() {
  const today = new Date().toDateString();
  const savedDate = localStorage.getItem("omikuji-date");

  if (savedDate === today) {
    const savedResult = JSON.parse(localStorage.getItem("omikuji-result"));
    show(savedResult);
    return;
  }

  document.getElementById("status").innerText = "……シャッフル中……";
  document.getElementById("name").innerText = "";
  document.getElementById("desc").innerText = "";
  document.getElementById("thanks").innerText = "";

  setTimeout(() => {
    const result = omikuji[Math.floor(Math.random() * omikuji.length)];
    localStorage.setItem("omikuji-date", today);
    localStorage.setItem("omikuji-result", JSON.stringify(result));
    show(result);
  }, 1200);
}

function show(r) {
  document.getElementById("status").innerText = "";
  document.getElementById("name").innerText = r.name;
  document.getElementById("desc").innerText = r.desc;
  document.getElementById("thanks").innerText = "ありがとう！また明日も来てね 🌱";
}
</script>

</body>
</html>
