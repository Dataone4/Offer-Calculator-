<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Valuation Multiple Calculator</title>
  <style>
    body {
      font-family: 'Montserrat', sans-serif;
      background: transparent;
      padding: 20px;
      max-width: 400px;
      margin: auto;
    }
    .button {
      padding: 10px 20px;
      background-color: #271b0c;
      color: #fff;
      border: none;
      border-radius: 20px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    .button:hover {
      background-color: #b02125;
    }
    input[type=range] {
      width: 100%;
      margin-bottom: 10px;
    }
    p {
      margin-top: 10px;
    }
    .disclaimer {
      font-size: 12px;
      color: #555;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div>
    <input
      type="range"
      min="1"
      max="10"
      value="3"
      id="multipleRange"
    >
    <p>Selected Multiple: <span id="multipleValue">3</span></p>
    <button class="button" onclick="calculateValuation()">Calculate Valuation</button>
    <p id="valuationResult"></p>
    <p class="disclaimer">Disclaimer: The results provided by this calculator are for informational purposes only and do not constitute financial advice. Actual business valuations may vary based on multiple factors. Consult with a financial advisor for a professional assessment.</p>
  </div>

  <script>
    const annualProfit2024 = 760000;
    const multipleRange = document.getElementById('multipleRange');
    const multipleValue = document.getElementById('multipleValue');
    const valuationResult = document.getElementById('valuationResult');

    multipleRange.addEventListener('input', () => {
      multipleValue.textContent = multipleRange.value;
    });

    function formatNumber(num) {
      return num.toLocaleString('en-US');
    }

    function calculateValuation() {
      const multiple = Number(multipleRange.value);
      const valuation = annualProfit2024 * multiple;
      valuationResult.textContent = `Estimated Valuation: ƒ${formatNumber(valuation)}`;
    }
  </script>
</body>
</html>
