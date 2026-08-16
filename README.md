# QDASH-Chi

<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>上肢功能受損程度問卷（Chinese QuickDASH）</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no, viewport-fit=cover">
  <style>
    :root {
      --primary: #007AFF;
      --primary-active: #0056b3;
      --bg: #F2F2F7;
      --card-bg: #FFFFFF;
      --text-main: #000000;
      --text-muted: #3C3C43;
      --border: #D1D1D6;
      --selected-bg: #E3F0FF;
    }

    * {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
      -webkit-text-size-adjust: 100%;
    }

    html, body {
      width: 100%;
      overflow-x: hidden;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display", "PingFang HK", "PingFang TC", "Noto Sans TC", sans-serif;
      background-color: var(--bg);
      color: var(--text-main);
      margin: 0;
      padding: env(safe-area-inset-top, 10px) 12px calc(36px + env(safe-area-inset-bottom, 20px)) 12px;
      font-size: clamp(17px, 4.8vw, 20px);
      line-height: 1.45;
    }

    .container {
      width: 100%;
      max-width: 600px;
      margin: 0 auto;
    }

    /* Header */
    .header-card {
      background: var(--card-bg);
      border-radius: 16px;
      padding: 16px 14px;
      margin-top: 6px;
      margin-bottom: 14px;
      text-align: center;
      box-shadow: 0 1px 4px rgba(0,0,0,0.06);
      border: 1px solid var(--border);
    }

    .hospital-title {
      font-size: clamp(1rem, 4vw, 1.15rem);
      color: #636366;
      font-weight: 600;
      margin-bottom: 4px;
    }

    .main-title {
      font-size: clamp(1.4rem, 5.5vw, 1.85rem);
      font-weight: 800;
      margin: 0 0 8px 0;
      color: var(--text-main);
      line-height: 1.25;
    }

    .instruction {
      font-size: clamp(1.05rem, 4.2vw, 1.2rem);
      color: var(--text-muted);
      margin: 0;
      line-height: 1.5;
    }

    /* Question Cards */
    .question-card {
      background: var(--card-bg);
      border-radius: 16px;
      padding: 18px 14px;
      margin-bottom: 14px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.05);
      border: 1.5px solid var(--border);
    }

    .question-header {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      margin-bottom: 12px;
    }

    .question-title {
      font-size: clamp(1.2rem, 4.8vw, 1.4rem);
      font-weight: 700;
      color: var(--text-main);
      line-height: 1.35;
    }

    /* Options Stack */
    .options-group {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .option-item {
      display: flex;
      align-items: center;
      padding: 14px 14px;
      border-radius: 14px;
      background: #F8F8FA;
      border: 2px solid transparent;
      cursor: pointer;
      font-size: clamp(1.05rem, 4.2vw, 1.2rem);
      color: #1C1C1E;
      transition: all 0.15s ease-in-out;
    }

    .option-item:active {
      transform: scale(0.99);
      background: #E5E5EA;
    }

    .option-item.selected {
      background: var(--selected-bg);
      border-color: var(--primary);
      color: #004CB8;
      font-weight: 700;
    }

    /* Custom Radio Dot */
    .custom-radio {
      width: 24px;
      height: 24px;
      border-radius: 50%;
      border: 2px solid #8E8E93;
      margin-right: 12px;
      flex-shrink: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #FFF;
    }

    .option-item.selected .custom-radio {
      border-color: var(--primary);
      background: var(--primary);
    }

    .option-item.selected .custom-radio::after {
      content: "";
      width: 10px;
      height: 10px;
      background: #FFF;
      border-radius: 50%;
    }

    .option-text {
      flex-grow: 1;
      line-height: 1.4;
    }

    .hidden-radio {
      position: absolute;
      opacity: 0;
      pointer-events: none;
    }

    /* Submit Button */
    .calc-btn {
      margin-top: 16px;
      padding: 18px;
      width: 100%;
      background: var(--primary);
      color: #FFFFFF;
      font-size: clamp(1.2rem, 5vw, 1.35rem);
      font-weight: 700;
      border: none;
      border-radius: 16px;
      cursor: pointer;
      box-shadow: 0 4px 14px rgba(0, 122, 255, 0.35);
      transition: background 0.15s, transform 0.1s;
    }

    .calc-btn:active {
      background: var(--primary-active);
      transform: scale(0.98);
    }

    .warning {
      color: #FF3B30;
      margin-top: 14px;
      font-size: 1.1rem;
      font-weight: 700;
      text-align: center;
    }

    /* Modal Sheet */
    .modal {
      display: none;
      position: fixed;
      z-index: 999;
      inset: 0;
      background: rgba(0, 0, 0, 0.5);
      backdrop-filter: blur(8px);
      -webkit-backdrop-filter: blur(8px);
      align-items: center;
      justify-content: center;
      padding: 16px;
    }

    .modal-content {
      background: #FFFFFF;
      padding: 24px 18px;
      border-radius: 22px;
      width: 100%;
      max-width: 400px;
      text-align: center;
      box-shadow: 0 12px 36px rgba(0,0,0,0.25);
    }

    .modal-content h2 {
      margin: 0 0 12px 0;
      font-size: 1.6rem;
    }

    .notice-box {
      background: #FFF9E6;
      border: 1.5px solid #FFD666;
      padding: 14px;
      margin: 16px 0;
      font-size: 1.05rem;
      color: #874D00;
      border-radius: 12px;
      line-height: 1.5;
      font-weight: 700;
    }

    .close-btn {
      width: 100%;
      padding: 16px;
      background: #1C1C1E;
      color: #FFF;
      font-size: 1.2rem;
      font-weight: 700;
      border: none;
      border-radius: 14px;
      cursor: pointer;
    }
  </style>
</head>
<body>

<div class="container">
  <div class="header-card">
    <h1 class="main-title">上肢功能受損程度問卷<br>（QuickDASH）</h1>
    <p class="instruction">請根據你<strong>過去一星期</strong>的情況，選擇最符合你能力或症狀的描述。</p>
  </div>

  <form id="dashForm">
    <div id="questions"></div>
    <button type="button" class="calc-btn" onclick="calculateQDASH()">計算評估結果</button>
  </form>

  <div id="warning" class="warning" aria-live="assertive"></div>
</div>

<div id="scoreModal" class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
  <div class="modal-content">
    <h2 id="modalTitle">評估結果</h2>
    <p id="rawScoreText" style="font-size: 1.25rem; margin: 8px 0; color: var(--text-muted);"></p>
    <p id="finalScoreText" style="font-size: 2.2rem; font-weight: 800; color: var(--primary); margin: 10px 0;"></p>
    <p style="font-size: 1rem; color: var(--text-muted); margin-bottom: 14px; line-height: 1.45;">QuickDASH 分數越低越好<br>（0 代表最佳功能，100 代表最嚴重失能）</p>

    <div class="notice-box">
      請不要離開此畫面，並出示給您的治療師。<br>
      您亦可以進行螢幕截圖。<br>
      謝謝。
    </div>
    
    <button type="button" class="close-btn" onclick="closeModal()">關閉</button>
  </div>
</div>

<script>
const questions = [
  "1. 扭開緊或新的瓶蓋",
  "2. 做消耗大量體力的家務（例如：抹窗或洗擦地板）",
  "3. 攜帶購物袋或公事包",
  "4. 清洗背部",
  "5. 用刀切食物",
  "6. 進行需要上肢發力或承受衝力的餘閒活動（如高爾夫、排球、網球等）",
  "7. 因肩膊、手臂或手部問題影響社交活動的程度",
  "8. 因肩膊、手臂或手部問題影響工作或日常活動的程度",
  "9. 肩膊、手臂或手部的痛楚程度",
  "10. 肩膊、手臂或手部的針刺感覺程度",
  "11. 因肩膊、手臂或手部痛楚引致睡眠困難的程度"
];

const labels = [
  "1 – 沒有困難 / 沒有症狀",
  "2 – 少許困難 / 輕微",
  "3 – 中度困難 / 中度",
  "4 – 非常困難 / 嚴重",
  "5 – 不能做到 / 極度"
];

const questionsDiv = document.getElementById("questions");

questions.forEach((q, index) => {
  const qNum = index + 1;
  const card = document.createElement("div");
  card.className = "question-card";
  card.id = `card-q${qNum}`;

  const header = document.createElement("div");
  header.className = "question-header";

  const title = document.createElement("div");
  title.className = "question-title";
  title.textContent = q;
  header.appendChild(title);

  card.appendChild(header);

  const optionsGroup = document.createElement("div");
  optionsGroup.className = "options-group";

  for (let i = 1; i <= 5; i++) {
    const label = document.createElement("label");
    label.className = "option-item";

    const radio = document.createElement("input");
    radio.type = "radio";
    radio.name = `q${qNum}`;
    radio.value = i;
    radio.className = "hidden-radio";

    radio.addEventListener("change", () => {
      const allLabels = card.querySelectorAll(".option-item");
      allLabels.forEach(l => l.classList.remove("selected"));
      label.classList.add("selected");
    });

    const dot = document.createElement("span");
    dot.className = "custom-radio";

    const text = document.createElement("span");
    text.className = "option-text";
    text.textContent = labels[i - 1];

    label.appendChild(radio);
    label.appendChild(dot);
    label.appendChild(text);
    optionsGroup.appendChild(label);
  }

  card.appendChild(optionsGroup);
  questionsDiv.appendChild(card);
});

function calculateQDASH() {
  const warning = document.getElementById("warning");
  warning.textContent = "";

  let total = 0;
  let count = 0;

  for (let i = 1; i <= 11; i++) {
    const selected = document.querySelector(`input[name="q${i}"]:checked`);
    if (!selected) {
      warning.textContent = `請先完成第 ${i} 題後再計算分數。`;
      const card = document.getElementById(`card-q${i}`);
      if (card) {
        card.scrollIntoView({ behavior: "smooth", block: "center" });
      }
      return;
    }
    total += parseInt(selected.value);
    count++;
  }

  // QuickDASH 公式: [ (總分 / 回答題數) - 1 ] × 25
  const mean = total / count;
  const finalScore = ((mean - 1) * 25).toFixed(1);

  document.getElementById("rawScoreText").innerHTML = `原始分數總和：<strong>${total}</strong> / 55`;
  document.getElementById("finalScoreText").innerHTML = `${finalScore}`;

  const modal = document.getElementById("scoreModal");
  modal.style.display = "flex";
}

function closeModal() {
  document.getElementById("scoreModal").style.display = "none";
}
</script>

</body>
</html>
