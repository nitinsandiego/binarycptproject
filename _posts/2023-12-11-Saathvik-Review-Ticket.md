---
hide: False
toc: False
comments: True
layout: notebook
title: Saathvik Gampa Review Ticket
description: Saathvik Gampa Review Ticket
type: tangibles
courses: {'compsci': {'week': 2}}
---

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

## If I had more time
If I had more time I would add....

    A better design

    More friendly UI.

    Progress Bar for the user

    Have an intro that shows how binary works.

## Problems I came accross
    My "Play Again" button wouldnt work, fixed this with help of my classmates, teammates and internet.
    Figuring out how to calculate the binary value, to do this I used the help of ChatGPT.