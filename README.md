<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Top Up Game - Cepat & Murah</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <style>
    #loader {
      display: none;
    }
  </style>
</head>
<body class="bg-gray-50 text-gray-800">
  <!-- Header -->
  <header class="bg-white shadow sticky top-0 z-50">
    <div class="max-w-7xl mx-auto px-4 py-4 flex items-center justify-between">
      <h1 class="text-2xl font-bold text-blue-600">TopUpZone</h1>
      <nav class="space-x-4">
        <a href="#produk" class="text-gray-600 hover:text-blue-600">Produk</a>
        <a href="#cara" class="text-gray-600 hover:text-blue-600">Cara Top Up</a>
        <a href="riwayat.php" class="text-gray-600 hover:text-blue-600">Riwayat</a>
      </nav>
    </div>
  </header>

  <!-- Hero -->
  <section class="bg-blue-600 text-white py-20 text-center">
    <div class="max-w-xl mx-auto px-4">
      <h2 class="text-4xl font-bold mb-4">Top Up Game Favoritmu dengan Mudah</h2>
      <p class="mb-6">Aman, cepat, dan harga bersahabat. Cukup pilih game, masukkan ID, dan bayar!</p>
      <a href="#produk" class="bg-white text-blue-600 font-semibold px-6 py-3 rounded-xl shadow hover:bg-gray-100 transition">Mulai Top Up</a>
    </div>
  </section>

  <!-- Produk -->
  <section id="produk" class="py-16">
    <div class="max-w-7xl mx-auto px-4">
      <h3 class="text-2xl font-bold text-center mb-10">Pilih Game</h3>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
        <button onclick="pilihGame('Mobile Legends')" class="bg-white shadow rounded-xl p-4 text-center hover:shadow-lg">
          <img src="https://pbs.twimg.com/media/GoK8MAPboAAig5Z?format=jpg&name=small" alt="Mobile Legends" class="w-full mb-3 rounded-xl shadow-md object-cover" />
          <p class="font-semibold">Mobile Legends</p>
        </button>
        <button onclick="pilihGame('Free Fire')" class="bg-white shadow rounded-xl p-4 text-center hover:shadow-lg">
          <img src="https://pbs.twimg.com/media/GoJm4hubAAEybsx?format=jpg&name=small" alt="Free Fire" class="w-full mb-3 rounded-xl shadow-md object-cover" />
          <p class="font-semibold">Free Fire</p>
        </button>
        <button onclick="pilihGame('PUBG')" class="bg-white shadow rounded-xl p-4 text-center hover:shadow-lg">
          <img src="https://pbs.twimg.com/media/GoJrHr8aUAAR9eu?format=jpg&name=small" alt="PUBG" class="w-full mb-3 rounded-xl shadow-md object-cover" />
          <p class="font-semibold">PUBG</p>
        </button>
        <button onclick="pilihGame('Honor of King')" class="bg-white shadow rounded-xl p-4 text-center hover:shadow-lg">
          <img src="https://pbs.twimg.com/media/GoJ0loEaQAAGKiL?format=jpg&name=small" alt="Honor of King" class="w-full mb-3 rounded-xl shadow-md object-cover" />
          <p class="font-semibold">Honor of King</p>
        </button>
      </div>
    </div>
  </section>
<!-- Form Top Up -->
<section id="form" class="py-16 bg-white hidden">
  <div class="max-w-lg mx-auto px-4">
    <h3 class="text-2xl font-bold text-center mb-8">Masukkan ID Game</h3>
    <form action="proses.php" method="POST" class="space-y-4" onsubmit="tampilkanLoader()">
      <input type="hidden" name="game" id="gameInput">
      <input type="text" name="id" placeholder="ID / Server" required class="w-full px-4 py-2 border rounded-xl" />
      <select id="nominalSelect" name="nominal" required class="w-full px-4 py-2 border rounded-xl"></select>
      <select name="method" required class="w-full px-4 py-2 border rounded-xl">
        <option value="QRIS">QRIS</option>
        <option value="Gopay">Gopay</option>
      </select>
      <input type="text" name="kontak" placeholder="Email atau No. WhatsApp" required class="w-full px-4 py-2 border rounded-xl" />
      <button type="submit" class="w-full bg-blue-600 text-white py-3 rounded-xl hover:bg-blue-700 flex justify-center items-center gap-2">
        <svg class="animate-spin h-5 w-5 mr-2 text-white hidden" id="spinner" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
          <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
          <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v8H4z"></path>
        </svg>
        <span id="btnText">Bayar Sekarang</span>
      </button>
      <div id="loader" class="text-center text-blue-600 font-semibold hidden">Memproses pembayaran...</div>
    </form>
  </div>
</section>

<!-- Script untuk Form Dinamis -->
<script>
  const dataProduk = {
    "Mobile Legends": [
      { label: "3 Diamond - Rp1.000", value: 1000 },
      { label: "5 Diamond - Rp1.100", value: 1100 },
      { label: "86 Diamond - Rp22.000", value: 22000 },
      { label: "172 Diamond - Rp45.000", value: 30000 }
    ],
    "Free Fire": [
      { label: "5 Diamond - Rp1.500", value: 1500 },
      { label: "70 Diamond - Rp20.000", value: 20000 },
      { label: "140 Diamond - Rp39.000", value: 39000 }
    ],
    "PUBG": [
      { label: "60 UC - Rp10.000", value: 10000 },
      { label: "325 UC - Rp49.000", value: 49000 }
    ],
    "Honor of King": [
      { label: "10 Token - Rp5.000", value: 5000 },
      { label: "50 Token - Rp20.000", value: 20000 }
    ]
  };

  function pilihGame(nama) {
    document.getElementById('form').classList.remove('hidden');
    document.getElementById('gameInput').value = nama;
    const nominalSelect = document.getElementById('nominalSelect');
    nominalSelect.innerHTML = "";
    dataProduk[nama].forEach(item => {
      const option = document.createElement("option");
      option.value = item.value;
      option.textContent = item.label;
      nominalSelect.appendChild(option);
    });
    document.getElementById('form').scrollIntoView({ behavior: 'smooth' });
  }

  function tampilkanLoader() {
    document.getElementById('loader').classList.remove('hidden');
    document.getElementById('spinner').classList.remove('hidden');
    document.getElementById('btnText').textContent = "Memproses...";
  }
</script>

  <!-- Cara Top Up -->
  <section id="cara" class="bg-gray-100 py-16">
    <div class="max-w-3xl mx-auto px-4 text-center">
      <h3 class="text-2xl font-bold mb-8">Cara Top Up</h3>
      <ol class="space-y-4 text-left">
        <li>1. Pilih game yang ingin kamu top up</li>
        <li>2. Masukkan ID game kamu</li>
        <li>3. Pilih nominal & metode pembayaran</li>
        <li>4. Lakukan pembayaran dan tunggu konfirmasi</li>
      </ol>
    </div>
  </section>

  <!-- Footer -->
  <footer class="bg-white border-t py-6 text-center text-sm text-gray-500">
    &copy; 2025 TopUpZone. All rights reserved.
  </footer>

  <!-- Script -->
  <script>
    const dataProduk = {
      "Mobile Legends": [
        { label: "3 Diamond - Rp1.000", value: 1000 },
        { label: "5 Diamond - Rp1.100", value: 1100 },
        { label: "86 Diamond - Rp22.000", value: 22000 },
        { label: "172 Diamond - Rp45.000", value: 30000 }
      ],
      "Free Fire": [
        { label: "5 Diamond - Rp1.500", value: 1500 },
        { label: "70 Diamond - Rp20.000", value: 20000 },
        { label: "140 Diamond - Rp39.000", value: 39000 }
      ],
      "PUBG": [
        { label: "60 UC - Rp10.000", value: 10000 },
        { label: "325 UC - Rp49.000", value: 49000 }
      ],
      "Honor of King": [
        { label: "10 Token - Rp5.000", value: 5000 },
        { label: "50 Token - Rp20.000", value: 20000 }
      ]
    };

    function pilihGame(nama) {
      document.getElementById('gameInput').value = nama;
      const nominalSelect = document.getElementById('nominalSelect');
      nominalSelect.innerHTML = "";
      dataProduk[nama].forEach(item => {
        const option = document.createElement("option");
        option.value = item.value;
        option.textContent = item.label;
        nominalSelect.appendChild(option);
      });
      document.getElementById('form').scrollIntoView({ behavior: 'smooth' });
    }

    function tampilkanLoader() {
      document.getElementById('loader').classList.remove('hidden');
      document.getElementById('spinner').classList.remove('hidden');
      document.getElementById('btnText').textContent = "Memproses...";
    }
  </script>
</body>
</html>
