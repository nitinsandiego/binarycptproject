---
hide: False
toc: False
comments: True
layout: notebook
title: Review Ticket
description: Review Ticket
type: tangibles
courses: {'compsci': {'week': 1}}
---

```python
Key commits:
- Diagrams
- Image Processor
- Puzzle
- Logical Operations

Improvements: 
- find ways to make encoding more efficient

```

# Summary of all Features

# Image Processor


```python
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Image Processing with JS</title>
</head>
<body>
  <label for="imageLink">Image Link:</label>
  <br>
  <input type="text" id="imageLink" placeholder="Enter image link...">
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
      let img = new Image();

      function clearCanvas() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
      }

      function loadAndDisplayImage() {
        const imageLink = document.getElementById('imageLink').value;
        if (!imageLink) {
          alert('Please enter an image link.');
          return;
        }
        clearCanvas();
        img.crossOrigin = 'Anonymous';
        img.onload = function() {
          canvas.width = img.width / 2;
          canvas.height = img.height / 2;
          ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
          processButton.style.display = 'inline';
          reverseHexButton.style.display = 'inline';
          originalButton.style.display = 'none';
        };
        img.onerror = function() {
          alert('Error loading image. Please check the URL and try again.');
          processButton.style.display = 'none';
          reverseHexButton.style.display = 'none';
          originalButton.style.display = 'none';
        };
        img.src = imageLink;
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
```

## Key Points
    - Binary Representation with image pixals
    - Switch modes (black and white) etc
    - User can apply one image to go to original etc
    
## Possible Improvements
    - Work on image adjustment
    - resizing
    - more elements for the feature

[Website](https://nitinsandiego.github.io/binarycptproject//2023/11/26/Binary-Image-Processing.html)

[Diagram](https://nitinsandiego.github.io/binarycptproject//2023/11/26/Binary-Image-processing-diagram.html)

# Binary Encryption
This JavaScript code implements a basic binary encryption technique called XOR (exclusive OR) encryption. The binaryEncrypt function takes a plaintext and a key as input, converts them into binary representation using ASCII values, and performs a bitwise XOR operation between corresponding bits of the plaintext and a repeating key. The resulting binary string represents the encrypted data. The binaryDecrypt function reverses this process to decrypt the binary data back to the original text. It uses the same key and performs the XOR operation again. The binary representation is then converted back to text. The key is repeated to match the length of the input text. It's important to note that XOR encryption is a simple method and may not be suitable for secure applications. For actual security, established encryption algorithms and libraries should be considered. This code provides a basic illustration of binary encryption concepts for educational purposes, showcasing the XOR operation in a JavaScript context.


```python
<html>
<body>
    <h2>Binary Encryption</h2>
    <textarea id="inputText" placeholder="Enter text here"></textarea><br>
    <button onclick="encrypt()">Encrypt</button>
    <button onclick="decrypt()">Decrypt</button><br>
    <h2>Result:</h2>
    <p id="result"></p>
</body>
</html>
<script>
    function encrypt() {
    var input = document.getElementById("inputText").value;
    var binary = '';
    for (var i = 0; i < input.length; i++) {
        binary += input[i].charCodeAt(0).toString(2) + " ";
    }
    document.getElementById("result").innerText = binary.trim();
    }
    function decrypt() {
        var input = document.getElementById("inputText").value;
        var text = '';
        var arr = input.split(" ");
        for (var i = 0; i < arr.length; i++) {
            text += String.fromCharCode(parseInt(arr[i], 2));
        }
        document.getElementById("result").innerText = text;
    }
</script>
```

# Binary Logical Operators
This HTML file titled "Binary Logical Operations" provides a user interface for performing basic binary logical operations. Users can input binary numbers in two fields, choose an operation from the dropdown menu (AND, OR, XOR, or NOT), and click the "Calculate" button to see the result. The interface dynamically adjusts to hide the second input field when the NOT operation is selected since it only requires one input. The JavaScript functions within the script tags handle the logic for performing the selected operation, displaying the binary result, and limiting the inputs and results to 8 bits for a byte-sized representation. The page serves as an interactive tool for exploring binary logical operations and understanding their outcomes.


```python
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

# Binary Puzzle 
The HTML file titled "Binary Puzzle" provides a web-based interface for a binary puzzle-solving game. The puzzle consists of a dynamically generated grid of cells that users can interact with by clicking to toggle the binary values (0, 1, or empty). The objective of the game is to fill the grid following certain rules, and when the user successfully completes the puzzle, an alert congratulates them. The interface includes controls for undoing and redoing moves, as well as a timer displaying the elapsed time since starting the puzzle. The JavaScript functions handle the logic for generating the grid, toggling cell values, managing a history of moves for undo and redo functionality, and checking the validity and completeness of the puzzle based on specified rules for rows and columns. Overall, the webpage offers an engaging interactive experience for solving binary puzzles.


```python
<html>
<head>
    <title>Binary Puzzle</title>
    <style>
    </style>
</head>
<body>
    <div id="puzzle-container">
        <!-- Grid will be generated by JavaScript -->
    </div>
    <div id="controls">
        <button id="undo">Undo</button>
        <button id="redo">Redo</button>
        <div id="timer">Time: 00:00</div>
    </div>
    <script>
    let history = [];
    let currentStep = -1;
    let timerInterval;
    let startTime;
    function generateGrid(size) {
        const container = document.getElementById('puzzle-container');
        container.style.gridTemplateColumns = `repeat(${size}, 50px)`;
        for (let i = 0; i < size; i++) {
            for (let j = 0; j < size; j++) {
                const cell = document.createElement('div');
                cell.className = 'puzzle-cell';
                cell.addEventListener('click', () => toggleCellValue(cell, true));
                container.appendChild(cell);
            }
        }
        startTimer();
        bindButtons();
    }
    function toggleCellValue(cell, addToHistory) {
        if (addToHistory) {
            saveHistory();
        }
        if (cell.textContent === '') {
            cell.textContent = '1';
        } else if (cell.textContent === '1') {
            cell.textContent = '0';
        } else {
            cell.textContent = '';
        }
        if (isPuzzleValid()) {
            alert("Congratulations! You solved the puzzle.");
        }
    }
    function startTimer() {
        startTime = new Date();
        timerInterval = setInterval(updateTimer, 1000);
    }
    function updateTimer() {
        const currentTime = new Date();
        const elapsed = new Date(currentTime - startTime);
        const minutes = elapsed.getUTCMinutes();
        const seconds = elapsed.getUTCSeconds();
        document.getElementById('timer').textContent = `Time: ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    }
    function saveHistory() {
        const state = Array.from(document.querySelectorAll('.puzzle-cell')).map(cell => cell.textContent);
        history = history.slice(0, currentStep + 1);
        history.push(state);
        currentStep++;
    }
    function undo() {
        if (currentStep > 0) {
            currentStep--;
            restoreState(history[currentStep]);
        }
    }
    function redo() {
        if (currentStep < history.length - 1) {
            currentStep++;
            restoreState(history[currentStep]);
        }
    }
    function restoreState(state) {
        const cells = document.querySelectorAll('.puzzle-cell');
        state.forEach((value, index) => {
            cells[index].textContent = value;
        });
    }
    function bindButtons() {
        document.getElementById('undo').addEventListener('click', undo);
        document.getElementById('redo').addEventListener('click', redo);
    }
    function isPuzzleValid() {
        const size = 6; // assuming a 6x6 grid
        for (let i = 0; i < size; i++) {
            if (!checkRow(i, size) || !checkColumn(i, size)) {
                return false;
            }
        }
        return isPuzzleComplete(); // Check if the puzzle is complete
    }
    function isPuzzleComplete() {
        // Check if all cells are filled and the puzzle follows the rules
        const cells = document.querySelectorAll('.puzzle-cell');
        for (let cell of cells) {
            if (cell.textContent === '') {
                return false; // Puzzle is not complete if any cell is empty
            }
        }
        return true;
    }
    function checkRow(row, size) {
        let count = { '0': 0, '1': 0, '': 0 };
        let lastValue = null, repeat = 0;
        for (let col = 0; col < size; col++) {
            let cellIndex = row * size + col;
            let value = document.querySelectorAll('.puzzle-cell')[cellIndex].textContent;
            count[value]++;
            if (value === lastValue) {
                repeat++;
                if (repeat > 1 && value !== '') return false; // More than two same numbers adjacent
            } else {
                repeat = 0;
            }
            lastValue = value;
        }
        return count['0'] === count['1'] || count[''] > 0; // Equal number of '0's and '1's or empty cells present
    }
    function checkColumn(col, size) {
        let count = { '0': 0, '1': 0, '': 0 };
        let lastValue = null, repeat = 0;
        for (let row = 0; row < size; row++) {
            let cellIndex = row * size + col;
            let value = document.querySelectorAll('.puzzle-cell')[cellIndex].textContent;
            count[value]++;
            if (value === lastValue) {
                repeat++;
                if (repeat > 1 && value !== '') return false; // More than two same numbers adjacent
            } else {
                repeat = 0;
            }
            lastValue = value;
        }
        return count['0'] === count['1'] || count[''] > 0; // Equal number of '0's and '1's or empty cells present
    }
    document.addEventListener('DOMContentLoaded', () => {
        generateGrid(6); // Initialize 6x6 grid
    });
</script>

</body>
</html>
```

# Binary game
The HTML file titled "Binary Guessing Game" presents an interactive game where players attempt to guess a randomly generated binary number within a specified range. The webpage includes a welcoming header and a user input section featuring an input field for binary guesses, constrained by a pattern for valid binary input (0s and 1s) with a maximum length of 8 digits. A "Guess" button triggers the JavaScript function makeAGuess(), which validates the user input, converts it to decimal, and provides feedback on whether the guess is correct or hints at whether it's too high or too low. The game dynamically adjusts the range of possible values based on the user's guesses, and the output is displayed in a designated div element. The game concludes with a congratulatory message upon successfully guessing the correct binary number, accompanied by the number of attempts made. Overall, the Binary Guessing Game offers an engaging and educational experience in binary number manipulation and guessing.


```python
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary Guessing Game</title>
</head>
<body>
    <h1>Welcome to the Binary Guessing Game!</h1>
    <div>
        <!-- Updated input field with pattern and maxlength -->
        <input type="text" id="userGuess" placeholder="Enter your binary guess" pattern="^[0-1]{1,8}$" maxlength="8"/>
        <button onclick="makeAGuess()">Guess</button>
    </div>
    <div44 id="output"></div44>
    <script>
        var minValue = 0;
        var maxValue = 255;
        var secretBinary = generateRandomBinary(minValue, maxValue);
        var attempts = 0;
        var outputDiv = document.getElementById('output');
        function generateRandomBinary(minValue, maxValue) {
            return (Math.floor(Math.random() * (maxValue - minValue + 1)) + minValue).toString(2);
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
                if (playerGuess === secretBinary) {
                    outputDiv.innerHTML = `Congratulations! You guessed the correct binary number ${secretBinary} (decimal: ${guessDecimal}) in ${attempts} attempts.`;
                } else {
                    if (playerGuess < secretBinary) {
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
    </script>
</body>
</html>
```

# Binary Song Converter
The HTML file titled "Song to Binary Converter" provides a simple yet effective tool for converting song lyrics into their binary representation. The webpage features a user-friendly interface with a heading announcing the purpose of the tool, a textarea for users to input song lyrics, and an output section displaying the binary representation of the entered lyrics. The JavaScript function convertToBinary() is triggered whenever the user inputs or modifies the song lyrics, converting each character into its ASCII code and then representing it as an 8-bit binary string. The resulting binary strings are concatenated with spaces and displayed in the designated output div. This tool allows users to explore the binary encoding of textual data, providing an educational and entertaining experience for those interested in the intersection of music and computing.


```python
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Song to Binary Converter</title>
</head>
<body>
    <h1>Song to Binary Converter</h1>
    <textarea id="songInput" placeholder="Enter song lyrics here..." rows="10" cols="50" oninput="convertToBinary()"></textarea>
    <h2>Binary Output</h2>
    <div id="binaryOutput"></div>
    <script>
        function convertToBinary() {
            const lyrics = document.getElementById('songInput').value;
            const binaryOutput = lyrics.split('').map(char => {
                return char.charCodeAt(0).toString(2).padStart(8, '0');
            }).join(' ');
            document.getElementById('binaryOutput').innerText = binaryOutput;
        }
    </script>
</body>
</html>
```

# Feedback .97/1 Tara's group
Their sass styling was very good. It was a good balance of stylish while also still being usable and readable. The binary puzzle could have added a description on how to win the puzzle because it was confusing how it worked. The Image processing had a lot of impressive features and he logical operators feature had all the proper features and worked perfectly. The Guessing Game could have had more helpful tips because the number range was very large as it was a byte size range. The song converter was good and correctly convertted song lyrics to binary. Overall, this group did a great job with their features.


