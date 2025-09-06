<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Live Age Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #6dd5ed, #2193b0);
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .container {
      background: #fff;
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 6px 15px rgba(0,0,0,0.3);
      max-width: 400px;
      width: 90%;
      text-align: center;
    }
    h2 {
      margin-bottom: 20px;
      color: #333;
    }
    input {
      padding: 12px;
      margin: 10px 0;
      width: 100%;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 16px;
    }
    .buttons {
      display: flex;
      gap: 10px;
      margin-top: 10px;
    }
    button {
      flex: 1;
      padding: 12px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      transition: background 0.3s ease-in-out;
    }
    .start-btn {
      background: #4CAF50;
      color: white;
    }
    .start-btn:hover {
      background: #45a049;
    }
    .reset-btn {
      background: #e74c3c;
      color: white;
    }
    .reset-btn:hover {
      background: #c0392b;
    }
    .result {
      margin-top: 20px;
      font-size: 18px;
      font-weight: bold;
      color: #222;
      background: #f9f9f9;
      padding: 12px;
      border-radius: 8px;
      min-height: 40px;
    }

    /* Responsive Design */
    @media (max-width: 500px) {
      body {
        padding: 20px;
      }
      .container {
        padding: 20px;
      }
      h2 {
        font-size: 20px;
      }
      input, button {
        font-size: 14px;
      }
      .result {
        font-size: 16px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Live Age Calculator</h2>
    <input type="date" id="dob" />
    
    <div class="buttons">
      <button class="start-btn" onclick="startAgeCalculation()">Start</button>
      <button class="reset-btn" onclick="resetCalculator()">Reset</button>
    </div>

    <div class="result" id="result">⏳ Waiting for input...</div>
  </div>

  <script>
    let intervalId = null;

    function startAgeCalculation() {
      const dob = document.getElementById("dob").value;
      const resultDiv = document.getElementById("result");

      if (!dob) {
        resultDiv.innerHTML = "⚠️ Please select your Date of Birth!";
        clearInterval(intervalId);
        return;
      }

      // Clear any previous intervals before starting a new one
      clearInterval(intervalId);

      intervalId = setInterval(() => {
        const today = new Date();
        const birthDate = new Date(dob);

        let years = today.getFullYear() - birthDate.getFullYear();
        let months = today.getMonth() - birthDate.getMonth();
        let days = today.getDate() - birthDate.getDate();
        let hours = today.getHours() - birthDate.getHours();
        let minutes = today.getMinutes() - birthDate.getMinutes();
        let seconds = today.getSeconds() - birthDate.getSeconds();

        // Adjust values if negative
        if (seconds < 0) {
          minutes--;
          seconds += 60;
        }
        if (minutes < 0) {
          hours--;
          minutes += 60;
        }
        if (hours < 0) {
          days--;
          hours += 24;
        }
        if (days < 0) {
          months--;
          const prevMonth = new Date(today.getFullYear(), today.getMonth(), 0).getDate();
          days += prevMonth;
        }
        if (months < 0) {
          years--;
          months += 12;
        }

        resultDiv.innerHTML =
          `🎉 You are <b>${years}</b> years, <b>${months}</b> months, <b>${days}</b> days, ` +
          `<b>${hours}</b> hours, <b>${minutes}</b> minutes, and <b>${seconds}</b> seconds old.`;
      }, 1000);
    }

    function resetCalculator() {
      clearInterval(intervalId);
      document.getElementById("dob").value = "";
      document.getElementById("result").innerHTML = "⏳ Waiting for input...";
    }
  </script>
</body>
</html>
