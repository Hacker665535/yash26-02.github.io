<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Interface with Timer</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(90deg, #39FF14, #006400);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container, .player-screen, .winner-screen {
            display: none;
            background: rgba(0, 0, 0, 0.8);
            border: 1px solid lightgreen;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            color: white;
            width: 300px;
        }
        .active {
            display: block;
        }
        button {
            background: green;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px 0;
        }
        button:hover {
            background: darkgreen;
        }
        select, input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid lightgreen;
            border-radius: 5px;
            background: black;
            color: white;
        }
        .premium {
            background: linear-gradient(90deg, #FFD700, #FF4500);
            color: black;
            padding: 10px;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <!-- Main Container -->
    <div class="container active" id="mainContainer">
        <h1>𝗡𝘂𝗺𝗯𝗲𝗿 𝗛𝗮𝗰𝗸 𝗣𝗮𝗻𝗲𝗹</h1>
        <button onclick="selectServer()">SELECT SERVER</button>

        <select id="serverSpinner">
            <option value="" disabled selected>SELECT SERVER</option>
            <option>91 CLUB</option>
            <option>TIRANGA</option>
            <option>BIG MUMBAI</option>
            <option>BIG DADDY</option>
            <option>GOA GAME</option>
            <option>OK WIN</option>
            <option>55 CLUB</option>
            <option>BDG WIN</option>
            <option>DIUWIN</option>
            <option>101GAME</option>
            <option>TP PLAY</option>
            <option>DAMAN</option>
            <option>RAJA LUCK</option>
            <option>KWG GAME</option>
            <option>51GAME</option>
        </select>

        <select id="playSpinner">
            <option value="" disabled selected>SELECT PLAY SERVER</option>
            <option value="big_small">BIG/SMALL</option>
            <option value="red_green">RED/GREEN</option>
        </select>

        <input type="password" id="paidKey" placeholder="PAID KEY">
        <button onclick="validateKey()">VALIDATE</button>
    </div>

    <!-- Player Screen -->
    <div class="player-screen" id="playerScreen">
        <h1>𝗡𝗨𝗠𝗕𝗘𝗥 𝗧𝗥𝗔𝗥𝗗𝗘</h1>
        <div class="premium">
            <h2>NUMBER TRADE</h2>
            <p id="textview1Player">Loading...</p>
            <p id="textview2Player">00:00</p>
        </div>
        <button onclick="checkPlayerResult()">CHECK RESULT</button>
        <p id="resultPlayer"></p>
    </div>

    <!-- Winner Screen -->
    <div class="winner-screen" id="winnerScreen">
        <h1>𝗡𝗨𝗠𝗕𝗘𝗥 𝗧𝗥𝗔𝗥𝗗𝗘</h1>
        <div class="premium">
            <h2>𝗡𝗨𝗠𝗕𝗘𝗥 𝗧𝗥𝗔𝗥𝗗𝗘</h2>
            <p id="textview1Winner">Loading...</p>
            <p id="textview2Winner">00:00</p>
        </div>
        <button onclick="checkWinnerResult()">CHECK RESULT</button>
        <p id="resultWinner"></p>
    </div>

    <script>
        let timer = setInterval(updateTimers, 1000);
        let previousPlayerText = "";
        let previousWinnerText = "";

        function updateTimers() {
            const now = new Date();
            const startHour = 5;
            const startMinute = 30;
            const startTime = new Date(now.getFullYear(), now.getMonth(), now.getDate(), startHour, startMinute, 0);
            const elapsedMillis = now - startTime;
            const elapsedSeconds = Math.max(0, Math.floor(elapsedMillis / 1000));
            const totalPeriods = Math.floor(elapsedSeconds / 30);
            const upcomingPeriod = totalPeriods + 1;

            const formattedDate = now.toISOString().split('T')[0].replace(/-/g, '');
            const periodNumber = "100005" + String(upcomingPeriod).padStart(4, '0');
            const textview1Content = formattedDate + periodNumber;

            const remainingSeconds = 30 - (elapsedSeconds % 30);
            const textview2Content = `00:${String(remainingSeconds).padStart(2, '0')}`;

            document.getElementById("textview1Player").textContent = textview1Content;
            document.getElementById("textview2Player").textContent = textview2Content;

            document.getElementById("textview1Winner").textContent = textview1Content;
            document.getElementById("textview2Winner").textContent = textview2Content;
        }

        function validateKey() {
            const key = document.getElementById('paidKey').value;
            if (key === 'BADSHAH_ON_TOP') {
                navigateToScreen();
            } else {
                alert('Wrong password. Please buy key from TG:// @BADSHAH_BHAI_ON_TOP');
            }
        }

        function navigateToScreen() {
            const playType = document.getElementById('playSpinner').value;
            document.getElementById('mainContainer').classList.remove('active');

            if (playType === 'big_small') {
                document.getElementById('playerScreen').classList.add('active');
            } else if (playType === 'red_green') {
                document.getElementById('winnerScreen').classList.add('active');
            } else {
                alert('Please select a play server option.');
                document.getElementById('mainContainer').classList.add('active');
            }
        }

        function checkPlayerResult() {
            const currentText = document.getElementById("textview1Player").textContent;
            if (currentText !== previousPlayerText) {
                const result = Math.random() > 0.5 ? "BIG" : "SMALL";
                document.getElementById("resultPlayer").textContent = `Result: ${result}`;
                previousPlayerText = currentText;
            } else {
                alert("PLS WAIT FOR NEXT PERIOD");
            }
        }

        function checkWinnerResult() {
            const currentText = document.getElementById("textview1Winner").textContent;
            if (currentText !== previousWinnerText) {
                const result = Math.random() > 0.5 ? "RED 🟥" : "GREEN 🟩";
                document.getElementById("resultWinner").textContent = `Result: ${result}`;
                previousWinnerText = currentText;
            } else {
                alert("PLS WAIT FOR NEXT PERIOD");
            }
        }
    </script>
</body>
</html>
