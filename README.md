<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: English Practice</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #009688 0%, #4CAF50 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #00796b, #009688);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 { margin-bottom: 10px; }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            background: white;
            color: #555;
            transition: all 0.2s ease;
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #00796b, #009688);
            color: white;
            transform: translateY(-2px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 350px;
        }

        .game-section.active { display: block; }

        .word-bank {
            background: #e0f2f1;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #009688;
        }

        .word-option {
            display: inline-block;
            background: #009688;
            color: white;
            padding: 8px 14px;
            border-radius: 20px;
            font-weight: bold;
            margin: 4px;
        }

        .question {
            background: #f8f9fa;
            padding: 18px;
            border-radius: 12px;
            margin-bottom: 15px;
            border-left: 4px solid #009688;
        }

        .fill-blank {
            border: 2px solid #ddd;
            padding: 6px 10px;
            border-radius: 8px;
            min-width: 120px;
        }

        .fill-blank-pron {
            display: inline-block;
            min-width: 120px;
            border-bottom: 2px solid #00796b;
            padding: 3px 2px;
            font-weight: bold;
        }

        .feedback {
            margin-top: 8px;
            padding: 10px;
            border-radius: 8px;
            font-weight: bold;
            display: none;
        }

        .feedback.correct {
            background: #E8F5E9;
            color: #2E7D32;
        }

        .feedback.incorrect {
            background: #FFEBEE;
            color: #C62828;
        }

        .check-btn, .reset-btn {
            padding: 10px 22px;
            border-radius: 25px;
            border: none;
            cursor: pointer;
            font-size: 15px;
            margin: 8px 4px 0 0;
        }

        .check-btn { background: #009688; color: white; }
        .reset-btn { background: #F44336; color: white; }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #00796b;
            color: white;
            padding: 10px 18px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        .vocabulary-list .vocabulary-item {
            background: #f8f9fa;
            padding: 18px;
            border-radius: 10px;
            margin-bottom: 16px;
        }

        .vocabulary-item h3 {
            margin-bottom: 6px;
        }

        .vocabulary-item button {
            margin-left: 8px;
            padding: 4px 10px;
            border-radius: 15px;
            border: none;
            cursor: pointer;
            font-size: 13px;
            background: #FF9800;
            color: white;
        }

        .match-col {
            width: 48%;
            display: inline-block;
            vertical-align: top;
        }

        .match-item {
            background: white;
            border-radius: 10px;
            padding: 10px;
            margin: 6px 0;
            border: 2px solid #ddd;
            cursor: pointer;
        }

        .match-item.selected {
            background: #B2DFDB;
            border-color: #009688;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #388E3C;
            cursor: default;
        }

        .pron-btn {
            padding: 6px 12px;
            border-radius: 18px;
            border: none;
            cursor: pointer;
            font-size: 14px;
            background: #00796b;
            color: white;
            margin-left: 6px;
            display: inline-flex;
            align-items: center;
            gap: 4px;
        }

        @media (max-width: 768px) {
            .match-col { width: 100%; display: block; }
            .score { position: static; margin-bottom: 10px; text-align: center; }
        }
    </style>
</head>
<body>
<div class="score">Score: <span id="score">0</span>/15</div>

<div class="container">
    <div class="header">
        <h1>Vocabulary Game: English Practice</h1>
        <p>Practice the words: dive, clean, bit, how long ago, both</p>
    </div>

    <div class="nav-buttons">
        <button class="nav-btn active" onclick="showSection('vocabulary', event)">Vocabulary List</button>
        <button class="nav-btn" onclick="showSection('fill-gaps', event)">Fill in the Gaps</button>
        <button class="nav-btn" onclick="showSection('matching', event)">Match Definitions</button>
        <button class="nav-btn" onclick="showSection('pronunciation', event)">Fill in the Gaps (Pronunciation)</button>
    </div>

    <!-- VOCABULARY SECTION -->
    <div id="vocabulary" class="game-section active">
        <h2 style="text-align:center; margin-bottom:20px;">Vocabulary List</h2>
        <div class="vocabulary-list">
            <div class="vocabulary-item">
                <h3>dive (tuffarsi)
                    <button onclick="speakWord('dive')">▶️ Hear</button>
                </h3>
                <p><strong>Italian meaning:</strong> tuffarsi</p>
                <p class="example">I love to dive into the sea.</p>
            </div>

            <div class="vocabulary-item">
                <h3>clean (pulire)
                    <button onclick="speakWord('clean')">▶️ Hear</button>
                </h3>
                <p><strong>Italian meaning:</strong> pulire</p>
                <p class="example">I need to clean my room.</p>
            </div>

            <div class="vocabulary-item">
                <h3>bit (un po')
                    <button onclick="speakWord('bit')">▶️ Hear</button>
                </h3>
                <p><strong>Italian meaning:</strong> un po'</p>
                <p class="example">Can you speak a bit slower?</p>
            </div>

            <div class="vocabulary-item">
                <h3>how long ago (quanto tempo fa)
                    <button onclick="speakWord('how long ago')">▶️ Hear</button>
                </h3>
                <p><strong>Italian meaning:</strong> quanto tempo fa</p>
                <p class="example">How long ago did you move here?</p>
            </div>

            <div class="vocabulary-item">
                <h3>both (entrambi)
                    <button onclick="speakWord('both')">▶️ Hear</button>
                </h3>
                <p><strong>Italian meaning:</strong> entrambi</p>
                <p class="example">Both of my friends came to visit.</p>
            </div>
        </div>
    </div>

    <!-- FILL IN THE GAPS (WRITING) -->
    <div id="fill-gaps" class="game-section">
        <div class="word-bank">
            <h3>Word Bank</h3>
            <span class="word-option">dive</span>
            <span class="word-option">clean</span>
            <span class="word-option">bit</span>
            <span class="word-option">how long ago</span>
            <span class="word-option">both</span>
        </div>
        <div id="writing-container"></div>
        <button class="check-btn" onclick="checkWriting()">Check Answers</button>
        <button class="reset-btn" onclick="resetWriting()">Reset</button>
    </div>

    <!-- MATCHING -->
    <div id="matching" class="game-section">
        <h2 style="text-align:center; margin-bottom:15px;">Match Definitions</h2>
        <div>
            <div class="match-col">
                <h3>Words</h3>
                <div class="match-item" data-word="dive" onclick="selectMatch(this)">dive</div>
                <div class="match-item" data-word="clean" onclick="selectMatch(this)">clean</div>
                <div class="match-item" data-word="bit" onclick="selectMatch(this)">bit</div>
                <div class="match-item" data-word="how long ago" onclick="selectMatch(this)">how long ago</div>
                <div class="match-item" data-word="both" onclick="selectMatch(this)">both</div>
            </div>
            <div class="match-col">
                <h3>Definitions</h3>
                <div id="definitions-container"></div>
            </div>
        </div>
    </div>

    <!-- PRONUNCIATION GAPS -->
    <div id="pronunciation" class="game-section">
        <h2 style="text-align:center; margin-bottom:15px;">Fill in the Gaps (Pronunciation)</h2>
        <p style="text-align:center; margin-bottom:10px;">🎤 Say the correct word to fill each gap.</p>
        <div id="pron-gaps-container"></div>
    </div>
</div>

<script>
    // -------- SPEECH SYNTHESIS (AUDIO) --------
    function speakWord(word) {
        const u = new SpeechSynthesisUtterance(word);
        u.lang = "en-US";
        speechSynthesis.speak(u);
    }

    // -------- DATA --------
    const writingSentences = [
        { text: "I want to <input class='fill-blank' data-answer='dive' placeholder='answer'> into the water.", answer: "dive" },
        { text: "Please <input class='fill-blank' data-answer='clean' placeholder='answer'> your room before dinner.", answer: "clean" },
        { text: "Can you wait a <input class='fill-blank' data-answer='bit' placeholder='answer'>?", answer: "bit" },
        { text: "<input class='fill-blank' data-answer='how long ago' placeholder='answer'> did you see her?", answer: "how long ago" },
        { text: "<input class='fill-blank' data-answer='both' placeholder='answer'> my cousins live in London.", answer: "both" }
    ];

    const definitionItems = [
        { word: "dive", text: "to jump into water" },
        { word: "clean", text: "to remove dirt" },
        { word: "bit", text: "a small amount" },
        { word: "how long ago", text: "asks how much time has passed" },
        { word: "both", text: "refers to two things together" }
    ];

    const pronSentences = [
        { before: "I want to ___ into the sea.", answer: "dive" },
        { before: "Can you ___ the kitchen later?", answer: "clean" },
        { before: "She was only a ___ late.", answer: "bit" },
        { before: "___ did you start learning English?", answer: "how long ago" },
        { before: "___ of them enjoyed the trip.", answer: "both" }
    ];

    // -------- STATE --------
    let writingCorrect = 0;
    let matchingCorrect = 0;
    let pronunciationCorrect = 0;

    let selectedWord = null;
    let selectedDef = null;
    let matchedWords = [];

    let pronRecognition = null;
    let activePronSentences = [];
    let pronCorrectFlags = [];

    // Feature-detect speech recognition
    if ('webkitSpeechRecognition' in window) {
        pronRecognition = new webkitSpeechRecognition();
    } else if ('SpeechRecognition' in window) {
        pronRecognition = new SpeechRecognition();
    }
    if (pronRecognition) {
        pronRecognition.lang = "en-US";
        pronRecognition.interimResults = false;
        pronRecognition.maxAlternatives = 1;
    }

    // -------- HELPERS --------
    function shuffle(array) {
        for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [array[i], array[j]] = [array[j], array[i]];
        }
        return array;
    }

    function updateScore() {
        const total = writingCorrect + matchingCorrect + pronunciationCorrect;
        document.getElementById("score").textContent = total;
    }

    // -------- WRITING GAPS --------
    function loadWriting() {
        const container = document.getElementById("writing-container");
        container.innerHTML = "";
        writingSentences.forEach((s, i) => {
            container.innerHTML += `
                <div class="question">
                    <p>${s.text}</p>
                    <div class="feedback" id="write-feed-${i}"></div>
                </div>
            `;
        });
    }

    function checkWriting() {
        const blanks = document.querySelectorAll("#fill-gaps .fill-blank");
        let correct = 0;
        writingSentences.forEach((s, i) => {
            const input = blanks[i];
            const val = input.value.toLowerCase().trim();
            const fb = document.getElementById(`write-feed-${i}`);
            if (val === s.answer) {
                fb.textContent = "✔️ Correct!";
                fb.className = "feedback correct";
                fb.style.display = "block";
                correct++;
            } else {
                fb.textContent = `❌ Incorrect. Correct: "${s.answer}"`;
                fb.className = "feedback incorrect";
                fb.style.display = "block";
            }
        });
        writingCorrect = correct;
        updateScore();
    }

    function resetWriting() {
        document.querySelectorAll("#fill-gaps .fill-blank").forEach(i => i.value = "");
        document.querySelectorAll("#fill-gaps .feedback").forEach(f => f.style.display = "none");
        writingCorrect = 0;
        updateScore();
    }

    // -------- MATCHING --------
    function loadDefinitions() {
        const container = document.getElementById("definitions-container");
        container.innerHTML = "";
        const shuffled = shuffle([...definitionItems]);
        shuffled.forEach(def => {
            container.innerHTML += `
                <div class="match-item" data-meaning="${def.word}" onclick="selectMatch(this)">
                    ${def.text}
                </div>
            `;
        });
    }

    function selectMatch(element) {
        if (element.classList.contains("matched")) return;

        if (element.dataset.word) {
            // word side
            if (selectedWord) selectedWord.classList.remove("selected");
            selectedWord = element;
            element.classList.add("selected");
        } else {
            // definition side
            if (selectedDef) selectedDef.classList.remove("selected");
            selectedDef = element;
            element.classList.add("selected");
        }

        if (selectedWord && selectedDef) {
            if (selectedWord.dataset.word === selectedDef.dataset.meaning) {
                selectedWord.classList.remove("selected");
                selectedWord.classList.add("matched");
                selectedDef.classList.remove("selected");
                selectedDef.classList.add("matched");
                matchedWords.push(selectedWord.dataset.word);
            } else {
                selectedWord.classList.remove("selected");
                selectedDef.classList.remove("selected");
            }
            selectedWord = null;
            selectedDef = null;
            matchingCorrect = matchedWords.length;
            updateScore();
        }
    }

    function resetMatching() {
        matchedWords = [];
        matchingCorrect = 0;
        updateScore();
        document.querySelectorAll("#matching .match-item").forEach(item => {
            item.classList.remove("selected", "matched");
        });
        loadDefinitions();
    }

    // -------- PRONUNCIATION GAPS (SHUFFLED) --------
    function loadPronunciationGaps() {
        const container = document.getElementById("pron-gaps-container");
        container.innerHTML = "";
        const shuffled = shuffle([...pronSentences]);
        activePronSentences = shuffled;
        pronCorrectFlags = shuffled.map(() => false);
        pronunciationCorrect = 0;
        updateScore();

        shuffled.forEach((s, i) => {
            container.innerHTML += `
                <div class="question">
                    <p>
                        ${s.before.replace("___", `<span id="pron-blank-${i}" class="fill-blank-pron">______</span>`)}
                        <button class="pron-btn" onclick="recordPronunciation(${i})">
                            <i class="fas fa-microphone"></i> Speak
                        </button>
                    </p>
                    <div class="feedback" id="pron-feed-${i}"></div>
                </div>
            `;
        });
    }

    function recordPronunciation(index) {
        if (!pronRecognition) {
            alert("Speech recognition is not supported in this browser.");
            return;
        }

        const fb = document.getElementById(`pron-feed-${index}`);
        fb.textContent = "🎤 Listening...";
        fb.className = "feedback";
        fb.style.display = "block";

        pronRecognition.start();

        pronRecognition.onresult = function(e) {
            const transcript = e.results[0][0].transcript.toLowerCase().trim();
            const expected = activePronSentences[index].answer.toLowerCase();

            const blank = document.getElementById(`pron-blank-${index}`);

            if (transcript === expected) {
                fb.textContent = `✔️ Correct! You said "${transcript}".`;
                fb.className = "feedback correct";
                blank.textContent = activePronSentences[index].answer;
                blank.style.color = "green";
                if (!pronCorrectFlags[index]) {
                    pronCorrectFlags[index] = true;
                    pronunciationCorrect = pronCorrectFlags.filter(Boolean).length;
                    updateScore();
                }
            } else {
                fb.textContent = `❌ You said "${transcript}". Try again.`;
                fb.className = "feedback incorrect";
            }
        };

        pronRecognition.onerror = function() {
            fb.textContent = "❌ Error during recognition. Please try again.";
            fb.className = "feedback incorrect";
        };
    }

    // -------- NAVIGATION --------
    function showSection(id, evt) {
        document.querySelectorAll(".game-section").forEach(sec => sec.classList.remove("active"));
        document.getElementById(id).classList.add("active");

        document.querySelectorAll(".nav-btn").forEach(btn => btn.classList.remove("active"));
        if (evt && evt.target) {
            evt.target.classList.add("active");
        }

        if (id === "fill-gaps") {
            // ensure writing loaded (only once necessary)
            // nothing extra here; we load on init
        }
        if (id === "matching") {
            resetMatching();
        }
        if (id === "pronunciation") {
            loadPronunciationGaps();
        }
    }

    // -------- INIT --------
    window.onload = function() {
        loadWriting();
        loadDefinitions();
        loadPronunciationGaps();
        updateScore();
    };
</script>
</body>
</html>
