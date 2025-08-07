# vishal[Uploading index.html.html…]()
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>कॉइन अर्निंग ऐप</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
            background-color: #fff;
            min-height: 100vh;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        
        /* हेडर स्टाइल */
        .header {
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            color: white;
            padding: 15px;
            text-align: center;
            position: relative;
        }
        
        .coin-display {
            position: absolute;
            right: 15px;
            top: 15px;
            background-color: rgba(255,255,255,0.2);
            padding: 5px 10px;
            border-radius: 20px;
            font-weight: bold;
            display: flex;
            align-items: center;
        }
        
        .coin-display img {
            width: 20px;
            margin-right: 5px;
        }
        
        /* मेनू ऑप्शन्स */
        .main-options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            padding: 15px;
        }
        
        .option-card {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            padding: 15px;
            text-align: center;
            transition: transform 0.3s;
        }
        
        .option-card:active {
            transform: scale(0.95);
        }
        
        .option-card img {
            width: 50px;
            height: 50px;
            margin-bottom: 10px;
        }
        
        /* बॉटम नेविगेशन */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            width: 100%;
            max-width: 500px;
            display: flex;
            background-color: white;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.1);
        }
        
        .nav-item {
            flex: 1;
            text-align: center;
            padding: 12px 0;
            font-size: 12px;
        }
        
        .nav-item.active {
            color: #6e8efb;
        }
        
        .nav-item img {
            width: 24px;
            height: 24px;
            margin-bottom: 5px;
        }
        
        /* लॉगिन पेज */
        .login-container {
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 80vh;
        }
        
        .login-container h2 {
            margin-bottom: 20px;
            color: #6e8efb;
        }
        
        .input-field {
            width: 100%;
            padding: 12px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }
        
        .submit-btn {
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            width: 100%;
        }
        
        /* मोडल स्टाइल */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0,0,0,0.5);
            z-index: 100;
            align-items: center;
            justify-content: center;
        }
        
        .modal-content {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            width: 90%;
            max-width: 400px;
        }
        
        .close-btn {
            float: right;
            font-size: 24px;
            cursor: pointer;
        }
        
        /* रेस्पॉन्सिव स्टाइल */
        @media (max-width: 400px) {
            .main-options {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- लॉगिन पेज (पहली बार ओपन करने पर) -->
    <div id="loginPage" class="container">
        <div class="login-container">
            <h2>ऐप में आपका स्वागत है!</h2>
            <p>पैसे कमाने के लिए रजिस्टर करें</p>
            <input type="text" id="userName" class="input-field" placeholder="आपका नाम">
            <input type="tel" id="mobileNumber" class="input-field" placeholder="मोबाइल नंबर">
            <button id="sendOtpBtn" class="submit-btn">OTP भेजें</button>
            
            <div id="otpSection" style="display: none; width: 100%;">
                <input type="text" id="otpInput" class="input-field" placeholder="OTP दर्ज करें">
                <button id="verifyOtpBtn" class="submit-btn">वेरिफाई करें</button>
            </div>
        </div>
    </div>
    
    <!-- मुख्य ऐप इंटरफेस (लॉगिन के बाद) -->
    <div id="appInterface" class="container" style="display: none;">
        <div class="header">
            <h2 id="welcomeMessage">नमस्ते, यूजर!</h2>
            <div class="coin-display" id="totalCoins">
                <img src="https://cdn-icons-png.flaticon.com/512/3132/3132693.png" alt="Coins">
                <span>0 कॉइन</span>
            </div>
        </div>
        
        <div class="main-options">
            <!-- ऑप्शन 1: एड वॉच -->
            <div class="option-card" onclick="openAdSection()">
                <img src="https://cdn-icons-png.flaticon.com/512/2491/2491995.png" alt="Ads">
                <h3>विज्ञापन देखें</h3>
                <p>2-10 कॉइन कमाएं</p>
            </div>
            
            <!-- ऑप्शन 2: रेफर एंड अर्न -->
            <div class="option-card" onclick="openReferSection()">
                <img src="https://cdn-icons-png.flaticon.com/512/3132/3132693.png" alt="Refer">
                <h3>दोस्तों को भेजें</h3>
                <p>400 कॉइन कमाएं</p>
            </div>
            
            <!-- ऑप्शन 3: टास्क -->
            <div class="option-card" onclick="openTasksSection()">
                <img src="https://cdn-icons-png.flaticon.com/512/3281/3281289.png" alt="Tasks">
                <h3>टास्क पूरा करें</h3>
                <p>10-500 कॉइन कमाएं</p>
            </div>
            
            <!-- ऑप्शन 4: गेम्स -->
            <div class="option-card" onclick="openGamesSection()">
                <img src="https://cdn-icons-png.flaticon.com/512/2604/2604672.png" alt="Games">
                <h3>गेम खेलें</h3>
                <p>कॉइन जीतें</p>
            </div>
            
            <!-- ऑप्शन 5: ऐप इंफो -->
            <div class="option-card" onclick="openAppInfo()">
                <img src="https://cdn-icons-png.flaticon.com/512/1570/1570913.png" alt="Info">
                <h3>ऐप की जानकारी</h3>
                <p>कैसे काम करता है</p>
            </div>
        </div>
        
        <!-- बॉटम नेविगेशन -->
        <div class="bottom-nav">
            <div class="nav-item active" onclick="showHome()">
                <img src="https://cdn-icons-png.flaticon.com/512/263/263115.png" alt="Home">
                <div>होम</div>
            </div>
            <div class="nav-item" onclick="showWithdraw()">
                <img src="https://cdn-icons-png.flaticon.com/512/3132/3132693.png" alt="Withdraw">
                <div>विड्रॉल</div>
            </div>
            <div class="nav-item" onclick="showAccount()">
                <img src="https://cdn-icons-png.flaticon.com/512/1077/1077063.png" alt="Account">
                <div>अकाउंट</div>
            </div>
        </div>
    </div>
    
    <!-- विड्रॉल मोडल -->
    <div id="withdrawModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('withdrawModal')">&times;</span>
            <h2>विड्रॉल करें</h2>
            <p>100 कॉइन = ₹1</p>
            <p>आपके पास: <span id="availableCoins">0</span> कॉइन</p>
            
            <div style="margin: 15px 0;">
                <label for="withdrawAmount">विड्रॉल राशि (₹ में):</label>
                <input type="number" id="withdrawAmount" class="input-field" placeholder="10 रुपये से शुरू">
            </div>
            
            <div style="margin: 15px 0;">
                <label>भुगतान विधि:</label>
                <div style="display: flex; flex-wrap: wrap; gap: 10px; margin-top: 10px;">
                    <div style="flex: 1; text-align: center;">
                        <img src="https://cdn-icons-png.flaticon.com/512/825/825454.png" width="40">
                        <p>UPI</p>
                    </div>
                    <div style="flex: 1; text-align: center;">
                        <img src="https://cdn-icons-png.flaticon.com/512/2504/2504739.png" width="40">
                        <p>Google Pay</p>
                    </div>
                    <div style="flex: 1; text-align: center;">
                        <img src="https://cdn-icons-png.flaticon.com/512/2504/2504903.png" width="40">
                        <p>Paytm</p>
                    </div>
                </div>
            </div>
            
            <div style="margin: 15px 0;">
                <label for="upiId">UPI ID:</label>
                <input type="text" id="upiId" class="input-field" placeholder="yourname@upi">
            </div>
            
            <button class="submit-btn" onclick="requestWithdrawal()">विड्रॉल रिक्वेस्ट</button>
        </div>
    </div>
    
    <!-- अकाउंट मोडल -->
    <div id="accountModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('accountModal')">&times;</span>
            <h2>अकाउंट</h2>
            
            <div style="text-align: center; margin: 15px 0;">
                <img src="https://cdn-icons-png.flaticon.com/512/3135/3135715.png" width="80" style="border-radius: 50%;">
                <h3 id="accountUserName">यूजर नाम</h3>
                <p id="accountMobile">+91 XXXXX XXXXX</p>
            </div>
            
            <div style="margin: 20px 0;">
                <div style="display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid #eee;">
                    <span>कुल कॉइन:</span>
                    <span id="accountCoins">0</span>
                </div>
                <div style="display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid #eee;">
                    <span>कुल विड्रॉल:</span>
                    <span>₹0</span>
                </div>
                <div style="display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid #eee;">
                    <span>रेफर कॉइन:</span>
                    <span>0</span>
                </div>
            </div>
            
            <button class="submit-btn" style="margin-bottom: 10px;" onclick="shareApp()">
                <img src="https://cdn-icons-png.flaticon.com/512/1358/1358023.png" width="20" style="vertical-align: middle;">
                ऐप शेयर करें
            </button>
            
            <button class="submit-btn" style="background-color: #f44336; margin-bottom: 10px;" onclick="openHelp()">
                <img src="https://cdn-icons-png.flaticon.com/512/159/159832.png" width="20" style="vertical-align: middle;">
                हेल्प
            </button>
            
            <button class="submit-btn" style="background-color: #9e9e9e;" onclick="logout()">
                <img src="https://cdn-icons-png.flaticon.com/512/1828/1828479.png" width="20" style="vertical-align: middle;">
                लॉगआउट
            </button>
        </div>
    </div>
    
    <!-- हेल्प मोडल -->
    <div id="helpModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('helpModal')">&times;</span>
            <h2>हमसे संपर्क करें</h2>
            
            <p style="margin: 15px 0;">किसी भी समस्या के लिए हमसे संपर्क करें:</p>
            
            <div style="display: flex; align-items: center; margin: 15px 0;">
                <img src="https://cdn-icons-png.flaticon.com/512/455/455705.png" width="30" style="margin-right: 10px;">
                <span>+91 7973831205</span>
            </div>
            
            <div style="display: flex; align-items: center; margin: 15px 0;">
                <img src="https://cdn-icons-png.flaticon.com/512/732/732200.png" width="30" style="margin-right: 10px;">
                <span>vs1630365@gmail.com</span>
            </div>
            
            <textarea class="input-field" placeholder="आपका संदेश..." style="height: 100px; margin: 15px 0;"></textarea>
            
            <button class="submit-btn">संदेश भेजें</button>
        </div>
    </div>
    
    <script>
        // वेरिएबल्स
        let userData = {
            name: "",
            mobile: "",
            coins: 0,
            loggedIn: false
        };
        
        // पेज लोड होने पर
        document.addEventListener('DOMContentLoaded', function() {
            // चेक करें अगर यूजर पहले से लॉगिन है
            const savedUser = localStorage.getItem('coinAppUser');
            if(savedUser) {
                userData = JSON.parse(savedUser);
                if(userData.loggedIn) {
                    showAppInterface();
                }
            }
        });
        
        // OTP भेजें बटन
        document.getElementById('sendOtpBtn').addEventListener('click', function() {
            const mobile = document.getElementById('mobileNumber').value;
            const name = document.getElementById('userName').value;
            
            if(!name || !mobile || mobile.length !== 10) {
                alert("कृपया वैध नाम और मोबाइल नंबर दर्ज करें");
                return;
            }
            
            // सिमुलेटेड OTP भेजना (असली ऐप में सर्वर से भेजा जाएगा)
            document.getElementById('otpSection').style.display = 'block';
            alert("OTP भेजा गया: 123456 (डेमो के लिए)");
            
            // यूजर डेटा सेव करें (अभी लॉगिन नहीं हुआ)
            userData.name = name;
            userData.mobile = mobile;
        });
        
        // OTP वेरिफाई बटन
        document.getElementById('verifyOtpBtn').addEventListener('click', function() {
            const otp = document.getElementById('otpInput').value;
            
            if(otp === "123456") { // डेमो OTP
                userData.loggedIn = true;
                localStorage.setItem('coinAppUser', JSON.stringify(userData));
                showAppInterface();
            } else {
                alert("गलत OTP, कृपया फिर से प्रयास करें");
            }
        });
        
        // ऐप इंटरफेस दिखाएं
        function showAppInterface() {
            document.getElementById('loginPage').style.display = 'none';
            document.getElementById('appInterface').style.display = 'block';
            
            // यूजर डेटा अपडेट करें
            document.getElementById('welcomeMessage').textContent = `नमस्ते, ${userData.name}!`;
            document.getElementById('accountUserName').textContent = userData.name;
            document.getElementById('accountMobile').textContent = `+91 ${userData.mobile}`;
            updateCoinDisplay();
        }
        
        // कॉइन डिस्प्ले अपडेट करें
        function updateCoinDisplay() {
            document.getElementById('totalCoins').innerHTML = `
                <img src="https://cdn-icons-png.flaticon.com/512/3132/3132693.png" alt="Coins">
                <span>${userData.coins} कॉइन</span>
            `;
            
            document.getElementById('availableCoins').textContent = userData.coins;
            document.getElementById('accountCoins').textContent = userData.coins;
        }
        
        // मोडल खोलें/बंद करें
        function openModal(modalId) {
            document.getElementById(modalId).style.display = 'flex';
        }
        
        function closeModal(modalId) {
            document.getElementById(modalId).style.display = 'none';
        }
        
        // विभिन्न सेक्शन खोलने के फंक्शन
        function openAdSection() {
            // रैंडम कॉइन जनरेट करें (2, 4, या 10)
            const coinsEarned = [2, 4, 10][Math.floor(Math.random() * 3)];
            
            userData.coins += coinsEarned;
            localStorage.setItem('coinAppUser', JSON.stringify(userData));
            updateCoinDisplay();
            
            alert(`बधाई हो! आपने ${coinsEarned} कॉइन कमाए!\nविज्ञापन देखने के लिए धन्यवाद।`);
        }
        
        function openReferSection() {
            alert("अपने दोस्तों को इस लिंक से ज्वाइन करवाएं: https://example.com/refer/${userData.mobile}\nजब आपका दोस्त रजिस्टर करेगा तो आपको 400 कॉइन मिलेंगे!");
        }
        
        function openTasksSection() {
            alert("टास्क सेक्शन:\n1. विज्ञापन देखें - 10 कॉइन\n2. ऐप रेट करें - 20 कॉइन\n3. सोशल मीडिया पर शेयर करें - 50 कॉइन");
        }
        
        function openGamesSection() {
            alert("गेम्स सेक्शन:\n1. लूडो\n2. सांप सीढ़ी\n3. बात गेम\nगेम्स खेलकर कॉइन जीतें!");
        }
        
        function openAppInfo() {
            alert("ऐप कैसे काम करता है:\n1. विज्ञापन देखकर कॉइन कमाएं\n2. दोस्तों को रेफर करके कॉइन कमाएं\n3. टास्क पूरा करके कॉइन कमाएं\n4. गेम्स खेलकर कॉइन जीतें\n5. 100 कॉइन = ₹1 विड्रॉल करें");
        }
        
        // बॉटम नेविगेशन फंक्शन
        function showHome() {
            // होम पहले से दिख रहा है
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('active');
            });
            document.querySelectorAll('.nav-item')[0].classList.add('active');
        }
        
        function showWithdraw() {
            openModal('withdrawModal');
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('active');
            });
            document.querySelectorAll('.nav-item')[1].classList.add('active');
        }
        
        function showAccount() {
            openModal('accountModal');
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('active');
            });
            document.querySelectorAll('.nav-item')[2].classList.add('active');
        }
        
        // विड्रॉल रिक्वेस्ट
        function requestWithdrawal() {
            const amount = parseInt(document.getElementById('withdrawAmount').value);
            const upiId = document.getElementById('upiId').value;
            
            if(!amount || amount < 10) {
                alert("कृपया 10 रुपये से अधिक की राशि दर्ज करें");
                return;
            }
            
            const coinsNeeded = amount * 100;
            
            if(userData.coins < coinsNeeded) {
                alert(`आपके पास पर्याप्त कॉइन नहीं हैं।\nआवश्यक: ${coinsNeeded} कॉइन\nउपलब्ध: ${userData.coins} कॉइन`);
                return;
            }
            
            if(!upiId || !upiId.includes('@')) {
                alert("कृपया वैध UPI ID दर्ज करें");
                return;
            }
            
            userData.coins -= coinsNeeded;
            localStorage.setItem('coinAppUser', JSON.stringify(userData));
            updateCoinDisplay();
            
            closeModal('withdrawModal');
            alert(`आपकी विड्रॉल रिक्वेस्ट ₹${amount} के लिए स्वीकार की गई है।\n48 घंटों में आपके UPI (${upiId}) पर भुगतान कर दिया जाएगा।`);
        }
        
        // ऐप शेयर करें
        function shareApp() {
            alert("ऐप शेयर करें:\nअपने दोस्तों को इस लिंक से ज्वाइन करवाएं: https://example.com/refer/${userData.mobile}\nआपको 400 कॉइन मिलेंगे जब आपका दोस्त रजिस्टर करेगा!");
        }
        
        // हेल्प ओपन करें
        function openHelp() {
            closeModal('accountModal');
            openModal('helpModal');
        }
        
        // लॉगआउट
        function logout() {
            userData.loggedIn = false;
            localStorage.setItem('coinAppUser', JSON.stringify(userData));
            
            document.getElementById('appInterface').style.display = 'none';
            document.getElementById('loginPage').style.display = 'block';
            
            // रीसेट फॉर्म
            document.getElementById('userName').value = userData.name;
            document.getElementById('mobileNumber').value = userData.mobile;
            document.getElementById('otpSection').style.display = 'none';
        }
    </script>
</body>
</html>
