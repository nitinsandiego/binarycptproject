---
hide: False
toc: False
comments: True
layout: notebook
title: Binary CPT Project Review Ticket
description: Binary CPT Project Review Ticket
type: tangibles
courses: {'compsci': {'week': 2}}
---
# Utterance Grading is at the bottom of the page

| Crossover Score | Feature 1 | Feature 2 | Feature 3 | Feature 4 | GitHub | Analytics |
| TBD | [Binary Image Processing](https://nitinsandiego.github.io/binarycptproject//2023/11/26/Binary-Image-Processing.html) | [Binary Logical Operators](https://nitinsandiego.github.io/binarycptproject//2023/11/28/Binary-Logical-Operations.html) | [Binary Encryption ](https://nitinsandiego.github.io/binarycptproject//2023/11/26/Binary-Encryption.html) | [Binary Number Guessng Game](https://nitinsandiego.github.io/binarycptproject//2023/11/30/Binary-Guessing-Game.html) | [BinaryCPT Project Repository](https://github.com/nitinsandiego/binarycptproject) | [Deployments](https://github.com/nitinsandiego/binarycptproject/deployments)

# Nitin's Feature video
<video  height="500" controls>
    <source src="/binarycptproject/videos/BinaryImageProcessing.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>
```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Image Processing with JS</title>
</head>
<body>
  <label for="imageLink">Image Link:</label>
  <br>
  <input type="file" id="fileInput" accept="image/*">
  <br>
  <button id="loadButton" style="display: inline;">Load Image</button>
  <br>
  <canvas id="canvas" style="border: 1px solid #000;"></canvas>
  <br>
  <button id="processButton" style="display: none;">Process Image to Binary</button>
  <button id="reverseHexButton" style="display: none;">Reverse Hex Color</button>
  <button id="originalButton" style="display: none;">Show Original Image</button>

  <script>
  document.addEventListener('DOMContentLoaded', function() {
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const loadButton = document.getElementById('loadButton');
    const processButton = document.getElementById('processButton');
    const originalButton = document.getElementById('originalButton');
    const reverseHexButton = document.getElementById('reverseHexButton');
    const fileInput = document.getElementById('fileInput');
    let img = new Image();

    function clearCanvas() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    }

    function loadAndDisplayImage() {
      const file = fileInput.files[0];

      if (!file) {
        alert('Please select a file.');
        return;
      }

      clearCanvas();

      const reader = new FileReader();
      reader.onload = function(e) {
        img.onload = function() {
          const targetWidth = 1000;
          const scaleFactor = targetWidth / img.width;
          canvas.width = targetWidth;
          canvas.height = img.height * scaleFactor;
          ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
          processButton.style.display = 'inline';
          reverseHexButton.style.display = 'inline';
          originalButton.style.display = 'none';
        };
        img.src = e.target.result;
      };
      reader.readAsDataURL(file);
    }

    function convertToBinary() {
      const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
      const data = imageData.data;
      for (let i = 0; i < data.length; i += 4) {
        const brightness = 0.34 * data[i] + 0.5 * data[i + 1] + 0.16 * data[i + 2];
        const threshold = 128;
        const color = brightness > threshold ? 255 : 0;
        data[i] = data[i + 1] = data[i + 2] = color;
      }
      ctx.putImageData(imageData, 0, 0);
      toggleButtonsAfterProcessing();
    }

    function reverseHexColor() {
      const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
      const data = imageData.data;
      for (let i = 0; i < data.length; i += 4) {
        data[i] = 255 - data[i];       // Reverse Red
        data[i + 1] = 255 - data[i + 1]; // Reverse Green
        data[i + 2] = 255 - data[i + 2]; // Reverse Blue
      }
      ctx.putImageData(imageData, 0, 0);
      toggleButtonsAfterProcessing();
    }

    function toggleButtonsAfterProcessing() {
      processButton.style.display = 'none';
      reverseHexButton.style.display = 'none';
      originalButton.style.display = 'inline';
    }

    loadButton.addEventListener('click', loadAndDisplayImage);
    processButton.addEventListener('click', convertToBinary);
    reverseHexButton.addEventListener('click', reverseHexColor);
    originalButton.addEventListener('click', () => {
      if (img.complete && img.src) {
        ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
        processButton.style.display = 'inline';
        reverseHexButton.style.display = 'inline';
        originalButton.style.display = 'none';
      }
    });
  });
</script>
</body>
</html>
```

## Convert to Binary
The goal of this function is to convert the loaded image into a binary format. It achieves this by applying a threshold to the brightness of each pixel in the image. Here's the breakdown:<br>

**Get Image Data**
```javascript
   const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
```
**Decide Whether Pixel is White or Black**
```javascript
for (let i = 0; i < data.length; i += 4) {
  const brightness = 0.34 * data[i] + 0.5 * data[i + 1] + 0.16 * data[i + 2];
  const threshold = 128;
  const color = brightness > threshold ? 255 : 0;
  data[i] = data[i + 1] = data[i + 2] = color;
}
```
It calculates the brightness of each pixel using a weighted sum of its RGB values. If the brightness is greater than a threshold (128), it sets the pixel color to white (255); otherwise, it sets it to black (0).

## Reverse Hex Color
The purpose of this function is to reverse the hex color of each pixel in the loaded image. It achieves this by subtracting each color component from 255. Here's the breakdown:<br>

**Get Image Data**
```javascript
   const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
```
**Reverse Hex Color**
```javascript
for (let i = 0; i < data.length; i += 4) {
  data[i] = 255 - data[i];        // Reverse Red
  data[i + 1] = 255 - data[i + 1]; // Reverse Green
  data[i + 2] = 255 - data[i + 2]; // Reverse Blue
}
```
It subtracts each color component (Red, Green, Blue) from 255, effectively creating a color negative.

# Akshay's Feature video
<video  height="500" controls>
  <source src="/binarycptproject/videos/Binary_Logical_Operators.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Binary Logical Operations</title>
</head>
<body>
    <br>
    <label>Input 1: <input type="text" id="input1" placeholder="Enter binary number"></label>
    <br>
    <br>
    <label id="input2Label">Input 2: <input type="text" id="input2" placeholder="Enter binary number"></label>
    <br>
    <br>
    <select id="operation" onchange="toggleInput2()">
        <option value="AND">AND</option>
        <option value="OR">OR</option>
        <option value="XOR">XOR</option>
        <option value="NOT">NOT</option>
    </select>
    <br>
    <br>
    <button onclick="performOperation()">Calculate</button>
    <br>
    <br>
    <div23>Result: <span id="result"></span></div23>
    <script>
        function toggleInput2() {
            document.getElementById('input2Label').style.display = 
                document.getElementById('operation').value === 'NOT' ? 'none' : 'inline';
        }
        function performOperation() {
            let input1 = parseInt(document.getElementById('input1').value, 2);
            let input2 = parseInt(document.getElementById('input2').value, 2);
            const operation = document.getElementById('operation').value;
            let result;
            switch (operation) {
                case 'AND': result = input1 & input2; break;
                case 'OR': result = input1 | input2; break;
                case 'XOR': result = input1 ^ input2; break;
                case 'NOT': 
                    // Limit input1 to 8 bits
                    input1 = input1 & 0xFF;
                    // Perform NOT operation and limit result to 8 bits
                    result = (~input1) & 0xFF; 
                    break;
                default: result = 'Invalid operation'; return;
            }
            const binaryResult = formatByte(result);
            document.getElementById('result').textContent = binaryResult + ' (Decimal: ' + result + ')';
        }
        function formatByte(number) {
            return ('00000000' + number.toString(2)).substr(-8);
        }
        toggleInput2(); // Initial call to set up the correct display
    </script>
</body>
</html>
```
## Logical Operations:
1. **AND (&):** Sets each bit of the result to 1 if both corresponding bits of the inputs are 1.
2. **OR (\|):** Sets each bit of the result to 1 if at least one corresponding bit of the inputs is 1.
3. **XOR (^):** Sets each bit of the result to 1 if the corresponding bits of the inputs are different.
4. **NOT (~):** Inverts each bit of the input, changing 1s to 0s and vice versa. Note that only the first input is used for the NOT operation.

## And Example
The AND operation compares each pair of corresponding bits in the two binary numbers. The result has a 1 in a particular bit position only if both input bits in that position are 1; otherwise, the result has a 0.
<br>
<br>
Input 1:  10101010<br>
Input 2:  11001100<br>
-----------------<br>
Result:   10001000<br>
<br>
In this example, only the third and seventh bits have 1s in both inputs, so the AND operation results in "10001000."

## Or Example
The OR operation compares each pair of corresponding bits in the two binary numbers. The result has a 1 in a particular bit position if at least one of the input bits in that position is 1.
<br>
<br>
Input 1:  10101010<br>
Input 2:  11001100<br>
-----------------<br>
Result:   11101110<br>
<br>
In this example, bits with 1s in either input contribute to the OR operation result, producing "11101110."

## XOR Example
The XOR (exclusive OR) operation compares each pair of corresponding bits in the two binary numbers. The result has a 1 in a particular bit position only if the input bits in that position are different.
<br>
<br>
Input 1:  10101010<br>
Input 2:  11001100<br>
-----------------<br>
Result:   01100110<br>
<br>
In this example, only the second, fourth, sixth, and eighth bits have different values in the inputs, resulting in "01100110."

## Not Example
The NOT operation inverts each bit of the input.
<br>
<br>
Input 1:  10101010<br>
-----------------<br>
Result:   01010101<br>
<br>
In this example, each 1 in the original input becomes a 0, and each 0 becomes a 1, resulting in "01010101."

# Ishan's Feature video
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

# Saatvik's Feature video
<video  height="500" controls>
  <source src="/binarycptproject/videos/BinaryEncryption.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
```html
<html>
<body>
    <h2>Binary Encryption and Decryption Guessing Game</h2>
    <textarea id="inputText" placeholder="Enter text here"></textarea><br>
    <button onclick="encrypt()">Encrypt</button>
    <button onclick="decrypt()">Decrypt</button><br>
    <h2>Encrypted Result:</h2>
    <p id="encryptedResult"></p>
    <input type="text" id="encryptGuessInput" placeholder="Enter your encryption guess">
    <br>
    <button onclick="checkEncryptGuess()">Check Encryption Guess</button>
    <p id="encryptGuessResult"></p>
    <h2>Decrypted Result:</h2>
    <p id="decryptedResult"></p>
    <input type="text" id="decryptGuessInput" placeholder="Enter your decryption guess">
    <br>
    <button onclick="checkDecryptGuess()">Check Decryption Guess</button>
    <p id="decryptGuessResult"></p>
    <script>
    var encryptedResult; // Variable to store the encrypted result
    var decryptedResult; // Variable to store the decrypted result
    function encrypt() {
        var input = document.getElementById("inputText").value;
        var binary = '';
        for (var i = 0; i < input.length; i++) {
            var charBinary = input[i].charCodeAt(0).toString(2);
            // Ensure each binary representation has 8 digits by padding with leading zeros
            charBinary = '00000000'.substring(charBinary.length) + charBinary;
            binary += charBinary + " ";
        }
        encryptedResult = binary.trim();
        document.getElementById("encryptedResult").innerText = "Guess the encrypted result!";
        document.getElementById("encryptGuessResult").innerText = "";
    }
    function decrypt() {
        var input = document.getElementById("inputText").value;
        var text = '';
        var arr = input.split(" ");
        for (var i = 0; i < arr.length; i++) {
            text += String.fromCharCode(parseInt(arr[i], 2));
        }
        decryptedResult = text;
        document.getElementById("decryptedResult").innerText = "Guess the decrypted result!";
        document.getElementById("decryptGuessResult").innerText = "";
    }
    function checkEncryptGuess() {
        var userGuess = document.getElementById("encryptGuessInput").value.trim().toLowerCase().replace(/\s+/g, "");
        var resultDisplay = document.getElementById("encryptGuessResult");
        // Convert the encrypted binary to letters
        var encryptedText = encryptedResult.toLowerCase().replace(/\s+/g, "");
        if (userGuess.toLowerCase().replace(/\s+/g, "") === encryptedText) {
            resultDisplay.innerText = "Correct! You guessed the encryption!";
        } else {
            resultDisplay.innerText = "Incorrect. Try again!";
        }
    }
    // Function to convert binary to letters
    function binaryToText(binaryString) {
        var binaryArray = binaryString.split(" ");
        var text = "";
        for (var i = 0; i < binaryArray.length; i++) {
            // Handle extra whitespaces in the binary string
            if (binaryArray[i] !== "") {
                // Convert each binary segment to decimal and then to ASCII character
                var decimalValue = parseInt(binaryArray[i], 2);
                text += String.fromCharCode(decimalValue);
            }
        }
        return text;
    }
    function checkDecryptGuess() {
        var userGuess = document.getElementById("decryptGuessInput").value.trim();
        var resultDisplay = document.getElementById("decryptGuessResult");
        if (userGuess === decryptedResult) {
            resultDisplay.innerText = "Correct! You guessed the decryption!";
        } else {
            resultDisplay.innerText = "Incorrect. Try again!";
        }
    }
</script>
</body>
</html>
```

## Encryption
- The encrypt function is triggered when the Encrypt button is clicked.
- It converts the entered text into binary by iterating through each character, converting it to its binary representation, and ensuring each binary representation has 8 digits.
- The resulting binary is displayed as the encrypted result

## Decryption
- The decrypt function is triggered when the Decrypt button is clicked.
- It converts the entered binary (previously encrypted) back into text by splitting the binary string, converting each segment to decimal, and then to its ASCII character.
- The resulting text is displayed as the decrypted result

## Guessing Encryption
- The checkEncryptGuess function is triggered when the "Check Encryption Guess" button is clicked.
- It compares the user's guess (entered text) with the stored encrypted result, providing feedback on correctness.

## Guessing Decryption
- The checkDecryptGuess function is triggered when the "Check Decryption Guess" button is clicked.
- It compares the user's guess (entered text) with the stored decrypted result, providing feedback on correctness.