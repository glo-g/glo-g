

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
