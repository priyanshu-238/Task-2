<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f8f9fa;
      margin: 0;
      padding: 0;
    }
    h1 {
      margin: 20px 0;
      color: #333;
    }
    .calculator {
      display: inline-block;
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    .display {
      width: 100%;
      height: 50px;
      margin-bottom: 20px;
      font-size: 1.5rem;
      text-align: right;
      border: 1px solid #ccc;
      border-radius: 5px;
      padding: 10px;
      box-sizing: border-box;
    }
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }
    .button {
      padding: 15px;
      font-size: 1.2rem;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background 0.3s;
    }
    .button:hover {
      background: #0056b3;
    }
    .button.operator {
      background: #28a745;
    }
    .button.operator:hover {
      background: #1c7a2f;
    }
    .button.clear {
      background: #dc3545;
    }
    .button.clear:hover {
      background: #a71d2a;
    }
  </style>
</head>
<body>
  <h1>Simple Calculator</h1>
  <div class="calculator">
    <input type="text" class="display" id="display" disabled>
    <div class="buttons">
      <button class="button" onclick="appendNumber('7')">7</button>
      <button class="button" onclick="appendNumber('8')">8</button>
      <button class="button" onclick="appendNumber('9')">9</button>
      <button class="button operator" onclick="setOperator('/')">/</button>

      <button class="button" onclick="appendNumber('4')">4</button>
      <button class="button" onclick="appendNumber('5')">5</button>
      <button class="button" onclick="appendNumber('6')">6</button>
      <button class="button operator" onclick="setOperator('*')">*</button>

      <button class="button" onclick="appendNumber('1')">1</button>
      <button class="button" onclick="appendNumber('2')">2</button>
      <button class="button" onclick="appendNumber('3')">3</button>
      <button class="button operator" onclick="setOperator('-')">-</button>

      <button class="button" onclick="appendNumber('0')">0</button>
      <button class="button" onclick="appendNumber('.')">.</button>
      <button class="button clear" onclick="clearDisplay()">C</button>
      <button class="button operator" onclick="setOperator('+')">+</button>
    </div>
    <button class="button operator" style="width: 100%; margin-top: 10px;" onclick="calculateResult()">=</button>
  </div>

  <script>
    let currentNumber = '';
    let previousNumber = '';
    let operator = '';

    function appendNumber(number) {
      currentNumber += number;
      updateDisplay();
    }

    function setOperator(op) {
      if (currentNumber === '') return;
      if (previousNumber !== '') calculateResult();
      operator = op;
      previousNumber = currentNumber;
      currentNumber = '';
    }

    function calculateResult() {
      if (previousNumber === '' || currentNumber === '' || operator === '') return;

      const num1 = parseFloat(previousNumber);
      const num2 = parseFloat(currentNumber);
      let result = 0;

      switch (operator) {
        case '+':
          result = num1 + num2;
          break;
        case '-':
          result = num1 - num2;
          break;
        case '*':
          result = num1 * num2;
          break;
        case '/':
          result = num1 / num2;
          break;
      }

      currentNumber = result.toString();
      previousNumber = '';
      operator = '';
      updateDisplay();
    }

    function clearDisplay() {
      currentNumber = '';
      previousNumber = '';
      operator = '';
      updateDisplay();
    }

    function updateDisplay() {
      document.getElementById('display').value = currentNumber;
    }
  </script>
</body>
</html>
