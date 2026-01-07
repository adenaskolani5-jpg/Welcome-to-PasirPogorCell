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
.page{animation:slide .45s ease}
@keyframes slide{
from{opacity:0;transform:translateX(30px) scale(.97);filter:blur(4px)}
to{opacity:1;transform:translateX(0) scale(1);filter:blur(0)}
}
.card{
background:white;color:black;
padding:1.4rem;border-radius:1rem;
font-weight:600;transition:.3s;cursor:pointer;
}
.card:hover{
background:black;color:white;
transform:scale(1.05);
border:1px solid white
}
.back-btn{
  display:inline-flex;
  align-items:center;
  gap:.6rem;
  padding:.6rem 1.2rem;
  border-radius:999px;
  background:linear-gradient(135deg,#111,#333);
  color:white;
  font-weight:600;
  border:1px solid rgba(255,255,255,.2);
  transition:.35s ease;
  position:relative;
  overflow:hidden;
  cursor:pointer;
}
.back-btn::before{
  content:"";
  position:absolute;
  inset:0;
  background:linear-gradient(120deg,transparent,rgba(255,255,255,.15),transparent);
  transform:translateX(-100%);
  transition:.6s;
}
.back-btn:hover::before{
  transform:translateX(100%);
}
.back-btn:hover{
  transform:translateX(-4px) scale(1.03);
  box-shadow:0 0 18px rgba(255,255,255,.25);
}
.back-btn:active{
  transform:scale(.95);
}
.back-icon{
  font-size:1.2rem;
}

/* ===== MENU GLOW ===== */
.menu-glow{
  position:relative;
  overflow:hidden;
  transition:.3s;
}
.menu-glow::after{
  content:"";
  position:absolute;
  inset:0;
  background:linear-gradient(120deg, transparent, rgba(255,255,255,.35), transparent);
  opacity:0;
  transition:.4s;
}
.menu-glow:hover::after{
  opacity:1;
  animation:glowMove 1.2s linear infinite;
}
@keyframes glowMove{
  from{transform:translateX(-100%)}
  to{transform:translateX(100%)}
}
.menu-glow:active{
  box-shadow:0 0 15px rgba(255,255,255,.6),0 0 35px rgba(34,197,94,.5);
  transform:scale(.97);
}
/* tombol aktif */
.menu-active{
  background:black !important;
  color:white !important;
  box-shadow:0 0 18px rgba(255,255,255,.6),0 0 40px rgba(34,197,94,.6);
}
.price{
  font-weight:bold;
  color:#22c55e;
}

</style>
</head>

<body class="min-h-screen bg-gradient-to-br from-black via-gray-900 to-white text-white">

<header class="p-6 text-center border-b border-gray-700">
<h1 class="text-4xl font-bold">PasirPogorCell</h1>
<p class="text-gray-300">Paket Internet & Top Up Game</p>
</header>

<!-- HOME -->
<section id="home" class="page p-6 max-w-4xl mx-auto grid md:grid-cols-2 gap-6 mt-10">
<button onclick="openInternet(this)" class="card menu-glow">📶 Paket Internet</button>
<button onclick="openGame(this)" class="card menu-glow">🎮 Top Up Game</button>
</section>

<!-- ================= INTERNET ================= -->
<section id="internet" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="backHome()" class="back-btn mb-6">
  <span class="back-icon">←</span> Kembali
</button>

<h2 class="text-2xl font-bold mb-4">Pilih Operator</h2>
<div id="operatorList" class="grid md:grid-cols-3 gap-4 mb-10"></div>

<h3 class="text-xl font-semibold mb-3">Cari Paket Kuota</h3>
<div class="relative mb-4">
<input id="globalPaketInput"
placeholder="Contoh: 1GB, Yellow, Unlimited, Rp10"
class="w-full p-3 pr-12 rounded-xl text-black">
<button onclick="activateGlobalPaketSearch()"
class="absolute right-3 top-1/2 -translate-y-1/2">🔍</button>
</div>
<div id="globalPaketResult" class="space-y-3"></div>
</section>

<section id="operatorDetail" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="openInternet()" class="back-btn mb-6">
  <span class="back-icon">←</span> Kembali
</button>

<h2 id="operatorTitle" class="text-2xl font-bold mb-4"></h2>
<div id="paketList" class="space-y-3"></div>
</section>

<!-- ================= GAME ================= -->
<section id="game" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="backHome()" class="back-btn mb-6">
  <span class="back-icon">←</span> Kembali
</button>

<h2 class="text-2xl font-bold mb-4">Pilih Game</h2>
<div id="gameList" class="grid md:grid-cols-3 gap-4 mb-10"></div>

<h3 class="text-xl font-semibold mb-3">Cari Diamond / UC / Robux</h3>
<div class="relative mb-4">
<input id="globalGameInput"
placeholder="Contoh: 5 Diamond, 15 UC, 250 Robux"
class="w-full p-3 pr-12 rounded-xl text-black">
<button onclick="activateGlobalGameSearch()"
class="absolute right-3 top-1/2 -translate-y-1/2">🔍</button>
</div>
<div id="globalGameResult" class="space-y-3"></div>
</section>

<section id="gameDetail" class="hidden page p-6 max-w-6xl mx-auto">
<button onclick="openGame()" class="back-btn mb-6">
  <span class="back-icon">←</span> Kembali
</button>

<h2 id="gameTitle" class="text-2xl font-bold mb-4"></h2>
<div id="topupList" class="space-y-3"></div>
</section>

<!-- FOOTER -->
<footer class="mt-20 p-6 text-center text-sm bg-black/60 space-y-3">
<h3 class="text-lg font-semibold">Silahkan Kunjungi Gerai PasirPogorCell Di Alamat Berikut</h3>

<p class="text-gray-300">
📍 Pasir Pogor, RT.2/RW.1, Ciparasi,<br>
Kec. Sobang, Kabupaten Lebak, Banten 42280
</p>

<a href="https://wa.me/6283844843020"
class="text-green-400 inline-block">
📞 (+62) 838-4484-3020
</a>

<hr class="border-gray-600 my-3">

<p class="text-gray-400 text-xs">
© 2026 PasirPogorCell<br>
Developed by <span class="font-semibold text-white">
Aden Askolani Fahri
</span>
</p>
</footer>

<script>
/* ================= DATA ================= */
/* ================= OPERATORS & GAMES DATA ================= */
const operators = {
  Indosat: {
    "Paket Internet Harian": [
      "Indosat Kuning 1GB 2 Hari - Rp 9.000",
      "Indosat Kuning 1GB 7 Hari - Rp 10.000",
      "Indosat Kuning 1GB 15 Hari - Rp 12.000",
      "Freedom Mini 3GB 1 Hari - Rp 10.000",
      "Freedom Mini 5GB 2 Hari - Rp 12.000",
      "Freedom Mini 3GB 3 Hari - Rp 15.000",
      "Freedom Mini 2,5GB 5 Hari (Unreg) - Rp 16.000",
      "Freedom Mini 3,5GB 5 Hari - Rp 17.000",
      "Freedom Mini 5GB 5 Hari (Tidak Reg) - Rp 20.000",
      "Freedom Mini 7GB 7 Hari - Rp 26.000",
      "Freedom Mini 15GB 7 Hari - Rp 32.000"
    ],
    "Paket Internet Bulanan": [
      "100MB 24 Jam 30 Hari - Rp 2.000",
      "200MB 24 Jam 30 Hari - Rp 3.000",
      "250MB 24 Jam 30 Hari - Rp 3.500",
      "300MB 24 Jam 30 Hari - Rp 4.000",
      "400MB 24 Jam 30 Hari - Rp 5.000",
      "500MB 24 Jam 30 Hari - Rp 6.000",
      "600MB 24 Jam 30 Hari - Rp 7.000",
      "700MB 24 Jam 30 Hari - Rp 8.000",
      "800MB 24 Jam 30 Hari - Rp 8.500",
      "1GB Semua Jaringan 30 Hari - Rp 9.000",
      "1,5GB Semua Jaringan 30 Hari - Rp 13.000",
      "2GB Semua Jaringan 30 Hari - Rp 16.000",
      "2,5 GB Semua Jaringan 30 Hari - Rp 20.000",
      "3GB Semua Jaringan 30 Hari - Rp 22.000",
      "4GB Semua Jaringan 30 Hari - Rp 28.000",
      "Freedom Internet 3GB 28 Hari - Rp 23.000",
      "Freedom Internet 4GB 28 Hari - Rp 29.000",
      "Freedom Internet 5.5GB 28 Hari - Rp 33.000",
      "Freedom Internet 9GB 28 Hari - Rp 44.000",
      "Freedom Internet 13GB 28 Hari - Rp 57.000",
      "Freedom Internet 16GB 28 Hari - Rp 69.000",
      "Freedom Internet 20GB 28 Hari - Rp 71.000",
      "Freedom Internet 25GB 28 Hari - Rp 83.000",
      "Freedom Internet 30GB 28 Hari - Rp 97.000",
      "Freedom Internet 42GB 28 Hari - Rp 105.000",
      "Freedom Internet Sensasi 50GB 28 Hari - Rp 106.000",
      "Freedom Internet Sensasi 70GB 28 Hari - Rp 127.000",
      "Freedom Internet Sensasi 150 GB 28 Hari - Rp 160.000",
      "Freedom Internet Sensasi 200GB 28 Hari - Rp 201.000"
    ],
    "Paket Unlimited": [
      "1GB + 2GB + Aplikasi Unlimited 6 Hari - Rp 20.000",
      "1GB Semua + 4,5GB + Aplikasi Unlimited 28 Hari - Rp 36.000",
      "2GB Semua + 7,5 s/d 8GB + Aplikasi Unli 28 Hari - Rp 59.000",
      "3GB Semua + 15 s/d 17GB + Aplikasi Tanpa Batas 28 Hari - Rp 83.000",
      "7GB Semua + 28GB + Aplikasi Unlimited 28 Hari - Rp 108.000",
      "10GB Semua + 35GB + Aplikasi Tanpa Batas 28 Hari - Rp 120.000",
      "15GB All + 25GB + Unlimited Aplikasi, Telp & SMS 28 Hari - Rp 131.000",
      "Unlimited (90GB All + Unl App + Telp + SMS) 24 jam 28 Hari - Rp 162.000"
    ]
  },

  Axis: {
    "Paket Internet Harian": [
      "Mini 1,5GB + Bonus Aigo 1 Hari - Rp 8.000",
      "Mini Axis 2,5GB + Bonus Aigo 1 Hari - Rp 10.000",
      "Mini Axis 2GB + Bonus Aigo 3 Hari - Rp 12.000",
      "Mini Axis 2,5GB + Bonus Aigo 3 Hari - Rp 13.000",
      "Mini Axis 3GB + Bonus Aigo 3 Hari - Rp 13.000",
      "Mini Axis 4,5GB + Bonus Aigo 3 Hari - Rp 15.000",
      "Mini Axis 9GB + Bonus Aigo 3 Hari - Rp 17.000",
      "Aigo Kuota Mini 1.5GB + Bonus 1GB 1 Hari Rp8.000"
    ],
    "Paket Internet Per Jam": [
      "Axis Paket Data Warnet 800 MB (1 Jam) - Rp 3.000",
      "Paket Data Axis Warnet Unlimited 1 Jam - Rp 4.000",
      "Axis Paket Data Warnet 1,5 GB (2 Jam) - Rp 4.000",
      "Axis Paket Data Warnet 3 GB (3 Jam) - Rp 5.000",
      "Paket Data Axis Warnet Unlimited 3 Jam - Rp 6.000",
      "Axis Paket Data Warnet 3 GB (6 Jam) - Rp 7.000",
      "Paket Data Axis Warnet Unlimited 24 Jam - Rp 10.000"
    ],
    "Paket Internet Bulanan": [
      "Axis Data 1GB Semua 30 Hari - Rp 10.000",
      "Bronet 2GB + Bonus Aigo 30 Hari - Rp 18.000",
      "Bronet 3GB + Bonus Aigo 30 Hari - Rp 21.000",
      "Bronet 6GB + Bonus Aigo 30 Hari - Rp 32.000",
      "Bronet 8GB + Bonus Aigo 30 Hari - Rp 41.000",
      "Bronet 14GB + Bonus Aigo 30 Hari - Rp 62.000",
      "Axis Data Bronet 16GB Semua 30 Hari - Rp 74.000",
      "Bronet 20GB + Bonus Aigo 30 Hari - Rp 74.000",
      "Bronet 30GB + Bonus Aigo 30 Hari - Rp 91.000",
      "Bronet 2GB Semua 24 Jam 60 Hari - Rp 32.000",
      "Bronet 3GB Semua 24 Jam 60 Hari - Rp 41.000",
      "Bronet 5GB Semua 24 Jam 60 Hari - Rp 58.000",
      "Bronet 8GB Semua 24 Jam 60 Hari - Rp 78.000",
      "Bronet 10GB Semua 24 Jam 60 Hari - Rp 89.000",
      "Bronet 12GB Semua 24 Jam 60 Hari - Rp 100.000",
      "Bronet 35GB + Bonus Aigo 60 Hari - Rp 110.000",
      "Bronet 16GB Semua 24 Jam 60 Hari - Rp 119.000",
      "Bronet 75GB + Bonus Aigo 60 Hari - Rp 171.000"
    ],
    "Paket Kuota Games": [
      "Kuota Games Hanya 1GB 30 Hari - Rp 7.000",
      "500MB Semua + 500MB Kuota Game 30 Hari - Rp 9.000",
      "Kuota Games Hanya 2GB 30 Hari - Rp 11.000",
      "1GB Semua + 1GB Kuota Game 30 Hari - Rp 14.000",
      "1,5GB All + 1,5GB Kuota Game 30 Hari - Rp 17.000",
      "1GB Semua Data + 1GB 4G + 2GB Game 30 Hari - Rp 21.000",
      "2GB Semua + 2GB Kuota Game 30 Hari - Rp 23.000",
      "1GB Semua Data + 3GB 4G + 4GB Game 30 Hari - Rp 35.000"
    ]
  },

  Telkomsel: {
    "Paket Internet Harian": [
      "Mini Data 1GB AII 1 Hari - Rp 10.000",
      "Mini Data 500MB AIl 3 Hari - Rp 10.000",
      "(Non-Pamasuka) Mini Data 1,5GB Semua 3 Hari - Rp 13.000",
      "Mini Data 1GB AIl 3 Hari - Rp 13.000",
      "Mini Data 2,5GB Semua 5 Hari - Rp 15.000",
      "Mini Data 2GB AIl 3 Hari - Rp 15.000",
      "Mini Data 2.5GB - 3GB Semua 5 Hari - Rp 16.000",
      "Mini Data 4GB AII 1 Hari - Rp 12.550",
      "Mini Data 6GB AIl 1 Hari - Rp 23.000",
      "Mini Data 5GB Semua 1 Hari - Rp 25.000",
      "Mini Data 3GB Semua 3 Hari - Rp 27.000",
      "Mini Data 5GB Semua 3 Hari - Rp 34.000",
      "Mini Data 8GB AII 3 Hari - Rp 40.000",
      "Mini Data 7GB AII 3 Hari - Rp 50.000",
      "Mini Data 17GB AII 3 Hari - Rp 64.000",
      "Mini Data 15GB AIl 3 Hari - Rp 66.000",
      "Mini Data 20GB AIl 3 Hari - Rp 74.000",
      "Mini Data 10GB AIl 3 Hari - Rp 78.000"
    ],
    "Paket Internet Mingguan": [
      "Tsel Mini Data 50MB 7 Hari - Rp 4.000",
      "Tsel Mini Data 100MB 7 Hari - Rp 7.000",
      "Tsel Mini Data 250MB 7 Hari - Rp 8.000",
      "Tsel Mini Data 500MB 7 Hari - Rp 10.000",
      "Mini Data 500MB Semua 7 Hari - Rp 11.000",
      "Mini Data 1GB AII 7 Hari - Rp 13.000",
      "1GB Semua Jaringan 30 Hari - Rp 15.000",
      "Tsel Mini Data 750MB 7 Hari - Rp 18.000",
      "Mini Data 2GB AIl 7 Hari - Rp 19.000",
      "Mini Data 3GB Semua 7 Hari - Rp 24.000",
      "Mini Data 2GB Semua 14 Hari - Rp 25.000",
      "Mini Data 5GB Semua 7 Hari - Rp 29.000",
      "Mini Data 7GB Semua 7 Hari - Rp 30.000",
      "Mini Data 17GB Semua 7 Hari - Rp 80.000"
    ],
    "Data Mini Jabo - Banten": [
      "Paket Data 1,5GB 3 Hari - Rp 11.000",
      "Paket Data 2,5GB 5 Hari - Rp 14.000",
      "Paket Data 3GB 3 Hari - Rp 15.000",
      "Paket Data 3GB 5 Hari - Rp 16.000",
      "Paket Data 3,5GB 7 Hari - Rp 22.000",
      "Paket Data 4,5GB 5 Hari - Rp 23.000",
      "Paket Data 5,5GB 5 Hari - Rp 27.000",
      "Paket Data 5GB 7 Hari - Rp 29.000",
      "Paket Data 7GB 7 Hari - Rp 30.000",
      "Data 0,5GB Semua+ 1,5GB Lokal + 2GB OMG 30 Hari - Rp 36.000",
      "Paket Data 10GB 7 Hari - Rp 39.000",
      "Paket Data 12GB 7 Hari - Rp 44.000",
      "Data 1,25GB Semua + 3,75GB Lokal + 2GB OMG 30 Hari - Rp 50.000",
      "Data 2GB Semua + 6GB Lokal + 2GB OMG 30 Hari - Rp 65.000",
      "Data 3GB Semua + 9GB Lokal + 2GB OMG 30 Hari - Rp 74.000",
      "Data 4,5GB Semua + 13,5GB Lokal + 2GB OMG 30 Hari - Rp 85.000",
      "Data 5GB+ 37GB Lokal Jabo - Jabar 30 Hari - Rp 101.000",
      "Data 6GB + 54GB Lokal Jabo - Jabar 30 Hari - Rp 141.000",
      "Data 9GB + 71GB Lokal Jabo - Jabar 30 Hari - Rp 170.000"
    ]
  },

  ByU: {
    "Paket Data ByU": [
      "1GB Semua + Bebas Tiktok 500MB/ Hari 1 Hari - Rp 8.000",
      "Kuota 2GB Semua 1 Hari - Rp 10.000",
      "2GB Semua + Bebas Tiktok 500MB/ Hari 3 Hari - Rp 12.000",
      "10GB Semua + Bebas Tiktok 500MB/ Hari 1 Hari - Rp 14.000",
      "Kuota 2,5GB Semua 5 Hari - Rp 14.000",
      "Kuota 3GB Semua 7 Hari - Rp 16.000",
      "ByU Yang Bikin Deket 3GB - 1 Hari - Rp 21.000",
      "Kuota 5GB Semua 7 Hari - Rp 21.000"
    ]
  },

  Tri: {
    "Tri Paket Data Bulanan": [
      "Tri All Jaringan 3GB 30 Hari Rp20.000"
    ],
    "Tri Paket Data Harian": [
      "Tri Data Mini 1GB + 1.5GB Malam 1 Hari Rp10.000"
    ]
  },

  XL: {
    "XL Data Harian": [
      "XL Data Blue 1GB All Jaringan 2 Hari Rp8.000"
    ],
    "XL Data Bulanan": [
      "XL Data Reguler 5GB 30 Hari Rp35.000"
    ]
  }
};

const games={
"Mobile Legends": [
  "3 Mobile Legend Diamonds Rp 3.000",
  "19 (17+2) Mobile Legend Diamonds Rp 10.000",   
  "28 (25+3) Mobile Legend Diamonds Rp 11.000",   
  "36 (33+3) Mobile Legend Diamonds Rp 13.000",
  "44 (40+4) Mobile Legend Diamonds Rp 15.000",  
  "56 (51+5) Mobile Legend Diamonds Rp 19.000",  
  "59 (53+6) Mobile Legend Diamonds Rp 20.000",
  "74 (69+5) Mobile Legend Diamonds Rp 23.000",  
  "85 (77+8) Mobile Legend Diamonds Rp 27.000",  
  "86 (78+8) Mobile Legend Diamonds Rp 27.000",  
  "100 Mobile Legend Diamonds Rp 31.000",
  "1X Weekly Diamond Pass 220 (80+20/Day) Rp 31.000",  
  "112(102+10) Mobile Legend Diamonds Rp 34.000",  
  "144(130+14) Mobile Legend Diamonds Rp 42.000",
  "170 (154+16) Mobile Legend Diamonds Rp 50.000",  
  "172 (156+16) Mobile Legend Diamonds Rp 50.000",  
  "185 (167+18) Mobile Legend Diamonds Rp 54.000",
  "2X Weekly Diamond Tickets 440 (80+20/Day) Rp 60.000",  
  "222(200+22) Mobile Legend Diamonds Rp 63.000",  
  "229(207+22) Mobile Legend Diamonds Rp 66.000",
  "240 (217+23) Mobile Legend Diamonds Rp 69.000",  
  "257 (234+23) Mobile Legend Diamonds Rp 72.000",
  "Mobile Legend Pass Coupon Rp 76000",  
  "278(251+27) Mobile Legend Diamonds Rp 79.000",
  "284 (254+30) Mobile Legend Diamonds Rp 80.000", 
  "296 (256+40) Mobile Legend Diamonds Rp 82.000", 
  "301 (261+40) Mobile Legend Diamonds Rp 84.000",
  "Starlight Membership Rp 85.000",  
  "3X Weekly Diamond Pass 660 (80+20/Day) Rp 87.000",  
  "344(312+32) Mobile Legend Diamonds Rp 96.000",
  "345 (301+44) Mobile Legend Diamonds Rp 97.000",  
  "355 (309+46) Mobile Legend Diamonds Rp 100.000",  
  "374 (326+48) Mobile Legend Diamonds Rp 106.000",
  "381(333+48) Mobile Legend Diamonds Rp 107.000",  
  "384 Mobile Legend Diamonds Rp 110.000",  
  "408(367+41) Mobile Legend Diamonds Rp 114.000",
  "4X Weekly Diamond Pass 880 (80+20/Day) Rp 15.000",  
  "429(390+39) Mobile Legend Diamonds Rp 118.000",  
  "425(373+52) Mobile Legend Diamonds Rp 120.000",
  "448 Mobile Legend Diamonds Rp 137.000", 
  "460 Mobile Legend Diamonds Rp 140.000", 
  "514 (468+46) Mobile Legend Diamonds Rp 142.000",
  "5X Weekly Diamond Tickets 1100 (80+20/Day) Rp 143.000",  
  "522(471+51) Mobile Legend Diamonds Rp 146.000",  
  "500 Mobile Legend Diamonds Rp 150.000",
  "Mobile Legend Twilight Pass Rp 155.000",  
  "568 (503+65) Mobile Legend Diamonds Rp 155.000",  
  "601 (533+68) Mobile Legend Diamonds Rp 165.000",
  "642 Mobile Legend Diamonds Rp 185.000",  
  "706 (625+81) Mobile Legend Diamonds Rp 200.000",  
  "712 (633+79) Mobile Legend Diamonds Rp 201.000",
  "717 (638+79) Mobile Legend Diamonds Rp 203.000",  
  "Starlight Plus Member Rp 220.000",  
  "875 (774+101) Mobile Legend Diamonds Rp 240.000",
  "965 (856+109) Mobile Legend Diamonds Rp 264.000",  
  "963 (859+104) Mobile Legend Diamonds Rp 265.000",  
  "977 (867+110) Mobile Legend Diamonds Rp 268.000"
],
"Free Fire":["5 Diamond Rp2.000"],
"PUBG Mobile":["15 UC Rp11.000"],
"Call Of Duty Mobile":["63 CP Rp12.000"],
"Honor Of Kings":["16 Token Rp5.000"],
"Genshin Impact":["60 Crystal Rp14.000"],
"Roblox":["250 Robux Rp50.000"]
};

let currentOperator="", currentGame="", currentPackage="";

/* ================= NAV ================= */
function hideAll(){document.querySelectorAll("section").forEach(s=>s.classList.add("hidden"))}
function backHome(){
  hideAll();
  document.getElementById("home").classList.remove("hidden");
  clearActive();
}

function clearActive(){
  document.querySelectorAll(".menu-active").forEach(b=>b.classList.remove("menu-active"));
  document.querySelectorAll(".package-active").forEach(b=>b.classList.remove("package-active"));
}

/* ================= INTERNET ================= */
function openInternet(btn){
  clearActive();
  if(btn) btn.classList.add("menu-active");
  hideAll();
  document.getElementById("internet").classList.remove("hidden");
  renderOperators();
}
function renderOperators(){
  const operatorList = document.getElementById("operatorList");
  operatorList.innerHTML="";
  Object.keys(operators).forEach(op=>{
    operatorList.innerHTML+=`<button class="card menu-glow" onclick="openOperator('${op}', this)">${op}</button>`;
  });
}
function openOperator(op, btn){
  currentOperator = op;
  hideAll();
  document.getElementById("operatorDetail").classList.remove("hidden");
  document.getElementById("operatorTitle").innerText = op;
  const paketList = document.getElementById("paketList");
  paketList.innerHTML="";
  Object.keys(operators[op]).forEach(cat=>{
    const wrapper = document.createElement("div");
    wrapper.className = "mb-6";
    wrapper.innerHTML = `<h3 class="text-lg font-semibold mb-3 text-gray-200">${cat}</h3>
      <div class="space-y-3">
      ${operators[op][cat].map((p,index)=>`<div class="card package-glow" onclick="highlightPrice(this)">${p.replace(/Rp\s?[\d.,]+/g,'<span class="price">$&</span>')}</div>`).join("")}
      </div>`;
    paketList.appendChild(wrapper);
  });
  // Aktifkan menu utama
  clearActive();
  if(btn) btn.classList.add("menu-active");
}

/* ================= GAME ================= */
function openGame(btn){
  clearActive();
  if(btn) btn.classList.add("menu-active");
  hideAll();
  document.getElementById("game").classList.remove("hidden");
  renderGames();
}
function renderGames(){
  const gameList = document.getElementById("gameList");
  gameList.innerHTML="";
  Object.keys(games).forEach(g=>{
    gameList.innerHTML+=`<button class="card menu-glow" onclick="openGameDetail('${g}', this)">${g}</button>`;
  });
}
function openGameDetail(g, btn){
  currentGame=g;
  hideAll();
  document.getElementById("gameDetail").classList.remove("hidden");
  document.getElementById("gameTitle").innerText=g;
  const topupList = document.getElementById("topupList");
  topupList.innerHTML="";
  games[g].forEach(t=>{
    topupList.innerHTML+=`<div class="card package-glow" onclick="highlightPrice(this)">${t.replace(/Rp\s?[\d.,]+/g,'<span class="price">$&</span>')}</div>`;
  });
  // Aktifkan menu utama
  clearActive();
  if(btn) btn.classList.add("menu-active");
}

/* ================= HIGHLIGHT PRICE ================= */
function highlightPrice(el){
  // Hapus highlight sebelumnya
  document.querySelectorAll(".package-active").forEach(b=>b.classList.remove("package-active"));
  // Tambahkan highlight pada klik
  el.classList.add("package-active");
  // Glow harga
  const price = el.querySelector(".price");
  if(price){
    // animasi cepat
    price.style.transition="0.3s";
    price.style.color="#22c55e";
    price.style.textShadow="0 0 10px #22c55e,0 0 20px #22c55e";
  }
}

/* ================= AKTIFKAN GLOBAL SEARCH ================= */
function activateGlobalPaketSearch(){ /* bisa kamu tambahkan logika filter */ }
function activateGlobalGameSearch(){ /* bisa kamu tambahkan logika filter */ }
</script>
