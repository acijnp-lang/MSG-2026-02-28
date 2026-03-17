< MSG TELECOM >
<html lang="en">
<head>
<form method="POST">
    <h2>Admin Login</h2>
   CREATE DATABASE recharge_db;
USE recharge_db;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    password VARCHAR(50),
    wallet INT DEFAULT 0
);

CREATE TABLE recharge (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    number VARCHAR(20),
    amount INT,
    status VARCHAR(20)
);

INSERT INTO users (username, password, wallet) VALUES ('user1','1234',1000);
<?php
$conn = mysqli_connect("localhost", "root", "", "recharge_db");
session_start();
?>
<?php
include "config.php";

if(isset($_POST['login'])){
    $u = $_POST['username'];
    $p = $_POST['password'];

    $res = mysqli_query($conn, "SELECT * FROM users WHERE username='$u' AND password='$p'");

    if(mysqli_num_rows($res)){
        $row = mysqli_fetch_assoc($res);
        $_SESSION['user_id'] = $row['id'];
        header("Location: index.php");
    } else {
        echo "Login Failed";
    }
}
?>

<form method="POST">
<h2>User Login</h2>
<input name="username" placeholder="Username"><br>
<input type="password" name="password" placeholder="Password"><br>
<button name="login">Login</button>
</form>
<?php include "config.php"; ?>

<h2>Recharge Panel</h2>

<form method="POST" action="recharge.php">
    <select name="service">
        <option>Mobile</option>
        <option>DTH</option>
        <option>Electricity</option>
    </select><br>

    <input name="number" placeholder="Number"><br>
    <input name="amount" placeholder="Amount"><br>

    <button name="recharge">Recharge</button>
</form>

<a href="wallet.php">Check Wallet</a>
<?php
include "config.php";

if(isset($_POST['recharge'])){
    $user = $_SESSION['user_id'];
    $num = $_POST['number'];
    $amt = $_POST['amount'];

    // Wallet check
    $res = mysqli_query($conn, "SELECT wallet FROM users WHERE id='$user'");
    $row = mysqli_fetch_assoc($res);

    if($row['wallet'] >= $amt){

        // Wallet deduct
        mysqli_query($conn, "UPDATE users SET wallet = wallet - $amt WHERE id='$user'");

        // 🔌 यहाँ REAL API लगाना है
        // Example:
        // $api = file_get_contents("https://api.com/recharge?num=$num&amt=$amt");

        $status = "SUCCESS";

        mysqli_query($conn, "INSERT INTO recharge(user_id, number, amount, status)
        VALUES('$user','$num','$amt','$status')");

        echo "Recharge Successful";

    } else {
        echo "Low Balance";
    }
}
?>
<?php
include "config.php";

$user = $_SESSION['user_id'];
$res = mysqli_query($conn, "SELECT wallet FROM users WHERE id='$user'");
$row = mysqli_fetch_assoc($res);

echo "<h2>Your Balance: ₹".$row['wallet']."</h2>";
?>
