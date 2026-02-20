<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Rankwise Pro Quiz</title>
<style>
body{
  font-family: Arial;
  background:#f2f4f8;
  text-align:center;
}
.container{
  width:95%;
  max-width:600px;
  margin:auto;
  margin-top:20px;
  background:white;
  padding:20px;
  border-radius:10px;
  box-shadow:0 0 15px rgba(0,0,0,0.2);
}
button{
  display:block;
  width:100%;
  padding:10px;
  margin:8px 0;
  font-size:16px;
  cursor:pointer;
}
.progress{
  height:10px;
  background:#ddd;
  border-radius:5px;
  overflow:hidden;
}
.progress-bar{
  height:10px;
  background:green;
  width:0%;
}
.correct{background:green;color:white;}
.wrong{background:red;color:white;}
#timer{color:red;font-weight:bold;}
</style>
</head>
<body>

<div class="container">

<h2>Rankwise Professional Quiz</h2>

<div id="categoryBox">
<button onclick="startQuiz('gs')">Start GS</button>
<button onclick="startQuiz('math')">Start Math</button>
</div>

<div id="quizBox" style="display:none;">
<p id="timer"></p>
<div class="progress"><div class="progress-bar" id="progressBar"></div></div>
<p id="question"></p>
<div id="options"></div>
</div>

</div>

<script>

const questions = {
gs:[
{q:"भारत का संविधान कब लागू हुआ?",o:["15 अगस्त 1947","26 जनवरी 1950","2 अक्टूबर 1949","1 जनवरी 1952"],a:1},
{q:"भारत का पहला राष्ट्रपति?",o:["नेहरू","राजेन्द्र प्रसाद","गांधी","पटेल"],a:1}
],
math:[
{q:"20 × 5 = ?",o:["100","120","150","80"],a:0},
{q:"50 ÷ 5 = ?",o:["5","15","10","20"],a:2}
]
};

let current=0;
let score=0;
let wrong=0;
let selected="";
let timer;
let timeLeft=30;
let shuffled=[];
let review=[];

function startQuiz(cat){
selected=cat;
shuffled = questions[cat].sort(()=>Math.random()-0.5);
document.getElementById("categoryBox").style.display="none";
document.getElementById("quizBox").style.display="block";
loadQuestion();
startTimer();
}

function loadQuestion(){
let q=shuffled[current];
document.getElementById("question").innerText=q.q;

let optionsHTML="";
q.o.forEach((opt,i)=>{
optionsHTML+=`<button onclick="checkAnswer(${i},this)">${opt}</button>`;
});
document.getElementById("options").innerHTML=optionsHTML;

updateProgress();
}

function checkAnswer(i,btn){
clearInterval(timer);
let correctAns=shuffled[current].a;

if(i===correctAns){
score++;
btn.classList.add("correct");
review.push("Q"+(current+1)+": Correct");
}else{
wrong++;
btn.classList.add("wrong");
review.push("Q"+(current+1)+": Wrong");
}

setTimeout(nextQuestion,1000);
}

function nextQuestion(){
current++;
if(current<shuffled.length){
timeLeft=30;
loadQuestion();
startTimer();
}else{
endQuiz();
}
}

function startTimer(){
document.getElementById("timer").innerText="Time Left: "+timeLeft;
timer=setInterval(()=>{
timeLeft--;
document.getElementById("timer").innerText="Time Left: "+timeLeft;
if(timeLeft<=0){
wrong++;
review.push("Q"+(current+1)+": Time Up");
clearInterval(timer);
nextQuestion();
}
},1000);
}

function updateProgress(){
let percent=((current)/shuffled.length)*100;
document.getElementById("progressBar").style.width=percent+"%";
}

function endQuiz(){
let finalScore = score - (wrong*0.25);
document.querySelector(".container").innerHTML=
"<h2>Quiz Completed 🎉</h2>"+
"<p>Correct: "+score+"</p>"+
"<p>Wrong: "+wrong+"</p>"+
"<p>Final Score (Negative -0.25): "+finalScore.toFixed(2)+"</p>"+
"<h3>Review:</h3><p>"+review.join("<br>")+"</p>"+
"<button onclick='location.reload()'>Restart</button>";
}

</script>

</body>
</html>
