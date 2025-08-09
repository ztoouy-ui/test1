<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>추천 보드</title>
    <style>
        .result {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            background-color: #f9f9f9;
        }
    </style>
</head>
<body>
<h1>🏄‍♂️ 서핑 보드 자동 매칭</h1>
<div class="container">
    <label>파고 (m)</label>
    <input type="number" id="height" step="0.1">
    <label>피리어드 (s)</label>
    <input type="number" id="period" step="0.1">

    <label>바람 방향</label>
    <select id="windDir">
        <option>온쇼어</option>
        <option>오프쇼어</option>
        <option>사이드</option>
        <option>무풍</option>
    </select>

    <label>바람 세기 (m/s)</label>
    <input type="number" id="windSpeed" step="0.1">

    <label>물결 상태</label>
    <select id="waveState">
        <option>클린</option>
        <option>흐림</option>
        <option>초록물</option>
    </select>

    <button onclick="matchBoard()">추천 보드 보기</button>

    <div id="result" class="result" style="display:none;"></div>
</div>

<script>
const boards = [
    { name: "Sharp Eye Synergy", size: "6'0\" 30.5L", tail: "Round Tail", fin: "Thruster", desc: "중~큰 파도 퍼포먼스 숏보드, 파워 있는 클린 페이스에 강함" },
    { name: "Lost Sub Driver 3.0", size: "5'10\" 31.0L", tail: "Squash Tail", fin: "Thruster/Quad", desc: "약~중간 파도 하이브리드 퍼포먼스, 패들력·가속 우수" },
    { name: "Chilli Fade 2.0", size: "5'11\" 30.8L", tail: "Squash Tail", fin: "Thruster", desc: "올라운드 퍼포먼스 숏보드, 다양한 조건 대응 가능" },
    { name: "JS Monsta", size: "6'0\" 30.5L", tail: "Round Tail", fin: "Thruster", desc: "올라운드 퍼포먼스, 중~큰 파도 안정성·드라이브 우수" },
    { name: "Channel Islands Bobby Quad", size: "5'8\" 29.0L", tail: "Swallow Tail", fin: "Quad", desc: "퍼포먼스 피시, 작은~중간 파도 속도·유연성 강점" }
];

function matchBoard() {
    const h = parseFloat(document.getElementById('height').value);
    const p = parseFloat(document.getElementById('period').value);
    const windDir = document.getElementById('windDir').value;
    const windSpeed = parseFloat(document.getElementById('windSpeed').value);
    const waveState = document.getElementById('waveState').value;

    let picks = [];

    if (h <= 1.0 && p <= 8) {
        if (waveState === "클린") picks = [boards[4], boards[1], boards[2]];
        else picks = [boards[4], boards[1]];
    }
    else if (h > 1.0 && h <= 1.3 && p >= 8) {
        if (waveState === "클린") picks = [boards[0], boards[3], boards[2]];
        else picks = [boards[3], boards[1], boards[2]];
    }
    else if (h >= 1.3 && p >= 9) {
        if (waveState === "클린") picks = [boards[0], boards[3]];
        else picks = [boards[3], boards[0]];
    }
    else if (h <= 0.9 && p <= 7 && windSpeed > 5) {
        picks = [boards[4], boards[1]];
    }
    else {
        picks = [boards[2], boards[1], boards[4]]; // 기본 안전 추천
    }

    let html = `<h2>추천 결과</h2>`;
    picks.forEach((b, i) => {
        html += `<div class="board-card">
            <h3>${i+1}순위: ${b.name}</h3>
            <p>${b.size} / ${b.tail} / ${b.fin}</p>
            <p>${b.desc}</p>
            <p class="pin">핀 추천: ${b.fin.includes("Quad") ? "쿼드 Performer" : "Thruster Performer"}</p>
        </div>`;
    });

    document.getElementById('result').innerHTML = html;
    document.getElementById('result').style.display = "block";
    </script>
</body>
</html>