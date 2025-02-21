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
            background-color: #f4d03f; /* Giallo ocra */
            color: #333;
            overflow: hidden; /* Nasconde elementi fuori dallo schermo */
        }
        h1 {
            text-align: center;
            padding: 20px;
            color: #d35400;
        }
        video {
            display: block;
            margin: 20px auto;
        }
        button {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            font-size: 18px;
            background-color: #e74c3c;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
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
    <p style="text-align: center;">Tocca il pulsante per iniziare!</p>
    <button onclick="startMusic()">Avvia Musica</button>
    <video id="video" width="320" height="240" controls>
        <source src="https://tuo-username.github.io/nome-repository/video.mp4" type="video/mp4">
        Il tuo browser non supporta i video.
    </video>

    <script>
        let songs = [
            "https://tuo-username.github.io/nome-repository/song1.mp3",
            "https://tuo-username.github.io/nome-repository/song2.mp3",
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
            const heartContainer = document.createElement("div");
            document.body.appendChild(heartContainer);

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