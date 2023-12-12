---
hide: False
toc: False
comments: True
layout: notebook
title: Ishan Cornick Review Ticket
description: Ishan Cornick Review Ticket
type: tangibles
courses: {'compsci': {'week': 2}}
---

<video  height="500" controls>
  <source src="/binarycptproject/videos/BinaryNumberGuessingGame.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
```html
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
        <br>
        <button onclick="restartGame()">Play Again</button> <!-- New button for restarting the game -->
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
        function restartGame() {
        // Reset variables
        minValue = 0;
        maxValue = 255;
        secretDecimal = generateRandomDecimal(minValue, maxValue);
        secretBinary = decimalToBinary(secretDecimal);
        attempts = 0;
        // Update display
        displayTargetNumber();
        outputDiv.innerHTML = "";
        document.getElementById('userGuess').value = ""; // Clear the input field
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
```
- When the user clicks the "Guess" button, the makeAGuess function is triggered.
- The user's input is validated to ensure it's a valid binary number (up to 8 digits).
- If the input is valid, it's converted to decimal, and the game logic determines whether the guess is correct, too low, or too high.
- Feedback is provided to the user, indicating whether the guess is correct or if they need to go higher or lower.
- The number of attempts is updated accordingly.

This HTML document implements a Binary Number Guessing Game. It consists of structural HTML elements like `<html>`, `<head>`, and `<body>`. Game elements include `<h1>`, `<p>`, `<input>`, and `<button>`, with a specific focus on guessing binary numbers from 0 to 255.

JavaScript manages variables such as minValue, maxValue, secretDecimal, and attempts. Functions include generating random decimals, converting decimals to binary, displaying the target number, restarting the game, and processing user guesses. An event listener displays the target number on page load.

The game flow involves users guessing binary numbers, receiving feedback, and restarting until the correct guess is made.

## If I had more time
If I had more time I would add....
    A bigger range of number.
    More friendly UI.
    Include more features in the game.
    Have an intro that shows how binary works.

## Problems I came accross
    My "Play Again" button wouldnt work, fixed this with help of my classmates, teammates and internet.
    Figuring out how to calculate the binary value, to do this I used the help of ChatGPT.
    Figuring about how to max the amount of characters to be added, ChatGPT helped a lot for that.
    
