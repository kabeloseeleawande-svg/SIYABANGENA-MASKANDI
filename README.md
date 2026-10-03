<!DOCTYPE html>
<html lang="zu">
<head>
<meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KABZA AI MUSIC - Mzansi AI Music Creation</title>
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://fonts.googleapis.com/css2?family=Manrope:wght@800&family=Noto+Sans:wght@400;600&display=swap" rel="stylesheet">
<style>body{font-family:'Noto Sans',sans-serif}h1,h2,h3{font-family:'Manrope',sans-serif}</style>
</head>
<body class="bg-black text-white min-h-screen">
<header class="flex justify-between items-center p-4 border-b border-zinc-900 sticky top-0 bg-black/90 backdrop-blur z-10">
<h1 class="font-black text-yellow-400">KABZA AI MUSIC</h1>
<div class="flex gap-2 items-center">
<span id="creditBadge" class="bg-zinc-800 px-3 py-1 rounded-full text-xs">500 Credits</span>
<span id="dailyBadge" class="bg-yellow-400 text-black px-3 py-1 rounded-full text-xs font-bold">30/30 namhlanje</span>
</div>
</header>
<main class="max-w-lg mx-auto p-5">
<div class="text-center mt-4">
<h2 class="text-4xl font-black leading-tight">Dala Ingoma<br><span class="text-yellow-400">YaseMzansi</span> Nge-AI</h2>
<p class="text-zinc-400 text-sm mt-3">Maskandi • Gospel • Isicathamiya • Amapiano • Gqom • Afro House</p>
</div>
<div class="grid grid-cols-3 gap-2 mt-6 text-xs">
<button onclick="setStyle(this,'Maskandi')" class="genre bg-zinc-900 border border-zinc-800 p-3 rounded-xl">🇿🇦 Maskandi</button>
<button onclick="setStyle(this,'Gospel')" class="genre bg-zinc-900 border border-zinc-800 p-3 rounded-xl">🙏 Gospel</button>
<button onclick="setStyle(this,'Isicathamiya')" class="genre bg-zinc-900 border border-zinc-800 p-3 rounded-xl">🎤 Isicathamiya</button>
<button onclick="setStyle(this,'Amapiano')" class="genre bg-zinc-900 border border-zinc-800 p-3 rounded-xl">🔥 Amapiano</button>
<button onclick="setStyle(this,'Gqom')" class="genre bg-zinc-900 border border-zinc-800 p-3 rounded-xl">🎶 Gqom</button>
<button onclick="setStyle(this,'Afro House')" class="genre bg-zinc-900 border border-zinc-800 p-3 rounded-xl">🥁 Afro House</button>
</div>
<textarea id="prompt" class="w-full bg-zinc-900 mt-6 p-4 rounded-2xl h-28 border border-zinc-800 text-sm" placeholder="Bhala: 'Maskandi esheshayo, isiginci esibukhali, indoda ecula ngothando, 120 BPM'"></textarea>
<p id="selectedStyle" class="text-xs text-yellow-400 mt-2">Isitayela: Maskandi</p>
<button onclick="generateSong()" class="w-full mt-4 bg-yellow-400 text-black py-4 rounded-full font-black text-sm">🎵 Dala Ingoma (30 Credits)</button>
<div id="result" class="hidden mt-6 bg-zinc-900 p-4 rounded-2xl border border-zinc-800">
<h3 class="font-bold text-sm">✅ Ingoma Yakho Isilungele!</h3>
<p id="resultText" class="text-xs text-zinc-400 mt-2"></p>
<audio controls class="w-full mt-3"><source src="" type="audio/mpeg"></audio>
<button class="w-full mt-3 bg-white text-black py-3 rounded-full font-bold text-sm">Landa MP3 (R50)</button>
</div>
<div id="paywall" class="hidden mt-6 bg-gradient-to-br from-yellow-400 to-orange-500 p-5 rounded-2xl text-black">
<h3 class="font-black">Ama-Credits Aphelile!</h3>
<p class="text-sm mt-1">Thuthukisa ukuze uqhubeke udala.</p>
<div class="grid grid-cols-2 gap-3 mt-4">
<div class="bg-black text-white p-4 rounded-xl text-center"><p class="font-black">R180</p><p class="text-xs">Ngenyanga</p><button class="bg-yellow-400 text-black w-full mt-2 py-2 rounded-full text-xs font-bold">Khetha</button></div>
<div class="bg-black text-white p-4 rounded-xl text-center border-2 border-yellow-400"><p class="font-black">R500</p><p class="text-xs">Ngonyaka - BEST</p><button class="bg-yellow-400 text-black w-full mt-2 py-2 rounded-full text-xs font-bold">Khetha</button></div>
</div>
</div>
<p class="text-center text-[10px] text-zinc-600 mt-10">500 Credits MAHHALA • 30 ngosuku • Yenziwe eKwaDabeka, KZN 🇿🇦</p>
</main>
<script>
let style='Maskandi';
let credits=parseInt(localStorage.getItem('kabza_credits')||'500');
let dailyUsed=parseInt(localStorage.getItem('kabza_daily_used')||'0');
let dailyDate=localStorage.getItem('kabza_daily_date')||new Date().toDateString();
if(dailyDate!==new Date().toDateString()){dailyUsed=0;dailyDate=new Date().toDateString();localStorage.setItem('kabza_daily_date',dailyDate);localStorage.setItem('kabza_daily_used','0');}
function updateUI(){document.getElementById('creditBadge').innerText=credits+' Credits';document.getElementById('dailyBadge').innerText=(30-dailyUsed)+'/30 namhlanje';localStorage.setItem('kabza_credits',credits);localStorage.setItem('kabza_daily_used',dailyUsed);}
function setStyle(el,s){style=s;document.querySelectorAll('.genre').forEach(b=>b.classList.remove('border-yellow-400'));el.classList.add('border-yellow-400');document.getElementById('selectedStyle').innerText='Isitayela: '+s;}
function generateSong(){
 if(credits<30){document.getElementById('paywall').classList.remove('hidden');return;}
 if(dailyUsed>=30){alert('Ususebenzise u-30 namhlanje. Buya kusasa! Uma ufuna okungapheli, thuthukisa ngo R180.');document.getElementById('paywall').classList.remove('hidden');return;}
 let p=document.getElementById('prompt').value||'Ingoma enhle';
 credits-=30;dailyUsed+=30;updateUI();
 document.getElementById('result').classList.remove('hidden');
 document.getElementById('resultText').innerText=style+' | "'+p+'" | Yenziwe nge-AI. Lena i-demo, uma uxhuma i-Suno API izodala i-MP3 yangempela.';
 window.scrollTo(0,document.body.scrollHeight);
}
updateUI();
</script>
</body>
</html>
