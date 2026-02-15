<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="robots" content="noindex, nofollow">
    
   <title>Version 18.0 | Archiv</title>
    
   <style>
        :root {
            --bg-color: #F5F5F7;
            --card-bg: #FFFFFF;
            --text-primary: #1D1D1F;
            --text-secondary: #86868B;
            --shadow: 0 4px 20px rgba(0,0,0,0.06);
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Helvetica Neue", Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-primary);
            margin: 0;
            padding: 20px;
            padding-top: 60px;
            -webkit-font-smoothing: antialiased;
            /* Versteckt die Seite anfangs, bis die PIN eingegeben wurde */
            visibility: hidden; 
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }

        h1 {
            font-size: 28px;
            font-weight: 700;
            margin: 0;
            letter-spacing: -0.5px;
        }

        p.subtitle {
            font-size: 15px;
            color: var(--text-secondary);
            margin-top: 8px;
        }

        /* Das Galerie-Raster */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr); 
            gap: 15px;
            max-width: 500px;
            margin: 0 auto;
        }

        /* Einzelne Karte */
        .card {
            background-color: var(--card-bg);
            border-radius: 16px;
            padding: 10px;
            box-shadow: var(--shadow);
            transition: transform 0.2s;
        }

        .card:active {
            transform: scale(0.96);
        }

        /* Das Bild in der Karte */
        .card img {
            width: 100%;
            aspect-ratio: 1 / 1; 
            object-fit: cover; 
            border-radius: 10px;
            background-color: #E5E5EA; 
        }

        .card-content {
            padding: 10px 4px 4px 4px;
        }

        .card-title {
            font-size: 13px;
            font-weight: 600;
            margin: 0;
        }

        .card-desc {
            font-size: 11px;
            color: var(--text-secondary);
            margin-top: 4px;
            line-height: 1.3;
        }

        /* Footer / Glückwunsch */
        .footer {
            text-align: center;
            margin-top: 60px;
            margin-bottom: 40px;
            font-size: 14px;
            color: var(--text-secondary);
            font-weight: 500;
            line-height: 1.5;
        }

    </style>
</head>
<body>

   <div class="header">
        <h1>Das Hannah-Archiv</h1>
        <p class="subtitle">Beweisstücke aus 18 Jahren Systemlaufzeit.</p>
    </div>

  <div class="gallery-grid">        
        <div class="card">
            <img src="bild1.jpg" alt="Erstes Date">
            <div class="card-content">
                <p class="card-title">Beweisstück A</p>
                <p class="card-desc">Der Tag, an dem wir fast den Zug verpasst haben.</p>
            </div>
        </div>
    <div class="card">
            <img src="bild2.jpg" alt="Insider">
            <div class="card-content">
                <p class="card-title">Fehler 404</p>
                <p class="card-desc">Orientierungssinn an diesem Tag nicht gefunden.</p>
            </div>
        </div>
        <div class="card">
            <img src="bild3.jpg" alt="Party">
            <div class="card-content">
                <p class="card-title">Bugfix #12</p>
                <p class="card-desc">Snacks nach 20 Uhr verhindern Hangry-Modus erfolgreich.</p>
            </div>
        </div>
        <div class="card">
            <img src="bild4.jpg" alt="Urlaub">
            <div class="card-content">
                <p class="card-title">System-Update</p>
                <p class="card-desc">Bester Urlaub bisher. Keine Abstürze gemeldet.</p>
            </div>
        </div>
        </div>
    <div class="footer">
        Version 18.0 erfolgreich installiert.<br>
        Happy Birthday! 🤍<br><br>
        (Entwickelt von [Dein Name])
    </div>

   <script>
        // Euer Jahrestag als PIN
        let richtigePIN = "25.03.2022"; 
        let pin = prompt("System gesperrt. Bitte Freischalt-PIN eingeben:");
        
        if (pin === richtigePIN) {
            // PIN ist richtig -> Seite wird sichtbar
            document.body.style.visibility = "visible";
        } else {
            // PIN ist falsch -> Rotes X und Fehlertext
            document.body.style.visibility = "visible";
            document.body.innerHTML = "<h1 style='text-align:center; margin-top:100px; color:#FF3B30;'>❌ Zugriff verweigert.</h1><p style='text-align:center; color:#86868B;'>Falsche PIN eingegeben. Seite neu laden, um es nochmal zu versuchen.</p>";
        }
    </script>

</body>
</html>
