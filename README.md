<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Access Programming Notes</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #ffffff;
      color: #333333;
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
    .btn {
      padding: 10px 20px;
      border-radius: 4px;
      border: none;
      cursor: pointer;
      background-color: #e0e0ff;
      color: #333333;
      font-size: 0.95rem;
    }
    .btn:hover {
      background-color: #d0d0f0;
    }
    .secret-area {
      margin-top: 30px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }
    .secret-input {
      padding: 8px 10px;
      border-radius: 4px;
      border: 1px solid #cccccc;
      width: 220px;
    }
    .icon-button {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 8px 12px;
      border-radius: 4px;
      border: 1px solid #cccccc;
      background-color: #f5f5f5;
      color: #444444;
      cursor: pointer;
      font-size: 0.9rem;
    }
    .icon-button span.icon {
      font-size: 1.1rem;
    }
    .small-note {
      margin-top: 8px;
      font-size: 0.8rem;
      color: #888888;
    }
  </style>
</head>
<body>
  <div class="center-box">
    <h1>Programming Notes Access</h1>
    <p>Pay 49 rupees or use the secret code to access the notes.</p>

    <div class="upi-box">
      <p>Send 49 rupees to this UPI ID:</p>
      <div class="upi-id">9959172924@fam</div>
      <div class="amount">Amount: ₹49</div>
      <!-- NOTE: This button does NOT verify real payment; it is just a manual step -->
      <button class="btn" onclick="goToNotes()">I have paid, continue</button>
      <p class="small-note">After payment, click the button to get access.</p>
    </div>

    <div class="secret-area">
      <button class="icon-button" onclick="toggleSecretInput()">
        <span class="icon">⚙️</span>
        <span>Secret Code</span>
      </button>
      <input
        id="secretInput"
        class="secret-input"
        type="password"
        placeholder="Enter secret code"
        style="display:none;"
      />
      <button
        id="secretSubmit"
        class="btn"
        style="display:none;"
        onclick="checkSecretCode()"
      >
        Unlock with code
      </button>
      <p class="small-note">Only people with the secret code can use this option.</p>
    </div>
  </div>

  <script>
    const SECRET_CODE = "vamsi jacks SVT";

    function goToNotes() {
      // No real payment verification. Just redirect.
      window.location.href = "notes.html";
    }

    function toggleSecretInput() {
      const input = document.getElementById("secretInput");
      const btn = document.getElementById("secretSubmit");
      const isHidden = input.style.display === "none";
      input.style.display = isHidden ? "block" : "none";
      btn.style.display = isHidden ? "inline-block" : "none";
    }

    function checkSecretCode() {
      const value = document.getElementById("secretInput").value;
      if (value === SECRET_CODE) {
        window.location.href = "notes.html";
      } else {
        alert("Wrong secret code.");
      }
    }
  </script>
</body>
</html>