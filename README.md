< MSG TELECOM >
<html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MSG Telecom</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f4f6f8;
        }
        header {
            background-color: #0a3d62;
            color: white;
            padding: 20px;
            text-align: center;
        }
        nav {
            background-color: #1e3799;
            padding: 10px;
            text-align: center;
        }
        nav a {
            color: white;
            margin: 0 15px;
            text-decoration: none;
            font-weight: bold;
        }
        section {
            padding: 30px;
            text-align: center;
        }
        .services {
            background-color: #ffffff;
            margin: 20px;
            padding: 20px;
            border-radius: 8px;
        }
        footer {
            background-color: #0a3d62;
            color: white;
            text-align: center;
            padding: 15px;
        }
        .btn {
            background-color: #1e3799;
            color: white;
            padding: 10px 20px;
            text-decoration: none;
            border-radius: 5px;
            display: inline-block;
            margin-top: 10px;
        }
    </style>
</head>
<body>
<!DOCTYPE html><html lang="en">
<head>
<body class="bg-gray-100"><div class="flex">
  <!-- Sidebar -->
  <div class="w-64 bg-blue-700 text-white min-h-screen p-5">
    <h2 class="text-2xl font-bold mb-6">Recharge App</h2>
    <ul>
      <li class="mb-3 cursor-pointer">Dashboard</li>
      <li class="mb-3 cursor-pointer">Mobile Recharge</li>
      <li class="mb-3 cursor-pointer">DTH Recharge</li>
      <li class="mb-3 cursor-pointer">History</li>
    </ul>
  </div>  <!-- Main Content -->  <div class="flex-1 p-6">
    <h1 class="text-3xl font-bold mb-6">Dashboard</h1><!-- Stats -->
<div class="grid grid-cols-3 gap-4 mb-6">
  <div class="bg-white p-4 rounded shadow">Total Users: 120</div>
  <div class="bg-white p-4 rounded shadow">Recharges Today: 45</div>
  <div class="bg-white p-4 rounded shadow">Revenue: ₹5000</div>
</div>

<!-- Recharge Form -->
<div class="bg-white p-6 rounded shadow w-full max-w-md">
  <h2 class="text-xl font-semibold mb-4">Mobile Recharge</h2>

  <input id="number" type="text" placeholder="Mobile Number" class="w-full mb-3 p-2 border rounded" />
  <input id="amount" type="number" placeholder="Amount" class="w-full mb-3 p-2 border rounded" />

  <button onclick="recharge()" class="bg-blue-600 text-white px-4 py-2 rounded w-full">Recharge</button>

  <p id="msg" class="mt-3 text-green-600"></p>
</div>

  </div>
</div><script>
function recharge() {
  const number = document.getElementById('number').value;
  const amount = document.getElementById('amount').value;

  if(number === '' || amount === '') {
    document.getElementById('msg').innerText = 'Please fill all fields';
    return;
  }

  document.getElementById('msg').innerText = `Recharge of ₹${amount} successful for ${number}`;
}
</script></body>
</html>


