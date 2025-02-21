<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sorpresa per Te ❤️</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #fef9c3; /* Giallo paglierino */
            color: #333;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden; /* Nasconde elementi fuori dallo schermo */
        }
        h1 {
            text-align: center;
            padding: 10px;
            color: #d35400;
        }
        p {
            text-align: center;
            font-size: 20px;
            margin-bottom: 20px;
            color: #6c5b7b;
        }
        video {
            width: 320px;
            height: 240px;
            margin: 20px auto;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        button {
            padding: 10px 20px;
            font-size: 18px;
            background-color: #e74c3c;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
        }
        button:hover {
            background-color: #c0392b;
        }
        .heart {
            position: absolute;
            width: 30px;
            height: 30px;
            background-color: #e74c3c;
            clip-path: polygon(50% 0%, 100% 35%, 75% 100%, 50% 75%, 25% 100%, 0% 35%);
            animation: fall 3s linear infinite;
        }
        @keyframes fall {
            0% {
                top: -50px;
                opacity: 1;
            }
            100% {
                top: 100vh;
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <h1>Ciao Amore ❤️</h1>
    <p>Sei il mio tutto e riempi ogni giorno di gioia e amore. 💛</p>
    <video id="video" controls>
        <source src="https://github.com/tagjunior91/Prova-3/blob/main/SnapTik_App_7468275277735529750.mp4" type="video/mp4">
        Il tuo browser non supporta i video.
    </video>
    <button onclick="startMusic()">Avvia Musica</button>

    <script>
        let songs = [
            "https://github.com/tagjunior91/Prova-3/blob/main/Song2.mp3",
            "https://tuo-username.github.io/nome-repository/song2.mp3", /* Quella con i cuoricini */
            "https://tuo-username.github.io/nome-repository/song3.mp3"
        ];

        let currentSongIndex = 0;
        let audio = new Audio(songs[currentSongIndex]);
        let shakeCount = 0;

        function startMusic() {
            audio.play()
                .then(() => {
                    console.log("Musica avviata!");
                    if (currentSongIndex === 1) {
                        // Mostra i cuoricini per una canzone specifica
                        startHearts();
                    }
                })
                .catch((error) => {
                    console.error("Errore durante l'avvio della musica:", error);
                });
        }

        // Funzione per far cadere i cuoricini
        function startHearts() {
            setInterval(() => {
                const heart = document.createElement("div");
                heart.classList.add("heart");
                heart.style.left = Math.random() * 100 + "vw";
                heart.style.animationDuration = Math.random() * 2 + 3 + "s";
                document.body.appendChild(heart);

                setTimeout(() => {
                    heart.remove();
                }, 5000);
            }, 300);
        }

        // Funzione per cambiare canzone
        function changeSong() {
            currentSongIndex = (currentSongIndex + 1) % songs.length;
            audio.src = songs[currentSongIndex];
            audio.play();
            if (currentSongIndex === 1) {
                startHearts();
            }
        }

        // Shake detection
        let lastShakeTime = 0;

        window.addEventListener("devicemotion", (event) => {
            const acceleration = event.accelerationIncludingGravity;
            const currentTime = new Date().getTime();

            if (
                Math.abs(acceleration.x) > 15 ||
                Math.abs(acceleration.y) > 15 ||
                Math.abs(acceleration.z) > 15
            ) {
                if (currentTime - lastShakeTime > 1000) {
                    lastShakeTime = currentTime;
                    shakeCount++;
                    if (shakeCount === 3) {
                        alert("Ma non ti sei stufata? D'accordo, un'altra ancora 😊");
                    } else if (shakeCount > 3) {
                        changeSong();
                    }
                }
            }
        });
    </script>
</body>
</html>