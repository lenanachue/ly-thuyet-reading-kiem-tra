<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Kiểm tra Lý thuyết Reading</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --orange-deep:   #c0440a;
      --orange-main:   #e8621a;
      --orange-warm:   #f47c30;
      --orange-light:  #fba96a;
      --orange-pale:   #fef0e6;
      --orange-cream:  #fff8f2;
      --green-stem:    #5a7a3a;
      --green-leaf:    #7dae4e;
      --petal-1:       #f05a1a;
      --petal-2:       #e03a0a;
      --text-dark:     #2d1a06;
      --text-mid:      #7a4820;
      --text-soft:     #b07040;
    }

    body {
      min-height: 100vh;
      background: linear-gradient(160deg, #fff4ec 0%, #fde8d0 50%, #fdf0e0 100%);
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      overflow-x: hidden;
      position: relative;
    }

    /* ── Falling petals background ─────────────────────────────── */
    #petal-layer {
      position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden;
    }
    .petal {
      position: absolute;
      width: 12px; height: 16px;
      background: var(--petal-1);
      border-radius: 50% 50% 50% 0;
      opacity: 0;
      animation: fall linear infinite;
    }
    @keyframes fall {
      0%   { transform: translateY(-30px) rotate(0deg);  opacity: 0.7; }
      80%  { opacity: 0.5; }
      100% { transform: translateY(110vh) rotate(540deg); opacity: 0; }
    }

    /* ── Header ────────────────────────────────────────────────── */
    #header {
      background: linear-gradient(135deg, var(--orange-deep) 0%, var(--orange-main) 55%, var(--orange-warm) 100%);
      padding: 32px 20px 50px;
      text-align: center;
      position: relative;
      overflow: hidden;
      z-index: 1;
    }
    #header::before {
      content: "";
      position: absolute; inset: 0;
      background: radial-gradient(ellipse 60% 40% at 50% 0%, rgba(255,220,150,0.18) 0%, transparent 70%);
    }
    #header-tulips {
      display: flex; justify-content: center; gap: 20px; margin-bottom: 12px;
    }
    .tulip-svg { animation: sway 3s ease-in-out infinite; transform-origin: bottom center; }
    .tulip-svg:nth-child(2) { animation-delay: 0.5s; }
    .tulip-svg:nth-child(3) { animation-delay: 1.1s; }
    @keyframes sway {
      0%,100% { transform: rotate(-4deg); }
      50%      { transform: rotate(4deg); }
    }
    #header h1 {
      color: #fff; font-size: 22px; font-weight: 800;
      letter-spacing: 0.5px; text-shadow: 0 2px 10px rgba(100,30,0,0.3);
      margin-bottom: 5px; position: relative;
    }
    #header p { color: rgba(255,255,255,0.88); font-size: 13px; position: relative; }

    .wave-foot {
      position: absolute; bottom: -1px; left: 0; right: 0; height: 28px;
    }
    .wave-foot svg { display: block; width: 100%; height: 100%; }

    /* ── Main layout ───────────────────────────────────────────── */
    #main {
      max-width: 680px; margin: 0 auto;
      padding: 24px 16px 60px;
      position: relative; z-index: 1;
    }

    /* ── Intro banner ──────────────────────────────────────────── */
    .intro-banner {
      background: linear-gradient(135deg, #fff3e8, #ffe0c5);
      border: 1.5px solid var(--orange-light);
      border-radius: 16px; padding: 18px 22px;
      margin-bottom: 24px;
      display: flex; align-items: flex-start; gap: 14px;
    }
    .intro-icon { font-size: 32px; flex-shrink: 0; margin-top: 2px; }
    .intro-banner h2 { color: var(--orange-deep); font-size: 15px; font-weight: 800; margin-bottom: 4px; }
    .intro-banner p  { color: var(--text-mid); font-size: 13px; line-height: 1.55; }

    /* ── Progress bar ──────────────────────────────────────────── */
    #progress-wrap {
      margin-bottom: 20px;
      display: flex; align-items: center; gap: 12px;
    }
    #progress-label { font-size: 12px; color: var(--text-soft); font-weight: 600; white-space: nowrap; }
    #progress-bar-bg {
      flex: 1; height: 8px; background: #f0d9c8; border-radius: 99px; overflow: hidden;
    }
    #progress-bar-fill {
      height: 100%; width: 0%;
      background: linear-gradient(90deg, var(--orange-warm), var(--orange-deep));
      border-radius: 99px;
      transition: width 0.5s ease;
    }

    /* ── Question cards ────────────────────────────────────────── */
    .q-card {
      background: var(--orange-cream);
      border: 1.5px solid #f0d0b0;
      border-radius: 16px; padding: 20px 22px;
      margin-bottom: 16px;
      transition: border-color 0.3s, box-shadow 0.3s;
      box-shadow: 0 2px 10px rgba(200,80,10,0.07);
      position: relative;
      overflow: hidden;
    }
    .q-card::before {
      content: "";
      position: absolute; top: 0; left: 0;
      width: 5px; height: 100%;
      background: linear-gradient(180deg, var(--orange-warm), var(--orange-deep));
      border-radius: 16px 0 0 16px;
    }
    .q-card.correct { background: #f0fdf0; border-color: #7ecf7e; box-shadow: 0 2px 12px rgba(80,190,80,0.12); }
    .q-card.correct::before { background: linear-gradient(180deg, #5dba5d, #2e8a2e); }
    .q-card.wrong   { background: #fff4f4; border-color: #f0a0a0; box-shadow: 0 2px 12px rgba(220,80,80,0.10); }
    .q-card.wrong::before   { background: linear-gradient(180deg, #f08080, #c03030); }

    .q-header { display: flex; align-items: center; gap: 8px; margin-bottom: 12px; }
    .q-badge {
      background: linear-gradient(135deg, var(--orange-warm), var(--orange-deep));
      color: #fff; border-radius: 8px;
      padding: 3px 11px; font-size: 12px; font-weight: 700; flex-shrink: 0;
    }
    .q-badge.correct { background: linear-gradient(135deg, #5dba5d, #2e8a2e); }
    .q-badge.wrong   { background: linear-gradient(135deg, #f08080, #c03030); }
    .q-tag {
      font-size: 11px; background: #f9e4d0; border-radius: 6px;
      padding: 2px 9px; color: var(--orange-deep); font-weight: 600;
    }
    .q-text {
      font-size: 14px; font-weight: 700; color: var(--text-dark);
      line-height: 1.55; margin-bottom: 14px; padding-left: 6px;
    }

    .options { display: grid; gap: 9px; }
    .opt-btn {
      background: #fff8f2; border: 1.5px solid #f0d5be;
      border-radius: 11px; padding: 10px 14px;
      text-align: left; cursor: pointer;
      font-size: 13.5px; color: var(--text-dark);
      font-weight: 400; transition: all 0.2s ease;
      outline: none; line-height: 1.45; width: 100%;
    }
    .opt-btn:hover:not(:disabled) {
      background: var(--orange-pale); border-color: var(--orange-light);
      transform: translateX(3px);
    }
    .opt-btn.selected  { background: #ffe8d4; border-color: var(--orange-warm); font-weight: 600; color: var(--orange-deep); }
    .opt-btn.is-answer { background: #d4f4d4; border-color: #5dba5d; font-weight: 700; color: #1a5a1a; }
    .opt-btn.is-wrong  { background: #fde0e0; border-color: #f08080; font-weight: 600; color: #a01515; }
    .opt-btn:disabled  { cursor: default; }

    .explanation {
      margin-top: 12px; padding: 10px 14px; border-radius: 10px;
      font-size: 13px; color: var(--text-dark); line-height: 1.6;
      display: none;
    }
    .explanation.show { display: block; }
    .explanation.correct { background: rgba(93,186,93,0.12); border: 1px solid #b0deb0; }
    .explanation.wrong   { background: rgba(240,128,128,0.10); border: 1px solid #f0c0c0; }

    /* ── Score banner ──────────────────────────────────────────── */
    #score-banner {
      display: none;
      background: linear-gradient(135deg, #fff0e0, #ffe0c5);
      border: 2px solid var(--orange-light);
      border-radius: 18px; padding: 28px 26px;
      text-align: center; margin-bottom: 24px;
      position: relative; overflow: hidden;
    }
    #score-banner.show { display: block; animation: popIn 0.5s cubic-bezier(0.34,1.56,0.64,1); }
    @keyframes popIn {
      from { transform: scale(0.85); opacity: 0; }
      to   { transform: scale(1);    opacity: 1; }
    }
    #score-banner .tulip-row {
      display: flex; justify-content: center; gap: 10px;
      margin-bottom: 10px;
    }
    #score-emoji  { font-size: 36px; margin-bottom: 4px; }
    #score-pct    { font-size: 36px; font-weight: 900; color: var(--orange-deep); line-height: 1; }
    #score-label  { font-size: 14px; color: var(--text-mid); margin: 6px 0 14px; }
    .score-row    { display: flex; justify-content: center; gap: 28px; font-size: 14px; color: var(--text-dark); }
    #score-msg    {
      margin-top: 14px; font-size: 14px; font-weight: 700;
      color: var(--orange-deep); background: rgba(255,255,255,0.7);
      border-radius: 10px; padding: 8px 16px; display: inline-block;
    }

    /* ── History ───────────────────────────────────────────────── */
    .history-bar {
      margin-bottom: 24px;
      background: var(--orange-cream); border: 1.5px solid #f0d0b0;
      border-radius: 14px; padding: 14px 18px;
    }
    .history-bar h3 { font-size: 13px; color: var(--text-mid); font-weight: 700; margin-bottom: 10px; }
    .h-stats { display: flex; gap: 20px; }
    .h-stat { text-align: center; }
    .h-stat .val { font-size: 20px; font-weight: 800; color: var(--orange-deep); }
    .h-stat .lbl { font-size: 10px; color: var(--text-soft); }
    .h-entries { margin-top: 10px; display: flex; flex-direction: column; gap: 6px; }
    .h-entry {
      background: #fff8f2; border-radius: 8px; padding: 7px 12px;
      display: flex; justify-content: space-between; align-items: center;
      font-size: 12px; color: var(--text-dark); border: 1px solid #f0d5be;
    }
    .h-entry .h-pct-chip {
      font-weight: 800; font-size: 13px;
      padding: 2px 10px; border-radius: 8px; background: var(--orange-pale); color: var(--orange-deep);
    }
    .h-entry .h-pct-chip.good { background: #dff4df; color: #2a7a2a; }
    .btn-clear-h {
      margin-top: 8px; font-size: 11px; background: transparent;
      border: 1px solid #f0a0a0; color: #c04040; border-radius: 6px;
      padding: 4px 12px; cursor: pointer;
    }

    /* ── Buttons ───────────────────────────────────────────────── */
    .btn-row { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
    .btn-submit {
      background: linear-gradient(135deg, var(--orange-warm), var(--orange-deep));
      color: #fff; border: none; border-radius: 12px;
      padding: 13px 40px; font-size: 15px; font-weight: 800;
      cursor: pointer; box-shadow: 0 4px 16px rgba(200,80,10,0.35);
      letter-spacing: 0.3px; transition: transform 0.15s, box-shadow 0.15s;
    }
    .btn-submit:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(200,80,10,0.45); }
    .btn-reset {
      background: linear-gradient(135deg, #fba96a, var(--orange-warm));
      color: #fff; border: none; border-radius: 12px;
      padding: 13px 40px; font-size: 15px; font-weight: 800;
      cursor: pointer; box-shadow: 0 4px 16px rgba(200,80,10,0.25);
      transition: transform 0.15s;
    }
    .btn-reset:hover { transform: translateY(-2px); }
  </style>
</head>
<body>

<!-- Falling petals -->
<div id="petal-layer"></div>

<!-- Header -->
<div id="header">
  <div id="header-tulips">
    <!-- Tulip 1 -->
    <svg class="tulip-svg" width="48" height="80" viewBox="0 0 48 80">
      <line x1="24" y1="80" x2="24" y2="38" stroke="#5a7a3a" stroke-width="3" stroke-linecap="round"/>
      <path d="M24 52 Q14 46 12 36 Q20 34 24 42 Q28 34 36 36 Q34 46 24 52Z" fill="#7dae4e"/>
      <ellipse cx="24" cy="27" rx="8" ry="11" fill="#e03a0a"/>
      <ellipse cx="17" cy="30" rx="6" ry="10" fill="#f05a1a" transform="rotate(-18,17,30)"/>
      <ellipse cx="31" cy="30" rx="6" ry="10" fill="#f05a1a" transform="rotate(18,31,30)"/>
      <ellipse cx="24" cy="18" rx="5" ry="9" fill="#f47c30"/>
    </svg>
    <!-- Tulip 2 (taller, center) -->
    <svg class="tulip-svg" width="52" height="88" viewBox="0 0 52 88">
      <line x1="26" y1="88" x2="26" y2="42" stroke="#5a7a3a" stroke-width="3.5" stroke-linecap="round"/>
      <path d="M26 58 Q14 50 12 38 Q22 36 26 46 Q30 36 40 38 Q38 50 26 58Z" fill="#7dae4e"/>
      <ellipse cx="26" cy="30" rx="9" ry="13" fill="#c0440a"/>
      <ellipse cx="18" cy="34" rx="7" ry="11" fill="#e8621a" transform="rotate(-20,18,34)"/>
      <ellipse cx="34" cy="34" rx="7" ry="11" fill="#e8621a" transform="rotate(20,34,34)"/>
      <ellipse cx="26" cy="20" rx="6" ry="10" fill="#f47c30"/>
    </svg>
    <!-- Tulip 3 -->
    <svg class="tulip-svg" width="48" height="80" viewBox="0 0 48 80">
      <line x1="24" y1="80" x2="24" y2="38" stroke="#5a7a3a" stroke-width="3" stroke-linecap="round"/>
      <path d="M24 54 Q12 48 10 36 Q18 34 24 44 Q30 34 38 36 Q36 48 24 54Z" fill="#7dae4e"/>
      <ellipse cx="24" cy="27" rx="8" ry="11" fill="#f05a1a"/>
      <ellipse cx="17" cy="30" rx="6" ry="10" fill="#fba96a" transform="rotate(-18,17,30)"/>
      <ellipse cx="31" cy="30" rx="6" ry="10" fill="#fba96a" transform="rotate(18,31,30)"/>
      <ellipse cx="24" cy="18" rx="5" ry="9" fill="#e8621a"/>
    </svg>
  </div>
  <h1>🌷 Kiểm tra Lý thuyết Reading</h1>
  <p>Đọc kỹ lý thuyết chưa? Hãy thử sức ngay!</p>
  <div class="wave-foot">
    <svg viewBox="0 0 1200 28" preserveAspectRatio="none">
      <path d="M0,14 Q150,0 300,14 T600,14 T900,14 T1200,14 L1200,28 L0,28 Z" fill="#fff4ec"/>
    </svg>
  </div>
</div>

<!-- Main -->
<div id="main">

  <!-- History bar -->
  <div class="history-bar" id="history-bar" style="display:none">
    <h3>📊 Lịch sử làm bài</h3>
    <div class="h-stats" id="h-stats"></div>
    <div class="h-entries" id="h-entries"></div>
    <button class="btn-clear-h" onclick="clearHistory()">🗑️ Xóa lịch sử</button>
  </div>

  <!-- Intro -->
  <div class="intro-banner">
    <div class="intro-icon">📘</div>
    <div>
      <h2>Kiểm tra mức độ đọc lý thuyết</h2>
      <p>Bộ câu hỏi này kiểm tra xem em đã hiểu đúng và nhớ chính xác 6 dạng câu hỏi đọc hiểu cùng các mẹo làm bài chưa. Chọn đáp án đúng nhất nhé!</p>
    </div>
  </div>

  <!-- Progress -->
  <div id="progress-wrap">
    <span id="progress-label">0 / 12 câu</span>
    <div id="progress-bar-bg"><div id="progress-bar-fill"></div></div>
  </div>

  <!-- Score banner (hidden until submit) -->
  <div id="score-banner">
    <div class="tulip-row">🌷🌷🌷</div>
    <div id="score-emoji">🎉</div>
    <div id="score-pct">—</div>
    <div id="score-label">điểm số của em</div>
    <div class="score-row">
      <span>✅ Đúng: <strong id="score-correct">—</strong></span>
      <span>❌ Sai: <strong id="score-wrong">—</strong></span>
      <span>📝 Tổng: <strong>12</strong></span>
    </div>
    <div id="score-msg"></div>
  </div>

  <!-- Questions container -->
  <div id="questions-container"></div>

  <!-- Action buttons -->
  <div class="btn-row" id="btn-row">
    <button class="btn-submit" id="btn-submit" onclick="submitQuiz()">🌷 Nộp bài</button>
  </div>

</div>

<script>
// ─── DATA ──────────────────────────────────────────────────────────────────────
const QUESTIONS = [
  // === NHÓM 1: Nhận biết định nghĩa dạng câu hỏi ===
  {
    id: 1,
    tag: "Nhận biết dạng",
    text: "Câu hỏi dạng nào yêu cầu em xác định CHỦ ĐỀ hoặc Ý CHÍNH của toàn bài đọc?",
    options: [
      "A. Factual (Lấy thông tin)",
      "B. Inference (Suy diễn)",
      "C. Main Idea (Ý chính)",
      "D. Reference (Liên hệ đại từ)"
    ],
    answer: 2,
    explanation: "Dạng Main Idea yêu cầu xác định chủ đề hoặc ý chính của bài đọc. Câu hỏi thường có dạng: 'What is the topic / main idea of this passage?'"
  },
  {
    id: 2,
    tag: "Nhận biết dạng",
    text: "Khi gặp câu hỏi 'According to the passage, why did...?', em đang làm dạng câu hỏi nào?",
    options: [
      "A. Vocabulary (Từ vựng)",
      "B. Factual (Lấy thông tin)",
      "C. Inference (Suy diễn)",
      "D. Author's Purpose (Mục đích tác giả)"
    ],
    answer: 1,
    explanation: "Câu hỏi Factual tìm thông tin được nêu TRỰC TIẾP trong bài. Dấu hiệu nhận biết là cụm 'According to the passage...'"
  },
  {
    id: 3,
    tag: "Nhận biết dạng",
    text: "Câu hỏi: 'The word \"X\" is closest in meaning to...' thuộc dạng nào?",
    options: [
      "A. Inference",
      "B. Reference",
      "C. Vocabulary",
      "D. Main Idea"
    ],
    answer: 2,
    explanation: "Dạng Vocabulary yêu cầu đoán nghĩa từ dựa vào ngữ cảnh hoặc tìm từ đồng nghĩa. Cụm 'closest in meaning to' là dấu hiệu đặc trưng."
  },
  {
    id: 4,
    tag: "Nhận biết dạng",
    text: "Câu hỏi 'It can be inferred from the passage that...' thuộc dạng nào?",
    options: [
      "A. Factual",
      "B. Inference",
      "C. Reference",
      "D. Vocabulary"
    ],
    answer: 1,
    explanation: "Dạng Inference yêu cầu SUY RA ý nghĩa ẩn từ thông tin trong bài. Thông tin không được nêu thẳng mà cần suy luận."
  },
  {
    id: 5,
    tag: "Nhận biết dạng",
    text: "Câu hỏi 'The word \"it\" in line X refers to...' thuộc dạng nào?",
    options: [
      "A. Vocabulary",
      "B. Main Idea",
      "C. Reference",
      "D. Factual"
    ],
    answer: 2,
    explanation: "Dạng Reference xác định đại từ (it, they, these...) trong bài đang thay thế cho từ hoặc cụm từ nào."
  },
  {
    id: 6,
    tag: "Nhận biết dạng",
    text: "Câu hỏi 'Why does the author mention...?' hoặc 'What is the author's opinion?' thuộc dạng nào?",
    options: [
      "A. Factual",
      "B. Inference",
      "C. Vocabulary",
      "D. Mục đích / Thái độ tác giả"
    ],
    answer: 3,
    explanation: "Dạng Mục đích / Thái độ tác giả yêu cầu hiểu LÝ DO tác giả đề cập và QUAN ĐIỂM của tác giả trong bài."
  },

  // === NHÓM 2: Phân biệt đặc điểm từng dạng ===
  {
    id: 7,
    tag: "Phân biệt đặc điểm",
    text: "Điểm khác nhau cơ bản giữa dạng Factual và dạng Inference là gì?",
    options: [
      "A. Factual tìm thông tin trực tiếp trong bài; Inference suy ra ý không được nêu thẳng",
      "B. Factual và Inference đều tìm thông tin ẩn trong bài",
      "C. Factual liên quan đến từ vựng; Inference liên quan đến ý chính",
      "D. Factual dễ hơn Inference vì câu hỏi ngắn hơn"
    ],
    answer: 0,
    explanation: "Factual = thông tin TRỰC TIẾP có trong bài. Inference = thông tin ẨN, phải suy luận từ những gì được viết."
  },
  {
    id: 8,
    tag: "Phân biệt đặc điểm",
    text: "Khi làm câu hỏi dạng Vocabulary, em cần làm gì để tìm nghĩa từ chính xác nhất?",
    options: [
      "A. Tra từ điển ngay lập tức",
      "B. Đọc cả đoạn văn xung quanh từ đó để hiểu nghĩa qua ngữ cảnh",
      "C. Chọn từ nào nghe quen nhất",
      "D. Dịch từng từ trong câu sang tiếng Việt"
    ],
    answer: 1,
    explanation: "Dạng Vocabulary yêu cầu ĐOÁN NGHĨA DỰA VÀO NGỮ CẢNH. Đọc câu chứa từ đó và câu xung quanh để suy ra nghĩa phù hợp."
  },
  {
    id: 9,
    tag: "Phân biệt đặc điểm",
    text: "Theo lý thuyết, dạng Reference đặc biệt chú ý đến loại từ nào trong bài đọc?",
    options: [
      "A. Danh từ chỉ người (nouns naming people)",
      "B. Tính từ (adjectives)",
      "C. Đại từ như it, they, these, those...",
      "D. Liên từ như and, but, because..."
    ],
    answer: 2,
    explanation: "Dạng Reference xác định đại từ (pronouns) như it, they, these, those... đang chỉ hoặc thay thế cho từ nào trong bài."
  },

  // === NHÓM 3: Mẹo làm bài ===
  {
    id: 10,
    tag: "Mẹo làm bài",
    text: "Theo phần Mẹo làm bài, em nên làm gì ĐẦU TIÊN khi nhận được bài đọc?",
    options: [
      "A. Đọc câu hỏi ngay để biết cần tìm gì",
      "B. Đọc đáp án trước rồi mới đọc bài",
      "C. Đọc lướt toàn bài để nắm nội dung chính",
      "D. Bắt đầu làm câu khó nhất trước"
    ],
    answer: 2,
    explanation: "Mẹo số 1: Đọc lướt để nắm nội dung chính TRƯỚC KHI đọc câu hỏi. Điều này giúp em có cái nhìn tổng thể về bài."
  },
  {
    id: 11,
    tag: "Mẹo làm bài",
    text: "Khi chưa chắc đáp án, mẹo làm bài gợi ý em nên dùng phương pháp nào?",
    options: [
      "A. Chọn đáp án đầu tiên vì thường đúng",
      "B. Phương pháp loại trừ",
      "C. Chọn đáp án dài nhất",
      "D. Hỏi bạn bên cạnh"
    ],
    answer: 1,
    explanation: "Mẹo số 4: Dùng phương pháp loại trừ — gạch bỏ các đáp án chắc chắn sai để thu hẹp lựa chọn, tăng khả năng chọn đúng."
  },
  {
    id: 12,
    tag: "Mẹo làm bài",
    text: "Mẹo làm bài khuyên em nên xử lý các câu hỏi theo thứ tự nào?",
    options: [
      "A. Từ câu cuối lên câu đầu",
      "B. Ngẫu nhiên, không theo thứ tự",
      "C. Câu dài trước, câu ngắn sau",
      "D. Làm câu dễ trước, quay lại câu khó sau"
    ],
    answer: 3,
    explanation: "Mẹo số 5: Làm câu dễ trước, quay lại câu khó sau. Cách này giúp em đảm bảo điểm ở câu chắc chắn và không mất thời gian vào câu khó sớm."
  }
];

// ─── STATE ──────────────────────────────────────────────────────────────────────
const state = {
  selected: {},
  submitted: false
};
let history = [];
try {
  const s = localStorage.getItem("ly-thuyet-quiz-history");
  if (s) history = JSON.parse(s);
} catch(e) {}

// ─── PETALS ─────────────────────────────────────────────────────────────────────
(function() {
  const layer = document.getElementById("petal-layer");
  const colors = ["#f05a1a","#e03a0a","#fba96a","#f47c30","#c0440a"];
  for (let i = 0; i < 18; i++) {
    const p = document.createElement("div");
    p.className = "petal";
    const size = 8 + Math.random() * 10;
    p.style.cssText = `
      left: ${Math.random() * 100}%;
      top: ${-20 - Math.random() * 60}px;
      width: ${size}px; height: ${size * 1.3}px;
      background: ${colors[i % colors.length]};
      animation-duration: ${7 + Math.random() * 8}s;
      animation-delay: ${Math.random() * 8}s;
      opacity: ${0.4 + Math.random() * 0.4};
      transform: rotate(${Math.random() * 360}deg);
    `;
    layer.appendChild(p);
  }
})();

// ─── RENDER ─────────────────────────────────────────────────────────────────────
function render() {
  const container = document.getElementById("questions-container");
  let html = "";
  QUESTIONS.forEach((q, qi) => {
    const sel = state.selected[qi];
    const sub = state.submitted;
    const isCorrect = sub && sel === q.answer;
    const isWrong   = sub && sel !== undefined && sel !== q.answer;

    html += `
      <div class="q-card ${sub ? (isCorrect ? 'correct' : (sel !== undefined ? 'wrong' : '')) : ''}" id="qcard-${qi}">
        <div class="q-header">
          <span class="q-badge ${sub ? (isCorrect ? 'correct' : (sel !== undefined ? 'wrong' : '')) : ''}">
            ${sub ? (isCorrect ? '✓' : (sel !== undefined ? '✗' : 'Q' + q.id)) : 'Q' + q.id}
          </span>
          <span class="q-tag">${q.tag}</span>
        </div>
        <p class="q-text">${q.text}</p>
        <div class="options">
          ${q.options.map((opt, oi) => {
            let cls = "opt-btn";
            if (!sub && sel === oi) cls += " selected";
            if (sub) {
              if (oi === q.answer) cls += " is-answer";
              else if (sel === oi) cls += " is-wrong";
            }
            const prefix = sub ? (oi === q.answer ? "✅ " : (sel === oi ? "❌ " : "")) : "";
            return `<button class="${cls}" ${sub ? 'disabled' : ''}
              data-qi="${qi}" data-oi="${oi}">${prefix}${opt}</button>`;
          }).join("")}
        </div>
        <div class="explanation ${sub ? 'show' : ''} ${isCorrect ? 'correct' : 'wrong'}">
          <strong>💡 Giải thích:</strong> ${q.explanation}
        </div>
      </div>
    `;
  });
  container.innerHTML = html;

  // event delegation
  container.querySelectorAll(".opt-btn").forEach(btn => {
    btn.addEventListener("click", () => {
      if (state.submitted) return;
      const qi = parseInt(btn.dataset.qi);
      const oi = parseInt(btn.dataset.oi);
      state.selected[qi] = oi;
      updateProgress();
      render();
    });
  });

  updateProgress();
  renderBtnRow();
}

function updateProgress() {
  const done = Object.keys(state.selected).length;
  const total = QUESTIONS.length;
  document.getElementById("progress-label").textContent = `${done} / ${total} câu`;
  document.getElementById("progress-bar-fill").style.width = `${(done / total) * 100}%`;
}

function renderBtnRow() {
  const row = document.getElementById("btn-row");
  if (state.submitted) {
    row.innerHTML = `<button class="btn-reset" onclick="resetQuiz()">🔄 Làm lại</button>`;
  } else {
    row.innerHTML = `<button class="btn-submit" onclick="submitQuiz()">🌷 Nộp bài</button>`;
  }
}

// ─── SUBMIT ──────────────────────────────────────────────────────────────────────
function submitQuiz() {
  const done = Object.keys(state.selected).length;
  if (done < QUESTIONS.length) {
    alert(`Em chưa trả lời hết! Còn ${QUESTIONS.length - done} câu chưa chọn.`);
    return;
  }
  state.submitted = true;

  const correct = QUESTIONS.filter((q, i) => state.selected[i] === q.answer).length;
  const total   = QUESTIONS.length;
  const pct     = Math.round((correct / total) * 100);

  // Score banner
  const banner = document.getElementById("score-banner");
  banner.classList.add("show");
  document.getElementById("score-emoji").textContent  = pct >= 80 ? "🎉" : pct >= 50 ? "👍" : "💪";
  document.getElementById("score-pct").textContent    = pct + "%";
  document.getElementById("score-correct").textContent = correct;
  document.getElementById("score-wrong").textContent   = total - correct;
  document.getElementById("score-msg").textContent =
    pct >= 80 ? "Xuất sắc! Em đã đọc kỹ lý thuyết rồi 🌷" :
    pct >= 50 ? "Khá tốt! Đọc lại những câu sai để nắm chắc hơn nhé." :
                "Cần đọc lại lý thuyết thật kỹ trước khi làm bài!";
  banner.scrollIntoView({ behavior: "smooth", block: "start" });

  // Save history
  saveHistory(correct, total, pct);
  render();
}

function resetQuiz() {
  state.selected = {};
  state.submitted = false;
  document.getElementById("score-banner").classList.remove("show");
  render();
  window.scrollTo({ top: 0, behavior: "smooth" });
}

// ─── HISTORY ─────────────────────────────────────────────────────────────────────
function saveHistory(correct, total, pct) {
  const entry = {
    correct, total, pct,
    date: new Date().toLocaleString("vi-VN")
  };
  history = [entry, ...history].slice(0, 10);
  try { localStorage.setItem("ly-thuyet-quiz-history", JSON.stringify(history)); } catch(e) {}
  renderHistory();
}

function renderHistory() {
  const bar = document.getElementById("history-bar");
  if (!history.length) { bar.style.display = "none"; return; }
  bar.style.display = "";

  const avg  = Math.round(history.reduce((a, h) => a + h.pct, 0) / history.length);
  const best = Math.max(...history.map(h => h.pct));

  document.getElementById("h-stats").innerHTML = `
    <div class="h-stat"><div class="val">${history.length}</div><div class="lbl">Lần làm</div></div>
    <div class="h-stat"><div class="val">${avg}%</div><div class="lbl">Trung bình</div></div>
    <div class="h-stat"><div class="val">${best}%</div><div class="lbl">Cao nhất</div></div>
  `;

  document.getElementById("h-entries").innerHTML = history.slice(0, 5).map(h => `
    <div class="h-entry">
      <span>${h.date} — ✅${h.correct}/❌${h.total - h.correct}</span>
      <span class="h-pct-chip ${h.pct >= 80 ? 'good' : ''}">${h.pct}%</span>
    </div>
  `).join("");
}

function clearHistory() {
  if (!confirm("Xóa toàn bộ lịch sử điểm?")) return;
  history = [];
  try { localStorage.removeItem("ly-thuyet-quiz-history"); } catch(e) {}
  renderHistory();
}

// ─── INIT ─────────────────────────────────────────────────────────────────────────
renderHistory();
render();
</script>
</body>
</html>
