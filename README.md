<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Business Management Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        #game-container {
            max-width: 900px;
            margin: 50px auto;
            padding: 20px;
            background: white;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .stat {
            font-size: 18px;
            margin: 10px 0;
            display: flex;
            justify-content: space-between;
        }
        .dashboard {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-top: 20px;
        }
        .card {
            padding: 15px;
            background: #007BFF;
            color: white;
            border-radius: 5px;
            text-align: center;
            font-size: 18px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        button {
            padding: 10px;
            margin: 10px 0;
            width: 100%;
            font-size: 16px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <h1>Advanced Business Management</h1>
        <div class="stat">
            <span>Finances:</span>
            <span id="finances">10000</span>
        </div>
        <div class="stat">
            <span>Employees:</span>
            <span id="employees">2</span>
        </div>
        <div class="stat">
            <span>Revenue:</span>
            <span id="revenue">2000</span>
        </div>
        <div class="stat">
            <span>Expenses:</span>
            <span id="expenses">1500</span>
        </div>
        <div class="dashboard">
            <div class="card">R&D: <span id="rnd">500</span></div>
            <div class="card">Marketing: <span id="marketing">1000</span></div>
        </div>
        <button id="invest">Invest in Marketing (Cost: 500)</button>
        <button id="rnd-button">Invest in R&D (Cost: 1000)</button>
        <button id="hire">Hire Employee (Cost: 1000)</button>
        <button id="next-turn">Next Turn</button>
    </div>

    <script>
        // Initial game state
        const state = {
            finances: 10000,
            employees: 2,
            revenue: 2000,
            expenses: 1500,
            rnd: 500,
            marketing: 1000,
        };

        // Update UI with current state
        function updateUI() {
            document.getElementById('finances').textContent = state.finances;
            document.getElementById('employees').textContent = state.employees;
            document.getElementById('revenue').textContent = state.revenue;
            document.getElementById('expenses').textContent = state.expenses;
            document.getElementById('rnd').textContent = state.rnd;
            document.getElementById('marketing').textContent = state.marketing;
        }

        // Event listeners for buttons
        document.getElementById('invest').addEventListener('click', () => {
            if (state.finances >= 500) {
                state.finances -= 500;
                state.marketing += 200;
                state.revenue += 300;
                updateUI();
                alert('Investment in marketing increased revenue and brand value!');
            } else {
                alert('Not enough finances to invest in marketing.');
            }
        });

        document.getElementById('rnd-button').addEventListener('click', () => {
            if (state.finances >= 1000) {
                state.finances -= 1000;
                state.rnd += 500;
                state.revenue += 400;
                updateUI();
                alert('Investment in R&D increased innovation and revenue!');
            } else {
                alert('Not enough finances to invest in R&D.');
            }
        });

        document.getElementById('hire').addEventListener('click', () => {
            if (state.finances >= 1000) {
                state.finances -= 1000;
                state.employees += 1;
                state.expenses += 500;
                updateUI();
                alert('You hired a new employee!');
            } else {
                alert('Not enough finances to hire.');
            }
        });

        document.getElementById('next-turn').addEventListener('click', () => {
            state.finances += state.revenue - state.expenses;
            if (state.finances < 0) {
                alert('You are bankrupt! Game Over.');
                location.reload(); // Restart the game
            } else {
                alert('Turn ended. Finances updated.');
                updateUI();
            }
        });

        // Initial render
        updateUI();
    </script>
</body>
</html>

