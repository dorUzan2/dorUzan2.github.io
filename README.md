# dorUzan2.github.io
<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>משחק הצ'ייסר - מושגים אקדמיים</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .game-container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            max-width: 800px;
            width: 100%;
            padding: 30px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .game-container::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(102,126,234,0.1) 0%, transparent 50%);
            animation: rotate 20s linear infinite;
        }

        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .content {
            position: relative;
            z-index: 1;
        }

        h1 {
            color: #4a5568;
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .subtitle {
            color: #718096;
            font-size: 1.2em;
            margin-bottom: 30px;
        }

        .game-area {
            margin: 30px 0;
        }

        .score-board {
            display: flex;
            justify-content: space-around;
            margin-bottom: 30px;
            background: linear-gradient(45deg, #f7fafc, #edf2f7);
            padding: 20px;
            border-radius: 15px;
            box-shadow: inset 0 2px 10px rgba(0,0,0,0.1);
        }

        .score-item {
            text-align: center;
        }

        .score-label {
            font-size: 0.9em;
            color: #718096;
            margin-bottom: 5px;
        }

        .score-value {
            font-size: 2em;
            font-weight: bold;
            color: #4a5568;
        }

        .question-card {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin-bottom: 20px;
            box-shadow: 0 10px 30px rgba(79, 172, 254, 0.3);
            transform: translateY(0);
            transition: transform 0.3s ease;
        }

        .question-card:hover {
            transform: translateY(-5px);
        }

        .question {
            font-size: 1.3em;
            font-weight: bold;
            margin-bottom: 20px;
            line-height: 1.5;
        }

        .options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 20px;
        }

        .option {
            background: rgba(255,255,255,0.2);
            border: 2px solid rgba(255,255,255,0.3);
            color: white;
            padding: 15px 20px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1em;
            backdrop-filter: blur(10px);
        }

        .option:hover {
            background: rgba(255,255,255,0.3);
            border-color: rgba(255,255,255,0.8);
            transform: scale(1.05);
        }

        .option.correct {
            background: #48bb78;
            border-color: #48bb78;
            animation: pulse 0.5s;
        }

        .option.incorrect {
            background: #f56565;
            border-color: #f56565;
            animation: shake 0.5s;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        .controls {
            margin-top: 30px;
        }

        .btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            margin: 0 10px;
            box-shadow: 0 5px 15px rgba(118, 75, 162, 0.3);
            transition: all 0.3s ease;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(118, 75, 162, 0.4);
        }

        .btn:active {
            transform: translateY(0);
        }

        .progress-bar {
            background: #e2e8f0;
            height: 10px;
            border-radius: 5px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress-fill {
            background: linear-gradient(45deg, #48bb78, #38a169);
            height: 100%;
            width: 0%;
            transition: width 0.5s ease;
            border-radius: 5px;
        }

        .result-message {
            margin-top: 20px;
            font-size: 1.2em;
            font-weight: bold;
            padding: 15px;
            border-radius: 10px;
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.3s ease;
        }

        .result-message.show {
            opacity: 1;
            transform: translateY(0);
        }

        .result-message.correct {
            background: #c6f6d5;
            color: #2f855a;
            border: 2px solid #48bb78;
        }

        .result-message.incorrect {
            background: #fed7d7;
            color: #c53030;
            border: 2px solid #f56565;
        }

        .game-over {
            text-align: center;
            padding: 30px;
        }

        .final-score {
            font-size: 3em;
            font-weight: bold;
            color: #667eea;
            margin: 20px 0;
        }

        @media (max-width: 600px) {
            .options {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 2em;
            }
            
            .score-board {
                flex-direction: column;
                gap: 15px;
            }
        }

        .chaser-animation {
            position: absolute;
            top: 50%;
            right: -100px;
            font-size: 3em;
            animation: chase 3s ease-in-out;
        }

        @keyframes chase {
            0% { right: -100px; }
            50% { right: 50%; }
            100% { right: -100px; }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <div class="content">
            <h1>🎓 משחק הצ'ייסר האקדמי</h1>
            <p class="subtitle">בדקו את הידע שלכם במושגים אקדמיים!</p>

            <div class="score-board">
                <div class="score-item">
                    <div class="score-label">שאלה נוכחית</div>
                    <div class="score-value" id="current-question">1</div>
                </div>
                <div class="score-item">
                    <div class="score-label">ניקוד</div>
                    <div class="score-value" id="score">0</div>
                </div>
                <div class="score-item">
                    <div class="score-label">זמן</div>
                    <div class="score-value" id="timer">30</div>
                </div>
            </div>

            <div class="progress-bar">
                <div class="progress-fill" id="progress"></div>
            </div>

            <div class="game-area" id="game-area">
                <div class="question-card">
                    <div class="question" id="question-text">לחצו "התחל משחק" כדי להתחיל!</div>
                    <div class="options" id="options-container" style="display: none;"></div>
                </div>
                
                <div class="result-message" id="result-message"></div>
            </div>

            <div class="controls">
                <button class="btn" id="start-btn" onclick="startGame()">התחל משחק</button>
                <button class="btn" id="next-btn" onclick="nextQuestion()" style="display: none;">שאלה הבאה</button>
                <button class="btn" id="restart-btn" onclick="restartGame()" style="display: none;">משחק חדש</button>
            </div>
        </div>
    </div>

    <script>
        const questions = [
            {
                question: "מה זו תעודת הסמכה?",
                options: ["מסמך המעיד על הכשרה והעמידה בדרישות בתחום מסוים", "תואר אקדמי", "דיפלומה", "נקודות זכות"],
                correct: 0
            },
            {
                question: "מה זו דיפלומה במערכת מה\"ט?",
                options: ["תואר אקדמי", "תעודה לסיום לימודי הנדסאים", "תעודת הוראה", "תעודת רישוי"],
                correct: 1
            },
            {
                question: "מה זה תואר?",
                options: ["מוסד להשכלה", "חוג באוניברסיטה", "תעודה אקדמית שמוענקת לסטודנטים שהשלימו תכנית לימודים", "נקודות זכות"],
                correct: 2
            },
            {
                question: "מה פירוש הקיצור מל\"ג?",
                options: ["מכון לטכנולוגיה", "מכללה להנדסה", "מכון למחקר", "מועצה להשכלה גבוהה"],
                correct: 3
            },
            {
                question: "על מה אחראי מה\"ט?",
                options: ["מערך המכללות הטכנולוגיות", "אוניברסיטאות", "חוגים אקדמיים", "תוארי דוקטור"],
                correct: 0
            },
            {
                question: "מה זו מכינה?",
                options: ["פקולטה באוניברסיטה", "תוכנית לימודים המכינה לתואר אקדמי או לימודי הנדסאים", "תעודת הסמכה", "סמסטר לימודים"],
                correct: 1
            },
            {
                question: "כמה זמן אורך סמסטר?",
                options: ["10-12 שבועות", "16-18 שבועות", "13-15 שבועות", "20-22 שבועות"],
                correct: 2
            },
            {
                question: "מה הן נקודות זכות?",
                options: ["ציון במבחן", "תעודה אקדמית", "שכר לימוד", "נקודות הניתנות לסטודנט בסיום קורס"],
                correct: 3
            },
            {
                question: "מה זה פרויקט גמר?",
                options: ["עבודה מעמיקה לקבלת תואר הנדסאי/טכנאי", "מבחן סופי", "תעודת הסמכה", "סמסטר לימודים"],
                correct: 0
            },
            {
                question: "מהי פקולטה?",
                options: ["חוג בודד באוניברסיטה", "יחידה העוסקת במחקר ובהוראה המאגדת כמה חוגים", "תעודה אקדמית", "משרד מנהלי"],
                correct: 1
            },
            {
                question: "מה זה חוג?",
                options: ["פקולטה גדולה", "מוסד להשכלה גבוהה", "תחום ידע מתוך הפקולטה", "תואר אקדמי"],
                correct: 2
            },
            {
                question: "מה המשמעות של דיקנט?",
                options: ["תואר אקדמי", "חוג באוניברסיטה", "תעודה של מה\"ט", "משרד או יחידה מנהלית באוניברסיטה"],
                correct: 3
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;
        let timeLeft = 30;
        let timer;
        let gameActive = false;

        function startGame() {
            gameActive = true;
            currentQuestionIndex = 0;
            score = 0;
            timeLeft = 30;
            
            document.getElementById('start-btn').style.display = 'none';
            document.getElementById('next-btn').style.display = 'none';
            document.getElementById('restart-btn').style.display = 'none';
            document.getElementById('result-message').className = 'result-message';
            
            updateDisplay();
            showQuestion();
            startTimer();
        }

        function showQuestion() {
            if (currentQuestionIndex >= questions.length) {
                endGame();
                return;
            }

            const questionData = questions[currentQuestionIndex];
            document.getElementById('question-text').textContent = questionData.question;
            
            const optionsContainer = document.getElementById('options-container');
            optionsContainer.style.display = 'grid';
            optionsContainer.innerHTML = '';
            
            questionData.options.forEach((option, index) => {
                const button = document.createElement('button');
                button.className = 'option';
                button.textContent = option;
                button.onclick = () => selectAnswer(index);
                optionsContainer.appendChild(button);
            });

            // Reset timer for new question
            timeLeft = 30;
            updateDisplay();
        }

        function selectAnswer(selectedIndex) {
            if (!gameActive) return;

            clearInterval(timer);
            const questionData = questions[currentQuestionIndex];
            const options = document.querySelectorAll('.option');
            const resultMessage = document.getElementById('result-message');

            options.forEach((option, index) => {
                option.onclick = null;
                if (index === questionData.correct) {
                    option.classList.add('correct');
                } else if (index === selectedIndex) {
                    option.classList.add('incorrect');
                }
            });

            if (selectedIndex === questionData.correct) {
                score += Math.max(10, timeLeft);
                resultMessage.textContent = `נכון! 🎉 קיבלתם ${Math.max(10, timeLeft)} נקודות`;
                resultMessage.className = 'result-message correct show';
                
                // Add chaser animation for correct answer
                const chaser = document.createElement('div');
                chaser.innerHTML = '🏃‍♂️';
                chaser.className = 'chaser-animation';
                document.querySelector('.game-container').appendChild(chaser);
                setTimeout(() => chaser.remove(), 3000);
            } else {
                resultMessage.textContent = `לא נכון 😞 התשובה הנכונה היא: ${questionData.options[questionData.correct]}`;
                resultMessage.className = 'result-message incorrect show';
            }

            updateDisplay();
            document.getElementById('next-btn').style.display = 'inline-block';
        }

        function nextQuestion() {
            currentQuestionIndex++;
            document.getElementById('next-btn').style.display = 'none';
            document.getElementById('result-message').className = 'result-message';
            
            if (currentQuestionIndex >= questions.length) {
                endGame();
            } else {
                showQuestion();
                startTimer();
            }
        }

        function startTimer() {
            timer = setInterval(() => {
                timeLeft--;
                updateDisplay();
                
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    selectAnswer(-1); // Auto-select wrong answer when time runs out
                }
            }, 1000);
        }

        function updateDisplay() {
            document.getElementById('current-question').textContent = currentQuestionIndex + 1;
            document.getElementById('score').textContent = score;
            document.getElementById('timer').textContent = timeLeft;
            
            const progress = ((currentQuestionIndex) / questions.length) * 100;
            document.getElementById('progress').style.width = progress + '%';
        }

        function endGame() {
            gameActive = false;
            clearInterval(timer);
            
            const gameArea = document.getElementById('game-area');
            gameArea.innerHTML = `
                <div class="game-over">
                    <h2>🎊 המשחק הסתיים!</h2>
                    <div class="final-score">${score}</div>
                    <p>ענית על ${currentQuestionIndex} מתוך ${questions.length} שאלות</p>
                    <p>${score >= questions.length * 15 ? 'ביצוע מעולה! 🌟' : score >= questions.length * 10 ? 'ביצוע טוב! 👍' : 'כדאי לחזור על החומר 📚'}</p>
                </div>
            `;
            
            document.getElementById('restart-btn').style.display = 'inline-block';
        }

        function restartGame() {
            location.reload();
        }
    </script>
</body>
</html>
