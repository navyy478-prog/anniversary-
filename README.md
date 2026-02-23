<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>4 Months of Magic ✨</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Montserrat:wght@300;400;600&display=swap');

        :root {
            --accent: #ff0054;
            --bg-dark: #0f0c29;
            --glass: rgba(255, 255, 255, 0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            background: #0f0c29;
            background: linear-gradient(to bottom, #0f0c29, #302b63, #24243e);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Montserrat', sans-serif;
            overflow: hidden;
            color: white;
        }

        /* Floating Background Elements */
        .bubble {
            position: absolute;
            bottom: -100px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            opacity: 0.5;
            animation: rise 10s infinite ease-in;
        }

        @keyframes rise {
            0% { transform: translateY(0) scale(1); opacity: 0; }
            50% { opacity: 0.5; }
            100% { transform: translateY(-120vh) scale(1.5); opacity: 0; }
        }

        .container {
            width: 85%;
            max-width: 400px;
            background: var(--glass);
            backdrop-filter: blur(25px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 30px;
            border-radius: 40px;
            text-align: center;
            box-shadow: 0 25px 45px rgba(0,0,0,0.5);
            display: none;
            z-index: 10;
        }

        .active { display: block; animation: slideIn 0.8s ease; }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h1 { font-family: 'Dancing Script', cursive; font-size: 2.8rem; color: #ff0054; text-shadow: 0 0 15px rgba(255,0,84,0.5); }

        /* Scratch Card Style */
        #scratch-container {
            position: relative;
            width: 250px;
            height: 150px;
            margin: 20px auto;
            border-radius: 20px;
            overflow: hidden;
            background: white;
            color: #333;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 1.2rem;
        }

        #scratch-canvas {
            position: absolute;
            top: 0;
            left: 0;
            cursor: crosshair;
            touch-action: none;
        }

        /* Live Timer */
        .timer-box {
            font-size: 0.9rem;
            margin: 15px 0;
            letter-spacing: 2px;
            color: #00f2fe;
            font-weight: 600;
        }

        .btn {
            background: linear-gradient(45deg, #ff0054, #ff5400);
            border: none;
            padding: 12px 30px;
            color: white;
            border-radius: 30px;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(255,0,84,0.4);
            margin-top: 20px;
        }

        .btn:active { transform: scale(0.95); }

        .milestone-tag {
            display: inline-block;
            background: rgba(255, 255, 255, 0.1);
            padding: 5px 15px;
            border-radius: 15px;
            margin: 5px;
            font-size: 0.8rem;
        }

    </style>
</head>
<body>

    <div id="step1" class="container active">
        <h1>Hey Love! ❤️</h1>
        <p style="margin-top: 10px;">Hamare safar ko ho gaye hain...</p>
        <div class="timer-box" id="timer">Calculating...</div>
        <p>Har ek second tumhare saath keemti hai.</p>
        <button class="btn" onclick="showStep(2)">Kya tum taiyaar ho?</button>
    </div>

    <div id="step2" class="container">
        <h1>Scratch the Card! ✨</h1>
        <p>Iske neeche ek secret message hai...</p>
        <div id="scratch-container">
            <div style="padding: 20px;">"You are my favorite 4-month-long habit! ❤️"</div>
            <canvas id="scratch-canvas" width="250" height="150"></canvas>
        </div>
        <p id="scratch-hint">Ghis kar dekho! 😉</p>
        <button id="next-from-scratch" class="btn" style="display:none;" onclick="showStep(3)">Aage dekho...</button>
    </div>

    <div id="step3" class="container">
        <h1>Mere Dil Se... ✍️</h1>
        <p style="font-style: italic; line-height: 1.8;">
            "Char mahine lage, dil ko ghar banane mein,<br>
            Tumsa na koi mila iss poore zamane mein.<br>
            Ye 121 din toh sirf ek haseen trailer hain,<br>
            Poori film baaki hai, mere saath nibhane mein."
        </p>
        <div style="margin-top: 15px;">
            <span class="milestone-tag">121 Days</span>
            <span class="milestone-tag">2904 Hours</span>
            <span class="milestone-tag">Infinity To Go</span>
        </div>
        <button class="btn" onclick="showStep(4)">Ek Aakhiri Cheez</button>
    </div>

    <div id="step4" class="container">
        <h1>Happy 4 Months! 🌹</h1>
        <img src="https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExbmN6M2xobGZrbWoxYnE2Nzh2ZzRkbmx0YWN6bGNidTVvYzBocXFhMiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/LpDmM2dQvXvA9dfmS2/giphy.gif" width="100%" style="border-radius: 20px; margin: 15px 0;">
        <p>Main hamesha tumhare saath hoon. I Promise!</p>
        <button class="btn" onclick="alert('I LOVE YOU FOREVER! ❤️')">Send a Kiss? 💋</button>
    </div>

    <script>
        // --- Timer Logic ---
        function updateTimer() {
            // Yahan apni anniversary date dalo (Year, MonthIndex(0-11), Day)
            const startDate = new Date(2025, 9, 24); // Example: Oct 24, 2025
            const now = new Date();
            const diff = now - startDate;

            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
            const mins = Math.floor((diff / 1000 / 60) % 60);
            const secs = Math.floor((diff / 1000) % 60);

            document.getElementById('timer').innerHTML = `${days}D : ${hours}H : ${mins}M : ${secs}S`;
        }
        setInterval(updateTimer, 1000);

        // --- Step Controller ---
        function showStep(s) {
            document.querySelectorAll('.container').forEach(c => c.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            if(s === 2) initScratch();
        }

        // --- Scratch Card Logic ---
        function initScratch() {
            const canvas = document.getElementById('scratch-canvas');
            const ctx = canvas.getContext('2d');
            let isDrawing = false;

            // Cover the canvas
            ctx.fillStyle = '#999';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#666';
            ctx.font = "16px Arial";
            ctx.fillText("Ghislo Mujhe 💋", 60, 80);

            function scratch(e) {
                if (!isDrawing) return;
                const rect = canvas.getBoundingClientRect();
                const x = (e.clientX || e.touches[0].clientX) - rect.left;
                const y = (e.clientY || e.touches[0].clientY) - rect.top;
                
                ctx.globalCompositeOperation = 'destination-out';
                ctx.beginPath();
                ctx.arc(x, y, 20, 0, Math.PI * 2);
                ctx.fill();

                // Check if enough is scratched
                checkScratch();
            }

            function checkScratch() {
                const data = ctx.getImageData(0, 0, canvas.width, canvas.height).data;
                let cleared = 0;
                for (let i = 0; i < data.length; i += 4) {
                    if (data[i + 3] === 0) cleared++;
                }
                if (cleared > (data.length / 4) * 0.5) {
                    document.getElementById('next-from-scratch').style.display = 'inline-block';
                    document.getElementById('scratch-hint').innerHTML = "Perfect! ❤️";
                }
            }

            canvas.addEventListener('mousedown', () => isDrawing = true);
            canvas.addEventListener('touchstart', () => isDrawing = true);
            window.addEventListener('mouseup', () => isDrawing = false);
            window.addEventListener('touchend', () => isDrawing = false);
            canvas.addEventListener('mousemove', scratch);
            canvas.addEventListener('touchmove', scratch);
        }

        // --- Create Bubbles ---
        function createBubbles() {
            const b = document.createElement('div');
            b.classList.add('bubble');
            const size = Math.random() * 60 + 10 + "px";
            b.style.width = size;
            b.style.height = size;
            b.style.left = Math.random() * 100 + "vw";
            b.style.animationDuration = Math.random() * 5 + 5 + "s";
            document.body.appendChild(b);
            setTimeout(() => b.remove(), 10000);
        }
        setInterval(createBubbles, 500);

    </script>
</body>
</html>
