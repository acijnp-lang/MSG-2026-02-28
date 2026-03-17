< MSG TELECOM >
<html lang="en">
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


