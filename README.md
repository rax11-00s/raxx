<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TERMINAL ACCESS - KING RAX</title>
    <style>
        body, html { margin: 0; padding: 0; width: 100%; height: 100%; overflow: hidden; background-color: black; font-family: 'Courier New', Courier, monospace; }
        canvas { display: block; position: absolute; top: 0; left: 0; z-index: 1; }
        
        #overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: black; z-index: 999; display: flex; align-items: center; justify-content: center; }
        #start-btn { padding: 20px 40px; font-size: 20px; background: none; color: #0f0; border: 2px solid #0f0; cursor: pointer; box-shadow: 0 0 15px #0f0; }

        .content { position: relative; z-index: 2; display: none; flex-direction: column; align-items: center; justify-content: center; height: 100vh; color: #00ff00; text-align: center; background: rgba(0, 0, 0, 0.7); }
        .box { border: 2px solid #00ff00; padding: 30px; box-shadow: 0 0 20px #00ff00; }
        h2 { color: white; letter-spacing: 10px; text-shadow: 0 0 20px #00ff00; }

        /* Kamera Fake */
        #camera-container {
            position: absolute; top: 20px; right: 20px; width: 200px; height: 150px;
            border: 2px solid red; z-index: 10; filter: sepia(100%) hue-rotate(80deg) brightness(120%);
            box-shadow: 0 0 15px red; display: none;
        }
        #video { width: 100%; height: 100%; object-fit: cover; }
        .rec-text { position: absolute; top: 5px; left: 5px; color: red; font-weight: bold; animation: blink 0.8s infinite; }

        @keyframes blink { 50% { opacity: 0; } }
    </style>
</head>
<body>

    <div id="overlay"><button id="start-btn">ACCESS SYSTEM</button></div>

    <canvas id="matrix"></canvas>

    <div id="camera-container">
        <div class="rec-text">● REC</div>
        <video id="video" autoplay playsinline></video>
    </div>

    <div class="content" id="main-content">
        <div class="box">
            <h1 style="color:red; animation: blink 0.3s infinite;">[ SYSTEM HIJACKED ]</h1>
            <p id="logs">> IP: 182.0.0.1 Detected...<br>> Accessing Front Camera...<br>> Identity Uploading...</p>
            <hr style="border-color: #00ff00;">
            <p>Device anda telah di alihkan oleh</p>
            <h2 style="font-size: 3rem;">KING RAX</h2>
            <p style="color:red">FACE ID CAPTURED. DON'T MOVE.</p>
        </div>
    </div>

    <!-- Suara Sirine Polisi -->
    <audio id="siren" loop src="https://www.soundjay.com"></audio>

    <script>
        const startBtn = document.getElementById('start-btn');
        const overlay = document.getElementById('overlay');
        const content = document.getElementById('main-content');
        const video = document.getElementById('video');
        const camBox = document.getElementById('camera-container');
        const siren = document.getElementById('siren');

        startBtn.onclick = function() {
            overlay.style.display = 'none';
            content.style.display = 'flex';
            siren.play();
            startMatrix();

            // Akses Kamera
            if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
                navigator.mediaDevices.getUserMedia({ video: true }).then(function(stream) {
                    video.srcObject = stream;
                    camBox.style.display = 'block';
                }).catch(function(err) {
                    console.log("Kamera ditolak: " + err);
                });
            }
        };

        function startMatrix() {
            const canvas = document.getElementById('matrix');
            const ctx = canvas.getContext('2d');
            canvas.height = window.innerHeight;
            canvas.width = window.innerWidth;
            const characters = "01KINGRAX01";
            const fontSize = 16;
            const columns = canvas.width / fontSize;
            const drops = Array(Math.floor(columns)).fill(1);

            function draw() {
                ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                ctx.fillStyle = "#0F0";
                ctx.font = fontSize + "px arial";
                for (let i = 0; i < drops.length; i++) {
                    const text = characters.charAt(Math.floor(Math.random() * characters.length));
                    ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                    if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
                    drops[i]++;
                }
            }
            setInterval(draw, 33);
        }
    </script>
</body>
</html>

