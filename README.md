<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Protected PDF Access</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        .login-page {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
        }
        .login-container {
            background: rgba(255,255,255,0.15);
            padding: 40px;
            border-radius: 20px;
            backdrop-filter: blur(15px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.3);
            max-width: 400px;
            width: 90%;
        }
        .pdf-page {
            display: none;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        h1 { color: white; margin-bottom: 10px; }
        h2 { color: #333; margin-bottom: 20px; }
        input[type="password"] {
            width: 100%;
            padding: 15px;
            margin: 20px 0;
            border: none;
            border-radius: 30px;
            font-size: 16px;
            text-align: center;
            background: rgba(255,255,255,0.9);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        .btn {
            background: linear-gradient(45deg, #ff6b6b, #ff8e8e);
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 30px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
            margin: 10px;
            box-shadow: 0 5px 15px rgba(255,107,107,0.4);
        }
        .btn:hover { transform: translateY(-3px); box-shadow: 0 8px 25px rgba(255,107,107,0.6); }
        .btn-success {
            background: linear-gradient(45deg, #4CAF50, #8BC34A);
            box-shadow: 0 5px 15px rgba(76,175,80,0.4);
        }
        .btn-success:hover { box-shadow: 0 8px 25px rgba(76,175,80,0.6); }
        .pdf-container {
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            margin-bottom: 20px;
        }
        .pdf-viewer {
            width: 100%;
            height: 70vh;
            border: none;
            border-radius: 10px;
        }
        .controls {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }
        @media (max-width: 768px) {
            .controls { flex-direction: column; align-items: center; }
            .btn { width: 100%; max-width: 300px; }
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div id="loginPage" class="login-page">
        <div class="login-container">
            <h1>🔒 Protected Document</h1>
            <p style="color: rgba(255,255,255,0.9);">Enter access key to proceed</p>
            <input type="password" id="keyInput" placeholder="Enter key code..." maxlength="20">
            <br>
            <button class="btn" onclick="checkKey()">Unlock Document</button>
        </div>
    </div>

    <!-- PDF Page -->
    <div id="pdfPage" class="pdf-page">
        <div class="pdf-container">
            <h2>✅ Access Granted</h2>
            <p>Document details and controls available below:</p>
            
            <iframe id="pdfViewer" class="pdf-viewer" 
                    src="https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/preview" 
                    allowfullscreen></iframe>
            
            <div class="controls">
                <a href="https://drive.google.com/uc?export=download&id=1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t" 
                   class="btn btn-success" target="_blank">💾 Save PDF</a>
                <button class="btn" onclick="printPDF()">🖨️ Print</button>
                <button class="btn" onclick="toggleFullscreen()">📱 Fullscreen</button>
                <button class="btn" onclick="goBack()">🔙 Back to Lock</button>
            </div>
        </div>
    </div>

    <script>
        const correctKey = "vamsi jacks";
        
        function checkKey() {
            const input = document.getElementById('keyInput').value.trim();
            
            if (input === correctKey) {
                document.getElementById('loginPage').style.display = 'none';
                document.getElementById('pdfPage').style.display = 'block';
                // Load PDF preview
                document.getElementById('pdfViewer').src = 
                    "https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/preview";
            } else {
                alert('❌ Wrong key! Key: "vamsi jacks"');
                document.getElementById('keyInput').value = '';
                document.getElementById('keyInput').focus();
            }
        }
        
        function printPDF() {
            window.open('https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/preview');
        }
        
        function toggleFullscreen() {
            const viewer = document.getElementById('pdfViewer');
            if (viewer.requestFullscreen) {
                viewer.requestFullscreen();
            } else if (viewer.webkitRequestFullscreen) {
                viewer.webkitRequestFullscreen();
            } else if (viewer.msRequestFullscreen) {
                viewer.msRequestFullscreen();
            }
        }
        
        function goBack() {
            document.getElementById('pdfPage').style.display = 'none';
            document.getElementById('loginPage').style.display = 'flex';
            document.getElementById('keyInput').value = '';
            document.getElementById('keyInput').focus();
        }
        
        // Enter key support
        document.getElementById('keyInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') checkKey();
        });
        
        // Auto-focus
        window.onload = function() {
            document.getElementById('keyInput').focus();
        }
    </script>
</body>
</html>