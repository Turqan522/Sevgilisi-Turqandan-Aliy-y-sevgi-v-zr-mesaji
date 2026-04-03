<!DOCTYPE html>
<html lang="az">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aliyə üçün Özəl ❤️</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <style>
        :root {
            --primary-pink: #ff758c;
            --secondary-pink: #ff7eb3;
            --text-color: #2d3436;
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #ff758c 0%, #ff7eb3 100%);
            display: flex;
            justify-content: center;
            align-items: center;
        }

        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            z-index: 0;
        }

        .card {
            position: relative;
            z-index: 10;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 30px;
            padding: 50px;
            width: 80%;
            max-width: 600px;
            text-align: center;
            box-shadow: 0 25px 45px rgba(0,0,0,0.1);
            color: white;
            display: none; /* JS ilə idarə olunacaq */
        }

        .card.active {
            display: block;
        }

        h1 {
            font-size: 2.8rem;
            margin-bottom: 20px;
            font-weight: 700;
            text-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        .typing-text {
            font-size: 1.3rem;
            line-height: 1.8;
            min-height: 100px;
            margin-bottom: 30px;
        }

        .btn {
            background: white;
            color: var(--primary-pink);
            padding: 15px 45px;
            border-radius: 50px;
            border: none;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }

        .btn:hover {
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 15px 30px rgba(0,0,0,0.2);
        }

        /* Ürək animasiyası */
        .floating-heart {
            position: absolute;
            pointer-events: none;
            opacity: 0.6;
            filter: drop-shadow(0 0 5px rgba(255,255,255,0.5));
            z-index: 1;
        }

        .highlight {
            color: #fff;
            font-weight: bold;
            display: block;
            margin-top: 15px;
            font-size: 1.6rem;
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <canvas id="bg-canvas"></canvas>

    <div id="step1" class="card active">
        <h1 id="title1"></h1>
        <div class="typing-text" id="text1"></div>
        <button class="btn" onclick="goToStep2()">Mənim üçün çox önəmlisən...</button>
    </div>

    <div id="step2" class="card">
        <h1 id="title2">Bağışla Məni... 🌹</h1>
        <div class="typing-text" id="text2"></div>
        <button class="btn" onclick="finalSurprise()">Səni Çox Sevirəm!</button>
    </div>

    <script>
        // Yazı animasiyası funksiyası
        function typeWriter(elementId, text, speed, callback) {
            let i = 0;
            const element = document.getElementById(elementId);
            element.innerHTML = "";
            function type() {
                if (i < text.length) {
                    element.innerHTML += text.charAt(i);
                    i++;
                    setTimeout(type, speed);
                } else if (callback) {
                    callback();
                }
            }
            type();
        }

        // İlkin yüklənmə
        window.onload = () => {
            typeWriter("title1", "Salam, Mənim Dünyam.. ❤️", 70, () => {
                typeWriter("text1", "Hər şeyi kənara qoyub, sadəcə mənə qulaq asmağını istəyirəm. Səninlə keçən hər anım mənim üçün bir möcüzədir...", 40);
            });
            createFloatingHearts();
        };

        function goToStep2() {
            gsap.to("#step1", {duration: 0.5, opacity: 0, scale: 0.8, display: "none", onComplete: () => {
                const s2 = document.getElementById("step2");
                s2.classList.add("active");
                gsap.fromTo("#step2", {opacity: 0, scale: 1.2}, {duration: 0.8, opacity: 1, scale: 1});
                
                typeWriter("text2", "Səni incitdiyim hər saniyə üçün peşmanam. Sənin gülüşün mənim günəşimdir. Gəl bütün qaranlıqları geridə qoyaq və yenidən biz olaq. Sən mənim həyatımın mənasısan. ❤️", 40);
            }});
        }

        function finalSurprise() {
            // Ekranı ürəklərlə doldur
            for(let i=0; i<50; i++) {
                setTimeout(createSingleHeart, i * 100);
            }
            alert("Səni Dünyalar Qədər Sevirəm, Aliyə! ❤️");
        }

        // Arxa fon ürək effekti
        function createSingleHeart() {
            const heart = document.createElement('div');
            heart.classList.add('floating-heart');
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.top = '110vh';
            heart.style.fontSize = (Math.random() * 30 + 10) + 'px';
            document.body.appendChild(heart);

            gsap.to(heart, {
                y: '-120vh',
                x: (Math.random() - 0.5) * 200,
                rotation: Math.random() * 360,
                duration: Math.random() * 3 + 2,
                ease: "power1.out",
                onComplete: () => heart.remove()
            });
        }

        function createFloatingHearts() {
            setInterval(createSingleHeart, 400);
        }

        // Mouse hərəkətinə görə kartın tərpənməsi (Paralaks)
        document.addEventListener("mousemove", (e) => {
            const x = (window.innerWidth / 2 - e.pageX) / 25;
            const y = (window.innerHeight / 2 - e.pageY) / 25;
            gsap.to(".card", {rotationY: x, rotationX: y, ease: "power2.out", duration: 0.5});
        });

    </script>
</body>
</html>
