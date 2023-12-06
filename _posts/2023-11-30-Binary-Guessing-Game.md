---
hide: True
layout: notebook
title: Binary Number Guessing Game
type: hacks
courses: {'compsci': {'week': 1}}
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary Number Guessing Game</title>
</head>
<body>
    <h1>Welcome to the Binary Number Guessing Game!</h1>
    <div>
        <p>Guess the binary representation of the number between 0 and 255:</p>
        <p id="targetNumber"></p>
        <input type="text" id="userGuess" placeholder="Enter your binary guess" pattern="^[0-1]{1,8}$" maxlength="8"/>
        <button onclick="makeAGuess()">Guess</button>
    </div>
    <div23 id="output"></div23>
    <script>
        var minValue = 0;
        var maxValue = 255;
        var secretDecimal = generateRandomDecimal(minValue, maxValue);
        var secretBinary = decimalToBinary(secretDecimal);
        var attempts = 0;
        var outputDiv = document.getElementById('output');
        var targetNumberDiv = document.getElementById('targetNumber');
        function generateRandomDecimal(minValue, maxValue) {
            return Math.floor(Math.random() * (maxValue - minValue + 1)) + minValue;
        }
        function decimalToBinary(decimal) {
            return decimal.toString(2);
        }
        function displayTargetNumber() {
            targetNumberDiv.innerText = `Number: ${secretDecimal}`;
        }
        function makeAGuess() {
            var playerGuess = document.getElementById('userGuess').value;
            // Validate the input
            if (!/^[0-1]{1,8}$/.test(playerGuess)) {
                outputDiv.innerHTML = "Invalid input. Please enter a binary number (0s and 1s) with up to 8 digits.";
                return;
            }
            try {
                var guessDecimal = parseInt(playerGuess, 2);
                if (guessDecimal === secretDecimal) {
                    outputDiv.innerHTML = `Congratulations! You guessed the correct binary number ${secretBinary} (decimal: ${guessDecimal}) in ${attempts} attempts.`;
                } else {
                    if (guessDecimal < secretDecimal) {
                        outputDiv.innerHTML = `Too low! Your guess ${playerGuess} in decimal is ${guessDecimal}. Try again.`;
                        minValue = guessDecimal + 1;
                    } else {
                        outputDiv.innerHTML = `Too high! Your guess ${playerGuess} in decimal is ${guessDecimal}. Try again.`;
                        maxValue = guessDecimal - 1;
                    }
                    attempts += 1;
                }
            } catch (error) {
                outputDiv.innerHTML = "Invalid input. Please enter a valid binary number.";
            }
        }
        // Display the target number when the page loads
        window.onload = displayTargetNumber;
    </script>
</body>
</html>
