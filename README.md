<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>PasirPogorCell</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
body{font-family:Poppins,sans-serif}
.page{animation:slide .4s ease}
@keyframes slide{
from{opacity:0;transform:translateX(30px) scale(.97);filter:blur(5px)}
to{opacity:1;transform:translateX(0) scale(1);filter:blur(0)}
}

/* ===== GLOW SYSTEM ===== */
.card{
  position:relative;
  background:#050505;
  color:white;
  padding:1.3rem;
  border-radius:1rem;
  font-weight:600;
  display:flex;
  justify-content:space-between;
  align-items:center;
  cursor:pointer;
  transition:.35s;
  box-shadow:0 0 15px rgba(34,197,94,.25),0 0 35px rgba(34,197,94,.15);
}
.card::before{
  content:"";
  position:absolute;
  inset:-2px;
  border-radius:1rem;
  background:linear-gradient(120deg,#22c55e,#3b82f6,#22c55e);
  filter:blur(18px);
  opacity:.6;
  z-index:-1;
  animation:glow 3s infinite alternate;
}
@keyframes glow{from{opacity:.3}to{opacity:.7}}

.card:hover{
  transform:scale(1.05);
  box-shadow:0 0 20px rgba(34,197,94,.8),0 0 60px rgba(59,130,246,.7);
}

.menu-active{
  box-shadow:0 0 25px rgba(34,197,94,1),0 0 80px rgba(59,130,246,1)!important;
}

/* buttons */
.back-btn{
  padding:.6rem 1.3rem;
  border-radius:999px;
  background:black;
  color:white;
  font-weight:600;
  border:1px solid #22c55e;
  box-shadow:0 0 15px rgba(34,197,94,.6);
  transition:.3s;
}
.back-btn:hover{transform:scale(1.05)}

.price{color:#22c55e;font-weight:bold}
.ket-btn{background:#facc15;color:black;padding:.2rem .6rem;border-radius:.5rem;font-size:.75rem}
.ket-box{display:none;color:#facc15;font-size:.85rem;padding-left:.5rem;margin-top:.3rem}
</style>
</head>

<body class="min-h-screen bg-gradient-to-br from-black via-gray-900 to-black text-white">

<header class="p-6 text-center border-b border-gray-700">
<h1 class="text-4xl font-bold">PasirPogorCell</h1>
<p class="text-gray-300">Paket Internet & Top Up Game</p>
</header>

<!-- HOME -->
<section id="home" class="page p-6 max-w-4xl mx-auto grid md:grid-cols-2 gap-6 mt-10">
<button onclick="openInternet(this)" class="card">📶 Paket Internet</button>
<button onclick="openGame(this)" class="card">🎮 Top Up Game</button>
</section>

<!-- INTERNET -->
<section id="internet" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="back()" class="back-btn mb-6">← Kembali</button>
<h2 class="text-2xl font-bold mb-4">Pilih Operator</h2>
<div id="operatorList" class="grid md:grid-cols-3 gap-4"></div>
</section>

<section id="paketTypes" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="back()" class="back-btn mb-6">← Kembali</button>
<h2 id="paketTitle" class="text-2xl font-bold mb-4"></h2>
<div id="paketTypeList" class="grid md:grid-cols-3 gap-4"></div>
</section>

<section id="operatorDetail" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="back()" class="back-btn mb-6">← Kembali</button>
<h2 id="operatorTitle" class="text-2xl font-bold mb-4"></h2>
<div id="paketList" class="space-y-3"></div>
</section>

<!-- GAME -->
<section id="game" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="back()" class="back-btn mb-6">← Kembali</button>
<h2 class="text-2xl font-bold mb-4">Pilih Game</h2>
<div id="gameList" class="grid md:grid-cols-3 gap-4"></div>
</section>

<section id="gameDetail" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="back()" class="back-btn mb-6">← Kembali</button>
<h2 id="gameTitle" class="text-2xl font-bold mb-4"></h2>
<div id="topupList" class="space-y-3"></div>
</section>

<footer class="mt-20 p-6 text-center text-sm bg-black/60 space-y-3">
<h3 class="text-lg font-semibold">Silahkan Kunjungi Gerai PasirPogorCell Di Alamat Berikut</h3>
<p class="text-gray-300">📍 Pasir Pogor, RT.2/RW.1, Ciparasi,<br>Kec. Sobang, Kabupaten Lebak, Banten 42280</p>
<a href="https://wa.me/6283844843020" class="text-green-400 inline-block">📞 (+62) 838-4484-3020</a>
<hr class="border-gray-600 my-3">
<p class="text-gray-400 text-xs">© 2026 PasirPogorCell<br>Developed by <span class="font-semibold text-white">Aden Askolani Fahri</span></p>
</footer>

<script>
/* ================= DATA ================= */
const operators = {
  Indosat: {
    "Paket Internet Harian": [
      {nama: "Indosat Yellow 1GB 2 Hari", harga: "Rp 9.000", ket: "Paket harian ringan, cocok untuk kebutuhan singkat"},
      {nama: "Indosat Yellow 1GB 7 Hari", harga: "Rp 10.000", ket: "Lebih hemat untuk pemakaian mingguan"},
      {nama: "Indosat Yellow 1GB 15 Hari", harga: "Rp 12.000", ket: "Cocok untuk pengguna hemat kuota"},
      {nama: "Freedom Mini 3GB 1 Hari", harga: "Rp 10.000", ket: "Kuota besar untuk pemakaian intensif sehari"},
      {nama: "Freedom Mini 5GB 2 Hari", harga: "Rp 12.000", ket: "Streaming & sosial media lebih puas"},
      {nama: "Freedom Mini 3GB 3 Hari", harga: "Rp 15.000", ket: "Paket fleksibel jangka pendek"},
      {nama: "Freedom Mini 2,5GB 5 Hari (Unreg)", harga: "Rp 16.000", ket: "Tidak perlu registrasi tambahan"},
      {nama: "Freedom Mini 3,5GB 5 Hari", harga: "Rp 17.000", ket: "Kuota utama semua jaringan"},
      {nama: "Freedom Mini 5GB 5 Hari (Unreg)", harga: "Rp 20.000", ket: "Langsung aktif tanpa syarat"},
      {nama: "Freedom Mini 7GB 7 Hari", harga: "Rp 26.000", ket: "Pilihan favorit mingguan"},
      {nama: "Freedom Mini 15GB 7 Hari", harga: "Rp 32.000", ket: "Kuota besar untuk aktivitas padat"}
    ],
    "Paket Internet Bulanan": [
      {nama: "100MB 24 Jam 30 Hari", harga: "Rp 2.000", ket: "Paket paling hemat bulanan"},
      {nama: "200MB 24 Jam 30 Hari", harga: "Rp 3.000", ket: "Cocok untuk cadangan kuota"},
      {nama: "250MB 24 Jam 30 Hari", harga: "Rp 3.500", ket: "Pemakaian ringan"},
      {nama: "300MB 24 Jam 30 Hari", harga: "Rp 4.000", ket: "Chat & notifikasi"},
      {nama: "400MB 24 Jam 30 Hari", harga: "Rp 5.000", ket: "Internet dasar bulanan"},
      {nama: "500MB 24 Jam 30 Hari", harga: "Rp 6.000", ket: "Pemakaian normal"},
      {nama: "600MB 24 Jam 30 Hari", harga: "Rp 7.000", ket: "Lebih stabil untuk browsing"},
      {nama: "700MB 24 Jam 30 Hari", harga: "Rp 8.000", ket: "Pilihan hemat bulanan"},
      {nama: "800MB 24 Jam 30 Hari", harga: "Rp 8.500", ket: "Kuota utama ringan"},
      {nama: "1GB Semua Jaringan 30 Hari", harga: "Rp 9.000", ket: "Semua jaringan tanpa batas aplikasi"},
      {nama: "1,5GB Semua Jaringan 30 Hari", harga: "Rp 13.000", ket: "Cocok untuk media sosial"},
      {nama: "2GB Semua Jaringan 30 Hari", harga: "Rp 16.000", ket: "Internet harian stabil"},
      {nama: "2,5GB Semua Jaringan 30 Hari", harga: "Rp 20.000", ket: "Pemakaian normal bulanan"},
      {nama: "3GB Semua Jaringan 30 Hari", harga: "Rp 22.000", ket: "Pilihan terlaris"},
      {nama: "4GB Semua Jaringan 30 Hari", harga: "Rp 28.000", ket: "Streaming ringan"},
      {nama: "Freedom Internet 3GB 28 Hari", harga: "Rp 23.000", ket: "Freedom reguler bulanan"},
      {nama: "Freedom Internet 4GB 28 Hari", harga: "Rp 29.000", ket: "Kuota utama Freedom"},
      {nama: "Freedom Internet 5.5GB 28 Hari", harga: "Rp 33.000", ket: "Lebih hemat kuota besar"},
      {nama: "Freedom Internet 9GB 28 Hari", harga: "Rp 44.000", ket: "Cocok untuk streaming"},
      {nama: "Freedom Internet 13GB 28 Hari", harga: "Rp 57.000", ket: "Aktivitas online intensif"},
      {nama: "Freedom Internet 16GB 28 Hari", harga: "Rp 69.000", ket: "Kuota besar bulanan"},
      {nama: "Freedom Internet 20GB 28 Hari", harga: "Rp 71.000", ket: "Penggunaan berat"},
      {nama: "Freedom Internet 25GB 28 Hari", harga: "Rp 83.000", ket: "Rekomendasi pengguna aktif"},
      {nama: "Freedom Internet 30GB 28 Hari", harga: "Rp 97.000", ket: "Streaming & gaming"},
      {nama: "Freedom Internet 42GB 28 Hari", harga: "Rp 105.000", ket: "Kuota jumbo"},
      {nama: "Freedom Internet Sensasi 50GB 28 Hari", harga: "Rp 106.000", ket: "Kuota besar harga hemat"},
      {nama: "Freedom Internet Sensasi 70GB 28 Hari", harga: "Rp 127.000", ket: "Streaming tanpa khawatir"},
      {nama: "Freedom Internet Sensasi 150GB 28 Hari", harga: "Rp 160.000", ket: "Kuota super besar"},
      {nama: "Freedom Internet Sensasi 200GB 28 Hari", harga: "Rp 201.000", ket: "Untuk kebutuhan ekstrem"}
    ],
    "Paket Unlimited": [
      {nama: "1GB + 2GB + Aplikasi Unlimited 6 Hari", harga: "Rp 20.000", ket: "Unlimited aplikasi pilihan"},
      {nama: "1GB Semua + 4,5GB + Aplikasi Unlimited 28 Hari", harga: "Rp 36.000", ket: "Kuota + unlimited app"},
      {nama: "2GB Semua + 7,5–8GB + Aplikasi Unli 28 Hari", harga: "Rp 59.000", ket: "Paket combo hemat"},
      {nama: "3GB Semua + 15–17GB + Aplikasi Tanpa Batas 28 Hari", harga: "Rp 83.000", ket: "Untuk pengguna aktif"},
      {nama: "7GB Semua + 28GB + Aplikasi Unlimited 28 Hari", harga: "Rp 108.000", ket: "Kuota besar + unlimited"},
      {nama: "10GB Semua + 35GB + Aplikasi Tanpa Batas 28 Hari", harga: "Rp 120.000", ket: "Streaming & kerja"},
      {nama: "15GB All + 25GB + Unlimited App, Telp & SMS 28 Hari", harga: "Rp 131.000", ket: "Paket lengkap all in one"},
      {nama: "Unlimited 90GB + Unli App + Telp + SMS 28 Hari", harga: "Rp 162.000", ket: "Unlimited maksimal"}
    ]
  },
  Axis: {
    "Paket Internet Harian": [
      {nama: "Mini 1,5GB + Bonus Aigo 1 Hari", harga: "Rp 8.000", ket: "Paket harian hemat"},
      {nama: "Mini Axis 2,5GB + Bonus Aigo 1 Hari", harga: "Rp 10.000", ket: "Internet cepat sehari"},
      {nama: "Mini Axis 2GB + Bonus Aigo 3 Hari", harga: "Rp 12.000", ket: "Cocok untuk aktivitas ringan"},
      {nama: "Mini Axis 2,5GB + Bonus Aigo 3 Hari", harga: "Rp 13.000", ket: "Pemakaian normal"},
      {nama: "Mini Axis 3GB + Bonus Aigo 3 Hari", harga: "Rp 13.000", ket: "Kuota lebih lega"},
      {nama: "Mini Axis 4,5GB + Bonus Aigo 3 Hari", harga: "Rp 15.000", ket: "Streaming & sosmed"},
      {nama: "Mini Axis 9GB + Bonus Aigo 3 Hari", harga: "Rp 17.000", ket: "Kuota besar harian"},
      {nama: "Aigo Kuota Mini 1,5GB + Bonus 1GB 1 Hari", harga: "Rp 8.000", ket: "Bonus AIGO aktif"}
    ],
    "Paket Per Jam": [
      {nama: "Mini 1,5GB + Bonus Aigo 1 Hari", harga: "Rp 8.000", ket: "Paket harian hemat"},
      {nama: "Mini Axis 2,5GB + Bonus Aigo 1 Hari", harga: "Rp 10.000", ket: "Internet cepat sehari"},
      {nama: "Mini Axis 2GB + Bonus Aigo 3 Hari", harga: "Rp 12.000", ket: "Cocok untuk aktivitas ringan"},
      {nama: "Mini Axis 2,5GB + Bonus Aigo 3 Hari", harga: "Rp 13.000", ket: "Pemakaian normal"},
      {nama: "Mini Axis 3GB + Bonus Aigo 3 Hari", harga: "Rp 13.000", ket: "Kuota lebih lega"},
      {nama: "Mini Axis 4,5GB + Bonus Aigo 3 Hari", harga: "Rp 15.000", ket: "Streaming & sosmed"},
      {nama: "Mini Axis 9GB + Bonus Aigo 3 Hari", harga: "Rp 17.000", ket: "Kuota besar harian"},
      {nama: "Aigo Kuota Mini 1,5GB + Bonus 1GB 1 Hari", harga: "Rp 8.000", ket: "Bonus AIGO aktif"}
    ],
    "Paket Internet Bulanan": [
      {nama: "Axis Data 1GB Semua 30 Hari", harga: "Rp 10.000", ket: "Paket dasar bulanan"},
      {nama: "Bronet 2GB + Bonus Aigo 30 Hari", harga: "Rp 18.000", ket: "Kuota + bonus AIGO"},
      {nama: "Bronet 3GB + Bonus Aigo 30 Hari", harga: "Rp 21.000", ket: "Pilihan hemat"},
      {nama: "Bronet 6GB + Bonus Aigo 30 Hari", harga: "Rp 32.000", ket: "Kuota sedang"},
      {nama: "Bronet 8GB + Bonus Aigo 30 Hari", harga: "Rp 41.000", ket: "Streaming ringan"},
      {nama: "Bronet 14GB + Bonus Aigo 30 Hari", harga: "Rp 62.000", ket: "Kuota besar"},
      {nama: "Axis Bronet 16GB Semua 30 Hari", harga: "Rp 74.000", ket: "Semua jaringan"},
      {nama: "Bronet 20GB + Bonus Aigo 30 Hari", harga: "Rp 74.000", ket: "Aktivitas padat"},
      {nama: "Bronet 30GB + Bonus Aigo 30 Hari", harga: "Rp 91.000", ket: "Kuota jumbo"},
      {nama: "Bronet 2GB Semua 24 Jam 60 Hari", harga: "Rp 32.000", ket: "Masa aktif panjang"},
      {nama: "Bronet 3GB Semua 24 Jam 60 Hari", harga: "Rp 41.000", ket: "Internet stabil"},
      {nama: "Bronet 5GB Semua 24 Jam 60 Hari", harga: "Rp 58.000", ket: "Hemat jangka panjang"},
      {nama: "Bronet 8GB Semua 24 Jam 60 Hari", harga: "Rp 78.000", ket: "Streaming bulanan"},
      {nama: "Bronet 10GB Semua 24 Jam 60 Hari", harga: "Rp 89.000", ket: "Kuota besar"},
      {nama: "Bronet 12GB Semua 24 Jam 60 Hari", harga: "Rp 100.000", ket: "Pemakaian aktif"},
      {nama: "Bronet 35GB + Bonus Aigo 60 Hari", harga: "Rp 110.000", ket: "Kuota super besar"},
      {nama: "Bronet 16GB Semua 24 Jam 60 Hari", harga: "Rp 119.000", ket: "All network"},
      {nama: "Bronet 75GB + Bonus Aigo 60 Hari", harga: "Rp 171.000", ket: "Kuota ekstrem"}
    ]
  },
  XL: {
    "XL Data Harian":[
      {nama: "XL Reguler 800MB 24 Jam 30 Hari", harga: "Rp 10.000", ket: "Kuota ringan harian"},
      {nama: "XL Xtra On 1GB All Jaringan 30 Hari", harga: "Rp 18.000", ket: "Internet stabil"},
      {nama: "XL Reguler 1,5GB 24 Jam 30 Hari", harga: "Rp 22.000", ket: "Browsing & chat"},
      {nama: "XL Xtra On 2GB All Jaringan 30 Hari", harga: "Rp 26.000", ket: "Aktivitas normal"},
      {nama: "XL Reguler 3GB 24 Jam 30 Hari", harga: "Rp 28.000", ket: "Streaming ringan"},
      {nama: "XL Reguler 6GB 24 Jam 30 Hari", harga: "Rp 61.000", ket: "Kuota menengah"},
      {nama: "XL Reguler 8GB 24 Jam 30 Hari", harga: "Rp 71.000", ket: "Pemakaian aktif"},
      {nama: "XL Reguler 12GB 24 Jam 30 Hari", harga: "Rp 97.000", ket: "Streaming & gaming"},
      {nama: "XL Reguler 16GB 24 Jam 30 Hari", harga: "Rp 102.000", ket: "Kuota besar bulanan"}
    ],
    "XL Data Bulanan":[
      {nama: "XL Kuota Games 1GB 30 Hari", harga: "Rp 8.000", ket: "Game online ringan"},
      {nama: "500MB All + 500MB Games 30 Hari", harga: "Rp 9.000", ket: "Combo internet & game"},
      {nama: "XL Kuota Games 2GB 30 Hari", harga: "Rp 12.000", ket: "Main game harian"},
      {nama: "1GB All + 1GB Games 30 Hari", harga: "Rp 13.000", ket: "Sosmed & gaming"},
      {nama: "1,5GB All + 1,5GB Games 30 Hari", harga: "Rp 18.000", ket: "Aktivitas seimbang"},
      {nama: "2GB All + 2GB Games 30 Hari", harga: "Rp 23.000", ket: "Main game rutin"},
      {nama: "3GB All + 3GB Games 30 Hari", harga: "Rp 33.000", ket: "Game intensif"},
      {nama: "4GB All + 4GB Games 30 Hari", harga: "Rp 44.000", ket: "Gamer aktif"},
      {nama: "5GB All + 5GB Games 30 Hari", harga: "Rp 53.000", ket: "Gamer berat"}
    ],
    "XL Data Games":[
      {nama: "XL Kuota Games 1GB 30 Hari", harga: "Rp 8.000", ket: "Game online ringan"},
      {nama: "500MB All + 500MB Games 30 Hari", harga: "Rp 9.000", ket: "Combo internet & game"},
      {nama: "XL Kuota Games 2GB 30 Hari", harga: "Rp 12.000", ket: "Main game harian"},
      {nama: "1GB All + 1GB Games 30 Hari", harga: "Rp 13.000", ket: "Sosmed & gaming"},
      {nama: "1,5GB All + 1,5GB Games 30 Hari", harga: "Rp 18.000", ket: "Aktivitas seimbang"},
      {nama: "2GB All + 2GB Games 30 Hari", harga: "Rp 23.000", ket: "Main game rutin"},
      {nama: "3GB All + 3GB Games 30 Hari", harga: "Rp 33.000", ket: "Game intensif"},
      {nama: "4GB All + 4GB Games 30 Hari", harga: "Rp 44.000", ket: "Gamer aktif"},
      {nama: "5GB All + 5GB Games 30 Hari", harga: "Rp 53.000", ket: "Gamer berat"}
    ]
  },

  Tri: {
    "Paket Internet Harian":[
      {nama: "1GB All + 1,5GB Malam 1 Hari", harga: "Rp 9.000", ket: "Internet + malam"},
      {nama: "1,5GB All Jaringan 14 Hari", harga: "Rp 13.000", ket: "Hemat panjang"},
      {nama: "Tri Data Mini 1,5GB 7 Hari", harga: "Rp 13.000", ket: "Ringan mingguan"},
      {nama: "2,75GB All Jaringan 3 Hari", harga: "Rp 16.000", ket: "Pemakaian singkat"},
      {nama: "750MB + 2GB 4G 3 Hari", harga: "Rp 16.000", ket: "Bonus jaringan 4G"},
      {nama: "2,5GB All Jaringan 14 Hari", harga: "Rp 18.000", ket: "Aktivitas normal"},
      {nama: "Tri Data Mini 3GB 7 Hari", harga: "Rp 23.000", ket: "Streaming ringan"},
      {nama: "4GB All Jaringan 14 Hari", harga: "Rp 27.000", ket: "Kuota sedang"},
      {nama: "1,75GB All + 2GB 4G 7 Hari", harga: "Rp 28.000", ket: "Combo kuota"},
      {nama: "2GB All Jaringan 14 Hari", harga: "Rp 28.000", ket: "Browsing & sosmed"},
      {nama: "10GB 10 Hari (1GB/Hari)", harga: "Rp 40.000", ket: "Kuota harian stabil"},
      {nama: "Tri Data Mini 12GB 7 Hari", harga: "Rp 33.000", ket: "Kuota besar mingguan"}
    ],
    "Paket Internet Bulanan":[
      {nama: "Tri All Jaringan 3GB 30 Hari", harga: "Rp 20.000", ket: "Bulanan hemat"},
      {nama: "Tri All Jaringan 10GB 30 Hari", harga: "Rp 38.000", ket: "Bulanan reguler"},
      {nama: "Data Harian 10GB 10 Hari", harga: "Rp 40.000", ket: "Kuota harian akumulasi"},
      {nama: "Tri All Jaringan 15GB 30 Hari", harga: "Rp 53.000", ket: "Streaming ringan"},
      {nama: "Data Harian 30GB 30 Hari", harga: "Rp 66.000", ket: "1GB per hari"},
      {nama: "Tri All Jaringan 20GB 30 Hari", harga: "Rp 74.000", ket: "Aktivitas padat"},
      {nama: "Tri All Jaringan 30GB 30 Hari", harga: "Rp 80.000", ket: "Kuota besar"},
      {nama: "Data Harian 60GB 30 Hari", harga: "Rp 101.000", ket: "2GB per hari"},
      {nama: "Tri All Jaringan 50GB 30 Hari", harga: "Rp 103.000", ket: "Streaming berat"},
      {nama: "Tri All Jaringan 100GB 28 Hari", harga: "Rp 130.000", ket: "Kuota jumbo"},
      {nama: "Tri All Jaringan 75GB 60 Hari", harga: "Rp 149.000", ket: "Masa aktif panjang"},
      {nama: "Tri All Jaringan 175GB 180 Hari", harga: "Rp 344.000", ket: "Kuota ekstrem"},
      {nama: "Tri All Jaringan 250GB 365 Hari", harga: "Rp 488.000", ket: "Tahunan super besar"}
    ]
  },

  Telkomsel: {
    "Paket Internet Harian": [
      {nama: "Mini Data 1GB All 1 Hari", harga: "Rp 10.000", ket: "Internet harian"},
      {nama: "Mini Data 500MB All 3 Hari", harga: "Rp 10.000", ket: "Hemat singkat"},
      {nama: "Mini Data 1,5GB Semua 3 Hari (Non-Pamasuka)", harga: "Rp 13.000", ket: "Area non Pamasuka"},
      {nama: "Mini Data 1GB All 3 Hari", harga: "Rp 13.000", ket: "Browsing ringan"},
      {nama: "Mini Data 2,5GB Semua 5 Hari", harga: "Rp 15.000", ket: "Pemakaian normal"},
      {nama: "Mini Data 2GB All 3 Hari", harga: "Rp 15.000", ket: "Aktivitas singkat"},
      {nama: "Mini Data 2,5GB – 3GB Semua 5 Hari", harga: "Rp 16.000", ket: "Kuota fleksibel"},
      {nama: "Mini Data 4GB All 1 Hari", harga: "Rp 12.550", ket: "Internet cepat"},
      {nama: "Mini Data 6GB All 1 Hari", harga: "Rp 23.000", ket: "Streaming seharian"},
      {nama: "Mini Data 5GB Semua 1 Hari", harga: "Rp 25.000", ket: "Kuota besar harian"},
      {nama: "Mini Data 3GB Semua 3 Hari", harga: "Rp 27.000", ket: "Internet stabil"},
      {nama: "Mini Data 5GB Semua 3 Hari", harga: "Rp 34.000", ket: "Streaming & sosmed"},
      {nama: "Mini Data 8GB All 3 Hari", harga: "Rp 40.000", ket: "Kuota jumbo singkat"},
      {nama: "Mini Data 7GB All 3 Hari", harga: "Rp 50.000", ket: "Pemakaian intensif"},
      {nama: "Mini Data 17GB All 3 Hari", harga: "Rp 64.000", ket: "Kuota ekstrem"},
      {nama: "Mini Data 15GB All 3 Hari", harga: "Rp 66.000", ket: "Streaming berat"},
      {nama: "Mini Data 20GB All 3 Hari", harga: "Rp 74.000", ket: "Kuota super besar"},
      {nama: "Mini Data 10GB All 3 Hari", harga: "Rp 78.000", ket: "Penggunaan padat"}
    ],
    "Paket Internet Mingguan": [
      {nama: "Mini Data 50MB 7 Hari", harga: "Rp 4.000", ket: "Darurat"},
      {nama: "Mini Data 100MB 7 Hari", harga: "Rp 7.000", ket: "Cadangan"},
      {nama: "Mini Data 250MB 7 Hari", harga: "Rp 8.000", ket: "Ringan"},
      {nama: "Mini Data 500MB 7 Hari", harga: "Rp 10.000", ket: "Hemat mingguan"},
      {nama: "Mini Data 500MB Semua 7 Hari", harga: "Rp 11.000", ket: "All network"},
      {nama: "Mini Data 1GB All 7 Hari", harga: "Rp 13.000", ket: "Pemakaian normal"},
      {nama: "1GB Semua Jaringan 30 Hari", harga: "Rp 15.000", ket: "Paket spesial"},
      {nama: "Mini Data 750MB 7 Hari", harga: "Rp 18.000", ket: "Aktivitas ringan"},
      {nama: "Mini Data 2GB All 7 Hari", harga: "Rp 19.000", ket: "Streaming ringan"},
      {nama: "Mini Data 3GB Semua 7 Hari", harga: "Rp 24.000", ket: "Sosmed & browsing"},
      {nama: "Mini Data 2GB Semua 14 Hari", harga: "Rp 25.000", ket: "Masa aktif panjang"},
      {nama: "Mini Data 5GB Semua 7 Hari", harga: "Rp 29.000", ket: "Kuota besar"},
      {nama: "Mini Data 7GB Semua 7 Hari", harga: "Rp 30.000", ket: "Streaming aktif"},
      {nama: "Mini Data 17GB Semua 7 Hari", harga: "Rp 80.000", ket: "Kuota ekstrem mingguan"}
    ],

    "Data Mini Jabo - Banten": [
      {nama: "Paket Data 1,5GB 3 Hari", harga: "Rp 11.000", ket: "Area Jabo-Banten"},
      {nama: "Paket Data 2,5GB 5 Hari", harga: "Rp 14.000", ket: "Lokal hemat"},
      {nama: "Paket Data 3GB 3 Hari", harga: "Rp 15.000", ket: "Internet stabil"},
      {nama: "Paket Data 3GB 5 Hari", harga: "Rp 16.000", ket: "Kuota fleksibel"},
      {nama: "Paket Data 3,5GB 7 Hari", harga: "Rp 22.000", ket: "Aktivitas mingguan"},
      {nama: "Paket Data 4,5GB 5 Hari", harga: "Rp 23.000", ket: "Streaming ringan"},
      {nama: "Paket Data 5,5GB 5 Hari", harga: "Rp 27.000", ket: "Kuota sedang"},
      {nama: "Paket Data 5GB 7 Hari", harga: "Rp 29.000", ket: "Pemakaian normal"},
      {nama: "Paket Data 7GB 7 Hari", harga: "Rp 30.000", ket: "Kuota besar lokal"},
      {nama: "0,5GB All + 1,5GB Lokal + 2GB OMG 30 Hari", harga: "Rp 36.000", ket: "Combo OMG"},
      {nama: "Paket Data 10GB 7 Hari", harga: "Rp 39.000", ket: "Streaming aktif"},
      {nama: "Paket Data 12GB 7 Hari", harga: "Rp 44.000", ket: "Kuota besar"},
      {nama: "1,25GB All + 3,75GB Lokal + 2GB OMG 30 Hari", harga: "Rp 50.000", ket: "Combo lokal"},
      {nama: "2GB All + 6GB Lokal + 2GB OMG 30 Hari", harga: "Rp 65.000", ket: "Kuota besar lokal"},
      {nama: "3GB All + 9GB Lokal + 2GB OMG 30 Hari", harga: "Rp 74.000", ket: "Aktivitas padat"},
      {nama: "4,5GB All + 13,5GB Lokal + 2GB OMG 30 Hari", harga: "Rp 85.000", ket: "Kuota jumbo lokal"},
      {nama: "5GB + 37GB Lokal Jabo-Jabar 30 Hari", harga: "Rp 101.000", ket: "Lokal super besar"},
      {nama: "6GB + 54GB Lokal Jabo-Jabar 30 Hari", harga: "Rp 141.000", ket: "Pemakaian berat"},
      {nama: "9GB + 71GB Lokal Jabo-Jabar 30 Hari", harga: "Rp 170.000", ket: "Kuota ekstrem lokal"}
    ]
  },

  ByU: {
    "Paket Internet Bulanan":[
      {nama: "1GB Semua + Bebas Tiktok 500MB / 1 Hari", harga: "Rp 8.000", ket: "Paket ByU harian"},
      {nama: "Kuota 2GB Semua 1 Hari", harga: "Rp 10.000", ket: "Internet cepat sehari"},
      {nama: "2GB Semua + Bebas Tiktok 500MB / 3 Hari", harga: "Rp 12.000", ket: "Bonus TikTok aktif"},
      {nama: "10GB Semua + Bebas Tiktok 500MB / 1 Hari", harga: "Rp 14.000", ket: "Kuota besar harian"},
      {nama: "Kuota 2,5GB Semua 5 Hari", harga: "Rp 14.000", ket: "Pemakaian normal"},
      {nama: "Kuota 3GB Semua 7 Hari", harga: "Rp 16.000", ket: "Mingguan hemat"},
      {nama: "ByU Yang Bikin Deket 3GB 1 Hari", harga: "Rp 21.000", ket: "Paket promo ByU"},
      {nama: "Kuota 5GB Semua 7 Hari", harga: "Rp 21.000", ket: "Streaming ringan"}
    ]
  }
};
  
const games = {
  "Mobile Legends":[  "3 Diamond Rp 3.000",
  "19 (17+2) Diamond Rp 10.000",
  "28 (25+3) Diamond Rp 11.000",
  "36 (33+3) Diamond Rp 13.000",
  "44 (40+4) Diamond Rp 15.000",
  "56 (51+5) Diamond Rp 19.000",
  "59 (53+6) Diamond Rp 20.000",
  "74 (69+5) Diamond Rp 23.000",
  "85 (77+8) Diamond Rp 27.000",
  "86 (78+8) Diamond Rp 27.000",
  "100 Diamond Rp 31.000",
  "Weekly Diamond Pass 220 (80+20/Day) Rp 31.000",
  "112 (102+10) Diamond Rp 34.000",
  "144 (130+14) Diamond Rp 42.000",
  "170 (154+16) Diamond Rp 50.000",
  "172 (156+16) Diamond Rp 50.000",
  "185 (167+18) Diamond Rp 54.000",
  "2x Weekly Diamond Pass 440 (80+20/Day) Rp 60.000",
  "222 (200+22) Diamond Rp 63.000",
  "229 (207+22) Diamond Rp 66.000",
  "240 (217+23) Diamond Rp 69.000",
  "257 (234+23) Diamond Rp 72.000",
  "Pass Coupon Rp 76.000",
  "278 (251+27) Diamond Rp 79.000",
  "284 (254+30) Diamond Rp 80.000",
  "296 (256+40) Diamond Rp 82.000",
  "301 (261+40) Diamond Rp 84.000",
  "Starlight Membership Rp 85.000",
  "3x Weekly Diamond Pass 660 (80+20/Day) Rp 87.000",
  "344 (312+32) Diamond Rp 96.000",
  "345 (301+44) Diamond Rp 97.000",
  "355 (309+46) Diamond Rp 100.000",
  "374 (326+48) Diamond Rp 106.000",
  "381 (333+48) Diamond Rp 107.000",
  "384 Diamond Rp 110.000",
  "408 (367+41) Diamond Rp 114.000",
  "4x Weekly Diamond Pass 880 (80+20/Day) Rp 115.000",
  "429 (390+39) Diamond Rp 118.000",
  "425 (373+52) Diamond Rp 120.000",
  "448 Diamond Rp 137.000",
  "460 Diamond Rp 140.000",
  "514 (468+46) Diamond Rp 142.000",
  "5x Weekly Diamond Pass 1100 (80+20/Day) Rp 143.000",
  "522 (471+51) Diamond Rp 146.000",
  "500 Diamond Rp 150.000",
  "Twilight Pass Rp 155.000",
  "568 (503+65) Diamond Rp 155.000",
  "601 (533+68) Diamond Rp 165.000",
  "642 Diamond Rp 185.000",
  "706 (625+81) Diamond Rp 200.000",
  "712 (633+79) Diamond Rp 201.000",
  "717 (638+79) Diamond Rp 203.000",
  "Starlight Plus Member Rp 220.000",
  "875 (774+101) Diamond Rp 240.000",
  "965 (856+109) Diamond Rp 264.000",
  "963 (859+104) Diamond Rp 265.000",
  "977 (867+110) Diamond Rp 268.000"],
  "Free Fire":[  "5 (0+5) Diamond Rp 3.000",
  "12 (9+3) Diamond Rp 4.000",
  "50 (45+5) Diamond Rp 10.000",
  "70 (63+7) Diamond Rp 12.000",
  "100 (90+10) Diamond Rp 16.000",
  "Membership Level Up Pass Rp 17.000",
  "140 (126+14) Diamond Rp 21.000",
  "210 (189+21) Diamond Rp 30.000",
  "Membership Mingguan 50 Diamond Rp 31.000",
  "300 (270+30) Diamond Rp 43.000",
  "Booyah Pass (BP Card) Rp 45.000",
  "355 (320+35) Diamond Rp 50.000",
  "500 (450+50) Diamond Rp 70.000",
  "Membership Bulanan 50 Diamond Rp 86.000",
  "720 (648+72) Diamond Rp 92.000",
  "1000 (900+100) Diamond Rp 132.000",
  "1450 (1305+145) Diamond Rp 190.000",
  "2180 (1962+218) Diamond Rp 290.000",
  "3640 (3276+364) Diamond Rp 480.000",
  "4000 (3600+400) Diamond Rp 530.000",
  "7290 (6561+729) Diamond Rp 950.000"
],
  "PUBG Mobile": [
  "15 (14+1) UC Rp 11.000",
  "25 (22+3) UC Rp 12.000",
  "35 (31+4) UC Rp 18.000",
  "50 (45+5) UC Rp 18.000",
  "60 (54+6) UC Rp 18.000",
  "70 (63+7) UC Rp 30.000",
  "100 (90+10) UC Rp 34.000",
  "125 (113+12) UC Rp 48.000",
  "150 (135+15) UC Rp 48.000",
  "200 (180+20) UC Rp 63.000",
  "210 (189+21) UC Rp 63.000",
  "250 (225+25) UC Rp 78.000",
  "300 (270+30) UC Rp 79.000",
  "350 (315+35) UC Rp 94.000",
  "375 (338+37) UC Rp 93.000",
  "500 (450+50) UC Rp 127.000",
  "525 (473+52) UC Rp 138.000",
  "700 (630+70) UC Rp 172.000",
  "750 (675+75) UC Rp 187.000",
  "1000 (900+100) UC Rp 244.000",
  "1100 (990+110) UC Rp 258.000",
  "1250 (1125+125) UC Rp 302.000",
  "1500 (1350+150) UC Rp 347.000",
  "1750 (1575+175) UC Rp 378.000",
  "Elite Pass Plus + Kupon Peti Rp 432.000",
  "2500 (2250+250) UC Rp 539.000"
],
"Call Of Duty Mobile": [
  "63 (57+6) CP Rp 12.000",
  "128 (115+13) CP Rp 21.000",
  "321 (288+33) CP Rp 48.000",
  "645 (580+65) CP Rp 94.000",
  "645 (580+65) CP Rp 101.000",
  "800 (720+80) CP Rp 114.000",
  "1373 (1235+138) CP Rp 188.000",
  "2060 (1854+206) CP Rp 276.000",
  "2750 (2475+275) CP Rp 349.000",
  "3564 (3207+357) CP Rp 454.000",
  "5619 (5057+562) CP Rp 691.000",
  "7656 (6890+766) CP Rp 978.000"
],
"Honor Of Kings": [
  "16 (14+2) Tokens Rp 6.000",
  "80 (72+8) Tokens Rp 18.000",
  "240 (216+24) Tokens Rp 47.000",
  "400 (360+40) Tokens Rp 76.000",
  "560 (504+56) Tokens Rp 105.000",
  "800 + 30 Tokens Rp 150.000",
  "1200 + 45 Tokens Rp 225.000",
  "2400 + 108 Tokens Rp 442.000",
  "4000 + 180 Tokens Rp 808.000"
],
"Genshin Impact": [
  "60 (54+6) Crystals Rp 14.000",
  "60 (54+6) Chronal Nexus Rp 15.000",
  "Blessing Welkin Moon Rp 60.000",
  "300 + 30 Crystals Rp 60.000",
  "300 + 30 Chronal Nexus Rp 66.000",
  "Blessing Welkin Moon x2 Rp 117.000",
  "Blessing Welkin Moon x3 Rp 175.000",
  "980 + 110 Crystals Rp 180.000",
  "980 + 110 Chronal Nexus Rp 194.000",
  "Blessing Welkin Moon x4 Rp 229.000",
  "Limited Outfit Guaranteed 1420 Crystals Rp 234.000",
  "1280 + 140 Crystals Rp 234.000",
  "Blessing Welkin Moon x5 Rp 283.000",
  "1980 + 260 Crystals Rp 365.000",
  "Blessing Welkin Moon x6 Rp 378.000",
  "1980 + 260 Chronal Nexus Rp 409.000",
  "3280 + 600 Crystals Rp 623.000",
  "3280 + 600 Chronal Nexus Rp 656.000",
  "4260 + 710 Crystals Rp 841.000"
],
"Roblox": [
  "100 (90+10) Robux Rp 50.000",
  "200 (180+20) Robux Rp 50.000",
  "250 (225+25) Robux Rp 50.000",
  "Gift Card IDR 50K Rp 50.000",
  "Gift Card IDR 65K Rp 65.000",
  "Gift Card IDR 100K Rp 97.000",
  "800 (720+80) Robux Rp 156.000",
  "Roblox USD 10 Global Rp 168.000",
  "Gift Card IDR 200K Rp 194.000",
  "Gift Card IDR 300K Rp 285.000",
  "Gift Card IDR 380K Rp 371.000",
  "2000 (1800+200) Robux Rp 373.000",
  "Roblox USD 25 Global Rp 405.000",
  "Gift Card IDR 500K Rp 470.000",
  "4500 (4050+450) Robux Rp 829.000",
  "Roblox USD 50 Global Rp 873.000",
  "Gift Card IDR 950K Rp 997.000"
]
};

//* ===== NAV ===== */
let historyStack=[];
function hideAll(){document.querySelectorAll("section").forEach(s=>s.classList.add("hidden"))}
function back(){const f=historyStack.pop();if(f){hideAll();f();}}
function clearActive(){document.querySelectorAll(".menu-active").forEach(x=>x.classList.remove("menu-active"))}

/* ===== INTERNET ===== */
function openInternet(b){
 clearActive();b.classList.add("menu-active");
 historyStack.push(()=>home.classList.remove("hidden"));
 hideAll();internet.classList.remove("hidden");
 operatorList.innerHTML="";
 Object.keys(operators).forEach(o=>{
  operatorList.innerHTML+=`<div class="card" onclick="openTypes('${o}')">${o}</div>`;
 });
}
function openTypes(op){
 historyStack.push(()=>internet.classList.remove("hidden"));
 hideAll();paketTypes.classList.remove("hidden");
 paketTitle.innerText=op;
 paketTypeList.innerHTML="";
 Object.keys(operators[op]).forEach(t=>{
  paketTypeList.innerHTML+=`<div class="card" onclick="openPaket('${op}','${t}')">${t}</div>`;
 });
}
function openPaket(op,cat){
 historyStack.push(()=>paketTypes.classList.remove("hidden"));
 hideAll();operatorDetail.classList.remove("hidden");
 operatorTitle.innerText=op+" - "+cat;
 paketList.innerHTML="";
 operators[op][cat].forEach((p,i)=>{
  paketList.innerHTML+=`
  <div class="card">${p.nama} <span class="price">${p.harga}</span>
  <button class="ket-btn" onclick="toggleKet('${op}${cat}${i}')">?</button></div>
  <div id="${op}${cat}${i}" class="ket-box">${p.ket}</div>`;
 });
}
function toggleKet(id){
 const e=document.getElementById(id);
 e.style.display=e.style.display=="block"?"none":"block";
}

/* ===== GAME ===== */
function openGame(b){
 clearActive();b.classList.add("menu-active");
 historyStack.push(()=>home.classList.remove("hidden"));
 hideAll();game.classList.remove("hidden");
 gameList.innerHTML="";
 Object.keys(games).forEach(g=>{
  gameList.innerHTML+=`<div class="card" onclick="openGameDetail('${g}')">${g}</div>`;
 });
}
function openGameDetail(g){
  historyStack.push(()=>game.classList.remove("hidden"));
  hideAll();
  gameDetail.classList.remove("hidden");
  gameTitle.innerText = g;
  topupList.innerHTML = "";

  games[g].forEach(item=>{
    const harga = item.match(/Rp\s?[\d\.]+/);
    let text = item;

    if(harga){
      text = item.replace(harga[0], `<span class="price">${harga[0]}</span>`);
    }

    topupList.innerHTML += `<div class="card">${text}</div>`;
  });
}
</script>

</body>
</html>

