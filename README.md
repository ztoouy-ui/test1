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

    <script>
        function matchBoard() {
            // 입력값 가져오기
            const period = document.getElementById('period').value;
            const windDir = document.getElementById('windDir').value;
            const windSpeed = document.getElementById('windSpeed').value;
            const waveState = document.getElementById('waveState').value;

            // 결과를 표시할 div
            const resultDiv = document.getElementById('result');

            // 간단한 로직으로 추천 보드 결정 (예제)
            let recommendation = "추천 보드: ";

            if (waveState === "클린" && windDir === "오프쇼어" && windSpeed <= 5) {
                recommendation += "숏보드";
            } else if (waveState === "흐림" || windSpeed > 5) {
                recommendation += "롱보드";
            } else {
                recommendation += "미니 말리부";
            }

            // 결과 표시
            resultDiv.textContent = recommendation;
            resultDiv.style.display = "block";
        }
    </script>
</body>
</html>