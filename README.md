# ETEA35-online
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ETEA Practice Test</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
<style>
body{font-family:'Poppins',sans-serif;background:linear-gradient(135deg,#ff9a9e,#fecfef);margin:0}
.container{max-width:900px;margin:20px auto;background:#fff;padding:30px;border-radius:20px;box-shadow:0 10px 30px rgba(0,0,0,.2)}
h2{text-align:center}
.center{text-align:center}
input{width:100%;padding:12px;margin-bottom:15px;border-radius:10px;border:2px solid #ddd}
button{padding:12px;border:none;border-radius:10px;font-size:16px;font-weight:bold;cursor:pointer;margin:5px}
#startBtn{background:#2980b9;color:#fff;width:100%}
#timer{background:#e74c3c;color:#fff;padding:15px;text-align:center;border-radius:10px;margin-bottom:10px}
.stats-bar{display:flex;justify-content:space-between;background:#f8f9fa;padding:10px;border-radius:10px;margin-bottom:15px;font-weight:600;font-size:14px;border:1px solid #eee}
.option{border:2px solid #ddd;padding:15px;border-radius:10px;margin-bottom:12px;cursor:pointer}
.option.correct{background:#2980b9;color:#fff}
.option.wrong{background:#e74c3c;color:#fff}
.buttons{display:flex;justify-content:space-between}
#submitBtn{display:none;background:#27ae60;color:white;width:100%;margin-top:20px}
.subject-box{background:#f4f6f7;padding:12px;border-radius:10px;margin:8px 0}
.review-option.correct{background:#2980b9;color:#fff;padding:8px;border-radius:8px;margin:4px 0}
.review-option.wrong{background:#e74c3c;color:#fff;padding:8px;border-radius:8px;margin:4px 0}
.footer{text-align:center;color:#555;margin:20px 0;font-size:14px}
#resName{font-size: 22px; color: #2980b9; font-weight: 600;}
</style>
</head>
<body>

<div class="container center" id="loginDiv">
<h2>ETEA Practice Test</h2>
<input id="studentName" placeholder="Student Name">
<input id="rollNo" placeholder="Roll Number">
<button id="startBtn" onclick="startCountdown()">Start Test</button>
<div id="countdown" style="font-size:28px;color:red"></div>
</div>

<div class="container" id="quizDiv" style="display:none">
<div id="timer">Time Left: 40:00</div>
<div class="stats-bar">
    <span id="qCounter">Question: 1/100</span>
    <span id="attemptedCounter">Attempted: 0/100</span>
</div>
<div id="questionBox"></div>
<div id="optionsBox"></div>
<div class="buttons">
<button onclick="prevQ()">Previous</button>
<button onclick="skipQ()">Skip</button>
<button onclick="nextQ()" id="nextBtn" disabled>Next</button>
</div>
<button id="submitBtn" onclick="submitTest()">Submit Test</button>
</div>

<div class="container center" id="resultDiv" style="display:none">
<h2 id="resStatus"></h2>
<p id="resName"></p>
<p id="resScore"></p>
<p id="resTime"></p>
<h3>Subject-Wise Result</h3>
<div id="subjectResult"></div>
<button onclick="showReview()">Review Test</button>
<button onclick="location.reload()">Restart</button>
</div>

<div class="container" id="reviewDiv" style="display:none">
<h2 class="center">Test Review</h2>
<div id="reviewContent"></div>
<button onclick="backToResult()">Back to Result</button>
</div>

<div class="footer">
Created by <b>MUHAMMAD FAIZAN NAWAB</b>
</div>

<script>
 const questions = [


    // --- SCIENCE (1-30) ---
    {subject:"Science", q:"If a plant cell loses turgidity, which organelle is primarily responsible for maintaining internal pressure?", o:["Nucleus", "Large Vacuole", "Mitochondria", "Chloroplast"], c:1},
    {subject:"Science", q:"In biological organization, 'heart' is to 'organ' as 'blood' is to:", o:["Cell", "Tissue", "System", "Organism"], c:1},
    {subject:"Science", q:"Which part of the flower is responsible for producing male gametes?", o:["Stigma", "Ovary", "Anther", "Filament"], c:2},
    {subject:"Science", q:"A seed is formed from which part of the flower after fertilization?", o:["Ovule", "Ovary", "Style", "Sepal"], c:0},
    {subject:"Science", q:"Which enzyme starts the chemical breakdown of carbohydrates in the buccal cavity?", o:["Pepsin", "Lipase", "Amylase", "Bile"], c:2},
    {subject:"Science", q:"The primary site for the absorption of nutrients into the bloodstream is:", o:["Stomach", "Large Intestine", "Villi in Small Intestine", "Esophagus"], c:2},
    {subject:"Science", q:"Why is a diet high in saturated fats considered 'unbalanced'?", o:["Lacks minerals", "Leads to cholesterol buildup", "Prevents protein synthesis", "Too much fiber"], c:1},
    {subject:"Science", q:"Night blindness is caused by the deficiency of which vitamin?", o:["Vitamin C", "Vitamin D", "Vitamin A", "Vitamin K"], c:2},
    {subject:"Science", q:"According to Kinetic Molecular Theory, gas particles move:", o:["In circular motions", "In fixed positions", "Randomly at high speeds", "Only when heated"], c:2},
    {subject:"Science", q:"Which of the following represents a 'Compound'?", o:["Oxygen Gas", "Pure Gold", "Pure Water (H2O)", "Iron Filings"], c:2},
    {subject:"Science", q:"An element is a substance that:", o:["Can be broken down by heat", "Is made of only one type of atom", "Is always solid", "Is a mixture of gases"], c:1},
    {subject:"Science", q:"In a series circuit, if one bulb blows out, the other bulbs will:", o:["Glow brighter", "Glow normally", "Switch off immediately", "Dim down"], c:2},
    {subject:"Science", q:"What is the function of a 'fuse' in an electrical circuit?", o:["Increase voltage", "Safety switch for surges", "Store energy", "Convert AC to DC"], c:1},
    {subject:"Science", q:"When a ball is held at the top of a hill, it possesses:", o:["Kinetic Energy", "Gravitational Potential Energy", "Chemical Energy", "Thermal Energy"], c:1},
    {subject:"Science", q:"Energy cannot be created or destroyed, only transformed. This is:", o:["Law of Gravity", "Law of Conservation of Energy", "Law of Inertia", "Law of Reflection"], c:1},
    {subject:"Science", q:"Which planet is known as the 'Red Planet'?", o:["Venus", "Jupiter", "Mars", "Saturn"], c:2},
    {subject:"Science", q:"The asteroid belt is located between the orbits of:", o:["Earth and Mars", "Mars and Jupiter", "Jupiter and Saturn", "Venus and Earth"], c:1},
    {subject:"Science", q:"A 'Light Year' is a unit of:", o:["Time", "Intensity", "Distance", "Speed"], c:2},
    {subject:"Science", q:"Which process involves movement of water through a semi-permeable membrane?", o:["Diffusion", "Osmosis", "Respiration", "Digestion"], c:1},
    {subject:"Science", q:"The part of the digestive system that absorbs excess water is:", o:["Rectum", "Large Intestine", "Small Intestine", "Pancreas"], c:1},
    {subject:"Science", q:"Which form of energy is stored in a battery?", o:["Electrical", "Kinetic", "Chemical Potential", "Nuclear"], c:2},
    {subject:"Science", q:"A material that does not allow electricity to pass through is an:", o:["Conductor", "Insulator", "Semiconductor", "Metal"], c:1},
    {subject:"Science", q:"Which gas is essential for the process of combustion?", o:["Nitrogen", "Carbon Dioxide", "Oxygen", "Hydrogen"], c:2},
    {subject:"Science", q:"The boiling point of water at sea level is:", o:["0°C", "50°C", "100°C", "212°C"], c:2},
    {subject:"Science", q:"Which celestial body is at the center of our Solar System?", o:["The Moon", "Earth", "The Sun", "The Milky Way"], c:2},
    {subject:"Science", q:"In plants, losing water through leaves is called:", o:["Photosynthesis", "Transpiration", "Respiration", "Germination"], c:1},
    {subject:"Science", q:"An atom consists of:", o:["Only protons", "Protons, Neutrons, and Electrons", "Only Electrons", "Molecules"], c:1},
    {subject:"Science", q:"Which of these is a renewable source of energy?", o:["Coal", "Natural Gas", "Solar Power", "Petroleum"], c:2},
    {subject:"Science", q:"Smallest unit of a compound that retains its properties is a:", o:["Atom", "Molecule", "Element", "Proton"], c:1},
    {subject:"Science", q:"The 'voice box' is scientifically known as the:", o:["Pharynx", "Larynx", "Trachea", "Esophagus"], c:1},

    // --- MATHEMATICS (31-60) ---
    {subject:"Math", q:"What is the HCF of 12 and 18?", o:["2", "3", "6", "36"], c:2},
    {subject:"Math", q:"Which of the following is a prime number?", o:["1", "9", "15", "17"], c:3},
    {subject:"Math", q:"Calculate: (-10) + (+15) - (-5)", o:["0", "10", "20", "-10"], c:2},
    {subject:"Math", q:"If A = {1, 2, 3} and B = {3, 4, 5}, what is A ∩ B?", o:["{1..5}", "{3}", "{ }", "{1, 2}"], c:1},
    {subject:"Math", q:"A set with no elements is called:", o:["Universal Set", "Finite Set", "Null Set", "Subset"], c:2},
    {subject:"Math", q:"Express 3/5 as a percentage.", o:["30%", "50%", "60%", "75%"], c:2},
    {subject:"Math", q:"Ratio of boys to girls is 2:3. If there are 20 boys, how many girls?", o:["10", "30", "40", "60"], c:1},
    {subject:"Math", q:"Simplify: 2x + 3y - x + 4y", o:["3x + 7y", "x + 7y", "3x - y", "x - 7y"], c:1},
    {subject:"Math", q:"Find the value of 'a' if 2a + 5 = 15.", o:["5", "10", "20", "7.5"], c:0},
    {subject:"Math", q:"An angle greater than 90° but less than 180° is:", o:["Acute", "Right", "Obtuse", "Reflex"], c:2},
    {subject:"Math", q:"The sum of angles in a triangle is always:", o:["90°", "180°", "270°", "360°"], c:1},
    {subject:"Math", q:"What is the area of a rectangle (L=8cm, W=5cm)?", o:["13 cm²", "26 cm²", "40 cm²", "80 cm²"], c:2},
    {subject:"Math", q:"Calculate the volume of a cube with side 3cm.", o:["9 cm³", "18 cm³", "27 cm³", "54 cm³"], c:2},
    {subject:"Math", q:"In data handling, the 'Mode' is:", o:["Average", "Middle value", "Most frequent", "Range"], c:2},
    {subject:"Math", q:"If a circle has a radius of 7cm, what is its diameter?", o:["3.5 cm", "7 cm", "14 cm", "21 cm"], c:2},
    {subject:"Math", q:"Find the LCM of 4 and 6.", o:["2", "12", "24", "10"], c:1},
    {subject:"Math", q:"Add: -25 and -15", o:["40", "-40", "10", "-10"], c:1},
    {subject:"Math", q:"If x = 2 and y = 3, find the value of x² + y.", o:["5", "7", "10", "13"], c:1},
    {subject:"Math", q:"25% of 200 is:", o:["25", "50", "75", "100"], c:1},
    {subject:"Math", q:"Line segment joining two points on circumference passing through center:", o:["Radius", "Chord", "Diameter", "Arc"], c:2},
    {subject:"Math", q:"Simplify the ratio 15:25.", o:["1:2", "3:5", "5:3", "2:3"], c:1},
    {subject:"Math", q:"The additive inverse of -8 is:", o:["0", "1/8", "8", "-1/8"], c:2},
    {subject:"Math", q:"If a set has 3 elements, how many subsets does it have?", o:["3", "6", "8", "9"], c:2},
    {subject:"Math", q:"The coefficient of 'y' in the term -5y is:", o:["5", "-5", "y", "1"], c:1},
    {subject:"Math", q:"Two angles whose sum is 90° are:", o:["Supplementary", "Complementary", "Adjacent", "Vertical"], c:1},
    {subject:"Math", q:"The surface area of a cube with edge 's' is:", o:["s²", "4s²", "6s²", "s³"], c:2},
    {subject:"Math", q:"The number of factors for a prime number is always:", o:["1", "2", "3", "Infinite"], c:1},
    {subject:"Math", q:"0.05 can be written as what percentage?", o:["0.5%", "5%", "50%", "500%"], c:1},
    {subject:"Math", q:"A triangle with all three sides equal is:", o:["Isosceles", "Scalene", "Equilateral", "Right"], c:2},
    {subject:"Math", q:"The 'Range' in data handling is calculated by:", o:["Adding all", "High - Low", "Middle value", "Mode"], c:1},

    // --- ENGLISH (61-80) ---
    {subject:"English", q:"Choose the correct sentence:", o:["He have finished", "He has finished", "He finishing", "He were finished"], c:1},
    {subject:"English", q:"'The cat is sitting ____ the table.'", o:["In", "Under", "Between", "Among"], c:1},
    {subject:"English", q:"What is the plural of 'Criterion'?", o:["Criterions", "Criterias", "Criteria", "Criteries"], c:2},
    {subject:"English", q:"Identify the pronoun in: 'She told him a secret.'", o:["Told", "Secret", "She", "A"], c:2},
    {subject:"English", q:"Which is in Past Continuous Tense?", o:["I play", "I played", "I was playing", "I will play"], c:2},
    {subject:"English", q:"'Neither of the two books ____ interesting.'", o:["Are", "Is", "Were", "Have"], c:1},
    {subject:"English", q:"Correct plural of 'Knife':", o:["Knifes", "Knive", "Knives", "Knife's"], c:2},
    {subject:"English", q:"'They ____ to the zoo tomorrow.'", o:["Go", "Went", "Will go", "Gone"], c:2},
    {subject:"English", q:"'She is afraid ____ spiders.'", o:["From", "With", "Of", "By"], c:2},
    {subject:"English", q:"Identify the Reflexive Pronoun:", o:["Who", "This", "Himself", "They"], c:2},
    {subject:"English", q:"'I have ____ my lunch.'", o:["Eat", "Ate", "Eaten", "Eating"], c:2},
    {subject:"English", q:"'The sun ____ in the East.'", o:["Rise", "Rising", "Rises", "Rose"], c:2},
    {subject:"English", q:"Plural of 'Focus':", o:["Focuses", "Foci", "Focusses", "Focus's"], c:1},
    {subject:"English", q:"'He is the boy ____ won the trophy.'", o:["Which", "Who", "Whom", "Whose"], c:1},
    {subject:"English", q:"____ is used for more than two people.", o:["Among", "Above", "Across", "Along"], c:0},
    {subject:"English", q:"'Every student ____ to pass the exam.'", o:["Want", "Wants", "Wanting", "Have wanted"], c:1},
    {subject:"English", q:"'She works ____ 9 am ____ 5 pm.'", o:["Since/To", "From/To", "At/In", "For/By"], c:1},
    {subject:"English", q:"Identify the Interrogative Pronoun:", o:["That", "Which", "Each", "Someone"], c:1},
    {subject:"English", q:"'They ____ playing chess since morning.'", o:["Are", "Was", "Have been", "Has been"], c:2},
    {subject:"English", q:"Plural of 'Deer':", o:["Deers", "Deer", "Deeres", "Dears"], c:1},

    // --- URDU (81-90) ---
    {subject:"Urdu", q:"وہ کلمہ جو کسی کام کے کرنے یا ہونے کو ظاہر کرے، کیا کہلاتا ہے؟", o:["اسم", "فعل", "حرف", "صفت"], c:1},
    {subject:"Urdu", q:"'میز پر کتاب ہے'۔ اس جملے میں 'پر' کیا ہے؟", o:["حرفِ جار", "اسمِ معرفہ", "فعلِ ماضی", "صفتِ ذاتی"], c:0},
    {subject:"Urdu", q:"اسمِ نکرہ کی نشاندہی کریں:", o:["لاہور", "علامہ اقبال", "لڑکا", "دریائے راوی"], c:2},
    {subject:"Urdu", q:"'خوبصورت باغ' میں 'خوبصورت' کیا ہے؟", o:["فعل", "صفت", "موصوف", "ضمیر"], c:1},
    {subject:"Urdu", q:"'وہ' ، 'تم' ، 'میں' گرامر کی رو سے کیا ہیں؟", o:["اسمِ ضمیر", "اسمِ اشارہ", "حرفِ عطف", "فعلِ حال"], c:0},
    {subject:"Urdu", q:"لفظ 'دن' کا متضاد کیا ہے؟", o:["صبح", "شام", "رات", "اجالا"], c:2},
    {subject:"Urdu", q:"واحد جمع کی درست جوڑی پہچانیں:", o:["کتاب - کتابیں", "بچہ - بچو", "کرسی - کرسوں", "قلم - قلموں"], c:0},
    {subject:"Urdu", q:"'احمد سکول جاتا ہے'۔ یہ کون سا زمانہ ہے؟", o:["فعلِ ماضی", "فعلِ حال", "فعلِ مستقبل", "فعلِ امر"], c:1},
    {subject:"Urdu", q:"وہ اسم جو کسی خاص جگہ یا شخص کا نام ہو:", o:["اسمِ نکرہ", "اسمِ معرفہ", "اسمِ صفت", "اسمِ ضمیر"], c:1},
    {subject:"Urdu", q:"جملہ مکمل کریں: 'بچے میدان میں ____ رہے ہیں۔'", o:["کھیل", "کھیلنا", "کھیلتے", "کھیلے"], c:0},

    // --- ISLAMIYAT (91-100) ---
    {subject:"Islamiyat", q:"عقیدہ توحید سے کیا مراد ہے؟", o:["اللہ کو ایک ماننا", "فرشتوں پر ایمان", "رسولوں پر ایمان", "قیامت پر ایمان"], c:0},
    {subject:"Islamiyat", q:"اللہ تعالیٰ کے آخری رسول کون ہیں؟", o:["حضرت عیسیٰؑ", "حضرت موسیٰؑ", "حضرت محمدؐ", "حضرت ابراہیمؑ"], c:2},
    {subject:"Islamiyat", q:"ہجرتِ مدینہ کے بعد مہاجرین اور انصار کے درمیان رشتہ کہلاتا ہے:", o:["میثاقِ مدینہ", "مواخات", "بیعتِ عقبہ", "صلح حدبیہ"], c:1},
    {subject:"Islamiyat", q:"غزوہ بدر کس ہجری میں ہوا؟", o:["1 ہجری", "2 ہجری", "3 ہجری", "4 ہجری"], c:1},
    {subject:"Islamiyat", q:"'رسالت' کا لغوی معنی کیا ہے؟", o:["پیغام پہنچانا", "عبادت کرنا", "ہجرت کرنا", "صبر کرنا"], c:0},
    {subject:"Islamiyat", q:"غزوہ احد میں مسلمانوں کے سپہ سالار کون تھے؟", o:["حضرت ابوبکرؓ", "حضرت عمرؓ", "حضرت محمدؐ", "حضرت خالد بن ولیدؓ"], c:2},
    {subject:"Islamiyat", q:"'انصار' سے کیا مراد ہے؟", o:["ہجرت کرنے والے", "مدد کرنے والے", "مکہ کے کافر", "تجارت کرنے والے"], c:1},
    {subject:"Islamiyat", q:"توحید کی ضد (الٹ) کیا ہے؟", o:["کفر", "شرک", "نفاق", "حسد"], c:1},
    {subject:"Islamiyat", q:"خاتم النبیین کا خطاب کس کو دیا گیا؟", o:["حضرت آدمؑ", "حضرت نوحؑ", "حضرت محمدؐ", "حضرت اسماعیلؑ"], c:2},
    {subject:"Islamiyat", q:"مواخات کا مدینہ کی معیشت پر کیا اثر پڑا؟", o:["غربت بڑھ گئی", "معاشی استحکام آیا", "تجارت بند ہوگئی", "کوئی اثر نہیں ہوا"], c:1},

];

let answers=new Array(questions.length).fill(null);
let index=0,time=2400,startTime,timerInt;

function startCountdown(){
if(!studentName.value||!rollNo.value){alert("Fill all fields");return;}
let c=5;countdown.innerText=c;
let i=setInterval(()=>{
c--;countdown.innerText=c;
if(c===0){
clearInterval(i);
loginDiv.style.display="none";
quizDiv.style.display="block";
startTime=Date.now();
loadQ();startTimer();
}},1000);
}

function updateStats() {
    let attempted = answers.filter(a => a !== null).length;
    document.getElementById("qCounter").innerText = `Question: ${index + 1}/${questions.length}`;
    document.getElementById("attemptedCounter").innerText = `Attempted: ${attempted}/${questions.length}`;
}

function loadQ(){
let q=questions[index];
questionBox.innerHTML=`<h3>${index+1}. (${q.subject}) ${q.q}</h3>`;
optionsBox.innerHTML="";
q.o.forEach((op,i)=>{
let d=document.createElement("div");
d.className="option";
if(answers[index] === i) d.classList.add(i===q.c?"correct":"wrong");
d.innerText=op;
d.onclick=()=>{
if(answers[index]!=null)return;
answers[index]=i;
d.classList.add(i===q.c?"correct":"wrong");
nextBtn.disabled=false;
updateStats();
};
optionsBox.appendChild(d);
});
nextBtn.disabled=answers[index]==null;
submitBtn.style.display=index===questions.length-1?"block":"none";
updateStats();
}

function nextQ(){if(index<questions.length-1){index++;loadQ();}}
function prevQ(){if(index>0){index--;loadQ();}}
function skipQ(){index=(index+1)%questions.length;loadQ();}

function startTimer(){
timerInt=setInterval(()=>{
let m=Math.floor(time/60),s=time%60;
timer.innerText=`Time Left: ${m}:${s<10?'0':''}${s}`;
if(time--<=0){clearInterval(timerInt);submitTest();}
},1000);
}

function submitTest(){
clearInterval(timerInt);
quizDiv.style.display="none";
resultDiv.style.display="block";
let score=0,subjectStats={};
questions.forEach((q,i)=>{
if(!subjectStats[q.subject]) subjectStats[q.subject]={total:0,correct:0};
subjectStats[q.subject].total++;
if(answers[i]===q.c){score++;subjectStats[q.subject].correct++;}
});
let pct=Math.round(score/questions.length*100);
resStatus.innerText=pct>=40?"PASSED":"FAILED";
resName.innerText=`Student Name: ${studentName.value}`;
resScore.innerText=`Overall Score: ${score}/${questions.length} (${pct}%)`;
resTime.innerText=`Time Taken: ${Math.floor((Date.now()-startTime)/60000)} minutes`;
subjectResult.innerHTML="";
for(let s in subjectStats){
let x=subjectStats[s];
subjectResult.innerHTML+=`<div class="subject-box"><b>${s}</b>: ${x.correct}/${x.total} → ${Math.round(x.correct/x.total*100)}%</div>`;
}
}

function showReview(){
resultDiv.style.display="none";
reviewDiv.style.display="block";
reviewContent.innerHTML="";
questions.forEach((q,i)=>{
let html=`<h4>${i+1}. ${q.q}</h4>`;
q.o.forEach((op,idx)=>{
let cls="review-option";
if(idx===q.c) cls+=" correct";
else if(answers[i]===idx) cls+=" wrong";
html+=`<div class="${cls}">${op}</div>`;
});
reviewContent.innerHTML+=html;
});
}

function backToResult(){
reviewDiv.style.display="none";
resultDiv.style.display="block";
}
</script>
</body>
</html>
