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
            /* Neue helle, romantische Farbpalette */
            --bg-color: #FAF5F5; /* Sehr weiches, helles Creme-Rosé */
            --card-bg: #FFFFFF; /* Cleane weiße Karten */
            --text-primary: #3A3335; /* Weiches Dunkelgrau/Braun statt hartem Schwarz */
            --text-secondary: #968D8F; /* Elegantes, mittleres Grau */
            --accent: #C28A94; /* Ein edles Altrosa / Roségold */
            --shadow: 0 10px 30px rgba(180, 160, 165, 0.2); /* Sanfter, warmer Schatten */
        }

        body {
            font-family: 'Outfit', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-primary);
            margin: 0;
            padding: 20px;
            padding-top: 60px;
            -webkit-font-smoothing: antialiased;
            display: none; 
        }

        #confetti {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 100;
        }

        .header {
            text-align: center;
            margin-bottom: 50px;
            animation: fadeInDown 1s ease-out;
        }

        h1 {
            font-size: 32px;
            font-weight: 600;
            margin: 0;
            color: var(--accent);
        }

        p.subtitle {
            font-size: 16px;
            color: var(--text-secondary);
            margin-top: 10px;
            font-weight: 300;
        }

        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr); 
            gap: 20px;
            max-width: 600px;
            margin: 0 auto;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 20px;
            padding: 12px;
            box-shadow: var(--shadow);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            opacity: 0;
            transform: translateY(30px);
            animation: fadeInUp 0.8s forwards;
        }

        .card:nth-child(1) { animation-delay: 0.2s; }
        .card:nth-child(2) { animation-delay: 0.4s; }
        .card:nth-child(3) { animation-delay: 0.6s; }
        .card:nth-child(4) { animation-delay: 0.8s; }

        .card:active {
            transform: scale(0.95);
            box-shadow: 0 5px 15px rgba(180, 160, 165, 0.3);
        }

        .card img {
            width: 100%;
            aspect-ratio: 1 / 1; 
            object-fit: cover; 
            border-radius: 12px;
            background-color: #F0EBEB; /* Heller Platzhalter */
        }

        .card-content {
            padding: 15px 5px 5px 5px;
            text-align: center;
        }

        .card-title {
            font-size: 14px;
            font-weight: 600;
            margin: 0;
            color: var(--accent);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .card-desc {
            font-size: 13px;
            color: var(--text-secondary);
            margin-top: 6px;
            line-height: 1.4;
            font-weight: 300;
        }

        .footer {
            text-align: center;
            margin-top: 80px;
            margin-bottom: 40px;
            font-size: 14px;
            color: var(--text-secondary);
            font-weight: 300;
            line-height: 1.6;
            animation: fadeInUp 1s forwards;
            animation-delay: 1s;
            opacity: 0;
        }

        @keyframes fadeInDown {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

    </style>
</head>
<body>

    <canvas id="confetti"></canvas>

    <div class="header">
        <h1>Happy Birthday, [Ihr Name]</h1>
        <p class="subtitle">System-Update 18.0 erfolgreich installiert.<br>Hier ist unser Logbuch.</p>
    </div>

    <div class="gallery-grid">
        
        <div class="card">
            <img src="bild1.jpg" alt="Foto 1">
            <div class="card-content">
                <p class="card-title">Patch 1.0</p>
                <p class="card-desc">Das Modul "Erstes Date" wurde initialisiert. Wir waren beide extrem nervös.</p>
            </div>
        </div>

        <div class="card">
            <img src="bild2.jpg" alt="Foto 2">
            <div class="card-content">
                <p class="card-title">Bugfix #404</p>
                <p class="card-desc">Orientierungssinn temporär offline. Trotzdem angekommen.</p>
            </div>
        </div>

        <div class="card">
            <img src="bild3.jpg" alt="Foto 3">
            <div class="card-content">
                <p class="card-title">Feature Update</p>
                <p class="card-desc">Gemeinsamer Urlaub erfolgreich in die Datenbank geladen.</p>
            </div>
        </div>

        <div class="card">
            <img src="bild4.jpg" alt="Foto 4">
            <div class="card-content">
                <p class="card-title">Performance</p>
                <p class="card-desc">Läuft seit dem 25.03.2022 erstaunlich stabil. Bestes Release bisher.</p>
            </div>
        </div>

    </div>

    <div class="footer">
        Alles Gute zur 18! ❤️<br>
        Code & Design von Niklas
    </div>

    <script>
        const richtigePIN = "25.03.2022"; 
        const pin = prompt("System gesperrt. Bitte Freischalt-PIN (Datum) eingeben:");
        
        if (pin === richtigePIN) {
            document.body.style.display = "block";
            startHearts(); 
        } else {
            document.body.style.display = "block";
            // Fehlerbildschirm ist jetzt auch an das helle Design angepasst
            document.body.innerHTML = "<div style='display:flex; height:100vh; justify-content:center; align-items:center; flex-direction:column;'><h1 style='color:#C28A94; font-size:40px; margin:0;'>❌</h1><p style='color:#968D8F; font-family:sans-serif; margin-top:20px;'>Zugriff verweigert. Falsche PIN.</p></div>";
        }

        function startHearts() {
            const canvas = document.getElementById('confetti'); 
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            
            const particles = [];
            // Neue, romantische Herz-Farben (Altrosa, Zartrosa, Weiß)
            const colors = ['#e09fa8', '#c97a86', '#f2d3d7', '#ffffff']; 
            
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
            
            setTimeout(() => { 
                canvas.style.opacity = '0'; 
                canvas.style.transition = 'opacity 2.5s ease-out'; 
            }, 5000);
        }
    </script>
</body>
</html>
