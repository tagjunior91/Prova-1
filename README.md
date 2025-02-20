<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sorpresa</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
            margin: 50px;
            background-color: #fdf6e3;
        }
        h1 {
            color: #d33682;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #268bd2;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
        }
        button:hover {
            background-color: #2aa198;
        }
    </style>
</head>
<body>
    <h1>Ciao Amore ❤️</h1>
    <p>Sei la persona più speciale della mia vita. Scorri in basso per vedere la sorpresa!</p>

    <video width="320" height="240" controls>
        <source src="/https://github.com/tagjunior91/Prova-1/blob/main/SnapTik_App_7468275277735529750.mp4" type="video/mp4">
        Il tuo browser non supporta i video.
    </video>
    <p style="margin-top: 20px;">Scuoti il telefono per cambiare la canzone!</p>

    <script>
        // Lista delle canzoni
        let songs = [
            "https://tagjunior91.github.io/nome-repository/Prova-1/blob/main/song1.mp3",
            "URL_DELLA_CANZONE_2",
            "URL_DELLA_CANZONE_3"
        ];
        let currentSongIndex = 0;
        let audio = new Audio(songs[currentSongIndex]);

        // Avvia la musica automaticamente
        window.onload = () => {
            audio.loop = true; // Imposta la musica in loop
            audio.play().catch(() => {
                alert("Tocca lo schermo per avviare la musica se non parte automaticamente!");
            });
        };

        // Cambia canzone
        function changeSong() {
            audio.pause();
            currentSongIndex = (currentSongIndex + 1) % songs.length;
            audio = new Audio(songs[currentSongIndex]);
            audio.play();
        }

        // Rileva il movimento del telefono
        let lastShakeTime = 0;
        window.addEventListener("devicemotion", (event) => {
            const currentTime = Date.now();
            if (currentTime - lastShakeTime < 1000) return; // Evita cambiamenti rapidi

            const acceleration = event.accelerationIncludingGravity;
            const shakeThreshold = 15; // Soglia per rilevare lo shake

            if (
                Math.abs(acceleration.x) > shakeThreshold ||
                Math.abs(acceleration.y) > shakeThreshold ||
                Math.abs(acceleration.z) > shakeThreshold
            ) {
                lastShakeTime = currentTime;
                changeSong();
            }
        });
    </script>
</body>
</html>
