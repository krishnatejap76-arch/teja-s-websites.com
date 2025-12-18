<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Programming Notes Access</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #ffffff;
            color: #333333;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .payment-container, .secret-container, .notes-container {
            text-align: center;
            max-width: 500px;
            width: 100%;
        }
        
        .payment-box, .secret-box {
            background: linear-gradient(145deg, #f8f9fa, #e9ecef);
            border-radius: 20px;
            padding: 40px;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            border: 2px solid #dee2e6;
        }
        
        h1 {
            color: #495057;
            margin-bottom: 30px;
            font-size: 2.5em;
            font-weight: 400;
        }
        
        .upi-id {
            background: #e3f2fd;
            padding: 20px;
            border-radius: 15px;
            font-size: 1.8em;
            font-weight: 600;
            color: #1976d2;
            margin: 20px 0;
            border: 2px solid #bbdefb;
            word-break: break-all;
        }
        
        .verify-section {
            margin-top: 20px;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 15px;
            border: 2px solid #dee2e6;
        }
        
        .txn-input {
            padding: 15px;
            font-size: 1.1em;
            border: 2px solid #dee2e6;
            border-radius: 10px;
            width: 100%;
            max-width: 350px;
            margin: 10px 0;
            text-align: center;
        }
        
        .verify-button {
            background: linear-gradient(145deg, #28a745, #20c997);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.2em;
            border-radius: 50px;
            cursor: pointer;
            margin-top: 10px;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(40, 167, 69, 0.4);
        }
        
        .verify-button:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(40, 167, 69, 0.6);
        }
        
        .verify-button:disabled {
            background: #6c757d;
            cursor: not-allowed;
            transform: none;
        }
        
        .secret-section {
            position: absolute;
            top: 20px;
            right: 20px;
        }
        
        .settings-icon {
            font-size: 1.8em;
            color: #adb5bd;
            cursor: pointer;
            transition: all 0.3s ease;
            padding: 10px;
            border-radius: 50%;
            background: rgba(255,255,255,0.8);
        }
        
        .settings-icon:hover {
            color: #495057;
            background: #f8f9fa;
            transform: scale(1.1) rotate(90deg);
        }
        
        .secret-input {
            padding: 15px;
            font-size: 1.1em;
            border: 2px solid #dee2e6;
            border-radius: 10px;
            width: 80%;
            max-width: 300px;
            margin: 10px 0;
        }
        
        .secret-button {
            background: linear-gradient(145deg, #28a745, #20c997);
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 1.1em;
            border-radius: 25px;
            cursor: pointer;
            margin-top: 10px;
        }
        
        .notes-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        
        .note-card {
            background: linear-gradient(145deg, #f8f9fa, #e9ecef);
            border-radius: 15px;
            padding: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid #dee2e6;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
        }
        
        .note-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.15);
            border-color: #adb5bd;
        }
        
        .note-title {
            font-size: 1.3em;
            color: #495057;
            margin-bottom: 10px;
            font-weight: 500;
        }
        
        .hidden {
            display: none !important;
        }
        
        .payment-verified {
            background: linear-gradient(145deg, #d4edda, #c3e6cb) !important;
            border-color: #28a745 !important;
        }
        
        .status-message {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: 500;
            font-size: 1.1em;
        }
        
        .status-success {
            background: #d4edda;
            color: #155724;
            border: 2px solid #c3e6cb;
        }
        
        .status-error {
            background: #f8d7da;
            color: #721c24;
            border: 2px solid #f5c6cb;
        }
        
        @media (max-width: 768px) {
            h1 { font-size: 2em; }
            .payment-box, .secret-box { padding: 30px 20px; }
            .notes-grid { grid-template-columns: 1fr; }
            .secret-section { top: 10px; right: 10px; }
            .settings-icon { font-size: 1.5em; }
        }
    </style>
</head>
<body>
    <!-- Payment Page -->
    <div id="paymentPage" class="payment-container">
        <div class="secret-section">
            <div class="settings-icon" onclick="toggleSecret()" title="Settings">⚙️</div>
        </div>
        
        <div class="payment-box" id="paymentBox">
            <h1>Programming Notes</h1>
            <p>Pay ₹49 to unlock all notes instantly</p>
            <div class="upi-id">9959172924@fam</div>
            
            <div class="verify-section">
                <p><strong>Enter UPI Transaction ID</strong> (from your payment app)</p>
                <input type="text" id="txnInput" class="txn-input" placeholder="TXN123456789..." maxlength="50">
                <br>
                <button class="verify-button" id="verifyButton" onclick="verifyTransaction()">Verify Payment</button>
                <div id="statusMessage" class="status-message" style="display: none;"></div>
            </div>
        </div>
    </div>
    
    <!-- Secret Code Input -->
    <div id="secretPage" class="secret-container hidden">
        <div class="secret-box">
            <h1>Enter Access Code</h1>
            <input type="text" id="secretInput" class="secret-input" placeholder="Enter code..." maxlength="20">
            <br>
            <button class="secret-button" onclick="checkSecret()">Verify Code</button>
            <br><br>
            <button class="pay-button" onclick="showPayment()">Back to Payment</button>
        </div>
    </div>
    
    <!-- Notes Page -->
    <div id="notesPage" class="notes-container hidden">
        <div style="margin-bottom: 30px;">
            <button class="pay-button" onclick="showPayment()" style="background: #6c757d;">← Back</button>
        </div>
        
        <h1>All Notes Unlocked</h1>
        <p>Select any note to view PDF</p>
        
        <div class="notes-grid">
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1EYPvPowbmdGhMY7j5FU_KfIkpq6-Le0D/view?usp=drivesdk')">
                <div class="note-title">Node.js Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1HSyoM1FdThM6bEr2nlFM8UrnKfo2pvWN/view?usp=drivesdk')">
                <div class="note-title">SQL Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1Mn5PaY9J6QzhyIgR9yXFMBxUtmfGuJ5e/view?usp=drivesdk')">
                <div class="note-title">MongoDB Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1zbAwVtqRjnw-PKa7SwOkDC4icW7Wj8EJ/view?usp=drivesdk')">
                <div class="note-title">React JS Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1491Xtw59gCOVzLL_b8nXB-D1m9UZNiTN/view?usp=drivesdk')">
                <div class="note-title">Python Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1yZ76wNM5_bIEM2_lvt_BUKfI3HhX84TF/view?usp=drivesdk')">
                <div class="note-title">Java Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1f3TyjLwFca5OVBgOnHsNW64pN4yo6QE2/view?usp=drivesdk')">
                <div class="note-title">CSS Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1J7sMPMxbqkrqJ8eJ_rO0BIcwrgGNU4as/view?usp=drivesdk')">
                <div class="note-title">HTML Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1xRDptNkN_9UgJyp3yA58cBR8TkmJjc9-/view?usp=drivesdk')">
                <div class="note-title">JavaScript Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/198R9ZWzp_CsSqn2PwUVqtTMDd9DeHXlj/view?usp=drivesdk')">
                <div class="note-title">DSA Handwritten Notes</div>
            </div>
            <div class="note-card" onclick="openPDF('https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/view?usp=drivesdk')">
                <div class="note-title">C Handwritten Notes</div>
            </div>
        </div>
    </div>
    
    <script>
        const SECRET_CODE = "vamsi jacks SVT";
        const VERIFIED_TXNS = new Set(); // Store verified transaction IDs
        
        function verifyTransaction() {
            const txnInput = document.getElementById('txnInput');
            const verifyButton = document.getElementById('verifyButton');
            const statusMessage = document.getElementById('statusMessage');
            const paymentBox = document.getElementById('paymentBox');
            
            const txnId = txnInput.value.trim().toUpperCase();
            
            if (!txnId) {
                showStatus('Please enter Transaction ID', 'error');
                return;
            }
            
            // Check if already verified
            if (VERIFIED_TXNS.has(txnId)) {
                showStatus('✅ This transaction is already verified!', 'success');
                setTimeout(accessNotes, 1000);
                return;
            }
            
            // Simulate UPI payment verification (12-digit UPI format check)
            if (/^[A-Z0-9]{12,50}$/.test(txnId)) {
                VERIFIED_TXNS.add(txnId);
                showStatus(`✅ Payment verified! TXN: ${txnId.substring(0,8)}...`, 'success');
                verifyButton.textContent = '✓ Verified';
                verifyButton.disabled = true;
                paymentBox.classList.add('payment-verified');
                
                // Auto unlock
                setTimeout(accessNotes, 1500);
            } else {
                showStatus('❌ Invalid Transaction ID format. Must be 12+ alphanumeric characters.', 'error');
                txnInput.focus();
            }
        }
        
        function showStatus(message, type) {
            const status = document.getElementById('statusMessage');
            status.textContent = message;
            status.className = `status-message ${type}`;
            status.style.display = 'block';
        }
        
        function accessNotes() {
            document.getElementById('paymentPage').classList.add('hidden');
            document.getElementById('notesPage').classList.remove('hidden');
        }
        
        function toggleSecret() {
            document.getElementById('paymentPage').classList.add('hidden');
            document.getElementById('secretPage').classList.remove('hidden');
            document.getElementById('secretInput').focus();
        }
        
        function showPayment() {
            document.getElementById('secretPage').classList.add('hidden');
            document.getElementById('notesPage').classList.add('hidden');
            document.getElementById('paymentPage').classList.remove('hidden');
        }
        
        function checkSecret() {
            const input = document.getElementById('secretInput').value.trim();
            if (input === SECRET_CODE) {
                document.getElementById('secretPage').classList.add('hidden');
                document.getElementById('notesPage').classList.remove('hidden');
            } else {
                alert('❌ Invalid code! Try again.');
                document.getElementById('secretInput').value = '';
                document.getElementById('secretInput').focus();
            }
        }
        
        function openPDF(url) {
            window.open(url, '_blank');
        }
        
        // Enter key support
        document.getElementById('txnInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                verifyTransaction();
            }
        });
        
        document.getElementById('secretInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkSecret();
            }
        });
    </script>
</body>
</html>