---
hide: True
layout: notebook
title: Binary Encryption
type: hacks
courses: {'compsci': {'week': 1}}
---

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
</body>
</html>

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