# Box-Opener-Simulator-
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boxenchaos - Startseite</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            text-align: center;
            background-color: #000;
            color: white;
        }
        h1 {
            color: #fff;
        }
        .container {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background: #333;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
            border-radius: 8px;
        }
        button {
            font-size: 18px;
            padding: 10px 20px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            background-color: #007BFF;
            color: white;
            cursor: pointer;
        }
        button:hover:not(:disabled) {
            background-color: #0056b3;
        }
        .info {
            font-size: 16px;
            margin: 10px 0;
        }
        #closeButton {
            position: absolute;
            top: 10px;
            right: 20px;
            font-size: 30px;
            color: #fff;
            background: transparent;
            border: none;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Willkommen zu Boxenchaos!</h1>
        <p class="info">Wähle, was du tun möchtest:</p>
        <button id="startGame">Spiel starten</button>
        <button id="goToShop">Zum Shop</button>
    </div>

    <button id="closeButton">X</button>

    <script>
        document.getElementById("startGame").addEventListener("click", () => {
            window.location.href = "game.html"; // Weiterleitung zur Spiel-Seite
        });

        document.getElementById("goToShop").addEventListener("click", () => {
            window.open("shop.html", "_blank"); // Öffnet den Shop in einem neuen Tab
        });

        document.getElementById("closeButton").addEventListener("click", () => {
            window.location.href = "index.html"; // Geht zurück zur Startseite
        });
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shop</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            text-align: center;
            background-color: #000;
            color: white;
        }
        h1 {
            color: #fff;
            margin: 20px 0;
        }
        .container {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background: #333;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
            border-radius: 8px;
        }
        button {
            font-size: 18px;
            padding: 10px 20px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            background-color: #007BFF;
            color: white;
            cursor: pointer;
        }
        button:hover:not(:disabled) {
            background-color: #0056b3;
        }
        #closeButton {
            position: absolute;
            top: 10px;
            right: 20px;
            font-size: 30px;
            color: #fff;
            background: transparent;
            border: none;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Shop</h1>
        <p>Münzen: <span id="coins">0</span></p>
        <button id="buyNormalBox">Normale Box (2 Münzen)</button>
        <button id="buyRareBox">Seltene Box (5 Münzen)</button>
        <button id="buyDuplikator">Duplikator (50 Münzen)</button>
        <button id="backToGame">Zurück zum Spiel</button>
        <p id="result"></p>
    </div>

    <button id="closeButton">X</button>

    <script>
        let coins = parseInt(localStorage.getItem("coins")) || 10;
        let duplikator = localStorage.getItem("duplikator") === "true";
        const coinsElement = document.getElementById("coins");
        const resultElement = document.getElementById("result");

        const updateCoins = (amount) => {
            coins += amount;
            if (coins < 0) coins = 0;
            coinsElement.textContent = coins;
            localStorage.setItem("coins", coins);
        };

        const updateDuplikator = () => {
            localStorage.setItem("duplikator", duplikator);
        };

        const buyItem = (cost, item) => {
            if (coins >= cost) {
                updateCoins(-cost);
                resultElement.textContent = `Du hast ${item} für ${cost} Münzen gekauft!`;
                if (item === "Duplikator") {
                    duplikator = true;
                    updateDuplikator();
                }
            } else {
                resultElement.textContent = "Nicht genug Münzen!";
            }
        };

        document.getElementById("buyNormalBox").addEventListener("click", () => {
            if (coins >= 2) {
                updateCoins(-2);
                resultElement.textContent = "Du hast eine normale Box geöffnet!";
                // Boxeninhalt anzeigen, z.B. Münzen
            }
        });

        document.getElementById("buyRareBox").addEventListener("click", () => {
            if (coins >= 5) {
                updateCoins(-5);
                resultElement.textContent = "Du hast eine seltene Box geöffnet!";
                // Boxeninhalt anzeigen, z.B. Münzen oder Gegenstände
            }
        });

        document.getElementById("buyDuplikator").addEventListener("click", () => {
            buyItem(50, "Duplikator");
        });

        document.getElementById("backToGame").addEventListener("click", () => {
            window.location.href = "game.html";
        });

        document.getElementById("closeButton").addEventListener("click", () => {
            window.location.href = "index.html"; // Geht zurück zur Startseite
        });

        coinsElement.textContent = coins;
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spiel</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            text-align: center;
            background-color: #000;
            color: white;
        }
        h1 {
            color: #fff;
        }
        .container {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background: #333;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
            border-radius: 8px;
        }
        button {
            font-size: 18px;
            padding: 10px 20px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            background-color: #007BFF;
            color: white;
            cursor: pointer;
        }
        button:hover:not(:disabled) {
            background-color: #0056b3;
        }
        .info {
            font-size: 16px;
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Boxenchaos Spiel</h1>
        <p class="info">Münzen: <span id="coins">0</span></p>
        <button id
