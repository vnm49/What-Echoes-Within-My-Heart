<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>What Echoes Within My Heart</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
@import url('https://fonts.googleapis.com/css2?family=Great+Vibes&family=Allura&display=swap');
*{box-sizing:border-box;margin:0;padding:0;}
body{
    min-height:100vh;
    background:#fff;
    display:flex;
    justify-content:center;
    align-items:center;
    perspective:2000px;
    overflow:hidden;
    font-family:'Allura',cursive;
}

/* Candle flicker glow */
.flicker{
    position:fixed;inset:0;
    pointer-events:none;
    box-shadow:0 0 120px 35px rgba(255,200,220,0.2) inset;
    animation:flickerGlow 2s infinite alternate;
}
@keyframes flickerGlow{
    0%{box-shadow:0 0 120px 35px rgba(255,200,220,0.2) inset;}
    50%{box-shadow:0 0 130px 40px rgba(255,180,200,0.25) inset;}
    100%{box-shadow:0 0 110px 30px rgba(255,200,220,0.15) inset;}
}

/* Floating hearts */
.heart{
    position:absolute;width:20px;height:20px;background:red;
    transform:rotate(45deg);border-radius:0 50% 50% 50%;
    animation:floatHeart linear infinite;
}
.heart::before,.heart::after{
    content:"";position:absolute;width:20px;height:20px;background:red;border-radius:50%;
}
.heart::before{top:-10px;left:0;}
.heart::after{left:-10px;top:0;}
@keyframes floatHeart{
    0%{transform:translateY(0) rotate(45deg);opacity:1;}
    100%{transform:translateY(-700px) rotate(45deg);opacity:0;}
}

/* Envelope */
.envelope{
    width:90%;
    max-width:460px;height:300px;
    position:relative;
    transform-style:preserve-3d;cursor:pointer;
    animation:float 4s ease-in-out infinite;z-index:10;
}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-10px)}}
.env-body{
    position:absolute;inset:0;
    background:linear-gradient(145deg,#f9f1e6,#e7d7c3);
    border-radius:16px;
    box-shadow:0 35px 90px rgba(0,0,0,.3), inset 0 0 60px rgba(255,255,255,.7);
}
.env-body::before{
    content:"";position:absolute;inset:16px;
    border:6px double rgba(255,255,255,.9);border-radius:12px;
}
.flap{
    position:absolute;inset:0;
    background:linear-gradient(145deg,#f3e7d5,#d8c2aa);
    clip-path:polygon(0 0,50% 58%,100% 0);
    border-radius:16px 16px 0 0;
    transform-origin:top;transition:1.2s cubic-bezier(.19,1,.22,1);
}
.seal{
    width:60px;height:60px;
    background:radial-gradient(circle,#a1121f,#5c000b);
    border-radius:50%;
    position:absolute;bottom:18px;left:50%;transform:translateX(-50%);
    box-shadow:0 8px 25px rgba(0,0,0,.5);transition:1s;
    z-index:5;
}
.seal::after{
    content:"❤";position:absolute;inset:0;display:flex;justify-content:center;align-items:center;
    font-size:26px;color:#ffd9df;
}
.env-text{
    position:absolute;top:18px;width:100%;text-align:center;
    font-family:'Great Vibes',cursive;font-size:6vw;color:#6a3a2a;
}

/* Letter */
.letter{
    display:none;
    width:90%;
    max-width:400px;
    max-height:60vh;
    background:linear-gradient(135deg,#fff,#fffaf4);
    padding:30px;
    border-radius:20px;
    box-shadow:0 40px 110px rgba(0,0,0,.25), inset 0 0 80px rgba(255,200,160,.3);
    font-size:18px;
    color:#444;
    line-height:1.8;
    position:relative;
    z-index:20;
    transform:scale(0.8);
    opacity:0;
    transition: transform 1s ease, opacity 1s ease;
    overflow-y:auto;
}
.letter.show{
    display:block;
    transform:scale(1);
    opacity:1;
}
.title{font-family:'Great Vibes',cursive;font-size:28px;text-align:center;color:#d6336c;margin-bottom:20px;}

/* Music Player / Vinyl */
.music-box{
    display:none;
    position:fixed;inset:0;
    background:rgba(255,255,255,.95);
    justify-content:center;align-items:center;
    flex-direction:column;
    gap:30px;
    padding:20px;
}
.album-bg{
    width:220px;height:220px;
    background:url('https://lh3.googleusercontent.com/q44lQH1iSZgZRt9rzaiQcItLvSk5r9LIgzkpIRFWU2CvKT4__-2NbUWpkvfllglHc8YGNMUk98m92X0=w544-h544-l90-rj') center/cover;
    border-radius:14px;display:flex;justify-content:center;align-items:center;box-shadow:0 25px 70px rgba(0,0,0,.45);
}
.vinyl{
    width:160px;height:160px;
    border-radius:50%;
    background:radial-gradient(circle,#000 0%,#111 45%,#000 70%,#222 100%);
    animation:spin 2.5s linear infinite;
    animation-play-state:paused;
    position:relative;box-shadow:0 0 20px rgba(0,0,0,.8);
}
.vinyl::before{
    content:"";
    position:absolute;
    inset:30px;
    background:url('https://lh3.googleusercontent.com/q44lQH1iSZgZRt9rzaiQcItLvSk5r9LIgzkpIRFWU2CvKT4__-2NbUWpkvfllglHc8YGNMUk98m92X0=w544-h544-l90-rj') center/cover no-repeat;
    border-radius:50%;
}
.vinyl::after{
    content:"";
    width:10px;height:10px;background:white;border-radius:50%;position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);
}
@keyframes spin{from{transform:rotate(0deg)}to{transform:rotate(360deg);}}

/* Clickable card beside vinyl */
.click-card{
    width:140px;height:60px;background:#ffe3e6;border-radius:20px;
    display:flex;justify-content:center;align-items:center;
    box-shadow:0 12px 35px rgba(0,0,0,.25);cursor:pointer;
    font-family:'Great Vibes',cursive;font-size:18px;color:#d6336c;
    transition:0.3s;
}
.click-card:hover{transform:scale(1.05);}
</style>
</head>
<body>
<div class="flicker"></div>

<script>
// floating hearts
for(let i=0;i<30;i++){
    let h=document.createElement("div");
    h.className="heart";
    h.style.left=Math.random()*100+"%";
    h.style.animationDuration=4+Math.random()*3+"s";
    h.style.animationDelay=Math.random()*5+"s";
    document.body.appendChild(h);
}
</script>

<div class="envelope" onclick="openEnvelope()">
    <div class="env-body"></div>
    <div class="flap" id="flap"></div>
    <div class="env-text">What Echoes Within My Heart</div>
    <div class="seal" id="seal"></div>
</div>

<div class="letter" id="letter">
    <div class="title">What Echoes Within My Heart</div>
    <p id="typewriter"></p>
    <span onclick="closeLetter()" style="position:absolute;top:10px;right:15px;font-size:25px;font-weight:bold;color:#d6336c;cursor:pointer;">&times;</span>
</div>

<div class="music-box" id="musicBox">
    <div class="album-bg">
        <div class="vinyl" id="vinyl"></div>
    </div>
    <div class="click-card" onclick="showLetter()">Open Letter</div>
    <iframe id="spotifyPlayer" src="https://open.spotify.com/embed/track/5cJZPy9Tad2aT3ZMnN6yvd?utm_source=generator&autoplay=1" width="250" height="80" frameborder="0" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" style="border-radius:12px;"></iframe>
</div>

<audio id="openSound" src="https://www.soundjay.com/paper/sounds/paper-rustle-2.mp3"></audio>
<audio id="clickSound" src="https://www.soundjay.com/button/sounds/button-16.mp3"></audio>

<script>
const letterText = `Ginamos,  Bagnet,  Pritong Talong,  Fried Banana…

Happy Heart's Day, Baby!!  Thanks for being my personal serotonin. Don’t even think about being jealous ‘cause others have someone—lucky for you… I’m here.  We’ve got the luxury of dumb jokes, the “expensive” date of remembering how we met, and all the weird little things that make us us. If you ever feel unloved or less valuable… nope. Not true. You are very much loved, appreciated, and yes, totally adored by me. ’Wag kang mainggit sa iba. Bakit? Kaya ba nilang gawin ‘to? don't think soooo hahahahah.

I hope I made your day, today! love u`;

function typeWriter(text,i=0){
    const letterEl=document.getElementById("letter");
    const typeEl=document.getElementById("typewriter");
    if(i<text.length){
        typeEl.innerHTML += text.charAt(i);
        letterEl.scrollTop = letterEl.scrollHeight; // auto-scroll
        setTimeout(()=>typeWriter(text,i+1),90);
    }
}

function openEnvelope(){
    document.getElementById('openSound').play();
    document.getElementById('flap').style.transform="rotateX(180deg)";
    document.getElementById('seal').style.display='none';
    setTimeout(()=>{
        document.querySelector('.envelope').style.display="none";
        document.getElementById('musicBox').style.display="flex";
        document.getElementById('vinyl').style.animationPlayState="running";
        document.getElementById('spotifyPlayer').src=document.getElementById('spotifyPlayer').src;
    },1200);
}

function showLetter(){
    document.getElementById('clickSound').play();
    const letter = document.getElementById('letter');
    letter.classList.add('show');
    typeWriter(letterText);
}

function closeLetter(){
    document.getElementById('clickSound').play();
    const letter = document.getElementById('letter');
    letter.classList.remove('show');
    document.getElementById('typewriter').innerHTML='';
}
</script>
</body>
</html>
