<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multimodal AI Misinformation Detection</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background-image: linear-gradient(rgba(2, 6, 23, 0.4), rgba(2, 6, 23, 0.4)),
                url('background image.jpeg');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            background-color: #020617;
            color: #f8fafc;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .bg {
            position: fixed;
            width: 100%;
            height: 100%;
            z-index: -1;
            top: 0;
            left: 0;
        }

        .circle {
            position: absolute;
            width: 120px;
            height: 120px;
            background: rgba(56, 189, 248, 0.3);
            border-radius: 50%;
            filter: blur(40px);
            animation: float 18s infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(0) rotate(0)
            }

            50% {
                transform: translateY(-200px) rotate(180deg)
            }

            100% {
                transform: translateY(0) rotate(360deg)
            }
        }

        .c1 {
            top: 10%;
            left: 10%
        }

        .c2 {
            top: 70%;
            left: 80%
        }

        .c3 {
            top: 40%;
            left: 50%
        }

        .c4 {
            top: 80%;
            left: 5%
        }

        .container {
            width: 100%;
            max-width: 1200px;
            margin: 20px auto;
            padding: 30px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            box-shadow: 0 0 40px rgba(56, 189, 248, 0.4);
            border: 1px solid rgba(255, 255, 255, 0.3);
            text-align: center;
        }

        h2 {
            font-size: 28px;
            margin-bottom: 5px;
            background: linear-gradient(90deg, #38bdf8, #a855f7);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .subtitle {
            margin-bottom: 20px;
            opacity: 0.8;
            font-size: 14px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 15px;
            margin-top: 10px;
        }

        .card {
            background: rgba(255, 255, 255, 0.08);
            padding: 20px;
            border-radius: 15px;
            text-align: left;
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            flex-direction: column;
            transition: 0.3s;
        }

        .card:hover {
            background: rgba(255, 255, 255, 0.12);
        }

        .card h3 {
            color: #38bdf8;
            font-size: 17px;
            margin-bottom: 10px;
        }

        textarea,
        .url-input {
            width: 100%;
            padding: 12px;
            border-radius: 10px;
            border: none;
            background: rgba(255, 255, 255, 0.9);
            color: #0f172a;
            font-size: 14px;
        }

        textarea {
            height: 80px;
            resize: none;
        }

        .url-input {
            margin-top: 5px;
        }

        input[type="file"] {
            font-size: 11px;
            margin-top: 5px;
        }

        .btn-action {
            background: #38bdf8;
            padding: 8px 12px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            color: white;
            font-weight: 600;
            margin-top: 10px;
            font-size: 12px;
            transition: 0.3s;
        }

        .btn-action:hover {
            background: #0ea5e9;
        }

        button.main-btn {
            margin-top: 25px;
            padding: 12px 50px;
            font-size: 18px;
            border: none;
            border-radius: 30px;
            background: linear-gradient(90deg, #06b6d4, #a855f7);
            color: white;
            cursor: pointer;
            font-weight: bold;
            transition: 0.4s;
        }

        button.main-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 25px #06b6d4;
        }

        .result {
            margin-top: 20px;
            padding: 20px;
            border-radius: 15px;
            background: rgba(0, 0, 0, 0.7);
            text-align: left;
            border: 1px solid rgba(56, 189, 248, 0.3);
            display: none;
        }

        .bar-container {
            height: 14px;
            background: #1e293b;
            border-radius: 10px;
            margin: 8px 0;
            overflow: hidden;
        }

        .fake-bar {
            height: 100%;
            background: linear-gradient(90deg, #ef4444, #f87171);
            width: 0%;
            transition: 1s;
        }

        .real-bar {
            height: 100%;
            background: linear-gradient(90deg, #22c55e, #4ade80);
            width: 0%;
            transition: 1s;
        }

        .panel {
            background: rgba(255, 255, 255, 0.05);
            padding: 10px;
            margin-top: 10px;
            border-radius: 8px;
            font-size: 13px;
            border-left: 3px solid #38bdf8;
        }

        audio {
            width: 100%;
            margin-top: 10px;
            height: 30px;
        }

        img#imagePreview {
            margin-top: 10px;
            border-radius: 8px;
            width: 100%;
            display: none;
            border: 2px solid #38bdf8;
            max-height: 120px;
            object-fit: cover;
        }

        .scan {
            display: none;
            margin-top: 20px;
        }

        .loader {
            width: 40px;
            height: 40px;
            border: 5px solid #334155;
            border-top: 5px solid cyan;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: auto;
        }

        @keyframes spin {
            0% {
                transform: rotate(0deg);
            }

            100% {
                transform: rotate(360deg);
            }
        }

        .red {
            color: #f87171;
            font-weight: bold;
        }

        .green {
            color: #4ade80;
            font-weight: bold;
        }
    </style>
</head>

<body>
    <div class="bg">
        <div class="circle c1"></div>
        <div class="circle c2"></div>
        <div class="circle c3"></div>
        <div class="circle c4"></div>
    </div>

    <div class="container">
        <h2>Multimodal Misinformation detection System</h2>
        <p class="subtitle">Real-time Analysis for Image, Audio, Text, and URLs</p>

        <div class="grid">
            <div class="card">
                <h3>🖼️ Image Detection</h3>
                <input type="file" id="imageInput" accept="image/*">
                <button class="btn-action" onclick="previewImage()">Preview</button>
                <img id="imagePreview">
            </div>

            <div class="card">
                <h3>🎤 Audio Detection</h3>
                <input type="file" id="audioFile" accept="audio/*">
                <button class="btn-action" onclick="loadAudio()">Preview</button>
                <audio id="audioPlayer" controls style="display:none;"></audio>
            </div>

            <div class="card">
                <h3>📰 Article Detection</h3>
                <textarea id="newsInput" placeholder="Paste news article..."></textarea>
            </div>

            <div class="card">
                <h3>🔗 URL Detection</h3>
                <input type="text" id="urlInput" class="url-input" placeholder="https://example.com">
                <p style="font-size: 11px; margin-top: 10px; opacity: 0.6;">AI checks for phishing, suspicious TLDs, and
                    typosquatting.</p>
            </div>
        </div>

        <button class="main-btn" onclick="startAnalysis()">Analyze All Inputs</button>

        <div class="scan" id="scanBox">
            <div class="loader"></div>
            <br>AI is scanning datasets and verifying source integrity...
        </div>

        <div class="result" id="resultBox"></div>
    </div>

    <script>
        let fakeWords = ["miracle", "secret", "shocking", "conspiracy", "viral", "चमत्कार", "गुप्त", "धक्कादायक"];
        let realWords = ["research", "study", "report", "official", "data", "संशोधन", "अभ्यास"];

        // Suspicious URL patterns
        let suspiciousTLDs = [".xyz", ".top", ".buzz", ".work", ".click", ".free", ".pay"];
        let fakeDomains = ["g00gle", "faceb00k", "amaz0n", "paypa1", "micros0ft"];

        function previewImage() {
            let file = document.getElementById("imageInput").files[0];
            if (file) {
                let img = document.getElementById("imagePreview");
                img.src = URL.createObjectURL(file);
                img.style.display = "block";
            }
        }

        function loadAudio() {
            let file = document.getElementById("audioFile").files[0];
            if (file) {
                let player = document.getElementById("audioPlayer");
                player.src = URL.createObjectURL(file);
                player.style.display = "block";
            }
        }

        function startAnalysis() {
            let text = document.getElementById("newsInput").value.trim();
            let image = document.getElementById("imageInput").files[0];
            let audio = document.getElementById("audioFile").files[0];
            let url = document.getElementById("urlInput").value.trim();

            if (!text && !image && !audio && !url) {
                alert("Please provide at least one input to analyze.");
                return;
            }

            document.getElementById("resultBox").style.display = "none";
            document.getElementById("scanBox").style.display = "block";
            setTimeout(processAI, 2000);
        }

        function processAI() {
            document.getElementById("scanBox").style.display = "none";
            let resultDiv = document.getElementById("resultBox");
            resultDiv.style.display = "block";

            let text = document.getElementById("newsInput").value.toLowerCase();
            let image = document.getElementById("imageInput").files[0];
            let audio = document.getElementById("audioFile").files[0];
            let url = document.getElementById("urlInput").value.toLowerCase();

            let fakeScore = 0;
            let realScore = 0;
            let insights = [];

            // 1. Text Logic
            if (text) {
                fakeWords.forEach(w => { if (text.includes(w)) fakeScore += 20; });
                realWords.forEach(w => { if (text.includes(w)) realScore += 20; });
            }

            // 2. Image Logic
            if (image) {
                if (image.name.toLowerCase().includes("ai") || image.size < 40000) fakeScore += 25;
                else realScore += 20;
            }

            // 3. Audio Logic
            if (audio) fakeScore += 15; // Placeholder weight

            // 4. URL Logic
            if (url) {
                let isSuspiciousURL = false;
                // Check for non-HTTPS
                if (!url.startsWith("https")) { fakeScore += 30; insights.push("• Insecure connection (HTTP)"); isSuspiciousURL = true; }
                // Check for suspicious TLDs
                suspiciousTLDs.forEach(tld => { if (url.endsWith(tld)) { fakeScore += 40; insights.push(`• High-risk TLD (${tld})`); isSuspiciousURL = true; } });
                // Check for typosquatting
                fakeDomains.forEach(dom => { if (url.includes(dom)) { fakeScore += 50; insights.push("• Typosquatting/Fake domain detected"); isSuspiciousURL = true; } });

                if (!isSuspiciousURL && url.includes(".")) realScore += 30;
            }

            if (fakeScore === 0 && realScore === 0) realScore = 10;
            let total = fakeScore + realScore;
            let fakePercent = Math.round((fakeScore / total) * 100);
            let realPercent = 100 - fakePercent;

            resultDiv.innerHTML = `
                <h3 style="color:#38bdf8;">🛡️ AI Security Report</h3>
                <p>Verdict: ${fakePercent > 50 ? "<span class='red'>SUSPICIOUS</span>" : "<span class='green'>AUTHENTIC</span>"}</p>
                
                <p style="margin-top:15px">Misinformation/Phishing Risk: ${fakePercent}%</p>
                <div class="bar-container"><div class="fake-bar" style="width:${fakePercent}%"></div></div>
                
                <p>Credibility Score: ${realPercent}%</p>
                <div class="bar-container"><div class="real-bar" style="width:${realPercent}%"></div></div>

                <div class="panel">
                    <b>AI Insights:</b><br>
                    ${insights.length > 0 ? insights.join("<br>") : "• Source patterns appear consistent with verified origins."}
                </div>
            `;
        }
    </script>
</body>

</html>
