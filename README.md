 
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Birthday Wish</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #ffe6f2;
    padding: 50px;
  }
  h1 {
    color: #ff3399;
  }
  p {
    color: #555;
    font-size: 1.2em;
  }
  button {
    background-color: #ff66b2;
    color: white;
    border: none;
    padding: 15px 30px;
    font-size: 1.2em;
    border-radius: 8px;
    cursor: pointer;
    margin-top: 20px;
  }
  button:hover {
    background-color: #ff3385;
  }
</style>
</head>
<body>
  <h1>🥳Happy Birthday Momos api🦉</h1>
  <p>May Allah live you long and give success or many many chocolate</p>
  <button onclick="launchConfetti()">Touch Me🥳</button>

  <canvas id="confettiCanvas" style="position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;"></canvas>

  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
  <script>
    function launchConfetti() {
      const duration = 2 * 1000;
      const end = Date.now() + duration;

      (function frame() {
        confetti({
          particleCount: 5,
          angle: 60,
          spread: 55,
          origin: { x: 0 }
        });
        confetti({
          particleCount: 5,
          angle: 120,
          spread: 55,
          origin: { x: 1 }
        });
        if (Date.now() < end) {
          requestAnimationFrame(frame);
        }
      }());
    }
  </script>
</body>
</html>
 
 
