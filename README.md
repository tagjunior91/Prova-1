<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crea il Tuo Giardino Incantato</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #dff0e3;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            color: #4b8f4b;
        }
        #garden {
            width: 90%;
            height: 400px;
            border: 2px dashed #4b8f4b;
            background-color: #ffffff;
            display: flex;
            flex-wrap: wrap;
            position: relative;
        }
        .item {
            width: 50px;
            height: 50px;
            cursor: grab;
        }
        .flower {
            background-color: #f78fb3;
            border-radius: 50%;
        }
        .tree {
            background-color: #4b8f4b;
            border-radius: 10%;
        }
        .fountain {
            background-color: #87ceeb;
            border-radius: 50%;
        }
        #score {
            margin-top: 20px;
            color: #4b8f4b;
        }
    </style>
</head>
<body>
    <h1>Crea il Tuo Giardino Incantato</h1>
    <div id="garden"></div>
    <div>
        <div class="item flower" draggable="true"></div>
        <div class="item tree" draggable="true"></div>
        <div class="item fountain" draggable="true"></div>
    </div>
    <p id="score">Punteggio Magia: 0</p>
    <script>
        const garden = document.getElementById("garden");
        const items = document.querySelectorAll(".item");
        let score = 0;

        // Trascinamento degli oggetti
        items.forEach(item => {
            item.addEventListener("dragstart", (e) => {
                e.dataTransfer.setData("class", e.target.className);
            });
        });

        // Rilascia l'oggetto nel giardino
        garden.addEventListener("dragover", (e) => {
            e.preventDefault();
        });

        garden.addEventListener("drop", (e) => {
            e.preventDefault();
            const className = e.dataTransfer.getData("class");
            const newItem = document.createElement("div");
            newItem.className = className + " item";
            newItem.style.position = "absolute";
            newItem.style.left = e.clientX - garden.offsetLeft - 25 + "px";
            newItem.style.top = e.clientY - garden.offsetTop - 25 + "px";
            garden.appendChild(newItem);

            // Incrementa il punteggio
            score += 10;
            document.getElementById("score").textContent = `Punteggio Magia: ${score}`;
        });
    </script>
</body>
</html>