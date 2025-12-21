<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ultimate Notes for Programmers</title>

    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>

    <style>
        /* [Your existing CSS remains exactly the same] */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; padding: 20px; color: #333; }
        .container { max-width: 900px; margin: 0 auto; background: rgba(255, 255, 255, 0.95); border-radius: 20px; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1); overflow: hidden; animation: fadeInUp 1s ease-out; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        .top-bar { display: flex; justify-content: flex-end; align-items: center; padding: 10px 20px; background: rgba(255,255,255,0.9); }
        .settings-btn { background: none; border: none; font-size: 24px; cursor: pointer; color: #555; padding: 6px 10px; }
        .header { background: linear-gradient(135deg, #ff6b6b, #feca57); padding: 40px 30px; text-align: center; color: white; position: relative; overflow: hidden; }
        .header h1 { font-size: 2.5rem; margin-bottom: 10px; position: relative; z-index: 2; text-shadow: 2px 2px 4px rgba(0,0,0,0.3); }
        .payment-section { padding: 30px; display: flex; flex-wrap: wrap; gap: 25px; justify-content: center; align-items: center; }
        .payment-card, .info-card { background: white; border-radius: 18px; box-shadow: 0 8px 25px rgba(0,0,0,0.08); padding: 20px 25px; flex: 1 1 260px; min-width: 260px; }
        .amount { font-size: 2.2rem; color: #28a745; margin: 10px 0 5px; }
        .upi-id { font-size: 1.1rem; margin: 5px 0 15px; color: #2c5aa0; word-break: break-all; }
        .qr-wrapper img { max-width: 210px; width: 100%; border-radius: 16px; }
        input { width: 100%; padding: 12px 14px; margin: 6px 0 10px; border: 2px solid #e0e0e0; border-radius: 10px; font-size: 0.95rem; }
        .btn { background: linear-gradient(135deg, #667eea, #764ba2); color: white; border: none; padding: 13px 20px; border-radius: 10px; font-size: 1rem; cursor: pointer; width: 100%; margin-top: 8px; transition: transform 0.2s; }
        .btn:disabled { background: #ccc; cursor: not-allowed; }
        .success-box { display: none; margin-top: 12px; padding: 12px; border-radius: 10px; background: #d4edda; color: #155724; font-size: 0.9rem; border: 1px solid #c3e6cb; }
        .notes-wrapper { display: none; }
        .notes-list { padding: 10px 30px 30px; }
        .note-item { display: flex; align-items: center; padding: 20px; margin-bottom: 15px; background: white; border-radius: 15px; box-shadow: 0 8px 25px rgba(0,0,0,0.08); animation: slideInLeft 0.6s ease-out forwards; }
        @keyframes slideInLeft { from { transform: translateX(-20px); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
        .note-title { flex: 1; font-size: 1.3rem; font-weight: 600; color: #2d3436; }
        .note-link { background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 10px 20px; text-decoration: none; border-radius: 50px; font-weight: 600; }
        .footer { background: #2d3436; color: white; text-align: center; padding: 18px; font-size: 1rem; }
        .modal { display: none; position: fixed; left: 0; top: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; justify-content: center; align-items: center; }
        .modal-content { background: white; padding: 25px; border-radius: 15px; width: 90%; max-width: 360px; text-align: center; }
        .modal-buttons { display: flex; gap: 10px; margin-top: 10px; }
    </style>
</head>
<body>
<div class="container">
    <div class="top-bar">
        <button class="settings-btn" onclick="openCodeModal()" title="Unlock Notes">⚙️</button>
    </div>

    <header class="header">
        <h1>Ultimate Notes for Programmers</h1>
        <p>Access premium handwritten notes after a small support of ₹29.</p>
    </header>

    <section class="payment-section" id="paymentSection">
        <div class="payment-card">
            <h3 style="margin-bottom:10px;">Pay to Unlock</h3>
            <div class="amount">₹29</div>
            <p class="upi-id">9959172924@fam</p>

            <div class="qr-wrapper">
                <img src="https://drive.google.com/uc?export=view&id=1XzCq_3PSP2ZeWDEwXfoBWD_XlQDYjOuw" alt="QR Code">
            </div>

            <input type="text" id="userName" placeholder="Your Name">
            <input type="email" id="userEmail" placeholder="Your Email">
            <input type="tel" id="userPhone" placeholder="Phone (Optional)">
            <input type="text" id="txnId" placeholder="UPI Transaction ID">

            <button class="btn" id="paidBtn" onclick="sendAccessRequest()">I've paid</button>

            <div class="success-box" id="successBox">
                ✅ Request sent! Check your email soon for the access code.
            </div>
        </div>

        <div class="info-card">
            <h3>How it works</h3>
            <ul style="margin: 15px 0 0 20px; line-height: 1.6;">
                <li>Pay ₹29 to the UPI ID.</li>
                <li>Submit your Transaction ID.</li>
                <li>Wait for the admin to verify.</li>
                <li>Receive code via email.</li>
                <li>Click ⚙️ to enter code and unlock.</li>
            </ul>
        </div>
    </section>

    <section class="notes-wrapper" id="notesWrapper">
        <div class="notes-list">
            <div class="note-item"><div class="note-title">Node.js Notes</div><a href="#" class="note-link">View</a></div>
             <div class="note-item"><div class="note-title">React JS Notes</div><a href="#" class="note-link">View</a></div>
        </div>
    </section>

    <footer class="footer">
        Written by Krishnateja.P
    </footer>
</div>

<div class="modal" id="codeModal">
    <div class="modal-content">
        <h3>Enter Access Code</h3>
        <input type="text" id="secretCodeInput" placeholder="Enter code here">
        <div class="modal-buttons">
            <button class="btn" onclick="checkAccessCode()">Unlock</button>
            <button class="btn" style="background:#6c757d" onclick="closeCodeModal()">Cancel</button>
        </div>
    </div>
</div>

<script>
    // 1. INITIALIZE (Replace with your Public Key)
    (function() {
        emailjs.init("YOUR_PUBLIC_KEY");
    })();

    async function sendAccessRequest() {
        const name  = document.getElementById('userName').value.trim();
        const email = document.getElementById('userEmail').value.trim();
        const phone = document.getElementById('userPhone').value.trim();
        const txnId = document.getElementById('txnId').value.trim();
        const btn   = document.getElementById('paidBtn');
        const box   = document.getElementById('successBox');

        // Validation
        if (!name || !email || !txnId) {
            alert("Please fill in Name, Email, and Transaction ID.");
            return;
        }

        // Email Format check
        if(!email.includes('@')) {
            alert("Please enter a valid email.");
            return;
        }

        btn.disabled = true;
        btn.textContent = "Verifying...";

        const params = {
            to_email: "krishnateiap76@gmail.com",
            user_name: name,
            user_email: email,
            user_phone: phone || "N/A",
            transaction_id: txnId,
            amount: "₹29",
            message: "New access request for Programmer Notes."
        };

        try {
            // 2. SEND (Replace with your Service and Template IDs)
            await emailjs.send("YOUR_SERVICE_ID", "YOUR_TEMPLATE_ID", params);
            
            box.style.display = "block";
            btn.textContent = "Sent Successfully ✅";
            
            // Clear inputs
            document.getElementById('txnId').value = "";
        } catch (err) {
            alert("Failed to send. Check console for error.");
            console.error("EmailJS Error:", err);
            btn.disabled = false;
            btn.textContent = "I've paid";
        }
    }

    function openCodeModal() { document.getElementById('codeModal').style.display = "flex"; }
    function closeCodeModal() { document.getElementById('codeModal').style.display = "none"; }

    function checkAccessCode() {
        const input = document.getElementById('secretCodeInput').value.trim();
        const masterCode = "vamsi jacks SVT";
        
        // Simple Logic: if code is correct OR ends with "-approved"
        if (input === masterCode || input.toLowerCase().endsWith("-approved")) {
            document.getElementById('paymentSection').style.display = "none";
            document.getElementById('notesWrapper').style.display = "block";
            closeCodeModal();
        } else {
            alert("Invalid Code. Please try again.");
        }
    }
</script>
</body>
</html>
