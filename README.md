<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Offer Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #271b0c;
      --primary-hover: #b02125;
      --background: #f9f9f9;
      --card-bg: #ffffff;
      --text: #333333;
      --border-radius: 12px;
    }
    
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    
    body {
      font-family: 'Montserrat', sans-serif;
      background: var(--background);
      color: var(--text);
      padding: 20px;
      line-height: 1.6;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    .calculator-container {
      width: 100%;
      max-width: 500px;
      background: var(--card-bg);
      padding: 30px;
      border-radius: var(--border-radius);
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
    
    h2 {
      margin-bottom: 20px;
      color: var(--primary);
      text-align: center;
    }
    
    .input-group {
      margin-bottom: 20px;
    }
    
    label {
      display: block;
      margin-bottom: 8px;
      font-weight: 500;
    }
    
    input[type="text"] {
      width: 100%;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 6px;
      font-family: inherit;
      margin-bottom: 15px;
    }
    
    .range-container {
      display: flex;
      flex-direction: column;
      margin-bottom: 20px;
    }
    
    .range-header {
      display: flex;
      justify-content: space-between;
      margin-bottom: 8px;
    }
    
    input[type="range"] {
      width: 100%;
      margin-bottom: 10px;
      accent-color: var(--primary);
    }
    
    .range-labels {
      display: flex;
      justify-content: space-between;
      font-size: 12px;
      color: #666;
    }
    
    .button {
      display: block;
      width: 100%;
      padding: 12px 20px;
      background-color: var(--primary);
      color: #fff;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      font-family: inherit;
      font-weight: 600;
      font-size: 16px;
      margin: 20px 0;
    }
    
    .button:hover {
      background-color: var(--primary-hover);
    }
    
    .result {
      background-color: #f5f5f5;
      padding: 15px;
      border-radius: 8px;
      margin-top: 20px;
      display: none;
    }
    
    .result.active {
      display: block;
    }
    
    .result-value {
      font-size: 24px;
      font-weight: 600;
      color: var(--primary);
      margin: 10px 0;
    }
    
    .disclaimer {
      font-size: 12px;
      color: #777;
      margin-top: 20px;
      padding-top: 15px;
      border-top: 1px solid #eee;
    }
    
    @media (max-width: 600px) {
      .calculator-container {
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="calculator-container">
    <h2>Offer Calculator</h2>
    
    <div class="input-group">
      <label for="ebitda">EBITDA (ƒ)</label>
      <input 
        type="text" 
        id="ebitda" 
        placeholder="Enter EBITDA" 
        value="760,000"
      >
    </div>
    
    <div class="range-container">
      <div class="range-header">
        <label for="multipleRange">In how many years would you like to see Return On Investment?</label>
        <span id="multipleValue">3</span>
      </div>
      <input
        type="range"
        min="1"
        max="10"
        value="3"
        id="multipleRange"
      >
      <div class="range-labels">
        <span>1</span>
        <span>5</span>
        <span>10</span>
      </div>
    </div>
    
    <button class="button" id="calculateBtn">Calculate Offer</button>
    
    <div class="result" id="resultContainer">
      <h3>Estimated Offer</h3>
      <div class="result-value" id="offerResult"></div>
      <p>Based on <span id="ebitdaDisplay"></span> EBITDA with a <span id="multipleDisplay"></span> years return period.</p>
    </div>
    
    <p class="disclaimer">Disclaimer: The results provided by this calculator are for informational purposes only and do not constitute financial advice. Actual business offers may vary based on multiple factors. Consult with a financial advisor for a professional assessment.</p>
  </div>

  <script>
    const ebitdaInput = document.getElementById('ebitda');
    const multipleRange = document.getElementById('multipleRange');
    const multipleValue = document.getElementById('multipleValue');
    const calculateBtn = document.getElementById('calculateBtn');
    const resultContainer = document.getElementById('resultContainer');
    const offerResult = document.getElementById('offerResult');
    const ebitdaDisplay = document.getElementById('ebitdaDisplay');
    const multipleDisplay = document.getElementById('multipleDisplay');

    ebitdaInput.addEventListener('input', () => {
      const value = ebitdaInput.value.replace(/,/g, '').replace(/\B(?=(\d{3})+(?!\d))/g, ',');
      ebitdaInput.value = value;
    });

    multipleRange.addEventListener('input', () => {
      multipleValue.textContent = multipleRange.value;
    });

    function formatCurrency(num) {
      return 'ƒ' + num.toLocaleString('en-US');
    }

    calculateBtn.addEventListener('click', () => {
      const ebitda = parseFloat(ebitdaInput.value.replace(/,/g, '')) || 0;
      const multiple = parseFloat(multipleRange.value);
      const offer = ebitda * multiple;

      offerResult.textContent = formatCurrency(offer);
      ebitdaDisplay.textContent = formatCurrency(ebitda);
      multipleDisplay.textContent = `${multiple}`;

      resultContainer.classList.add('active');
    });
  </script>
</body>
</html>
