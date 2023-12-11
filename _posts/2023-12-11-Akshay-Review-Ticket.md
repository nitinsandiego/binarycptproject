---
hide: False
toc: False
comments: True
layout: notebook
title: Akshay Nagesh Review Ticket
description: Akshay Nagesh Review Ticket
type: tangibles
courses: {'compsci': {'week': 2}}
---

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
