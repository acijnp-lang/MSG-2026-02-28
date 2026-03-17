< MSG TELECOM >
<html lang="en">
<head>
<form method="POST">
    <h2>Admin Login</h2>
    <input type="text" name="username" placeholder="Username"><br><br>
    <input type="password" name="password" placeholder="Password"><br><br>
    <button name="login">Login</button>
</form>
<?php
$conn = mysqli_connect("localhost", "root", "", "recharge_db");
?>

<h2>Admin Dashboard</h2>

<h3>Add User</h3>
<form method="POST">
    <input type="text" name="name" placeholder="User Name">
    <button name="addUser">Add</button>
</form>

<?php
if(isset($_POST['addUser'])){
    $name = $_POST['name'];
    mysqli_query($conn, "INSERT INTO users(name) VALUES('$name')");
}
?>

<h3>Users List</h3>
<?php
$res = mysqli_query($conn, "SELECT * FROM users");
while($row = mysqli_fetch_assoc($res)){
    echo $row['name']."<br>";
}
?>

<hr>

<h3>Add Recharge</h3>
<form method="POST">
    <input type="text" name="number" placeholder="Number">
    <input type="number" name="amount" placeholder="Amount">
    <button name="addRecharge">Add</button>
</form>

<?php
if(isset($_POST['addRecharge'])){
    $num = $_POST['number'];
    $amt = $_POST['amount'];
    mysqli_query($conn, "INSERT INTO recharge(number, amount) VALUES('$num', '$amt')");
}
?>

<h3>Recharge History</h3>
<?php
$res = mysqli_query($conn, "SELECT * FROM recharge");
while($row = mysqli_fetch_assoc($res)){
    echo $row['number']." - ₹".$row['amount']."<br>";
}
?>
http://localhost/login.php

