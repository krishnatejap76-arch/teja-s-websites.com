<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ultimate Notes for Programmers</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; padding: 20px; color: #333; }
        .container { max-width: 1000px; margin: 0 auto; background: rgba(255, 255, 255, 0.95); border-radius: 20px; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2); overflow: hidden; }
        
        .header { background: linear-gradient(135deg, #ff6b6b, #feca57); padding: 40px; text-align: center; color: white; }
        .header h1 { font-size: 2.2rem; margin-bottom: 10px; }

        .payment-section { padding: 40px; display: flex; flex-wrap: wrap; gap: 20px; justify-content: center; }
        .card { background: white; border-radius: 15px; padding: 25px; box-shadow: 0 5px 15px rgba(0,0,0,0.05); flex: 1 1 350px; border: 1px solid #eee; }
        .amount { font-size: 2.8rem; color: #28a745; font-weight: bold; text-align: center; margin: 10px 0; }
        .upi-box { background: #f0f4ff; border: 2px dashed #667eea; padding: 12px; border-radius: 8px; text-align: center; font-weight: bold; margin-bottom: 20px; color: #2c5aa0; }
        
        input { width: 100%; padding: 12px; margin: 8px 0; border: 2px solid #ddd; border-radius: 8px; font-size: 1rem; outline: none; }
        input:focus { border-color: #667eea; }
        .btn-wa { background: linear-gradient(135deg, #25D366, #128C7E); color: white; border: none; padding: 15px; width: 100%; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 1.1rem; transition: 0.3s; }
        .btn-wa:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(37,211,102,0.4); }

        /* Notes Grid */
        .notes-wrapper { display: none; padding: 40px; background: #fff; animation: fadeIn 0.5s ease-in; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .notes-header { text-align: center; margin-bottom: 30px; padding-bottom: 20px; border-bottom: 2px solid #f0f0f0; }
        .grid-container { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
        .note-card { background: #f9f9f9; border: 1px solid #eee; border-radius: 15px; padding: 20px; text-align: center; transition: 0.3s; }
        .note-card:hover { transform: translateY(-5px); background: #fff; box-shadow: 0 10px 20px rgba(0,0,0,0.1); border-color: #667eea; }
        .pdf-icon { font-size: 45px; margin-bottom: 10px; display: block; }
        .view-btn { display: inline-block; margin-top: 15px; padding: 10px 20px; background: #667eea; color: white; text-decoration: none; border-radius: 8px; font-weight: 600; font-size: 0.9rem; }

        /* Modal */
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.8); z-index: 1000; justify-content: center; align-items: center; }
        .modal-content { background: white; padding: 35px; border-radius: 20px; width: 90%; max-width: 400px; text-align: center; }
    </style>
</head>
<body>

<div class="container">
    <div style="text-align: right; padding: 15px;">
        <button onclick="openModal()" style="cursor:pointer; padding: 10px 20px; border-radius: 50px; border: none; background: #333; color: #fff; font-weight: bold;">Unlock with Code 🔑</button>
    </div>

    <header class="header">
        <h1>Premium Programmer Notes</h1>
        <p>12 Premium Handwritten PDF Resources</p>
    </header>

    <section class="payment-section" id="paymentView">
        <div class="card">
            <h3 style="text-align: center; color: #555;">Scan to Pay ₹29</h3>
            <div style="text-align: center; margin: 20px 0;">
                <img src="https://api.qrserver.com/v1/create-qr-code/?size=180x180&data=upi://pay?pa=9959172924@fam&pn=Krishnateja&am=29" alt="UPI QR">
            </div>
            <div class="upi-box">9959172924@fam</div>
            
            <input type="text" id="uName" placeholder="Your Full Name">
            <input type="text" id="uTxn" placeholder="Transaction ID (Last 5 digits)">
            <button class="btn-wa" onclick="requestAccess()">I Have Paid - Open WhatsApp</button>
        </div>
    </section>

    <section class="notes-wrapper" id="unlockedView">
        <div class="notes-header">
            <h2 style="color: #667eea;">📚 Your Unlocked Library</h2>
            <p>Access your 12 Premium Handwritten Notes</p>
        </div>
        
        <div class="grid-container" id="notesGrid">
            </div>
    </section>
</div>

<div class="modal" id="unlockModal">
    <div class="modal-content">
        <h3 style="margin-bottom: 10px;">Enter Access Code</h3>
        <p style="font-size: 0.85rem; color: #666; margin-bottom: 20px;">Paste the secret code you received from Krishnateja.</p>
        <input type="text" id="txnRef" placeholder="Confirm Txn ID (Last 5 digits)">
        <input type="text" id="otpInput" placeholder="Enter Secret Code (e.g. 54321vamsi jacks)">
        <button class="btn-wa" style="background: #667eea; margin-top: 15px;" onclick="verifyCode()">Verify & Access</button>
        <button onclick="closeModal()" style="margin-top: 15px; border:none; background:none; color:gray; cursor:pointer;">Close</button>
    </div>
</div>

<script>
    // 12 NOTES DATA WITH YOUR LINKS
    const notesData = [
        { title: "Node.js Notes", link: "https://drive.google.com/file/d/1EYPvPowbmdGhMY7j5FU_KfIkpq6-Le0D/view?usp=drivesdk" },
        { title: "SQL Notes", link: "https://drive.google.com/file/d/1HSyoM1FdThM6bEr2nlFM8UrnKfo2pvWN/view?usp=drivesdk" },
        { title: "MongoDB Notes", link: "https://drive.google.com/file/d/1Mn5PaY9J6QzhyIgR9yXFMBxUtmfGuJ5e/view?usp=drivesdk" },
        { title: "OOPS Notes", link: "https://drive.google.com/file/d/1zbAwVtqRjnw-PKa7SwOkDC4icW7Wj8EJ/view?usp=drivesdk" },
        { title: "React JS Notes", link: "https://drive.google.com/file/d/1zbAwVtqRjnw-PKa7SwOkDC4icW7Wj8EJ/view?usp=drivesdk" },
        { title: "Python Notes", link: "https://drive.google.com/file/d/1491Xtw59gCOVzLL_b8nXB-D1m9UZNiTN/view?usp=drivesdk" },
        { title: "Java Notes", link: "https://drive.google.com/file/d/1yZ76wNM5_bIEM2_lvt_BUKfI3HhX84TF/view?usp=drivesdk" },
        { title: "CSS Notes", link: "https://drive.google.com/file/d/1f3TyjLwFca5OVBgOnHsNW64pN4yo6QE2/view?usp=drivesdk" },
        { title: "HTML Notes", link: "https://drive.google.com/file/d/1J7sMPMxbqkrqJ8eJ_rO0BIcwrgGNU4as/view?usp=drivesdk" },
        { title: "JS Notes", link: "https://drive.google.com/file/d/1xRDptNkN_9UgJyp3yA58cBR8TkmJjc9-/view?usp=drivesdk" },
        { title: "DSA Notes", link: "https://drive.google.com/file/d/198R9ZWzp_CsSqn2PwUVqtTMDd9DeHXlj/view?usp=drivesdk" },
        { title: "C Language Notes", link: "https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/view?usp=drivesdk" }
    ];

    // Load Grid Items
    const grid = document.getElementById('notesGrid');
    notesData.forEach(note => {
        grid.innerHTML += `
            <div class="note-card">
                <span class="pdf-icon">📒</span>
                <h4 style="font-size: 0.95rem;">${note.title}</h4>
                <a href="${note.link}" target="_blank" class="view-btn">View PDF</a>
            </div>
        `;
    });

    // BUSINESS LOGIC
    const SECRET_TEXT = "vamsi jacks"; // Your custom string

    function requestAccess() {
        const name = document.getElementById('uName').value.trim();
        const txn = document.getElementById('uTxn').value.trim();
        if(!name || txn.length < 5) { alert("Please enter Name and last 5 digits of Txn ID"); return; }

        const msg = `*PAYMENT VERIFICATION*%0AName: ${name}%0ATxn ID: ${txn}%0A_I have paid ₹29. Please verify and send the unlock code._`;
        window.open(`https://wa.me/919959172924?text=${msg}`, '_blank');
    }

    function openModal() { document.getElementById('unlockModal').style.display = 'flex'; }
    function closeModal() { document.getElementById('unlockModal').style.display = 'none'; }

    function verifyCode() {
        const userTxnInput = document.getElementById('txnRef').value.trim();
        const userSecretInput = document.getElementById('otpInput').value.trim();

        // LOGIC: Reverse the Txn ID + add "vamsi jacks"
        // Example: "98668" becomes "86689" + "vamsi jacks"
        const reversedTxn = userTxnInput.split('').reverse().join('');
        const expectedCode = reversedTxn + SECRET_TEXT;

        if(userSecretInput === expectedCode && userTxnInput !== "") {
            document.getElementById('paymentView').style.display = 'none';
            document.getElementById('unlockedView').style.display = 'block';
            closeModal();
            alert("Verification Successful! Enjoy your notes.");
        } else {
            alert("Invalid Code! Make sure you entered the ID and the Secret Code exactly as instructed.");
        }
    }
</script>
</body>
</html>
