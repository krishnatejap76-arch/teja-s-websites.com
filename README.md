<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ultimate Notes for Programmers</title>

    <!-- EmailJS SDK -->
    <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            animation: fadeInUp 1s ease-out;
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to   { opacity: 1; transform: translateY(0); }
        }

        .top-bar {
            display: flex;
            justify-content: flex-end;
            align-items: center;
            padding: 10px 20px;
            background: rgba(255,255,255,0.9);
        }

        .settings-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #555;
            padding: 6px 10px;
        }

        .settings-btn:hover {
            color: #222;
        }

        .header {
            background: linear-gradient(135deg, #ff6b6b, #feca57);
            padding: 40px 30px;
            text-align: center;
            color: white;
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.3) 0%, transparent 70%);
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: rotate(0deg); }
            50%      { transform: rotate(180deg); }
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            position: relative;
            z-index: 2;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            position: relative;
            z-index: 2;
            font-size: 1.1rem;
        }

        /* PAYMENT SECTION */

        .payment-section {
            padding: 30px;
            display: flex;
            flex-wrap: wrap;
            gap: 25px;
            justify-content: center;
            align-items: center;
        }

        .payment-card,
        .info-card {
            background: white;
            border-radius: 18px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.08);
            padding: 20px 25px;
            flex: 1 1 260px;
            min-width: 260px;
        }

        .payment-title {
            font-size: 1.4rem;
            margin-bottom: 10px;
            color: #2d3436;
        }

        .amount {
            font-size: 2.2rem;
            color: #28a745;
            margin: 10px 0 5px;
        }

        .upi-id {
            font-size: 1.1rem;
            margin: 5px 0 15px;
            color: #2c5aa0;
            word-break: break-all;
        }

        .qr-wrapper {
            text-align: center;
            margin-bottom: 15px;
        }

        .qr-wrapper img {
            max-width: 210px;
            width: 100%;
            border-radius: 16px;
        }

        .field-label {
            font-size: 0.9rem;
            color: #555;
            margin-top: 5px;
        }

        input {
            width: 100%;
            padding: 12px 14px;
            margin: 6px 0 10px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 0.95rem;
        }

        .btn {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 13px 20px;
            border-radius: 10px;
            font-size: 1rem;
            cursor: pointer;
            width: 100%;
            margin-top: 8px;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 15px rgba(102,126,234,0.4);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(102,126,234,0.6);
        }

        .btn:disabled {
            background: #ccc;
            box-shadow: none;
            cursor: not-allowed;
            transform: none;
        }

        .success-box {
            display: none;
            margin-top: 12px;
            padding: 12px;
            border-radius: 10px;
            background: #d4edda;
            color: #155724;
            font-size: 0.9rem;
        }

        .info-card ul {
            margin-left: 18px;
            margin-top: 8px;
        }

        .info-card li {
            margin-bottom: 6px;
            font-size: 0.95rem;
        }

        /* NOTES SECTION (HIDDEN UNTIL CODE) */

        .notes-wrapper {
            display: none;
        }

        .notes-list {
            padding: 10px 30px 30px;
        }

        .note-item {
            display: flex;
            align-items: center;
            padding: 20px;
            margin-bottom: 15px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.08);
            transform: translateX(-20px);
            opacity: 0;
            animation: slideInLeft 0.6s ease-out forwards;
            transition: all 0.3s ease;
            border-left: 5px solid transparent;
        }

        .note-item:hover {
            transform: translateX(5px) scale(1.02);
            box-shadow: 0 15px 35px rgba(0,0,0,0.15);
        }

        .note-item:nth-child(1) { animation-delay: 0.1s; border-left-color: #ff6b6b; }
        .note-item:nth-child(2) { animation-delay: 0.2s; border-left-color: #4ecdc4; }
        .note-item:nth-child(3) { animation-delay: 0.3s; border-left-color: #45b7d1; }
        .note-item:nth-child(4) { animation-delay: 0.4s; border-left-color: #f9ca24; }
        .note-item:nth-child(5) { animation-delay: 0.5s; border-left-color: #6c5ce7; }
        .note-item:nth-child(6) { animation-delay: 0.6s; border-left-color: #fd79a8; }
        .note-item:nth-child(7) { animation-delay: 0.7s; border-left-color: #00b894; }
        .note-item:nth-child(8) { animation-delay: 0.8s; border-left-color: #e17055; }
        .note-item:nth-child(9) { animation-delay: 0.9s; border-left-color: #74b9ff; }
        .note-item:nth-child(10){ animation-delay: 1.0s; border-left-color: #a29bfe; }
        .note-item:nth-child(11){ animation-delay: 1.1s; border-left-color: #fdcb6e; }
        .note-item:nth-child(12){ animation-delay: 1.2s; border-left-color: #00cec9; }

        @keyframes slideInLeft {
            to { transform: translateX(0); opacity: 1; }
        }

        .note-title {
            flex: 1;
            font-size: 1.3rem;
            font-weight: 600;
            color: #2d3436;
            margin-right: 20px;
        }

        .note-link {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 12px 25px;
            text-decoration: none;
            border-radius: 50px;
            font-weight: 600;
            font-size: 0.95rem;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
        }

        .note-link:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.6);
            background: linear-gradient(135deg, #764ba2, #667eea);
        }

        .footer {
            background: linear-gradient(135deg, #2d3436, #636e72);
            color: white;
            text-align: center;
            padding: 18px;
            font-size: 1rem;
            font-weight: 500;
        }

        /* SECRET / APPROVAL CODE MODAL */

        .modal {
            display: none;
            position: fixed;
            left: 0; top: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 999;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background: white;
            padding: 25px 20px;
            border-radius: 15px;
            width: 90%;
            max-width: 360px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }

        .modal-content h3 {
            margin-bottom: 10px;
        }

        .modal-buttons {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .btn-secondary {
            background: #6c757d;
            box-shadow: none;
        }

        @media (max-width: 768px) {
            .header h1 { font-size: 2rem; }
            .payment-section { padding: 20px; }
            .note-item { flex-direction: column; text-align: center; }
            .note-title { margin-right: 0; margin-bottom: 12px; }
        }
    </style>
</head>
<body>
<div class="container">

    <div class="top-bar">
        <!-- Settings-style icon -->
        <button class="settings-btn" onclick="openCodeModal()" title="Settings">⚙️</button>
    </div>

    <header class="header">
        <h1>Ultimate Notes for Programmers</h1>
        <p>Access premium handwritten notes after a small support of ₹29.</p>
    </header>

    <!-- PAYMENT / HOME SECTION -->
    <section class="payment-section" id="paymentSection">
        <div class="payment-card">
            <div class="payment-title">Pay to Unlock Notes</div>
            <div class="amount">₹29</div>
            <div class="field-label">Pay using UPI ID or scan QR:</div>
            <div class="upi-id">9959172924@fam</div>

            <div class="qr-wrapper">
                <!-- QR displayed from your Drive link -->
                <img src="https://drive.google.com/uc?export=view&id=1XzCq_3PSP2ZeWDEwXfoBWD_XlQDYjOuw"
                     alt="UPI QR Code for 9959172924@fam">
            </div>

            <div class="field-label">Your Name</div>
            <input type="text" id="userName" placeholder="Enter your name">

            <div class="field-label">Email (for approval)</div>
            <input type="email" id="userEmail" placeholder="you@example.com">

            <div class="field-label">Phone (optional)</div>
            <input type="tel" id="userPhone" placeholder="Phone number">

            <div class="field-label">Transaction ID (after paying)</div>
            <input type="text" id="txnId" placeholder="Enter UPI transaction ID">

            <button class="btn" id="paidBtn" onclick="sendAccessRequest()">I've paid</button>

            <div class="success-box" id="successBox">
                ✅ Request sent to admin. You will receive an access code after payment is verified.
            </div>
        </div>

        <div class="info-card">
            <div class="payment-title">How this works</div>
            <ul>
                <li>Pay ₹29 to UPI ID 9959172924@fam or scan the QR.</li>
                <li>Enter your details and tap “I've paid”.</li>
                <li>A request email goes to: krishnateiap76@gmail.com.</li>
                <li>After payment is checked and accepted, you receive a unique code.</li>
                <li>Use the ⚙️ icon to enter that code and unlock notes.</li>
                <li>Special users can use personal code: vamsi jacks SVT.</li>
            </ul>
        </div>
    </section>

    <!-- NOTES SECTION (UNLOCKED BY CODE) -->
    <section class="notes-wrapper" id="notesWrapper">
        <div class="notes-list">
            <div class="note-item">
                <div class="note-title">Node.js Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1EYPvPowbmdGhMY7j5FU_KfIkpq6-Le0D/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">SQL Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1HSyoM1FdThM6bEr2nlFM8UrnKfo2pvWN/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">MongoDB Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1Mn5PaY9J6QzhyIgR9yXFMBxUtmfGuJ5e/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">OOPs Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1zbAwVtqRjnw-PKa7SwOkDC4icW7Wj8EJ/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">React JS Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1491Xtw59gCOVzLL_b8nXB-D1m9UZNiTN/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">Python Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1yZ76wNM5_bIEM2_lvt_BUKfI3HhX84TF/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">Java Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1f3TyjLwFca5OVBgOnHsNW64pN4yo6QE2/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">CSS Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1J7sMPMxbqkrqJ8eJ_rO0BIcwrgGNU4as/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">HTML Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1xRDptNkN_9UgJyp3yA58cBR8TkmJjc9-/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">JavaScript Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">DSA Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/198R9ZWzp_CsSqn2PwUVqtTMDd9DeHXlj/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
            <div class="note-item">
                <div class="note-title">C Handwritten Notes</div>
                <a href="https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/view?usp=drivesdk" target="_blank" class="note-link">View Notes</a>
            </div>
        </div>
    </section>

    <footer class="footer">
        Written by Krishnateja.P - Intermediate passed out but still no college
    </footer>
</div>

<!-- SECRET / APPROVAL CODE MODAL -->
<div class="modal" id="codeModal">
    <div class="modal-content">
        <h3>Enter access code</h3>
        <p style="font-size:0.9rem; color:#555;">Use the code sent by the owner after approval.</p>
        <input type="text" id="secretCodeInput" placeholder="Access code" />
        <div class="modal-buttons">
            <button class="btn" onclick="checkAccessCode()">Unlock</button>
            <button class="btn btn-secondary" onclick="closeCodeModal()">Cancel</button>
        </div>
    </div>
</div>

<script>
    // Initialize EmailJS with your public key
    emailjs.init("YOUR_PUBLIC_KEY");

    async function sendAccessRequest() {
        const name  = document.getElementById('userName').value.trim();
        const email = document.getElementById('userEmail').value.trim();
        const phone = document.getElementById('userPhone').value.trim();
        const txnId = document.getElementById('txnId').value.trim();
        const btn   = document.getElementById('paidBtn');
        const box   = document.getElementById('successBox');

        if (!name || !email || !txnId) {
            alert("Please fill your name, email and transaction ID.");
            return;
        }

        btn.disabled = true;
        btn.textContent = "Sending...";

        const params = {
            to_email: "krishnateiap76@gmail.com",
            user_name: name,
            user_email: email,
            user_phone: phone,
            transaction_id: txnId,
            amount: "₹29",
            message: "This person wants to access your PDFs webpage."
        };

        try {
            await emailjs.send("YOUR_SERVICE_ID", "YOUR_TEMPLATE_ID", params);
            box.style.display = "block";
        } catch (err) {
            alert("Could not send request. Please try again later.");
            console.error(err);
        }

        btn.disabled = false;
        btn.textContent = "I've paid";
    }

    function openCodeModal() {
        document.getElementById('codeModal').style.display = "flex";
        document.getElementById('secretCodeInput').focus();
    }

    function closeCodeModal() {
        document.getElementById('codeModal').style.display = "none";
        document.getElementById('secretCodeInput').value = "";
    }

    window.onclick = function(e) {
        const modal = document.getElementById('codeModal');
        if (e.target === modal) closeCodeModal();
    };

    function checkAccessCode() {
        const input = document.getElementById('secretCodeInput').value.trim();
        const masterCode = "vamsi jacks SVT";
        const isApprovedCode = input.toLowerCase().endsWith("-approved");

        if (input === masterCode || isApprovedCode) {
            document.getElementById('paymentSection').style.display = "none";
            document.getElementById('notesWrapper').style.display   = "block";
            closeCodeModal();
        } else {
            alert("Invalid access code. Please check again.");
        }
    }
</script>
</body>
</html>