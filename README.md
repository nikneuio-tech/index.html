<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="robots" content="noindex, nofollow">
    <title>Version 18.0 | Hannah</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;700&display=swap" rel="stylesheet">
    
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
            padding: 0;
            -webkit-font-smoothing: antialiased;
        }

        /* 1. SPERRBILDSCHIRM */
        #lock-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100vh;
            background-color: var(--bg-color); display: flex; flex-direction: column;
            justify-content: center; align-items: center; z-index: 3000;
            transition: opacity 1s ease-out;
        }
        .lock-icon { font-size: 40px; margin-bottom: 20px; }
        .pin-input {
            background: transparent; border: none; border-bottom: 2px solid var(--accent);
            font-size: 24px; text-align: center; color: var(--text-primary);
            margin: 20px 0; padding: 10px; width: 220px; outline: none; font-family: 'Outfit', sans-serif;
        }
        .pin-input::placeholder { color: #d6d0d1; font-size: 18px; }
        .unlock-btn {
            background-color: var(--accent); color: white; border: none; padding: 15px 40px;
            border-radius: 30px; font-size: 16px; font-weight: 600; cursor: pointer;
            box-shadow: 0 5px 15px rgba(194, 138, 148, 0.4); transition: transform 0.2s; font-family: 'Outfit', sans-serif;
        }
        .unlock-btn:active { transform: scale(0.95); }
        #error-msg { color: #ff4d4d; font-size: 14px; margin-top: 15px; opacity: 0; transition: opacity 0.3s; }

        /* 2. DER SÜSSE 16-SEKUNDEN LADE-SCREEN */
        #loading-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100vh;
            background-color: var(--bg-color); display: none; flex-direction: column;
            justify-content: center; align-items: center; z-index: 2000;
            transition: opacity 1.5s ease-out;
        }
        
        .beating-heart {
            font-size: 50px; color: #ff4d4d;
            animation: heartbeat 1.2s infinite; margin-bottom: 30px;
        }

        .loading-bar-container {
            width: 80%; max-width: 300px; height: 6px;
            background-color: #F0EBEB; border-radius: 3px; overflow: hidden;
            margin-bottom: 15px;
        }

        .loading-bar {
            height: 100%; width: 0%; background-color: var(--accent);
            transition: width 16s linear; /* Lädt exakt 16 Sekunden lang! */
        }
        
        .loading-text { font-size: 14px; color: var(--text-secondary); font-weight: 300; text-align: center; }

        @keyframes heartbeat {
            0% { transform: scale(1); }
            15% { transform: scale(1.3); }
            30% { transform: scale(1); }
            45% { transform: scale(1.15); }
            60% { transform: scale(1); }
        }

        /* 3. HAUPTINHALT (Wird bei Sekunde 16 sichtbar) */
        #main-content {
            display: none; padding: 40px 20px 80px 20px; max-width: 600px; margin: 0 auto;
        }

        #confetti { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 100; }

        .header { text-align: center; margin-bottom: 30px; animation: fadeInDown 1.5s ease-out; }
        h1 { font-size: 32px; font-weight: 600; margin: 0; color: var(--accent); }
        p.subtitle { font-size: 16px; color: var(--text-secondary); margin-top: 10px; font-weight: 300; }

        /* --- DIE AUTOMATISCHE COLLAGE --- */
        .collage-container {
            background-color: var(--card-bg); border-radius: 20px; padding: 15px;
            box-shadow: var(--shadow); position: relative; margin: 0 auto 50px auto;
            animation: fadeInUp 1.5s ease-out;
        }
        .image-frame { position: relative; width: 100%; aspect-ratio: 1 / 1; border-radius: 15px; overflow: hidden; background-color: #F0EBEB; }
        .collage-img { position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; opacity: 0; transition: opacity 1.5s ease-in-out, transform 6s ease-in-out; transform: scale(1); }
        .collage-img.active { opacity: 1; transform: scale(1.05); }
        .text-frame { text-align: center; padding: 20px 10px 10px 10px; min-height: 70px; }
        .collage-title { font-size: 16px; font-weight: 600; color: var(--accent); margin: 0; text-transform: uppercase; letter-spacing: 1px; transition: opacity 0.5s;}
        .collage-desc { font-size: 14px; color: var(--text-secondary); margin-top: 8px; line-height: 1.5; font-weight: 300; transition: opacity 0.5s;}

        /* --- DIE 4 FESTEN KACHELN --- */
        .gallery-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; max-width: 600px; margin: 0 auto; }
        .card { background-color: var(--card-bg); border-radius: 20px; padding: 12px; box-shadow: var(--shadow); opacity: 0; transform: translateY(30px); animation: fadeInUp 0.8s forwards; animation-delay: 1s; }
        .card img { width: 100%; aspect-ratio: 1 / 1; object-fit: cover; border-radius: 12px; background-color: #F0EBEB; }
        .card-content { padding: 15px 5px 5px 5px; text-align: center; }
        .card-title { font-size: 14px; font-weight: 600; margin: 0; color: var(--accent); text-transform: uppercase; letter-spacing: 1px; }
        .card-desc { font-size: 13px; color: var(--text-secondary); margin-top: 6px; line-height: 1.4; font-weight: 300; }

        /* --- INTERAKTIVER BEREICH --- */
        .interactive-section { text-align: center; margin-top: 50px; opacity: 0; animation: fadeInUp 1s forwards; animation-delay: 1.5s;}
        .action-btn { background-color: white; color: var(--text-primary); border: 2px solid var(--accent); padding: 15px 30px; border-radius: 25px; font-family: 'Outfit', sans-serif; font-weight: 600; font-size: 16px; cursor: pointer; margin: 10px; width: 90%; max-width: 300px; transition: all 0.3s; }
        .action-btn:hover { background-color: var(--accent); color: white; }
        #generator-result { margin: 20px auto; width: 90%; transition: all 0.5s ease; }
        #secret-box { background-color: var(--card-bg); border-radius: 20px; padding: 25px; box-shadow: var(--shadow); margin-top: 20px; font-size: 15px; line-height: 1.6; color: var(--text-primary); display: none; border-left: 5px solid var(--accent); text-align: left; }

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
        <div class="loading-bar-container">
            <div class="loading-bar" id="load-bar"></div>
        </div>
        <p class="loading-text" id="load-text">Entschlüssele Erinnerungen... (0%)</p>
    </div>

    <audio id="bg-music">
        <source src="song.mp3" type="audio/mpeg">
    </audio>

    <div id="main-content">
        <canvas id="confetti"></canvas>

        <div class="header">
            <h1>Happy Birthday, Hannah</h1>
            <p class="subtitle">System-Update 18.0 erfolgreich installiert.<br>Hier ist unser Logbuch.</p>
        </div>

        <div class="collage-container">
            <div class="image-frame">
                <img src="bild1.jpeg" class="collage-img active" id="img-0">
                <img src="bild2.jpeg" class="collage-img" id="img-1">
                <img src="bild3.jpeg" class="collage-img" id="img-2">
                <img src="bild4.jpeg" class="collage-img" id="img-3">
            </div>
            <div class="text-frame">
                <p class="collage-title" id="c-title">Patch 1.0</p>
                <p class="collage-desc" id="c-desc">Das Modul "Erstes Date" wurde initialisiert. Wir waren beide extrem nervös.</p>
            </div>
        </div>

        <div class="gallery-grid">
            <div class="card"><img src="bild1.jpeg" alt="Foto 1"><div class="card-content"><p class="card-title">Memory #1</p><p class="card-desc">Insider oder kurzer Text.</p></div></div>
            <div class="card"><img src="bild2.jpeg" alt="Foto 2"><div class="card-content"><p class="card-title">Memory #2</p><p class="card-desc">Orientierungssinn temporär offline.</p></div></div>
            <div class="card"><img src="bild3.jpeg" alt="Foto 3"><div class="card-content"><p class="card-title">Memory #3</p><p class="card-desc">Gemeinsamer Urlaub erfolgreich geladen.</p></div></div>
            <div class="card"><img src="bild4.jpeg" alt="Foto 4"><div class="card-content"><p class="card-title">Memory #4</p><p class="card-desc">Läuft erstaunlich stabil.</p></div></div>
        </div>

        <div class="interactive-section">
            <button class="action-btn" onclick="startGenerator()" id="gen-btn">🎁 Geschenk-Datenbank hacken</button>
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
    </div>

    <script>
        const richtigePIN = "25.03.2022"; 

        function checkPIN() {
            const input = document.getElementById("pin-input").value;
            const errorMsg = document.getElementById("error-msg");
            
            if (input === richtigePIN) {
                // PIN richtig!
                errorMsg.style.opacity = "0";
                
                // 1. Sperrbildschirm weg, Ladescreen an!
                document.getElementById("lock-screen").style.opacity = "0";
                setTimeout(() => {
                    document.getElementById("lock-screen").style.display = "none";
                    document.getElementById("loading-screen").style.display = "flex";
                }, 800);

                // 2. MUSIK STARTEN (Intro läuft ab Sekunde 0)
                try {
                    const music = document.getElementById("bg-music");
                    music.currentTime = 0; 
                    music.play();
                } catch(err) { console.log("Audio konnte nicht gestartet werden."); }

                // 3. LADEBALKEN & TEXT STARTEN (Dauert exakt 16 Sekunden)
                setTimeout(() => {
                    document.getElementById("load-bar").style.width = "100%";
                    
                    // Kleine Texte, die sich während der 16 Sekunden ändern
                    const loadText = document.getElementById("load-text");
                    setTimeout(() => { loadText.innerText = "Lade gemeinsame Momente... (24%)"; }, 4000);
                    setTimeout(() => { loadText.innerText = "Umgehe Cringe-Filter... (68%)"; }, 8000);
                    setTimeout(() => { loadText.innerText = "Bereite System-Upgrade vor... (99%)"; }, 12000);

                    // NACH EXAKT 16 SEKUNDEN: BEAT DROP!
                    setTimeout(() => {
                        document.getElementById("loading-screen").style.opacity = "0";
                        setTimeout(() => {
                            document.getElementById("loading-screen").style.display = "none";
                            document.getElementById("main-content").style.display = "block";
                            startHearts();
                            startCollage(); 
                        }, 1000); // 1 Sekunde für den sanften Übergang
                    }, 16000); // 16.000 Millisekunden = 16 Sekunden!

                }, 1000);

            } else {
                errorMsg.style.opacity = "1";
            }
        }

        // --- DIE AUTOMATISCHE COLLAGE ---
        const memories = [
            { title: "Patch 1.0", desc: "Das Modul 'Erstes Date' wurde initialisiert. Wir waren beide extrem nervös." },
            { title: "Bugfix #404", desc: "Orientierungssinn temporär offline. Trotzdem angekommen." },
            { title: "Feature Update", desc: "Gemeinsamer Urlaub erfolgreich in die Datenbank geladen." },
            { title: "Performance", desc: "Läuft seit dem 25.03.2022 erstaunlich stabil. Bestes Release bisher." }
        ];
        let currentSlide = 0;

        function startCollage() {
            setInterval(() => {
                document.getElementById("img-" + currentSlide).classList.remove("active");
                currentSlide = (currentSlide + 1) % memories.length;
                document.getElementById("img-" + currentSlide).classList.add("active");
                
                const titleEl = document.getElementById("c-title");
                const descEl = document.getElementById("c-desc");
                titleEl.style.opacity = 0; descEl.style.opacity = 0;
                
                setTimeout(() => {
                    titleEl.innerText = memories[currentSlide].title;
                    descEl.innerText = memories[currentSlide].desc;
                    titleEl.style.opacity = 1; descEl.style.opacity = 1;
                }, 400);
            }, 4500); 
        }

        // --- GESCHENK-GENERATOR ---
        function startGenerator() {
            const resultBox = document.getElementById("generator-result");
            document.getElementById("gen-btn").style.display = "none"; 
            
            resultBox.style.backgroundColor = "#1D1D1F"; resultBox.style.color = "#34C759";
            resultBox.style.padding = "20px"; resultBox.style.borderRadius = "12px";
            resultBox.style.fontFamily = "monospace"; resultBox.style.textAlign = "left";
            resultBox.style.fontSize = "14px"; resultBox.style.boxShadow = "0 10px 30px rgba(0,0,0,0.5)";

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
                    resultBox.style.backgroundColor = "var(--card-bg)"; resultBox.style.border = "2px solid var(--accent)";
                    resultBox.style.textAlign = "center"; resultBox.style.color = "var(--text-primary)"; resultBox.style.fontFamily = "'Outfit', sans-serif";
                    
                    resultBox.innerHTML = "<span style='font-size:12px; color:var(--text-secondary); text-transform:uppercase;'>System-Upgrade gefunden</span><br><br><span style='font-size:24px; font-weight:700; color:var(--accent); line-height:1.2;'>Ein Pandora-Anhänger für dein Armband 💍✨</span>";
                    startHearts(); 
                }, 3500);
            }, 6000); 
        }

        // --- TOP SECRET BRIEF ---
        function toggleSecret() {
            const box = document.getElementById("secret-box");
            box.style.display = (box.style.display === "none" || box.style.display === "") ? "block" : "none";
        }

        // --- HERZ-ANIMATION ---
        function startHearts() {
            const canvas = document.getElementById('confetti'); const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth; canvas.height = window.innerHeight;
            const particles = []; const colors = ['#ff0000', '#cc0000', '#e60000', '#ff4d4d']; 
            
            for(let i=0; i<60; i++) { 
                particles.push({
                    x: Math.random() * canvas.width, y: Math.random() * canvas.height - canvas.height,
                    size: Math.random() * 15 + 15, color: colors[Math.floor(Math.random() * colors.length)],
                    speedY: Math.random() * 2 + 1.5, speedX: Math.random() * 1 - 0.5
                });
            }

            function draw() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                for(let p of particles) {
                    ctx.font = p.size + "px Arial"; ctx.fillStyle = p.color; ctx.fillText("❤", p.x, p.y); 
                    p.y += p.speedY; p.x += p.speedX;
                    if(p.y > canvas.height + 50) { p.y = -50; p.x = Math.random() * canvas.width; }
                }
                requestAnimationFrame(draw);
            }
            draw();
            setTimeout(() => { canvas.style.opacity = '0'; canvas.style.transition = 'opacity 2.5s ease-out'; }, 5000);
        }
    </script>
</body>
</html>
