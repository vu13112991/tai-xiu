<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Tài Xỉu</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Game Tài Xỉu</h1>
        <p>Số dư: <span id="balance">1000</span> VND</p>
        
        <label for="betAmount">Số tiền cược:</label>
        <input type="number" id="betAmount" min="1" value="100">
        
        <button onclick="playGame('tai')">Cược Tài</button>
        <button onclick="playGame('xiu')">Cược Xỉu</button>
        
        <div id="result"></div>
        <div id="dice">
            🎲 🎲 🎲
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #282c34;
    color: white;
}

.container {
    margin-top: 50px;
}

button {
    padding: 10px 20px;
    margin: 10px;
    font-size: 16px;
    cursor: pointer;
}

#dice {
    font-size: 30px;
    margin-top: 20px;
}

let balance = 1000;

function playGame(choice) {
    let bet = parseInt(document.getElementById("betAmount").value);
    
    if (bet > balance || bet <= 0) {
        alert("Số tiền cược không hợp lệ!");
        return;
    }

    // Xúc xắc ngẫu nhiên
    let dice1 = Math.floor(Math.random() * 6) + 1;
    let dice2 = Math.floor(Math.random() * 6) + 1;
    let dice3 = Math.floor(Math.random() * 6) + 1;
    let total = dice1 + dice2 + dice3;

    let resultText = `🎲 Xúc xắc: ${dice1} - ${dice2} - ${dice3} (Tổng: ${total})`;

    let isTai = total >= 11; // Tài: 11-18, Xỉu: 3-10
    let won = (choice === 'tai' && isTai) || (choice === 'xiu' && !isTai);

    if (won) {
        balance += bet;
        resultText += "<br><b>🎉 Bạn thắng! + " + bet + " VND</b>";
    } else {
        balance -= bet;
        resultText += "<br><b>😢 Bạn thua! - " + bet + " VND</b>";
    }

    document.getElementById("result").innerHTML = resultText;
    document.getElementById("balance").innerText = balance;
}
