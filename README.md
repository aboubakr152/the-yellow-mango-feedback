<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.yellow-mango-container {
    font-family: 'Arial', sans-serif;
    background: #F1C40F;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
}

.yellow-mango-form {
    background: white;
    border-radius: 20px;
    box-shadow: 0 10px 40px rgba(0,0,0,0.1);
    padding: 40px;
    max-width: 500px;
    width: 100%;
    text-align: center;
    position: relative;
    overflow: hidden;
}

.yellow-mango-form::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 5px;
    background: #F39C12;
}

.ym-logo {
    font-size: 2.5rem;
    font-weight: bold;
    color: #2C3E50;
    margin-bottom: 10px;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
}

.ym-header-text {
    font-size: 1.2rem;
    color: #333;
    margin-bottom: 15px;
    font-weight: 600;
}

.ym-subheader-text {
    font-size: 1rem;
    color: #555;
    margin-bottom: 30px;
}

.ym-form-group {
    margin-bottom: 20px;
    text-align: left;
}

.ym-form-group label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
    color: #333;
}

.ym-input {
    width: 100%;
    padding: 12px;
    border: 2px solid #ddd;
    border-radius: 10px;
    font-size: 1rem;
    transition: all 0.3s ease;
}

.ym-input:focus {
    outline: none;
    border-color: #F7DC6F;
    box-shadow: 0 0 10px rgba(247, 220, 111, 0.5);
}

.ym-button-group {
    display: flex;
    gap: 15px;
    margin: 30px 0;
}

.ym-btn {
    flex: 1;
    padding: 15px;
    border: none;
    border-radius: 10px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.ym-btn-happy {
    background: #3498DB;
    color: white;
}

.ym-btn-unhappy {
    background: #E74C3C;
    color: white;
}

.ym-btn-primary {
    background: #F39C12;
    color: white;
    width: 100%;
    margin-top: 20px;
}

.ym-btn-return {
    background: #95A5A6;
    color: white;
    padding: 10px 20px;
    font-size: 0.9rem;
    margin-top: 15px;
    width: 100%;
}

.ym-textarea {
    width: 100%;
    padding: 12px;
    border: 2px solid #ddd;
    border-radius: 10px;
    font-size: 1rem;
    resize: vertical;
    min-height: 100px;
    font-family: Arial, sans-serif;
}

.ym-message {
    margin: 20px 0;
    padding: 20px;
    border-radius: 10px;
    font-size: 1rem;
    line-height: 1.6;
}

.ym-message-success {
    background: #EBF3FD;
    color: #3498DB;
    border-left: 4px solid #3498DB;
}

.ym-message-sorry {
    background: #FDEDEC;
    color: #E74C3C;
    border-left: 4px solid #E74C3C;
}

.ym-stars {
    font-size: 3rem;
    color: #F7DC6F;
    margin: 20px 0;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
}

.ym-hidden {
    display: none;
}

.ym-countdown {
    font-size: 1.1rem;
    color: #F39C12;
    font-weight: bold;
    margin-top: 15px;
}
</style>

<div class="yellow-mango-container">
    <div class="yellow-mango-form">
        <div class="ym-logo">The Yellow Mango</div>
        
        <!-- Initial Form -->
        <div id="ym-initial-form">
            <div class="ym-header-text">This will only take about 30 seconds we promise</div>
            <div class="ym-subheader-text">Please provide accurate details so we can locate your Amazon order</div>
            
            <div class="ym-form-group">
                <label for="ym-customer-name">Your Name:</label>
                <input type="text" class="ym-input" id="ym-customer-name" placeholder="Enter your full name">
            </div>
            
            <div class="ym-form-group">
                <label for="ym-order-number">Order Number:</label>
                <input type="text" class="ym-input" id="ym-order-number" placeholder="Enter your Amazon order number">
            </div>
            
            <button class="ym-btn ym-btn-primary" onclick="ymProceedToSatisfaction()">Continue</button>
        </div>

        <!-- Satisfaction Question -->
        <div id="ym-satisfaction-question" class="ym-hidden">
            <div class="ym-header-text">Were you happy with your order?</div>
            <div class="ym-button-group">
                <button class="ym-btn ym-btn-happy" onclick="ymHandleHappy()">Yes I am happy</button>
                <button class="ym-btn ym-btn-unhappy" onclick="ymHandleUnhappy()">No I am not satisfied</button>
            </div>
        </div>

        <!-- Unhappy Path -->
        <div id="ym-unhappy-feedback" class="ym-hidden">
            <div class="ym-message ym-message-sorry">
                We are so sorry we could not meet your expectations. Please provide feedback of what you didn't like specifically. Your feedback is very important to us as it genuinely helps us improve our products.
            </div>
            
            <div class="ym-form-group">
                <label for="ym-negative-feedback">What didn't you like?</label>
                <textarea class="ym-textarea" id="ym-negative-feedback" placeholder="Please share your honest feedback..."></textarea>
            </div>
            
            <button class="ym-btn ym-btn-primary" onclick="ymSubmitNegativeFeedback()">Submit Feedback</button>
            <button class="ym-btn ym-btn-return" onclick="ymReturnToStart()">← Return to Start</button>
        </div>

        <!-- Unhappy Thank You -->
        <div id="ym-unhappy-thankyou" class="ym-hidden">
            <div class="ym-message ym-message-success">
                Thank you so much for your feedback. Your response is being processed. We will match it with your order number and we will process your $5 feedback reward within the next few business days. We wish you all the best and thank you for shopping with The Yellow Mango.
            </div>
        </div>

        <!-- Happy Path -->
        <div id="ym-happy-feedback" class="ym-hidden">
            <div class="ym-message ym-message-success">
                We are glad you are happy with the product you ordered! Please give us some feedback about what you liked.
            </div>
            
            <div class="ym-form-group">
                <label for="ym-positive-feedback">What did you like about your order?</label>
                <textarea class="ym-textarea" id="ym-positive-feedback" placeholder="Tell us what you loved about your experience..."></textarea>
            </div>
            
            <button class="ym-btn ym-btn-primary" onclick="ymSubmitPositiveFeedback()">Submit Feedback</button>
        </div>

        <!-- Review Instructions -->
        <div id="ym-review-instructions" class="ym-hidden">
            <div class="ym-message ym-message-success">
                Your feedback has been copied to your clipboard! Please share it as a 5 star review on Amazon.
            </div>
            
            <button class="ym-btn ym-btn-primary" onclick="ymShareReview()">Share as 5 Star Review on Amazon</button>
        </div>

        <!-- Final Review Steps -->
        <div id="ym-final-steps" class="ym-hidden">
            <div class="ym-stars">⭐⭐⭐⭐⭐</div>
            <div class="ym-message ym-message-success">
                Please select 5 stars, click paste in the form and submit.
                <br><br>
                Your Amazon review page will open automatically now and your $5 feedback reward will be processed soon!
                <div class="ym-countdown" id="ym-countdown">Opening Amazon in 6 seconds...</div>
            </div>
        </div>
    </div>
</div>

<script>
let ymCustomerData = {};

function ymSaveFeedback(data) {
    // Email yourself the feedback data
    console.log('Customer Feedback:', data);
    
    // You can also use Squarespace forms to collect this data
    // For now, it's saved in browser console - check browser dev tools
}

function ymReturnToStart() {
    document.getElementById('ym-satisfaction-question').classList.add('ym-hidden');
    document.getElementById('ym-unhappy-feedback').classList.add('ym-hidden');
    document.getElementById('ym-unhappy-thankyou').classList.add('ym-hidden');
    document.getElementById('ym-happy-feedback').classList.add('ym-hidden');
    document.getElementById('ym-review-instructions').classList.add('ym-hidden');
    document.getElementById('ym-final-steps').classList.add('ym-hidden');
    
    document.getElementById('ym-initial-form').classList.remove('ym-hidden');
    
    document.getElementById('ym-customer-name').value = '';
    document.getElementById('ym-order-number').value = '';
    document.getElementById('ym-negative-feedback').value = '';
    document.getElementById('ym-positive-feedback').value = '';
    
    ymCustomerData = {};
}

function ymProceedToSatisfaction() {
    const name = document.getElementById('ym-customer-name').value.trim();
    const orderNumber = document.getElementById('ym-order-number').value.trim();
    
    if (!name || !orderNumber) {
        alert('Please fill in both your name and order number.');
        return;
    }
    
    ymCustomerData.name = name;
    ymCustomerData.orderNumber = orderNumber;
    
    document.getElementById('ym-initial-form').classList.add('ym-hidden');
    document.getElementById('ym-satisfaction-question').classList.remove('ym-hidden');
}

function ymHandleUnhappy() {
    document.getElementById('ym-satisfaction-question').classList.add('ym-hidden');
    document.getElementById('ym-unhappy-feedback').classList.remove('ym-hidden');
}

function ymSubmitNegativeFeedback() {
    const feedback = document.getElementById('ym-negative-feedback').value.trim();
    
    if (!feedback) {
        alert('Please provide your feedback before submitting.');
        return;
    }
    
    ymCustomerData.feedback = feedback;
    ymCustomerData.satisfied = false;
    ymCustomerData.timestamp = new Date().toLocaleString();
    
    ymSaveFeedback(ymCustomerData);
    
    document.getElementById('ym-unhappy-feedback').classList.add('ym-hidden');
    document.getElementById('ym-unhappy-thankyou').classList.remove('ym-hidden');
}

function ymHandleHappy() {
    document.getElementById('ym-satisfaction-question').classList.add('ym-hidden');
    document.getElementById('ym-happy-feedback').classList.remove('ym-hidden');
}

function ymSubmitPositiveFeedback() {
    const feedback = document.getElementById('ym-positive-feedback').value.trim();
    
    if (!feedback) {
        alert('Please provide your feedback before submitting.');
        return;
    }
    
    ymCustomerData.feedback = feedback;
    ymCustomerData.satisfied = true;
    ymCustomerData.timestamp = new Date().toLocaleString();
    
    ymSaveFeedback(ymCustomerData);
    
    navigator.clipboard.writeText(feedback).then(function() {
        document.getElementById('ym-happy-feedback').classList.add('ym-hidden');
        document.getElementById('ym-review-instructions').classList.remove('ym-hidden');
    }).catch(function(err) {
        document.getElementById('ym-happy-feedback').classList.add('ym-hidden');
        document.getElementById('ym-review-instructions').classList.remove('ym-hidden');
    });
}

function ymShareReview() {
    document.getElementById('ym-review-instructions').classList.add('ym-hidden');
    document.getElementById('ym-final-steps').classList.remove('ym-hidden');
    
    let seconds = 6;
    const countdownElement = document.getElementById('ym-countdown');
    
    const countdownInterval = setInterval(() => {
        seconds--;
        countdownElement.textContent = `Opening Amazon in ${seconds} seconds...`;
        
        if (seconds <= 0) {
            clearInterval(countdownInterval);
            window.open('https://www.amazon.com/review/create-review/error?ie=UTF8&channel=glance-detail&asin=B0F82Z2C52', '_blank');
        }
    }, 1000);
}
</script>
