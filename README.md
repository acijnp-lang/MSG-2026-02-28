< MSG TELECOM >
recharge-pro/
│
├── config.php
├── login.php
├── register.php
├── dashboard.php
├── recharge.php
├── wallet.php
├── history.php
├── admin/
│   ├── admin.php
│   ├── users.php
│   ├── recharges.php
│   └── add_balance.php
└── database.sql
CREATE DATABASE recharge_pro;
USE recharge_pro;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    password VARCHAR(255),
    wallet FLOAT DEFAULT 0,
    role VARCHAR(20) DEFAULT 'user'
);

CREATE TABLE recharge (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    number VARCHAR(20),
    amount FLOAT,
    commission FLOAT,
    status VARCHAR(20),
    txn_id VARCHAR(50)
);

CREATE TABLE transactions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    amount FLOAT,
    type VARCHAR(20),
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
<?php
include "config.php";

if(isset($_POST['register'])){
    $u = $_POST['username'];
    $p = password_hash($_POST['password'], PASSWORD_DEFAULT);

    mysqli_query($conn, "INSERT INTO users(username,password) VALUES('$u','$p')");
    echo "Registered!";
}
?>

<form method="POST">
<input name="username" placeholder="Username">
<input type="password" name="password" placeholder="Password">
<button name="register">Register</button>
</form>
<?php
include "config.php";

if(isset($_POST['login'])){
    $u = $_POST['username'];
    $p = $_POST['password'];

    $res = mysqli_query($conn, "SELECT * FROM users WHERE username='$u'");
    $row = mysqli_fetch_assoc($res);

    if($row && password_verify($p, $row['password'])){
        $_SESSION['user_id'] = $row['id'];
        $_SESSION['role'] = $row['role'];

        if($row['role'] == 'admin'){
            header("Location: admin/admin.php");
        } else {
            header("Location: dashboard.php");
        }
    } else {
        echo "Login Failed";
    }
}
?>
<?php include "config.php"; ?>

<h2>User Dashboard</h2>

<a href="wallet.php">Wallet</a> |
<a href="history.php">History</a>

<form method="POST" action="recharge.php">
<input name="number" placeholder="Mobile Number">
<input name="amount" placeholder="Amount">
<button name="recharge">Recharge</button>
</form>
<?php
include "config.php";

if(isset($_POST['recharge'])){
    $user = $_SESSION['user_id'];
    $num = $_POST['number'];
    $amt = $_POST['amount'];

    $res = mysqli_query($conn, "SELECT wallet FROM users WHERE id='$user'");
    $row = mysqli_fetch_assoc($res);

    if($row['wallet'] >= $amt){

        // Deduct wallet
        mysqli_query($conn, "UPDATE users SET wallet = wallet - $amt WHERE id='$user'");

        // Commission (2%)
        $commission = $amt * 0.02;

        // Generate TXN ID
        $txn = "TXN".rand(10000,99999);

        // 🔌 API CALL (replace with real)
        $api_response = "SUCCESS";

        $status = ($api_response == "SUCCESS") ? "SUCCESS" : "FAILED";

        mysqli_query($conn, "INSERT INTO recharge(user_id,number,amount,commission,status,txn_id)
        VALUES('$user','$num','$amt','$commission','$status','$txn')");

        echo "Recharge $status | TXN: $txn";

    } else {
        echo "Insufficient Balance";
    }
}
?>
<?php
include "config.php";

$user = $_SESSION['user_id'];

$res = mysqli_query($conn, "SELECT wallet FROM users WHERE id='$user'");
$row = mysqli_fetch_assoc($res);

echo "<h2>Balance: ₹".$row['wallet']."</h2>";
?>
<?php
include "config.php";

$user = $_SESSION['user_id'];

$res = mysqli_query($conn, "SELECT * FROM recharge WHERE user_id='$user'");

while($r = mysqli_fetch_assoc($res)){
    echo $r['number']." | ₹".$r['amount']." | ".$r['status']." | ".$r['txn_id']."<br>";
}
?>
<?php include "../config.php"; ?>

<h2>Admin Panel</h2>

<a href="users.php">Users</a> |
<a href="recharges.php">Recharges</a>
$api_response = "SUCCESS";
$api_url = "https://api.com/recharge?number=$num&amount=$amt&key=APIKEY";
$response = file_get_contents($api_url);
$data = json_decode($response, true);

$status = $data['status'];
