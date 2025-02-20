<body>
    <h1>Ciao Amore ❤️</h1>
    <p>Sei la persona più speciale della mia vita. Scorri in basso per vedere la sorpresa!</p>

    <!-- Pulsante per avviare la musica -->
    <button onclick="startMusic()">Avvia Musica</button>

    <video width="320" height="240" controls>
        <source src="https://github.com/tagjunior91/Prova-1/blob/main/SnapTik_App_7468275277735529750.mp4" type="video/mp4">
        Il tuo browser non supporta i video.
    </video>
    <p style="margin-top: 20px;">Scuoti il telefono per cambiare la canzone!</p>

    <script>
        // Lista delle canzoni
        let songs = [
             "https://tagjunior91.github.io/nome-repository/Song2.mp3"];
        ];
        let currentSongIndex = 0;
        let audio = new Audio(songs[currentSongIndex]);

        // Funzione per avviare la musica manualmente
        function startMusic() {
            audio.loop = true;
            audio.play()
                .then(() => {
                    console.log("Musica avviata correttamente");
                    alert("Musica avviata! Scuoti il telefono per cambiare la canzone.");
                })
                .catch((error) => {
                    console.error("Errore durante l'avvio della musica:", error);
                    alert("Impossibile avviare la musica. Prova di nuovo.");
                });
        }

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
            if (currentTime - lastShakeTime < 1000) return;

            const acceleration = event.accelerationIncludingGravity;
            const shakeThreshold = 15;

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