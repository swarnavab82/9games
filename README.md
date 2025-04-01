# 9games
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>9games - Play & Compete</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>🎮 Welcome to 9games!</h1>
        <p>Play arcade games & compete on the leaderboard.</p>
    </header>

    <section id="games">
        <h2>Featured Games</h2>
        <div class="game-list">
            <div class="game">
                <h3>Flappy Bird</h3>
                <button onclick="playGame('games/flappy.html')">Play</button>
            </div>
            <div class="game">
                <h3>Brick Breaker</h3>
                <button onclick="playGame('games/brick.html')">Play</button>
            </div>
        </div>
    </section>

    <section id="leaderboard">
        <h2>🏆 Leaderboard</h2>
        <ul id="scores"></ul>
    </section>

    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #1a1a1a;
    color: white;
    margin: 0;
}

header {
    background: #ff9800;
    padding: 20px;
    font-size: 24px;
}

#games, #leaderboard {
    margin: 20px auto;
    width: 80%;
}

.game {
    display: inline-block;
    background: #444;
    padding: 15px;
    margin: 10px;
    border-radius: 8px;
}
// Sample leaderboard data
let leaderboard = [
    { name: "Player1", score: 500 },
    { name: "Player2", score: 350 },
    { name: "Player3", score: 250 }
];

// Display leaderboard
function displayLeaderboard() {
    const scoresList = document.getElementById("scores");
    scoresList.innerHTML = "";
    leaderboard.forEach(player => {
        let li = document.createElement("li");
        li.textContent = `${player.name}: ${player.score} pts`;
        scoresList.appendChild(li);
    });
}

// Redirect to game page
function playGame(gameUrl) {
    window.location.href = gameUrl;
}

// Load leaderboard on page load
window.onload = displayLeaderboard;
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flappy Bird Clone</title>
    <style>
        body { text-align: center; }
        canvas { background-color: skyblue; }
    </style>
</head>
<body>
    <h1>Flappy Bird</h1>
    <canvas id="gameCanvas" width="400" height="500"></canvas>
    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        let bird = { x: 50, y: 200, gravity: 2, lift: -20, velocity: 0 };
        let obstacles = [{ x: 400, gapY: 150, width: 50, height: 200 }];
        let score = 0;

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw bird
            ctx.fillStyle = "yellow";
            ctx.fillRect(bird.x, bird.y, 20, 20);

            // Draw obstacles
            ctx.fillStyle = "green";
            obstacles.forEach(obstacle => {
                ctx.fillRect(obstacle.x, 0, obstacle.width, obstacle.gapY);
                ctx.fillRect(obstacle.x, obstacle.gapY + 100, obstacle.width, canvas.height - obstacle.gapY - 100);
            });

            requestAnimationFrame(draw);
        }

        function update() {
            bird.velocity += bird.gravity;
            bird.y += bird.velocity;

            obstacles.forEach(obstacle => {
                obstacle.x -= 2;
                if (obstacle.x + obstacle.width < 0) {
                    obstacle.x = 400;
                    obstacle.gapY = Math.random() * 200 + 100;
                    score++;
                }
            });

            if (bird.y > canvas.height || bird.y < 0) {
                alert("Game Over! Score: " + score);
                location.reload();
            }
        }

        document.addEventListener("keydown", () => {
            bird.velocity = bird.lift;
        });

        function gameLoop() {
            update();
            draw();
        }

        setInterval(gameLoop, 30);
    </script>
</body>
</html>

button {
    background: #ff9800;
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
    font-size: 16px;
}
