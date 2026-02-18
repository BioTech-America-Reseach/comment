<!DOCTYPE html>
<html lang="sw">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UMEINGIA KWENYE KILINGE CHA ASILI</title>
    <!-- jspdf (imeachwa kwa ajili ya siku zijazo) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        :root {
            --primary-gold: #d4af37;
            --deep-gold: #b8860b;
            --bg-dark: #0a0f1a;
            --card-glass: rgba(255, 255, 255, 0.07);
            --white: #ffffff;
            --whatsapp-green: #117535;
            --warning-red: #ff4444;
            --warning-bg: rgba(255, 0, 0, 0.2);
            --jupiter: #ffaa00;
            --sun: #ff6600;
            --ketu: #993366;
            --mars: #ff3333;
            --saturn: #3366cc;
            --mercury: #33cc33;
            --moon: #cccc00;
            --rahu: #660066;
            --venus: #ff66b2;
        }

        body {
            font-family: 'Garamond', serif;
            background: linear-gradient(rgba(0,0,0,0.8), rgba(0,0,0,0.8)), 
                        url('https://images.unsplash.com/photo-1505751172876-fa1923c5c528?auto=format&fit=crop&w=1350&q=80');
            background-size: cover;
            background-attachment: fixed;
            color: var(--white);
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        header {
            text-align: center;
            padding: 40px 20px;
            width: 100%;
            border-bottom: 2px solid var(--primary-gold);
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(10px);
        }

        .dr-title {
            font-size: 2.5rem;
            letter-spacing: 3px;
            color: var(--primary-gold);
            text-shadow: 2px 2px 10px rgba(0,0,0,0.5);
            margin: 0;
        }

        .container {
            width: 90%;
            max-width: 600px;
            margin: 30px auto;
            background: var(--card-glass);
            padding: 30px;
            border-radius: 15px;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(212, 175, 55, 0.3);
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        h2 { color: var(--primary-gold); text-align: center; }

        label { display: block; margin-top: 15px; font-weight: bold; color: var(--primary-gold); }

        input, select, textarea {
            width: 100%;
            padding: 12px;
            margin-top: 8px;
            border-radius: 8px;
            border: 1px solid var(--primary-gold);
            background: rgba(0,0,0,0.3);
            color: white;
            box-sizing: border-box;
        }

        .btn-magic {
            background: linear-gradient(135deg, var(--primary-gold), var(--deep-gold));
            color: #000;
            padding: 15px;
            border: none;
            border-radius: 8px;
            font-weight: 900;
            cursor: pointer;
            width: 100%;
            font-size: 1.1rem;
            margin-top: 20px;
            transition: 0.3s;
        }

        .btn-magic:hover { transform: scale(1.02); box-shadow: 0 0 20px var(--primary-gold); }

        /* MENU BUTTONS */
        .service-menu {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }

        .btn-service {
            background: transparent;
            border: 1px solid var(--primary-gold);
            color: var(--primary-gold);
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9rem;
        }

        .btn-service.active { background: var(--primary-gold); color: black; }

        /* WHATSAPP FLOAT */
        .whatsapp-float {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--whatsapp-green);
            width: 60px; height: 60px;
            border-radius: 50%;
            display: flex; justify-content: center; align-items: center;
            box-shadow: 0 4px 15px rgba(43, 4, 68, 0.4);
            cursor: pointer;
            z-index: 1000;
        }

        #cards-container { 
            display: none; 
            gap: 20px; 
            flex-wrap: wrap; 
            justify-content: center; 
            padding: 20px; 
            transition: all 0.3s ease;
        }
        .card { 
            width: 260px; 
            height: 400px; 
            perspective: 1000px;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        .card.expanded { 
            width: 500px; 
            height: 600px; 
            z-index: 10;
            box-shadow: 0 0 30px var(--primary-gold);
        }
        .card:not(.expanded) {
            opacity: 0.7;
        }
        .card.expanded ~ .card {
            opacity: 0.3;
            transform: scale(0.9);
        }
        .card-inner { 
            position: relative; 
            width: 100%; 
            height: 100%; 
            transition: transform 0.8s; 
            transform-style: preserve-3d; 
        }
        .card.flipped .card-inner { transform: rotateY(180deg); }
        .card-front, .card-back { 
            position: absolute; 
            width: 100%; 
            height: 100%; 
            backface-visibility: hidden; 
            border-radius: 15px; 
            border: 2px solid var(--primary-gold); 
            overflow-y: auto;
            padding: 15px;
            box-sizing: border-box;
        }
        .card-back { 
            background: #1b0606; 
            display: flex; 
            flex-direction: column;
            align-items: center; 
            justify-content: center; 
            font-size: 1.3rem; 
            color: var(--primary-gold); 
        }
        .card-back small {
            font-size: 0.9rem;
            color: #ccc;
            margin-top: 10px;
            text-align: center;
        }
        .card-front { 
            background: white; 
            color: black; 
            transform: rotateY(180deg); 
        }

        /* Job images */
        .job-image {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            margin-right: 10px;
            object-fit: cover;
            border: 2px solid var(--primary-gold);
        }
        .job-item {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
            background: rgba(0,0,0,0.05);
            padding: 10px;
            border-radius: 10px;
        }

        /* Phone section for appointment/dawa */
        .phone-section {
            margin-top: 20px;
            background: rgba(1, 19, 11, 0.3);
            padding: 15px;
            border-radius: 10px;
        }
        .country-code-select {
            display: flex;
            gap: 10px;
        }
        .country-code-select select {
            width: 40%;
        }
        .country-code-select input {
            width: 60%;
        }
        .error-message {
            color: #ff6b6b;
            font-size: 0.9rem;
            margin-top: 5px;
        }
        .success-message {
            color: #4CAF50;
            font-size: 0.9rem;
            margin-top: 5px;
        }

        /* Send button for results */
        #send-results-container {
            display: none;
            text-align: center;
            margin: 20px auto;
            width: 90%;
            max-width: 500px;
        }
        .send-btn {
            background: var(--whatsapp-green);
            color: white;
            padding: 15px;
            border: none;
            border-radius: 50px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            font-size: 1.2rem;
            transition: 0.3s;
        }
        .send-btn:hover {
            transform: scale(1.02);
            box-shadow: 0 0 20px var(--whatsapp-green);
        }
        /* Warning area */
        #warning-area {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: var(--warning-bg);
            border: 2px solid var(--warning-red);
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            z-index: 2000;
            backdrop-filter: blur(10px);
            box-shadow: 0 0 50px rgba(255, 0, 0, 0.5);
            animation: warningPulse 1s infinite;
        }
        @keyframes warningPulse {
            0% { box-shadow: 0 0 30px rgba(255, 0, 0, 0.5); }
            50% { box-shadow: 0 0 60px rgba(255, 0, 0, 0.8); }
            100% { box-shadow: 0 0 30px rgba(255, 0, 0, 0.5); }
        }
        .warning-title {
            color: var(--warning-red);
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 15px;
        }
        .warning-text {
            color: white;
            font-size: 1.2rem;
            max-width: 400px;
        }

        /* Donation section */
        #donation-section {
            display: none;
            text-align: center;
            margin: 20px auto;
            width: 90%;
            max-width: 500px;
            background: var(--card-glass);
            padding: 20px;
            border-radius: 15px;
            border: 2px solid var(--primary-gold);
        }
        .donation-question {
            font-size: 1.2rem;
            margin-bottom: 15px;
            color: var(--primary-gold);
        }
        .donation-buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
        }
        .donation-btn {
            padding: 10px 30px;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 1.1rem;
        }
        .donation-yes {
            background: #4CAF50;
            color: white;
        }
        .donation-no {
            background: #f44336;
            color: white;
        }
        .donation-details {
            display: none;
            margin-top: 20px;
            text-align: left;
        }
        .network-item {
            background: rgba(0,0,0,0.3);
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
            border-left: 4px solid var(--primary-gold);
        }
        .office-name {
            font-weight: bold;
            color: var(--primary-gold);
            margin-top: 15px;
            text-align: center;
        }
        .red-alert {
            background: rgba(255, 0, 0, 0.2);
            border: 1px solid red;
            color: white;
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
            font-weight: bold;
            animation: blinkRed 1s infinite;
        }
        @keyframes blinkRed {
            0% { background: rgba(255, 0, 0, 0.2); }
            50% { background: rgba(255, 0, 0, 0.5); }
            100% { background: rgba(255, 0, 0, 0.2); }
        }
        .note-box {
            background: rgba(255, 255, 0, 0.1);
            border: 1px solid yellow;
            color: white;
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
        }
        .planet-colorful {
            padding: 5px;
            margin: 2px 0;
            border-radius: 3px;
        }
    </style>
</head>
<body>

<header>
    <h1 class="dr-title">DR. WILLIAM MTANZANIA</h1>
    <p style="color: #f8f2f2; letter-spacing: 2px;">HUDUMA ZA KITABIBU NA RAMLI ASILIA</p>
</header>

<div class="service-menu">
    <button class="btn-service active" onclick="switchPage('ramli', this)">Kilinge cha Ramli</button>
    <button class="btn-service" onclick="switchPage('appointment', this)">Miadi</button>
    <button class="btn-service" onclick="switchPage('dawa', this)">Agiza Dawa</button>
    <button class="btn-service" onclick="switchPage('malalamiko', this)">Malalamiko</button>
</div>

<!-- WARNING AREA (itaonekana kwa sekunde 2) -->
<div id="warning-area" style="display: none;">
    <div class="warning-title">⚠️ O N Y O  K U B W A ⚠️</div>
    <div class="warning-text">Dr. William ameona kwenye roho yako ... usiendelee kabla hujajiandaa kiroho. Kitu kibaya kimepita njia yako. Soma kwa makini!</div>
</div>

<!-- PAGE RAMLI (iliyo na fomu nyepesi) -->
<div id="page-ramli" class="container">
    <h2>RAMLI YA AFYA NA NYOTA</h2>
    <label>Jina lako kamili:</label>
    <input type="text" id="full-name" placeholder="Mfano: BARAKA RICHARD">
    
    <label>Jinsia yako:</label>
    <select id="gender">
        <option value="Mwanaume">Mwanaume</option>
        <option value="Mwanamke">Mwanamke</option>
    </select>

    <label>Tarehe uliozaliwa:</label>
    <div style="display:flex; gap:10px;">
        <select id="birth-day">
            <script>for(let i=1;i<=31;i++) document.write(`<option value="${i}">${i}</option>`);</script>
        </select>
        <select id="birth-month">
            <script>
                const miezi = ["Januari","Februari","Machi","Aprili","Mei","Juni","Julai","Agosti","Septemba","Oktoba","Novemba","Desemba"];
                miezi.forEach((m, i) => document.write(`<option value="${i+1}">${m}</option>`));
            </script>
        </select>
    </div>
    <p style="font-size:0.8rem; color:#ccc;">(Huna haja ya kuweka mwaka wala namba ya simu hapa)</p>

    <button class="btn-magic" onclick="anzaRamli()">NIANZIE RAMLI YANGU</button>
</div>

<div id="page-appointment" class="container" style="display:none;">
    <h2>📅 WEKA MIADI</h2>
    <label>Jina lako:</label>
    <input type="text" id="app-name">
    <label>Tarehe unayotaka kuja kliniki:</label>
    <input type="date" id="app-date">
    <label>Sababu ya kuja:</label>
    <textarea id="app-reason" placeholder="Elezea tatizo lako kwa ufupi..."></textarea>
    
    <!-- SEHEMU YA NAMBA YA SIMU KWA MIADI -->
    <div class="phone-section">
        <label>Namba yako ya simu (kwa mawasiliano ya haraka):</label>
        <div class="country-code-select">
            <select id="app-country-code">
                <option value="+255">Tanzania (+255)</option>
                <option value="+254">Kenya (+254)</option>
                <option value="+256">Uganda (+256)</option>
            </select>
            <input type="text" id="app-phone" placeholder="Mfano: 712345678" maxlength="9">
        </div>
        <div id="app-phone-error" class="error-message"></div>
    </div>
    
    <button class="btn-magic" onclick="tumaAppointment()">TUMA MIADI KWA WHATSAPP</button>
</div>

<div id="page-dawa" class="container" style="display:none;">
    <h2>🌿AGIZA DAWA ASILIA</h2>
    <label>Dawa unayohitaji:</label>
    <select id="dawa-type">
        <option value="Dawa ya Nguvu za Kiume">Dawa ya Nguvu za Kiume</option>
        <option value="Dawa ya Vidonda vya Tumbo">Dawa ya Vidonda vya Tumbo</option>
        <option value="Dawa ya Mapenzi/Mvuto">Dawa ya Mapenzi/Mvuto</option>
        <option value="Dawa ya Kusafisha Nyota">Dawa ya Kusafisha Nyota</option>
        <option value="Dawa ya Ngiri">Dawa ya Ngiri</option>
        <option value="Dawa ya Minyoo">Dawa ya Minyoo</option>
        <option value="Dawa ya kutoa sumu">Dawa ya kutoa sumu mwilini</option>
        <option value="Dawa ya kutoa uchawi">Dawa ya kutoa uchawi mwilini</option>
        <option value="Dawa zingine">Dawa zingine (taja kwenye maelezo)</option>
    </select>
    <label>Mahali unapoishi (kwa delivery):</label>
    <input type="text" id="dawa-location" placeholder="Mkoa na mtaa...">
    
    <!-- SEHEMU YA NAMBA YA SIMU KWA ODA YA DAWA -->
    <div class="phone-section">
        <label>Namba yako ya simu (tukupigie kuhusu utoaji):</label>
        <div class="country-code-select">
            <select id="dawa-country-code">
                <option value="+255">Tanzania (+255)</option>
                <option value="+254">Kenya (+254)</option>
                <option value="+256">Uganda (+256)</option>
            </select>
            <input type="text" id="dawa-phone" placeholder="Mfano: 712345678" maxlength="9">
        </div>
        <div id="dawa-phone-error" class="error-message"></div>
    </div>
    
    <button class="btn-magic" onclick="tumaOda()">TUMA ODA KWA WHATSAPP</button>
</div>

<div id="page-malalamiko" class="container" style="display:none;">
    <h2>⚠️ MALALAMIKO / MAONI</h2>
    <label>Ujumbe wako:</label>
    <textarea id="msg-content" rows="5" placeholder="Andika hapa..."></textarea>
    <button class="btn-magic" onclick="tumaLalamiko()">TUMA KWA DR. WILLIAM</button>
</div>

<div id="loading-area" style="display:none; text-align:center; margin-top:20px;">
    <img src="https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExOHJ6am96am96am96am96am96am96am96am96am96am96am96/3o7TKMGpxxSAt/giphy.gif" width="100">
    <p>Dr. William anachambua nyota zako ... subiri kidogo ...</p>
</div>

<div id="cards-container">
    <!-- Cards zitaingizwa na JavaScript -->
</div>

<!-- KITUFE CHA KUTUMA MATOKEO KWA WHATSAPP (kinaonekana baada ya kadi) -->
<div id="send-results-container">
    <button class="send-btn" onclick="tumaMatokeoKwaWhatsApp()">📲 Tuma matokeo yako ofisini ili kupata maelezo zaidi</button>
</div>

<!-- SEHEMU YA KUCHANGIA -->
<div id="donation-section">
    <div class="donation-question">Je, ungependa kuchangia huduma hizi? Fedha nyingi zimetumika kuwezesha huduma hizi.</div>
    <div class="donation-buttons">
        <button class="donation-btn donation-yes" onclick="onyeshaNambaZaKuchangia(true)">Ndio</button>
        <button class="donation-btn donation-no" onclick="onyeshaNambaZaKuchangia(false)">Hapana</button>
    </div>
    <div id="donation-details" class="donation-details">
        <div class="network-item">
            <strong>Vodacom (M-Pesa):</strong> *150*00# (Namba: 0762 286 282)
        </div>
        <div class="network-item">
            <strong>Tigo Pesa:</strong> *150*01# (Namba: 0712 345 678)
        </div>
        <div class="network-item">
            <strong>Airtel Money:</strong> *150*60# (Namba: 0682 345 678)
        </div>
        <div class="network-item">
            <strong>Halopesa:</strong> *150*88# (Namba: 0742 345 678)
        </div>
        <div class="office-name">BARAKA RICHARD (MWASIBU WA OFISI)</div>
    </div>
</div>

<div class="whatsapp-float" onclick="window.open('https://wa.me/255762286282', '_blank')">
    <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" width="35">
</div>

<script>
    // ==================== DATABASE KAMILI (HAKUNA ILIYOPUNGUA) ====================
    // Sifa za herufi (Kiarabu) – zimeandikwa kwa Kiswahili cha Tanzania
    const HERUFI_DB = {
        'A': [
            "Una uhodari wa uongozi na wengine wanakutii kwa hiari.",
            "Wewe ni jasiri, hukimbii changamoto wala hofu.",
            "Una nguvu za kiroho zinazokusaidia katika maamuzi.",
            "Wewe ni mwaminifu na huwa wasemaji wa kweli.",
            "Una kipaji cha kutatua matatizo kwa haraka na busara.",
            "Wewe ni mkarimu na huwasaidia wengine kwa moyo wote.",
            "Una nidhamu ya kazi na unajituma kwa bidii.",
            "Wewe ni mvumilivu na hukata tamaa kwa urahisi.",
            "Una bahati ya pesa na mafanikio katika shughuli zako.",
            "Wewe ni mkweli na hupendi uongo au hila.",
            "Una uwezo wa kuhamasisha na kuinua wengine.",
            "Wewe una maono makubwa na ndoto za mbali.",
            "Una uwezo wa kusimamia watu na rasilimali kwa ufanisi.",
            "Wewe una hekima ya kufanya maamuzi sahihi nyakati zote.",
            "Unajitolea kwa wengine kwa upendo usio na masharti.",
            "Wewe una ushawishi mkubwa kwa watu unaokutana nao.",
            "Una uwezo wa kuleta mageuzi chanya katika jamii.",
            "Wewe una kipaji cha uongozi wa hali ya juu.",
            "Unawavutia watu kwa utu wako mzuri na tabia yako.",
            "Wewe ni mwenye bahati na baraka katika kila unalofanya."
        ],
        'B': [
            "Wewe ni mpole na una upendo mwingi kwa wote.",
            "Wewe ni msiri mzuri, huhifadhi siri za watu kwa uaminifu.",
            "Una mvuto wa pekee unaowafanya watu wakupende na kukutumainia.",
            "Wewe una busara na hekima ya kutosha kushauri wengine.",
            "Wewe ni mkarimu na huwajali wengine kwa dhati.",
            "Una uwezo wa kusikiliza kwa makini na kuelewa hisia za watu.",
            "Wewe ni mvumilivu sana na huvumilia hata nyakati ngumu.",
            "Una uwezo wa kuleta amani na utulivu popote uendako.",
            "Wewe una hekima ya kuepuka migogoro na vita.",
            "Una upendo usio na masharti kwa wote, hata adui zako.",
            "Wewe huwasaidia maskini na wenye shida kwa moyo wote.",
            "Una roho ya kusamehe na kusahau makosa ya wengine.",
            "Wewe ni mnyenyekevu na hujivuna kwa mali au hadhi.",
            "Una uwezo wa kuwashauri watu wenye matatizo ya maisha.",
            "Wewe ni mtulivu na hukasirika kwa urahisi.",
            "Una uwezo wa kuleta umoja na mshikamano kwenye familia.",
            "Wewe una kipaji cha kuponya kwa maneno yako matamu.",
            "Unawavutia wateja na marafiki kwa urahisi na tabia yako.",
            "Wewe una huruma kubwa kwa wanyonge na walio hatarini.",
            "Una uwezo wa kujenga uhusiano mzuri na watu wa kila aina."
        ],
        'C': [
            "Wewe ni mbunifu na unagundua mambo mapya kila mara.",
            "Wewe ni mcheshi na unawafurahisha watu unaokutana nao.",
            "Una kipaji cha sanaa na ubunifu wa hali ya juu.",
            "Wewe una akili ya haraka na unaelewa mambo kwa upesi.",
            "Unapenda kujifunza mambo mapya kila siku na huchoki.",
            "Wewe ni mwerevu katika mawazo na mipango yako.",
            "Una uwezo wa kuchambua mambo magumu kwa urahisi.",
            "Wewe una uwezo wa kuona fursa ambazo wengine hawaoni.",
            "Unawavutia watu kwa tabia yako nzuri na ucheshi wako.",
            "Wewe ni mbunifu wa kutatua matatizo kwa njia za kisasa.",
            "Una uwezo wa kubadilika na kuzoea mazingira yoyote.",
            "Wewe unapenda kusafiri na kujifunza tamaduni za watu.",
            "Una kipaji cha kuandika na kueleza mawazo yako kwa uzuri.",
            "Wewe ni hodari wa kuigiza na kucheza mbele ya watu.",
            "Una roho ya kujifunza na kufundisha wengine kwa upendo.",
            "Wewe una ushawishi mkubwa kwa maneno yako ya busara.",
            "Una uwezo wa kuwa msanii au mwandishi maarufu siku moja.",
            "Wewe una kipaji cha kuongoza katika nyanja za ubunifu.",
            "Una uwezo wa kugeuza mawazo yako kuwa bidhaa halisi.",
            "Wewe una mawazo ya kimataifa na mtazamo mpana."
        ],
        'D': [
            "Wewe una msimamo mkali na haubadiliki kwa urahisi.",
            "Nidhamu yako kazini na maishani inaigwa na wengi.",
            "Wewe ni mchapakazi na huchoki mpaka umalize ulichoanzia.",
            "Wewe ni muaminifu na watu wanakuamini mali na siri zao.",
            "Huyumbishwi na changamoto za maisha bali unazishinda.",
            "Wewe ni mwenye utaratibu na unapenda kila kitu kiwe sawa.",
            "Una uwezo wa kusimamia miradi mikubwa kwa ufanisi.",
            "Wewe ni sahihi na unajali undani wa kila jambo unalofanya.",
            "Watu wanakuamini mali zao kwa urahisi kwa sababu ya uaminifu wako.",
            "Wewe una nguvu ya kazi na huchoki haraka hata kazi ngumu.",
            "Una uwezo wa kufanya kazi kwa muda mrefu bila kupumzika.",
            "Wewe una malengo na unafanya kazi kwa bidii kuyafikia.",
            "Una nidhamu ya kujiepusha na vishawishi vya maisha.",
            "Wewe ni mtulivu na hupotezi mwelekeo hata kwenye shida.",
            "Unajitolea kwa kazi yako kwa bidii na moyo wote.",
            "Wewe una kipaji cha uongozi wa kiutendaji na madhubuti.",
            "Una uwezo wa kuhamasisha timu kufanya kazi kwa nguvu.",
            "Wewe una heshima kubwa miongoni mwa wenzako na wanaokuzunguka.",
            "Una uwezo wa kutatua migogoro kwa busara na haki.",
            "Wewe una nguvu ya kusimamia rasilimali kwa uadilifu."
        ],
        'E': [
            "Unapenda uhuru wa akili na mwili na hupendi kuzuiwa.",
            "Asili yako ni kusafiri na kujifunza mambo mapya kila mahali.",
            "Wewe ni mwerevu katika kuchambua mambo magumu na kuyafafanua.",
            "Unawavutia watu kwa wepesi wako wa kuzoeana na wageni.",
            "Wewe ni mdadisi na unapenda kuchunguza mambo ya kina.",
            "Una uwezo wa kufundisha na kueleza mambo kwa urahisi kwa wengine.",
            "Wewe una akili ya haraka na unaelewa mambo kwa sekunde.",
            "Una uwezo wa kubadilika na kuzoea mazingira yoyote kwa urahisi.",
            "Wewe unapenda kusafiri na kujifunza tamaduni mpya za watu.",
            "Una kipaji cha kuandika na kueleza mawazo yako kwa usanii.",
            "Wewe ni hodari wa kuigiza na kuleta maisha katika hadithi unazosimulia.",
            "Una uwezo wa kuona fursa ambapo wengine wanaona shida tu.",
            "Wewe ni mcheshi na unawafurahisha watu hata wakati wa shida.",
            "Una roho ya kujifunza kila siku kitu kipya na kukua kielimu.",
            "Wewe una ushawishi mkubwa kwa hoja zako zenye mantiki.",
            "Una uwezo wa kufanya maamuzi ya haraka na yenye usahihi.",
            "Wewe una kipaji cha lugha na mawasiliano bora.",
            "Una uwezo wa kuwa mwalimu bora au mhadhiri mahiri.",
            "Wewe una uvumilivu wa kufundisha wengine hata wenye uelewa mdogo.",
            "Unawavutia wanafunzi na wafuasi kwa urahisi kwa ujuzi wako."
        ],
        'F': [
            "Wewe ni mwenye huruma kubwa na unawasikia wengine kirahisi.",
            "Una uwezo wa kuwa mlezi mzuri wa familia na jamii yako.",
            "Wewe ni mkarimu na hutoa bila kutarajia kurudishiwa.",
            "Una upendo usio na mipaka kwa wapendwa wako na wengine.",
            "Wewe hujitolea kwa wengine kwa moyo wote na kujinyima.",
            "Una nguvu ya kusamehe na kusahau makosa yaliyopita.",
            "Wewe ni mwenye subira na huvumilia hata wakati mgumu.",
            "Una uwezo wa kuleta amani na maelewano kwenye familia.",
            "Wewe una huruma kubwa kwa wanyonge na walio hatarini.",
            "Una upendo usio na masharti kwa wote, hata wasiokupenda.",
            "Wewe huwasaidia maskini na wenye shida kwa moyo wote.",
            "Una roho ya kusamehe na kusahau makosa ya wengine.",
            "Wewe ni mnyenyekevu na hujivuna kwa mali au hadhi.",
            "Una uwezo wa kushauri watu wenye matatizo ya kifamilia.",
            "Wewe ni mtulivu na hukasirika kwa urahisi hata ukikosewa.",
            "Una uwezo wa kuleta mshikamano na umoja kwenye jamii.",
            "Wewe una kipaji cha kuponya kwa maneno yako ya upole.",
            "Unawavutia watu kwa ukarimu wako na tabia yako nzuri.",
            "Wewe una huruma kubwa kwa wanyonge na walio hatarini.",
            "Una uwezo wa kujenga uhusiano mzuri na watu wa kila aina."
        ],
        'G': [
            "Wewe una busara ya kale na hekima ya kizamani.",
            "Wewe ni msiri na unapenda kufanya mambo yako kwa utulivu.",
            "Una uwezo wa kutafiti na kuchunguza mambo ya kina kirahisi.",
            "Wewe una imani thabiti na huyumbishwi na mabadiliko.",
            "Una uwezo wa kushauri watu kwa busara na hekima yako.",
            "Wewe unathamini hekima na maarifa kuliko mali.",
            "Una uwezo wa kuvutia wasomi na wenye akili kwa hoja zako.",
            "Wewe unapenda kusoma na kujifunza mambo mapya kila mara.",
            "Una nguvu ya kushawishi watu kwa hoja zako za msingi.",
            "Wewe ni mwenye utulivu na hupotezi mwelekeo kwa urahisi.",
            "Una uwezo wa kuwaongoza wengine kwenye njia sahihi.",
            "Wewe una hekima ya kuepuka mitego na hatari mbalimbali.",
            "Una uwezo wa kutatua matatizo magumu kwa urahisi.",
            "Wewe ni mchambuzi mahiri wa mambo ya kijamii na kiuchumi.",
            "Una uwezo wa kuleta mageuzi kwa njia za amani.",
            "Wewe una kipaji cha kufundisha na kuelimisha wengine.",
            "Una nguvu ya kushawishi watawala na wenye mamlaka.",
            "Wewe ni mwenye busara na hufanya maamuzi sahihi.",
            "Una uwezo wa kujenga hoja zenye mantiki na ushahidi.",
            "Wewe unavutia watu wenye hekima na ujuzi."
        ]
    };

    // ZODIAC_DB (Kiarabu) – Maelezo 10 kwa kila zodiac
    const ZODIAC_DB = {
        1: { // Aries (Konde)
            name: "Konde (Aries - Al-Hamal)",
            traits: [
                "Wewe ni shujaa na jasiri, hukimbii vita wala changamoto.",
                "Una nguvu na uhodari wa kushindana na wapinzani wako.",
                "Wewe ni mwenye bidii na hamasa ya kufanikisha malengo yako.",
                "Una kipaji cha uongozi na wewe huwa wa kwanza kuanza mambo.",
                "Wewe ni mkweli na husema ukweli wazi hata ukiumiza.",
                "Una roho ya kujitegemea na hupendi kufungwa na wengine.",
                "Wewe ni mkarimu na huwasaidia wengine kwa ukarimu wako.",
                "Una hasira kali lakini hupolei haraka pia.",
                "Wewe ni mwenye nguvu za kiroho na imani thabiti.",
                "Una bahati ya fedha na mafanikio katika shughuli zako."
            ]
        },
        2: { // Taurus (Farasi)
            name: "Farasi (Taurus - Al-Thawr)",
            traits: [
                "Wewe ni mvumilivu na thabiti kama mlima usioyumba.",
                "Una nguvu za kustahimili magumu na changamoto za maisha.",
                "Wewe ni mkarimu na unapenda starehe na anasa za maisha.",
                "Una uhodari wa kusimamia mali na rasilimali zako vizuri.",
                "Wewe ni mwaminifu na hutegemeka kwa ahadi zako.",
                "Una upendo mkubwa kwa familia na watu wako wa karibu.",
                "Wewe ni mwerevu katika biashara na shughuli za kifedha.",
                "Una uvumilivu wa kusubiri matokeo bila kukata tamaa.",
                "Wewe ni mwenye nguvu za kiroho na imani thabiti.",
                "Una bahati ya kupata vitu vizuri na anasa za maisha."
            ]
        },
        3: { // Gemini (Mapacha)
            name: "Mapacha (Gemini - Al-Jawza)",
            traits: [
                "Wewe ni mwerevu na una akili ya haraka ya kuelewa mambo.",
                "Una uwezo wa kujifunza lugha na mawasiliano kwa urahisi.",
                "Wewe ni mcheshi na unawafurahisha watu unaokutana nao.",
                "Una uwezo wa kubadilika na kuzoea mazingira yoyote.",
                "Wewe ni mdadisi na unapenda kujua habari na mambo mapya.",
                "Una uhodari wa kuandika na kueleza mawazo yako kwa usanii.",
                "Wewe ni mwenye urafiki na unapenda kukutana na watu wapya.",
                "Una kipaji cha biashara na mawasiliano bora.",
                "Wewe ni mwenye nguvu za kiroho na imani thabiti.",
                "Una bahati ya kusafiri na kujifunza tamaduni mbalimbali."
            ]
        },
        4: { // Cancer (Kaa)
            name: "Kaa (Cancer - Al-Sartan)",
            traits: [
                "Wewe ni mwenye hisia nyeti na unawajali wengine kwa dhati.",
                "Una upendo mkubwa kwa familia na watu wako wa karibu.",
                "Wewe ni mkarimu na huwasaidia wengine kwa moyo wote.",
                "Una uwezo wa kuhisi mazingira na watu unaokutana nao.",
                "Wewe ni mlinzi mzuri wa familia na watu wako.",
                "Una nguvu za kiroho na unavutiwa na mambo ya siri.",
                "Wewe ni mwenye uvumilivu na huvumilia hali ngumu.",
                "Una kipaji cha kupika na kuwakaribisha wageni.",
                "Wewe ni mwaminifu na hutegemeka kwa watu wako.",
                "Una bahati ya kupata nyumba nzuri na familia yenye furaha."
            ]
        },
        5: { // Leo (Simba)
            name: "Simba (Leo - Al-Asad)",
            traits: [
                "Wewe ni shujaa na jasiri kama simba mwenye nguvu.",
                "Una kipaji cha uongozi na wewe huwa wa kwanza kuongoza.",
                "Wewe ni mkarimu na huwapa wengine kwa ukarimu wako.",
                "Una nguvu za kuvutia watu na kuwa na ushawishi kwao.",
                "Wewe ni mkweli na husema ukweli wazi hata ukiumiza.",
                "Una roho ya kujitegemea na hupendi kufungwa na wengine.",
                "Wewe ni mwenye nguvu za kiroho na imani thabiti.",
                "Una kipaji cha kuigiza na kuwa kwenye mbele ya watu.",
                "Wewe ni mwenye bahati ya fedha na mafanikio makubwa.",
                "Una uwezo wa kuvutia watu na kuwa kiongozi wao."
            ]
        },
        6: { // Virgo (Mashuke)
            name: "Mashuke (Virgo - Al-Sumbula)",
            traits: [
                "Wewe ni mwenye utaratibu na unapenda kila kitu kiwe sawa.",
                "Una uhodari wa kuchambua mambo na kuyafanyia kazi.",
                "Wewe ni mwenye akili ya haraka na unaelewa mambo kwa upesi.",
                "Una uwezo wa kufanya kazi kwa bidii na usahihi mkubwa.",
                "Wewe ni mkarimu na huwasaidia wengine kwa maarifa yako.",
                "Una nguvu za kujifunza na kufundisha wengine kwa urahisi.",
                "Wewe ni mwaminifu na hutegemeka kwa kazi na majukumu.",
                "Una kipaji cha kutafiti na kuchunguza mambo ya kina.",
                "Wewe ni mwenye nguvu za kiroho na imani thabiti.",
                "Una bahati ya kufanikiwa katika masomo na taaluma zako."
            ]
        },
        7: { // Libra (Mizani)
            name: "Mizani (Libra - Al-Mizan)",
            traits: [
                "Wewe ni mwenye usawa na unapenda haki na uadilifu.",
                "Una uwezo wa kupatanisha watu na kuleta amani kati yao.",
                "Wewe ni mkarimu na huwasaidia wengine kwa usawa.",
                "Una kipaji cha sanaa na uzuri na unavutiwa na mambo mazuri.",
                "Wewe ni mwenye urafiki na unapenda kukutana na watu wapya.",
                "Una nguvu za kuvutia watu kwa tabia yako nzuri.",
                "Wewe ni mwaminifu na hutegemeka kwa ushauri wako.",
                "Una uwezo wa kufanya maamuzi ya haki na busara.",
                "Wewe ni mwenye nguvu za kiroho na imani thabiti.",
                "Una bahati ya kupata wapenzi na marafiki wengi."
            ]
        },
        8: { // Scorpio (Nge)
            name: "Nge (Scorpio - Al-Aqrab)",
            traits: [
                "Wewe ni mwenye nguvu za siri na unavutiwa na mambo ya kina.",
                "Una uwezo wa kuchunguza na kufichua mambo yaliyofichika.",
                "Wewe ni mkweli na husema ukweli hata ukiumiza.",
                "Una nguvu za kiroho na unavutiwa na mambo ya mizimu.",
                "Wewe ni mwaminifu kwa watu wako na hutegemeka.",
                "Una uhodari wa kusimamia mali na rasilimali zako.",
                "Wewe ni mwenye uvumilivu na huvumilia hali ngumu.",
                "Una kipaji cha kutafiti na kuchunguza mambo ya siri.",
                "Wewe ni mwenye nguvu za kushawishi watu kwa hoja zako.",
                "Una bahati ya kupata utajiri na mafanikio makubwa."
            ]
        },
        9: { // Sagittarius (Mshale)
            name: "Mshale (Sagittarius - Al-Qaws)",
            traits: [
                "Wewe ni mpenzi wa safari na unapenda kujifunza mambo mapya.",
                "Una uwezo wa kuona mbali na kuwa na maono makubwa.",
                "Wewe ni mkweli na husema ukweli wazi hata ukiumiza.",
                "Una nguvu za kiroho na unavutiwa na falsafa na dini.",
                "Wewe ni mkarimu na huwasaidia wengine kwa ukarimu wako.",
                "Una uhodari wa kufundisha na kuelimisha wengine.",
                "Wewe ni mwenye urafiki na unapenda kukutana na watu wapya.",
                "Una kipaji cha kuandika na kueleza mawazo yako kwa usanii.",
                "Wewe ni mwenye nguvu za kushawishi watu kwa hoja zako.",
                "Una bahati ya kusafiri na kujifunza tamaduni mbalimbali."
            ]
        },
        10: { // Capricorn (Mbuuzi)
            name: "Mbuuzi (Capricorn - Al-Jadi)",
            traits: [
                "Wewe ni mwenye bidii na unafanya kazi kwa nguvu zote.",
                "Una uwezo wa kusimamia miradi na rasilimali kwa ufanisi.",
                "Wewe ni mwaminifu na hutegemeka kwa ahadi na majukumu.",
                "Una nguvu za kustahimili magumu na changamoto za maisha.",
                "Wewe ni mwenye utaratibu na unapenda kila kitu kiwe sawa.",
                "Una uhodari wa kupanga mipango na kutekeleza kwa usahihi.",
                "Wewe ni mwenye uvumilivu na huvumilia hata hali ngumu.",
                "Una kipaji cha uongozi na wewe huwa wa kwanza kuongoza.",
                "Wewe ni mwenye nguvu za kiroho na imani thabiti.",
                "Una bahati ya kupata mafanikio makubwa na heshima."
            ]
        },
        11: { // Aquarius (Ndoo)
            name: "Ndoo (Aquarius - Al-Dalu)",
            traits: [
                "Wewe ni mbunifu na unagundua mambo mapya kila mara.",
                "Una uwezo wa kubadilika na kuzoea mazingira yoyote.",
                "Wewe ni mwenye urafiki na unapenda kukutana na watu wapya.",
                "Una nguvu za kiroho na unavutiwa na mambo ya siri.",
                "Wewe ni mkweli na husema ukweli wazi hata ukiumiza.",
                "Una uhodari wa kufikiria mambo ya kina na ya baadaye.",
                "Wewe ni mkarimu na huwasaidia wengine kwa maarifa yako.",
                "Una kipaji cha kuandika na kueleza mawazo yako kwa usanii.",
                "Wewe ni mwenye nguvu za kushawishi watu kwa hoja zako.",
                "Una bahati ya kupata marafiki wengi na mitandao mipana."
            ]
        },
        12: { // Pisces (Samaki)
            name: "Samaki (Pisces - Al-Hut)",
            traits: [
                "Wewe ni mwenye hisia nyeti na unawajali wengine kwa dhati.",
                "Una uwezo wa kuhisi mazingira na watu unaokutana nao.",
                "Wewe ni mkarimu na huwasaidia wengine kwa moyo wote.",
                "Una nguvu za kiroho na unavutiwa na mambo ya dini na imani.",
                "Wewe ni mwaminifu na hutegemeka kwa watu wako.",
                "Una uhodari wa sanaa na ubunifu wa hali ya juu.",
                "Wewe ni mwenye uvumilivu na huvumilia hali ngumu.",
                "Una kipaji cha kuponya kwa maneno yako na hisia zako.",
                "Wewe ni mwenye nguvu za kushawishi watu kwa upole wako.",
                "Una bahati ya kupata upendo na furaha katika maisha."
            ]
        }
    };

    // SIFA_DB ina sifa 20 na kazi 5 kwa kila herufi (zote kwa Kiswahili) + picha za kazi
    const SIFA_DB = {
        'A': {
            traits: HERUFI_DB['A'],
            careers: [
                { title: "Jeshi / Ulinzi", desc: "Una uwezo wa kulinda na kuongoza. Kazi za ulinzi na usalama zitakufaa sana.", image: "https://img.icons8.com/color/48/000000/military.png" },
                { title: "Uongozi wa serikali", desc: "Sifa zako za ujasiri na uongozi zinakufaa katika siasa au utawala.", image: "https://img.icons8.com/color/48/000000/government.png" },
                { title: "Biashara ya kimataifa", desc: "Akili yako ya haraka na ujasiri vitakufanya ufanikiwe katika biashara kubwa.", image: "https://img.icons8.com/color/48/000000/global-business.png" },
                { title: "Mkurugenzi wa kampuni", desc: "Uwezo wako wa kusimamia na kuongoza utakufaa kama mkurugenzi.", image: "https://img.icons8.com/color/48/000000/company.png" },
                { title: "Mkufunzi wa maisha", desc: "Uwezo wako wa kuhamasisha na kusaidia wengine utakufaa kama mkufunzi.", image: "https://img.icons8.com/color/48/000000/personal-trainer.png" }
            ]
        },
        'B': {
            traits: HERUFI_DB['B'],
            careers: [
                { title: "Mshauri wa familia", desc: "Upole na busara yako inakufaa kuwasaidia wengine katika mahusiano.", image: "https://img.icons8.com/color/48/000000/family.png" },
                { title: "Daktari wa magonjwa ya akili", desc: "Uwezo wako wa kusikiliza na kuelewa hisia za watu ni zawadi.", image: "https://img.icons8.com/color/48/000000/mental-state.png" },
                { title: "Kiongozi wa dini", desc: "Mvuto wako wa kiroho na upendo unakufaa kuwaongoza wengine kiroho.", image: "https://img.icons8.com/color/48/000000/church.png" },
                { title: "Mfanyakazi wa ustawi wa jamii", desc: "Moyo wako wa kujali unakufaa kusaidia jamii.", image: "https://img.icons8.com/color/48/000000/social-work.png" },
                { title: "Mwalimu wa watoto", desc: "Uvumilivu na upendo wako kwa watoto utakufanya mwalimu bora.", image: "https://img.icons8.com/color/48/000000/teacher.png" }
            ]
        },
        'C': {
            traits: HERUFI_DB['C'],
            careers: [
                { title: "Msanii (muziki, uchoraji)", desc: "Ubunifu wako na ucheshi vitakufanya uwe msanii maarufu.", image: "https://img.icons8.com/color/48/000000/art.png" },
                { title: "Mwandishi", desc: "Uwezo wako wa kuchambua na kueleza mambo unakufaa kuwa mwandishi.", image: "https://img.icons8.com/color/48/000000/writer.png" },
                { title: "Mjasiriamali wa teknolojia", desc: "Akili yako ya haraka na ubunifu utakusaidia kuanzisha biashara za kisasa.", image: "https://img.icons8.com/color/48/000000/technology.png" },
                { title: "Mkurugenzi wa ubunifu", desc: "Uwezo wako wa kuona mambo kwa mtazamo mpya utakufaa katika tasnia ya ubunifu.", image: "https://img.icons8.com/color/48/000000/innovation.png" },
                { title: "Mwalimu wa sanaa", desc: "Unaweza kufundisha wengine ubunifu wako.", image: "https://img.icons8.com/color/48/000000/art-teacher.png" }
            ]
        },
        'D': {
            traits: HERUFI_DB['D'],
            careers: [
                { title: "Meneja wa miradi", desc: "Nidhamu na uwezo wako wa kusimamia unakufaa kuwa meneja bora.", image: "https://img.icons8.com/color/48/000000/project-management.png" },
                { title: "Mhasibu", desc: "Usahihi na uaminifu wako utakufanya mhasibu anayeaminika.", image: "https://img.icons8.com/color/48/000000/accountant.png" },
                { title: "Mhandisi", desc: "Ustadi wako wa kuchambua na kutatua matatizo unakufaa katika uhandisi.", image: "https://img.icons8.com/color/48/000000/engineer.png" },
                { title: "Mratibu wa shughuli", desc: "Uwezo wako wa kutekeleza na kusimamia unakufaa kuratibu.", image: "https://img.icons8.com/color/48/000000/coordinator.png" },
                { title: "Meneja wa rasilimali watu", desc: "Uwezo wako wa kuwaunganisha watu unakufaa katika usimamizi.", image: "https://img.icons8.com/color/48/000000/human-resources.png" }
            ]
        },
        'E': {
            traits: HERUFI_DB['E'],
            careers: [
                { title: "Mwalimu", desc: "Uwezo wako wa kueleza na kufundisha ni zawadi.", image: "https://img.icons8.com/color/48/000000/teacher.png" },
                { title: "Mtafiti", desc: "Upendo wako wa kutafiti na kuchambua unakufaa katika utafiti.", image: "https://img.icons8.com/color/48/000000/research.png" },
                { title: "Mkurugenzi wa utalii", desc: "Upendo wako wa safari na mabadiliko unakufaa kuwaongoza wengine.", image: "https://img.icons8.com/color/48/000000/tourism.png" },
                { title: "Mwandishi wa riwaya", desc: "Ubunifu wako na hisia safi zitakusaidia kuandika riwaya zenye mvuto.", image: "https://img.icons8.com/color/48/000000/novel.png" },
                { title: "Mkufunzi wa maisha", desc: "Uvumilivu wako na uwezo wa kugeuza mambo utawasaidia wengine.", image: "https://img.icons8.com/color/48/000000/life-coach.png" }
            ]
        }
    };

    // NYOTA_DESC – Kila nyota ina maradhi 20 na lishe 20 (zimeandikwa kwa Kiswahili)
    const NYOTA_DESC = {
        1: { 
            n: "KONDE (ARIES)", 
            h: [
                "Unaweza kupata maumivu ya kichwa mara kwa mara kwa sababu unafikiri sana.",
                "Macho yako huchoka haraka unapotumia simu au kompyuta kwa muda mrefu.",
                "Shinikizo la damu linaweza kukusumbua ukikosa usingizi.",
                "Mikono na vidole vyako vinaweza kufa ganzi ukikaa sehemu moja kwa muda.",
                "Meno yako ni nyeti kwa baridi au moto, epuka vinywaji baridi sana au moto sana.",
                "Unaweza kuhisi kizunguzungu ukisimama ghafla, simama taratibu.",
                "Masikio yako yanaweza kuziba ukiwa na mafua au mawazo mengi.",
                "Kumbukumbu yako inaweza kukusaliti kidogo ukichoka, ni kawaida.",
                "Unaweza kukosa usingizi (insomnia) ukiwa na mawazo mengi.",
                "Mapafu yako yanaweza kuathiriwa na mabadiliko ya ghafla ya hewa.",
                "Unaweza kuwa na mzio wa vumbi au moshi.",
                "Moyo wako unahitaji kupumzika vya kutosha, usijikaze kupita kiasi.",
                "Unaweza kupata maumivu ya mgongo ukikaa vibaya.",
                "Misuli yako inaweza kukaza ukifanya kazi nyingi bila kunyooka.",
                "Unaweza kuwa na upungufu wa damu (anemia) ukila lishe duni.",
                "Ngozi yako inaweza kukauka wakati wa baridi.",
                "Unaweza kupatwa na mafua mara kwa mara usipojilinda.",
                "Shinikizo la damu linaweza kuongezeka ukiwa na msongo.",
                "Unaweza kuwa na matatizo ya mmeng'enyo wa chakula ukila haraka.",
                "Mifupa yako inaweza kuwa dhaifu ukikosa madini ya kalsiamu."
            ], 
            d: [
            "Juisi ya tikiti maji: Osha tunda, kata vipande, saga na kunywa asubuhi kuongeza maji mwilini.",
            "Tangawizi: Chukua kipande, osha, chemsha na kunywa asubuhi kufungua mishipa ya damu.",
            "Karoti tatu: Osha, menya na itafune jioni kuimarisha macho yako.",
            "Samaki aipwe: Pika kwa mvuke. Protini yake inasaidia ubongo wako.",
            "Mafuta ya zeituni: Weka kijiko kimoja kwenye mboga baada ya kupika ili kulainisha mishipa ya moyo.",
            "Mayai mawili ya kienyeji: Chemsha na ule asubuhi kupambana na uchovu.",
            "Mdalasini: Weka kijiko kidogo kwenye uji ili kutuliza neva.",
            "Juisi ya beetroot: Osha, menya na saga. Kunywa mara mbili kwa siku kusafisha damu.",
            "Nanasi: Osha, menya na ule nyama yake; itasaidia tumbo kusaga chakula.",
            "Asali mbichi: Kijiko kimoja asubuhi kabla ya kula kitu kingine kuongeza kinga ya mwili.",
            "Parachichi nusu: Lioshe na ule kila siku; mafuta yake yanalinda ngozi na moyo.",
            "Mbegu za maboga: Kausha na kaanga bila mafuta, tafuna kiganja kimoja kuimarisha akili.",
            "Papai: Osha, menya na ule vipande vikubwa jioni kusafisha utumbo.",
            "Mchicha: Osha majani, pika kwa dakika tano tu ili usipoteze virutubisho.",
            "Maji safi: Kunywa glasi 10 kwa siku kusafisha figo.",
            "Komamanga: Pasua na ule mbegu zake; linazuia kansa na kusafisha mishipa.",
            "Epuka kahawa kali: Badala yake kunywa maji ya madafu.",
            "Maziwa ya mgando: Kunywa glasi moja mchana kuimarisha kinga ya tumbo.",
            "Bamia tano: Osha, chemsha na kunywa maji yake yenye utelezi; ni tiba ya magoti.",
            "Pilipili mtama: Weka kidogo kwenye chakula kufungua mishipa ya damu.",
            "Matunda ya zambarau: Osha na ule; yanazuia seli kuzeeka haraka.",
            "Limao na maji ya moto: Kamua limao moja kwenye maji ya moto asubuhi kuchoma mafuta.",
            "Kabeji mbichi: Osha majani na ule kama saladi; inatengeneza kinga ya vidonda vya tumbo.",
            "Ndizi mbivu mbili: Ile asubuhi kupata potasiamu inayolinda misuli.",
            "Njegere mbichi: Chemsha na kula kama mboga; protini yake inajenga tishu zilizojeruhiwa.",
            "Supu ya mifupa: Chemsha mifupa ya ng'ombe kwa saa kadhaa na kunywa supu hiyo kuimarisha mifupa.",
            "Viazi vitamu: Osha na chemsha na maganda yake; sukari yake ni asilia.",
            "Majani ya kunde: Osha vizuri na upike kidogo; yanasafisha macho na ngozi.",
            "Unga wa lishe: Changanya ulezi na ngano kwa nguvu ya asili.",
            "Chai ya mchaichai: Osha majani na chemshe, kunywa mchana kutuliza akili."
            ]
        },
        2: { 
            n: "FARASI (TAURUS)", 
            h: [
                "Koo lako linaweza kukwaruza au kuuma ukiongea sana.",
                "Tezi yako ya nyironi inaweza kusababisha mabadiliko ya uzito usipolinda lishe.",
                "Shingo yako inaweza kukakamaa ukikaa sehemu moja kwa muda mrefu.",
                "Mabega yako huchukua mkazo wa mawazo yako, hivyo yanaweza kuuma.",
                "Sukari yako inaweza kupanda ukizidisha vyakula vitamu.",
                "Uzito wako unaweza kuongezeka haraka ukila chakula kingi.",
                "Mafua na kikohozi vinaweza kukupata mara kwa mara kwenye mazingira yenye vumbi.",
                "Masikio yako yanaweza kuziba ukiwa na mafua.",
                "Mgongo wako wa chini unaweza kuuma unapoinama sana.",
                "Shinikizo la damu linaweza kuongezeka ukiwa na msongo.",
                "Unaweza kupatwa na maumivu ya kichwa ya sinus.",
                "Ngozi yako inaweza kukauka usipokunywa maji ya kutosha.",
                "Unaweza kuwa na upungufu wa vitamini D ukikosa jua.",
                "Misuli ya miguu inaweza kukaza ukitembea sana.",
                "Unaweza kupatwa na maumivu ya goti kutokana na uzito.",
                "Mfumo wako wa kinga unaweza kuwa dhaifu ukila lishe duni.",
                "Unaweza kuwa na mzio wa vyakula fulani.",
                "Shinikizo la damu linaweza kushuka ghafla.",
                "Unaweza kupata maumivu ya viungo wakati wa baridi.",
                "Meno yako yanaweza kuoza ukisahau kusafisha."
            ], 
            d: [
                "Tufaha moja kila siku: Osha kwa maji ya moto kidogo, ule asubuhi kusafisha tumbo na koo.",
                "Karanga mbichi: Osha kiganja kimoja na ule; mafuta yake yanalinda sauti yako.",
                "Limao na asali: Kamua limao moja kwenye glasi ya maji vuguvugu, weka asali kijiko kimoja na unywe asubuhi.",
                "Supu ya kuku wa kienyeji: Chemsha kuku na tangawizi na kitunguu saumu; kunywa supu hii kuimarisha kinga ya koo.",
                "Ndizi mbivu: Ile asubuhi saa tano; inakupa nguvu na kuzuia uchovu.",
                "Mihogo ya kuchemsha: Osha na chemsha; inakupa nguvu ya kudumu.",
                "Mapera mawili: Osha vizuri na ule; yana vitamini C nyingi inayolinda koo lako.",
                "Bamia mbichi: Osha na kata vipande vidogo, ule kama saladi; utelezi wake unalainisha shingo.",
                "Dengu za kuchemsha: Kula dengu badala ya nyama nyekundu; ni rafiki wa moyo.",
                "Maziwa safi: Chemsha na unywe glasi moja jioni kulainisha koo.",
                "Zabibu: Osha kwa maji mengi na ule kiganja kimoja; sukari yake asilia inakupa nguvu.",
                "Chai ya mchaichai: Osha majani na chemshe; inaondoa gesi na harufu mbaya.",
                "Kisamvu: Osha vizuri na chemshe; kinarutubisha damu yako.",
                "Viazi vikuu: Osha na chemsha; vinakupa nguvu ya kudumu.",
                "Maji lita tatu: Kunywa maji mengi ili ngozi na figo ziwe safi.",
                "Juisi ya karoti: Osha na saga karoti; kunywa jioni kusaidia macho.",
                "Kitunguu saumu: Meza punje mbili kila jioni baada ya kuzikata; ni kinga dhidi ya maradhi ya koo.",
                "Ugali wa dona: Usitumie sembe; dona ina nyuzi zinazosaidia tumbo.",
                "Papai la sukari: Osha na ule jioni; litakusaidia kulala vizuri.",
                "Mafuta ya zeituni: Weka kijiko kimoja kwenye saladi; inazuia mishipa ya shingo kukaza.",
                "Mboga za kijani: Osha jani kwa jani; kula mchicha kwa wingi kuimarisha damu.",
                "Beetroot: Osha na chemshe kidogo kisha ule; inasafisha ini lako.",
                "Mdalasini kwenye uji: Inatuliza akili na kuzuia msongo.",
                "Maji ya madafu: Kunywa dafu moja kila wiki; yana madini yanayolinda mwili.",
                "Komamanga: Pasua na ule mbegu zake; inasaidia tezi yako.",
                "Chai ya kijani: Kunywa asubuhi kuchoma mafuta ya ziada.",
                "Viazi mbatata: Osha na chemsha na maganda yake; maganda yana madini muhimu.",
                "Matikiti maji: Ule sehemu nyeupe ya ndani; inalinda figo zako.",
                "Unga wa lishe: Changanya ngano na ulezi; kunywa uji huu ukiwa na asali.",
                "Majani ya kunde: Osha vizuri na upike kidogo; yanaimarisha mifupa."
            ]
        }
    };

    // AYURVEDA_DB – Tiba 25 za asili (zimeandikwa kwa Kiswahili cha Tanzania)
    const AYURVEDA_DB = {
        "Tangawizi": {
            name: "Tangawizi",
            scientific: "Zingiber officinale",
            uses: [
                { condition: "Kuumwa tumbo (Indigestion)", recipe: "Chukua kipande kidogo cha tangawizi, saga, changanya na chumvi au sukari nyekundu. Kula mara mbili kwa siku kabla ya chakula." },
                { condition: "Maumivu ya sikio", recipe: "Tone tone la juisi ya tangawizi yenye joto joto (si moto) kwenye sikio lenye kuumwa. Usitumie kama kuna usaha." },
                { condition: "Kukosa sauti", recipe: "Kausha tangawizi, saga kuwa unga. Kijiko kimoja changanya na asali, kunywa mara tatu kwa siku." },
                { condition: "Mafua / Kikohozi", recipe: "Chemsha kipande cha tangawizi na maji, kunywa maji yake mara mbili kwa siku." }
            ]
        },
        "Kamanga": {
            name: "Komamanga",
            scientific: "Punica granatum",
            uses: [
                { condition: "Kuhara / Kichochoro", recipe: "Kausha maganda ya komamanga, saga. Kijiko kimoja changanya na sukari, kunywa mara mbili kwa siku." },
                { condition: "Kuwashwa tumbo (Hyperacidity)", recipe: "Kula tunda la komamanga lenyewe kwa wingi." },
                { condition: "Kutoa damu mwanzoni", recipe: "Juisi ya komamanga vijiko viwili na sukari, kunywa mara mbili kwa siku." },
                { condition: "Harufu mbaya mdomoni", recipe: "Tafuna mbegu za komamanga baada ya kula." }
            ]
        },
        "Amla": {
            name: "Amla (Nyeupe)",
            scientific: "Emblica officinalis",
            uses: [
                { condition: "Afya kwa ujumla", recipe: "Kula Amla mbichi mara kwa mara huongeza nguvu na kinga ya mwili." },
                { condition: "Kiwango cha sukari (Diabetes)", recipe: "Juisi ya Amla na juisi ya manjano (Haldi) vijiko viwili kila moja, kunywa mara mbili kwa siku." },
                { condition: "Kupunguza msongo (Stress)", recipe: "Saga Amla na maziwa ya mgando, paka kwenye paji la uso." },
                { condition: "Kuzuia mvi na kudumisha nywele", recipe: "Loweka Amla usiku kucha, asubuhi paka maji yake kwenye nywele kabla ya kuoga." }
            ]
        },
        "Mdalasini": {
            name: "Mdalasini",
            scientific: "Cinnamomum zeylanicum",
            uses: [
                { condition: "Kuhara", recipe: "Kijiko kimoja cha unga wa mdalasini na maji ya moto, kunywa mara mbili kwa siku." },
                { condition: "Kichefuchefu", recipe: "Kijiko kimoja cha unga wa mdalasini na asali, kunywa." },
                { condition: "Maumivu ya kichwa", recipe: "Saga mdalasini na maji, paka kwenye paji la uso." },
                { condition: "Kukosa hamu ya kula", recipe: "Chemsha mdalasini na tangawizi, kunywa maji yake kabla ya chakula." }
            ]
        },
        "Dhania": {
            name: "Dhania (majani au mbegu)",
            scientific: "Coriandrum sativum",
            uses: [
                { condition: "Mafua na kikohozi", recipe: "Chemsha mbegu za dhania, ongeza sukari na manjano, kunywa mara tatu kwa siku." },
                { condition: "Minyoo tumboni", recipe: "Kijiko kimoja cha unga wa dhania na sukari nyekundu, kula asubuhi kwa siku tano." },
                { condition: "Kuchoka kwa jua", recipe: "Chemsha mbegu za dhania, ongeza sukari na chumvi kidogo, kunywa mara kwa mara." },
                { condition: "Homa", recipe: "Chemsha dhania na tangawizi, kunywa maji yake." }
            ]
        },
        "Iliki": {
            name: "Iliki (kardiamu)",
            scientific: "Elettaria cardamomum",
            uses: [
                { condition: "Kwikwi (Hiccough)", recipe: "Tafuna iliki mbili mbili (usiweze zaidi ya 4 kwa siku)." },
                { condition: "Kutapika", recipe: "Unga wa iliki uliokaangwa kwa samli, kijiko kidogo na asali mara tatu kwa siku." },
                { condition: "Harufu mbaya mdomoni", recipe: "Tafuna iliki baada ya kula." },
                { condition: "Kuhara na kutapika", recipe: "Choma maganda ya iliki, chukua majivu yake kijiko kimoja na asali." }
            ]
        },
        "Samli (Ghee)": {
            name: "Samli (siagi iliyoyeyushwa)",
            scientific: "Clarified Butter",
            uses: [
                { condition: "Vidonda na majeraha", recipe: "Paka samli kwenye kidonda mara kwa mara." },
                { condition: "Kukosa hamu ya kula", recipe: "Changanya samli na Hing na Jeera, weka kwenye chakula." },
                { condition: "Kumbukumbu kwa watoto", recipe: "Kula samli kidogo kila siku huongeza kumbukumbu." },
                { condition: "Kuvimbiwa", recipe: "Kijiko kimoja cha samli kwenye maziwa ya joto kabla ya kulala." }
            ]
        },
        "Manjano": {
            name: "Manjano (Haldi)",
            scientific: "Curcuma longa",
            uses: [
                { condition: "Kiwango cha sukari", recipe: "Juisi ya manjano na juisi ya Amla vijiko viwili kila moja, kunywa mara mbili kwa siku." },
                { condition: "Chunusi", recipe: "Paka paste ya manjano kwenye chunusi mara mbili kwa siku." },
                { condition: "Mafua", recipe: "Kijiko kimoja cha manjano na maziwa ya joto na sukari, kunywa mara mbili kwa siku." },
                { condition: "Mzio wa ngozi", recipe: "Chemsha manjano na maji, kisha tumia maji hayo kuosha sehemu yenye mzio." }
            ]
        },
        "Hing": {
            name: "Hing (Uvumba wa kula)",
            scientific: "Ferula narthex",
            uses: [
                { condition: "Maumivu ya tumbo", recipe: "Changanya Hing na maji, paka kwenye kitovu na kuzunguka." },
                { condition: "Maumivu ya jino", recipe: "Kaaanga Hing kwa samli, weka kwenye jino lenye kuumwa." },
                { condition: "Kukosa hamu ya kula", recipe: "Kijiko kidogo cha Hing kilichokaangwa kwenye samli, changanya na maziwa ya mgando, kunywa." },
                { condition: "Tumbo kujaa gesi kwa watoto", recipe: "Changanya Hing na maji, paka kwenye tumbo la mtoto." }
            ]
        },
        "Jayphal": {
            name: "Jayphal (kungu)",
            scientific: "Myristica fragrans",
            uses: [
                { condition: "Kuhara kwa watoto", recipe: "Saga Jayphal, chukua dozi ndogo (kichaa cha kijiko) changanya na maziwa, mpe mtoto mara 3-4 kwa siku." },
                { condition: "Mtoto kukosa usingizi na kuwa na wasiwasi", recipe: "Dozi ndogo ya Jayphal kwenye maziwa hulaza mtoto." },
                { condition: "Madoa meusi usoni", recipe: "Saga Jayphal kwenye maziwa, paka usoni." },
                { condition: "Maumivu ya tumbo kutokana na kuhara", recipe: "Kijiko kimoja cha unga wa Jayphal na maji ya moto, kunywa mara 4-5 kwa siku." }
            ]
        },
        "Jeera": {
            name: "Jeera (bizari)",
            scientific: "Cuminum cyminum",
            uses: [
                { condition: "Kuumwa tumbo", recipe: "Unga wa jeera uliokaangwa na chumvi, kijiko kimoja na maji ya moto mara tatu kwa siku." },
                { condition: "Kuhara", recipe: "Kijiko kimoja cha jeera kwenye glasi ya maziwa ya mgando, mara nne kwa siku." },
                { condition: "Kiwango cha asidi tumboni", recipe: "Kaanga jeera kwenye samli, weka kwenye wali au ugali." },
                { condition: "Magonjwa ya ngozi", recipe: "Kijiko kimoja cha jeera kilichokaangwa na maziwa, kunywa mara mbili kwa siku." }
            ]
        },
        "Pilipili manga": {
            name: "Pilipili manga",
            scientific: "Piper nigrum",
            uses: [
                { condition: "Magonjwa ya ngozi", recipe: "Kijiko kimoja cha unga wa pilipili na samli na asali, kunywa mara mbili kwa siku." },
                { condition: "Kupoteza sauti", recipe: "Changanya pilipili na mafuta ya nazi, paka kwenye koo." },
                { condition: "Kwikwi", recipe: "Kijiko kimoja cha pilipili iliyokaangwa na samli, weka mdomoni." },
                { condition: "Kuumwa tumbo", recipe: "Kijiko kimoja cha pilipili na sukari, kunywa mara mbili kwa siku." }
            ]
        },
        "Karela": {
            name: "Karela (ubwabwa)",
            scientific: "Momordica charantia",
            uses: [
                { condition: "Kuumwa tumbo", recipe: "Juisi ya karela vijiko 5-10 mara mbili kwa siku." },
                { condition: "Kiwango cha sukari", recipe: "Unga wa mbegu za karela kijiko kimoja na maji mara mbili kwa siku." },
                { condition: "Kukosa hamu ya kula", recipe: "Juisi ya karela na maziwa ya mgando mara 1-2." },
                { condition: "Magonjwa ya ngozi", recipe: "Juisi ya karela asubuhi kabla ya kula kitu." }
            ]
        },
        "Kitunguu saumu": {
            name: "Kitunguu saumu",
            scientific: "Allium sativum",
            uses: [
                { condition: "Maumivu ya sikio", recipe: "Tone la juisi ya kitunguu saumu yenye joto kwenye sikio (usitumie kama kuna usaha)." },
                { condition: "Gesi tumboni", recipe: "Juisi ya kitunguu saumu vijiko 6 na asali, kunywa mara mbili kwa siku." },
                { condition: "Mafua na kikohozi", recipe: "Chemsha karafuu za kitunguu saumu na maji, kunywa maji hayo na sukari." },
                { condition: "Maumivu ya viungo", recipe: "Paste ya kitunguu saumu na asali au kwenye chakula, kula mara mbili kwa siku." }
            ]
        },
        "Karafuu": {
            name: "Karafuu",
            scientific: "Syzygium aromaticum",
            uses: [
                { condition: "Kikohozi", recipe: "Tafuna karafuu au kijiko kimoja cha unga na asali mara 2-3 kwa siku." },
                { condition: "Mafua na kwikwi", recipe: "Chemsha karafuu na maji, kunywa maji hayo mara 3-4 kwa siku." },
                { condition: "Kuumwa tumbo", recipe: "Unga wa karafuu na asali mara tatu kwa siku." },
                { condition: "Maumivu ya jino", recipe: "Weka karafuu kwenye jino linalouma." }
            ]
        },
        "Asali": {
            name: "Asali",
            scientific: "Honey",
            uses: [
                { condition: "Unene kupita kiasi", recipe: "Kijiko kimoja cha asali kwenye glasi ya maji asubuhi." },
                { condition: "Kukosa hamu ya kula", recipe: "Asali na pilipili manga mara 3-4 kwa siku." },
                { condition: "Kikohozi", recipe: "Asali na unga wa karafuu mara 3-4." },
                { condition: "Vidonda na majeraha", recipe: "Changanya asali na samli, paka." }
            ]
        },
        "Methi": {
            name: "Methi (ubarwe)",
            scientific: "Trigonella foenum-graecum",
            uses: [
                { condition: "Kiwango cha sukari", recipe: "Unga wa methi kijiko kimoja na maziwa mara mbili kwa siku." },
                { condition: "Maumivu ya mwili", recipe: "Unga wa methi na jeera kwa maziwa ya joto na sukari." },
                { condition: "Kuongeza maziwa ya mama", recipe: "Unga wa methi kijiko kimoja na maziwa na sukari asubuhi." },
                { condition: "Mba (dandruff)", recipe: "Paka paste ya methi kwenye kichwa nusu saa kabla ya kuoga." }
            ]
        },
        "Nazi": {
            name: "Nazi",
            scientific: "Cocos nucifera",
            uses: [
                { condition: "Kiwango cha asidi", recipe: "Maji ya nazi mabichi mara mbili kwa siku." },
                { condition: "Mawe kwenye figo", recipe: "Maji ya nazi mabichi mara mbili kwa siku." },
                { condition: "Majeraha na kuungua", recipe: "Paka mafuta ya nazi mara kwa mara." },
                { condition: "Kukosa maji mwilini (dehydration)", recipe: "Kunywa maji ya nazi mabichi." }
            ]
        },
        "Mwambe": {
            name: "Mwambe (Neem)",
            scientific: "Azadirachta indica",
            uses: [
                { condition: "Magonjwa ya ngozi", recipe: "Juisi ya majani ya mwambe na asali mara mbili kwa siku." },
                { condition: "Vidonda na majeraha", recipe: "Paka paste ya majani ya mwambe yenye joto." },
                { condition: "Minyoo tumboni", recipe: "Chemsha majani ya mwambe, kunywa maji hayo asubuhi kwa siku tatu." },
                { condition: "Mba na ukurutu", recipe: "Chemsha majani ya mwambe, tumia maji hayo kuosha kichwa." }
            ]
        },
        "Ndimu": {
            name: "Ndimu",
            scientific: "Citrus limon",
            uses: [
                { condition: "Kuumwa tumbo", recipe: "Juisi ya ndimu na chumvi kidogo na pilipili kabla ya chakula." },
                { condition: "Kuchoka kwa jua", recipe: "Ndimu moja kwenye glasi ya maji na sukari na chumvi." },
                { condition: "Kutoa damu kwenye ufizi", recipe: "Saga ganda la ndimu, paka kwenye ufizi mara mbili kwa siku." },
                { condition: "Kukosa hamu ya kula", recipe: "Juisi ya ndimu na chumvi na pilipili kabla ya chakula." }
            ]
        },
        "Kitunguu maji": {
            name: "Kitunguu maji",
            scientific: "Allium cepa",
            uses: [
                { condition: "Kuchoka kwa jua", recipe: "Kula kitunguu maji kwa wingi husaidia kuzuia kuchoka." },
                { condition: "Mafua na kikohozi", recipe: "Kwa watoto, chemsha kitunguu maji na sukari nyekundu, kunywa maji hayo." },
                { condition: "Kuhara", recipe: "Kata kitunguu maji, kaanga kwa samli, kula na wali." }
            ]
        },
        "Pilipili ndogo": {
            name: "Pilipili ndogo (Pippali)",
            scientific: "Piper longum",
            uses: [
                { condition: "Kuumwa tumbo", recipe: "Unga wa pilipili ndogo na sukari nyekundu kabla ya chakula mara mbili kwa siku." },
                { condition: "Mafua", recipe: "Unga wa pilipili ndogo na asali mara tatu kwa siku." },
                { condition: "Kikohozi chenye homa", recipe: "Chemsha pilipili ndogo, tangawizi, na pilipili manga, ongeza sukari, kunywa." },
                { condition: "Kuhara", recipe: "Changanya unga wa pilipili ndogo kwenye lita moja ya maziwa ya mgando, gawa mara nne, kunywa." }
            ]
        },
        "Saunf": {
            name: "Saunf (bizari tamu)",
            scientific: "Foeniculum vulgare",
            uses: [
                { condition: "Kuumwa tumbo", recipe: "Unga wa saunf na jeera na chumvi na maji ya moto mara tatu kwa siku." },
                { condition: "Kuhara", recipe: "Unga wa saunf na maziwa ya mgando mara 3-4 kwa siku." },
                { condition: "Maumivu ya tumbo", recipe: "Unga wa saunf na maziwa ya mgando mara 3-4." },
                { condition: "Harufu mbaya mdomoni", recipe: "Tafuna saunf baada ya kula." }
            ]
        },
        "Mchaichai": {
            name: "Mchaichai (Tulsi)",
            scientific: "Ocimum sanctum",
            uses: [
                { condition: "Mafua na kikohozi", recipe: "Juisi ya majani ya mchaichai na asali mara mbili au tatu kwa siku." },
                { condition: "Homa", recipe: "Chemsha majani ya mchaichai na dhania, kunywa mara tatu." },
                { condition: "Mzio wa ngozi", recipe: "Juisi ya mchaichai mara mbili kwa siku." },
                { condition: "Maumivu ya sikio", recipe: "Tone la juisi ya mchaichai yenye joto kwenye sikio (usitumie kama kuna usaha)." }
            ]
        }
    };

    // PLANET_OBESITY_DB – Sayari na unene (zimeandikwa kwa Kiswahili, zenye rangi)
    const PLANET_OBESITY_DB = {
        "Jupiter": {
            name: "Mshtarii (Jupiter)",
            impact: "Kula kupita kiasi",
            percentage: "30%",
            description: "Sayari hii inapanua kila inachogusa. Ikiwa na nguvu kwenye nyota yako, utakuwa na hamu kubwa ya kula na kula kupita kiasi.",
            color: "var(--jupiter)"
        },
        "Sun": {
            name: "Jua (Sun)",
            impact: "Kuumwa tumbo na mmeng'enyo mbaya",
            percentage: "20%",
            description: "Jua likiwa dhaifu, mfumo wako wa kumeng'enya chakula haufanyi kazi vizuri, hivyo chakula kinakaa tumboni na kukufanya unene.",
            color: "var(--sun)"
        },
        "Ketu": {
            name: "Ketu",
            impact: "Kuvimbiwa (constipation)",
            percentage: "15%",
            description: "Ketu ikisumbuliwa, husababisha kuvimbiwa na sumu kujilimbikiza mwilini, hivyo kusababisha unene.",
            color: "var(--ketu)"
        },
        "Mars": {
            name: "Mirihi (Mars)",
            impact: "Ukosefu wa shughuli za mwili",
            percentage: "10%",
            description: "Mars dhaifu hukufanya uwe mvivu na usifanye mazoezi, hivyo kalori hazichomi na unene unakuja.",
            color: "var(--mars)"
        },
        "Saturn": {
            name: "Zohali (Saturn)",
            impact: "Kukosa usingizi vizuri",
            percentage: "7%",
            description: "Zohali likiwa na mvuto mbaya, usingizi wako unakuwa mbaya, na hii huathiri homoni zinazodhibiti uzito.",
            color: "var(--saturn)"
        },
        "Mercury": {
            name: "Zebaki (Mercury)",
            impact: "Homoni kuharibika",
            percentage: "6%",
            description: "Zebaki ikiwa na dosari, homoni za mwili huharibika na kusababisha unene usio wa kawaida.",
            color: "var(--mercury)"
        },
        "Moon": {
            name: "Mwezi (Moon)",
            impact: "Msongo wa mawazo",
            percentage: "5%",
            description: "Mwezi ukiwa na mvuto mbaya, huleta msongo na wasiwasi, na watu wengi hula sana wanapofadhaika.",
            color: "var(--moon)"
        },
        "Rahu": {
            name: "Rahu",
            impact: "Urithi wa kimaumbile (genetics)",
            percentage: "4%",
            description: "Rahu hubeba habari za urithi kutoka kwa wazazi. Kama wazazi walikuwa wanene, uwezekano wa wewe kuwa mnene ni mkubwa.",
            color: "var(--rahu)"
        },
        "Venus": {
            name: "Zuhura (Venus)",
            impact: "Uzee / Ujauzito",
            percentage: "3%",
            description: "Zuhura inahusishwa na uzuri na umri. Baada ya umri fulani au baada ya ujauzito, mwili hubadilika na unene unaweza kutokea.",
            color: "var(--venus)"
        }
    };

    // Vigezo vya programu
    let currentResults = null;
    let currentJina = '', currentS = '', currentM = '', currentJinsia = '';
    let currentZodiacIdx = 1;

    function switchPage(pageId, btnElement) {
        const pages = ['ramli', 'appointment', 'dawa', 'malalamiko'];
        pages.forEach(p => document.getElementById('page-' + p).style.display = 'none');
        document.getElementById('page-' + pageId).style.display = 'block';
        
        document.querySelectorAll('.btn-service').forEach(btn => btn.classList.remove('active'));
        btnElement.classList.add('active');
    }

    // Validations za appointment na dawa
    function validateAppPhone() {
        const code = document.getElementById('app-country-code').value;
        const phone = document.getElementById('app-phone').value.trim();
        const errorDiv = document.getElementById('app-phone-error');
        if (phone === '') { errorDiv.innerText = 'Weka namba yako ya simu.'; return false; }
        if (!/^\d{9}$/.test(phone)) { errorDiv.innerText = 'Namba lazima iwe na tarakimu 9.'; return false; }
        errorDiv.innerText = '';
        return code + phone;
    }
    function validateDawaPhone() {
        const code = document.getElementById('dawa-country-code').value;
        const phone = document.getElementById('dawa-phone').value.trim();
        const errorDiv = document.getElementById('dawa-phone-error');
        if (phone === '') { errorDiv.innerText = 'Weka namba yako ya simu.'; return false; }
        if (!/^\d{9}$/.test(phone)) { errorDiv.innerText = 'Namba lazima iwe na tarakimu 9.'; return false; }
        errorDiv.innerText = '';
        return code + phone;
    }

    function tumaAppointment() {
        const jina = document.getElementById('app-name').value;
        const tarehe = document.getElementById('app-date').value;
        const sababu = document.getElementById('app-reason').value;
        const fullPhone = validateAppPhone();
        if (!fullPhone) return;
        const msg = `*MIADI MPYA*%0A%0AJina: ${jina}%0ATarehe ya kuja: ${tarehe}%0ASababu: ${sababu}%0ANamba ya simu: ${fullPhone}`;
        window.open(`https://wa.me/255762286282?text=${msg}`, '_blank');
    }

    function tumaOda() {
        const dawa = document.getElementById('dawa-type').value;
        const loc = document.getElementById('dawa-location').value;
        const fullPhone = validateDawaPhone();
        if (!fullPhone) return;
        const msg = `*ODA YA DAWA*%0A%0ADawa: ${dawa}%0AMahali: ${loc}%0ANamba ya simu: ${fullPhone}`;
        window.open(`https://wa.me/255762286282?text=${msg}`, '_blank');
    }

    function tumaLalamiko() {
        const txt = document.getElementById('msg-content').value;
        const msg = `*MALALAMIKO*%0A%0AUjumbe: ${txt}`;
        window.open(`https://wa.me/255762286282?text=${msg}`, '_blank');
    }

    function anzaRamli() {
        const jina = document.getElementById('full-name').value.trim();
        const s = parseInt(document.getElementById('birth-day').value);
        const m = parseInt(document.getElementById('birth-month').value);
        const jinsia = document.getElementById('gender').value;

        if (!jina || jina.split(' ').length < 2) {
            alert('Tafadhali weka jina lako kamili (angalau maneno mawili).');
            return;
        }

        currentJina = jina;
        currentS = s;
        currentM = m;
        currentJinsia = jinsia;

        // Determine zodiac index (simplified)
        let idx = 1;
        if ((m == 3 && s >= 21) || (m == 4 && s <= 19)) idx = 1;
        else if ((m == 4 && s >= 20) || (m == 5 && s <= 20)) idx = 2;
        else if ((m == 5 && s >= 21) || (m == 6 && s <= 20)) idx = 3;
        else if ((m == 6 && s >= 21) || (m == 7 && s <= 22)) idx = 4;
        else if ((m == 7 && s >= 23) || (m == 8 && s <= 22)) idx = 5;
        else if ((m == 8 && s >= 23) || (m == 9 && s <= 22)) idx = 6;
        else if ((m == 9 && s >= 23) || (m == 10 && s <= 22)) idx = 7;
        else if ((m == 10 && s >= 23) || (m == 11 && s <= 21)) idx = 8;
        else if ((m == 11 && s >= 22) || (m == 12 && s <= 21)) idx = 9;
        else if ((m == 12 && s >= 22) || (m == 1 && s <= 19)) idx = 10;
        else if ((m == 1 && s >= 20) || (m == 2 && s <= 18)) idx = 11;
        else if ((m == 2 && s >= 19) || (m == 3 && s <= 20)) idx = 12;
        else idx = (m % 12) + 1;
        currentZodiacIdx = idx;

        // Onyesha warning kwa sekunde 2 kisha loading
        document.getElementById('page-ramli').style.display = 'none';
        document.getElementById('warning-area').style.display = 'block';
        
        setTimeout(() => {
            document.getElementById('warning-area').style.display = 'none';
            document.getElementById('loading-area').style.display = 'block';
        }, 2000);

        setTimeout(() => {
            document.getElementById('loading-area').style.display = 'none';
            document.getElementById('cards-container').style.display = 'flex';
            document.getElementById('send-results-container').style.display = 'block';
            document.getElementById('donation-section').style.display = 'block';
            chakataRamli(jina, idx, jinsia);
        }, 5000);
    }

    function chakataRamli(jina, zodiacIdx, jinsia) {
        const h1 = jina[0].toUpperCase();
        
        const d = NYOTA_DESC[zodiacIdx] || NYOTA_DESC[1];
        const sifaData = SIFA_DB[h1] || SIFA_DB['A'];
        const zodiacData = ZODIAC_DB[zodiacIdx] || ZODIAC_DB[1];
        const jinaTraits = HERUFI_DB[h1] || ["Wewe ni mwenye heri","Wewe ni mtafutaji","Wewe ni mkarimu"];

        // Tayarisha sifa za jina (5 kutoka herufi + 5 kutoka zodiac)
        const jinaSifaZote = [];
        for (let i=0; i<5; i++) {
            if (jinaTraits[i]) jinaSifaZote.push("🔹 " + jinaTraits[i]);
        }
        for (let i=0; i<5; i++) {
            if (zodiacData.traits[i]) jinaSifaZote.push("⭐ " + zodiacData.traits[i]);
        }

        // Tayarisha orodha za tiba 5 kutoka kwenye AYURVEDA_DB
        const tibaZote = Object.values(AYURVEDA_DB);
        const tibaChache = tibaZote.slice(0,5).map(t => t.name + ": " + t.uses[0].recipe);

        currentResults = {
            sifa: sifaData.traits.slice(0, 15),
            kazi: sifaData.careers,
            hatari: d.h.slice(0, 15),
            lishe: d.d.slice(0, 5),
            tibaAsili: tibaChache,
            jinaSifa: jinaSifaZote
        };

        // Kadi ya kwanza (Jina na zodiac)
        let cardsHtml = `
            <div class="card" onclick="geuzaKadi(this)">
                <div class="card-inner">
                    <div class="card-back">
                        ${jina.toUpperCase()}
                        <small style="display:block; margin-top:10px;">Gusa kadi kuona sifa zako</small>
                    </div>
                    <div class="card-front"><h3>${jina.toUpperCase()} - ${zodiacData.name}</h3><ul><li>${jinaSifaZote.join('</li><li>')}</li></ul></div>
                </div>
            </div>
        `;

        // Kadi ya pili (Sifa 15)
        cardsHtml += `
            <div class="card" onclick="geuzaKadi(this)">
                <div class="card-inner">
                    <div class="card-back">
                        SIFA ZAKO 15
                        <small style="display:block; margin-top:10px;">Gusa kadi kuona maelezo</small>
                    </div>
                    <div class="card-front"><h3>SIFA 15 ZA TABIA YAKO</h3><ul><li>${sifaData.traits.slice(0,15).join('</li><li>')}</li></ul></div>
                </div>
            </div>
        `;

        // Kadi ya tatu (Kazi)
        let kaziHtml = '';
        sifaData.careers.forEach(k => {
            kaziHtml += `<div class="job-item"><img src="${k.image}" class="job-image" alt="${k.title}"><div><strong>${k.title}</strong><br>${k.desc}</div></div>`;
        });
        cardsHtml += `
            <div class="card" onclick="geuzaKadi(this)">
                <div class="card-inner">
                    <div class="card-back">
                        KAZI 5 ZINAZOKUFAA
                        <small style="display:block; margin-top:10px;">Gusa kadi kuona maelezo</small>
                    </div>
                    <div class="card-front"><h3>KAZI ZINAZOKUFAA</h3>${kaziHtml}</div>
                </div>
            </div>
        `;

        // Kadi ya nne (Hatari za afya)
        cardsHtml += `
            <div class="card" onclick="geuzaKadi(this)">
                <div class="card-inner">
                    <div class="card-back">
                        HATARI ZA KIAFYA 15
                        <small style="display:block; margin-top:10px;">Gusa kadi kuona maelezo</small>
                    </div>
                    <div class="card-front">
                        <h3>HATARI 15</h3>
                        <ul><li>${d.h.slice(0,15).join('</li><li>')}</li></ul>
                        <div class="note-box">
                            ⚠️ Ni muhimu sana ukaanza kutumia Zetrone maana matatizo mengine bado hayajaanza kuonekana. Zetrone inaweza kukusaidia.
                        </div>
                    </div>
                </div>
            </div>
        `;

        // Kadi ya tano (Tiba za asili)
        cardsHtml += `
            <div class="card" onclick="geuzaKadi(this)">
                <div class="card-inner">
                    <div class="card-back">
                        TIBA ZA ASILI (5)
                        <small style="display:block; margin-top:10px;">Gusa kadi kuona maelezo</small>
                    </div>
                    <div class="card-front">
                        <div class="red-alert">
                            ⚠️ Hizi ni njia za kuzingatia kwa afya yako kulingana na mwili wa afya yako. Vyema ukawa unazitumia ingawa zinaweza zisimalize tatizo lakini zitaendelea kuboresha afya yako.
                        </div>
                        <ul><li>${tibaChache.join('</li><li>')}</li></ul>
                    </div>
                </div>
            </div>
        `;

        // Kadi ya sita (Sayari na unene - colorful)
        let planetHtml = '';
        Object.values(PLANET_OBESITY_DB).forEach(p => {
            planetHtml += `<div class="planet-colorful" style="background: ${p.color}; color: black; padding: 8px; margin: 5px 0; border-radius: 5px;"><strong>${p.name}</strong> - ${p.impact} (${p.percentage})<br><small>${p.description}</small></div>`;
        });
        cardsHtml += `
            <div class="card" onclick="geuzaKadi(this)">
                <div class="card-inner">
                    <div class="card-back">
                        SAYARI NA UNENE
                        <small style="display:block; margin-top:10px;">Gusa kadi kuona maelezo</small>
                    </div>
                    <div class="card-front"><h3>USHAWISHI WA SAYARI</h3>${planetHtml}</div>
                </div>
            </div>
        `;

        document.getElementById('cards-container').innerHTML = cardsHtml;
    }

    // Kazi ya kugeuza na kupanua kadi
    window.geuzaKadi = function(card) {
        // Kwanza ondoa class 'expanded' kwenye kadi zote
        document.querySelectorAll('.card').forEach(c => {
            if (c !== card) {
                c.classList.remove('expanded');
                c.classList.remove('flipped');
            }
        });
        // Badilisha hali ya kadi iliyobofywa: expanded na flipped
        card.classList.toggle('expanded');
        card.classList.toggle('flipped');
    };

    function tumaMatokeoKwaWhatsApp() {
        if (!currentResults) {
            alert('Matokeo bado hayajapatikana. Subiri kidogo.');
            return;
        }
        // Tuma taarifa zote kwa WhatsApp (jina, tarehe, jinsia na matokeo)
        let message = `*MAJIBU YA RAMLI SAFI*%0A%0A`;
        message += `Jina: ${currentJina}%0A`;
        message += `Tarehe: ${currentS}/${currentM}%0A`;
        message += `Jinsia: ${currentJinsia}%0A`;
        message += `Zodiac: ${ZODIAC_DB[currentZodiacIdx].name}%0A%0A`;
        message += `*SIFA ZA JINA (10)*%0A`;
        currentResults.jinaSifa.slice(0,5).forEach(t => message += `- ${t}%0A`);
        message += `%0A*SIFA ZAKO (15)*%0A`;
        currentResults.sifa.slice(0,3).forEach(t => message += `- ${t}%0A`);
        message += `%0A*KAZI ZINAZOKUFAA*%0A`;
        currentResults.kazi.slice(0,3).forEach(k => message += `- ${k.title}%0A`);
        message += `%0A*HATARI ZA KIAFYA*%0A`;
        currentResults.hatari.slice(0,3).forEach(h => message += `- ${h}%0A`);
        window.open(`https://wa.me/255762286282?text=${message}`, '_blank');
    }

    function onyeshaNambaZaKuchangia(ndio) {
        if (ndio) {
            document.getElementById('donation-details').style.display = 'block';
        } else {
            document.getElementById('donation-details').style.display = 'none';
        }
    }
</script>
</body>
</html>
