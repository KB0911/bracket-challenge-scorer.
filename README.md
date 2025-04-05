# bracket-challenge-scorer.
An interactive NCAA Bracket Challenge Scorer.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>NCAA Bracket Challenge Scorer</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    .container { display: flex; gap: 40px; }
    .form-section { border: 1px solid #ccc; padding: 20px; border-radius: 8px; }
    h2 { margin-top: 0; }
    label { display: block; margin-top: 10px; }
    input[type="number"] { width: 60px; margin-left: 10px; }
    .results { margin-top: 20px; font-weight: bold; }
  </style>
</head>
<body>
  <h1>NCAA Bracket Challenge Score Calculator</h1>

  <div class="container">
    <div class="form-section">
      <h2>Men's Bracket</h2>
      <form id="mensForm">
        <label>Round 1 correct picks (1pt): <input type="number" id="menR1" min="0" max="32"></label>
        <label>Round 2 correct picks (2pt): <input type="number" id="menR2" min="0" max="16"></label>
        <label>Sweet 16 (4pt): <input type="number" id="menR3" min="0" max="8"></label>
        <label>Elite 8 (8pt): <input type="number" id="menR4" min="0" max="4"></label>
        <label>Final 4 (16pt): <input type="number" id="menR5" min="0" max="2"></label>
        <label>Championship (32pt): <input type="number" id="menR6" min="0" max="1"></label>
        <div class="results" id="menTotal">Total Score: 0</div>
      </form>
    </div>

    <div class="form-section">
      <h2>Women's Bracket</h2>
      <form id="womensForm">
        <label>Round 1 correct picks (1pt): <input type="number" id="womenR1" min="0" max="32"></label>
        <label>Round 2 correct picks (2pt): <input type="number" id="womenR2" min="0" max="16"></label>
        <label>Sweet 16 (4pt): <input type="number" id="womenR3" min="0" max="8"></label>
        <label>Elite 8 (8pt): <input type="number" id="womenR4" min="0" max="4"></label>
        <label>Final 4 (16pt): <input type="number" id="womenR5" min="0" max="2"></label>
        <label>Championship (32pt): <input type="number" id="womenR6" min="0" max="1"></label>
        <div class="results" id="womenTotal">Total Score: 0</div>
      </form>
    </div>
  </div>

  <div style="margin-top: 30px;">
    <button onclick="calculateScores()">Calculate Combined Score</button>
    <div class="results" id="combinedScore">Combined Score: 0</div>
  </div>

  <script>
    function calculateBracketScore(prefix) {
      const multipliers = [1, 2, 4, 8, 16, 32];
      let total = 0;
      for (let i = 1; i <= 6; i++) {
        const value = parseInt(document.getElementById(`${prefix}R${i}`).value) || 0;
        total += value * multipliers[i - 1];
      }
      return total;
    }

    function calculateScores() {
      const menScore = calculateBracketScore('men');
      const womenScore = calculateBracketScore('women');

      document.getElementById('menTotal').textContent = `Total Score: ${menScore}`;
      document.getElementById('womenTotal').textContent = `Total Score: ${womenScore}`;
      document.getElementById('combinedScore').textContent = `Combined Score: ${menScore + womenScore}`;
    }
  </script>
</body>
</html>
