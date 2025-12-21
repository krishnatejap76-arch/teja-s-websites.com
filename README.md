<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ultimate Notes for Programmers</title>

    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; padding: 20px; color: #333; }
        .container { max-width: 900px; margin: 0 auto; background: rgba(255, 255, 255, 0.95); border-radius: 20px; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1); overflow: hidden; animation: fadeInUp 1s ease-out; }
        
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .top-bar { display: flex; justify-content: flex-end; align-items: center; padding: 10px 20px; background: rgba(255,255,255,0.9); border-bottom: 1px solid #eee; }
        .settings-btn { background: #f0f0f0; border: none; font-size: 20px; cursor: pointer; color: #555; padding: 8px 15px; border-radius: 10px; transition: 0.3s; }
        .settings-btn:hover { background: #e0e0e0; }

        .header { background: linear-gradient(135deg, #ff6b6b, #feca57); padding: 40px 30px; text-align: center; color: white; }
        .header h1 { font-size: 2.2rem; margin-bottom: 10px; text-shadow: 2px 2px 4px rgba(0,0,0,0.2); }

        .payment-section { padding: 30px; display: flex; flex-wrap: wrap; gap: 25px; justify-content: center; }
        .payment-card, .info-card { background: white; border-radius: 18px; box-shadow: 0 8px 25px rgba(0,0,0,0.05); padding: 25px; flex: 1 1 300px; }
        
        .amount { font-size: 2.5rem; color: #28a745; font-weight: bold; margin: 10px 0; }
        .upi-id { background: #f8f9fa; padding: 10px; border-radius: 8px; border: 1px dashed #667eea; color: #2c5aa0; font-weight: 600; margin-bottom: 15px; text-align: center; }
        
        .qr-wrapper { text-align: center; margin-bottom: 20px; }
        .qr-wrapper img { max-width: 180px; border-radius: 12px; border: 5px solid #f8f9fa; }

        .field-group { margin-bottom: 12px; text-align: left; }
        .field-label { font-size: 0.85rem; font-weight: 600; color: #666; margin-left: 5px; }
        input { width: 100%; padding: 12px; border: 2px solid #eee; border-radius: 10px; outline: none; transition: 0.3s; }
        input:focus { border-color: #667eea; }

        .btn { background: linear-gradient(135deg, #25D366, #128C7E); color: white; border: none; padding: 15px; border-radius: 10px; font-size: 1rem; font-weight: 600; cursor: pointer; width: 100%; transition: 0.3s; display: flex; align-items: center; justify-content: center; gap: 10px; }
        .btn:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(37, 211, 102, 0.4); }

        .success-box { display: none; margin-top: 15px; padding: 15px; border-radius: 10px; background: #e7f3ff; color: #004085; font-size: 0.9rem; line-height: 1.4; border: 1px solid #b8daff; }

        /* Notes (Hidden) */
        .notes-wrapper { display: none; padding: 30px; }
        .note-item { display: flex; justify-content: space-between; align-items: center; padding: 15px; margin-bottom: 10px; background: #fff; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.05); border-left: 5px solid #667eea; }
        .note-link { background: #667eea; color: white; padding: 8px 15px; text-decoration: none; border-radius: 8px; font-size: 0.9rem; }

        /* Modal */
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.6); z-index: 1000; justify-content: center; align-items: center; }
        .modal-content { background: white; padding: 30px; border-radius: 20px; width: 90%; max-width: 400px; text-align: center; }
        .modal-content h3 { margin-bottom: 15px; }
        .modal-buttons { display: flex; gap: 10px; margin-top: 20px; }

        footer { text-align: center; padding: 20px; color: rgba(255,255,255,0.8); font-size: 0.9rem; }
    </style>
</head>
<body>

<div class="container">
    <div class="top-bar">
        <button class="settings-btn" onclick="openCodeModal()">Unlock with Code 🔑</button>
    </div>

    <header class="header">
        <h1>Premium Programmer Notes</h1>
        <p>Handwritten resources to ace your coding journey.</p>
    </header>

    <section class="payment-section" id="paymentSection">
        <div class="payment-card">
            <div class="qr-wrapper">
                <img src="https://drive.google.com/uc?export=view&id=1XzCq_3PSP2ZeWDEwXfoBWD_XlQDYjOuw" alt="UPI QR">
            </div>
            <div class="upi-id">9959172924@fam</div>
            <div class="amount">₹29</div>

            <div class="field-group">
                <span class="field-label">Name</span>
                <input type="text" id="userName" placeholder="Enter your name">
            </div>
            <div class="field-group">
                <span class="field-label">Transaction ID</span>
                <input type="text" id="txnId" placeholder="Paste UPI Ref No. here">
            </div>

            <button class="btn" onclick="sendWhatsAppRequest()">
                <span>Proceed to WhatsApp</span>
            </button>

            <div class="success-box" id="successBox">
                <strong>Next Step:</strong> WhatsApp will open. Tap <b>'Send'</b> to share your payment proof. Once I verify, I will reply with your unlock code!
            </div>
        </div>

        <div class="info-card">
            <h3>How to Access</h3>
            <ul style="margin: 15px 0; line-height: 1.8; color: #555;">
                <li>✅ Pay ₹29 via QR or UPI.</li>
                <li>✅ Enter Name & Txn ID on the left.</li>
                <li>✅ Click the green button to message me.</li>
                <li>✅ Wait for my <b>Approval Code</b> on WhatsApp.</li>
                <li>✅ Click "Unlock with Code" at the top.</li>
            </ul>
            <p style="font-size: 0.8rem; color: #888;">*Verification usually takes 5-10 minutes.</p>
        </div>
    </section>

    <section class="notes-wrapper" id="notesWrapper">
        <h2 style="margin-bottom: 20px;">Unlocked Resources</h2>
        <div class="note-item"><span>Node.js Notes</span><a href="YOUR_LINK" class="note-link">View PDF</a></div>
        <div class="note-item"><span>React JS Notes</span><a href="YOUR_LINK" class="note-link">View PDF</a></div>
        <div class="note-item"><span>Python Notes</span><a href="YOUR_LINK" class="note-link">View PDF</a></div>
        <div class="note-item"><span>DSA Notes</span><a href="YOUR_LINK" class="note-link">View PDF</a></div>
        </section>
</div>

<footer>Written by Krishnateja.P</footer>

<div class="modal" id="codeModal">
    <div class="modal-content">
        <h3>Enter Access Code</h3>
        <p style="margin-bottom: 15px; color: #666;">Enter the code you received on WhatsApp.</p>
        <input type="text" id="secretCodeInput" placeholder="Code (e.g. ABCD-APPROVED)">
        <div class="modal-buttons">
            <button class="btn" style="background: #667eea;" onclick="checkAccessCode()">Unlock Now</button>
            <button class="btn" style="background: #ccc;" onclick="closeCodeModal()">Cancel</button>
        </div>
    </div>
</div>

<script>
    function sendWhatsAppRequest() {
        const name = document.getElementById('userName').value.trim();
        const txn  = document.getElementById('txnId').value.trim();
        
        if (!name || !txn) {
            alert("Please fill in your Name and Transaction ID.");
            return;
        }

        const myNumber = "919959172924";
        const message = `*PAYMENT NOTIFICATION*%0A*Name:* ${name}%0A*Transaction ID:* ${txn}%0A*Amount:* ₹29%0A--------------------------%0A_I have paid. Please verify and send the access code._`;
        
        window.open(`https://wa.me/${myNumber}?text=${message}`, '_blank');
        document.getElementById('successBox').style.display = "block";
    }

    function openCodeModal() { document.getElementById('codeModal').style.display = "flex"; }
    function closeCodeModal() { document.getElementById('codeModal').style.display = "none"; }

    function checkAccessCode() {
        const input = document.getElementById('secretCodeInput').value.trim();
        // You can give users codes like "VAMSI-SVT" or anything ending in "-APPROVED"
        if (input === "vamsi jacks SVT" || input.toUpperCase().endsWith("-APPROVED")) {
            document.getElementById('paymentSection').style.display = "none";
            document.getElementById('notesWrapper').style.display = "block";
            closeCodeModal();
            alert("Access Granted! Enjoy your notes.");
        } else {
            alert("Invalid Code. Please wait for admin approval on WhatsApp.");
        }
    }
</script>

</body>
</html>
