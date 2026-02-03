# Simple-Calculator-Web
Simple Calculator Web
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        .calculator {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            padding: 20px;
            width: 100%;
            max-width: 320px;
        }

        .display {
            background: #2d3436;
            color: #00ff88;
            font-size: 2.5em;
            font-weight: 300;
            padding: 20px;
            border-radius: 10px;
            text-align: right;
            margin-bottom: 20px;
            word-wrap: break-word;
            word-break: break-all;
            min-height: 60px;
            display: flex;
            align-items: flex-end;
            justify-content: flex-end;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        button {
            padding: 20px;
            font-size: 1.5em;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 500;
        }

        button:active {
            transform: scale(0.95);
        }

        .number {
            background: #f0f0f0;
            color: #2d3436;
        }

        .number:hover {
            background: #e0e0e0;
        }

        .operator {
            background: #667eea;
            color: white;
        }

        .operator:hover {
            background: #5568d3;
        }

        .equals {
            background: #00ff88;
            color: #2d3436;
            grid-column: span 2;
            font-weight: 600;
        }

        .equals:hover {
            background: #00dd6e;
        }

        .clear {
            background: #ff6b6b;
            color: white;
            grid-column: span 2;
            font-weight: 600;
        }

        .clear:hover {
            background: #ee5a52;
        }

        .delete {
            background: #ffa502;
            color: white;
        }

        .delete:hover {
            background: #ff9100;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="clear" onclick="clearDisplay()">AC</button>
            <button class="delete" onclick="deleteLast()">DEL</button>
            <button class="operator" onclick="appendOperator('/')">/</button>
            <button class="operator" onclick="appendOperator('*')">×</button>

            <button class="number" onclick="appendNumber('7')">7</button>
            <button class="number" onclick="appendNumber('8')">8</button>
            <button class="number" onclick="appendNumber('9')">9</button>
            <button class="operator" onclick="appendOperator('-')">−</button>

            <button class="number" onclick="appendNumber('4')">4</button>
            <button class="number" onclick="appendNumber('5')">5</button>
            <button class="number" onclick="appendNumber('6')">6</button>
            <button class="operator" onclick="appendOperator('+')">+</button>

            <button class="number" onclick="appendNumber('1')">1</button>
            <button class="number" onclick="appendNumber('2')">2</button>
            <button class="number" onclick="appendNumber('3')">3</button>
            <button class="operator" onclick="appendOperator('.')">.</button>

            <button class="number" onclick="appendNumber('0')" style="grid-column: span 2;">0</button>
            <button class="equals" onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let currentValue = '0';
        let previousValue = '';
        let operator = null;
        let shouldResetDisplay = false;

        function updateDisplay() {
            display.textContent = currentValue;
        }

        function appendNumber(num) {
            if (shouldResetDisplay) {
                currentValue = num;
                shouldResetDisplay = false;
            } else {
                if (currentValue === '0' && num !== '.') {
                    currentValue = num;
                } else if (num === '.' && currentValue.includes('.')) {
                    return;
                } else {
                    currentValue += num;
                }
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (operator !== null && !shouldResetDisplay) {
                calculate();
            }
            previousValue = currentValue;
            operator = op;
            shouldResetDisplay = true;
        }

        function calculate() {
            if (operator === null || shouldResetDisplay) {
                return;
            }

            let result;
            const prev = parseFloat(previousValue);
            const current = parseFloat(currentValue);

            switch (operator) {
                case '+':
                    result = prev + current;
                    break;
                case '-':
                    result = prev - current;
                    break;
                case '*':
                    result = prev * current;
                    break;
                case '/':
                    result = prev / current;
                    break;
                case '.':
                    return;
                default:
                    return;
            }

            currentValue = result.toString();
            operator = null;
            shouldResetDisplay = true;
            updateDisplay();
        }

        function clearDisplay() {
            currentValue = '0';
            previousValue = '';
            operator = null;
            shouldResetDisplay = false;
            updateDisplay();
        }

        function deleteLast() {
            if (currentValue.length > 1) {
                currentValue = currentValue.slice(0, -1);
            } else {
                currentValue = '0';
            }
            updateDisplay();
        }
    </script>
</body>
</html>

<img width="1870" height="968" alt="Screenshot 2026-02-03 214337" src="https://github.com/user-attachments/assets/58eae3be-a2fd-4475-91ec-a1b03e05eae4" />
<img width="428" height="828" alt="Screenshot 2026-02-03 214357" src="https://github.com/user-attachments/assets/35b8dd20-3129-4b35-9020-909f37765cf3" />

