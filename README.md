<!DOCTYPE html>
<html lang="az">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sənin üçün, Aliyə ❤️</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Montserrat:wght@300;500;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    
    <style>
        :root {
            --accent: #ff4d6d;
            --glass: rgba(255, 255, 255, 0.12);
            --border: rgba(255, 255, 255, 0.25);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            cursor: none; /* Custom cursor üçün */
        }

        body {
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #0a0a0a;
            font-family: 'Montserrat', sans-serif;
            overflow: hidden;
            color: #fff;
        }

        /* Arxa fon animasiyası */
        #bg-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at center, #1a0a1a 0%, #000 100%);
            z-index: -1;
        }

        /* Özel Kursor */
        #cursor {
            position: fixed;
            width: 20px;
            height: 20px;
            background: var(--accent);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            mix-blend-mode: screen;
            box-shadow: 0 0 20px var(--accent);
        }

        /* Əsas Konteyner */
        .stage {
            position: relative;
            width: 90%;
            max-width: 550px;
            padding: 50px;
            background: var(--glass);
            backdrop-filter: blur(25px);
            -webkit-backdrop-filter: blur(25px);
            border: 1px solid var(--border);
            border-radius: 40px;
            text-align: center;
            box-shadow: 0 25px 50px rgba(0,0,0,0.5);
            display: none; /* JS idarə edəcək */
            transform-style: preserve-3d;
        }

        .stage.active {
            display: block;
        }

        h1 {
            font-family: 'Dancing Script', cursive;
            font-size: 3.5rem;
            margin-bottom: 25px;
            background: linear-gradient(to right, #ff4d6d, #ff8fa3);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        p {
            font-size: 1.1rem;
            line-height: 1.8;
            font-weight: 300;
            margin-bottom: 40px;
            color: #eee;
        }

        /* Professional Düymə */
        .btn-modern {
            position: relative;
            padding: 18px 40px;
            background: transparent;
            border: 2px solid var(--accent);
            color: #fff;
            font-size: 1rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 2px;
            border-radius: 100px;
            overflow: hidden;
            transition: 0.4s;
            z-index: 1;
        }

        .btn-modern::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 0%;
            height: 100%;
            background: var(--accent);
            z-index: -1;
            transition: 0.4s;
        }

        .btn-modern:hover::before {
            width: 100%;
        }

        .btn-modern:hover {
            box-shadow: 0 0 30px var(--accent);
            transform: scale(1.05);
        }

        /* Ürək Yağışı Animasiyası */
        .heart-particle {
            position: absolute;
            color: var(--accent);
            user-select: none;
            pointer-events: none;
        }

        /* Progress Bar */
        .progress-container {
            position: absolute;
            bottom: -60px;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            height: 4px;
            background: rgba(255,255,255,0.1);
            border-radius: 2px;
        }

        .progress-fill {
            width: 33%;
            height: 100%;
            background: var(--accent);
            box-shadow: 0 0 10px var(--accent);
            transition: 1s ease;
        }
    </style>
</head>
<body>

    <div id="cursor"></div>
    <canvas id="bg-canvas"></canvas>

    <div id="s1" class="stage active">
        <h1>Mənim Dünyam.. ❤️</h1>
        <p id="t1">Bəzən sözlər hisslərin qarşısında aciz qalır. Sənin varlığın mənim üçün ən böyük hədiyyədir. Hər şeyi yenidən yazmağa hazırsan?</p>
        <button class="btn-modern" onclick="nextStage(2)">Bəli, Hazıram</button>
        <div class="progress-container"><div class="progress-fill" style="width: 33%;"></div></div>
    </div>

    <div id="s2" class="stage">
        <h1>Bağışla Məni... 🌹</h1>
        <p id="t2">Səni incitdiyim hər an üçün içimdə bir boşluq yaranır. Sən mənim qəlbimin tək sahibisən. Gəl bütün kədəri silək, sadəcə biz qalaq.</p>
        <button class="btn-modern" onclick="nextStage(3)">Davam edək...</button>
        <div class="progress-container"><div class="progress-fill" style="width: 66%;"></div></div>
    </div>

    <div id="s3" class="stage">
        <h1>Söz Verirəm ❤️</h1>
        <p id="t3">Turqanın həyatında səndən daha dəyərli heç nə yoxdur. Sənin gülüşün üçün dünyanı qarşıma alaram. Səni hər şeydən çox sevirəm, Aliyə!</p>
        <button class="btn-modern" onclick="finalSurprise()">Həmişə Yanımda Qal</button>
        <div class="progress-container"><div class="progress-fill" style="width: 100%;"></div></div>
    </div>

    <script>
        // Custom Cursor Movement
        const cursor = document.getElementById('cursor');
        document.addEventListener('mousemove', e => {
            gsap.to(cursor, {x: e.clientX, y: e.clientY, duration: 0.1});
        });

        // Stage Management
        function nextStage(num) {
            const current = document.querySelector('.stage.active');
            const next = document.getElementById('s' + num);

            gsap.to(current, {
                opacity: 0, 
                y: -50, 
                rotateX: 20, 
                duration: 0.6, 
                onComplete: () => {
                    current.classList.remove('active');
                    next.classList.add('active');
                    gsap.fromTo(next, 
                        {opacity: 0, y: 50, rotateX: -20}, 
                        {opacity: 1, y: 0, rotateX: 0, duration: 0.8, ease: "back.out(1.7)"}
                    );
                }
            });
        }

        // Background Animation (Simple Starfield)
        const canvas = document.getElementById('bg-canvas');
        const ctx = canvas.getContext('2d');
        let stars = [];

        function initCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            stars = [];
            for(let i=0; i<150; i++) {
                stars.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height,
                    size: Math.random() * 2,
                    speed: Math.random() * 0.5
                });
            }
        }

        function drawStars() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "rgba(255, 77, 109, 0.5)";
            stars.forEach(s => {
                ctx.beginPath();
                ctx.arc(s.x, s.y, s.size, 0, Math.PI * 2);
                ctx.fill();
                s.y -= s.speed;
                if(s.y < 0) s.y = canvas.height;
            });
            requestAnimationFrame(drawStars);
        }

        window.addEventListener('resize', initCanvas);
        initCanvas();
        drawStars();

        // Final Heart Explosion
        function finalSurprise() {
            for(let i=0; i<100; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'heart-particle';
                    heart.innerHTML = '❤️';
                    heart.style.left = Math.random() * 100 + 'vw';
                    heart.style.top = '100vh';
                    heart.style.fontSize = Math.random() * 30 + 10 + 'px';
                    document.body.appendChild(heart);

                    gsap.to(heart, {
                        y: '-110vh',
                        x: (Math.random() - 0.5) * 400,
                        duration: 3 + Math.random() * 2,
                        opacity: 0,
                        ease: "power1.out",
                        onComplete: () => heart.remove()
                    });
                }, i * 50);
            }
            
            gsap.to(".btn-modern", {scale: 0.9, yoyo: true, repeat: 5});
        }
    </script>
</body>
</html>
