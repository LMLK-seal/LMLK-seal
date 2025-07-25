<details>
<summary>🎮 Interactive Code Challenge - Click to Play!</summary>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matrix Code Challenge</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Fira Code', monospace;
            background: #000;
            color: #00ff41;
            overflow: hidden;
            height: 100vh;
            position: relative;
        }
        
        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            opacity: 0.3;
        }
        
        .game-container {
            position: relative;
            z-index: 10;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            padding: 20px;
            background: rgba(0, 0, 0, 0.8);
        }
        
        .title {
            font-size: 3rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 20px;
            text-shadow: 0 0 20px #00ff41;
            animation: glow 2s ease-in-out infinite alternate;
        }
        
        @keyframes glow {
            from { text-shadow: 0 0 20px #00ff41, 0 0 30px #00ff41; }
            to { text-shadow: 0 0 30px #00ff41, 0 0 40px #00ff41, 0 0 50px #00ff41; }
        }
        
        .subtitle {
            font-size: 1.2rem;
            text-align: center;
            margin-bottom: 30px;
            opacity: 0.8;
        }
        
        .game-area {
            background: rgba(0, 20, 0, 0.9);
            border: 2px solid #00ff41;
            border-radius: 10px;
            padding: 30px;
            max-width: 800px;
            width: 100%;
            box-shadow: 0 0 50px rgba(0, 255, 65, 0.3);
        }
        
        .challenge-text {
            font-size: 1.1rem;
            line-height: 1.6;
            margin-bottom: 20px;
            padding: 20px;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 5px;
            border-left: 4px solid #00ff41;
            animation: typewriter 3s steps(50, end);
            overflow: hidden;
            white-space: nowrap;
        }
        
        @keyframes typewriter {
            from { width: 0; }
            to { width: 100%; }
        }
        
        .input-area {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .code-input {
            flex: 1;
            padding: 15px;
            font-family: 'Fira Code', monospace;
            font-size: 1rem;
            background: rgba(0, 0, 0, 0.7);
            border: 2px solid #00ff41;
            border-radius: 5px;
            color: #00ff41;
            outline: none;
            transition: all 0.3s ease;
        }
        
        .code-input:focus {
            box-shadow: 0 0 20px rgba(0, 255, 65, 0.5);
            transform: scale(1.02);
        }
        
        .submit-btn {
            padding: 15px 30px;
            font-family: 'Fira Code', monospace;
            font-size: 1rem;
            background: transparent;
            border: 2px solid #00ff41;
            border-radius: 5px;
            color: #00ff41;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .submit-btn:hover {
            background: #00ff41;
            color: #000;
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(0, 255, 65, 0.4);
        }
        
        .stats {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            font-size: 0.9rem;
        }
        
        .stat-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .progress-bar {
            width: 100%;
            height: 8px;
            background: rgba(0, 255, 65, 0.2);
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 20px;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #00ff41, #00cc33);
            width: 0%;
            transition: width 0.5s ease;
            border-radius: 4px;
        }
        
        .message {
            text-align: center;
            font-size: 1.1rem;
            margin-top: 15px;
            padding: 10px;
            border-radius: 5px;
            transition: all 0.3s ease;
        }
        
        .success {
            background: rgba(0, 255, 65, 0.2);
            border: 1px solid #00ff41;
        }
        
        .error {
            background: rgba(255, 0, 0, 0.2);
            border: 1px solid #ff0000;
            color: #ff6666;
        }
        
        .hint {
            font-size: 0.9rem;
            opacity: 0.7;
            text-align: center;
            margin-top: 10px;
        }
        
        .particle {
            position: absolute;
            color: #00ff41;
            font-family: 'Fira Code', monospace;
            pointer-events: none;
            z-index: 1;
        }
        
        @media (max-width: 768px) {
            .title { font-size: 2rem; }
            .game-area { padding: 20px; margin: 10px; }
            .input-area { flex-direction: column; }
        }
    </style>
</head>
<body>
    <canvas class="matrix-bg"></canvas>
    
    <div class="game-container">
        <h1 class="title">MATRIX CODE CHALLENGE</h1>
        <p class="subtitle">Decode the scrolling algorithms • Prove your programming skills</p>
        
        <div class="game-area">
            <div class="stats">
                <div class="stat-item">🎯 Level: <span id="level">1</span></div>
                <div class="stat-item">⚡ Score: <span id="score">0</span></div>
                <div class="stat-item">⏰ Time: <span id="timer">60</span>s</div>
            </div>
            
            <div class="progress-bar">
                <div class="progress-fill" id="progress"></div>
            </div>
            
            <div class="challenge-text" id="challenge">
                def fibonacci(n): return n if n <= 1 else fibonacci(n-1) + fibonacci(n-2)
            </div>
            
            <div class="input-area">
                <input type="text" class="code-input" id="codeInput" placeholder="Type the code exactly as shown...">
                <button class="submit-btn" id="submitBtn">EXECUTE</button>
            </div>
            
            <div class="message" id="message"></div>
            <div class="hint">💡 Tip: Watch the scrolling code carefully and type it exactly!</div>
        </div>
    </div>

    <script>
        // Matrix Rain Effect
        const canvas = document.querySelector('.matrix-bg');
        const ctx = canvas.getContext('2d');
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*(){}[]<>/\\';
        const fontSize = 14;
        const columns = canvas.width / fontSize;
        const drops = [];
        
        for (let x = 0; x < columns; x++) {
            drops[x] = 1;
        }
        
        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.04)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.fillStyle = '#00ff41';
            ctx.font = fontSize + 'px Fira Code';
            
            for (let i = 0; i < drops.length; i++) {
                const text = characters.charAt(Math.floor(Math.random() * characters.length));
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }
        
        setInterval(drawMatrix, 35);
        
        // Game Logic
        const challenges = [
            'def fibonacci(n): return n if n <= 1 else fibonacci(n-1) + fibonacci(n-2)',
            'const quickSort = arr => arr.length <= 1 ? arr : [...quickSort(arr.slice(1).filter(x => x <= arr[0])), arr[0], ...quickSort(arr.slice(1).filter(x => x > arr[0]))]',
            'class TreeNode: def __init__(self, val=0, left=None, right=None): self.val, self.left, self.right = val, left, right',
            'function binarySearch(arr, target) { let left = 0, right = arr.length - 1; while (left <= right) { const mid = Math.floor((left + right) / 2); if (arr[mid] === target) return mid; arr[mid] < target ? left = mid + 1 : right = mid - 1; } return -1; }',
            'def merge_sort(arr): return arr if len(arr) <= 1 else merge(merge_sort(arr[:len(arr)//2]), merge_sort(arr[len(arr)//2:]))',
            'const dijkstra = (graph, start) => { const dist = {}, visited = new Set(), pq = [[0, start]]; Object.keys(graph).forEach(v => dist[v] = Infinity); dist[start] = 0; while (pq.length) { const [d, u] = pq.shift(); if (visited.has(u)) continue; visited.add(u); Object.entries(graph[u] || {}).forEach(([v, w]) => { if (dist[u] + w < dist[v]) { dist[v] = dist[u] + w; pq.push([dist[v], v]); pq.sort((a, b) => a[0] - b[0]); } }); } return dist; }'
        ];
        
        let currentLevel = 1;
        let score = 0;
        let timeRemaining = 60;
        let currentChallenge = '';
        let gameTimer;
        
        const elements = {
            challenge: document.getElementById('challenge'),
            input: document.getElementById('codeInput'),
            submit: document.getElementById('submitBtn'),
            message: document.getElementById('message'),
            level: document.getElementById('level'),
            score: document.getElementById('score'),
            timer: document.getElementById('timer'),
            progress: document.getElementById('progress')
        };
        
        function startNewChallenge() {
            currentChallenge = challenges[Math.floor(Math.random() * challenges.length)];
            elements.challenge.textContent = currentChallenge;
            elements.challenge.style.animation = 'none';
            setTimeout(() => {
                elements.challenge.style.animation = 'typewriter 3s steps(' + currentChallenge.length + ', end)';
            }, 10);
            elements.input.value = '';
            elements.message.textContent = '';
            elements.message.className = 'message';
        }
        
        function updateStats() {
            elements.level.textContent = currentLevel;
            elements.score.textContent = score;
            elements.timer.textContent = timeRemaining;
            elements.progress.style.width = ((60 - timeRemaining) / 60 * 100) + '%';
        }
        
        function checkAnswer() {
            const userInput = elements.input.value.trim();
            if (userInput === currentChallenge) {
                score += currentLevel * 10;
                currentLevel++;
                elements.message.textContent = '✅ CORRECT! +' + (currentLevel - 1) * 10 + ' points';
                elements.message.className = 'message success';
                createParticles('🚀');
                setTimeout(startNewChallenge, 1500);
            } else {
                elements.message.textContent = '❌ INCORRECT! Try again...';
                elements.message.className = 'message error';
                elements.input.focus();
            }
            updateStats();
        }
        
        function createParticles(emoji) {
            for (let i = 0; i < 10; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.textContent = emoji;
                particle.style.left = Math.random() * window.innerWidth + 'px';
                particle.style.top = Math.random() * window.innerHeight + 'px';
                particle.style.fontSize = (Math.random() * 20 + 10) + 'px';
                document.body.appendChild(particle);
                
                setTimeout(() => {
                    particle.style.transform = 'translateY(-100px) scale(0)';
                    particle.style.opacity = '0';
                    particle.style.transition = 'all 1s ease';
                }, 100);
                
                setTimeout(() => particle.remove(), 1100);
            }
        }
        
        function startGame() {
            timeRemaining = 60;
            gameTimer = setInterval(() => {
                timeRemaining--;
                updateStats();
                if (timeRemaining <= 0) {
                    endGame();
                }
            }, 1000);
            
            startNewChallenge();
        }
        
        function endGame() {
            clearInterval(gameTimer);
            elements.message.textContent = `🎉 GAME OVER! Final Score: ${score} | Level Reached: ${currentLevel}`;
            elements.message.className = 'message success';
            elements.input.disabled = true;
            elements.submit.disabled = true;
            
            setTimeout(() => {
                if (confirm('Game Over! Play again?')) {
                    location.reload();
                }
            }, 2000);
        }
        
        // Event Listeners
        elements.submit.addEventListener('click', checkAnswer);
        elements.input.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') checkAnswer();
        });
        
        elements.input.addEventListener('input', () => {
            const progress = (elements.input.value.length / currentChallenge.length) * 100;
            elements.input.style.background = `linear-gradient(90deg, rgba(0,255,65,0.1) ${progress}%, rgba(0,0,0,0.7) ${progress}%)`;
        });
        
        // Resize handler
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
        
        // Start the game
        startGame();
        elements.input.focus();
        
        // Easter egg: Konami code
        let konamiCode = [];
        const konamiSequence = ['ArrowUp', 'ArrowUp', 'ArrowDown', 'ArrowDown', 'ArrowLeft', 'ArrowRight', 'ArrowLeft', 'ArrowRight', 'KeyB', 'KeyA'];
        
        document.addEventListener('keydown', (e) => {
            konamiCode.push(e.code);
            if (konamiCode.length > konamiSequence.length) {
                konamiCode.shift();
            }
            
            if (JSON.stringify(konamiCode) === JSON.stringify(konamiSequence)) {
                score += 1000;
                elements.message.textContent = '🎮 KONAMI CODE ACTIVATED! +1000 BONUS!';
                elements.message.className = 'message success';
                createParticles('⭐');
                updateStats();
            }
        });
    </script>
</body>
</html>

</details>
