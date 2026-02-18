<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="robots" content="noindex, nofollow">
    <title>Version 18.0 | Hannah</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;700&family=Fira+Code:wght@400;500&family=Permanent+Marker&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-color: #FAF5F5; 
            --card-bg: #FFFFFF; 
            --text-primary: #3A3335; 
            --text-secondary: #968D8F; 
            --accent: #C28A94; 
            --shadow: 0 15px 35px rgba(180, 160, 165, 0.25);
            --terminal-green: #34C759;
        }

        body {
            font-family: 'Outfit', sans-serif; background-color: var(--bg-color);
            color: var(--text-primary); margin: 0; padding: 0;
            -webkit-font-smoothing: antialiased; overflow-x: hidden;
            overscroll-behavior-y: none;
        }

        /* --- SPERRBILDSCHIRM --- */
        #lock-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100vh;
            background-color: var(--bg-color); display: flex; flex-direction: column;
            justify-content: center; align-items: center; z-index: 3000; transition: opacity 1s ease-out;
        }
        .lock-icon { font-size: 40px; margin-bottom: 20px; text-shadow: 0 0 15px rgba(194, 138, 148, 0.5); }
        .pin-input {
            background: transparent; border: none; border-bottom: 2px solid var(--accent);
            font-size: 24px; text-align: center; color: var(--text-primary);
            margin: 20px 0; padding: 10px; width: 220px; outline: none; font-family: 'Outfit', sans-serif;
            transition: border-color 0.3s;
        }
        .pin-input:focus { border-bottom: 2px solid #3A3335; }
        .pin-input::placeholder { color: #d6d0d1; font-size: 18px; }
        .unlock-btn {
            background-color: var(--accent); color: white; border: none; padding: 15px 40px;
            border-radius: 30px; font-size: 16px; font-weight: 600; cursor: pointer;
            box-shadow: 0 5px 20px rgba(194, 138, 148, 0.5); transition: all 0.2s; font-family: 'Outfit', sans-serif;
        }
        .unlock-btn:active { transform: scale(0.92); box-shadow: 0 2px 10px rgba(194, 138, 148, 0.5); }
        #error-msg { color: #ff4d4d; font-size: 14px; margin-top: 15px; opacity: 0; transition: opacity 0.3s; }

        /* --- LADE-SCREEN --- */
        #loading-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100vh;
            background-color: var(--bg-color); display: none; flex-direction: column;
            justify-content: center; align-items: center; z-index: 2000; transition: opacity 1.5s ease-out;
        }
        .beating-heart { font-size: 50px; color: #ff4d4d; animation: heartbeat 1.2s infinite; margin-bottom: 30px; text-shadow: 0 0 20px rgba(255, 77, 77, 0.6); }
        .loading-bar-container { width: 80%; max-width: 300px; height: 6px; background-color: #F0EBEB; border-radius: 3px; overflow: hidden; margin-bottom: 15px; }
        .loading-bar { height: 100%; width: 0%; background-color: var(--accent); transition: width 16s linear; box-shadow: 0 0 10px var(--accent); }
        .loading-text { font-size: 14px; color: var(--text-secondary); font-weight: 300; text-align: center; }
        @keyframes heartbeat { 0% { transform: scale(1); } 15% { transform: scale(1.3); } 30% { transform: scale(1); } 45% { transform: scale(1.15); } 60% { transform: scale(1); } }

        /* --- HAUPTINHALT --- */
        #main-content { display: none; padding: 40px 20px 80px 20px; max-width: 600px; margin: 0 auto; transition: opacity 1s ease-out; }
        
        .header { text-align: center; margin-bottom: 40px; animation: fadeInDown 1.5s ease-out; }
        h1 { font-size: 32px; font-weight: 700; margin: 0; color: var(--accent); }
        p.subtitle { font-size: 16px; color: var(--text-secondary); margin-top: 10px; font-weight: 300; }

        /* --- SCRAPBOOK & GALERIE --- */
        .scrapbook-container { position: relative; width: 100%; max-width: 400px; height: 450px; margin: 0 auto 60px auto; }
        .scrap-item { position: absolute; width: 55%; background: var(--card-bg); padding: 10px 10px 30px 10px; border-radius: 4px; box-shadow: 0 15px 30px rgba(0,0,0,0.2); opacity: 0; transform: translateY(-150px) scale(1.2) rotate(0deg); transition: all 0.6s cubic-bezier(0.34, 1.56, 0.64, 1); }
        .scrap-item img { width: 100%; aspect-ratio: 1 / 1; object-fit: cover; border-radius: 2px; background-color: #F0EBEB; }
        .scrap-text { font-family: 'Permanent Marker', cursive; font-size: 14px; color: var(--text-primary); text-align: center; margin-top: 12px; transform: rotate(-2deg); }
        .scrap-item:nth-child(1).dropped { opacity: 1; top: 0%; left: 0%; transform: rotate(-8deg); z-index: 1; }
        .scrap-item:nth-child(2).dropped { opacity: 1; top: 12%; right: 0%; transform: rotate(12deg); z-index: 2; }
        .scrap-item:nth-child(3).dropped { opacity: 1; top: 40%; left: 5%; transform: rotate(-5deg); z-index: 3; }
        .scrap-item:nth-child(4).dropped { opacity: 1; top: 52%; right: 8%; transform: rotate(7deg); z-index: 4; }
        
        .gallery-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; max-width: 600px; margin: 0 auto; }
        .card { background-color: var(--card-bg); border-radius: 20px; padding: 12px; box-shadow: var(--shadow); opacity: 0; transform: translateY(30px); animation: fadeInUp 0.8s forwards; animation-delay: 2.5s; transition: transform 0.3s, box-shadow 0.3s; }
        .card:active { transform: scale(0.95); box-shadow: 0 5px 15px rgba(0,0,0,0.1); }
        .card img { width: 100%; aspect-ratio: 1 / 1; object-fit: cover; border-radius: 12px; background-color: #F0EBEB; }
        .card-content { padding: 15px 5px 5px 5px; text-align: center; }
        .card-title { font-size: 14px; font-weight: 600; margin: 0; color: var(--accent); text-transform: uppercase; letter-spacing: 1px; }
        .card-desc { font-size: 13px; color: var(--text-secondary); margin-top: 6px; line-height: 1.4; font-weight: 300; }
        
        .interactive-section { text-align: center; margin-top: 50px; opacity: 0; animation: fadeInUp 1s forwards; animation-delay: 3s;}
        .action-btn { background-color: white; color: var(--text-primary); border: 2px solid var(--accent); padding: 15px 30px; border-radius: 25px; font-family: 'Outfit', sans-serif; font-weight: 600; font-size: 16px; cursor: pointer; margin: 10px; width: 90%; max-width: 300px; transition: all 0.3s; box-shadow: 0 4px 15px rgba(194, 138, 148, 0.2); }
        .action-btn:active { transform: scale(0.92); }
        .action-btn:hover { background-color: var(--accent); color: white; }
        #generator-result { margin: 20px auto; width: 90%; transition: all 0.5s ease; }

        /* --- DER KINO-TERMINAL --- */
        #terminal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: #050505; z-index: 4000;
            display: none; flex-direction: column; justify-content: center; align-items: center;
            padding: 30px; box-sizing: border-box; opacity: 0; transition: opacity 1s ease-in;
        }
        #typing-container {
            font-family: 'Fira Code', monospace; color: var(--terminal-green); font-size: 15px; line-height: 1.6;
            white-space: pre-wrap; width: 100%; max-width: 500px; text-align: left;
            text-shadow: 0 0 5px rgba(52, 199, 89, 0.5);
        }
        .cursor { display: inline-block; width: 10px; height: 18px; background-color: var(--terminal-green); margin-left: 5px; animation: blink 1s infinite; box-shadow: 0 0 8px var(--terminal-green); }
        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

        /* --- SCREEN SHAKE FÜR DEN BEAT DROP (Hier ist deine #2) --- */
        .screen-shake { animation: shake 0.4s cubic-bezier(.36,.07,.19,.97) both; }
        @keyframes shake { 10%, 90% { transform: translate3d(-2px, 2px, 0); } 20%, 80% { transform: translate3d(3px, -2px, 0); } 30%, 50%, 70% { transform: translate3d(-4px, 4px, 0); } 40%, 60% { transform: translate3d(4px, -4px, 0); } }

        /* Der Kamera-Blitz */
        #flash-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: white; z-index: 5000; opacity: 0; pointer-events: none; transition: opacity 1s ease-out; display: none; }

        /* Das "Ich liebe dich" am Ende */
        #final-message {
            position: absolute; font-family: 'Outfit', sans-serif; color: white; text-align: center; width: 100%;
            font-size: 38px; font-weight: 700; opacity: 0; transform: scale(0.8);
            text-shadow: 0 0 30px rgba(255, 50, 50, 0.8), 0 0 60px rgba(255, 50, 50, 0.5);
            transition: all 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275); display: none; line-height: 1.2;
        }
        #final-message span { font-size: 20px; font-weight: 400; color: #ffebba; display: block; margin-top: 15px; }

        #confetti { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 4500; }

        @keyframes fadeInDown { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="lock-screen">
        <div class="lock-icon">🔒</div>
        <h2 style="color: var(--text-primary); margin: 0;">System gesperrt</h2>
        <p style="color: var(--text-secondary); margin-top: 5px;">Bitte Freischalt-PIN eingeben:</p>
        <input type="text" id="pin-input" class="pin-input" placeholder="TT.MM.JJJJ">
        <button class="unlock-btn" onclick="checkPIN()">System entsperren</button>
        <p id="error-msg">Zugriff verweigert. Falsches Datum.</p>
    </div>

    <div id="loading-screen">
        <div class="beating-heart">❤</div>
        <div class="loading-bar-container"><div class="loading-bar" id="load-bar"></div></div>
        <p class="loading-text" id="load-text">Entschlüssele Erinnerungen... (0%)</p>
    </div>

    <audio id="bg-music">
        <source src="song.mp3" type="audio/mpeg">
        <source src="song.m4a" type="audio/mp4">
    </audio>

    <div id="main-content">
        <div class="header">
            <h1>Happy Birthday, Hannah</h1>
            <p class="subtitle">System-Update 18.0 erfolgreich installiert.<br>Hier ist unser Logbuch.</p>
        </div>

        <div class="scrapbook-container" id="scrapbook">
            <div class="scrap-item"><img src="bild1.jpeg" alt=""><div class="scrap-text">Patch 1.0</div></div>
            <div class="scrap-item"><img src="bild2.jpeg" alt=""><div class="scrap-text">Error 404</div></div>
            <div class="scrap-item"><img src="bild3.jpeg" alt=""><div class="scrap-text">Update geladen</div></div>
            <div class="scrap-item"><img src="bild4.jpeg" alt=""><div class="scrap-text">Seit 2022</div></div>
        </div>

        <div class="gallery-grid">
            <div class="card"><img src="bild1.jpeg" alt="Foto 1"><div class="card-content"><p class="card-title">Memory #1</p><p class="card-desc">Das Modul "Erstes Date" wurde initialisiert. Wir waren beide extrem nervös.</p></div></div>
            <div class="card"><img src="bild2.jpeg" alt="Foto 2"><div class="card-content"><p class="card-title">Memory #2</p><p class="card-desc">Orientierungssinn temporär offline. Trotzdem angekommen.</p></div></div>
            <div class="card"><img src="bild3.jpeg" alt="Foto 3"><div class="card-content"><p class="card-title">Memory #3</p><p class="card-desc">Gemeinsamer Urlaub erfolgreich in die Datenbank geladen.</p></div></div>
            <div class="card"><img src="bild4.jpeg" alt="Foto 4"><div class="card-content"><p class="card-title">Memory #4</p><p class="card-desc">Läuft erstaunlich stabil. Bestes Release bisher.</p></div></div>
        </div>

        <div class="interactive-section">
            <button class="action-btn" onclick="startGenerator()" id="gen-btn">🎁 Geschenk-Datenbank hacken</button>
            <div id="generator-result"></div>
            <button class="action-btn" onclick="startCinematicFinale()">✉️ System-Admin Nachricht</button>
        </div>
    </div>

    <div id="terminal-overlay">
        <div id="typing-container"></div><div class="cursor" id="cursor"></div>
        <div id="final-message">Happy Birthday.<br>Ich liebe dich.<span>Dein Niklas</span></div>
    </div>
    
    <div id="flash-overlay"></div>
    <canvas id="confetti"></canvas>

    <script>
        const richtigePIN = "25.03.2022"; 

        // TIMING FÜR DEN SONG
        const buildUpStartSekunde = 61; 

        function checkPIN() {
            const input = document.getElementById("pin-input").value;
            const errorMsg = document.getElementById("error-msg");
            if (input === richtigePIN) {
                errorMsg.style.opacity = "0";
                document.getElementById("lock-screen").style.opacity = "0";
                setTimeout(() => {
                    document.getElementById("lock-screen").style.display = "none";
                    document.getElementById("loading-screen").style.display = "flex";
                }, 800);
                try { const music = document.getElementById("bg-music"); music.currentTime = 0; music.volume = 1.0; music.play(); } catch(err) {}
                setTimeout(() => {
                    document.getElementById("load-bar").style.width = "100%";
                    const loadText = document.getElementById("load-text");
                    setTimeout(() => { loadText.innerText = "Lade gemeinsame Momente... (24%)"; }, 4000);
                    setTimeout(() => { loadText.innerText = "Umgehe Cringe-Filter... (68%)"; }, 8000);
                    setTimeout(() => { loadText.innerText = "Bereite System-Upgrade vor... (99%)"; }, 12000);
                    setTimeout(() => {
                        document.getElementById("loading-screen").style.opacity = "0";
                        setTimeout(() => {
                            document.getElementById("loading-screen").style.display = "none";
                            document.getElementById("main-content").style.display = "block";
                            startNormalHearts(); 
                            const scraps = document.querySelectorAll('.scrap-item');
                            scraps.forEach((scrap, index) => { setTimeout(() => { scrap.classList.add('dropped'); }, index * 400); });
                        }, 1000); 
                    }, 16000); 
                }, 1000);
            } else { errorMsg.style.opacity = "1"; }
        }

        // --- DAS KINOREIFE FINALE (BEAT-SYNC) ---
        function startCinematicFinale() {
            const overlay = document.getElementById('terminal-overlay');
            const mainContent = document.getElementById('main-content');
            const music = document.getElementById("bg-music");
            const typingContainer = document.getElementById('typing-container');
            
            // 1. Alles wird schwarz
            overlay.style.display = 'flex';
            setTimeout(() => { 
                overlay.style.opacity = '1'; 
                mainContent.style.opacity = '0';
                
                music.volume = 0;
                music.currentTime = buildUpStartSekunde; 
                let vol = 0;
                let fadeIn = setInterval(() => { if (vol < 1.0) { vol += 0.1; music.volume = vol.toFixed(1); } else { clearInterval(fadeIn); } }, 100);
            }, 100);

            // 3. TEXT-SYNCHRONISATION 
            setTimeout(() => { typingContainer.innerHTML += "> Initialisiere Admin-Nachricht...\n"; }, 1500);
            setTimeout(() => { typingContainer.innerHTML += "> Empfänger: Hannah\n"; }, 3500);
            setTimeout(() => { typingContainer.innerHTML += "> Absender: Niklas (SysAdmin)\n\n"; }, 5000);
            
            setTimeout(() => { typingContainer.innerHTML += "Hey Hannah,\n\n"; }, 7000);
            setTimeout(() => { typingContainer.innerHTML += "ich bin absolut nicht der Typ für kitschige Romane oder Liebesbriefe.\n"; }, 9000);
            setTimeout(() => { typingContainer.innerHTML += "Aber ich wollte dir trotzdem etwas schenken, das zeigt, wie wichtig du mir bist.\n"; }, 12500);
            setTimeout(() => { typingContainer.innerHTML += "Danke für die geile Zeit seit 2022.\n\n"; }, 15500);
            
            setTimeout(() => { typingContainer.innerHTML += "> System Overload in 3... 2... 1..."; }, 17000);

            // 4. DER MEGA BOOM (MIT SCREEN SHAKE)
            setTimeout(() => {
                // Kamera-Blitz
                const flash = document.getElementById('flash-overlay');
                flash.style.display = 'block';
                flash.style.opacity = '1';
                
                // HIER PASSIERT DAS BEBEN (#2)
                document.body.classList.add('screen-shake');
                
                // Terminal Text weg
                typingContainer.style.display = 'none'; 
                document.getElementById('cursor').style.display = 'none';

                // Supernova Explosion
                startSupernova();

                // Blitz blendet weich aus, Nachricht erscheint riesig
                setTimeout(() => {
                    flash.style.opacity = '0';
                    const finalMsg = document.getElementById('final-message');
                    finalMsg.style.display = 'block';
                    setTimeout(() => { 
                        finalMsg.style.opacity = '1'; 
                        finalMsg.style.transform = 'scale(1)'; 
                    }, 50);
                }, 100);

            }, 18000); 
        }

        // --- GESCHENK-GENERATOR ---
        function startGenerator() {
            const resultBox = document.getElementById("generator-result");
            document.getElementById("gen-btn").style.display = "none"; 
            resultBox.style.backgroundColor = "#1D1D1F"; resultBox.style.color = "#34C759"; resultBox.style.padding = "20px"; resultBox.style.borderRadius = "12px"; resultBox.style.fontFamily = "monospace"; resultBox.style.textAlign = "left"; resultBox.style.fontSize = "14px"; resultBox.style.boxShadow = "0 10px 30px rgba(0,0,0,0.5)";
            resultBox.innerHTML = "> Initiiere Geschenk-Protokoll...<br>";
            setTimeout(() => { resultBox.innerHTML += "> Umgehe Firewall...<br>"; }, 1200);
            setTimeout(() => { resultBox.innerHTML += "> Scanne Datenbank nach Loot...<br>"; }, 2400);
            setTimeout(() => { resultBox.innerHTML += "> <span style='color:#FF3B30;'>WARNUNG:</span> Option 'Socken' blockiert.<br>"; }, 3800);
            setTimeout(() => { resultBox.innerHTML += "> Starte Premium-Lootbox-Entschlüsselung:<br><br>"; }, 5000);
            setTimeout(() => {
                const fakeGifts = ["Gutschein für Abwasch", "Nichts", "Ein gebrauchter Kaugummi", "1x Recht haben"];
                let i = 0; let slotText = document.createElement("span");
                slotText.style.color = "white"; slotText.style.backgroundColor = "black"; slotText.style.padding = "2px 5px";
                resultBox.appendChild(slotText);
                let interval = setInterval(() => { slotText.innerText = " " + fakeGifts[i % fakeGifts.length] + " %X&@!"; i++; }, 100); 
                setTimeout(() => {
                    clearInterval(interval);
                    resultBox.style.backgroundColor = "var(--card-bg)"; resultBox.style.border = "2px solid var(--accent)"; resultBox.style.textAlign = "center"; resultBox.style.color = "var(--text-primary)"; resultBox.style.fontFamily = "'Outfit', sans-serif";
                    resultBox.innerHTML = "<span style='font-size:12px; color:var(--text-secondary); text-transform:uppercase;'>System-Upgrade gefunden</span><br><br><span style='font-size:24px; font-weight:700; color:var(--accent); line-height:1.2;'>Ein Pandora-Anhänger für dein Armband 💍✨</span>";
                    startNormalHearts(); 
                }, 3500);
            }, 6000); 
        }

        // Normale kleine Herzen
        function startNormalHearts() {
            const canvas = document.getElementById('confetti'); const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth; canvas.height = window.innerHeight;
            const particles = []; const colors = ['#ff0000', '#cc0000', '#e60000']; 
            for(let i=0; i<40; i++) { particles.push({ x: Math.random() * canvas.width, y: Math.random() * canvas.height - canvas.height, size: Math.random() * 15 + 10, color: colors[Math.floor(Math.random() * colors.length)], speedY: Math.random() * 2 + 1.5, speedX: Math.random() * 1 - 0.5 }); }
            function draw() { ctx.clearRect(0, 0, canvas.width, canvas.height); for(let p of particles) { ctx.font = p.size + "px Arial"; ctx.fillStyle = p.color; ctx.fillText("❤", p.x, p.y); p.y += p.speedY; p.x += p.speedX; if(p.y > canvas.height + 50) { p.y = -50; p.x = Math.random() * canvas.width; } } requestAnimationFrame(draw); }
            draw(); setTimeout(() => { canvas.style.opacity = '0'; canvas.style.transition = 'opacity 2.5s ease-out'; setTimeout(() => { ctx.clearRect(0,0, canvas.width, canvas.height); canvas.style.opacity = '1'; }, 2500); }, 4000);
        }

        // --- DIE MASSIVE SUPERNOVA ---
        function startSupernova() {
            const canvas = document.getElementById('confetti'); 
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth; canvas.height = window.innerHeight;
            
            const particles = [];
            const colors = ['#ff0000', '#ff4d4d', '#ffebba', '#d4af37', '#ffffff']; 
            
            for(let i=0; i<250; i++) { 
                const angle = Math.random() * Math.PI * 2;
                const speed = Math.random() * 18 + 5; 
                particles.push({
                    x: canvas.width / 2, y: canvas.height / 2,
                    size: Math.random() * 30 + 10, 
                    color: colors[Math.floor(Math.random() * colors.length)],
                    speedX: Math.cos(angle) * speed, speedY: Math.sin(angle) * speed,
                    gravity: 0.25, life: 1.0 
                });
            }

            function draw() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                let alive = false;
                
                for(let p of particles) {
                    if (p.life > 0) {
                        alive = true;
                        ctx.globalAlpha = p.life;
                        ctx.font = p.size + "px Arial"; ctx.fillStyle = p.color; 
                        
                        if(Math.random() > 0.4) { ctx.fillText("❤", p.x, p.y); } 
                        else { ctx.beginPath(); ctx.arc(p.x, p.y, p.size/3, 0, Math.PI*2); ctx.fill(); }
                        
                        p.x += p.speedX; p.y += p.speedY;
                        p.speedY += p.gravity; 
                        p.life -= 0.006; 
                    }
                }
                if(alive) { requestAnimationFrame(draw); } 
                else { ctx.globalAlpha = 1.0; } 
            }
            draw();
        }
    </script>
</body>
</html>
