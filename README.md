<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sorpresa</title>
</head>
<body>
    <h1>Ciao Amore ❤️</h1>
    <p>Tocca il pulsante per avviare la musica:</p>
    <button onclick="startMusic()">Avvia Musica</button>
    
    <video width="320" height="240" controls>
        <source src="https://github.com/tagjunior91/Prova-1/blob/main/SnapTik_App_7468275277735529750.mp4" type="video/mp4">
        Il tuo browser non supporta i video.
    </video>

    <script>
        let audio = new Audio("https://tuo-username.github.io/nome-repository/song1.mp3");

        function startMusic() {
            audio.loop = true;
            audio.play()
                .then(() => {
                    console.log("Musica avviata!");
                })
                .catch((error) => {
                    console.error("Errore durante l'avvio della musica:", error);
                });
        }
    </script>
</body>
</html>