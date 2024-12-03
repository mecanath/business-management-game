<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Garage Management Simulator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        #game-container {
            max-width: 1200px;
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
        #garage {
            margin: 20px auto;
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
        }
        .vehicle {
            width: 100px;
            height: 50px;
            background: url('https://via.placeholder.com/100x50?text=Car') no-repeat center center;
            background-size: cover;
            border: 2px solid #007BFF;
            border-radius: 4px;
        }
        .tool {
            width: 50px;
            height: 50px;
            background: url('https://via.placeholder.com/50?text=Tool') no-repeat center center;
            background-size: cover;
            border: 2px solid #FF5733;
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <h1>Garage Management Simulator</h1>
        <div class="stat">
            <span>Finances:</span>
            <span id="finances">20000</span>
        </div>
        <div class="stat">
            <span>Employees:</span>
            <span id="employees">3</span>
        </div>
        <div class="stat">
            <span>Revenue:</span>
            <span id="revenue">5000</span>
        </div>
        <div class="stat">
            <span>Expenses:</span>
            <span id="expenses">2500</span>
        </div>
        <div class="stat">
            <span>Tools Owned:</span>
            <span id="tools">0</span>
        </div>
        <div class="stat">
            <span>Vehicles Serviced:</span>
            <span id="vehicles">0</span>
        </div>
        <div class="dashboard">
            <div class="card">Marketing: <span id="marketing">1000</span></div>
            <div class="card">R&D: <span id="rnd">500</span></div>
        </div>
        <button id="invest-marketing">Invest in Marketing (Cost: 500)</button>
        <button id="invest-rnd">Invest in R&D (Cost: 1000)</button>
        <button id="buy-tool">Buy Tool (Cost: 2000)</button>
        <button id="hire-staff">Hire Staff (Cost: Variable)</button>
        <button id="next-turn">Next Turn</button>
        
        <div id="garage">
            <div class="vehicle" title="Vehicle 1"></div>
            <div class="vehicle" title="Vehicle 2"></div>
        </div>
    </div>

    <script>
        const state = {
            finances: 20000,
            employees: 3,
            revenue: 5000,
            expenses: 2500,
            tools: 0,
            vehicles: 0,
            marketing: 1000,
            rnd: 500,
        };

        function updateUI() {
            document.getElementById('finances').textContent = state.finances;
            document.getElementById('employees').textContent = state.employees;
            document.getElementById('revenue').textContent = state.revenue;
            document.getElementById('expenses').textContent = state.expenses;
            document.getElementById('tools').textContent = state.tools;
            document.getElementById('vehicles').textContent = state.vehicles;
            document.getElementById('marketing').textContent = state.marketing;
            document.getElementById('rnd').textContent = state.rnd;

            const garage = document.getElementById('garage');
            garage.innerHTML = '';
            for (let i = 0; i < state.vehicles; i++) {
                const vehicle = document.createElement('div');
                vehicle.className = 'vehicle';
                garage.appendChild(vehicle);
            }
            for (let i = 0; i < state.tools; i++) {
                const tool = document.createElement('div');
                tool.className = 'tool';
                garage.appendChild(tool);
            }
        }

        document.getElementById('invest-marketing').addEventListener('click', () => {
            if (state.finances >= 500) {
                state.finances -= 500;
                state.marketing += 200;
                state.revenue += 300;
                alert('Investment in marketing increased customer awareness!');
            } else {
                alert('Not enough finances to invest in marketing.');
            }
            updateUI();
        });

        document.getElementById('invest-rnd').addEventListener('click', () => {
            if (state.finances >= 1000) {
                state.finances -= 1000;
                state.rnd += 500;
                state.revenue += 400;
                alert('R&D investment improved operational efficiency!');
            } else {
                alert('Not enough finances to invest in R&D.');
            }
            updateUI();
        });

        document.getElementById('buy-tool').addEventListener('click', () => {
            if (state.finances >= 2000) {
                state.finances -= 2000;
                state.tools += 1;
                state.revenue += 500;
                alert('New tool purchased, enhancing garage capability!');
            } else {
                alert('Not enough finances to buy tools.');
            }
            updateUI();
        });

        document.getElementById('hire-staff').addEventListener('click', () => {
            let salary = 1000 + Math.floor(Math.random() * 1000);
            if (state.finances >= salary) {
                state.finances -= salary;
                state.employees += 1;
                state.expenses += salary / 10;
                alert(`Hired new staff with salary: $${salary}`);
            } else {
                alert('Not enough finances to hire staff.');
            }
            updateUI();
        });

        document.getElementById('next-turn').addEventListener('click', () => {
            state.finances += state.revenue - state.expenses;
            state.vehicles += Math.floor(state.tools * 1.5);
            if (state.finances < 0) {
                alert('You are bankrupt! Game Over.');
                location.reload();
            } else {
                alert('Turn ended. Finances updated.');
            }
            update
