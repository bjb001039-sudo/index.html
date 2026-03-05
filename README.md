<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title>운빨쿠지 대포게임</title>

<style>

body{
margin:0;
font-family:sans-serif;
text-align:center;
background:#8fb6f7;
overflow:hidden;
}

/* 배경 워터마크 */

.watermark{
position:fixed;
top:50%;
left:50%;
transform:translate(-50%,-50%);
font-size:120px;
color:rgba(255,255,255,0.2);
font-weight:bold;
pointer-events:none;
}

/* 결과 공 */

#ball{
width:140px;
height:140px;
border-radius:50%;
background:#2e7d32;
color:#ffd600;
font-size:60px;
display:flex;
align-items:center;
justify-content:center;
margin:120px auto 20px;
transition:transform 0.4s;
}

/* 대포 */

#cannon{
font-size:80px;
margin-top:20px;
}

/* 발사 애니메이션 */

.fire{
transform:translateY(-150px) scale(1.2);
}

/* 버튼 */

button{
padding:14px 30px;
font-size:18px;
border-radius:25px;
border:none;
background:yellow;
cursor:pointer;
margin:5px;
}

input{
padding:8px;
font-size:16px;
width:120px;
}

/* 기록 */

#history{
position:fixed;
right:30px;
top:80px;
width:200px;
background:white;
border:2px solid black;
border-radius:15px;
padding:20px;
}

</style>
</head>

<body>

<div class="watermark">운빨쿠지</div>

<h2>운빨쿠지 대포게임</h2>

<div>
최대 숫자
<input id="maxInput" type="number" value="8">

관리자 강제숫자
<input id="forceInput" type="number" placeholder="없으면 랜덤">

<button onclick="initGame()">게임 시작</button>
</div>

<div id="ball">?</div>

<div id="cannon">💣</div>

<button onclick="fire()">발사</button>

<div id="history">
<b>나온 숫자</b>
<ul id="list"></ul>
</div>

<script>

let numbers=[]
let history=[]

function initGame(){

const max = Number(document.getElementById("maxInput").value)

numbers=[]

for(let i=1;i<=max;i++){
numbers.push(i)
}

history=[]
updateHistory()

document.getElementById("ball").innerText="?"

}

/* 발사 */

function fire(){

if(numbers.length===0){
alert("모든 숫자가 나왔습니다")
return
}

const ball=document.getElementById("ball")

ball.classList.add("fire")

setTimeout(()=>{

let result

const forced = Number(document.getElementById("forceInput").value)

if(forced && numbers.includes(forced)){
result=forced
}else{

const index=Math.floor(Math.random()*numbers.length)
result=numbers[index]

}

numbers=numbers.filter(n=>n!==result)

history.unshift(result)

ball.innerText=result

updateHistory()

ball.classList.remove("fire")

},400)

}

/* 기록 업데이트 */

function updateHistory(){

const list=document.getElementById("list")

list.innerHTML=""

history.forEach(n=>{
const li=document.createElement("li")
li.innerText=n+"번"
list.appendChild(li)
})

}

</script>

</body>
</html>
