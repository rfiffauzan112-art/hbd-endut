<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HBD Dafiya Faqiha - Entong 3D Edition</title>
    <link href="https://fonts.googleapis.com/css2?family=Luckiest+Guy&family=Fredoka+One&display=swap" rel="stylesheet">
    <style>
        :root {
            --ungu-vibes: #9b59b6;
            --ungu-tua: #6c3483;
            --kuning: #f1c40f;
            --putih: #ffffff;
        }

        body {
            margin: 0;
            padding: 0;
            background: radial-gradient(circle, #e1bee7, #9b59b6);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Fredoka One', cursive;
            overflow: hidden;
        }

        /* --- KADO BERGOYANG --- */
        #gift-screen {
            text-align: center;
            cursor: pointer;
        }

        .box {
            position: relative;
            width: 160px;
            height: 140px;
            background: var(--kuning);
            margin: 0 auto;
            border-radius: 10px;
            animation: bounce 0.6s infinite alternate;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
        }

        .box::before { content: ''; position: absolute; width: 30px; height: 100%; background: var(--ungu-tua); left: 50%; transform: translateX(-50%); }
        .box::after { content: ''; position: absolute; width: 100%; height: 30px; background: var(--ungu-tua); top: 50%; transform: translateY(-50%); }

        @keyframes bounce {
            from { transform: translateY(0) rotate(-5deg); }
            to { transform: translateY(-20px) rotate(5deg); }
        }

        /* --- KARTU UTAMA --- */
        #main-card {
            display: none;
            width: 90%;
            max-width: 400px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 30px;
            padding: 25px;
            text-align: center;
            border: 6px solid var(--putih);
            box-shadow: 0 10px 50px rgba(0,0,0,0.3);
            position: relative;
            animation: popIn 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes popIn {
            0% { transform: scale(0); }
            100% { transform: scale(1); }
        }

        /* --- BINGKAI FOTO & ENTONG 3D --- */
        .frame-container {
            position: relative;
            width: 100%;
            height: 250px;
            margin: 20px 0;
        }

        .photo-slider {
            width: 100%;
            height: 100%;
            border-radius: 20px;
            overflow: hidden;
            border: 4px solid var(--ungu-vibes);
            position: relative;
            background: #eee;
        }

        .slides {
            display: flex;
            height: 100%;
            transition: 0.5s ease-in-out;
        }

        .slide {
            min-width: 100%;
            background-size: cover;
            background-position: center;
        }

        /* Karakter Entong 3D (Floating) */
        .entong-3d {
            position: absolute;
            bottom: -10px;
            right: -20px;
            width: 140px;
            filter: drop-shadow(5px 5px 10px rgba(0,0,0,0.3));
            z-index: 5;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(5deg); }
            50% { transform: translateY(-15px) rotate(-5deg); }
        }

        h1 {
            font-family: 'Luckiest Guy', cursive;
            color: var(--ungu-tua);
            font-size: 2.2em;
            margin: 10px 0;
            letter-spacing: 2px;
        }

        .wish-text {
            color: #444;
            font-size: 0.95rem;
            line-height: 1.6;
            background: #fdf2ff;
            padding: 15px;
            border-radius: 15px;
            border: 2px dashed var(--ungu-vibes);
        }

        /* --- BALLOONS --- */
        .balloon {
            position: absolute;
            width: 40px;
            height: 50px;
            border-radius: 50%;
            z-index: -1;
            animation: floatUp 4s linear infinite;
        }

        @keyframes floatUp {
            from { transform: translateY(100vh); opacity: 1; }
            to { transform: translateY(-100vh); opacity: 0; }
        }
    </style>
</head>
<body>

    <audio id="bday-music" loop>
        <source src="https://assets.mixkit.co/music/preview/mixkit-happy-birthday-to-you-child-singing-665.mp3" type="audio/mpeg">
    </audio>

    <div id="gift-screen" onclick="startCelebration()">
        <div class="box"></div>
        <h1 style="color: white; text-shadow: 2px 2px var(--ungu-tua);">KLIK KADONYA, DAFIYA!</h1>
    </div>

    <div id="main-card">
        <h1>HAPPY 8<sup>th</sup> BIRTHDAY</h1>
        <p style="color: var(--ungu-vibes); margin-bottom: 5px;">Dafiya Faqiha Nasution</p>
        
        <div class="frame-container">
            <div class="photo-slider">
                <div class="slides" id="slide-engine">
                    <div class="slide" style="background-image: url('dafiya1.jpeg')"></div>
                    <div class="slide" style="background-image: url('dafiya2.jpg')"></div>
                    <div class="slide" style="background-image: url('dafiya3.jpg')"></div>
                </div>
            </div>

            <img src="https://api.dicebear.com/7.x/adventurer/svg?seed=Dafiya&top[]=shaved&topProbability=100&backgroundColor=b6e3f4" class="entong-3d" alt="Entong 3D">
        </div>

        <div class="wish-text">
            Selamat ulang tahun ya Ndut! Semoga panjang umur, sehat selalu, dan jadi anak yang pintar. Berbakti kepada kedua orang tua, dan
            Makin rajin belajarnya!! 🎉💜
        </div>

        <p style="font-size: 0.7rem; color: #999; margin-top: 10px;">Klik foto untuk ganti manual!</p>
    </div>

    <script>
        function startCelebration() {
            // Sembunyikan Kado, Tampilkan Kartu
            document.getElementById('gift-screen').style.display = 'none';
            document.getElementById('main-card').style.display = 'block';
            
            // Putar Lagu Happy Birthday
            const music = document.getElementById('bday-music');
            music.play();

            // Efek Balon & Confetti
            setInterval(createBalloon, 500);
            
            // Jalankan Slider Foto
            let current = 0;
            const engine = document.getElementById('slide-engine');
            setInterval(() => {
                current = (current + 1) % 3;
                engine.style.transform = `translateX(-${current * 100}%)`;
            }, 3000);
        }

        function createBalloon() {
            const colors = ['#9b59b6', '#8e44ad', '#f1c40f', '#e74c3c', '#3498db'];
            const b = document.createElement('div');
            b.className = 'balloon';
            b.style.left = Math.random() * 100 + 'vw';
            b.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
            b.style.opacity = '0.7';
            document.body.appendChild(b);
            
            setTimeout(() => { b.remove(); }, 4000);
        }
    </script>
</body>
</html>
