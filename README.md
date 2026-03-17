< MSG TELECOM >
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Admin Panel</title>

<style>
body {
    font-family: Arial;
    margin: 0;
    background: #f4f4f4;
}

.sidebar {
    width: 200px;
    height: 100vh;
    background: #222;
    color: white;
    position: fixed;
    padding-top: 20px;
}

.sidebar h2 {
    text-align: center;
}

.sidebar a {
    display: block;
    color: white;
    padding: 10px;
    text-decoration: none;
}

.sidebar a:hover {
    background: #575757;
}

.main {
    margin-left: 210px;
    padding: 20px;
}

.card {
    background: white;
    padding: 15px;
    margin-bottom: 15px;
    border-radius: 10px;
    box-shadow: 0 0 5px gray;
}

button {
    padding: 8px 12px;
    background: green;
    color: white;
    border: none;
    cursor: pointer;
}

table {
    width: 100%;
    border-collapse: collapse;
}

table, th, td {
    border: 1px solid #ccc;
}

th, td {
    padding: 10px;
    text-align: center;
}
</style>
</head>

<body>

<div class="sidebar">
    <h2>Admin</h2>
    <a href="#" onclick="show('dashboard')">Dashboard</a>
    <a href="#" onclick="show('users')">Users</a>
    <a href="#" onclick="show('recharge')">Recharge History</a>
</div>

<div class="main">

    <!-- Dashboard -->
    <div id="dashboard" class="card">
        <h3>Dashboard</h3>
        <p>Total Balance: ₹ <span id="balance">10000</span></p>
        <button onclick="addMoney()">Add ₹500</button>
    </div>

    <!-- Users -->
    <div id="users" class="card" style="display:none;">
        <h3>Users</h3>
        <input type="text" id="username" placeholder="Enter user name">
        <button onclick="addUser()">Add User</button>

        <ul id="userList"></ul>
    </div>

    <!-- Recharge History -->
    <div id="recharge" class="card" style="display:none;">
        <h3>Recharge History</h3>

        <input type="text" id="num" placeholder="Number">
        <input type="number" id="amt" placeholder="Amount">
        <button onclick="addRecharge()">Add Recharge</button>

        <table>
            <tr>
                <th>Number</th>
                <th>Amount</th>
            </tr>
            <tbody id="history"></tbody>
        </table>
    </div>

</div>

<script>
function show(section) {
    document.getElementById("dashboard").style.display = "none";
    document.getElementById("users").style.display = "none";
    document.getElementById("recharge").style.display = "none";

    document.getElementById(section).style.display = "block";
}

// Balance
function addMoney() {
    let bal = document.getElementById("balance");
    bal.innerText = parseInt(bal.innerText) + 500;
}

// Users
function addUser() {
    let name = document.getElementById("username").value;
    if(name === "") return;

    let li = document.createElement("li");
    li.innerText = name;
    document.getElementById("userList").appendChild(li);
}

// Recharge History
function addRecharge() {
    let num = document.getElementById("num").value;
    let amt = document.getElementById("amt").value;

    if(num === "" || amt === "") return;

    let row = `<tr>
        <td>${num}</td>
        <td>₹${amt}</td>
    </tr>`;

    document.getElementById("history").innerHTML += row;
}
</script>

</body>
</html>

