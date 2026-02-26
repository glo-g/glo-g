<!DOCTYPE html>
<html>
<head>
  <title>Visitor Counter</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #111;
      color: white;
      font-family: Arial, sans-serif;
    }

    .counter-container {
      text-align: center;
    }

    .flip-counter {
      display: flex;
      gap: 8px;
      margin-top: 20px;
    }

    .digit {
      background: black;
      color: #00ffcc;
      font-size: 3rem;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 5px 0 #00aa88;
      min-width: 50px;
      text-align: center;
      transition: transform 0.3s ease;
    }

    .digit.flip {
      transform: rotateX(360deg);
    }
  </style>
</head>
<body>

<div class="counter-container">
  <h2>Visitor Count</h2>
  <div class="flip-counter" id="counter"></div>
</div>

<script>
  const namespace = "glo-g-website";
  const key = "visits";

  fetch(`https://api.countapi.xyz/hit/${namespace}/${key}`)
    .then(res => res.json())
    .then(data => {
      const count = data.value;
      const counterElement = document.getElementById("counter");
      counterElement.innerHTML = "";

      count.toString().split("").forEach((digit) => {
        const digitDiv = document.createElement("div");
        digitDiv.classList.add("digit");
        digitDiv.textContent = digit;
        counterElement.appendChild(digitDiv);

        setTimeout(() => {
          digitDiv.classList.add("flip");
        }, 100);
      });
    })
    .catch(err => {
      console.error("Counter failed:", err);
    });
</script>

</body>
</html>
