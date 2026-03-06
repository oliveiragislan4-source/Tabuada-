
function startGame(){

nextQuestion()

}

function nextQuestion(){

let table=document.getElementById("table").value

if(table=="random"){

num1=random(1,level+2)

}else{

num1=parseInt(table)

}

num2=random(1,10)

correct=num1*num2

document.getElementById("question").innerText=num1+" × "+num2

generateAnswers()

}

function generateAnswers(){

let arr=[correct]

while(arr.length<4){

let n=random(1,120)

if(!arr.includes(n)) arr.push(n)

}

arr.sort(()=>Math.random()-0.5)

let div=document.getElementById("answers")

div.innerHTML=""

arr.forEach(a=>{

let btn=document.createElement("button")

btn.innerText=a

btn.onclick=()=>checkAnswer(btn,a)

div.appendChild(btn)

})

}

function checkAnswer(btn,a){

if(a==correct){

btn.classList.add("correct")

xp+=10

if(xp%100==0){

level++

}

}else{

btn.classList.add("wrong")

lives--

if(lives<=0){

alert("Fim de jogo")

xp=0
level=1
lives=3

}

}

update()

setTimeout(nextQuestion,900)

}

function update(){

document.getElementById("xp").innerText=xp
document.getElementById("lives").innerText=lives
document.getElementById("level").innerText="Nível "+level

let progress=(xp%100)

document.getElementById("progressBar").style.width=progress+"%"

save()

}

function save(){

localStorage.setItem("xp",xp)
localStorage.setItem("level",level)

}

function load(){

let sXP=localStorage.getItem("xp")
let sLevel=localStorage.getItem("level")

if(sXP){

xp=parseInt(sXP)
level=parseInt(sLevel)

}

update()

}

function random(min,max){

return Math.floor(Math.random()*(max-min+1))+min

}

load()

</script>

</body>
</html>
