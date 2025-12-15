<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Phone OTP Verification</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; display: flex; align-items: center; justify-content: center; }
        .container { background: white; padding: 2rem; border-radius: 20px; box-shadow: 0 20px 40px rgba(0,0,0,0.1); width: 100%; max-width: 400px; }
        h2 { text-align: center; color: #333; margin-bottom: 1.5rem; }
        .phone-input { width: 100%; padding: 15px; font-size: 18px; border: 2px solid #e1e5e9; border-radius: 12px; margin-bottom: 1rem; text-align: center; }
        .otp-container { display: none; }
        .otp-inputs { display: flex; gap: 10px; justify-content: center; margin-bottom: 1rem; }
        .otp-input { width: 60px; height: 60px; font-size: 24px; text-align: center; border: 2px solid #e1e5e9; border-radius: 12px; font-weight: bold; }
        .otp-input:focus { border-color: #667eea; outline: none; box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1); }
        button { width: 100%; padding: 15px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border: none; border-radius: 12px; font-size: 16px; font-weight: 600; cursor: pointer; transition: transform 0.2s; }
        button:hover { transform: translateY(-2px); }
        button:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }
        .message { text-align: center; margin-top: 1rem; padding: 10px; border-radius: 8px; font-weight: 500; }
        .success { background: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
        .error { background: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }
        .resend { text-align: center; margin-top: 1rem; color: #666; cursor: pointer; text-decoration: underline; }
        .resend:hover { color: #667eea; }
    </style>
</head>
<body>
    <div class="container">
        <h2>🔐 Phone Verification</h2>
        
        <!-- Phone Number Section -->
        <div id="phoneSection">
            <input type="tel" id="phoneInput" class="phone-input" placeholder="Enter phone number (10 digits)" maxlength="10">
            <button onclick="sendOTP()">Send OTP</button>
        </div>

        <!-- OTP Section -->
        <div id="otpSection" class="otp-container">
            <p style="text-align: center; margin-bottom: 1rem; color: #666;">Enter 5-digit OTP sent to your phone</p>
            <div class="otp-inputs">
                <input type="text" class="otp-input" maxlength="1" id="otp1">
                <input type="text" class="otp-input" maxlength="1" id="otp2">
                <input type="text" class="otp-input" maxlength="1" id="otp3">
                <input type="text" class="otp-input" maxlength="1" id="otp4">
                <input type="text" class="otp-input" maxlength="1" id="otp5">
            </div>
            <button id="verifyBtn" onclick="verifyOTP()">Verify OTP</button>
            <div id="resend" class="resend" onclick="resendOTP()">Didn't receive? Resend OTP</div>
        </div>

        <div id="message"></div>
    </div>

    <script>
        let generatedOTP = '';
        let countdown = 0;

        // Auto-focus next OTP input
        document.querySelectorAll('.otp-input').forEach((input, index) => {
            input.addEventListener('input', (e) => {
                if (e.target.value.length === 1) {
                    const nextInput = document.querySelector(`#otp${index + 2}`);
                    if (nextInput) nextInput.focus();
                }
            });
            input.addEventListener('keydown', (e) => {
                if (e.key === 'Backspace' && !e.target.value) {
                    const prevInput = document.querySelector(`#otp${index}`);
                    if (prevInput) prevInput.focus();
                }
            });
        });

        function sendOTP() {
            const phone = document.getElementById('phoneInput').value.trim();
            if (!/^d{10}$/.test(phone)) {
                showMessage('Please enter a valid 10-digit phone number', 'error');
                return;
            }

            // Generate 5-digit OTP (for demo purposes)
            generatedOTP = Math.floor(10000 + Math.random() * 90000).toString();
            console.log('Generated OTP:', generatedOTP); // For demo - check console

            document.getElementById('phoneSection').style.display = 'none';
            document.getElementById('otpSection').style.display = 'block';
            document.getElementById('otp1').focus();

            showMessage('OTP sent successfully! Check console for demo OTP.', 'success');
            startCountdown();
        }

        function verifyOTP() {
            const otpInputs = ['otp1', 'otp2', 'otp3', 'otp4', 'otp5'];
            let enteredOTP = '';
            
            otpInputs.forEach(id => {
                enteredOTP += document.getElementById(id).value;
            });

            if (enteredOTP.length !== 5) {
                showMessage('Please enter complete 5-digit OTP', 'error');
                return;
            }

            if (enteredOTP === generatedOTP) {
                showMessage('✅ Phone number verified successfully!', 'success');
                document.getElementById('verifyBtn').disabled = true;
                document.getElementById('verifyBtn').textContent = 'Verified!';
            } else {
                showMessage('❌ Invalid OTP. Please try again.', 'error');
                clearOTPInputs();
            }
        }

        function resendOTP() {
            clearOTPInputs();
            document.getElementById('otp1').focus();
            generatedOTP = Math.floor(10000 + Math.random() * 90000).toString();
            console.log('New Generated OTP:', generatedOTP);
            showMessage('New OTP sent! Check console.', 'success');
            startCountdown();
        }

        function clearOTPInputs() {
            document.querySelectorAll('.otp-input').forEach(input => {
                input.value = '';
            });
        }

        function showMessage(text, type) {
            const messageDiv = document.getElementById('message');
            messageDiv.textContent = text;
            messageDiv.className = `message ${type}`;
        }

        function startCountdown() {
            countdown = 30;
            const resendBtn = document.getElementById('resend');
            const timer = setInterval(() => {
                countdown--;
                resendBtn.textContent = countdown > 0 ? `Resend OTP (${countdown}s)` : "Didn't receive? Resend OTP";
                resendBtn.style.color = countdown > 0 ? '#999' : '#666';
                resendBtn.style.cursor = countdown > 0 ? 'not-allowed' : 'pointer';
                resendBtn.style.textDecoration = countdown > 0 ? 'none' : 'underline';
                
                if (countdown <= 0) {
                    clearInterval(timer);
                }
            }, 1000);
        }

        // Enter key support
        document.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                const activeEl = document.activeElement;
                if (activeEl.classList.contains('phone-input')) {
                    sendOTP();
                } else if (activeEl.classList.contains('otp-input')) {
                    verifyOTP();
                }
            }
        });
    </script>
</body>
</html>