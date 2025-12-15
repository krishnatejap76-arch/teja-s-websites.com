<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Paid PDF Access - ₹49</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #ff6b6b 0%, #feca57 50%, #48dbfb 100%);
            min-height: 100vh;
        }
        .payment-page {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
        }
        .payment-container {
            background: rgba(255,255,255,0.95);
            padding: 40px;
            border-radius: 25px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
            max-width: 450px;
            width: 90%;
            border: 3px solid #ff6b6b;
        }
        .pdf-page {
            display: none;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        .price-tag {
            background: linear-gradient(45deg, #ff6b6b, #ff8e8e);
            color: white;
            padding: 15px 30px;
            border-radius: 50px;
            font-size: 24px;
            font-weight: bold;
            margin: 20px 0;
            display: inline-block;
            box-shadow: 0 10px 30px rgba(255,107,107,0.4);
        }
        h1 { color: #333; margin-bottom: 10px; }
        h2 { color: #333; margin-bottom: 20px; }
        .upi-id {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 15px;
            border: 2px dashed #ff6b6b;
            font-size: 20px;
            font-weight: bold;
            color: #333;
            letter-spacing: 2px;
            margin: 20px 0;
            word-break: break-all;
        }
        .qr-placeholder {
            width: 200px;
            height: 200px;
            background: linear-gradient(45deg, #ff6b6b, #feca57);
            border-radius: 15px;
            margin: 20px auto;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            color: white;
            border: 4px dashed rgba(255,255,255,0.5);
        }
        .btn {
            background: linear-gradient(45deg, #4CAF50, #8BC34A);
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 30px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            margin: 15px;
            box-shadow: 0 5px 15px rgba(76,175,80,0.4);
            text-decoration: none;
            display: inline-block;
        }
        .btn:hover { transform: translateY(-3px); box-shadow: 0 8px 25px rgba(76,175,80,0.6); }
        .btn-danger {
            background: linear-gradient(45deg, #ff6b6b, #ff8e8e);
        }
        .pdf-container {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
            margin-bottom: 20px;
            border-top: 5px solid #4CAF50;
        }
        .pdf-viewer {
            width: 100%;
            height: 70vh;
            border: none;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        .controls {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            margin-top: 25px;
        }
        .success-badge {
            background: #4CAF50;
            color: white;
            padding: 10px 25px;
            border-radius: 25px;
            font-weight: bold;
            margin: 15px 0;
        }
        @media (max-width: 768px) {
            .controls { flex-direction: column; align-items: center; }
            .btn, .upi-id { width: 100%; max-width: 350px; box-sizing: border-box; }
            .payment-container { padding: 30px 20px; }
        }
    </style>
</head>
<body>
    <!-- Payment Page -->
    <div id="paymentPage" class="payment-page">
        <div class="payment-container">
            <h1>📄 Premium PDF Access</h1>
            <div class="price-tag">ONLY ₹49</div>
            <p style="color: #666; font-size: 18px;">Complete payment to unlock document</p>
            
            <div class="upi-id">9959172924@fam</div>
            
            <div class="qr-placeholder">
                📱 UPI QR Code<br>
                (Scan & Pay ₹49)
            </div>
            
            <p style="color: #666;">
                <strong>Instructions:</strong><br>
                1. Pay exactly <strong>₹49</strong> to UPI ID above<br>
                2. Enter <strong>Transaction ID/Ref#</strong> below<br>
                3. Click Verify to access PDF
            </p>
            
            <input type="text" id="transactionId" placeholder="Enter Transaction ID / UPI Reference #" 
                   style="width: 100%; padding: 15px; margin: 20px 0; border: 2px solid #ddd; border-radius: 25px; font-size: 16px; text-align: center;">
            
            <button class="btn" onclick="verifyPayment()">✅ Verify Payment & Unlock</button>
            
            <p style="font-size: 12px; color: #999; margin-top: 20px;">
                💳 Supports: PhonePe, Google Pay, Paytm, BHIM
            </p>
        </div>
    </div>

    <!-- PDF Access Page -->
    <div id="pdfPage" class="pdf-page">
        <div class="pdf-container">
            <div class="success-badge">✅ Payment Verified - Access Granted</div>
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
    </