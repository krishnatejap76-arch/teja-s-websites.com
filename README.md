<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Premium PDF Access</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ff6b6b 0%, #feca57 50%, #48dbfb 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }
        .main-container {
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }
        .header {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1000;
        }
        .key-icon {
            width: 50px;
            height: 50px;
            background: rgba(255,255,255,0.9);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 20px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
            transition: all 0.3s;
            backdrop-filter: blur(10px);
        }
        .key-icon:hover {
            transform: scale(1.1) rotate(90deg);
            background: white;
            box-shadow: 0 12px 35px rgba(0,0,0,0.4);
        }
        .key-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 2000;
            backdrop-filter: blur(5px);
        }
        .key-modal.active { display: flex; }
        .key-container {
            background: rgba(255,255,255,0.95);
            margin: auto;
            padding: 40px;
            border-radius: 25px;
            text-align: center;
            max-width: 400px;
            width: 90%;
            box-shadow: 0 20px 50px rgba(0,0,0,0.4);
        }
        .payment-section {
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 100px 20px 20px;
            text-align: center;
        }
        .payment-container {
            background: rgba(255,255,255,0.95);
            padding: 50px 40px;
            border-radius: 30px;
            box-shadow: 0 25px 50px rgba(0,0,0,0.3);
            max-width: 500px;
            width: 90%;
            border: 4px solid #ff6b6b;
        }
        .price-tag {
            background: linear-gradient(45deg, #ff6b6b, #ff8e8e);
            color: white;
            padding: 20px 40px;
            border-radius: 50px;
            font-size: 28px;
            font-weight: bold;
            margin: 20px 0;
            display: inline-block;
            box-shadow: 0 15px 40px rgba(255,107,107,0.4);
        }
        .upi-id {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 20px;
            border: 3px dashed #ff6b6b;
            font-size: 22px;
            font-weight: bold;
            color: #333;
            letter-spacing: 2px;
            margin: 30px 0;
            word-break: break-all;
        }
        .qr-placeholder {
            width: 220px;
            height: 220px;
            background: linear-gradient(45deg, #ff6b6b, #feca57);
            border-radius: 20px;
            margin: 30px auto;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            color: white;
            border: 5px dashed rgba(255,255,255,0.6);
            font-weight: bold;
        }
        input[type="text"], input[type="password"] {
            width: 100%;
            padding: 18px;
            margin: 20px 0;
            border: 3px solid #ddd;
            border-radius: 30px;
            font-size: 18px;
            text-align: center;
            backdrop-filter: blur(10px);
        }
        .btn {
            background: linear-gradient(45deg, #4CAF50, #8BC34A);
            color: white;
            border: none;
            padding: 18px 45px;
            border-radius: 30px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            margin: 15px;
            box-shadow: 0 8px 25px rgba(76,175,80,0.4);
            text-decoration: none;
            display: inline-block;
        }
        .btn:hover { transform: translateY(-4px); box-shadow: 0 12px 35px rgba(76,175,80,0.6); }
        .btn-key { background: linear-gradient(45deg, #2196F3, #21CBF3); box-shadow: 0 8px 25px rgba(33,150,243,0.4); }
        .btn-key:hover { box-shadow: 0 12px 35px rgba(33,150,243,0.6); }
        .pdf-page {
            display: none;
            padding: 120px 20px 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        .pdf-container {
            background: white;
            border-radius: 25px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            border-top: 8px solid #4CAF50;
        }
        .success-badge {
            background: #4CAF50;
            color: white;
            padding: 15px 35px;
            border-radius: 30px;
            font-weight: bold;
            font-size: 18px;
            margin-bottom: 25px;
            display: inline-block;
        }
        .pdf-viewer {
            width: 100%;
            height: 70vh;
            border: none;
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
        }
        .controls {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
            margin-top: 30px;
        }
        @media (max-width: 768px) {
            .header { top: 15px; right: 15px; }
            .key-icon { width: 45px; height: 45px; font-size: 18px; }
            .payment-section { padding: 120px 15px 15px; }
            .controls { flex-direction: column; align-items: center; }
            .btn { width: 100%; max-width: 350px; }
            .upi-id { font-size: 18px; }
        }
    </style>
</head>
<body>
    <div class="main-container">
        <!-- Settings/Key Icon (Top Right) -->
        <div class="header">
            <div class="key-icon" onclick="toggleKeyModal()" title="Secret Access">⚙️</div>
        </div>

        <!-- Key Entry Modal -->
        <div id="keyModal" class="key-modal">
            <div class="key-container">
                <h2>🔑 Secret Access</h2>
                <p>Enter key for FREE access:</p>
                <input type="password" id="keyInput" placeholder="Enter secret key..." maxlength="20">
                <button class="btn btn-key" onclick="checkKey()">Unlock PDF</button>
                <button class="btn" onclick="toggleKeyModal()">Close</button>
            </div>
        </div>

        <!-- Payment Section (Full Screen Center) -->
        <div id="paymentSection" class="payment-section">
            <div class="payment-container">
                <h1>📄 Premium PDF Access</h1>
                <div class="price-tag">ONLY ₹49</div>
                <p style="color: #666; font-size: 18px; margin-bottom: 20px;">OR use secret key ⚙️ (top right)</p>
                
                <div class="upi-id">9959172924@fam</div>
                
                <div class="qr-placeholder">
                    📱 UPI QR Code<br>
                    Scan & Pay ₹49
                </div>
                
                <p style="color: #666; margin: 20px 0;">
                    <strong>Pay ₹49 → Enter Transaction ID → Get Access</strong>
                </p>
                
                <input type="text" id="transactionId" placeholder="Enter Transaction ID / UPI Reference #">
                <button class="btn" onclick="verifyPayment()">✅ Verify & Unlock</button>
            </div>
        </div>

        <!-- PDF Page -->
        <div id="pdfPage" class="pdf-page">
            <div class="pdf-container">
                <div class="success-badge">✅ Access Granted!</div>
                <h2>📖 Your PDF Document</h2>
                
                <iframe id="pdfViewer" class="pdf-viewer" 
                        src="https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/preview" 
                        allowfullscreen></iframe>
                
                <div class="controls">
                    <a href="https://drive.google.com/uc?export=download&id=1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t" 
                       class="btn" target="_blank">💾 Download PDF</a>
                    <button class="btn" onclick="printPDF()">🖨️ Print</button>
                    <button class="btn" onclick="toggleFullscreen()">📱 Fullscreen</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        function toggleKeyModal() {
            document.getElementById('keyModal').classList.toggle('active');
        }
        
        function checkKey() {
            const input = document.getElementById('keyInput').value.trim();
            if (input === "vamsi jacks") {
                grantAccess();
                toggleKeyModal();
            } else {
                alert('❌ Wrong key! Try: "vamsi jacks SVT"');
                document.getElementById('keyInput').value = '';
            }
        }
        
        function verifyPayment() {
            const transactionId = document.getElementById('transactionId').value.trim();
            if (transactionId.length < 5) {
                alert('❌ Enter valid Transaction ID');
                return;
            }
            if (confirm(`Verify ₹49 payment?
Transaction: ${transactionId}`)) {
                grantAccess();
            }
        }
        
        function grantAccess() {
            document.getElementById('paymentSection').style.display = 'none';
            document.getElementById('pdfPage').style.display = 'block';
            document.getElementById('pdfViewer').src = 
                "https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/preview";
        }
        
        function printPDF() {
            window.open('https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/preview');
        }
        
        function toggleFullscreen() {
            const viewer = document.getElementById('pdfViewer');
            if (viewer.requestFullscreen) viewer.requestFullscreen();
            else if (viewer.webkitRequestFullscreen) viewer.webkitRequestFullscreen();
            else if (viewer.msRequestFullscreen) viewer.msRequestFullscreen();
        }
        
        // Enter key support
        document.getElementById('keyInput').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') checkKey();
        });
        document.getElementById('transactionId').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') verifyPayment();
        });
        
        window.onload = () => {
            document.getElementById('transactionId').focus();
        }
    </script>
</body>
</html>