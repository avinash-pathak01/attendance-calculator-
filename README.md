//# attendance-calculator-
//Attendance Calculator a modern, professional, and responsive
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Attendance Calculator</title>
  <style>
    /* --- Basic Page Style --- */
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #0078d7, #00b4d8);
      color: #333;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    /* --- Card Container --- */
    .container {
      background: #fff;
      padding: 2.5rem;
      border-radius: 15px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
      text-align: center;
      width: 360px;
      position: relative;
      animation: fadeIn 0.8s ease-in-out;
    }

    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(10px);}
      to {opacity: 1; transform: translateY(0);}
    }

    h1 {
      color: #0078d7;
      margin-bottom: 0.5rem;
    }

    p.subtitle {
      font-size: 0.9rem;
      color: #555;
      margin-bottom: 1.5rem;
    }

    /* --- Input Fields --- */
    input {
      width: 100%;
      margin: 10px 0;
      padding: 10px;
      border: 2px solid #e0e0e0;
      border-radius: 8px;
      font-size: 1rem;
      outline: none;
      transition: border 0.2s ease-in-out;
    }

    input:focus {
      border-color: #0078d7;
      box-shadow: 0 0 5px rgba(0,120,215,0.3);
    }

    /* --- Button --- */
    button {
      background: linear-gradient(90deg, #0078d7, #00b4d8);
      color: white;
      border: none;
      padding: 12px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 1rem;
      margin-top: 10px;
      transition: 0.3s;
      width: 100%;
    }

    button:hover {
      transform: scale(1.05);
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }

    /* --- Result Display --- */
    #result {
      margin-top: 1.5rem;
      font-weight: 500;
      color: #333;
    }

    /* --- Progress Circle --- */
    .progress {
      margin: 20px auto;
      position: relative;
      width: 120px;
      height: 120px;
      border-radius: 50%;
      background: conic-gradient(#0078d7 0deg, #e0e0e0 0deg);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .progress span {
      position: absolute;
      font-weight: 600;
      color: #0078d7;
      font-size: 1.2rem;
    }

    footer {
      margin-top: 1.5rem;
      font-size: 0.8rem;
      color: #777;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Attendance Calculator</h1>
    <p class="subtitle">Find out how many more classes you need 🎓</p>

    <div class="progress">
      <span id="progressText">0%</span>
    </div>

    <input type="number" id="total" placeholder="Total Classes Held">
    <input type="number" id="attended" placeholder="Classes Attended">
    <input type="number" id="target" placeholder="Target Percentage (e.g. 75)">

    <button onclick="calculate()">Calculate</button>
    <p id="result"></p>

    <footer>Made by <b>Avinash Pathak</b> 💡</footer>
  </div>

  <script>
    function calculate() {
      const total = parseFloat(document.getElementById('total').value);
      const attended = parseFloat(document.getElementById('attended').value);
      const target = parseFloat(document.getElementById('target').value);
      const resultEl = document.getElementById('result');
      const progressEl = document.querySelector('.progress');
      const progressText = document.getElementById('progressText');

      if (isNaN(total) || isNaN(attended) || isNaN(target) || total <= 0 || attended < 0) {
        resultEl.textContent = "⚠️ Please enter valid numbers.";
        return;
      }

      const currentPercent = (attended / total) * 100;
      progressEl.style.background = `conic-gradient(#0078d7 ${currentPercent * 3.6}deg, #e0e0e0 0deg)`;
      progressText.textContent = currentPercent.toFixed(1) + "%";

      if (target <= currentPercent) {
        resultEl.textContent = `🎉 Great! You already have ${currentPercent.toFixed(1)}%, which meets or exceeds your target of ${target}%.`;
        return;
      }

      const x = ((target/100)*total - attended) / (1 - target/100);
      const classesNeeded = Math.ceil(x);

      resultEl.innerHTML = `
        📚 You need to attend at least <b>${classesNeeded}</b> more classes in a row
        to reach <b>${target}%</b> attendance.<br>
        (Current: ${currentPercent.toFixed(1)}%)
      `;
    }
  </script>
</body>
</html>
