<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sorpresa per la mia moglie</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div id="content">
    <h1 id="message">Sei la persona più importante della mia vita!</h1>
    <video id="video" controls>
      <source src="video.mp4" type="video/mp4">
      Il tuo browser non supporta i video.
    </video>
  </div>
  <script src="script.js"></script>
</body>
</html>

/* style.css */
body {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #ffeff5;
  overflow: hidden;
}

#message {
  font-size: 2rem;
  color: #ff69b4;
  margin-top: 20px;
}

video {
  margin-top: 20px;
  width: 80%;
  border: 3px solid #ff69b4;
  border-radius: 12px;
}

.heart {
  position: absolute;
  color: red;
  font-size: 2rem;
  animation: fall 3s linear infinite;
}

@keyframes fall {
  from {
    transform: translateY(-100%);
  }
  to {
    transform: translateY(100vh);
  }
}

/* script.js */
const phrases = [
  "Sei la persona più importante della mia vita!",
  "Ogni giorno con te è speciale!",
  "Non dimenticare mai quanto sei amata!",
];

let shakeCount = 0;
let currentPhrase = 0;

window.addEventListener("devicemotion", (event) => {
  const acceleration = event.accelerationIncludingGravity;
  if (acceleration.x > 15 || acceleration.y > 15 || acceleration.z > 15) {
    shakeCount++;
    if (shakeCount < 3) {
      currentPhrase = (currentPhrase + 1) % phrases.length;
      document.getElementById("message").innerText = phrases[currentPhrase];
    } else if (shakeCount === 3) {
      alert("Ancora non ti sei stancata? Prova un'altra canzone!");
    }
    // Aggiungi cuoricini
    createHearts();
  }
});

function createHearts() {
  const heart = document.createElement("div");
  heart.className = "heart";
  heart.innerText = "❤️";
  heart.style.left = Math.random() * 100 + "vw";
  document.body.appendChild(heart);

  setTimeout(() => heart.remove(), 3000);
}
