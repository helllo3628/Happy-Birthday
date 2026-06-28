
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday bluuebvrry🎉</title>
    <style>
        :root {
            --primary-pink: #ff758c;
            --secondary-pink: #ff7eb3;
            --bg-gradient: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--bg-gradient);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            overflow-x: hidden;
        }

        /* --- Confetti Canvas --- */
        #confetti-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 999;
        }

        /* --- Main Card Container --- */
        .card {
            background: white;
            padding: 2.5rem;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            text-align: center;
            max-width: 450px;
            width: 90%;
            margin: 3rem auto 1.5rem;
            position: relative;
            z-index: 10;
            animation: fadeIn 1.2s ease-out;
        }

        /* --- Photo Styling with Cute Floating Animation --- */
        .photo-container {
            width: 180px;
            height: 180px;
            margin: 0 auto 1.5rem;
            border-radius: 50%;
            border: 5px solid white;
            box-shadow: 0 8px 20px rgba(255, 117, 140, 0.4);
            overflow: hidden;
            animation: float 3s ease-in-out infinite;
        }

        .photo-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        /* --- Typography --- */
        h1 {
            color: #333;
            margin-bottom: 0.5rem;
            font-size: 2.2rem;
        }

        .wishes {
            color: #666;
            font-size: 1.1rem;
            line-height: 1.6;
            margin-bottom: 2rem;
        }

        /* --- Interactive Button --- */
        .btn {
            background: linear-gradient(45deg, var(--primary-pink), var(--secondary-pink));
            color: white;
            border: none;
            padding: 0.8rem 2rem;
            font-size: 1.1rem;
            font-weight: bold;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(255, 117, 140, 0.4);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .btn:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 20px rgba(255, 117, 140, 0.6);
        }

        .btn:active {
            transform: scale(0.98);
        }

        /* --- Interactive Balloon Section --- */
        .game-zone {
            width: 100%;
            max-width: 500px;
            height: 200px;
            position: relative;
            margin-top: 1rem;
            overflow: hidden;
            border-radius: 15px;
            background: rgba(255, 255, 255, 0.3);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.5);
        }

        .game-instruction {
            color: #555;
            font-weight: 500;
            margin-top: 1rem;
            font-size: 0.9rem;
        }

        .balloon {
            position: absolute;
            width: 40px;
            height: 50px;
            border-radius: 50% 50% 50% 50% / 40% 40% 60% 60%;
            cursor: pointer;
            animation: rise 4s linear infinite;
            bottom: -60px;
        }

        .balloon::after {
            content: "▲";
            color: inherit;
            font-size: 8px;
            position: absolute;
            bottom: -6px;
            left: 16px;
        }

        /* --- Animations --- */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-10px) rotate(3deg); }
        }

        @keyframes rise {
            0% { transform: translateY(0); opacity: 1; }
            90% { opacity: 1; }
            100% { transform: translateY(-280px); opacity: 0; }
        }
    </style>
</head>
<body>

    <canvas id="confetti-canvas"></canvas>

    <div class="card">
        <!-- Birthday Photo -->
        <div class="photo-container">
            <!-- Replace the URL below with your own photo file path (e.g., "birthday-girl.jpg") -->
            <img src="she.png" alt="Birthday Person">
        </div>

        <h1>Happy Birthday, Name! 🎂</h1>
        <p class="wishes">
            Wishing you a day filled with laughter, love, and lots of cake! May this year bring you endless joy and success. ✨
        </p>

        <button class="btn" onclick="burstConfetti()">Celebrate! 🎉</button>
    </div>

    <!-- Interactive Game Zone -->
    <p class="game-instruction">🎈 Pop the balloons for a surprise! 🎈</p>
    <div class="game-zone" id="game-zone"></div>

    <script>
        // --- Confetti System ---
        const canvas = document.getElementById('confetti-canvas');
        const ctx = canvas.getContext('2d');
        let confetti = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class ConfettiParticle {
            constructor(burst = false) {
                this.x = burst ? window.innerWidth / 2 : Math.random() * window.innerWidth;
                this.y = burst ? window.innerHeight / 2 : Math.random() * -window.innerHeight;
                this.size = Math.random() * 8 + 5;
                this.color = `hsl(${Math.random() * 360}, 80%, 60%)`;
                this.speedX = burst ? (Math.random() - 0.5) * 15 : (Math.random() - 0.5) * 3;
                this.speedY = burst ? (Math.random() - 0.7) * 15 : Math.random() * 3 + 2;
                this.rotation = Math.random() * 360;
                this.rotationSpeed = (Math.random() - 0.5) * 10;
            }

            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                this.rotation += this.rotationSpeed;
                // Friction for bursts
                this.speedX *= 0.98;
                this.speedY += 0.1; // gravity
            }

            draw() {
                ctx.save();
                ctx.translate(this.x, this.y);
                ctx.rotate(this.rotation * Math.PI / 180);
                ctx.fillStyle = this.color;
                ctx.fillRect(-this.size / 2, -this.size / 2, this.size, this.size);
                ctx.restore();
            }
        }

        // Initialize steady stream of confetti
        for(let i = 0; i < 50; i++) {
            confetti.push(new ConfettiParticle());
        }

        function burstConfetti() {
            for (let i = 0; i < 80; i++) {
                confetti.push(new ConfettiParticle(true));
            }
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            confetti.forEach((p, index) => {
                p.update();
                p.draw();
                // Remove dead burst particles or offscreen normal ones
                if (p.y > canvas.height || p.x < 0 || p.x > canvas.width) {
                    confetti[index] = new ConfettiParticle(); // recycle
                }
            });
            requestAnimationFrame(animate);
        }
        animate();


        // --- Interactive Balloon Game ---
        const gameZone = document.getElementById('game-zone');
        const colors = ['#ff4d6d', '#ff758c', '#ff8fa3', '#ffb3c1', '#38b000', '#00b4d8', '#ffb703'];

        function createBalloon() {
            const balloon = document.createElement('div');
            balloon.classList.add('balloon');
            
            // Random styling
            const randomColor = colors[Math.floor(Math.random() * colors.length)];
            balloon.style.backgroundColor = randomColor;
            balloon.style.color = randomColor;
            balloon.style.left = Math.random() * (gameZone.clientWidth - 40) + 'px';
            
            // Random speed variation
            const duration = Math.random() * 2 + 3; // 3s to 5s
            balloon.style.animationDuration = duration + 's';

            // Pop Event
            balloon.addEventListener('click', () => {
                burstConfetti(); // Trigger explosion on pop!
                balloon.remove();
            });

            gameZone.appendChild(balloon);

            // Auto remove when animation ends to prevent memory leak
            setTimeout(() => {
                balloon.remove();
            }, duration * 1000);
        }

        // Keep spawning balloons
        setInterval(createBalloon, 800);
    </script>
</body>
</html>
