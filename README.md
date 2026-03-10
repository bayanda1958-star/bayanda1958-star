<!DOCTYPE html>
<html>
<head>
<title>Pro Game Website</title>

<style>
body{
    margin:0;
    font-family:Arial;
    background:#0f172a;
    color:white;
    text-align:center;
}

header{
    background:#020617;
    padding:15px;
    font-size:25px;
}

button{
    padding:10px;
    margin:5px;
    border:none;
    background:#22c55e;
    color:white;
    cursor:pointer;
}

button:hover{
    background:#16a34a;
}

#gameArea{
    width:350px;
    height:350px;
    background:#111827;
    margin:auto;
    margin-top:20px;
    position:relative;
    border:2px solid white;
}

#box{
    width:50px;
    height:50px;
    background:red;
    position:absolute;
    display:none;
    border-radius:10px;
}

#enemy{
    width:40px;
    height:40px;
    background:yellow;
    position:absolute;
    display:none;
    border-radius:50%;
}

.panel{
    margin-top:10px;
    font-size:18px;
}

.dark{
    background:black;
}

.light{
    background:white;
    color:black;
}
</style>

</head>
<body>

<header>🎮 Pro Game Website</header>

<div class="panel">

Score: <span id="score">0</span> |
Time: <span id="time">15</span>

<br>

<button onclick="startGame()">Start</button>
<button onclick="restartGame()">Restart</button>
<button onclick="toggleTheme()">Dark / Light</button>

</div>

<div id="gameArea">

<div id="box" onclick="hitBox()"></div>
<div id="enemy" onclick="hitEnemy()"></div>

</div>

<audio id="clickSound">
<source src="https://www.soundjay.com/buttons/sounds/button-16.mp3">
</audio>

<script>

let score = 0
let time = 15
let running = false
let timer

function startGame(){

score = 0
time = 15
running = true

updateUI()

showBox()
showEnemy()

timer = setInterval(()=>{

time--
updateUI()

if(time <= 0){
endGame()
}

},1000)

}

function restartGame(){
clearInterval(timer)
startGame()
}

function updateUI(){
document.getElementById("score").innerText = score
document.getElementById("time").innerText = time
}

function randomPos(size){

let max = 300

return Math.random() * (max - size)

}

function showBox(){

let box = document.getElementById("box")

box.style.display = "block"

moveBox()

}

function moveBox(){

if(!running) return

let box = document.getElementById("box")

box.style.left = randomPos(50) + "px"
box.style.top = randomPos(50) + "px"

setTimeout(moveBox,800)

}

function hitBox(){

if(!running) return

score++

playSound()

moveBox()

updateUI()

}

function showEnemy(){

let enemy = document.getElementById("enemy")

enemy.style.display = "block"

moveEnemy()

}

function moveEnemy(){

if(!running) return

let enemy = document.getElementById("enemy")

enemy.style.left = randomPos(40) + "px"
enemy.style.top = randomPos(40) + "px"

setTimeout(moveEnemy,600)

}

function hitEnemy(){

if(!running) return

score--

updateUI()

}

function endGame(){

running = false

clearInterval(timer)

alert("Game Over Score: " + score)

}

function toggleTheme(){

let body = document.body

if(body.classList.contains("light")){
body.classList.remove("light")
}else{
body.classList.add("light")
}

}

function playSound(){
document.getElementById("clickSound").play()
}

</script>

</body>
</html>