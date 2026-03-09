<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎮 Tebak Emoji Mabar 2-4 Orang</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background: linear-gradient(145deg, #2b3a4e 0%, #1d2a36 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0;
            padding: 16px;
        }
        .game-container {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(8px);
            border-radius: 40px;
            padding: 24px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.6);
            width: 100%;
            max-width: 600px;
            border: 2px solid #ffd966;
        }
        h1 {
            text-align: center;
            color: #ffd966;
            margin-top: 0;
            margin-bottom: 24px;
            font-size: 2.2rem;
            text-shadow: 4px 4px 0 #b3541c;
            letter-spacing: 2px;
        }
        .setup-panel, .game-panel {
            background: #fefae0;
            border-radius: 32px;
            padding: 24px;
            box-shadow: inset 0 2px 8px rgba(0,0,0,0.1), 0 8px 0 #a3b18a;
            border: 2px solid #a3b18a;
        }
        .setup-panel h2, .game-panel h2 {
            color: #283618;
            margin-top: 0;
            text-align: center;
            border-bottom: 3px dashed #bc6c25;
            padding-bottom: 12px;
        }
        label {
            font-weight: bold;
            color: #283618;
            display: block;
            margin: 16px 0 8px;
        }
        select, input[type="text"] {
            width: 100%;
            padding: 14px 18px;
            font-size: 1.1rem;
            border-radius: 60px;
            border: 2px solid #bc6c25;
            background: #fff;
            outline: none;
            transition: 0.2s;
        }
        select:focus, input:focus {
            border-color: #faa307;
            box-shadow: 0 0 0 3px #ffe68f;
        }
        .nama-inputs {
            margin: 20px 0;
        }
        .nama-inputs input {
            margin-bottom: 12px;
        }
        .btn {
            background: #faa307;
            border: none;
            color: #283618;
            font-weight: bold;
            font-size: 1.3rem;
            padding: 16px 24px;
            border-radius: 60px;
            width: 100%;
            cursor: pointer;
            border-bottom: 6px solid #b3541c;
            transition: 0.07s ease;
            margin-top: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .btn:active {
            border-bottom-width: 2px;
            transform: translateY(4px);
        }
        .btn.secondary {
            background: #a7c957;
            border-bottom-color: #6b8e4c;
        }
        .btn.danger {
            background: #e85d5d;
            border-bottom-color: #9d2b2b;
            color: white;
        }
        .game-info {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
            background: #a7c957;
            padding: 16px 20px;
            border-radius: 60px;
            color: #283618;
            font-weight: bold;
            border: 3px solid #6b8e4c;
        }
        .turn-box {
            background: #283618;
            color: #fefae0;
            padding: 8px 24px;
            border-radius: 40px;
            font-size: 1.3rem;
        }
        .scores {
            display: flex;
            gap: 16px;
            flex-wrap: wrap;
            justify-content: center;
        }
        .score-badge {
            background: #fefae0;
            padding: 6px 16px;
            border-radius: 40px;
            border: 2px solid #283618;
            font-size: 1.2rem;
        }
        .emoji-display {
            font-size: 8rem;
            text-align: center;
            background: #fff;
            border-radius: 60px;
            padding: 20px;
            margin: 20px 0;
            border: 6px dashed #bc6c25;
            box-shadow: inset 0 0 20px #ffe68f;
            line-height: 1.2;
            word-break: break-word;
        }
        .input-area {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-top: 20px;
        }
        .input-area input {
            text-align: center;
            font-size: 1.3rem;
        }
        .action-buttons {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }
        .action-buttons .btn {
            flex: 1;
            font-size: 1rem;
            padding: 14px 0;
        }
        .message {
            text-align: center;
            font-weight: bold;
            color: #bc6c25;
            min-height: 2rem;
            margin: 12px 0;
            font-size: 1.2rem;
        }
        .footer {
            text-align: center;
            color: #ffe68f;
            margin-top: 16px;
        }
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
<div class="game-container">
    <h1>🔎 TEBAK EMOJI</h1>

    <!-- PANEL SETUP -->
    <div id="setupPanel" class="setup-panel">
        <h2>👥 Siapa yang main?</h2>
        <label>Jumlah pemain</label>
        <select id="playerCount">
            <option value="2">2 orang</option>
            <option value="3" selected>3 orang</option>
            <option value="4">4 orang</option>
        </select>

        <div id="namaInputs" class="nama-inputs">
            <!-- diisi javascript -->
        </div>

        <button id="startGameBtn" class="btn">🎮 MULAI GAME 🎮</button>
    </div>

    <!-- PANEL GAME -->
    <div id="gamePanel" class="game-panel hidden">
        <div class="game-info">
            <span class="turn-box" id="turnDisplay">Giliran: -</span>
            <div class="scores" id="scoresDisplay"></div>
        </div>

        <div id="emojiDisplay" class="emoji-display">❓</div>

        <div class="input-area">
            <input type="text" id="answerInput" placeholder="Jawaban..." autocomplete="off">
            <div class="action-buttons">
                <button id="checkBtn" class="btn">✅ CEK</button>
                <button id="skipBtn" class="btn secondary">⏭️ SKIP</button>
            </div>
        </div>

        <div id="messageBox" class="message"></div>

        <button id="resetBtn" class="btn danger">🔄 GANTI PEMAIN</button>
    </div>

    <div class="footer">mabar bareng 2-4 orang — seru giliran!</div>
</div>

<script>
    (function() {
        // ==================== DATABASE PERTANYAAN ====================
        const questionsDB = [
            { emoji: "🐱", answer: "kucing" },
            { emoji: "🐶", answer: "anjing" },
            { emoji: "🐭", answer: "tikus" },
            { emoji: "🐹", answer: "hamster" },
            { emoji: "🐰", answer: "kelinci" },
            { emoji: "🦊", answer: "rubah" },
            { emoji: "🐻", answer: "beruang" },
            { emoji: "🐼", answer: "panda" },
            { emoji: "🐨", answer: "koala" },
            { emoji: "🦁", answer: "singa" },
            { emoji: "🐮", answer: "sapi" },
            { emoji: "🦓", answer: "zebra" },
            { emoji: "🐸", answer: "katak" },
            { emoji: "🐙", answer: "gurita" },
            { emoji: "🦐", answer: "udang" },
            { emoji: "🐧", answer: "pinguin" },
            { emoji: "🦆", answer: "bebek" },
            { emoji: "🦅", answer: "elang" },
            { emoji: "🦉", answer: "burung hantu" },
            { emoji: "🦇", answer: "kelelawar" },
            { emoji: "🐝", answer: "lebah" },
            { emoji: "🐞", answer: "kepik" },
            { emoji: "🦋", answer: "kupu kupu" },
            { emoji: "🐌", answer: "siput" },
            { emoji: "🐢", answer: "kura kura" },
            { emoji: "🐍", answer: "ular" },
            { emoji: "🦎", answer: "kadal" },
            { emoji: "🦖", answer: "t rex" },
            { emoji: "🦕", answer: "dinosaurus" },
            { emoji: "🐉", answer: "naga" },
            { emoji: "🍕", answer: "pizza" },
            { emoji: "🍔", answer: "burger" },
            { emoji: "🍟", answer: "kentang goreng" },
            { emoji: "🌮", answer: "taco" },
            { emoji: "🍣", answer: "sushi" },
            { emoji: "🍜", answer: "mie" },
            { emoji: "🍝", answer: "spaghetti" },
            { emoji: "🍦", answer: "es krim" },
            { emoji: "🍩", answer: "donat" },
            { emoji: "🍪", answer: "kue kering" },
            { emoji: "🎂", answer: "kue ulang tahun" },
            { emoji: "🍫", answer: "cokelat" },
            { emoji: "🍬", answer: "permen" },
            { emoji: "☕", answer: "kopi" },
            { emoji: "🥤", answer: "soda" },
            { emoji: "🧃", answer: "jus" },
            { emoji: "🍺", answer: "bir" },
            { emoji: "🥥", answer: "kelapa" },
            { emoji: "🥝", answer: "kiwi" },
            { emoji: "🍓", answer: "stroberi" },
            { emoji: "🍉", answer: "semangka" },
            { emoji: "🍌", answer: "pisang" },
            { emoji: "🥑", answer: "alpukat" },
            { emoji: "🌽", answer: "jagung" },
            { emoji: "🥕", answer: "wortel" },
            { emoji: "🧅", answer: "bawang" },
            { emoji: "🥦", answer: "brokoli" },
            { emoji: "🍄", answer: "jamur" },
            { emoji: "🌶️", answer: "cabai" },
            { emoji: "🍞", answer: "roti" },
            { emoji: "🥐", answer: "croissant" },
            { emoji: "🥨", answer: "pretzel" },
            { emoji: "🧀", answer: "keju" },
            { emoji: "🍳", answer: "telur goreng" },
            { emoji: "🥓", answer: "bacon" },
            { emoji: "🍗", answer: "paha ayam" },
            { emoji: "🥩", answer: "steak" },
            { emoji: "🚗", answer: "mobil" },
            { emoji: "✈️", answer: "pesawat" },
            { emoji: "🚲", answer: "sepeda" },
            { emoji: "🚂", answer: "kereta" },
            { emoji: "🚀", answer: "roket" },
            { emoji: "🏀", answer: "basket" },
            { emoji: "⚽", answer: "sepak bola" },
            { emoji: "🎮", answer: "game" },
            { emoji: "📱", answer: "handphone" },
            { emoji: "💻", answer: "komputer" },
            { emoji: "☎️", answer: "telepon" },
            { emoji: "⌚", answer: "jam tangan" },
            { emoji: "📷", answer: "kamera" },
            { emoji: "🔫", answer: "pistol" },
            { emoji: "💣", answer: "bom" },
            { emoji: "🧨", answer: "petasan" },
            { emoji: "🔪", answer: "pisau" },
            { emoji: "🪓", answer: "kapak" },
            { emoji: "🏠", answer: "rumah" },
            { emoji: "🏥", answer: "rumah sakit" },
            { emoji: "🏫", answer: "sekolah" },
            { emoji: "⛪", answer: "gereja" },
            { emoji: "🕌", answer: "masjid" },
            { emoji: "🗼", answer: "menara" },
            { emoji: "🌋", answer: "gunung berapi" },
            { emoji: "🏝️", answer: "pulau" },
            { emoji: "🏜️", answer: "gurun" },
            { emoji: "🌲", answer: "pohon" },
            { emoji: "🌵", answer: "kaktus" },
            { emoji: "🌻", answer: "bunga matahari" },
            { emoji: "🌹", answer: "mawar" },
            { emoji: "🌸", answer: "bunga sakura" },
            { emoji: "🌺", answer: "bunga sepatu" },
            { emoji: "👻", answer: "hantu" },
            { emoji: "🎃", answer: "halloween" },
            { emoji: "🤖", answer: "robot" },
            { emoji: "👽", answer: "alien" },
            { emoji: "🧛", answer: "vampir" },
            { emoji: "🧟", answer: "zombie" },
            { emoji: "🧙", answer: "penyihir" },
            { emoji: "🧚", answer: "peri" },
            { emoji: "🧜", answer: "putri duyung" },
            { emoji: "🦸", answer: "pahlawan" },
            { emoji: "🦹", answer: "penjahat" },
            { emoji: "👮", answer: "polisi" },
            { emoji: "👩‍🚒", answer: "pemadam kebakaran" },
            { emoji: "👨‍⚕️", answer: "dokter" },
            { emoji: "👩‍🏫", answer: "guru" },
            { emoji: "👨‍🍳", answer: "koki" },
            { emoji: "👩‍🌾", answer: "petani" },
            { emoji: "👨‍🚀", answer: "astronot" },
            { emoji: "🎨", answer: "lukisan" },
            { emoji: "🎭", answer: "teater" },
            { emoji: "🎤", answer: "mic" },
            { emoji: "🎧", answer: "headphone" },
            { emoji: "🎸", answer: "gitar" },
            { emoji: "🥁", answer: "drum" },
            { emoji: "🎺", answer: "terompet" },
            { emoji: "🎻", answer: "biola" },
            { emoji: "🪕", answer: "banjo" },
            { emoji: "🎲", answer: "dadu" },
            { emoji: "♟️", answer: "pion catur" },
            { emoji: "🎯", answer: "target" },
            { emoji: "🎳", answer: "bowling" },
            { emoji: "⚾", answer: "baseball" },
            { emoji: "🥊", answer: "tinju" },
            { emoji: "🥋", answer: "beladiri" },
            { emoji: "🛹", answer: "skateboard" },
            { emoji: "🛴", answer: "skuter" },
            { emoji: "🚁", answer: "helikopter" },
            { emoji: "🛸", answer: "ufo" },
            { emoji: "🌍", answer: "bumi" },
            { emoji: "🌕", answer: "bulan" },
            { emoji: "☀️", answer: "matahari" },
            { emoji: "⭐", answer: "bintang" },
            { emoji: "🌈", answer: "pelangi" },
            { emoji: "⛈️", answer: "badai" },
            { emoji: "❄️", answer: "salju" },
            { emoji: "🔥", answer: "api" },
            { emoji: "💧", answer: "air" },
            { emoji: "🌊", answer: "ombak" },
        ];

        // ==================== UTILS ====================
        function normalize(str) {
            return str.toLowerCase().replace(/[^a-z0-9]/g, '');
        }

        // ==================== STATE GAME ====================
        let players = [];               // array nama
        let scores = [];                // array poin
        let currentPlayerIndex = 0;
        let currentQuestion = null;      // objek { emoji, answer }

        // Elemen DOM
        const setupPanel = document.getElementById('setupPanel');
        const gamePanel = document.getElementById('gamePanel');
        const playerCountSelect = document.getElementById('playerCount');
        const namaInputsDiv = document.getElementById('namaInputs');
        const startBtn = document.getElementById('startGameBtn');
        const resetBtn = document.getElementById('resetBtn');
        const turnDisplay = document.getElementById('turnDisplay');
        const scoresDisplay = document.getElementById('scoresDisplay');
        const emojiDisplay = document.getElementById('emojiDisplay');
        const answerInput = document.getElementById('answerInput');
        const checkBtn = document.getElementById('checkBtn');
        const skipBtn = document.getElementById('skipBtn');
        const messageBox = document.getElementById('messageBox');

        // ==================== FUNGSI UPDATE UI ====================
        function updateNamaInputs() {
            const count = parseInt(playerCountSelect.value);
            let html = '';
            for (let i = 1; i <= count; i++) {
                html += `<input type="text" id="nama${i}" placeholder="Nama pemain ${i}" value="Pemain ${i}" required>`;
            }
            namaInputsDiv.innerHTML = html;
        }

        // Ambil nama dari input
        function getNamaArray() {
            const count = parseInt(playerCountSelect.value);
            const names = [];
            for (let i = 1; i <= count; i++) {
                const input = document.getElementById(`nama${i}`);
                let val = input ? input.value.trim() : `Pemain ${i}`;
                if (val === '') val = `Pemain ${i}`;
                names.push(val);
            }
            return names;
        }

        // Acak pertanyaan
        function getRandomQuestion() {
            const randomIndex = Math.floor(Math.random() * questionsDB.length);
            return questionsDB[randomIndex];
        }

        // Update tampilan giliran & skor
        function updateGameUI() {
            // Giliran
            if (players.length > 0) {
                turnDisplay.textContent = `🎯 Giliran: ${players[currentPlayerIndex]}`;
            } else {
                turnDisplay.textContent = `🎯 Giliran: -`;
            }

            // Skor
            let scoresHtml = '';
            players.forEach((p, i) => {
                scoresHtml += `<span class="score-badge">${p} : ${scores[i]}</span>`;
            });
            scoresDisplay.innerHTML = scoresHtml;

            // Emoji
            if (currentQuestion) {
                emojiDisplay.textContent = currentQuestion.emoji;
            } else {
                emojiDisplay.textContent = '❓';
            }

            // Kosongkan input dan message
            answerInput.value = '';
            messageBox.textContent = '';
        }

        // Pindah giliran (dan opsional ganti pertanyaan)
        function nextTurn(changeQuestion = true) {
            // Pindah ke pemain berikutnya
            currentPlayerIndex = (currentPlayerIndex + 1) % players.length;

            if (changeQuestion) {
                currentQuestion = getRandomQuestion();
            }

            updateGameUI();
            answerInput.focus();
        }

        // Mulai game
        function startGame() {
            players = getNamaArray();
            if (players.length < 2) {
                alert('Minimal 2 pemain!');
                return;
            }
            scores = new Array(players.length).fill(0);
            currentPlayerIndex = 0;
            currentQuestion = getRandomQuestion();

            // Sembunyikan setup, tampilkan game
            setupPanel.classList.add('hidden');
            gamePanel.classList.remove('hidden');

            updateGameUI();
            answerInput.focus();
        }

        // Reset ke setup
        function resetToSetup() {
            setupPanel.classList.remove('hidden');
            gamePanel.classList.add('hidden');
            players = [];
            scores = [];
            currentQuestion = null;
            // Refresh input nama sesuai jumlah
            updateNamaInputs();
        }

        // ==================== EVENT LISTENER ====================
        playerCountSelect.addEventListener('change', updateNamaInputs);
        updateNamaInputs(); // inisialisasi

        startBtn.addEventListener('click', startGame);

        resetBtn.addEventListener('click', resetToSetup);

        // Tombol CEK jawaban
        checkBtn.addEventListener('click', function() {
            if (!currentQuestion || players.length === 0) return;

            const jawaban = answerInput.value.trim();
            if (jawaban === '') {
                messageBox.textContent = '✏️ Tulis jawaban dulu!';
                return;
            }

            const normalizedAnswer = normalize(jawaban);
            const normalizedCorrect = normalize(currentQuestion.answer);

            if (normalizedAnswer === normalizedCorrect) {
                // BENAR
                scores[currentPlayerIndex] += 1;
                messageBox.textContent = `✅ Benar! +1 poin untuk ${players[currentPlayerIndex]}`;
                // Giliran berikutnya dengan pertanyaan baru
                nextTurn(true);
            } else {
                // SALAH
                messageBox.textContent = `❌ Salah! Giliran pindah.`;
                // Giliran berikutnya dengan pertanyaan TETAP (changeQuestion = false)
                nextTurn(false);
            }
        });

        // Tombol SKIP (ganti pertanyaan, pindah giliran)
        skipBtn.addEventListener('click', function() {
            if (!currentQuestion || players.length === 0) return;
            messageBox.textContent = `⏩ Skip! Pertanyaan diganti.`;
            nextTurn(true); // ganti pertanyaan dan pindah giliran
        });

        // Biarkan enter di input memicu tombol CEK
        answerInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                e.preventDefault();
                checkBtn.click();
            }
        });

        // Jaga agar saat jumlah pemain berubah, input nama menyesuaikan
        // Sudah di atas

    })();
</script>
</body>
</html>
