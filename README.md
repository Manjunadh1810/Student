<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>College Portal - Login</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .login-container {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            padding: 40px;
            width: 100%;
            max-width: 400px;
            position: relative;
            overflow: hidden;
        }

        .login-container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, #667eea, #764ba2);
        }

        .college-logo {
            text-align: center;
            margin-bottom: 30px;
        }

        .college-logo h1 {
            color: #333;
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .college-logo p {
            color: #666;
            font-size: 14px;
            font-weight: 300;
        }

        .form-group {
            margin-bottom: 20px;
            position: relative;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 500;
            font-size: 14px;
        }

        .form-group input {
            width: 100%;
            padding: 12px 16px;
            border: 2px solid #e1e1e1;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s ease;
            background: #fff;
        }

        .form-group input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .form-group input.error {
            border-color: #e74c3c;
            box-shadow: 0 0 0 3px rgba(231, 76, 60, 0.1);
        }

        .error-message {
            color: #e74c3c;
            font-size: 12px;
            margin-top: 5px;
            display: none;
        }

        .user-type {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .user-type label {
            flex: 1;
            text-align: center;
            padding: 10px;
            border: 2px solid #e1e1e1;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 14px;
            font-weight: 500;
        }

        .user-type input[type="radio"] {
            display: none;
        }

        .user-type input[type="radio"]:checked + label {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }

        .remember-forgot {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            font-size: 14px;
        }

        .remember-me {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .remember-me input[type="checkbox"] {
            width: auto;
        }

        .forgot-password {
            color: #667eea;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s ease;
        }

        .forgot-password:hover {
            color: #764ba2;
        }

        .login-btn {
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 20px;
        }

        .login-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
        }

        .login-btn:active {
            transform: translateY(0);
        }

        .login-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .divider {
            text-align: center;
            margin: 20px 0;
            position: relative;
            color: #666;
        }

        .divider::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 0;
            right: 0;
            height: 1px;
            background: #e1e1e1;
        }

        .divider span {
            background: rgba(255, 255, 255, 0.95);
            padding: 0 15px;
            font-size: 14px;
        }

        .register-link {
            text-align: center;
            margin-top: 20px;
        }

        .register-link a {
            color: #667eea;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s ease;
        }

        .register-link a:hover {
            color: #764ba2;
        }

        .success-message {
            background: #d4edda;
            color: #155724;
            padding: 12px;
            border-radius: 10px;
            margin-bottom: 20px;
            display: none;
            text-align: center;
            font-size: 14px;
        }

        @media (max-width: 480px) {
            .login-container {
                padding: 30px 20px;
            }

            .college-logo h1 {
                font-size: 24px;
            }

            .user-type {
                flex-direction: column;
            }

            .remember-forgot {
                flex-direction: column;
                gap: 10px;
                align-items: stretch;
            }
        }

        .loading {
            display: none;
            width: 20px;
            height: 20px;
            border: 2px solid #ffffff;
            border-top: 2px solid transparent;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-right: 10px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="login-container">
        <div class="college-logo">
            <h1>University Portal</h1>
            <p>Academic Excellence • Innovation • Leadership</p>
        </div>

        <div class="success-message" id="successMessage">
            Login successful! Redirecting to dashboard...
        </div>

        <form id="loginForm">
            <div class="user-type">
                <input type="radio" id="student" name="userType" value="student" checked>
                <label for="student">Student</label>
                
                <input type="radio" id="faculty" name="userType" value="faculty">
                <label for="faculty">Faculty</label>
                
                <input type="radio" id="admin" name="userType" value="admin">
                <label for="admin">Admin</label>
            </div>

            <div class="form-group">
                <label for="username">Username / Student ID</label>
                <input type="text" id="username" name="username" required>
                <div class="error-message" id="usernameError">Please enter a valid username</div>
            </div>

            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" id="password" name="password" required>
                <div class="error-message" id="passwordError">Password must be at least 6 characters</div>
            </div>

            <div class="remember-forgot">
                <div class="remember-me">
                    <input type="checkbox" id="rememberMe" name="rememberMe">
                    <label for="rememberMe">Remember me</label>
                </div>
                <a href="#" class="forgot-password">Forgot Password?</a>
            </div>

            <button type="submit" class="login-btn" id="loginBtn">
                <span class="loading" id="loading"></span>
                <span id="btnText">Login to Portal</span>
            </button>
        </form>

        <div class="divider">
            <span>or</span>
        </div>

        <div class="register-link">
            <p>Don't have an account? <a href="#">Register here</a></p>
        </div>
    </div>

    <script>
        // Form validation and submission
        const loginForm = document.getElementById('loginForm');
        const usernameInput = document.getElementById('username');
        const passwordInput = document.getElementById('password');
        const loginBtn = document.getElementById('loginBtn');
        const loading = document.getElementById('loading');
        const btnText = document.getElementById('btnText');
        const successMessage = document.getElementById('successMessage');

        // Real-time validation
        usernameInput.addEventListener('input', validateUsername);
        passwordInput.addEventListener('input', validatePassword);

        function validateUsername() {
            const username = usernameInput.value.trim();
            const errorElement = document.getElementById('usernameError');
            
            if (username.length < 3) {
                showError(usernameInput, errorElement, 'Username must be at least 3 characters');
                return false;
            } else {
                hideError(usernameInput, errorElement);
                return true;
            }
        }

        function validatePassword() {
            const password = passwordInput.value;
            const errorElement = document.getElementById('passwordError');
            
            if (password.length < 6) {
                showError(passwordInput, errorElement, 'Password must be at least 6 characters');
                return false;
            } else {
                hideError(passwordInput, errorElement);
                return true;
            }
        }

        function showError(input, errorElement, message) {
            input.classList.add('error');
            errorElement.textContent = message;
            errorElement.style.display = 'block';
        }

        function hideError(input, errorElement) {
            input.classList.remove('error');
            errorElement.style.display = 'none';
        }

        // Form submission
        loginForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const isUsernameValid = validateUsername();
            const isPasswordValid = validatePassword();
            
            if (isUsernameValid && isPasswordValid) {
                simulateLogin();
            }
        });

        function simulateLogin() {
            // Show loading state
            loginBtn.disabled = true;
            loading.style.display = 'inline-block';
            btnText.textContent = 'Logging in...';
            
            // Simulate API call
            setTimeout(() => {
                // Hide loading state
                loginBtn.disabled = false;
                loading.style.display = 'none';
                btnText.textContent = 'Login to Portal';
                
                // Show success message
                successMessage.style.display = 'block';
                
                // Get form data
                const formData = new FormData(loginForm);
                const userData = {
                    username: formData.get('username'),
                    userType: formData.get('userType'),
                    rememberMe: formData.get('rememberMe') === 'on'
                };
                
                console.log('Login data:', userData);
                
                // Simulate redirect after 2 seconds
                setTimeout(() => {
                    alert(`Welcome ${userData.username}! You would be redirected to the ${userData.userType} dashboard.`);
                    // In a real application, you would redirect to the appropriate dashboard
                    // window.location.href = `/${userData.userType}/dashboard`;
                }, 2000);
                
            }, 1500);
        }

        // User type selection animation
        const userTypeInputs = document.querySelectorAll('input[name="userType"]');
        userTypeInputs.forEach(input => {
            input.addEventListener('change', function() {
                const label = document.querySelector(`label[for="${this.id}"]`);
                // Update username placeholder based on user type
                if (this.value === 'student') {
                    usernameInput.placeholder = 'Enter Student ID';
                } else if (this.value === 'faculty') {
                    usernameInput.placeholder = 'Enter Faculty ID';
                } else {
                    usernameInput.placeholder = 'Enter Admin Username';
                }
            });
        });

        // Forgot password link
        document.querySelector('.forgot-password').addEventListener('click', function(e) {
            e.preventDefault();
            alert('Forgot password feature would redirect to password reset page.');
        });

        // Register link
        document.querySelector('.register-link a').addEventListener('click', function(e) {
            e.preventDefault();
            alert('Registration feature would redirect to registration page.');
        });

        // Initialize placeholder
        usernameInput.placeholder = 'Enter Student ID';
    </script>
</body>
</html>
