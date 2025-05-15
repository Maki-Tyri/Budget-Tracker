<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Let’s do the ‘happily ever after’ thing</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: url('https://static.wikia.nocookie.net/p__/images/2/23/Sadness_Full_Body_2.webp/revision/latest?cb=20240412213000&path-prefix=protagonist') no-repeat center center fixed;
      background-size: cover;
      height: 100vh;
      overflow: hidden;
    }

    .overlay {
      background-color: rgba(255, 255, 255, 0.0);
      padding: 20px;
      border-radius: 15px;
      text-align: center;
      width: 90%;
      max-width: 400px;
      margin: auto;
      margin-top: 20%;
      opacity: 0;
      animation: fadeIn 2s ease-in-out forwards;
    }

    .login-box {
      background-color: white;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 0 15px rgba(0,0,0,0.2);
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h2 {
      font-size: 24px;
      color: #1877f2;
      margin-bottom: 10px;
    }

    #proposal {
      font-size: 30px;
      margin-bottom: 20px;
      color: #fff;
      text-shadow: 1px 1px 4px #000;
    }

    button {
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      margin: 10px;
      font-size: 16px;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
    }

    #yesBtn {
      background-color: #ff69b4;
      color: white;
    }

    #noBtn {
      background-color: #aaa;
      color: white;
      transform: scale(1);
    }

    .heart {
      position: absolute;
      width: 20px;
      height: 20px;
      background: red;
      transform: rotate(45deg);
      animation: explode 1s ease-out forwards;
    }

    .heart::before,
    .heart::after {
      content: "";
      position: absolute;
      width: 20px;
      height: 20px;
      background: red;
      border-radius: 50%;
    }

    .heart::before {
      top: -10px;
      left: 0;
    }

    .heart::after {
      left: -10px;
      top: 0;
    }

    @keyframes explode {
      0% { opacity: 1; transform: scale(1) rotate(45deg); }
      100% { opacity: 0; transform: scale(4) rotate(45deg); top: -200px; }
    }

    #loginPage, #proposalPage {
      display: none;
    }

    #loginPage.show, #proposalPage.show {
      display: block;
    }

    iframe {
      display: none;
    }

    @media (max-width: 600px) {
      .overlay {
        margin-top: 30%;
      }

      #proposal {
        font-size: 24px;
      }

      button {
        font-size: 14px;
      }
    }
  </style>
</head>
<body>

<!-- 🎵 YouTube Music -->
<iframe
  id="ytplayer"
  src=""
  allow="autoplay"
  allowfullscreen
  frameborder="0"
  width="0"
  height="0"
></iframe>

<!-- 🔐 Login Page -->
<div class="overlay" id="loginPage">
  <div class="login-box">
    <h2>Maki Web</h2>
    <p>Log in to continue...</p>
    <input type="text" id="username" placeholder="Username"><br><br>
    <input type="password" id="password" placeholder="Password"><br><br>
    <button onclick="login()">Login</button>
  </div>
</div>

<!-- 💍 Proposal Page -->
<div class="overlay" id="proposalPage">
  <div id="proposal">
    I've loved you since I can't remember when,<br>
    and I'm gonna love you till I can't forget how.<br><br>
    <strong>Will you marry me?</strong>
  </div>
  <button id="yesBtn" onclick="sayYes()">Yes 💍</button>
  <button id="noBtn" onclick="shrinkNo()">No 🙈</button>
</div>

<script>
  const users = {
    "Tyri": "0452",
    "Sample": "0000",
    "Maki": "112621"
  };

  window.onload = () => {
    document.getElementById("loginPage").classList.add("show");
  };

  function login() {
    const u = document.getElementById("username").value.trim();
    const p = document.getElementById("password").value.trim();

    if (users[u] === p) {
      document.getElementById("loginPage").style.display = "none";
      document.getElementById("proposalPage").classList.add("show");

      // Start YouTube music autoplay
      const ytplayer = document.getElementById('ytplayer');
      ytplayer.src = "https://www.youtube.com/embed/wLcGOpZgmj4?autoplay=1&loop=1&playlist=wLcGOpZgmj4";
    } else {
      alert("Incorrect username or password.");
    }
  }

  let noScale = 1;
  let noClicked = false;

  function shrinkNo() {
    const noBtn = document.getElementById("noBtn");

    if (!noClicked) {
      document.body.style.backgroundImage = "url('https://static.wikia.nocookie.net/insideout/images/0/0f/Inside-out-d150_20mcs.sel16.171.jpg/revision/latest/scale-to-width-down/1000?cb=20160306084146')";
      noClicked = true;
    }

    if (noScale > 0.1) {
      noScale -= 0.05; // Shrink gradually after each click
      noBtn.style.transform = `scale(${noScale})`;
    }

    if (noScale <= 0.1) {
      noBtn.style.display = "none";
      enlargeYes();  // Enlarge the "Yes" button after "No" disappears
    }
  }

  function enlargeYes() {
    const yesBtn = document.getElementById("yesBtn");
    let yesScale = 1;

    // Gradually enlarge the "Yes" button
    const enlargeInterval = setInterval(() => {
      yesScale += 0.05;
      yesBtn.style.transform = `scale(${yesScale})`;

      if (yesScale >= 2) {
        clearInterval(enlargeInterval); // Stop enlarging once it's big enough
      }
    }, 100);
  }

  function sayYes() {
    document.body.style.backgroundImage = "url('https://static.wikia.nocookie.net/insideout/images/9/9d/A_DEAD_MOUSE%21.png/revision/latest/scale-to-width-down/1000?cb=20160222221405')";

    for (let i = 0; i < 50; i++) {
      const heart = document.createElement('div');
      heart.classList.add('heart');
      heart.style.left = Math.random() * window.innerWidth + 'px';
      heart.style.top = Math.random() * window.innerHeight + 'px';
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 1000);
    }

    for (let i = 0; i < 100; i++) {
      const sparkle = document.createElement('div');
      sparkle.classList.add('heart');
      sparkle.style.background = 'hotpink';
      sparkle.style.left = Math.random() * 100 + 'vw';
      sparkle.style.top = Math.random() * 100 + 'vh';
      document.body.appendChild(sparkle);
      setTimeout(() => sparkle.remove(), 1200);
    }

    setTimeout(() => {
      alert("💖 She said YES! 💍💖");
    }, 1200);
  }
</script>

</body>
</html>
