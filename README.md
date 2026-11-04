<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Apple 🍎</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;text-align:center;
 font-family:Georgia,serif;color:#793451;
 background:linear-gradient(135deg,#ffe4ed,#fff4ed,#ffd9e8);
 min-height:100vh;overflow-x:hidden;
}
section{
 background:#ffffffdc;
 margin:25px auto;padding:30px 20px;
 width:92%;max-width:750px;
 border-radius:25px;
 box-shadow:0 8px 30px #d66a8a30;
}
h1{font-size:clamp(2rem,7vw,3.5rem);color:#d83d79}
h2{color:#d83d79}
p{line-height:1.7;font-size:18px}
button{
 background:#ed6595;color:white;border:0;
 padding:14px 25px;border-radius:30px;
 font-size:16px;cursor:pointer;margin:10px;
}
input{
 padding:14px;border:2px solid pink;
 border-radius:12px;font-size:18px;
 text-align:center;max-width:90%;
}
.hidden{display:none!important}
.timer{display:flex;justify-content:center;gap:10px;flex-wrap:wrap}
.time{
 background:#ffe1eb;padding:15px;
 border-radius:15px;min-width:75px;
}
.time b{display:block;font-size:27px;color:#d83d79}
.cake{font-size:100px;animation:bounce 1s infinite alternate}
@keyframes bounce{to{transform:translateY(-12px)}}
.gallery{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.photo{
 background:#ffe4ed;border-radius:18px;
 padding:35px 5px;font-size:45px;
}
.photo small{display:block;font-size:14px}
.letter{
 background:#fff4e8;padding:25px;
 border-radius:18px;line-height:2;text-align:left;
}
.heart{
 position:fixed;bottom:-30px;
 animation:float 6s linear forwards;
 pointer-events:none;
}
@keyframes float{to{transform:translateY(-110vh);opacity:0}}
</style>
</head>
<body>

<section id="countdown">
<h1>Something Special Is Coming 💗</h1>
<h2>For Apple 🍎</h2>
<p>Your birthday surprise is waiting!</p>
<div class="timer">
<div class="time"><b id="d">00</b>Days</div>
<div class="time"><b id="h">00</b>Hours</div>
<div class="time"><b id="m">00</b>Minutes</div>
<div class="time"><b id="s">00</b>Seconds</div>
</div>
<p>Midnight magic begins on 9 November! 🎂</p>
</section>

<section id="lock" class="hidden">
<h1>🔐 Secret Surprise</h1>
<p>Apple, enter your special password!</p>
<input id="pass" type="password" placeholder="Secret password">
<br>
<button onclick="unlock()">Unlock My Surprise ❤️</button>
<p id="error"></p>
</section>

<div id="birthday" class="hidden">

<section>
<h1>Happy Birthday Apple! 🍎</h1>
<p>Today is your special day! May your life always be filled with happiness, love and beautiful memories. 💗</p>
<button onclick="music()" id="musicBtn">🎵 Play Birthday Music</button>
</section>

<section>
<h2>Your Birthday Cake 🎂</h2>
<div class="cake">🎂</div>
<p>Close your eyes and make a wish! ✨</p>
<button onclick="confetti()">Make a Wish 🎉</button>
</section>

<section>
<h2>Beautiful Memories 📸</h2>
<p>Temporary pictures for now. Your real photos can be added later!</p>
<div class="gallery">
<div class="photo">🌷<small>Sweet Memories</small></div>
<div class="photo">🧸<small>Special Moments</small></div>
<div class="photo">🌸<small>Beautiful Smile</small></div>
<div class="photo">💝<small>Forever Memories</small></div>
</div>
</section>

<section>
<h2>A Message For You ❤️</h2>
<p>You are special, and you deserve all the beautiful things life has to offer. May every day bring you a new reason to smile.</p>
<p>Keep shining, Apple! 🍎💕</p>
</section>

<section>
<h2>A Little Surprise Letter 💌</h2>
<button onclick="document.getElementById('letter').classList.toggle('hidden')">Open Your Letter</button>
<div id="letter" class="letter hidden">
Dear Apple ❤️,

Happy Birthday!

I hope this little surprise brings a big smile to your face.

May your dreams come true, your heart stay happy, and your life be full of unforgettable moments.

You deserve all the happiness in the world.

Happy Birthday once again! 🎂

With lots of love 💗
</div>
</section>

</div>

<script>
// Countdown: 9 November 2026 at 12:00 AM
const target=new Date(2026,10,9,0,0,0);

function timer(){
 let diff=target-new Date();

 if(diff<=0){
 document.getElementById("countdown").classList.add("hidden");
 document.getElementById("lock").classList.remove("hidden");
 return;
 }

 document.getElementById("d").textContent=Math.floor(diff/86400000);
 document.getElementById("h").textContent=Math.floor(diff%86400000/3600000);
 document.getElementById("m").textContent=Math.floor(diff%3600000/60000);
 document.getElementById("s").textContent=Math.floor(diff%60000/1000);
}
timer();
setInterval(timer,1000);

function unlock(){
 let p=document.getElementById("pass").value.trim().toUpperCase();

 if(p==="APPLEENA"){
 document.getElementById("lock").classList.add("hidden");
 document.getElementById("birthday").classList.remove("hidden");
 hearts();
 confetti();
 }else{
 document.getElementById("error").textContent="Wrong password! Try again 💗";
 }
}

document.getElementById("pass").addEventListener("keydown",e=>{
 if(e.key==="Enter")unlock();
});

// Original little birthday melody
let audio=null,playing=false,musicTimer;
function music(){
 const btn=document.getElementById("musicBtn");

 if(playing){
 clearInterval(musicTimer);
 playing=false;
 btn.textContent="🎵 Play Birthday Music";
 return;
 }

 audio=audio||new(window.AudioContext||window.webkitAudioContext)();
 audio.resume();
 let notes=[523,587,659,523,698,659,587,523];
 let i=0;

 function play(){
 let osc=audio.createOscillator();
 let gain=audio.createGain();
 osc.frequency.value=notes[i++%notes.length];
 gain.gain.setValueAtTime(.1,audio.currentTime);
 gain.gain.exponentialRampToValueAtTime(.001,audio.currentTime+.35);
 osc.connect(gain);gain.connect(audio.destination);
 osc.start();osc.stop(audio.currentTime+.4);
 }
 play();
 musicTimer=setInterval(play,450);
 playing=true;
 btn.textContent="⏸ Pause Music";
}

function hearts(){
 setInterval(()=>{
 let heart=document.createElement("div");
 heart.className="heart";
 heart.textContent=["💗","💕","💖","✨","🌸"][Math.floor(Math.random()*5)];
 heart.style.left=Math.random()*100+"vw";
 heart.style.fontSize="25px";
 document.body.appendChild(heart);
 setTimeout(()=>heart.remove(),6000);
 },500);
}

function confetti(){
 for(let i=0;i<70;i++){
 let el=document.createElement("div");
 el.className="heart";
 el.textContent=["🎉","✨","💗","🎊"][Math.floor(Math.random()*4)];
 el.style.left=Math.random()*100+"vw";
 el.style.bottom="-20px";
 el.style.animationDuration=(3+Math.random()*4)+"s";
 document.body.appendChild(el);
 setTimeout(()=>el.remove(),7000);
 }
}
</script>
</body>
</html>
</body>
</html>
