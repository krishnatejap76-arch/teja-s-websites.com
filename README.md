<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ultimate Notes for Programmers</title>
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
            max-width: 800px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            animation: fadeInUp 1s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
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
            50% { transform: rotate(180deg); }
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            position: relative;
            z-index: 2;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .notes-list {
            padding: 40px 30px;
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
            to {
                transform: translateX(0);
                opacity: 1;
            }
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
            padding: 25px;
            font-size: 1.1rem;
            font-weight: 500;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2rem;
            }
            
            .note-item {
                flex-direction: column;
                text-align: center;
            }
            
            .note-title {
                margin-right: 0;
                margin-bottom: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <h1>Ultimate Notes for Programmers</h1>
        </header>

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

        <footer class="footer">
            Written by Krishnateja.P - Intermediate passed out but still no college
        </footer>
    </div>
</body>
</html>