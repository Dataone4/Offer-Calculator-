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
    }
    
    .calculator-container {
      max-width: 500px;
      margin: 0 auto;
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
    
    input[type="number"] {
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
    
    .link-container {
      text-align: center;
      margin: 10px 0;
    }
    
    .learn-more-link {
      color: var(--primary);
      text-decoration: none;
      font-size: 14px;
      font-weight: 500;
      transition: color 0.3s ease;
    }
    
    .learn-more-link:hover {
      color: var(--primary-hover);
      text-decoration: underline;
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
    
    .embed-section {
      margin-top: 30px;
      padding-top: 20px;
      border-top: 1px solid #eee;
    }
    
    .embed-title {
      font-size: 16px;
      font-weight: 600;
      margin-bottom: 10px;
    }
    
    .embed-code {
      background-color: #f5f5f5;
      border: 1px solid #ddd;
      border-radius: 6px;
      padding: 10px;
      font-family: monospace;
      font-size: 12px;
      overflow-x: auto;
      white-space: nowrap;
      margin-bottom: 10px;
    }
    
    .copy-button {
      background-color: var(--primary);
      color: white;
      border: none;
      border-radius: 4px;
      padding: 8px 12px;
      font-size: 12px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    
    .copy-button:hover {
      background-color: var(--primary-hover);
    }
    
    .copy-success {
      display: none;
      color: green;
      font-size: 12px;
      margin-left: 10px;
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
      <label for="annualProfit">Annual Profit (ƒ)</label>
      <input 
        type="number" 
        id="annualProfit" 
        placeholder="Enter annual profit" 
        value="760000"
      >
    </div>
    
    <div class="range-container">
      <div class="range-header">
        <label for="multipleRange">Multiple</label>
        <span id="multipleValue">3x</span>
      </div>
      <input
        type="range"
        min="1"
        max="10"
        value="3"
        id="multipleRange"
      >
      <div class="range-labels">
        <span>1x</span>
        <span>5x</span>
        <span>10x</span>
      </div>
    </div>
    
    <button class="button" id="calculateBtn">Calculate Offer</button>
    
    <div class="link-container">
      <a href="#" class="learn-more-link" id="learnMoreLink">Learn more about how we calculate offers</a>
    </div>
    
    <div class="result" id="resultContainer">
      <h3>Estimated Offer</h3>
      <div class="result-value" id="offerResult"></div>
      <p>Based on <span id="profitDisplay"></span> annual profit with a <span id="multipleDisplay"></span> multiple.</p>
    </div>
    
    <p class="disclaimer">Disclaimer: The results provided by this calculator are for informational purposes only and do not constitute financial advice. Actual business offers may vary based on multiple factors. Consult with a financial advisor for a professional assessment.</p>
    
    <div class="embed-section">
      <div class="embed-title">Embed this calculator on your website</div>
      <div class="embed-code" id="embedCode">
        &lt;iframe src="https://your-website.com/offer-calculator.html" width="100%" height="600" frameborder="0" scrolling="no"&gt;&lt;/iframe&gt;
      </div>
      <div>
        <button class="copy-button" id="copyButton">Copy embed code</button>
        <span class="copy-success" id="copySuccess">Copied!</span>
      </div>
    </div>
  </div>

  <script>
    // Get DOM elements
    const annualProfitInput = document.getElementById('annualProfit');
    const multipleRange = document.getElementById('multipleRange');
    const multipleValue = document.getElementById('multipleValue');
    const calculateBtn = document.getElementById('calculateBtn');
    const resultContainer = document.getElementById('resultContainer');
    const offerResult = document.getElementById('offerResult');
    const profitDisplay = document.getElementById('profitDisplay');
    const multipleDisplay = document.getElementById('multipleDisplay');
    const learnMoreLink = document.getElementById('learnMoreLink');
    const copyButton = document.getElementById('copyButton');
    const embedCode = document.getElementById('embedCode');
    const copySuccess = document.getElementById('copySuccess');
    
    // Update multiple value display when slider changes
    multipleRange.addEventListener('input', () => {
      const value = multipleRange.value;
      multipleValue.textContent = `${value}x`;
    });
    
    // Format number with commas and currency symbol
    function formatCurrency(num) {
      return 'ƒ' + num.toLocaleString('en-US');
    }
    
    // Calculate offer when button is clicked
    calculateBtn.addEventListener('click', () => {
      // Get values
      const profit = parseFloat(annualProfitInput.value) || 0;
      const multiple = parseFloat(multipleRange.value);
      
      // Calculate offer
      const offer = profit * multiple;
      
      // Display results
      offerResult.textContent = formatCurrency(offer);
      profitDisplay.textContent = formatCurrency(profit);
      multipleDisplay.textContent = `${multiple}x`;
      
      // Show result container
      resultContainer.classList.add('active');
    });
    
    // Learn more link handler (you can customize this)
    learnMoreLink.addEventListener('click', (e) => {
      e.preventDefault();
      // You can add custom behavior here, like opening a modal or navigating to another page
      alert('You can customize this link to point to more information about your offer calculation process.');
    });
    
    // Copy embed code functionality
    copyButton.addEventListener('click', () => {
      // Create a temporary textarea element to copy from
      const textarea = document.createElement('textarea');
      textarea.value = embedCode.textContent.trim();
      document.body.appendChild(textarea);
      
      // Select and copy the text
      textarea.select();
      document.execCommand('copy');
      
      // Remove the temporary textarea
      document.body.removeChild(textarea);
      
      // Show success message
      copySuccess.style.display = 'inline';
      setTimeout(() => {
        copySuccess.style.display = 'none';
      }, 2000);
    });
    
    // Initialize calculation on page load
    window.addEventListener('DOMContentLoaded', () => {
      // Set initial multiple value display
      multipleValue.textContent = `${multipleRange.value}x`;
    });
  </script>
</body>
</html>
