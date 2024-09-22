<!DOCTYPE html>
<html>
<head>
    <title>Course Selling Platform</title>
</head>
<body>
    <h1>Upload Your Course Video</h1>
    <form action="/upload" method="POST" enctype="multipart/form-data">
        <input type="file" name="course_video" required>
        <button type="submit">Upload Video</button>
    </form>

    <h2>Payment</h2>
    <form action="/payment" method="POST">
        <input type="text" name="amount" placeholder="Enter amount" required>
        <button type="submit">Pay Now</button>
    </form>
</body>
</html>
const express = require('express');
const multer = require('multer');
const Razorpay = require('razorpay');
const app = express();

// Multer setup for video upload
const upload = multer({ dest: 'uploads/' });

// Razorpay Setup
const razorpay = new Razorpay({
    key_id: 'RAZORPAY_KEY_ID',
    key_secret: 'RAZORPAY_SECRET',
});

// Upload video route
app.post('/upload', upload.single('course_video'), (req, res) => {
    res.send('Video uploaded successfully');
});

// Payment route
app.post('/payment', async (req, res) => {
    const amount = req.body.amount * 100; // Convert to paise
    const options = {
        amount: amount,
        currency: 'INR',
        receipt: 'order_rcptid_11',
    };

    try {
        const order = await razorpay.orders.create(options);
        res.json(order);
    } catch (error) {
        res.status(500).send('Error in creating payment');
    }
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
npm init -y
npm install express multer razorpay
