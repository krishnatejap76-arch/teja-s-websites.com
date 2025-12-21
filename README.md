<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Programming Notes Access</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #ffffff;
      color: #333333;
    }

    .top-right-secret {
      position: fixed;
      top: 10px;
      right: 10px;
      display: flex;
      align-items: center;
      gap: 6px;
      z-index: 100;
    }

    .secret-btn {
      padding: 6px 10px;
      border-radius: 4px;
      border: 1px solid #cccccc;
      background-color: #f5f5f5;
      color: #444444;
      cursor: pointer;
      font-size: 0.85rem;
    }

    .secret-input {
      padding: 6px 8px;
      border-radius: 4px;
      border: 1px solid #cccccc;
      font-size: 0.85rem;
      display: none;
    }

    .secret-submit {
      padding: 6px 10px;
      border-radius: 4px;
      border: 1px solid #cccccc;
      background-color: #e0e0ff;
      color: #333333;
      cursor: pointer;
      font-size: 0.85rem;
      display: none;
    }

    .center-box {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 20px;
    }

    h1 {
      font-weight: normal;
      color: #555555;
      margin-bottom: 10px;
    }

    p {
      color: #666666;
    }

    .upi-box {
      border: 1px solid #dddddd;
      border-radius: 8px;
      padding: 20px 30px;
      margin-top: 20px;
      background-color: #f8f8f8;
    }

    .upi-id {
      font-size: 1.1rem;
      color: #444444;
      margin: 10px 0;
    }

    .amount {
      margin: 5px 0 15px;
      color: #777777;
    }

    .btn-pay {
      padding: 10px 20px;
      border-radius: 4px;
      border: none;
      cursor: pointer;
      background-color: #e0e0ff;
      color: #333333;
      font-size: 0.95rem;
    }

    .btn-pay:hover {
      background-color: #d0d0f0;
    }

    .small-note {
      margin-top: 8px;
      font-size: 0.8rem;
      color: #888888;
    }
  </style>
</head>
<body>
  <!-- Secret code in top-right corner -->
  <div class="top-right-secret">
    <button class="secret-btn" onclick="toggleSecretInput()">
      ⚙️ Secret Code
    </button>
    <input
      id="secretInput"
      class="secret-input"
      type="password"
      placeholder="Enter code"
    />
    <button
      id="secretSubmit"
      class="secret-submit"
      onclick="checkSecretCode()"
    >
      Unlock
    </button>
  </div>

  <!-- Center payment section -->
  <div class="center-box">
    <h1>Programming Notes Access</h1>
    <p>Pay 49 rupees to get access to the notes.</p>

    <div class="upi-box">
      <p>Send 49 rupees to this UPI ID:</p>
      <div class="upi-id">9959172924@fam</div>
      <div class="amount">Amount: ₹49</div>

      <!-- This just redirects; it does NOT check real payment -->
      <button class="btn-pay" onclick="goToNotes()">
        I have paid, continue
      </button>

      <p class="small-note">
        After completing the payment, click the button to access the notes page.
      </p>
    </div>
  </div>

  <script>
    const SECRET_CODE = "vamsi jacks SVT";

    function goToNotes() {
      // Redirect to the notes page (second page)
      window.location.href = "notes.html";
    }

    function toggleSecretInput() {
      const input = document.getElementById("secretInput");
      const submit = document.getElementById("secretSubmit");

      if (input.style.display === "none" || input.style.display === "") {
        input.style.display = "inline-block";
        submit.style.display = "inline-block";
      } else {
        input.style.display = "none";
        submit.style.display = "none";
      }
    }

    function checkSecretCode() {
      const inputVal = document.getElementById("secretInput").value;
      if (inputVal === SECRET_CODE) {
        window.location.href = "notes.html";
      } else {
        alert("Wrong secret code.");
      }
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Programming Notes List</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #ffffff;
      color: #333333;
      display: flex;
      height: 100vh;
    }

    .left-panel {
      width: 30%;
      border-right: 1px solid #dddddd;
      padding: 15px;
      box-sizing: border-box;
      background-color: #f8f8f8;
      overflow-y: auto;
    }

    .right-panel {
      flex: 1;
      padding: 10px;
      box-sizing: border-box;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    h2 {
      font-weight: normal;
      color: #555555;
      margin-top: 0;
    }

    .note-item {
      padding: 10px;
      margin-bottom: 8px;
      border-radius: 4px;
      border: 1px solid #cccccc;
      background-color: #ffffff;
      cursor: pointer;
      font-size: 0.95rem;
      color: #444444;
    }

    .note-item:hover {
      background-color: #eaeaea;
    }

    .toolbar {
      display: flex;
      gap: 10px;
      align-items: center;
    }

    .toolbar button {
      padding: 6px 10px;
      border-radius: 4px;
      border: 1px solid #cccccc;
      background-color: #f3f3f3;
      cursor: pointer;
      font-size: 0.85rem;
      color: #444444;
    }

    .toolbar button:hover {
      background-color: #e0e0e0;
    }

    .viewer-container {
      flex: 1;
      border: 1px solid #cccccc;
      border-radius: 4px;
      overflow: hidden;
    }

    iframe {
      width: 100%;
      height: 100%;
      border: none;
      background-color: #ffffff;
    }

    .placeholder-text {
      padding: 15px;
      color: #777777;
      font-size: 0.9rem;
    }
  </style>
</head>
<body>
  <div class="left-panel">
    <h2>Handwritten Notes</h2>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1EYPvPowbmdGhMY7j5FU_KfIkpq6-Le0D/preview')">
      Node JS handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1HSyoM1FdThM6bEr2nlFM8UrnKfo2pvWN/preview')">
      SQL handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1Mn5PaY9J6QzhyIgR9yXFMBxUtmfGuJ5e/preview')">
      MongoDB handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1zbAwVtqRjnw-PKa7SwOkDC4icW7Wj8EJ/preview')">
      React JS handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1491Xtw59gCOVzLL_b8nXB-D1m9UZNiTN/preview')">
      Python handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1yZ76wNM5_bIEM2_lvt_BUKfI3HhX84TF/preview')">
      Java handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1f3TyjLwFca5OVBgOnHsNW64pN4yo6QE2/preview')">
      CSS handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1J7sMPMxbqkrqJ8eJ_rO0BIcwrgGNU4as/preview')">
      HTML handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1xRDptNkN_9UgJyp3yA58cBR8TkmJjc9-/preview')">
      JS handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/198R9ZWzp_CsSqn2PwUVqtTMDd9DeHXlj/preview')">
      DSA handwritten notes
    </div>

    <div class="note-item" onclick="openPdf('https://drive.google.com/file/d/1LdV4hQF9rmKq3eC8uM-tLfwxO3Rx3k4t/preview')">
      C handwritten notes
    </div>
  </div>

  <div class="right-panel">
    <div class="toolbar">
      <button onclick="savePdf()">Save PDF</button>
      <button onclick="fullScreenPdf()">Full Screen</button>
      <button onclick="printPdf()">Print</button>
    </div>

    <div class="viewer-container">
      <iframe id="pdfFrame" src=""></iframe>
      <div id="placeholder" class="placeholder-text">
        Select any note on the left to open the PDF. Use the buttons above to save, print, or view full screen in a new tab using the browser / Google Drive controls.
      </div>
    </div>
  </div>

  <script>
    let currentPdfUrl = "";

    function openPdf(url) {
      currentPdfUrl = url;
      const frame = document.getElementById("pdfFrame");
      const placeholder = document.getElementById("placeholder");
      frame.src = url;
      placeholder.style.display = "none";
    }

    function savePdf() {
      if (!currentPdfUrl) {
        alert("Please select a PDF first.");
        return;
      }
      const viewUrl = currentPdfUrl.replace("/preview", "/view");
      window.open(viewUrl, "_blank");
    }

    function fullScreenPdf() {
      if (!currentPdfUrl) {
        alert("Please select a PDF first.");
        return;
      }
      window.open(currentPdfUrl, "_blank");
    }

    function printPdf() {
      if (!currentPdfUrl) {
        alert("Please select a PDF first.");
        return;
      }
      const fileUrl = currentPdfUrl.replace("/preview", "/view");
      window.open(fileUrl, "_blank");
    }
  </script>
</body>
</html>