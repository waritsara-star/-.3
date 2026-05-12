<html lang="th">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>เกมวงจรไฟฟ้า ม.3</title>

<style>
    *{
        margin:0;
        padding:0;
        box-sizing:border-box;
        font-family: "Sarabun", sans-serif;
    }

    body{
        background: linear-gradient(135deg,#0f172a,#1e293b);
        color:white;
        min-height:100vh;
        padding:20px;
    }

    .container{
        max-width:1200px;
        margin:auto;
    }

    h1{
        text-align:center;
        margin-bottom:10px;
        font-size:42px;
        color:#facc15;
    }

    .subtitle{
        text-align:center;
        margin-bottom:30px;
        color:#cbd5e1;
    }

    .game-area{
        display:grid;
        grid-template-columns:1fr 1fr;
        gap:25px;
    }

    .card{
        background:#1e293b;
        border-radius:20px;
        padding:25px;
        box-shadow:0 0 20px rgba(0,0,0,0.3);
    }

    h2{
        margin-bottom:15px;
        color:#38bdf8;
    }

    .circuit-box{
        background:#0f172a;
        border-radius:15px;
        padding:20px;
        min-height:260px;
        position:relative;
        overflow:hidden;
    }

    .wire{
        position:absolute;
        background:#94a3b8;
    }

    .bulb{
        width:50px;
        height:50px;
        border-radius:50%;
        background:#334155;
        border:4px solid #94a3b8;
        position:absolute;
        transition:0.3s;
        box-shadow:0 0 10px transparent;
    }

    .bulb.on{
        background:yellow;
        box-shadow:0 0 25px yellow;
    }

    .battery{
        width:80px;
        height:40px;
        background:#ef4444;
        border-radius:8px;
        position:absolute;
        color:white;
        display:flex;
        align-items:center;
        justify-content:center;
        font-weight:bold;
    }

    .controls{
        margin-top:20px;
        display:flex;
        flex-wrap:wrap;
        gap:10px;
    }

    button{
        padding:12px 18px;
        border:none;
        border-radius:10px;
        cursor:pointer;
        font-size:16px;
        font-weight:bold;
        transition:0.2s;
    }

    .series-btn{
        background:#22c55e;
        color:white;
    }

    .parallel-btn{
        background:#3b82f6;
        color:white;
    }

    .power-btn{
        background:#f59e0b;
        color:white;
    }

    button:hover{
        transform:scale(1.05);
    }

    .question-box{
        margin-top:20px;
        background:#0f172a;
        border-radius:15px;
        padding:20px;
    }

    .choices{
        display:grid;
        gap:12px;
        margin-top:15px;
    }

    .choice{
        background:#334155;
        padding:14px;
        border-radius:10px;
        cursor:pointer;
        transition:0.2s;
    }

    .choice:hover{
        background:#475569;
    }

    .score{
        font-size:24px;
        color:#facc15;
        margin-top:10px;
    }

    .info{
        margin-top:15px;
        line-height:1.8;
        color:#cbd5e1;
    }

    .result{
        margin-top:15px;
        font-size:20px;
        font-weight:bold;
    }

    @media(max-width:900px){
        .game-area{
            grid-template-columns:1fr;
        }
    }
</style>
</head>

<body>

<div class="container">

    <h1>⚡ เกมวงจรไฟฟ้า ม.3 ⚡</h1>
    <p class="subtitle">
        เรียนรู้วงจรไฟฟ้าแบบอนุกรมและแบบขนานผ่านเกมแสนสนุก
    </p>

    <div class="game-area">

        <!-- ซ้าย -->
        <div class="card">

            <h2>🔌 จำลองวงจรไฟฟ้า</h2>

            <div class="circuit-box" id="circuitBox">

                <!-- Battery -->
                <div class="battery" style="left:20px; top:100px;">
                    Battery
                </div>

                <!-- Bulbs -->
                <div class="bulb" id="bulb1" style="left:220px; top:40px;"></div>
                <div class="bulb" id="bulb2" style="left:220px; top:160px;"></div>

            </div>

            <div class="controls">
                <button class="series-btn" onclick="setSeries()">
                    วงจรอนุกรม
                </button>

                <button class="parallel-btn" onclick="setParallel()">
                    วงจรขนาน
                </button>

                <button class="power-btn" onclick="togglePower()">
                    เปิด / ปิด สวิตช์
                </button>
            </div>

            <div class="info" id="infoText">
                เลือกรูปแบบวงจรเพื่อเริ่มเรียนรู้
            </div>

        </div>

        <!-- ขวา -->
        <div class="card">

            <h2>🎮 Quiz Challenge</h2>

            <div class="question-box">

                <div id="question">
                    วงจรใดถ้าหลอดไฟดวงหนึ่งดับ ดวงอื่นจะดับทั้งหมด?
                </div>

                <div class="choices">
                    <div class="choice" onclick="checkAnswer(this,true)">
                        วงจรอนุกรม
                    </div>

                    <div class="choice" onclick="checkAnswer(this,false)">
                        วงจรขนาน
                    </div>
                </div>

                <div class="result" id="result"></div>

                <div class="score">
                    คะแนน: <span id="score">0</span>
                </div>

            </div>

            <div class="info">
                <b>ความรู้เพิ่มเติม</b><br><br>

                🔹 วงจรอนุกรม:
                กระแสไฟฟ้าไหลได้เพียงทางเดียว
                ถ้าหลอดหนึ่งดับ ทุกดวงดับทั้งหมด
                <br><br>

                🔹 วงจรขนาน:
                กระแสไฟฟ้ามีหลายเส้นทาง
                ถ้าหลอดหนึ่งดับ ดวงอื่นยังติดได้
            </div>

        </div>

    </div>

</div>

<script>

let powerOn = false;
let currentMode = "";

const bulb1 = document.getElementById("bulb1");
const bulb2 = document.getElementById("bulb2");
const infoText = document.getElementById("infoText");

function setSeries(){

    currentMode = "series";

    document.getElementById("circuitBox").innerHTML = `
        <div class="battery" style="left:20px; top:100px;">
            Battery
        </div>

        <div class="wire" style="width:170px;height:6px;left:90px;top:60px;"></div>
        <div class="wire" style="width:170px;height:6px;left:90px;top:180px;"></div>

        <div class="wire" style="width:6px;height:120px;left:260px;top:60px;"></div>

        <div class="bulb ${powerOn ? 'on' : ''}" id="bulb1"
        style="left:220px; top:40px;"></div>

        <div class="bulb ${powerOn ? 'on' : ''}" id="bulb2"
        style="left:220px; top:160px;"></div>
    `;

    infoText.innerHTML = `
        <b>วงจรอนุกรม</b><br>
        กระแสไฟฟ้าไหลในเส้นทางเดียว
        หากหลอดใดหลอดหนึ่งดับ วงจรจะขาดและหลอดทั้งหมดดับ
    `;
}

function setParallel(){

    currentMode = "parallel";

    document.getElementById("circuitBox").innerHTML = `
        <div class="battery" style="left:20px; top:100px;">
            Battery
        </div>

        <div class="wire" style="width:120px;height:6px;left:90px;top:100px;"></div>

        <div class="wire" style="width:6px;height:80px;left:210px;top:40px;"></div>
        <div class="wire" style="width:6px;height:80px;left:210px;top:120px;"></div>

        <div class="bulb ${powerOn ? 'on' : ''}" id="bulb1"
        style="left:240px; top:30px;"></div>

        <div class="bulb ${powerOn ? 'on' : ''}" id="bulb2"
        style="left:240px; top:150px;"></div>
    `;

    infoText.innerHTML = `
        <b>วงจรขนาน</b><br>
        กระแสไฟฟ้ามีหลายเส้นทาง
        หากหลอดไฟดวงหนึ่งดับ ดวงอื่นยังทำงานได้
    `;
}

function togglePower(){

    powerOn = !powerOn;

    if(currentMode === "series"){
        setSeries();
    }
    else if(currentMode === "parallel"){
        setParallel();
    }
    else{
        alert("กรุณาเลือกวงจรก่อน");
    }
}

let score = 0;

function checkAnswer(element,correct){

    const result = document.getElementById("result");

    if(correct){
        result.innerHTML = "✅ ถูกต้อง!";
        result.style.color = "#22c55e";
        score += 10;
    }else{
        result.innerHTML = "❌ ยังไม่ถูก";
        result.style.color = "#ef4444";
    }

    document.getElementById("score").innerText = score;
}

</script>

</body>
</html>
