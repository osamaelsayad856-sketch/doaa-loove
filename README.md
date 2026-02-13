<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>دعاء ♾️</title>

<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;700&display=swap" rel="stylesheet">

<style>
body{
margin:0;
font-family:'Cairo',sans-serif;
background:black;
color:white;
overflow:hidden;
}

.section{
position:absolute;
width:100%;
height:100vh;
display:flex;
flex-direction:column;
justify-content:center;
align-items:center;
text-align:center;
opacity:0;
transition:1.5s ease;
}

.active{opacity:1;}

h1{
font-size:42px;
font-weight:700;
text-shadow:0 0 30px rgba(255,255,255,.7);
}

p{
max-width:800px;
font-size:22px;
line-height:2;
font-weight:300;
}

button{
padding:14px 40px;
margin-top:40px;
font-size:18px;
border:none;
border-radius:50px;
background:linear-gradient(45deg,#ff4b5c,#ff758c);
color:white;
cursor:pointer;
transition:.4s;
}

button:hover{
transform:scale(1.1);
box-shadow:0 0 30px #ff758c;
}

.fade-black{
background:black;
position:absolute;
width:100%;
height:100%;
top:0;
left:0;
z-index:10;
opacity:1;
animation:fadeOut 3s forwards;
}

@keyframes fadeOut{
to{opacity:0;}
}

#slider{
width:80%;
max-width:600px;
height:400px;
background-size:cover;
background-position:center;
border-radius:20px;
box-shadow:0 0 60px rgba(255,255,255,.2);
transition:1s;
}

#finalImg{
width:300px;
border-radius:20px;
box-shadow:0 0 60px rgba(255,255,255,.5);
margin-top:20px;
}

#counter{
margin-top:30px;
font-size:24px;
}

canvas{
position:fixed;
top:0;
left:0;
z-index:-1;
}
</style>
</head>
<body>

<div class="fade-black"></div>

<canvas id="galaxy"></canvas>

<audio id="music" loop>
<source src="song.mp3" type="audio/mpeg">
</audio>

<!-- المشهد 1 -->
<div id="s1" class="section active">
<h1 id="typing"></h1>
<button onclick="start()">ابدأي الحكاية ❤️</button>
</div>

<!-- المشهد 2 -->
<div id="s2" class="section">
<h1>ذكرياتنا</h1>
<div id="slider"></div>
<button onclick="next('s3')">كمّلي…</button>
</div>

<!-- المشهد 3 -->
<div id="s3" class="section">
<h1>رسالة ليكي يا دعاء</h1>
<p id="letter"></p>
<button onclick="next('s4')">آخر مشهد…</button>
</div>

<!-- المشهد 4 -->
<div id="s4" class="section">
<h1>تحبي نكمّل عمرنا سوا؟ 💍</h1>
<button onclick="final()">أيوه ♾️</button>
</div>

<!-- النهاية -->
<div id="s5" class="section">
<h1>كوتي موتي بوتي للأبد ✨</h1>
<img src="final.jpg" id="finalImg">
<div id="counter"></div>
</div>

<script>

/* كتابة سينمائية */
let intro="إلى دعاء… الحب اللي غير حياتي من 2021 ✨";
let i=0;
function typeIntro(){
if(i<intro.length){
document.getElementById("typing").innerHTML+=intro[i];
i++;
setTimeout(typeIntro,80);
}}
typeIntro();

/* رسالة */
let message="من 2021… وأنا كل يوم باختارك من جديد.\nوجودك أمان… ضحكتك حياة.\nيمكن الدنيا كلها تناديكي دعاء…\nبس أنا بس اللي ليا أقولك كوتي موتي بوتي ❤️";
let j=0;
function typeLetter(){
if(j<message.length){
document.getElementById("letter").innerHTML+=message[j];
j++;
setTimeout(typeLetter,40);
}}
setTimeout(typeLetter,4000);

/* تنقل */
function next(id){
document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
document.getElementById(id).classList.add('active');
}

/* تشغيل */
function start(){
let music=document.getElementById("music");
music.volume=0;
music.play();
let fade=setInterval(()=>{
if(music.volume<0.6){music.volume+=0.02;}
else clearInterval(fade);
},200);
next('s2');
}

/* سلايدر */
let images=["photo1.jpg","photo2.jpg","photo3.jpg"];
let index=0;
setInterval(()=>{
document.getElementById("slider").style.backgroundImage="url('"+images[index]+"')";
index=(index+1)%images.length;
},3000);

/* النهاية + عداد */
function final(){
next('s5');
let startDate=new Date("2021-01-01");
let today=new Date();
let diff=today-startDate;
let days=Math.floor(diff/(1000*60*60*24));
let years=Math.floor(days/365);
let months=Math.floor((days%365)/30);
let remainingDays=(days%365)%30;

document.getElementById("counter").innerHTML=
years+" سنة و "+months+" شهر و "+remainingDays+" يوم حب ♾️";
}

/* Galaxy */
let canvas=document.getElementById("galaxy");
let ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;
let stars=[];
for(let i=0;i<300;i++){
stars.push({x:Math.random()*canvas.width,
y:Math.random()*canvas.height,
r:Math.random()*1.5});
}
function draw(){
ctx.clearRect(0,0,canvas.width,canvas.height);
ctx.fillStyle="white";
stars.forEach(s=>{
ctx.beginPath();
ctx.arc(s.x,s.y,s.r,0,Math.PI*2);
ctx.fill();
});
requestAnimationFrame(draw);
}
draw();

</script>

</body>
</html>
