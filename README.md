<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Handwritten Notes Access</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
            background: radial-gradient(circle at top, #fefefe 0%, #e9f0ff 40%, #d8e2ff 100%);
            min-height: 100vh;
            color: #333;
        }
        .main-container {
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        .header {
            position: fixed;
            top: 18px;
            right: 18px;
            z-index: 1000;
        }
        .key-icon {
            width: 46px;
            height: 46px;
            background: rgba(255,255,255,0.9);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 22px;
            box-shadow: 0 8px 24px rgba(0,0,0,0.18);
            transition: transform 0.25s ease, box-shadow 0.25s ease, background 0.25s ease;
        }
        .key-icon:hover {
            transform: rotate(90deg) scale(1.05);
            background: #ffffff;
            box-shadow: 0 10px 30px rgba(0,0,0,0.25);
        }

        .key-label {
            position: fixed;
            top: 22px;
            right: 70px;
            font-size: 12px;
            color: #555;
            background: rgba(255,255,255,0.9);
            padding: 4px 10px;
            border-radius: 999px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
        }

        .key-modal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.55);
            z-index: 2000;
            backdrop-filter: blur(4px);
            align-items: center;
            justify-content: center;
        }
        .key-modal.active { display: flex; }
        .key-container {
            background: #fdfdfd;
            padding: 32px 26px;
            border-radius: 22px;
            max-width: 360px;
            width: 90%;
            box-shadow: 0 20px 45px rgba(0,0,0,0.35);
            text-align: center;
        }
        .key-title {
            font-size: 20px;
            margin-bottom: 6px;
        }
        .key-sub {
            font-size: 14px;
            color: #666;
            margin-bottom: 18px;
        }

        .payment-section {
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 80px 16px 24px;
            text-align: center;
        }
        .payment-card {
            background: rgba(255,255,255,0.96);
            padding: 42px 32px;
            border-radius: 26px;
            max-width: 460px;
            width: 100%;
            box-shadow: 0 24px 55px rgba(0,0,0,0.22);
            border: 1px solid rgba(0,0,0,0.05);
        }
        .payment-title {
            font-size: 22px;
            letter-spacing: 0.02em;
        }
        .price-pill {
            display: inline-block;
            margin: 18px 0 14px;
            padding: 10px 26px;
            border-radius: 999px;
            background: linear-gradient(120deg, #f5d0a9, #f9cdd2);
            color: #3c3c3c;
            font-size: 18px;
        }
        .payment-note {
            font-size: 14px;
            color: #666;
            margin-bottom: 20px;
        }
        .upi-block {
            margin: 18px 0;
            padding: 16px 18px;
            border-radius: 16px;
            background: #f5f6ff;
            border: 1px dashed #b1b6ff;
            font-size: 16px;
            letter-spacing: 0.04em;
        }
        .qr-box {
            width: 190px;
            height: 190px;
            margin: 20px auto 10px;
            border-radius: 18px;
            background: linear-gradient(135deg, #ced4ff, #ffd6c4);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #323232;
            font-size: 14px;
            border: 3px dashed rgba(255,255,255,0.7);
        }
        .field {
            width: 100%;
            margin: 20px 0 12px;
        }
        .input {
            width: 100%;
            padding: 12px 16px;
            border-radius: 999px;
            border: 1px solid #d3d7e8;
            font-size: 15px;
            text-align: center;
            outline: none;
            background: #f7f8ff;
        }
        .input:focus {
            border-color: #9ea7ff;
            background: #ffffff;
        }
        .btn {
            display: inline-block;
            padding: 11px 30px;
            border-radius: 999px;
            border: none;
            outline: none;
            background: linear-gradient(120deg, #9ad4b5, #7bc6ff);
            color: #243343;
            font-size: 15px;
            cursor: pointer;
            transition: transform 0.18s ease, box-shadow 0.18s ease, filter 0.18s ease;
            box-shadow: 0 8px 24px rgba(0,0,0,0.16);
        }
        .btn:hover {
            transform: translateY(-1px);
            filter: brightness(1.03);
            box-shadow: 0 10px 28px rgba(0,0,0,0.2);
        }
        .btn-secondary {
            background: #e5e7f5;
            box-shadow: none;
            margin-left: 6px;
        }
        .btn-secondary:hover {
            box-shadow: 0 5px 16px rgba(0,0,0,0.12);
        }

        .content-page {
            display: none;
            padding: 82px 14px 18px;
        }
        .content-inner {
            max-width: 1100px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: minmax(0, 3fr) minmax(0, 5fr);
            gap: 18px;
        }

        .list-panel {
            background: rgba(255,255,255,0.96);
            border-radius: 24px;
            padding: 18px 16px 16px;
            box-shadow: 0 18px 40px rgba(0,0,0,0.15);
        }
        .list-title {
            font-size: 18px;
            margin-bottom: 10px;
            color: #444;
        }
        .list-sub {
            font-size: 13px;
            color: #777;
            margin-bottom: 12px;
        }
        .notes-list {
            list-style: none;
            margin-top: 6px;
        }
        .note-item {
            margin: 4px 0;
        }
        .note-button {
            width: 100%;
            border: none;
            outline: none;
            text-align: left;
            padding: 10px 12px;
            border-radius: 14px;
            background: #f4f5ff;
            color: #333;
            font-size: 14px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: background 0.18s ease, transform 0.12s ease, box-shadow 0.18s ease;
        }
        .note-button span {
            font-size: 13px;
            color: #888;
        }
        .note-button:hover {
            background: #e6e8ff;
            transform: translateY(-1px);
            box-shadow: 0 6px 18px rgba(0,0,0,0.12);
        }
        .note-button.active {
            background: #dde3ff;
            box-shadow: inset 0 0 0 1px rgba(122,137,255,0.55);
        }

        .viewer-panel {
            background: rgba(255,255,255,0.98);
            border-radius: 24px;
            padding: 18px 16px 16px;
            box-shadow: 0 18px 40px rgba(0,0,0,0.17);
            display: flex;
            flex-direction: column;
            min-height: 420px;
        }
        .viewer-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            gap: 8px;
        }
        .viewer-title {
            font-size: 16px;
            color: #444;
        }
        .viewer-controls {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }
        .small-btn {
            border-radius: 999px;
            border: none;
            padding: 6px 12px;
            font-size: 12px;
            background: #edf0ff;
            color: #3a3a3a;
            cursor: pointer;
            transition: background 0.15s ease;
        }
        .small-btn:hover {
            background: #dde2ff;
        }
        .pdf-frame {
            width: 100%;
            height: 70vh;
            border: none;
            border-radius: 16px;
            margin-top: 8px;
            background: #f4f5fb;
        }

        @media (max-width: 880px) {
            .content-inner {
                grid-template-columns: minmax(0, 1fr);
            }
            .pdf-frame {
                height: 60vh;
            }
            .key-label {
                display: none;
            }
        }
    </style>
</head>
<body>
<div class="main-container">

    <div class="key-label">
        tap ⚙ for key access
    </div>
    <div class="header">
        <div class="key-icon" onclick="toggleKeyModal()" title="Key access">
            ⚙️
        </div>
    </div>

    <div id="keyModal" class="key-modal">
        <div class="key-container">
            <div class="key-title">Secret access</div>
            <div class="key-sub">Enter the key to open all handwritten notes.</div>
            <input type="password" id="keyInput" class="input" placeholder="Enter key code" maxlength="20">
            <div style="margin-top: 12px;">
                <button class="btn" onclick="checkKey()">Open notes</button>
                <button class="btn btn-secondary" onclick="toggleKeyModal()">Close</button>
            </div>
        </div>
    </div>

    <div id="paymentSection" class="payment-section">
        <div class="payment-card">
            <div class="payment-title">Handwritten notes folder</div>
            <div class="price-pill">Access for ₹49</div>
            <div class="payment-note">
                Pay once to view and download all handwritten notes.
                Or use the secret key from the settings icon in the top-right corner.
            </div>
            <div class="upi-block">
                UPI ID: 9959172924@fam
            </div>
            <div class="qr-box">
                Scan and pay ₹49
                with any UPI app
            </div>
            <div class="payment-note">
                After payment, paste your UPI transaction or reference ID below.
            </div>
            <div class="field">
                <input type="text" id="transactionId" class="input"
                       placeholder="Transaction / UPI reference ID">
            </div>
            <div style="margin-top: 6px;">
                <button class="btn" onclick="verifyPayment()">Verify and open folder</button>
            </div>
            <div class="payment-note" style="margin-top: 10px; font-size: 12px;">
                Works with PhonePe, Google Pay, Paytm, BHIM and other UPI apps.
            </div>
        </div>
    </div>

    <div id="contentPage" class="content-page">
        <div class="content-inner">

            <div class="list-panel">
                <div class="list-title">Handwritten notes</div>
                <div class="list-sub">Choose a note from the list to open it in the viewer.</div>
                <ul class="notes-list">
                    <li class="note-item"><button class="note-button" onclick="loadNote(0)"><span>Node JS handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(1)"><span>SQL handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(2)"><span>MongoDB handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(3)"><span>Oops handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(4)"><span>React JS handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(5)"><span>Python handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(6)"><span>Java handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(7)"><span>CSS handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(8)"><span>HTML handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(9)"><span>JS handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(10)"><span>DSA handwritten notes</span><span>PDF</span></button></li>
                    <li class="note-item"><button class="note-button" onclick="loadNote(11)"><span>C handwritten notes</span><span>PDF</span></button></li>
                </ul>
            </div>

            <div class="viewer-panel">
                <div class="viewer-header">
                    <div class="viewer-title" id="viewerTitle">No note selected</div>
                    <div class="viewer-controls">
                        <button class="small-btn" onclick="openInNewTab()">Open in new tab</button>
                        <button class="small-btn" onclick="printCurrent()">Print</button>
                        <button class="small-btn" onclick="toggleFullscreen()">Fullscreen</button>
                    </div>
                </div>
                <iframe id="pdfViewer" class="pdf-frame"></iframe>
            </div>
        </div>
    </div>

</div>

<script>
    const correctKey = "vamsi jacks";

    const notes = [
        { name: "Node JS handwritten notes",  share: "https://drive.google.com/file/d/1EYPvPowbmdGhMY7j5FU_KfIkpq6-Le0D/view?usp=drivesdk" },
        { name: "SQL handwritten notes",      share: "https://drive.google.com/file/d/1HSyoM1FdThM6bEr2nlFM8UrnKfo2pvWN/view?usp=drivesdk" },
        { name: "MongoDB handwritten notes",  share: "https://drive.google.com/file/d/1Mn5PaY9J6QzhyIgR9yXFMBxUtmfGuJ5e/view?usp=drivesdk" },
        { name: "Oops handwritten notes",     share: "https://drive.google.com/file/d/1zbAwVtqRjnw-PKa7SwOkDC4icW7Wj8EJ/view?usp=drivesdk" },
        { name: "React JS handwritten notes", share: "https://drive.google.com/file/d/1491Xtw59gCOVzLL_b8nXB-D1m9UZNiTN/view?usp=drivesdk" },
        { name: "Python handwritten notes",   share: "https://drive.google.com/file/d/1491Xtw59gCOVzLL_b8nXB-D1m9UZNiTN/view?usp=drivesdk" },
        { name: "Java handwritten notes",     share: "https://drive.google.com/file/d/1yZ76wNM5_bIEM2_lvt_BUKfI3HhX84TF/view?usp=drivesdk" },
        { name: "CSS handwritten notes",      share: "https://drive.google.com/file/d/1f3TyjLwFca5OVBgOnHsNW64pN4yo6QE2/view?usp=drivesdk" },
        { name: "HTML handwritten notes",     share: "https://drive.google.com/file/d/1J7sMPMxbqkrqJ8eJ_rO0BIcwrgGNU4as/view?usp=drivesdk" },
        { name: "JS handwritten notes",       share: "https://drive.google.com/file/d/1xRDptNkN_9UgJyp3yA58cBR8TkmJjc9-/view?usp=drivesdk" },
        { name: "DSA handwritten notes",      share: "https://drive.google.com/file/d/198R9ZWzp_CsSqn2PwUVqtTMDd9DeHXlj/view?usp=drivesdk" },
        { name: "C handwritten notes",        share: "https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/view?usp=drivesdk" }
    ];

    let currentIndex = null;

    function shareToPreview(url) {
        const match = url.match(/(https://drive.google.com/file/d/[^/]+)/view/i);
        if (match) {
            return match[1] + "/preview";  // Google Drive preview format for iframe[web:9][web:2]
        }
        return url;
    }

    function toggleKeyModal() {
        const modal = document.getElementById("keyModal");
        modal.classList.toggle("active");
        if (modal.classList.contains("active")) {
            setTimeout(() => {
                document.getElementById("keyInput").focus();
            }, 120);
        }
    }

    function checkKey() {
        const value = document.getElementById("keyInput").value.trim();
        if (value === correctKey) {
            openContent();
            toggleKeyModal();
        } else {
            alert("Key is not correct. Try again.");
            document.getElementById("keyInput").value = "";
        }
    }

    function verifyPayment() {
        const tx = document.getElementById("transactionId").value.trim();
        if (tx.length < 5) {
            alert("Please enter a valid transaction or reference ID.");
            return;
        }
        const ok = confirm("Confirm that ₹49 has been received for transaction:
" + tx);
        if (ok) {
            openContent();
        }
    }

    function openContent() {
        document.getElementById("paymentSection").style.display = "none";
        document.getElementById("contentPage").style.display = "block";
        loadNote(0);
    }

    function loadNote(index) {
        currentIndex = index;
        const note = notes[index];
        const iframe = document.getElementById("pdfViewer");
        iframe.src = shareToPreview(note.share);
        document.getElementById("viewerTitle").textContent = note.name;

        const buttons = document.querySelectorAll(".note-button");
        buttons.forEach((btn, i) => {
            if (i === index) btn.classList.add("active");
            else btn.classList.remove("active");
        });
    }

    function openInNewTab() {
        if (currentIndex === null) return;
        const link = notes[currentIndex].share.replace("view?usp=drivesdk", "view");
        window.open(link, "_blank");
    }

    function printCurrent() {
        if (currentIndex === null) return;
        const link = shareToPreview(notes[currentIndex].share);
        window.open(link, "_blank");
    }

    function toggleFullscreen() {
        const viewer = document.getElementById("pdfViewer");
        if (viewer.requestFullscreen) viewer.requestFullscreen();
        else if (viewer.webkitRequestFullscreen) viewer.webkitRequestFullscreen();
        else if (viewer.msRequestFullscreen) viewer.msRequestFullscreen();
    }

    document.getElementById("keyInput").addEventListener("keypress", (e) => {
        if (e.key === "Enter") checkKey();
    });
    document.getElementById("transactionId").addEventListener("keypress", (e) => {
        if (e.key === "Enter") verifyPayment();
    });

    window.onload = function () {
        document.getElementById("transactionId").focus();
    };
</script>
</body>
</html>