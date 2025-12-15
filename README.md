<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My Notes</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
    }
    /* top-left text */
    .inspired {
      position: absolute;
      top: 10px;
      left: 10px;
      font-size: 14px;
      color: #555;
    }
    /* heading + logo row */
    .header-row {
      display: flex;
      align-items: center;
      justify-content: flex-start;
      margin-top: 40px;
      gap: 10px;
    }
    h1 {
      color: green; /* "My Notes" in green */
      margin: 0;
    }
    .cr7-logo {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background-color: black; /* placeholder circle */
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
      font-size: 14px;
    }
    /* bottom blue box */
    .bottom-box {
      margin-top: 200px;
      border: 2px solid #1e40af;
      background-color: #3b82f6;
      color: white;
      padding: 15px 20px;
      width: fit-content;
      border-radius: 8px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="inspired">inspired by me</div>

  <div class="header-row">
    <h1>My Notes</h1>
    <!-- Replace this with an actual CR7 image if you have one -->
    <!-- Example: <img src="cr7-logo.png" alt="CR7 Logo" class="cr7-logo-img"> -->
    <div class="cr7-logo">CR7</div>
  </div>

  <div class="bottom-box">
    C language full notes
  </div>
</body>
</html>