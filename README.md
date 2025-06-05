<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <title>會考預估排名系統</title>
    <style>
        body {
            background-color: #f6f1eb;
            font-family: "Helvetica Neue", Arial, sans-serif;
            color: #4b3832;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }
        select, button {
            margin: 10px;
            padding: 12px;
            font-size: 16px;
            border-radius: 8px;
            border: 1px solid #c8b7a6;
            background-color: #fff;
            width: 250px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        button {
            background-color: #d6c1b1;
            color: #fff;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #a8907d;
        }
        .card {
            background-color: #fff;
            padding: 25px;
            margin-top: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-width: 500px;
            text-align: center;
        }
        .grade {
            font-size: 22px;
            color: #5c4a42;
            margin-bottom: 10px;
        }
        .ranking {
            font-size: 24px;
            font-weight: bold;
            color: #8c6d5d;
            background-color: #f9f5f1;
            padding: 10px;
            border-radius: 8px;
            display: inline-block;
            margin-top: 10px;
        }
        .footer {
            margin-top: 20px;
            font-size: 14px;
            color: #777;
        }
        h1 {
            font-weight: 600;
            font-size: 28px;
            color: #3c2f2f;
            margin-bottom: 30px;
        }
    </style>
</head>
<body>
    <h1>會考預估排名系統</h1>

    <select id="region">
        <option value="">請選擇考區</option>
        <option value="21311">臺北考區</option>
        <option value="29825">新北考區</option>
        <option value="3561">宜蘭考區</option>
        <option value="2392">基隆考區</option>
        <option value="18474">桃園考區</option>
        <option value="14022">竹苗考區</option>
        <option value="29181">中投考區</option>
        <option value="9041">彰化考區</option>
        <option value="4953">雲林考區</option>
        <option value="5169">嘉義考區</option>
        <option value="13373">臺南考區</option>
        <option value="5102">屏東考區</option>
        <option value="18796">高雄考區</option>
        <option value="2400">花蓮考區</option>
        <option value="1472">臺東考區</option>
        <option value="524">澎湖考區</option>
        <option value="589">金門考區</option>
        <option value="80">馬祖考區</option>
    </select>

    <div>
        <select id="chinese">
            <option value="">國文</option>
            <option value="A">A++</option>
            <option value="A">A+</option>
            <option value="A">A</option>
            <option value="B">B++</option>
            <option value="B">B+</option>
            <option value="B">B</option>
            <option value="C">C++</option>
            <option value="C">C+</option>
            <option value="C">C</option>
        </select>
        <select id="math">
            <option value="">數學</option>
            <option value="A">A++</option>
            <option value="A">A+</option>
            <option value="A">A</option>
            <option value="B">B++</option>
            <option value="B">B+</option>
            <option value="B">B</option>
            <option value="C">C++</option>
            <option value="C">C+</option>
            <option value="C">C</option>
        </select>
        <select id="english">
            <option value="">英文</option>
            <option value="A">A++</option>
            <option value="A">A+</option>
            <option value="A">A</option>
            <option value="B">B++</option>
            <option value="B">B+</option>
            <option value="B">B</option>
            <option value="C">C++</option>
            <option value="C">C+</option>
            <option value="C">C</option>
        </select>
        <select id="science">
            <option value="">理化</option>
            <option value="A">A++</option>
            <option value="A">A+</option>
            <option value="A">A</option>
            <option value="B">B++</option>
            <option value="B">B+</option>
            <option value="B">B</option>
            <option value="C">C++</option>
            <option value="C">C+</option>
            <option value="C">C</option>
        </select>
        <select id="social">
            <option value="">社會</option>
            <option value="A">A++</option>
            <option value="A">A+</option>
            <option value="A">A</option>
            <option value="B">B++</option>
            <option value="B">B+</option>
            <option value="B">B</option>
            <option value="C">C++</option>
            <option value="C">C+</option>
            <option value="C">C</option>
        </select>
    </div>

    <button onclick="calculateRank()">計算排名</button>

    <div class="card" id="result" style="display:none;">
        <div id="grade" class="grade"></div>
        <div id="ranking" class="ranking"></div>
    </div>

    <div class="footer">僅供參考</div>

    <script>
        const scoreData = [
            { grade: "5A0B0C", count: 17569 },
            { grade: "4A1B0C", count: 10355 },
            { grade: "4A0B1C", count: 31 },
            { grade: "3A2B0C", count: 10313 },
            { grade: "3A1B1C", count: 90 },
            { grade: "3A0B2C", count: 0 },
            { grade: "2A3B0C", count: 13281 },
            { grade: "2A2B1C", count: 338 },
            { grade: "2A1B2C", count: 17 },
            { grade: "2A0B3C", count: 0 },
            { grade: "1A4B0C", count: 20787 },
            { grade: "1A3B1C", count: 2008 },
            { grade: "1A2B2C", count: 277 },
            { grade: "1A1B3C", count: 62 },
            { grade: "1A0B4C", count: 43 }
        ];

        const totalStudents = 74681;
        const percentData = scoreData.map(d => ({...d, percent: d.count / totalStudents}));

        function calculateRank() {
            const region = document.getElementById("region").value;
            const scores = [
                document.getElementById("chinese").value,
                document.getElementById("math").value,
                document.getElementById("english").value,
                document.getElementById("science").value,
                document.getElementById("social").value
            ];

            if (!region || scores.includes("")) {
                alert("請選擇考區並填寫所有科目成績！");
                return;
            }

            const A = scores.filter(s => s === 'A').length;
            const B = scores.filter(s => s === 'B').length;
            const C = scores.filter(s => s === 'C').length;
            const gradeCombo = `${A}A${B}B${C}C`;

            let cumulative = 0;
            for (let data of percentData) {
                if (data.grade === gradeCombo) {
                    const startPercent = cumulative;
                    const endPercent = cumulative + data.percent;
                    const startRank = Math.floor(region * startPercent) + 1;
                    const endRank = Math.floor(region * endPercent);
                    document.getElementById("grade").innerText = `成績類別：${gradeCombo}`;
                    document.getElementById("ranking").innerText = `預估排名範圍：第 ${startRank} 名 ～ 第 ${endRank} 名`;
                    document.getElementById("result").style.display = "block";
                    return;
                }
                cumulative += data.percent;
            }

            document.getElementById("grade").innerText = `成績類別：${gradeCombo}`;
            document.getElementById("ranking").innerText = `預估排名範圍：無法估算`;
            document.getElementById("result").style.display = "block";
        }
    </script>
</body>
</html>
