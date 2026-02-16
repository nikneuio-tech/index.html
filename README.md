<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="robots" content="noindex, nofollow">
    <title>Version 18.0 | Hannah</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-color: #FAF5F5; 
            --card-bg: #FFFFFF; 
            --text-primary: #3A3335; 
            --text-secondary: #968D8F; 
            --accent: #C28A94; 
            --shadow: 0 10px 30px rgba(180, 160, 165, 0.2); 
        }

        body {
            font-family: 'Outfit', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-primary);
            margin: 0;
            padding: 20px;
            padding-top: 40px;
            -webkit-font-smoothing: antialiased;
            display: none; 
            padding-bottom: 80px;
        }

        #confetti {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 100;
        }

        /* Musik-Button oben */
        .music-btn {
            background-color: var(--accent);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            font-family: 'Outfit', sans-serif;
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            display: block;
            margin: 0 auto 30px auto;
            box-shadow: 0 4px 15px rgba(194, 138, 148, 0.4);
            transition: transform 0.2s;
        }
        .music-btn:active { transform: scale(0.95); }

        .header {
            text-align: center;
            margin-bottom: 40px;
            animation: fadeInDown 1s ease-out;
        }

        h1 { font-size: 32px; font-weight: 600; margin: 0; color: var(--accent); }
        p.subtitle { font-size: 16px; color: var(--text-secondary); margin-top: 10px; font-weight: 300; }

        .gallery-grid {
            display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; max-width: 600px; margin: 0 auto;
        }

        .card {
            background-color: var(--card-bg); border-radius: 20px; padding: 12px;
            box-shadow: var(--shadow); opacity: 0; transform: translateY(30px);
            animation: fadeInUp 0.8s forwards;
        }
        .card:nth-child(1) { animation-delay: 0.2s; }
        .card:nth-child(2) { animation-delay: 0.4s; }
        .card:nth-child(3) { animation-delay: 0.6s; }
        .card:nth-child(4) { animation-delay: 0.8s; }

        .card img {
            width: 100%; aspect-ratio: 1 / 1; object-fit: cover; border-radius: 12px; background-color: #F0EBEB; 
        }

        .card-content { padding: 15px 5px 5px 5px; text-align: center; }
        .card-title { font-size: 14px; font-weight: 600; margin: 0; color: var(--accent); text-transform: uppercase; letter-spacing: 1px; }
        .card-desc { font-size: 13px; color: var(--text-secondary); margin-top: 6px; line-height: 1.4; font-weight: 300; }

        /* --- NEUER INTERAKTIVER BEREICH --- */
        .interactive-section {
            max-width: 600px;
            margin: 60px auto 0 auto;
            text-align: center;
            opacity: 0;
            animation: fadeInUp 1s forwards;
            animation-delay: 1.2s;
        }

        .action-btn {
            background-color: white;
            color: var(--text-primary);
            border: 2px solid var(--accent);
            padding: 15px 30px;
            border-radius: 25px;
            font-family: 'Outfit', sans-serif;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            margin: 10px;
            width: 90%;
            max-width: 300px;
            transition: all 0.3s;
        }
        .action-btn:active { transform: scale(0.95); }
        .action-btn:hover { background-color: var(--accent); color: white; }

        /* Generator Box */
        #generator-result {
            font-size: 18px;
            font-weight: 600;
            color: var(--accent);
            margin: 20px 0;
            min-height: 30px;
        }

        /* Top Secret Box */
        #secret-box {
            background-color: var(--card-bg);
            border-radius: 20px;
            padding: 25px;
            box-shadow: var(--shadow);
            margin-top: 20px;
            font-size: 15px;
            line-height: 1.6;
            color: var(--text-primary);
            display: none; /* Erstmal versteckt */
            border-left: 5px solid var(--accent);
            text-align: left;
        }

        @keyframes fadeInDown { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

    </style>
</head>
<body>

    <canvas id="confetti"></canvas>

    <audio id="bg-music" loop>
        <source src="song.mp3" type="audio/mpeg">
    </audio>

    <button class="music-btn" onclick="playMusic()" id="play-btn">🎵 Vibe aktivieren</button>

    <div class="header">
        <h1>Happy Birthday, Hannah</h1>
        <p class="subtitle">System-Update 18.0 erfolgreich installiert.<br>Hier ist unser Logbuch.</p>
    </div>

    <div class="gallery-grid">
        <div class="card">
            <img src="bild1.jpeg" alt="Foto 1">
            <div class="card-content">
                <p class="card-title">Patch 1.0</p>
                <p class="card-desc">Das Modul "Erstes Date" wurde initialisiert. Wir waren beide extrem nervös.</p>
            </div>
        </div>
        <div class="card">
            <img src="bild2.jpeg" alt="Foto 2">
            <div class="card-content">
                <p class="card-title">Bugfix #404</p>
                <p class="card-desc">Orientierungssinn temporär offline. Trotzdem angekommen.</p>
            </div>
        </div>
        <div class="card">
            <img src="bild3.jpeg" alt="Foto 3">
            <div class="card-content">
                <p class="card-title">Feature Update</p>
                <p class="card-desc">Gemeinsamer Urlaub erfolgreich in die Datenbank geladen.</p>
            </div>
        </div>
        <div class="card">
            <img src="bild4.jpeg" alt="Foto 4">
            <div class="card-content">
                <p class="card-title">Performance</p>
                <p class="card-desc">Läuft seit dem 25.03.2022 erstaunlich stabil. Bestes Release bisher.</p>
            </div>
        </div>
    </div>

    <div class="interactive-section">
        
        <button class="action-btn" onclick="startGenerator()">🎁 Geschenk-Modul starten</button>
        <div id="generator-result"></div>

        <button class="action-btn" onclick="toggleSecret()">✉️ System-Admin Nachricht</button>
        <div id="secret-box">
            Hey Hannah,<br><br>
            du weißt ganz genau, ich bin absolut nicht der Typ für kitschige Romane oder ellenlange Liebesbriefe. Das ist einfach null meine Art.<br><br>
            Aber ich wollte dir trotzdem etwas schenken, das zeigt, wie wichtig du mir bist. Also hab ich mich hingesetzt und dir das hier auf meine Art gebaut. Danke für die geile Zeit seit 2022. <br><br>
            Alles Gute zum 18. Geburtstag. Ich liebe dich!<br><br>
            Dein Niklas
        </div>

    </div>

    <script>
        const richtigePIN = "25.03.2022"; 
        const pin = prompt("System gesperrt. Bitte Freischalt-PIN (Datum) eingeben:");
        
        if (pin === richtigePIN) {
            document.body.style.display = "block";
            startHearts(); 
        } else {
            document.body.style.display = "block";
            document.body.innerHTML = "<div style='display:flex; height:100vh; justify-content:center; align-items:center; flex-direction:column;'><h1 style='color:#C28A94; font-size:40px; margin:0;'>❌</h1><p style='color:#968D8F; font-family:sans-serif; margin-top:20px;'>Zugriff verweigert. Falsche PIN.</p></div>";
        }

        // Musik abspielen
        function playMusic() {
            let music = document.getElementById("bg-music");
            let btn = document.getElementById("play-btn");
            if (music.paused) {
                music.play();
                btn.innerText = "🎵 Musik läuft...";
                btn.style.backgroundColor = "#968D8F";
            } else {
                music.pause();
                btn.innerText = "🎵 Vibe aktivieren";
                btn.style.backgroundColor = "var(--accent)";
            }
        }

        // Geschenk-Generator (Spielautomat)
        function startGenerator() {
            const resultBox = document.getElementById("generator-result");
            const btn = document.querySelector("button[onclick='startGenerator()']");
            btn.disabled = true; // Button sperren während es läuft
            
            // Witzige Fake-Geschenke
            const fakeGifts = [
                "Lade Datenbank...", 
                "Gutschein für 1x Abwasch", 
                "Ein feuchter Händedruck", 
                "Ein gebrauchter Kaugummi", 
                "Gutschein für 1x Recht haben", 
                "Fehler im System...", 
                "Socken"
            ];
            
            // Das echte Geschenk!
            const finalGift = "Ein Pandora-Anhänger für dein Armband 💍✨";
            
            let i = 0;
            // Der "Rattern"-Effekt
            let interval = setInterval(() => {
                resultBox.innerText = fakeGifts[i % fakeGifts.length];
                i++;
            }, 150); // Alle 150 Millisekunden wechselt der Text

            // Nach 3 Sekunden stoppen und richtiges Geschenk zeigen
            setTimeout(() => {
                clearInterval(interval);
                resultBox.innerHTML = "<span style='color:#3A3335;'>System-Ergebnis:</span><br><span style='font-size:22px; font-weight:700;'>" + finalGift + "</span>";
                btn.style.display = "none"; // Button verschwindet danach
            }, 3000);
        }

        // Top Secret Brief aufklappen
        function toggleSecret() {
            const box = document.getElementById("secret-box");
            if(box.style.display === "none" || box.style.display === "") {
                box.style.display = "block";
            } else {
                box.style.display = "none";
            }
        }

        // Herz-Animation
        function startHearts() {
            const canvas = document.getElementById('confetti'); 
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            
            const particles = [];
            const colors = ['#ff0000', '#cc0000', '#e60000', '#ff4d4d']; 
            
            for(let i=0; i<60; i++) { 
                particles.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height - canvas.height,
                    size: Math.random() * 15 + 15, 
                    color: colors[Math.floor(Math.random() * colors.length)],
                    speedY: Math.random() * 2 + 1.5, 
                    speedX: Math.random() * 1 - 0.5
                });
            }

            function draw() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                for(let p of particles) {
                    ctx.font = p.size + "px Arial";
                    ctx.fillStyle = p.color;
                    ctx.fillText("❤", p.x, p.y); 
                    p.y += p.speedY;
                    p.x += p.speedX;
                    if(p.y > canvas.height + 50) {
                        p.y = -50;
                        p.x = Math.random() * canvas.width;
                    }
                }
                requestAnimationFrame(draw);
            }
            draw();
            setTimeout(() => { canvas.style.opacity = '0'; canvas.style.transition = 'opacity 2.5s ease-out'; }, 5000);
        }
    </script>
</body>
</html>
