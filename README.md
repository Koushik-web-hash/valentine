# valentine[code.html](https://github.com/user-attachments/files/25062807/code.html)
  [code.html](https://github.com/user-attachments/files/25062810/code.html)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Valentine Week Surprise 💖</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #ffb6c1, #ffc0cb);
      overflow: hidden;
    }

    /* Falling petals */
    .petals {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 0;
    }
    .petal {
      position: absolute;
      width: 22px;
      height: 22px;
      background: radial-gradient(circle at 30% 30%, #ff69b4, #ff1493);
      border-radius: 50% 50% 50% 0;
      transform: rotate(45deg);
      opacity: 0.6;
      animation: fall 25s linear infinite;
    }
    @keyframes fall {
      0% { transform: translateY(-10vh) rotate(0deg); }
      100% { transform: translateY(110vh) rotate(360deg); }
    }

    .card {
      position: relative;
      z-index: 2;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .content {
      background: rgba(255, 255, 255, 0.3);
      backdrop-filter: blur(12px);
      border-radius: 24px;
      padding: 28px 22px;
      max-width: 420px;
      width: 100%;
      text-align: center;
      box-shadow: 0 20px 40px rgba(0,0,0,0.15);
    }

    h1 {
      margin: 0 0 10px;
      font-size: 26px;
      color: #c2185b;
    }

    p {
      font-size: 16px;
      color: #880e4f;
      margin-bottom: 18px;
    }

    /* Bunny */
    .bunny {
      display: none;
      justify-content: center;
      margin-bottom: 10px;
    }

    .bunny-img {
      width: 180px;
      max-width: 70vw;
    }

    @keyframes bunnyJump {
      0% { transform: translateY(0); }
      40% { transform: translateY(-45px); }
      60% { transform: translateY(-45px); }
      100% { transform: translateY(0); }
    }

    /* Buttons */
    .buttons {
      display: flex;
      gap: 16px;
      justify-content: center;
    }

    button {
      border: none;
      padding: 14px 22px;
      font-size: 16px;
      border-radius: 999px;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    #yesBtn {
      background: #e91e63;
      color: white;
      box-shadow: 0 8px 20px rgba(233,30,99,0.4);
    }

    #noBtn {
      background: white;
      color: #e91e63;
      position: relative;
    }

    .hidden { display: none; }

    @keyframes flyUp {
      0% { transform: translateY(0) scale(1); opacity: 1; }
      100% { transform: translateY(-80vh) scale(1.4); opacity: 0; }
    }

    @media (max-width: 480px) {
      h1 { font-size: 22px; }
      p { font-size: 15px; }
    }
  </style>
</head>
<body>

  <div class="petals" id="petals"></div>

  <div class="card">
    <div class="content">

      <!-- Bunny -->
      <div class="bunny" id="bunny">
        <img src="bunny.png" alt="Cute Bunny" class="bunny-img" />
      </div>

      <h1 id="dayTitle"></h1>
      <p id="dayText"></p>
      <p><strong>Will you be my wife? 💍❤️</strong></p>

      <div class="buttons" id="choiceButtons">
        <button id="yesBtn">Yes 💖</button>
        <button id="noBtn">No 🙈</button>
      </div>

      <p id="result" class="hidden"></p>
    </div>
  </div>

  <script>
    /* Create petals */
    const petalsContainer = document.getElementById('petals');
    for (let i = 0; i < 25; i++) {
      const petal = document.createElement('div');
      petal.className = 'petal';
      petal.style.left = Math.random() * 100 + 'vw';
      petal.style.animationDelay = Math.random() * 20 + 's';
      petal.style.animationDuration = 20 + Math.random() * 10 + 's';
      petalsContainer.appendChild(petal);
    }

    /* Valentine week text */
    const days = {
      7: { title: 'Rose Day 🌹', text: 'A rose for the girl who makes my world bloom.' },
      8: { title: 'Propose Day 💍', text: 'I may not be perfect, but my feelings are true.' },
      9: { title: 'Chocolate Day 🍫', text: 'Life is sweeter with you in it.' },
      10:{ title: 'Teddy Day 🧸', text: 'I wish I could hug you like a teddy forever.' },
      11:{ title: 'Promise Day 🤝', text: 'I promise to always care for you.' },
      12:{ title: 'Hug Day 🤗', text: 'Sending you the warmest hug.' },
      13:{ title: 'Kiss Day 😘', text: 'A kiss to seal my feelings.' },
      14:{ title: 'Valentine’s Day ❤️', text: 'You are my favorite love story.' }
    };

    const today = new Date().getDate();
    const data = days[today] || { title: 'My Love 💗', text: '' };

    document.getElementById('dayTitle').innerText = data.title;
    document.getElementById('dayText').innerText = data.text;

    /* Buttons logic */
    const yesBtn = document.getElementById('yesBtn');
    const noBtn = document.getElementById('noBtn');
    const result = document.getElementById('result');

    yesBtn.onclick = () => {
      document.getElementById('choiceButtons').style.display = 'none';

      const bunny = document.getElementById('bunny');
      const bunnyImg = bunny.querySelector('img');
      bunny.style.display = 'flex';
      bunnyImg.style.animation = 'bunnyJump 0.9s ease-in-out infinite';

      result.classList.remove('hidden');
      result.style.color = '#c2185b';
      result.style.fontSize = '18px';
      result.innerHTML =
        'I know you love me more 🥹💖<br>' +
        'Thank you for accepting 💍✨<br>' +
        '<strong>You are the best thing happened to me 🌸</strong>';

      for (let i = 0; i < 20; i++) {
        const heart = document.createElement('div');
        heart.innerText = '💗';
        heart.style.position = 'fixed';
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.bottom = '0px';
        heart.style.fontSize = '24px';
        heart.style.animation = 'flyUp 3s ease-out forwards';
        document.body.appendChild(heart);
        setTimeout(() => heart.remove(), 3000);
      }
    };

    noBtn.onmouseover = () => {
      const x = Math.random() * 200 - 100;
      const y = Math.random() * 200 - 100;
      noBtn.style.transform = `translate(${x}px, ${y}px)`;
    };
  </script>
</body>
</html>
