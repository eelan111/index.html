<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Happy Birthday</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body, html {
      width: 100%;
      height: 100%;
      background: #000;
      overflow: hidden;
      font-family: sans-serif;
    }

    .heart {
      position: fixed;
      top: -50px;
      color: #ff6699;
      font-size: 14px;
      animation: fall linear;
      user-select: none;
    }

    @keyframes fall {
      to { transform: translateY(110vh); }
    }

    .message {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      color: white;
      font-size: 2em;
      text-align: center;
      opacity: 0;
      transition: opacity 0.5s;
    }

    .message.show {
      opacity: 1;
    }

    .big-heart {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 6em;
      color: red;
      display: none;
    }

    .final-heart {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 20em;
      color: red;
      display: none;
    }

    #restartBtn {
      position: absolute;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      padding: 10px 20px;
      font-size: 1em;
      background-color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      z-index: 10;
    }
  </style>
</head>
<body>

  <!-- القلوب المتساقطة -->
  <div id="hearts"></div>

  <!-- الرسائل -->
  <div id="msg1" class="message">Warten Sie!! 🥺</div>
  <div id="msg2" class="message">Noof, du bist wirklich wunderschön 🫢</div>
  <div id="msg3" class="message">Weißt du, warum heute der schönste Tag im Jahr ist?</div>
  <div id="msg4" class="message">Weil du Geburtstag hast!</div>
  <div id="msg5" class="message">Dein Geburtstag ist mein Lieblingsfeiertag ❤</div>
  <div id="msg6" class="message">Letztes Wort für das schönste Mädchen: In einer Welt voller Mädchen bist du die Schönste.</div>

  <!-- القلب الكبير قبل الرسالة الأخيرة -->
  <div id="bigHeart" class="big-heart">❤</div>

  <!-- القلب النهائي بعد الرسالة الأخيرة -->
  <div id="finalHeart" class="final-heart">❤</div>

  <!-- زر إعادة التشغيل -->
  <button id="restartBtn">🔁 إعادة تشغيل</button>

  <script>
    function createHeart() {
      const heart = document.createElement("div");
      heart.className = "heart";
      heart.textContent = "❤";
      heart.style.fontSize = (Math.random() * 10 + 10) + "px";
      heart.style.left = Math.random() * 100 + "vw";
      heart.style.animationDuration = (Math.random() * 5 + 5) + "s";
      document.getElementById("hearts").appendChild(heart);
      setTimeout(() => heart.remove(), 10000);
    }

    setInterval(createHeart, 50);

    const messages = [
      document.getElementById("msg1"),
      document.getElementById("msg2"),
      document.getElementById("msg3"),
      document.getElementById("msg4"),
      document.getElementById("msg5"),
      document.getElementById("msg6")
    ];

    const bigHeart = document.getElementById("bigHeart");
    const finalHeart = document.getElementById("finalHeart");

    function showMessage(element, duration) {
      messages.forEach(msg => msg.classList.remove("show"));
      element.classList.add("show");
      setTimeout(() => {
        element.classList.remove("show");
      }, duration);
    }

    function startSequence() {
      messages.forEach(msg => msg.classList.remove("show"));
      bigHeart.style.display = "none";
      finalHeart.style.display = "none";

      setTimeout(() => showMessage(messages[0], 5000), 500);     // msg1
      setTimeout(() => showMessage(messages[1], 5000), 6000);    // msg2
      setTimeout(() => showMessage(messages[2], 5000), 11500);   // msg3
      setTimeout(() => showMessage(messages[3], 5000), 17000);   // msg4
      setTimeout(() => showMessage(messages[4], 5000), 22500);   // msg5

      // عرض القلب قبل الرسالة الأخيرة
      setTimeout(() => bigHeart.style.display = "block", 28000);
      setTimeout(() => bigHeart.style.display = "none", 30000);

      // عرض الرسالة الأخيرة لمدة أطول
      setTimeout(() => showMessage(messages[5], 8000), 30500);   // msg6

      // بعد الرسالة الأخيرة، عرض القلب النهائي الكبير
      setTimeout(() => {
        finalHeart.style.display = "block";
      }, 39000);
    }

    window.onload = startSequence;
    document.getElementById("restartBtn").onclick = startSequence;
  </script>

</body>
</html>
