<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>eBook Viewer</title>

  <style>
    body{
      font-family: "Noto Serif KR", serif;
      background:#f5f3ef;
      margin:0;
      padding:0;
      display:flex;
      justify-content:center;
    }

    .container{
      max-width:700px;
      width:100%;
      background:white;
      min-height:100vh;
      padding:30px 20px 40px;
      box-shadow:0 0 20px rgba(0,0,0,0.05);
      box-sizing:border-box;
    }

    .book-frame{
      position:relative;
      overflow:hidden;
      min-height:760px;
    }

    .page-card{
      width:100%;
      opacity:1;
      transform:translateX(0);
      transition:opacity 0.35s ease, transform 0.35s ease;
    }

    .page-card.fade-out-left{
      opacity:0;
      transform:translateX(-30px);
    }

    .page-card.fade-out-right{
      opacity:0;
      transform:translateX(30px);
    }

    .page-card.fade-in{
      opacity:0;
      transform:translateX(20px);
    }

    .page-card.fade-in.active{
      opacity:1;
      transform:translateX(0);
    }

    .cover{
      text-align:center;
      padding:40px 10px 20px;
    }

    .cover-image{
      width:100%;
      max-height:520px;
      object-fit:cover;
      border-radius:12px;
      margin-bottom:28px;
      box-shadow:0 8px 24px rgba(0,0,0,0.08);
    }

    .cover-title{
      font-size:30px;
      line-height:1.4;
      margin-bottom:14px;
      font-weight:700;
      color:#2f2a24;
      text-align:center;
    }

    .cover-subtitle{
      font-size:17px;
      line-height:1.8;
      color:#6b6258;
      text-align:center;
      white-space:pre-line;
    }

    .title{
      text-align:center;
      font-size:26px;
      margin-bottom:20px;
      font-weight:600;
      color:#2f2a24;
    }

    .image{
      width:100%;
      border-radius:10px;
      margin-bottom:25px;
      display:block;
      box-shadow:0 8px 24px rgba(0,0,0,0.06);
    }

    .text{
      font-size:18px;
      line-height:1.9;
      text-align:left;
      white-space:pre-line;
      margin-bottom:30px;
      color:#333;
      padding:0 4px;
    }

    .navigation{
      display:flex;
      justify-content:space-between;
      gap:12px;
      margin-top:20px;
    }

    .nav-left,
    .nav-right{
      display:flex;
      gap:10px;
      align-items:center;
    }

    button{
      padding:12px 18px;
      border:none;
      background:#8c7a5b;
      color:white;
      border-radius:8px;
      cursor:pointer;
      font-size:15px;
    }

    button:hover{
      background:#6f5f46;
    }

    button:disabled{
      background:#c7beb0;
      cursor:not-allowed;
    }

    .page{
      text-align:center;
      margin-top:15px;
      color:#999;
      font-size:15px;
    }

    .audio-status{
      text-align:center;
      margin-top:14px;
      color:#7a6f62;
      font-size:14px;
      min-height:20px;
    }

    @media (max-width: 768px){
      .container{
        padding:20px 14px 30px;
      }

      .book-frame{
        min-height:auto;
      }

      .cover-title{
        font-size:25px;
      }

      .title{
        font-size:22px;
      }

      .text{
        font-size:17px;
      }

      .navigation{
        flex-direction:column;
      }

      .nav-left,
      .nav-right{
        width:100%;
        justify-content:space-between;
      }

      button{
        flex:1;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="book-frame">
      <div id="pageCard" class="page-card">
        <div id="content"></div>
      </div>
    </div>

    <div class="navigation">
      <div class="nav-left">
        <button id="prevBtn" onclick="prev()">← 이전</button>
        <button id="speakBtn" onclick="toggleSpeech()">🔊 읽기</button>
      </div>

      <div class="nav-right">
        <button id="stopBtn" onclick="stopSpeech()">■ 정지</button>
        <button id="nextBtn" onclick="next()">다음 →</button>
      </div>
    </div>

    <div id="page" class="page"></div>
    <div id="audioStatus" class="audio-status"></div>
  </div>

  <script>
    let currentPage = -1; // -1 = cover page
    let data = null;
    let isSpeaking = false;
    let currentUtterance = null;
    let currentVoice = null;

    const params = new URLSearchParams(location.search);
    const book = params.get("book") || "story-01";

    fetch(`../data/stories/${book}.json`)
      .then(res => res.json())
      .then(json => {
        data = json;
        loadVoices();
        renderPage("init");
      });

    function loadVoices(){
      const voices = speechSynthesis.getVoices();
      currentVoice =
        voices.find(v => v.lang && v.lang.toLowerCase().includes("ko")) ||
        voices.find(v => v.lang && v.lang.toLowerCase().includes("en")) ||
        null;
    }

    speechSynthesis.onvoiceschanged = () => {
      loadVoices();
    };

    function getTotalPages(){
      return (data?.pages?.length || 0) + 1; // cover 포함
    }

    function getReadableText(){
      if (!data) return "";

      if (currentPage === -1) {
        return `${data.title || ""}\n${data.description || ""}`.trim();
      }

      const pageData = data.pages[currentPage];
      return (pageData?.text || "").trim();
    }

    function renderPage(direction = "init"){
      const pageCard = document.getElementById("pageCard");

      if (direction === "next") {
        pageCard.className = "page-card fade-out-left";
      } else if (direction === "prev") {
        pageCard.className = "page-card fade-out-right";
      }

      setTimeout(() => {
        const content = document.getElementById("content");

        if (currentPage === -1) {
          content.innerHTML = `
            <div class="cover">
              ${
                data.coverImage
                  ? `<img src="../public${data.coverImage}" alt="cover" class="cover-image">`
                  : ""
              }
              <div class="cover-title">${escapeHtml(data.title || "제목 없음")}</div>
              <div class="cover-subtitle">${escapeHtml(data.description || "")}</div>
            </div>
          `;
        } else {
          const p = data.pages[currentPage];

          content.innerHTML = `
            <div class="title">${escapeHtml(data.title || "")}</div>
            ${
              p.image
                ? `<img src="../public${p.image}" alt="page image" class="image">`
                : ""
            }
            <div class="text">${escapeHtml(p.text || "")}</div>
          `;
        }

        const currentNumber = currentPage + 2; // cover가 1페이지
        document.getElementById("page").innerText = `${currentNumber} / ${getTotalPages()}`;

        document.getElementById("prevBtn").disabled = currentPage === -1;
        document.getElementById("nextBtn").disabled = currentPage === data.pages.length - 1;

        pageCard.className = "page-card fade-in";
        requestAnimationFrame(() => {
          pageCard.classList.add("active");
        });

        stopSpeech(false);
      }, direction === "init" ? 0 : 180);
    }

    function next(){
      if (!data) return;
      if (currentPage < data.pages.length - 1) {
        currentPage++;
        renderPage("next");
      }
    }

    function prev(){
      if (!data) return;
      if (currentPage > -1) {
        currentPage--;
        renderPage("prev");
      }
    }

    function toggleSpeech(){
      if (!("speechSynthesis" in window)) {
        document.getElementById("audioStatus").innerText = "이 브라우저에서는 음성 읽기를 지원하지 않습니다.";
        return;
      }

      if (isSpeaking) {
        stopSpeech();
        return;
      }

      const text = getReadableText();
      if (!text) {
        document.getElementById("audioStatus").innerText = "읽을 텍스트가 없습니다.";
        return;
      }

      speechSynthesis.cancel();

      currentUtterance = new SpeechSynthesisUtterance(text);
      currentUtterance.lang = "ko-KR";
      currentUtterance.rate = 0.95;
      currentUtterance.pitch = 1;
      currentUtterance.volume = 1;

      if (currentVoice) {
        currentUtterance.voice = currentVoice;
      }

      currentUtterance.onstart = () => {
        isSpeaking = true;
        document.getElementById("speakBtn").innerText = "⏸ 읽는 중";
        document.getElementById("audioStatus").innerText = "페이지를 읽고 있습니다.";
      };

      currentUtterance.onend = () => {
        isSpeaking = false;
        document.getElementById("speakBtn").innerText = "🔊 읽기";
        document.getElementById("audioStatus").innerText = "";
      };

      currentUtterance.onerror = () => {
        isSpeaking = false;
        document.getElementById("speakBtn").innerText = "🔊 읽기";
        document.getElementById("audioStatus").innerText = "음성 읽기 중 문제가 발생했습니다.";
      };

      speechSynthesis.speak(currentUtterance);
    }

    function stopSpeech(showMessage = true){
      if ("speechSynthesis" in window) {
        speechSynthesis.cancel();
      }

      isSpeaking = false;
      document.getElementById("speakBtn").innerText = "🔊 읽기";

      if (showMessage) {
        document.getElementById("audioStatus").innerText = "읽기를 멈췄습니다.";
        setTimeout(() => {
          if (!isSpeaking) {
            document.getElementById("audioStatus").innerText = "";
          }
        }, 1200);
      } else {
        document.getElementById("audioStatus").innerText = "";
      }
    }

    function escapeHtml(text){
      return String(text)
        .replaceAll("&", "&amp;")
        .replaceAll("<", "&lt;")
        .replaceAll(">", "&gt;")
        .replaceAll('"', "&quot;")
        .replaceAll("'", "&#039;");
    }
  </script>
</body>
</html>
