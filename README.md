<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Protected PDF Access</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 500px;
            margin: 50px auto;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            text-align: center;
        }
        .container {
            background: rgba(255,255,255,0.1);
            padding: 40px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        }
        input[type="password"] {
            width: 80%;
            padding: 12px;
            margin: 15px 0;
            border: none;
            border-radius: 25px;
            font-size: 16px;
            text-align: center;
        }
        button {
            background: #ff6b6b;
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
        }
        button:hover {
            background: #ff5252;
            transform: translateY(-2px);
        }
        .hidden {
            display: none;
        }
        .pdf-container {
            margin-top: 20px;
        }
        .pdf-container iframe {
            width: 100%;
            height: 600px;
            border: none;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🔒 Protected Document</h1>
        <p>Enter the access key to view the PDF:</p>
        
        <input type="password" id="keyInput" placeholder="Enter key code..." maxlength="20">
        <br>
        <button onclick="checkKey()">Unlock Document</button>
        
        <div id="pdfContainer" class="pdf-container hidden">
            <h2>✅ Access Granted</h2>
            <iframe src="https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/preview" 
                    allowfullscreen></iframe>
        </div>
    </div>

    <script>
        function checkKey() {
            const input = document.getElementById('keyInput').value.trim();
            const correctKey = "vamsi jacks";
            
            if (input === correctKey) {
                document.getElementById('pdfContainer').classList.remove('hidden');
                document.getElementById('keyInput').style.display = 'none';
                document.querySelector('button').style.display = 'none';
            } else {
                alert('❌ Incorrect key! Try again.');
                document.getElementById('keyInput').value = '';
                document.getElementById('keyInput').focus();
            }
        }
        
        // Allow Enter key to submit
        document.getElementById('keyInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkKey();
            }
        });
        
        // Auto-focus on load
        window.onload = function() {
            document.getElementById('keyInput').focus();
        }
    </script>
</body>
</html>