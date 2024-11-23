<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Energy Demand Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            line-height: 1.6;
            background-color: #f4f4f4;
        }
        h1, h2 {
            color: #0044cc;
        }
        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 50%;
            margin: 0 auto;
        }
        label {
            display: block;
            margin-top: 10px;
        }
        input, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            font-size: 16px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        button {
            background-color: #0044cc;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background-color: #0033a0;
        }
        .result {
            margin-top: 20px;
            padding: 10px;
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Energy Demand Calculator</h1>

        <!-- Section for calculating Energy Demand in France -->
        <h2>1. Energy Demand in France (2000)</h2>
        <label for="demand_2015">Energy Demand in 2015 (Mtoe):</label>
        <input type="number" id="demand_2015" placeholder="Enter demand in 2015 (Mtoe)" required>

        <label for="growth_rate">Annual Growth Rate (%):</label>
        <input type="number" id="growth_rate" placeholder="Enter growth rate in %" required>

        <label for="years">Number of Years (e.g., 15 for 2000 to 2015):</label>
        <input type="number" id="years" placeholder="Enter number of years" required>

        <button onclick="calculateDemand()">Calculate Energy Demand in 2000</button>

        <div class="result" id="result_2000"></div>

        <!-- Section for calculating Growth Rate -->
        <h2>2. Growth Rate from 2015 to 2016</h2>
        <label for="demand_2016">Energy Demand in 2016 (Mtoe):</label>
        <input type="number" id="demand_2016" placeholder="Enter demand in 2016 (Mtoe)" required>

        <button onclick="calculateGrowthRate()">Calculate Growth Rate</button>

        <div class="result" id="result_growth_rate"></div>

        <!-- Section for calculating Energy Demand in Germany -->
        <h2>3. Energy Demand in Germany (2015)</h2>
        <label for="gdp_2015">GDP in 2015 (Billion €):</label>
        <input type="number" id="gdp_2015" placeholder="Enter GDP in 2015" required>

        <label for="gdp_2016">GDP in 2016 (Billion €):</label>
        <input type="number" id="gdp_2016" placeholder="Enter GDP in 2016" required>

        <label for="elasticity">GDP Elasticity of Energy Demand:</label>
        <input type="number" id="elasticity" placeholder="Enter elasticity (e.g., 2.4)" required>

        <label for="demand_2016_germany">Primary Energy Consumption in 2016 (Mtoe):</label>
        <input type="number" id="demand_2016_germany" placeholder="Enter energy consumption in 2016 (Mtoe)" required>

        <button onclick="calculateGermanyDemand()">Calculate Energy Demand in 2015 (Germany)</button>

        <div class="result" id="result_germany"></div>
    </div>

    <script>
        // Calculate Energy Demand in 2000 for France
        function calculateDemand() {
            let demand_2015 = parseFloat(document.getElementById("demand_2015").value);
            let growth_rate = parseFloat(document.getElementById("growth_rate").value) / 100;
            let years = parseFloat(document.getElementById("years").value);

            let demand_2000 = demand_2015 / Math.pow(1 + growth_rate, years);
            document.getElementById("result_2000").innerHTML = "Energy Demand in 2000: " + demand_2000.toFixed(2) + " Mtoe";
        }

        // Calculate Growth Rate from 2015 to 2016
        function calculateGrowthRate() {
            let demand_2015 = parseFloat(document.getElementById("demand_2015").value);
            let demand_2016 = parseFloat(document.getElementById("demand_2016").value);

            let growth_rate = ((demand_2016 - demand_2015) / demand_2015) * 100;
            document.getElementById("result_growth_rate").innerHTML = "Growth Rate from 2015 to 2016: " + growth_rate.toFixed(2) + "%";
        }

        // Calculate Energy Demand in Germany for 2015
        function calculateGermanyDemand() {
            let gdp_2015 = parseFloat(document.getElementById("gdp_2015").value);
            let gdp_2016 = parseFloat(document.getElementById("gdp_2016").value);
            let elasticity = parseFloat(document.getElementById("elasticity").value);
            let demand_2016_germany = parseFloat(document.getElementById("demand_2016_germany").value);

            let gdp_growth_rate = (gdp_2016 - gdp_2015) / gdp_2015;
            let demand_2015_germany = demand_2016_germany / (1 + elasticity * gdp_growth_rate);

            document.getElementById("result_germany").innerHTML = "Primary Energy Consumption in 2015 (Germany): " + demand_2015_germany.toFixed(2) + " Mtoe";
        }
    </script>
</body>
</html>
