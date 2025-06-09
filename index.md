<!DOCTYPE html>
<html>
<head>
  <title>Coupon Validator</title>
</head>
<body>
  <h2>Restaurant Coupon Checker</h2>
  <form id="couponForm">
    <label for="code">Enter Coupon Code:</label><br><br>
    <input type="text" id="code" name="code" required><br><br>
    <button type="submit">Check Coupon</button>
  </form>

  <p id="result" style="font-weight:bold;"></p>

  <script>
    const form = document.getElementById('couponForm');
    const resultText = document.getElementById('result');

    form.addEventListener('submit', async (e) => {
      e.preventDefault();
      const code = document.getElementById('code').value;
      
      resultText.textContent = "Checking...";
      
      try {
        const response = await fetch('[https://script.google.com/macros/s/AKfycbxSk94MDcJ805Ksn4IMso8cVlVVM0opyYiwA2tjuAkI_eMlailmtDnCw20oZYZgnWiTgw/exec]', {
          method: 'POST',
          body: new URLSearchParams({ code })
        });
        
        const text = await response.text();
        resultText.textContent = text;
      } catch (err) {
        resultText.textContent = "Error validating coupon.";
        console.error(err);
      }
    });
  </script>
</body>
</html>
