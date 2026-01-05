# chillandcheng
คุณคือสัตว์ตัวอะไรในตำนานจีน
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<title>แบบทดสอบสัตว์ในตำนานจีน</title>

<style>
body{
  margin:0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg,#b71c1c,#f9a825);
  min-height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
}
.card{
  background:#fff8e1;
  width:90%;
  max-width:450px;
  padding:25px;
  border-radius:20px;
  text-align:center;
}
img{
  width:200px;
  height:200px;
  object-fit:cover;
  border-radius:15px;
}
.option{
  text-align:left;
  margin:8px 0;
}
button{
  width:100%;
  padding:12px;
  background:#b71c1c;
  color:#fff;
  border:none;
  border-radius:10px;
  margin-top:15px;
}
</style>
</head>

<body>

<div class="card" id="quiz">
  <h2 id="question"></h2>
  <img id="animalImg">
  <div id="options"></div>
  <button onclick="nextQuestion()">ถัดไป</button>
</div>

<script>
let questions=[
{
 q:"ข้อ 1: เมื่อเจอปัญหา คุณจะ…",
 img:"images/dragon.png",
 a:[
  ["dragon","นำทีมแก้ปัญหา"],
  ["tiger","ลุยตรงๆ"],
  ["phoenix","ประนีประนอม"],
  ["turtle","คิดรอบคอบ"],
  ["qilin","เลือกทางยุติธรรม"]
 ]
},
{
 q:"ข้อ 2: คนอื่นมองคุณว่า?",
 img:"images/tiger.png",
 a:[
  ["dragon","ผู้นำ"],
  ["tiger","กล้าหาญ"],
  ["phoenix","อบอุ่น"],
  ["turtle","สุขุม"],
  ["qilin","ใจดี"]
 ]
},
{
 q:"ข้อ 3: สิ่งที่คุณให้ค่ามากที่สุด?",
 img:"images/phoenix.png",
 a:[
  ["dragon","ความสำเร็จ"],
  ["tiger","อิสระ"],
  ["phoenix","ความรัก"],
  ["turtle","ความมั่นคง"],
  ["qilin","ความถูกต้อง"]
 ]
},
{
 q:"ข้อ 4: เวลามีปัญหา คุณมัก…",
 img:"images/turtle.png",
 a:[
  ["dragon","ควบคุมสถานการณ์"],
  ["tiger","เผชิญหน้า"],
  ["phoenix","เยียวยา"],
  ["turtle","อดทน"],
  ["qilin","ไกล่เกลี่ย"]
 ]
},
{
 q:"ข้อ 5: บทบาทที่คุณชอบ?",
 img:"images/qilin.png",
 a:[
  ["dragon","ผู้นำ"],
  ["tiger","นักสู้"],
  ["phoenix","ผู้ดูแล"],
  ["turtle","ที่ปรึกษา"],
  ["qilin","ผู้ปกป้อง"]
 ]
}
];

let index=0;
let score={dragon:0,tiger:0,phoenix:0,turtle:0,qilin:0};

function loadQuestion(){
 document.getElementById("question").innerText=questions[index].q;
 document.getElementById("animalImg").src=questions[index].img;
 let html="";
 questions[index].a.forEach(i=>{
  html+=`<div class="option">
  <input type="radio" name="ans" value="${i[0]}"> ${i[1]}
  </div>`;
 });
 document.getElementById("options").innerHTML=html;
}

function nextQuestion(){
 let s=document.querySelector("input[name=ans]:checked");
 if(!s) return alert("กรุณาเลือกคำตอบ");
 score[s.value]++;
 index++;
 index<questions.length?loadQuestion():showResult();
}

function showResult(){
 let r=Object.keys(score).reduce((a,b)=>score[a]>score[b]?a:b);
 let text={
 dragon:"🐉 มังกร (龙 Lóng)<br>ผู้นำ มีพลัง อำนาจ",
 tiger:"🐯 เสือขาว (白虎 Bái Hǔ)<br>กล้าหาญ เด็ดเดี่ยว",
 phoenix:"🔥 หงส์แดง (凤凰 Fèng Huáng)<br>สง่างาม เมตตา",
 turtle:"🐢 เต่าดำ (玄武 Xuán Wǔ)<br>สุขุม รอบคอบ",
 qilin:"🐍 กิเลน (麒麟 Qí Lín)<br>โชคดี ปัญญา ยุติธรรม"
 };
 document.getElementById("quiz").innerHTML=
 `<h2>ผลลัพธ์ของคุณ</h2><p>${text[r]}</p>`;
}

loadQuestion();
</script>

</body>
</html>
