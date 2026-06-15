<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Premium Flohmarkt - Privatverkauf</title>
    <style>
        /* Modernes CSS Reset & Variablen */
        :root {
            --bg-color: #0f172a;
            --card-bg: #ffffff;
            --text-main: #1e293b;
            --text-muted: #64748b;
            --accent-color: #3b82f6;
            --price-color: #ef4444;
            --success-color: #10b981;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            line-height: 1.6;
            padding: 40px 20px;
        }

        /* Header */
        header {
            text-align: center;
            padding: 40px 20px;
            background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            margin-bottom: 40px;
            border: 1px solid #334155;
        }

        header h1 {
            color: #ffffff;
            font-size: 32px;
            font-weight: 800;
            letter-spacing: -0.5px;
            margin-bottom: 12px;
        }

        .info-badge {
            display: inline-block;
            background-color: rgba(239, 68, 68, 0.15);
            color: #f87171;
            padding: 6px 16px;
            border-radius: 50px;
            font-size: 14px;
            font-weight: 600;
            border: 1px solid rgba(239, 68, 68, 0.3);
        }

        /* Produkt-Grid */
        .grid-container {
            max-width: 1100px;
            margin: 0 auto;
        }

        .items-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            margin-bottom: 50px;
        }

        .item-card {
            background: var(--card-bg);
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            overflow: hidden;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: 1px solid rgba(255,255,255,0.1);
            display: flex;
            flex-direction: column;
        }

        .item-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 35px rgba(59, 130, 246, 0.2);
            border-color: rgba(59, 130, 246, 0.4);
        }

        /* Teaser-Bild auf der Hauptseite */
        .item-card-image {
            width: 100%;
            height: 220px;
            object-fit: cover;
            background-color: #f1f5f9;
            border-bottom: 1px solid #e2e8f0;
        }

        .item-info {
            padding: 24px;
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            flex-grow: 1;
        }

        .item-info h2 {
            font-size: 20px;
            font-weight: 700;
            color: var(--text-main);
            margin-bottom: 10px;
        }

        .item-price {
            font-size: 22px;
            color: var(--price-color);
            font-weight: 800;
            background: rgba(239, 68, 68, 0.08);
            padding: 4px 12px;
            border-radius: 10px;
            display: inline-block;
            margin: 0 auto;
        }

        .click-hint {
            margin-top: 16px;
            font-size: 14px;
            color: var(--accent-color);
            font-weight: 600;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
        }

        .item-card:hover .click-hint {
            text-decoration: underline;
        }

        /* Modernes Popup / Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(15, 23, 42, 0.8);
            backdrop-filter: blur(8px);
            justify-content: center;
            align-items: center;
            z-index: 1000;
            padding: 20px;
        }

        .modal-content {
            background-color: #ffffff;
            border-radius: 24px;
            max-width: 550px;
            width: 100%;
            position: relative;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
            overflow: hidden;
            animation: modalSlideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        }

        @keyframes modalSlideUp {
            from { opacity: 0; transform: translateY(30px) scale(0.98); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }

        .close-btn {
            position: absolute;
            top: 15px;
            right: 20px;
            font-size: 32px;
            font-weight: bold;
            color: #ffffff;
            cursor: pointer;
            z-index: 10;
            background: rgba(15, 23, 42, 0.6);
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50px;
            transition: background 0.2s;
        }

        .close-btn:hover {
            background: rgba(15, 23, 42, 0.9);
        }

        /* Großes Bild im Popup */
        .modal-image {
            width: 100%;
            height: 280px;
            object-fit: cover;
            background-color: #f1f5f9;
        }

        .modal-body {
            padding: 30px;
        }

        .modal-title {
            font-size: 26px;
            font-weight: 800;
            color: var(--text-main);
            margin-bottom: 6px;
        }

        .modal-price {
            font-size: 22px;
            color: var(--price-color);
            font-weight: 800;
            margin-bottom: 20px;
        }

        .modal-description {
            font-size: 16px;
            color: #334155;
            border-top: 1px solid #e2e8f0;
            padding-top: 15px;
        }

        /* Styling für Listen im Multitool */
        .modal-description ul {
            list-style: none;
            margin-top: 12px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
        }

        .modal-description li {
            position: relative;
            padding-left: 20px;
            font-size: 14px;
        }

        .modal-description li::before {
            content: "✓";
            position: absolute;
            left: 0;
            color: var(--success-color);
            font-weight: bold;
        }

        /* Footer / Kontaktbereich */
        footer {
            background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
            color: #ffffff;
            padding: 40px 20px;
            border-radius: 20px;
            text-align: center;
            border: 1px solid #334155;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        footer p {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 15px;
        }

        .contact-box {
            display: flex;
            flex-direction: column;
            gap: 15px;
            max-width: 400px;
            margin: 0 auto;
        }

        .btn-contact {
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 14px 20px;
            border-radius: 12px;
            text-decoration: none;
            font-weight: 700;
            font-size: 16px;
            transition: transform 0.2s, filter 0.2s;
        }

        .btn-contact:hover {
            transform: scale(1.02);
        }

        .btn-phone {
            background-color: var(--accent-color);
            color: white;
        }

        .btn-whatsapp {
            background-color: var(--success-color);
            color: white;
        }
    </style>
</head>
<body>

    <header>
        <h1>Premium Flohmarkt</h1>
        <div class="info-badge">Privatverkauf</div>
    </header>

    <div class="grid-container">
        <div class="items-grid">
            
            <div class="item-card" onclick="openModal('Magic Mouse', '20€ VB', 'Eine Maus kabellos und mit Bluetooth.<br><br>Original von Apple.', 'maus.jpg')">
                <img class="item-card-image" src="maus.jpg" alt="Magic Mouse">
                <div class="item-info">
                    <h2>Magic Mouse</h2>
                    <div>
                        <div class="item-price">20€ VB</div>
                    </div>
                    <div class="click-hint">Details &amp; Beschreibung ➔</div>
                </div>
            </div>

            <div class="item-card" onclick="openModal('Uhr', '10€ VB', 'Eine moderne Uhr mit vielen nützlichen Funktionen und stabiler Bluetooth-Verbindung.', 'uhr.jpg')">
                <img class="item-card-image" src="uhr.jpg" alt="Uhr">
                <div class="item-info">
                    <h2>Smart-Uhr</h2>
                    <div>
                        <div class="item-price">10€ VB</div>
                    </div>
                    <div class="click-hint">Details &amp; Beschreibung ➔</div>
                </div>
            </div>

            <div class="item-card" onclick="openModal('Tablet Hülle', '5€ VB', 'Eine hochwertige Schutzhülle.<br><br><strong>Wichtig:</strong> Nur mit Apple iPad Modellen kompatibel.', 'huelle.jpg')">
                <img class="item-card-image" src="huelle.jpg" alt="Tablet Hülle">
                <div class="item-info">
                    <h2>Tablet Hülle</h2>
                    <div>
                        <div class="item-price">5€ VB</div>
                    </div>
                    <div class="click-hint">Details &amp; Beschreibung ➔</div>
                </div>
            </div>

            <div class="item-card" onclick="openModal('Multitool', '12€ VB', 'Ein kompaktes und robustes Multitool mit folgenden Werkzeugen:<ul><li>Zange</li><li>Finger-Reinigung</li><li>Bieröffner</li><li>2 Reinigungstools</li><li>Fingernagelfeile</li><li>Kleines Messer</li><li>Kleiner Kreuz-Schraubendreher</li><li>Öffner-Tool</li><li>Minisäge</li></ul>', 'multitool.jpg')">
                <img class="item-card-image" src="multitool.jpg" alt="Multitool">
                <div class="item-info">
                    <h2>Multitool</h2>
                    <div>
                        <div class="item-price">12€ VB</div>
                    </div>
                    <div class="click-hint">Details &amp; Beschreibung ➔</div>
                </div>
            </div>

        </div>
    </div>

    <div id="detailsModal" class="modal" onclick="closeModalOutside(event)">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">&times;</span>
            <img id="modalImage" class="modal-image" src="" alt="Produktbild">
            <div class="modal-body">
                <div id="modalTitle" class="modal-title">Produktname</div>
                <div id="modalPrice" class="modal-price">Preis</div>
                <div id="modalDescription" class="modal-description">Beschreibung</div>
            </div>
        </div>
    </div>

    <footer>
        <p>Jetzt direkt Kontakt aufnehmen:</p>
        <div class="contact-box">
            <a href="tel:+4915567174773" class="btn-contact btn-phone">📞 Anrufen: +49 15567 174773</a>
            <a href="https://chat.whatsapp.com/LnmhnMRCnRt3JONs8v4ZUt" target="_blank" class="btn-contact btn-whatsapp">💬 WhatsApp Gruppe beitreten</a>
        </div>
    </footer>

    <script>
        // Funktion zum Öffnen des Menüs mit Bild-Übergabe
        function openModal(title, price, description, imageSrc) {
            document.getElementById('modalTitle').innerText = title;
            document.getElementById('modalPrice').innerText = price;
            document.getElementById('modalDescription').innerHTML = description;
            
            // Setzt das passende Bild im Popup
            const modalImg = document.getElementById('modalImage');
            modalImg.src = imageSrc;
            modalImg.alt = title;
            
            document.getElementById('detailsModal').style.display = 'flex';
        }

        function closeModal() {
            document.getElementById('detailsModal').style.display = 'none';
        }

        function closeModalOutside(event) {
            if (event.target.id === 'detailsModal') {
                closeModal();
            }
        }
    </script>

</body>
</html>
