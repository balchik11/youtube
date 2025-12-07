<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Киця мур</title>
<style>
  body {
    margin: 0;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: linear-gradient(135deg, #ff9a9e, #fad0c4, #fbc2eb);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    overflow: hidden;
    background-size: 400% 400%;
    animation: gradientShift 15s ease infinite;
  }

  @keyframes gradientShift {
    0% {background-position: 0% 50%;}
    50% {background-position: 100% 50%;}
    100% {background-position: 0% 50%;}
  }

  h1 {
    color: #e91e63;
    font-size: 36px;
    margin-bottom: 15px;
    text-align: center;
    text-shadow: 2px 2px 5px rgba(0,0,0,0.3);
    z-index: 2;
  }

  .video-container {
    width: 90%;
    max-width: 800px;
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 15px 30px rgba(0,0,0,0.3);
    transition: transform 0.3s ease;
    z-index: 1;
    margin-bottom: 15px;
  }

  .video-container:hover {
    transform: scale(1.03);
  }

  iframe {
    width: 100%;
    height: 300px;
    border: none;
  }

  input, button {
    padding: 10px 15px;
    font-size: 16px;
    border-radius: 10px;
    border: none;
    margin: 5px;
  }

  button {
    background: #e91e63;
    color: white;
    cursor: pointer;
    transition: 0.3s;
  }

  button:hover {
    background: #c2185b;
  }

  /* Сердечки */
  .heart {
    position: absolute;
    font-size: 20px;
    color: #ff1744;
    animation: fall linear infinite;
    pointer-events: none;
  }

  @keyframes fall {
    0% {transform: translateY(-50px) scale(1);}
    50% {transform: translateY(50vh) scale(1.2);}
    100% {transform: translateY(100vh) scale(1);}
  }

  @media (max-width: 480px) {
    h1 { font-size: 28px; }
    iframe { height: 220px; }
  }

  @media (max-width: 320px) {
    h1 { font-size: 24px; }
    iframe { height: 180px; }
  }
</style>
</head>
<body>
  <h1>Люблю тебе ❤️</h1>

  <div class="video-container">
    <iframe id="videoFrame" src="https://www.youtube.com/embed/i2XWsmvCed0" 
      title="YouTube video" allowfullscreen></iframe>
  </div>

  <div>
    <input type="text" id="videoLink" placeholder="Встав посилання на YouTube">
    <button onclick="loadVideo()">Дивитися</button>
  </div>

<script>
  // Функція для заміни відео
  function loadVideo() {
    const link = document.getElementById('videoLink').value;
    if (!link) return;

    // Перетворюємо повне посилання на embed
    let videoId = '';
    if(link.includes('watch?v=')) {
      videoId = link.split('watch?v=')[1];
      const ampersand = videoId.indexOf('&');
      if(ampersand !== -1) videoId = videoId.substring(0, ampersand);
    } else if(link.includes('youtu.be/')) {
      videoId = link.split('youtu.be/')[1];
    } else {
      alert('Невірне посилання на YouTube');
      return;
    }

    const embedLink = 'https://www.youtube.com/embed/' + videoId;
    document.getElementById('videoFrame').src = embedLink;
  }

  // Сердечки
  function createHeart() {
    const heart = document.createElement('div');
    heart.className = 'heart';
    heart.style.left = Math.random() * window.innerWidth + 'px';
    heart.style.animationDuration = (4 + Math.random() * 3) + 's';
    heart.innerHTML = '❤️';
    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 7000);
  }
  setInterval(createHeart, 500);
</script>
</body>
</html>
