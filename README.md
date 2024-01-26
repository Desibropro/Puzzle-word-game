<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Word Puzzle Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #f4f4f4;
            color: #333;
        }

        #word-container {
            margin-top: 20px;
            font-size: 1.5em;
        }

        #user-input {
            margin-top: 10px;
            padding: 8px;
            font-size: 1em;
        }

        #attempts {
            margin-top: 10px;
            color: #777;
            font-size: 1.2em;
        }

        #result-message {
            margin-top: 20px;
            font-weight: bold;
            font-size: 1.2em;
        }

        button {
            padding: 10px;
            margin-top: 15px;
            cursor: pointer;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
        }

        #timer {
            font-size: 1.2em;
        }

        #score {
            font-size: 1.2em;
        }

        #level {
            margin-top: 20px;
            font-size: 1.2em;
        }
    </style>
</head>
<body>

<h1>Welcome to the Word Puzzle Game!</h1>
<p>Select a difficulty level:</p>
<select id="difficulty" onchange="changeDifficulty()">
    <option value="easy">Easy</option>
    <option value="medium">Medium</option>
    <option value="hard">Hard</option>
</select>

<div id="word-container">
    <p id="shuffled-word"></p>
</div>

<input type="text" id="user-input" placeholder="Enter your guess">
<button onclick="checkGuess()">Submit Guess</button>

<p id="attempts">Attempts left: <span id="attempt-count">3</span></p>
<p id="result-message"></p>

<button onclick="reshuffle()">Reshuffle Letters</button>

<p id="timer">Time: <span id="timer-count">0</span>s</p>
<p id="score">Score: <span id="score-count">0</span></p>
<p id="level">Level: <span id="level-count">Easy</span></p>

<script>
    var words = {
        easy: ["cat", "dog", "sun", "red", "blue"],
        medium: ["apple", "table", "happy", "music", "water"],
        hard: ["elephant", "algorithm", "university", "challenge", "exquisite"]
    };
    var originalWord;
    var shuffledWord;
    var attemptsLeft = 3;
    var score = 0;
    var timer = 0;
    var currentLevel = "easy";

    function chooseWord() {
        return words[currentLevel][Math.floor(Math.random() * words[currentLevel].length)];
    }

    function shuffleWord(word) {
        return word.split('').sort(function () {
            return 0.5 - Math.random()
        }).join('');
    }

    function displayShuffledWord() {
        document.getElementById("shuffled-word").innerHTML = "Shuffled word: " + shuffledWord;
    }

    function checkGuess() {
        var userGuess = document.getElementById("user-input").value.toLowerCase();
        var resultMessage = document.getElementById("result-message");

        if (userGuess === originalWord) {
            resultMessage.style.color = "green";
            resultMessage.innerHTML = "Congratulations! You've guessed the word correctly.";
            document.getElementById("user-input").disabled = true;
            updateScore();
        } else {
            attemptsLeft--;
            document.getElementById("attempt-count").innerHTML = attemptsLeft;

            if (attemptsLeft > 0) {
                resultMessage.style.color = "red";
                resultMessage.innerHTML = "Incorrect. Try again.";
            } else {
                resultMessage.style.color = "red";
                resultMessage.innerHTML = "Sorry, you're out of attempts. The correct word was '" + originalWord + "'.";
                document.getElementById("user-input").disabled = true;
            }
        }
    }

    function reshuffle() {
        attemptsLeft = 3;
        document.getElementById("attempt-count").innerHTML = attemptsLeft;

        originalWord = chooseWord();
        shuffledWord = shuffleWord(originalWord);
        displayShuffledWord();

        document.getElementById("user-input").value = "";
        document.getElementById("result-message").innerHTML = "";
        document.getElementById("user-input").disabled = false;
    }

    function updateScore() {
        score += attemptsLeft * 10;
        document.getElementById("score-count").innerHTML = score;
    }

    function startTimer() {
        timer = 0;
        setInterval(function () {
            timer++;
            document.getElementById("timer-count").innerHTML = timer;
        }, 1000);
    }

    function changeDifficulty() {
        currentLevel = document.getElementById("difficulty").value;
        document.getElementById("level-count").innerHTML = capitalizeFirstLetter(currentLevel);
        reshuffle();
    }

    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }

    window.onload = function () {
        changeDifficulty();
        startTimer();
    };
</script>

</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Word Puzzle Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #f4f4f4;
            color: #333;
        }

        #word-container {
            margin-top: 20px;
            font-size: 1.5em;
        }

        #user-input {
            margin-top: 10px;
            padding: 8px;
            font-size: 1em;
        }

        #attempts {
            margin-top: 10px;
            color: #777;
            font-size: 1.2em;
        }

        #result-message {
            margin-top: 20px;
            font-weight: bold;
            font-size: 1.2em;
        }

        button {
            padding: 10px;
            margin-top: 15px;
            cursor: pointer;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
        }

        #timer {
            font-size: 1.2em;
        }

        #score {
            font-size: 1.2em;
        }

        #level {
            margin-top: 20px;
            font-size: 1.2em;
        }
    </style>
</head>
<body>

<h1>Welcome to the Word Puzzle Game!</h1>
<p>Select a difficulty level:</p>
<select id="difficulty" onchange="changeDifficulty()">
    <option value="easy">Easy</option>
    <option value="medium">Medium</option>
    <option value="hard">Hard</option>
</select>

<div id="word-container">
    <p id="shuffled-word"></p>
</div>

<input type="text" id="user-input" placeholder="Enter your guess">
<button onclick="checkGuess()">Submit Guess</button>

<p id="attempts">Attempts left: <span id="attempt-count">3</span></p>
<p id="result-message"></p>

<button onclick="reshuffle()">Reshuffle Letters</button>

<p id="timer">Time: <span id="timer-count">0</span>s</p>
<p id="score">Score: <span id="score-count">0</span></p>
<p id="level">Level: <span id="level-count">Easy</span></p>

<script>
    var words = {
        easy: ["cat", "dog", "sun", "red", "blue"],
        medium: ["apple", "table", "happy", "music", "water"],
        hard: ["elephant", "algorithm", "university", "challenge", "exquisite"]
    };
    var originalWord;
    var shuffledWord;
    var attemptsLeft = 3;
    var score = 0;
    var timer = 0;
    var currentLevel = "easy";

    function chooseWord() {
        return words[currentLevel][Math.floor(Math.random() * words[currentLevel].length)];
    }

    function shuffleWord(word) {
        return word.split('').sort(function () {
            return 0.5 - Math.random()
        }).join('');
    }

    function displayShuffledWord() {
        document.getElementById("shuffled-word").innerHTML = "Shuffled word: " + shuffledWord;
    }

    function checkGuess() {
        var userGuess = document.getElementById("user-input").value.toLowerCase();
        var resultMessage = document.getElementById("result-message");

        if (userGuess === originalWord) {
            resultMessage.style.color = "green";
            resultMessage.innerHTML = "Congratulations! You've guessed the word correctly.";
            document.getElementById("user-input").disabled = true;
            updateScore();
        } else {
            attemptsLeft--;
            document.getElementById("attempt-count").innerHTML = attemptsLeft;

            if (attemptsLeft > 0) {
                resultMessage.style.color = "red";
                resultMessage.innerHTML = "Incorrect. Try again.";
            } else {
                resultMessage.style.color = "red";
                resultMessage.innerHTML = "Sorry, you're out of attempts. The correct word was '" + originalWord + "'.";
                document.getElementById("user-input").disabled = true;
            }
        }
    }

    function reshuffle() {
        attemptsLeft = 3;
        document.getElementById("attempt-count").innerHTML = attemptsLeft;

        originalWord = chooseWord();
        shuffledWord = shuffleWord(originalWord);
        displayShuffledWord();

        document.getElementById("user-input").value = "";
        document.getElementById("result-message").innerHTML = "";
        document.getElementById("user-input").disabled = false;
    }

    function updateScore() {
        score += attemptsLeft * 10;
        document.getElementById("score-count").innerHTML = score;
    }

    function startTimer() {
        timer = 0;
        setInterval(function () {
            timer++;
            document.getElementById("timer-count").innerHTML = timer;
        }, 1000);
    }

    function changeDifficulty() {
        currentLevel = document.getElementById("difficulty").value;
        document.getElementById("level-count").innerHTML = capitalizeFirstLetter(currentLevel);
        reshuffle();
    }

    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }

    window.onload = function () {
        changeDifficulty();
        startTimer();
    };
</script>

</body>
</html>
