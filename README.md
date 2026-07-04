<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<title>Birthday Surprise</title>

<style>
body {
  margin:0;
  font-family:sans-serif;
  background:#ffdde1;
  text-align:center;
  overflow:hidden;
}

/* กล่องของขวัญ */
#giftBox {
  position:fixed;
  width:100%;
  height:100%;
  background:black;
  display:flex;
  justify-content:center;
  align-items:center;
  flex-direction:column;
  color:white;
}

.box {
  width:120px;
  height:120px;
  background:red;
  cursor:pointer;
  position:relative;
  animation:shake 1s infinite;
}

.box::before, .box::after {
  content:"";
  position:absolute;
  background:gold;
}

.box::before {
  width:20px;
  height:120px;
  left:50%;
  transform:translateX(-50%);
}

.box::after {
  width:120px;
  height:20px;
  top:50%;
  transform:translateY(-50%);
}

@keyframes shake {
  0%{transform:rotate(0)}
  50%{transform:rotate(3deg)}
  100%{transform:rotate(-3deg)}
}

/* เนื้อเว็บ */
#content {
  display:none;
  padding:20px;
}

.slide {
  width:250px;
  height:250px;
  object-fit:cover;
  border-radius:20px;
}

/* จดหมาย */
#letter {
  margin-top:20px;
  white-space:pre-line;
  font-size:18px;
}

/* หัวใจ */
.heart {
  position:fixed;
  top:-10px;
  color:red;
  animation:fall linear forwards;
}

@keyframes fall {
  to {
    transform:translateY(100vh);
    opacity:0;
  }
}
</style>
</head>

<body>

<audio id="music" loop>
  <source src="music.mp3">
</audio>

<!-- กล่องของขวัญ -->
<div id="giftBox" onclick="openGift()">
  <div class="box"></div>
  <p>กดเปิดของขวัญ 🎁</p>
</div>

<!-- เนื้อเว็บ -->
<div id="content">
  <h1>🎉 Happy Birthday ❤️</h1>
  <img id="slide" class="slide" src="1.jpg">
  <div id="letter"></div>
</div>

<script>

/* เปิดของขวัญ */
function openGift(){
  document.getElementById("giftBox").style.display="none";
  document.getElementById("content").style.display="block";
  document.getElementById("music").play();

  startSlide();
  typeText();
  hearts();
}

/* สไลด์ */
let images=["1.jpg","2.jpg","3.jpg"];
let i=0;

function startSlide(){
  setInterval(()=>{
    i=(i+1)%images.length;
    document.getElementById("slide").src=images[i];
  },2000);
}

/* พิมพ์ข้อความ */
let text="สุขสันต์วันเกิดนะ ❤️\nขอให้มีความสุขมากๆ\nอยู่ด้วยกันนานๆนะ";
let idx=0;

function typeText(){
  let el=document.getElementById("letter");
  let t=setInterval(()=>{
    el.innerHTML+=text[idx];
    idx++;
    if(idx>=text.length) clearInterval(t);
  },80);
}

/* หัวใจลอย */
function hearts(){
  setInterval(()=>{
    let h=document.createElement("div");
    h.className="heart";
    h.innerHTML="❤️";
    h.style.left=Math.random()*100+"vw";
    h.style.fontSize=Math.random()*20+10+"px";
    h.style.animationDuration=(Math.random()*3+2)+"s";
    document.body.appendChild(h);

    setTimeout(()=>h.remove(),5000);
  },200);
}

</script>

</body>
</html>
