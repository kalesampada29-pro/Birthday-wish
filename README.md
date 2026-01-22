# Birthday-wish<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday ❤️</title>

<style>
body {
  margin: 0;
  font-family: 'Comic Sans MS', cursive;
  background: linear-gradient(135deg,#ffd6e8,#e0f7fa);
  text-align: center;
  overflow-x: hidden;
}

h1 {
  color: #ff5fa2;
  animation: pop 2s infinite;
}

@keyframes pop {
  0%,100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

#cake {
  font-size: 100px;
  margin-top: 20px;
}

.candle {
  display: inline-block;
  width: 10px;
  height: 30px;
  background: orange;
  margin: 5px;
  border-radius: 5px;
}

#message {
  display: none;
  font-size: 22px;
  color: #ff4081;
  margin: 20px;
  animation: fadeIn 2s forwards;
}

@keyframes fadeIn {
  from {opacity:0;}
  to {opacity:1;}
}

.cats {
  display: flex;
  justify-content: center;
  gap: 40px;
  margin-top: 30px;
}

.cat {
  font-size: 80px;
  cursor: pointer;
  animation: dance 1s infinite alternate;
}

@keyframes dance {
  from { transform: rotate(-5deg); }
  to { transform: rotate(5deg); }
}

#banner {
  font-size: 28px;
  color: #ff1493;
  margin-top: 20px;
}

.heart {
  position: fixed;
  color: red;
  font-size: 20px;
  animation: float 2s forwards;
}

@keyframes float {
  from { opacity:1; transform: translateY(0); }
  to { opacity:0; transform: translateY(-100px); }
}

footer {
  margin: 40px 0;
  font-size: 18px;
  color: #ff4081;
}
</style>
</head>

<body>

<h1>🎂 Happy Birthday My Love 💖</h1>

<div id="cake">🎂</div>
<div id="candles">
  <div class="candle"></div>
  <div class="candle"></div>
  <div class="candle"></div>
  <div class="candle"></div>
</div>

<p>Blow into the mic to blow the candles 🕯️🎤</p>

<div id="message">
  💕 Happy Birthday to the most special girl in my life 💕  
  <br>You make my world brighter every day 🌸✨
</div>

<div id="banner">🎀 Happy Birthday 🎀</div>

<div class="cats">
  <div class="cat" onclick="love()">🐱 Dudu</div>
  <div class="cat" onclick="love()">🐱 Bubu</div>
</div>

<footer>
  Made with love 💖🎂
</footer>

<script>
let blown = false;

navigator.mediaDevices.getUserMedia({ audio: true }).then(stream => {
  const audioContext = new AudioContext();
  const mic = audioContext.createMediaStreamSource(stream);
  const analyser = audioContext.createAnalyser();
  mic.connect(analyser);
  const data = new Uint8Array(analyser.frequencyBinCount);

  function detectBlow() {
    analyser.getByteFrequencyData(data);
    let volume = data.reduce((a,b)=>a+b)/data.length;
    if (volume > 50 && !blown) {
      blown = true;
      blowCandles();
    }
    requestAnimationFrame(detectBlow);
  }
  detectBlow();
});

function blowCandles() {
  document.getElementById("candles").innerHTML = "✨ Candles Blown! ✨";
  document.getElementById("message").style.display = "block";
  confetti();
}

function love() {
  let heart = document.createElement("div");
  heart.className = "heart";
  heart.innerHTML = "❤️";
  heart.style.left = Math.random()*100+"vw";
  heart.style.top = "80vh";
  document.body.appendChild(heart);
  setTimeout(()=>heart.remove(),2000);
  new Audio("https://www.soundjay.com/cat/cat-meow-2.mp3").play();
}

function confetti() {
  for(let i=0;i<50;i++){
    let c = document.createElement("div");
    c.className="heart";
    c.innerHTML="🎈";
    c.style.left=Math.random()*100+"vw";
    c.style.top=Math.random()*100+"vh";
    document.body.appendChild(c);
    setTimeout(()=>c.remove(),3000);
  }
}
</script>

</body>
</html>
