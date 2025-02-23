<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sorpresa Speciale</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f9f7f6;
      margin: 0;
      padding: 20px;
    }
    h1 {
      font-size: 2rem;
      color: #ff6f61;
    }
    p {
      font-size: 1.2rem;
      margin: 10px 0;
    }
    video, audio {
      margin: 20px 0;
      width: 80%;
      max-width: 600px;
      border: 2px solid #ff6f61;
      border-radius: 10px;
    }
    #hearts {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
    }
    .heart {
      position: absolute;
      width: 50px;
      height: 50px;
      background-color: #ff6f61;
      clip-path: polygon(50% 0%, 100% 37%, 82% 100%, 50% 82%, 18% 100%, 0% 37%);
      animation: float 4s linear infinite;
    }
    @keyframes float {
      0% {
        transform: translateY(100%);
        opacity: 1;
      }
      100% {
        transform: translateY(-100%);
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <h1>Sorpresa per Te</h1>
  <p>"Un piccolo gesto per ricordarti quanto sei speciale."</p>

  <!-- Video -->
  <video controls>
    <source src="./Videounica.mp4" type="video/mp4">
    Il tuo browser non supporta il video.
  </video>

  <!-- Audio Player -->
  <audio id="audio-player" controls>
    <source src="./song1.mp3" type="audio/mp3">
    Il tuo browser non supporta l'audio.
  </audio>

  <canvas id="hearts"></canvas>

  <script>
    const songs = ["./song1.mp3", "./song2.mp3", "./song3.mp3", "./song4.mp3"];
    const specialSong = "./song2.mp3";
    const audioPlayer = document.getElementById("audio-player");
    const heartsCanvas = document.getElementById("hearts");
    const ctx = heartsCanvas.getContext("2d");
    let width, height;

    // Resize canvas
    function resizeCanvas() {
      width = heartsCanvas.width = window.innerWidth;
      height = heartsCanvas.height = window.innerHeight;
    }
    window.addEventListener("resize", resizeCanvas);
    resizeCanvas();

    // Heart animation
    function createHeart() {
      const x = Math.random() * width;
      const size = Math.random() * 50 + 10;
      const duration = Math.random() * 2 + 3;
      const heart = document.createElement("div");
      heart.className = "heart";
      heart.style.left = `${x}px`;
      heart.style.width = `${size}px`;
      heart.style.height = `${size}px`;
      heart.style.animationDuration = `${duration}s`;
      document.body.appendChild(heart);

      setTimeout(() => heart.remove(), duration * 1000);
    }

    // Detect shake
    let currentSongIndex = 0;
    window.addEventListener("devicemotion", (event) => {
      const { x, y, z } = event.acceleration;
      const shakeThreshold = 15;
      if (Math.abs(x) > shakeThreshold || Math.abs(y) > shakeThreshold || Math.abs(z) > shakeThreshold) {
        currentSongIndex = (currentSongIndex + 1) % songs.length;
        audioPlayer.src = songs[currentSongIndex];
        audioPlayer.play();

        if (songs[currentSongIndex] === specialSong) {
          for (let i = 0; i < 20; i++) {
            setTimeout(createHeart, i * 200);
          }
        }
      }
    });

    // Special message after 3 shakes
    let shakeCount = 0;
    audioPlayer.addEventListener("play", () => {
      shakeCount++;
      if (shakeCount === 3) {
        alert("Ancora non ti sei stancata? Va bene, un'altra canzone allora!");
      }
    });
  </script>
</body>
</html>
