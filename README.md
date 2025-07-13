<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Science Guess for You 💚</title>
    <style>
        /* Same styles as before, trimmed for clarity */
        body {
            background: #2f4f4f;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            text-align: center;
            padding: 20px;
            overflow-x: hidden;
        }

        img {
            width: 100%;
            max-width: 350px;
            height: auto;
            margin-top: 15px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
            display: block;
            margin-left: auto;
            margin-right: auto;
        }

        input, button {
            padding: 12px;
            margin-top: 15px;
            font-size: 1rem;
            border: none;
            border-radius: 8px;
            width: 80%;
            max-width: 300px;
        }

        .hidden-message {
            display: none;
            margin-top: 30px;
        }

        .card {
            width: 90%;
            max-width: 300px;
            height: 300px;
            perspective: 1000px;
            margin: 20px auto;
        }

        .inner-card {
            width: 100%;
            height: 100%;
            background: #3b6040;
            border-radius: 20px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            transform-style: preserve-3d;
            transition: transform 0.8s;
            cursor: pointer;
            position: relative;
        }

        .card:hover .inner-card {
            transform: rotateY(180deg);
        }

        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 20px;
            color: white;
            backface-visibility: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 15px;
            box-sizing: border-box;
            flex-direction: column;
        }

        .front {
            background: #4b7054;
        }

        .back {
            background: #2e4631;
            transform: rotateY(180deg);
        }

        .back img {
            width: 120px;
            height: 120px;
            border-radius: 15px;
            border: 4px solid white;
            box-shadow: 0 4px 8px rgba(0,0,0,0.5);
            margin-bottom: 10px;
        }

        @media (max-width: 480px) {
            img {
                max-width: 280px;
            }
        }

        #startArea {
            margin-top: 30px;
            padding: 30px 20px;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }

        #startArea button {
            background: linear-gradient(135deg, #4caf50, #81c784);
            color: white;
            font-size: 1.1rem;
            box-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
            transition: all 0.3s ease;
            animation: pulse 2s infinite;
        }

        #startArea button:hover {
            transform: scale(1.1);
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.7);
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 10px rgba(0, 255, 0, 0.5); }
            50% { box-shadow: 0 0 20px rgba(0, 255, 0, 0.8); }
            100% { box-shadow: 0 0 10px rgba(0, 255, 0, 0.5); }
        }
    </style>
</head>
<body>

<div id="startArea">
    <h1>Good Morning, Love! 🌿</h1>
    <p style="font-size: 1rem;">This is another random appreciation for your existence day! 💚</p>
    <button onclick="startQuiz()">Click me to reach the letter for you today 💌</button>
</div>

<div id="quizArea" style="display:none;">
    <h2>Guess the Science Picture 💚</h2>
    <p style="font-size: 1rem; margin-top: -10px;">Type all answers in small letters (lowercase only)</p>

    <img id="quizImage" src="" alt="Science Image">
    <div id="quizText" style="margin-top: 15px;"></div>
    <input type="text" id="answer" placeholder="Type your answer here">
    <br>
    <button onclick="checkAnswer()">Submit</button>
</div>

<div class="hidden-message" id="hiddenMessage">
    <h2>Correct! You unlocked my letter 💌</h2>

    <div class="card">
        <div class="inner-card">
            <div class="card-face front">
                <p>Good morning! Hover me 💌</p>
            </div>
            <div class="card-face back">
                <img src="https://i.imgur.com/nkkqwSx.jpg" alt="Your Face">
                <p>You’re so handsome and I love you. Thank you for the food and your presence always. 💚 Please listen carefully to the lyrics now!</p>
            </div>
        </div>
    </div>
</div>

<audio id="mainSong" autoplay loop>
    <source src="https://voca.ro/1fcG1NZeC9id" type="audio/mpeg">
</audio>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

<script>
    const quizSteps = [
        { image: 'https://i.imgur.com/1ARQ3UD.jpg', answer: 'animal cell' },
        { image: 'https://i.imgur.com/EtzxMM6.jpg', answer: 'human heart' },
        { image: 'https://i.imgur.com/s8TAZxU.jpg', answer: 'punnett square' },
        { text: 'Powerhouse of the cell', answer: 'mitochondria' },
        { text: "Fill in the blank lyric: I'm glad I share a ________ with you.", answer: 'universe' }
    ];

    let currentStep = 0;

    function startQuiz() {
        document.getElementById("startArea").style.display = "none";
        document.getElementById("quizArea").style.display = "block";
        updateQuizStep();
    }

    function checkAnswer() {
        const input = document.getElementById("answer").value.trim().toLowerCase();
        if (input === quizSteps[currentStep].answer) {
            launchConfetti();
            currentStep++;
            if (currentStep >= quizSteps.length) {
                document.getElementById("quizArea").style.display = "none";
                document.getElementById("hiddenMessage").style.display = "block";
            } else {
                updateQuizStep();
            }
        } else {
            alert("Try again, love! Small letters only!");
        }
    }

    function updateQuizStep() {
        if (quizSteps[currentStep].image) {
            document.getElementById("quizImage").src = quizSteps[currentStep].image;
            document.getElementById("quizImage").style.display = 'block';
            document.getElementById("quizText").innerText = '';
        } else {
            document.getElementById("quizImage").style.display = 'none';
            document.getElementById("quizText").innerText = quizSteps[currentStep].text;
        }
        document.getElementById("answer").value = '';
    }

    function launchConfetti() {
        confetti({
            particleCount: 150,
            spread: 70,
            origin: { y: 0.6 }
        });
    }
</script>

</body>
</html>
