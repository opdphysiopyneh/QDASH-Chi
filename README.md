# QDASH-Chi

<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>QuickDASH Outcome Measure</title>
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
      font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display", "Segoe UI", Roboto, sans-serif;
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

    .main-title {
      font-size: clamp(1.35rem, 5.2vw, 1.75rem);
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
    <h1 class="main-title">QuickDASH Outcome Measure</h1>
    <p class="instruction">Please select the single option that best describes your condition <strong>in the past week</strong>.</p>
  </div>

  <form id="dashForm">
    <div id="questions"></div>
    <button type="button" class="calc-btn" onclick="calculateQDASH()">Calculate Assessment Result</button>
  </form>

  <div id="warning" class="warning" aria-live="assertive"></div>
</div>

<div id="scoreModal" class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
  <div class="modal-content">
    <h2 id="modalTitle">Assessment Result</h2>
    <p id="rawScoreText" style="font-size: 1.25rem; margin: 8px 0; color: var(--text-muted);"></p>
    <p id="finalScoreText" style="font-size: 2.2rem; font-weight: 800; color: var(--primary); margin: 10px 0;"></p>
    <p style="font-size: 1rem; color: var(--text-muted); margin-bottom: 14px; line-height: 1.45;">The lower the QuickDASH score, the better.<br>(0 represents no disability, 100 represents most severe disability)</p>

    <div class="notice-box">
      Please do not leave this page and present it to your therapist.<br>
      Alternatively, you may take a screenshot.<br>
      Thank you.
    </div>
    
    <button type="button" class="close-btn" onclick="closeModal()">Close</button>
  </div>
</div>

<script>
const questions = [
  "1. Open a tight or new jar.",
  "2. Do heavy household chores (e.g., wash walls, floors).",
  "3. Carry a shopping bag or briefcase.",
  "4. Wash your back.",
  "5. Use a knife to cut food.",
  "6. Recreational activities requiring force/impact through the arm (e.g., golf, hammering, tennis).",
  "7. Extent your arm/shoulder/hand problem interfered with social activities.",
  "8. Limitation in work or daily activities due to arm/shoulder/hand problem.",
  "9. Arm, shoulder or hand pain.",
  "10. Tingling (pins and needles) in your arm, shoulder or hand.",
  "11. Difficulty sleeping due to arm/shoulder/hand pain."
];

const labels = [
  "1 – No difficulty / None",
  "2 – Mild difficulty / Mild",
  "3 – Moderate difficulty / Moderate",
  "4 – Severe difficulty / Severe",
  "5 – Unable / Extreme"
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
      warning.textContent = `Please complete Question ${i} before calculating.`;
      const card = document.getElementById(`card-q${i}`);
      if (card) {
        card.scrollIntoView({ behavior: "smooth", block: "center" });
      }
      return;
    }
    total += parseInt(selected.value);
    count++;
  }

  // QuickDASH Formula: [ (sum of completed items / n) - 1 ] × 25
  const mean = total / count;
  const finalScore = ((mean - 1) * 25).toFixed(1);

  document.getElementById("rawScoreText").innerHTML = `Raw Total Score: <strong>${total}</strong> / 55`;
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
