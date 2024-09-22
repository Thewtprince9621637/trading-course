<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Prince Wealth</title>
</head>
<body>
    <h1>Buy Video Course - ₹4499</h1>
    <button id="pay-button">Pay Now</button>

    <script src="https://checkout.razorpay.com/v1/checkout.js"></script>
    <script>
        document.getElementById('pay-button').onclick = function () {
            var options = {
                "key": "YOUR_RAZORPAY_KEY", // Razorpay Key ID
                "amount": 4900, // Amount is in paise
                "currency": "INR",
                "name": "The Prince Wealth",
                "description": "Video Course Purchase",
                "image": "https://yourlogo.com/logo.png", // Optional
                "handler": function (response){
                    alert("Payment successful: " + response.razorpay_payment_id);
                    // Here you can handle video access after payment
                },
                "prefill": {
                    "contact": "7068721720", // Pre-filled contact
                    "email": "your-email@example.com"
                },
                "theme": {
                    "color": "#3399cc"
                }
            };
            var rzp = new Razorpay(options);
            rzp.open();
        };
    </script>
</body>
</html>
