[Front Page.html](https://github.com/user-attachments/files/34076558/Front.Page.html)
# SMART-EXPENSE-TRACKER-WEBSITE<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Expense Tracker</title>

    <link rel="stylesheet" href="style.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="script.js" defer></script>
</head>
<body>

<header class="header">
    <div>
        <h1>SpendWise</h1>
        <p>Smart Expense Tracker Dashboard</p>
    </div>

    <button id="themeBtn">🌙 Dark Mode</button>
</header>

<main>
    <!-- Dashboard Cards -->
    <section class="stats">
        <div class="card">
            <h3>Total Income</h3>
            <h2 class="income" id="income">Rs 0</h2>
        </div>

        <div class="card">
            <h3>Total Expenses</h3>
            <h2 class="expense" id="expenses">Rs 0</h2>
        </div>

        <div class="card">
            <h3>Available Balance</h3>
            <h2 id="balance">Rs 0</h2>
        </div>
    </section>

    <!-- Add Transaction and Budget -->
    <section class="content">

        <div class="card">
            <h2 id="formTitle">Add Transaction</h2>

            <form id="expenseForm">
                <label for="description">Description</label>
                <input type="text" id="description"
                       placeholder="e.g. Grocery shopping" required>

                <label for="amount">Amount (Rs)</label>
                <input type="number" id="amount"
                       min="0.01" step="0.01"
                       placeholder="Enter amount" required>

                <label for="type">Transaction Type</label>
                <select id="type">
                    <option value="expense">Expense</option>
                    <option value="income">Income</option>
                </select>

                <label for="category">Category</label>
                <select id="category">
                    <option>Food</option>
                    <option>Travel</option>
                    <option>Shopping</option>
                    <option>Bills</option>
                    <option>Health</option>
                    <option>Education</option>
                    <option>Salary</option>
                    <option>Other</option>
                </select>

                <label for="date">Date</label>
                <input type="date" id="date" required>

                <div class="buttons">
                    <button type="submit" id="saveBtn">
                        Add Transaction
                    </button>

                    <button type="button" id="cancelEdit" hidden>
                        Cancel
                    </button>
                </div>
            </form>
        </div>

        <div class="card">
            <h2>Monthly Budget</h2>

            <label for="budget">Set Monthly Budget (Rs)</label>
            <input type="number" id="budget" min="1"
                   placeholder="Enter budget">

            <button type="button" id="saveBudget">
                Save Budget
            </button>

            <div class="budget-info">
                <p>Spent: <strong id="spent">Rs 0</strong></p>
                <p>Budget: <strong id="budgetLimit">Rs 0</strong></p>
                <p id="budgetAlert">Set your monthly budget.</p>
            </div>

            <div class="progress">
                <div id="progressBar"></div>
            </div>

            <h2 class="chart-heading">Expenses by Category</h2>
            <div class="chart-container">
                <canvas id="expenseChart"></canvas>
            </div>
        </div>

    </section>

    <!-- Transactions -->
    <section class="card transaction-card">
        <h2>Transactions</h2>

        <div class="filters">
            <input type="search" id="search"
                   placeholder="Search transactions...">

            <select id="filter">
                <option value="">All Categories</option>
                <option>Food</option>
                <option>Travel</option>
                <option>Shopping</option>
                <option>Bills</option>
                <option>Health</option>
                <option>Education</option>
                <option>Salary</option>
                <option>Other</option>
            </select>

            <select id="typeFilter">
                <option value="">All Types</option>
                <option value="income">Income</option>
                <option value="expense">Expense</option>
            </select>

            <input type="date" id="dateFilter">

            <button type="button" id="resetFilters">
                Reset Filters
            </button>
        </div>

        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th>Description</th>
                        <th>Category</th>
                        <th>Date</th>
                        <th>Type</th>
                        <th>Amount</th>
                        <th>Actions</th>
                    </tr>
                </thead>

                <tbody id="transactionList"></tbody>
            </table>

            <p id="emptyMessage" hidden>No transactions found.</p>
        </div>
    </section>
</main>

<footer>
    <p>© 2026 SpendWise | Smart Expense Tracker</p>
</footer>

</body>
</html>
<style>```css
:root {
    --bg: #f3f5fb;
    --card: #ffffff;
    --text: #20263b;
    --muted: #747b8e;
    --primary: #6558e8;
    --border: #e3e7ef;
    --green: #159a72;
    --red: #e05260;
}

body.dark {
    --bg: #111827;
    --card: #1c2637;
    --text: #edf2fb;
    --muted: #a2aec2;
    --primary: #9186ff;
    --border: #344055;
    --green: #48d6a6;
    --red: #ff7d88;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
}

body {
    background: var(--bg);
    color: var(--text);
    padding: 25px;
    transition: 0.3s;
}

.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 15px;
    flex-wrap: wrap;
    margin-bottom: 25px;
}

h1 {
    color: var(--primary);
    margin-bottom: 8px;
}

p {
    line-height: 1.6;
}

button {
    padding: 10px 14px;
    background: var(--primary);
    color: white;
    border: none;
    border-radius: 7px;
    cursor: pointer;
    transition: 0.2s;
}

button:hover {
    opacity: 0.85;
}

button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

input, select {
    width: 100%;
    padding: 11px;
    margin: 7px 0 14px;
    border: 1px solid var(--border);
    border-radius: 7px;
    background: var(--bg);
    color: var(--text);
}

label {
    display: block;
    font-size: 13px;
    font-weight: bold;
    color: var(--muted);
}

.stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    margin-bottom: 25px;
}

.card {
    background: var(--card);
    padding: 22px;
    border-radius: 13px;
    box-shadow: 0 4px 15px #0000000a;
    border: 1px solid var(--border);
    min-width: 0;
}

.card h2 {
    margin-bottom: 18px;
}

.card h3 {
    color: var(--muted);
    margin-bottom: 13px;
}

.card h2.income,
.income {
    color: var(--green);
}

.card h2.expense,
.expense {
    color: var(--red);
}

.stats .card h2 {
    font-size: 25px;
    overflow-wrap: anywhere;
}

.content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin-bottom: 25px;
}

.buttons {
    display: flex;
    gap: 10px;
}

.budget-info {
    margin-top: 20px;
}

.budget-info p {
    margin-bottom: 8px;
}

#budgetAlert {
    color: var(--green);
    margin: 12px 0;
    font-size: 14px;
}

#budgetAlert.warning {
    color: var(--red);
}

.progress {
    height: 10px;
    background: var(--border);
    border-radius: 20px;
    overflow: hidden;
    margin-bottom: 25px;
}

#progressBar {
    height: 100%;
    width: 0;
    background: var(--primary);
    transition: width 0.3s;
}

.chart-heading {
    margin-top: 25px;
}

.chart-container {
    position: relative;
    max-width: 100%;
    height: 250px;
}

.transaction-card {
    margin-bottom: 25px;
}

.filters {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr auto;
    gap: 10px;
    align-items: center;
    margin-bottom: 15px;
}

.filters input,
.filters select {
    margin: 0;
    min-width: 0;
}

.table-container {
    width: 100%;
    overflow-x: auto;
}

table {
    width: 100%;
    border-collapse: collapse;
    white-space: nowrap;
}

th, td {
    text-align: left;
    padding: 13px 10px;
    border-bottom: 1px solid var(--border);
}

th {
    color: var(--muted);
    font-size: 12px;
    text-transform: uppercase;
}

td {
    font-size: 13px;
}

.action-buttons {
    display: flex;
    gap: 6px;
}

.edit-btn {
    background: #e5a23c;
}

.delete-btn {
    background: var(--red);
}

#emptyMessage {
    color: var(--muted);
    text-align: center;
    padding: 20px;
}

footer {
    color: var(--muted);
    text-align: center;
    font-size: 13px;
    padding: 15px;
}

[hidden] {
    display: none !important;
}

@media (max-width: 1050px) {
    .content {
        grid-template-columns: 1fr;
    }

    .filters {
        grid-template-columns: repeat(2, minmax(0, 1fr));
    }
}

@media (max-width: 700px) {
    body {
        padding: 15px;
    }

    .stats {
        grid-template-columns: 1fr;
        gap: 13px;
    }

    .stats .card h2 {
        font-size: 23px;
    }

    .header {
        align-items: flex-start;
    }

    .card {
        padding: 16px;
    }

    .filters {
        grid-template-columns: 1fr;
    }

    .chart-container {
        height: 220px;
    }

    th, td {
        padding: 11px 8px;
    }
}
```</style>
<script>
const $ = id => document.getElementById(id);

const today = new Date();
const todayString = [
    today.getFullYear(),
    String(today.getMonth() + 1).padStart(2, "0"),
    String(today.getDate()).padStart(2, "0")
].join("-");

let transactions = JSON.parse(
    localStorage.getItem("swTransactions") || "[]"
);

let monthlyBudget = Number(
    localStorage.getItem("swBudget") || 0
);

let editingId = null;
let chart = null;

const money = amount =>
    "Rs " + Number(amount).toLocaleString("en-PK", {
        maximumFractionDigits: 2
    });

function saveData() {
    localStorage.setItem(
        "swTransactions",
        JSON.stringify(transactions)
    );

    localStorage.setItem("swBudget", monthlyBudget);
}

function currentMonthTransactions() {
    const month = todayString.slice(0, 7);

    return transactions.filter(t => t.date.startsWith(month));
}

// Add and edit transactions
$("expenseForm").addEventListener("submit", function (event) {
    event.preventDefault();

    const description = $("description").value.trim();
    const amount = Number($("amount").value);
    const date = $("date").value;

    if (!description || !Number.isFinite(amount) ||
        amount <= 0 || !date) {
        alert("Please enter valid transaction details.");
        return;
    }

    const transaction = {
        id: editingId || Date.now(),
        description,
        amount,
        type: $("type").value,
        category: $("category").value,
        date
    };

    if (editingId !== null) {
        transactions = transactions.map(t =>
            t.id === editingId ? transaction : t
        );
    } else {
        transactions.push(transaction);
    }

    editingId = null;
    $("formTitle").textContent = "Add Transaction";
    $("saveBtn").textContent = "Add Transaction";
    $("cancelEdit").hidden = true;

    this.reset();
    $("date").value = todayString;

    saveData();
    renderAll();
});

// Display transaction rows
function renderTransactions() {
    const search = $("search").value.toLowerCase().trim();
    const category = $("filter").value;
    const type = $("typeFilter").value;
    const date = $("dateFilter").value;

    const filtered = transactions.filter(t =>
        t.description.toLowerCase().includes(search) &&
        (!category || t.category === category) &&
        (!type || t.type === type) &&
        (!date || t.date === date)
    );

    filtered.sort((a, b) => b.date.localeCompare(a.date));

    const list = $("transactionList");
    list.innerHTML = "";

    $("emptyMessage").hidden = filtered.length > 0;

    filtered.forEach(t => {
        const row = document.createElement("tr");

        const values = [
            t.description,
            t.category,
            t.date,
            t.type === "income" ? "Income" : "Expense",
            (t.type === "income" ? "+ " : "- ") + money(t.amount)
        ];

        values.forEach((value, index) => {
            const cell = document.createElement("td");
            cell.textContent = value;

            if (index === 3) {
                cell.className = t.type === "income"
                    ? "income" : "expense";
            }

            row.appendChild(cell);
        });

        const actions = document.createElement("td");
        actions.className = "action-buttons";

        const edit = document.createElement("button");
        edit.textContent = "Edit";
        edit.className = "edit-btn";
        edit.addEventListener("click", () => editTransaction(t.id));

        const remove = document.createElement("button");
        remove.textContent = "Delete";
        remove.className = "delete-btn";
        remove.addEventListener("click", () => deleteTransaction(t.id));

        actions.append(edit, remove);
        row.appendChild(actions);
        list.appendChild(row);
    });
}

// Edit transaction
function editTransaction(id) {
    const t = transactions.find(item => item.id === id);
    if (!t) return;

    editingId = id;

    $("description").value = t.description;
    $("amount").value = t.amount;
    $("type").value = t.type;
    $("category").value = t.category;
    $("date").value = t.date;

    $("formTitle").textContent = "Edit Transaction";
    $("saveBtn").textContent = "Update Transaction";
    $("cancelEdit").hidden = false;

    $("expenseForm").scrollIntoView({ behavior: "smooth" });
    $("description").focus();
}

// Cancel edit
$("cancelEdit").addEventListener("click", () => {
    editingId = null;
    $("expenseForm").reset();
    $("date").value = todayString;
    $("formTitle").textContent = "Add Transaction";
    $("saveBtn").textContent = "Add Transaction";
    $("cancelEdit").hidden = true;
});

// Delete transaction
function deleteTransaction(id) {
    const t = transactions.find(item => item.id === id);
    if (!t) return;

    if (!confirm(`Delete "${t.description}"?`)) return;

    transactions = transactions.filter(item => item.id !== id);

    saveData();
    renderAll();
}

// Update dashboard statistics
function updateDashboard() {
    const current = currentMonthTransactions();

    const income = current
        .filter(t => t.type === "income")
        .reduce((sum, t) => sum + Number(t.amount), 0);

    const expenses = current
        .filter(t => t.type === "expense")
        .reduce((sum, t) => sum + Number(t.amount), 0);

    $("income").textContent = money(income);
    $("expenses").textContent = money(expenses);
    $("balance").textContent = money(income - expenses);

    $("spent").textContent = money(expenses);
    $("budgetLimit").textContent = money(monthlyBudget);

    const alertBox = $("budgetAlert");
    const progress = $("progressBar");
    const percent = monthlyBudget > 0
        ? expenses / monthlyBudget * 100 : 0;

    progress.style.width = Math.min(percent, 100) + "%";

    if (percent >= 100 && monthlyBudget > 0) {
        alertBox.textContent =
            "⚠ Budget exceeded by " +
            money(expenses - monthlyBudget);

        alertBox.className = "warning";
        progress.style.background = "var(--red)";
    } else if (percent >= 80 && monthlyBudget > 0) {
        alertBox.textContent =
            "⚠ Warning: " + Math.round(percent) +
            "% of your budget has been used.";

        alertBox.className = "warning";
        progress.style.background = "#e5a23c";
    } else {
        alertBox.textContent = monthlyBudget > 0
            ? money(monthlyBudget - expenses) + " budget remaining."
            : "Set your monthly budget.";

        alertBox.className = "";
        progress.style.background = "var(--primary)";
    }

    updateChart(current);
}

// Expense chart using Chart.js
function updateChart(current) {
    const totals = {};

    current.filter(t => t.type === "expense").forEach(t => {
        totals[t.category] =
            (totals[t.category] || 0) + Number(t.amount);
    });

    if (chart) chart.destroy();

    const labels = Object.keys(totals);
    const values = Object.values(totals);

    chart = new Chart($("expenseChart"), {
        type: "doughnut",
        data: {
            labels: labels.length ? labels : ["No expenses"],
            datasets: [{
                data: values.length ? values : [1],
                backgroundColor: [
                    "#6558e8", "#159a72", "#e5a23c",
                    "#e05260", "#4d9de0", "#b56ad8",
                    "#4ab6c4", "#a0aec0"
                ],
                borderWidth: 0
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: {
                    position: "bottom"
                },
                tooltip: {
                    callbacks: {
                        label: context => labels.length
                            ? context.label + ": " + money(context.raw)
                            : "No expenses recorded"
                    }
                }
            }
        }
    });
}

// Save monthly budget
$("saveBudget").addEventListener("click", () => {
    const value = Number($("budget").value);

    if (!Number.isFinite(value) || value <= 0) {
        alert("Please enter a budget greater than zero.");
        return;
    }

    monthlyBudget = value;

    saveData();
    updateDashboard();
});

// Search and filters
["search", "filter", "typeFilter", "dateFilter"].forEach(id => {
    $(id).addEventListener(
        id === "search" ? "input" : "change",
        renderTransactions
    );
});

$("resetFilters").addEventListener("click", () => {
    $("search").value = "";
    $("filter").value = "";
    $("typeFilter").value = "";
    $("dateFilter").value = "";

    renderTransactions();
});

// Dark and light mode
function applyTheme(dark) {
    document.body.classList.toggle("dark", dark);
    $("themeBtn").textContent = dark
        ? "☀ Light Mode" : "🌙 Dark Mode";

    localStorage.setItem("swTheme", dark ? "dark" : "light");

    if (chart) updateChart(currentMonthTransactions());
}

$("themeBtn").addEventListener("click", () => {
    applyTheme(!document.body.classList.contains("dark"));
});

// Render everything
function renderAll() {
    saveData();
    updateDashboard();
    renderTransactions();
}

// Restore saved preferences and initialize the page
if (localStorage.getItem("swTheme") === "dark") {
    document.body.classList.add("dark");
    $("themeBtn").textContent = "☀ Light Mode";
}

$("date").value = todayString;
$("budget").value = monthlyBudget || "";

renderAll()
</script>
