---
comments: True
layout: notebook
hide: True
title: Formula 1 Drivers
description: Formula 1 Drivers Contest
type: hacks
toc: True
courses: {'compsci': {'week': 1}}
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Champion Bracket</title>
  <style>
    .bracket {
      position: relative;
      display: flex;
      justify-content: space-around;
    }
    .round {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .match {
      margin: 10px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    img {
      max-width: 100px;
      max-height: 100px;
      cursor: pointer;
    }
    .selected {
      border: 2px solid green;
      pointer-events: none; /* Disable further clicks on the same player */
    }
    .editable {
      border: 2px dashed blue;
      pointer-events: auto; /* Enable clicks on the editable column */
    }
    .bracket1 {
      border-right: 2px solid black;
    }
    .bracket2 {
      border-left: 2px solid black;
    }
    canvas {
      position: absolute;
      top: 0;
      left: 0;
      pointer-events: none;
    }
    .connecting-line {
      position: absolute;
      background-color: transparent;
      pointer-events: none;
      z-index: 1;
    }

    .highlight {
      background-color: #00ff00; /* Neon green color */
    }
  </style>
</head>
<body>
<div class="bracket">
  <canvas id="canvas" width="600" height="400"></canvas>
  <div class="round bracket1" id="round1">
    <div class="match">
      <img id="player1" onclick="moveToSemi('player1', 'semi1')" src="../../../images/FernandoAlonso.png" alt="Player 1">
      <p>VS</p>
      <img id="player2" onclick="moveToSemi('player2', 'semi1')" src="../../../images/LandoNorris.png" alt="Player 2">
    </div>
    <div class="match">
      <img id="player3" onclick="moveToSemi('player3', 'semi2')" src="../../../images/LewisHamilton.png" alt="Player 3">
      <p>VS</p>
      <img id="player4" onclick="moveToSemi('player4', 'semi2')" src="../../../images/MaxVerstappen.png" alt="Player 4">
    </div>
  </div>
  <div class="round bracket2 editable" id="round2">
    <div class="match">
      <img id="semi1" onclick="moveToChampion('semi1', 'finals')" src="" alt="Semi 1">
      <p>VS</p>
      <img id="semi2" onclick="moveToChampion('semi2', 'finals')" src="" alt="Semi 2">
    </div>
  </div>
  <div class="round finals" id="finals">
    <div class="match">
      <img id="champion" src="" alt="Champion">
      <p>Champion</p>
    </div>
  </div>
</div>
<script>
  let selectedPlayers = {};
  let selectedColumn = null; // Keep track of the selected column
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');
  function moveToSemi(player, semiId) {
    // Move the selected player to the semi-final bracket
    document.getElementById(semiId).src = document.getElementById(player).src;
    selectedPlayers[semiId] = document.getElementById(player).src;
    // Disable further clicks on the same player
    document.getElementById(player).style.pointerEvents = 'none';
    // Draw connecting lines
    drawConnectingLines(semiId);
    // Highlight the selected column
    highlightColumn(semiId);
  }
  function moveToChampion(player, columnId) {
    // Move the selected player to the champion bracket
    document.getElementById(columnId).src = selectedPlayers[player];
    selectedPlayers[columnId] = selectedPlayers[player];
    document.getElementById(columnId).style.pointerEvents = 'auto';
    // Disable further clicks on the same player
    document.getElementById(player).style.pointerEvents = 'none';
    // Check if both semi-final winners are selected for the finals
    if (selectedPlayers['semi1'] && selectedPlayers['semi2']) {
      decideChampion();
    }
    // Draw connecting lines
    drawConnectingLines(columnId);
    // Highlight the selected column
    highlightColumn(columnId);
  }
  function highlightColumn(columnId) {
    // Remove highlight from the previously selected column
    if (selectedColumn) {
      document.getElementById(selectedColumn).classList.remove('selected');
    }
    // Highlight the current selected column
    document.getElementById(columnId).classList.add('selected');
    selectedColumn = columnId;
  }
  function decideChampion() {
    const shuffledSemiFinalists = shuffleArray(['semi1', 'semi2']);
    const champion = shuffledSemiFinalists[0];
    document.getElementById('champion').src = selectedPlayers[champion];
    animateChampion();
  }
  function drawConnectingLines(columnId) {
    // Drawing connecting lines between matches
    const columnRect = document.getElementById(columnId).getBoundingClientRect();
    const semi1Rect = document.getElementById('semi1').getBoundingClientRect();
    const semi2Rect = document.getElementById('semi2').getBoundingClientRect();
    const startX = columnRect.left + columnRect.width / 2;
    const startY = columnRect.bottom;
    const semi1X = semi1Rect.left + semi1Rect.width / 2;
    const semi1Y = semi1Rect.top;
    const semi2X = semi2Rect.left + semi2Rect.width / 2;
    const semi2Y = semi2Rect.top;
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.beginPath();
    ctx.moveTo(startX, startY);
    ctx.lineTo(semi1X, semi1Y);
    ctx.lineTo(semi2X, semi2Y);
    ctx.stroke();
    // Create a connecting line element
    const line = document.createElement('div');
    line.className = 'connecting-line';
    document.body.appendChild(line);
    // Set line coordinates and length
    const length = Math.sqrt((semi2X - semi1X)**2 + (semi2Y - semi1Y)**2);
    const angle = Math.atan2(semi2Y - semi1Y, semi2X - semi1X) * 180 / Math.PI;
    line.style.width = length + 'px';
    line.style.height = '2px'; // Adjust line thickness if needed
    line.style.transform = `rotate(${angle}deg)`;
    line.style.top = startY + 'px';
    line.style.left = startX + 'px';
    // Add click event to highlight the line
    line.addEventListener('click', function() {
      line.classList.toggle('highlight');
    });
  }
  function animateChampion() {
    // Add animation or any other action for the champion
    console.log('Champion:', selectedPlayers['champion']);
  }
  function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
    return array;
  }
</script>
</body>
</html>





