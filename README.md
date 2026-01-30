<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>みゃくみゃくじ</title>

<meta name="description" content="12の「脈」から、今日のあなたに流れている運をひとつ授ける、1日1回のwebおみくじ。">

<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-07RSW2R6PW"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-07RSW2R6PW');
</script>

<style>
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Hiragino Sans", sans-serif;
    text-align: center;
    padding: 32px 16px;
    background: linear-gradient(180deg, #fdfefe, #f1f7f6);
    color: #222;
  }

  h1 {
    font-size: 26px;
    margin-bottom: 6px;
  }

  .intro {
    font-size: 15px;
    color: #555;
    margin-bottom: 24px;
  }

  button.main {
    font-size: 18px;
    padding: 14px 28px;
    border-radius: 999px;
    border: none;
    background: #0a5c56;
    color: #fff;
    cursor: pointer;
  }

  button.main:active {
    transform: scale(0.97);
  }

  .result {
    margin-top: 32px;
  }

  .shuffle {
    color: #999;
    font-size: 16px;
  }

  .name {
    font-size: 22px;
    font-weight: bold;
    margin-top: 12px;
  }

  .desc {
    font-size: 16px;
    margin-top: 10px;
    line-height: 1.7;
  }

  .thanks {
    margin-top: 20px;
    font-size: 14px;
    color: #666;
  }

  .share {
    margin-top: 24px;
    display: flex;
    gap: 10px;
    justify-content: center;
    flex-wrap: wrap;
  }

  .share button {
    font-size: 14px;
    padding: 8px 14px;
    border-radius: 6px;
    border: none;
    cursor: pointer;
    color: #fff;
  }

  .x { background: #000; }
  .line { background: #06c755; }
  .fb { background: #1877f2; }

  footer {
    margin-top: 48px;
    font-size: 12px;
    color: #888;
    line-height: 1.7;
  }
</style>
</head>

<body>

<h1>みゃくみゃくじ</h1>
<div class="intro">
  12の「脈」から、今日のあなたに流れている運をひとつ授けます。
</div>

<button class="main" onclick="draw()">くじを引く</button>

<div class="result">
  <div id="status" class="shuffle"></div>
  <div id="name" class="name"></div>
  <div id="desc" class="desc"></div>
  <div id="thanks" class="thanks"></div>

  <div class="share" id="shareArea" style="display:none;">
    <button class="x" onclick="shareX()">X</button>
    <button class="line" onclick="shareLINE()">LINE</button>
    <button class="fb" onclick="shareFB()">Facebook</button>
  </div>
</div>

<footer>
  © 2026 みゃくみゃくじ<br>
  ※ 本コンテンツは個人制作の占いコンテンツです。<br>
  ※ 特定の団体・キャラクターとは関係ありません。
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
    show(JSON.parse(localStorage.getItem("omikuji-result")));
    return;
  }

  document.getElementById("status").innerText = "……シャッフル中……";
  document.getElementById("shareArea").style.display = "none";

  setTimeout(() => {
    const result = omikuji[Math.floor(Math.random() * omikuji.length)];
    localStorage.setItem("omikuji-date", today);
    localStorage.setItem("omikuji-result", JSON.stringify(result));
    show(result);

    gtag('event', 'draw_omikuji');
  }, 1200);
}

function show(r) {
  document.getElementById("status").innerText = "";
  document.getElementById("name").innerText = r.name;
  document.getElementById("desc").innerText = r.desc;
  document.getElementById("thanks").innerText = "ありがとう！また明日も来てね 🌱";
  document.getElementById("shareArea").style.display = "flex";
}

function shareText() {
  return `今日の「みゃくみゃくじ」は【${name.innerText}】\n${desc.innerText}\n\n#みゃくみゃくじ`;
}

function shareX() {
  window.open(
    "https://twitter.com/intent/tweet?text=" +
    encodeURIComponent(shareText()) +
    "&url=" + encodeURIComponent(location.href),
    "_blank"
  );
}

function shareLINE() {
  window.open(
    "https://social-plugins.line.me/lineit/share?text=" +
    encodeURIComponent(shareText() + "\n" + location.href),
    "_blank"
  );
}

function shareFB() {
  window.open(
    "https://www.facebook.com/sharer/sharer.php?u=" +
    encodeURIComponent(location.href),
    "_blank"
  );
}
</script>

</body>
</html>
