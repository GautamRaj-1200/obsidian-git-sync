# Authentication and Authorization
## 1. Registration
- [x] Register Basic (username - email - password - etc - save to DB)
- [ ] Register Advanced (confirm email using otp or magic link)
    - [x] Using OTP
    - [ ] Using Magic Link
- [ ] Register with Image (handle image upload)
- [ ] Social Login (OAuth)
    - [ ] Google
    - [ ] Facebook
    - [ ] GitHub (or other providers)
- [ ] Email Verification
    - [ ] Send Verification Email after Registration
    - [ ] Re-send Verification Email (if not received)
- [ ] Rate Limiting for Registration
## 2. Login
- [x] Login with access and refresh tokens
- [ ] Social Login (OAuth)
    - [ ] Google
    - [ ] Facebook
    - [ ] GitHub
- [ ] ***Two-Factor Authentication (2FA)***
    - [ ] ***2FA via SMS/Email***
    - [ ] ***2FA via Authenticator Apps (e.g., Google Authenticator)***
- [ ] ***CAPTCHA (e.g., Google reCAPTCHA) for bots protection***
## 3. Logout
- [x] Clear access and refresh tokens
- [ ] ***Token Revocation (allow manual revocation for security)***
- [ ] ***Automatic token invalidation after password reset or suspicious activity***
## 4. Password Management
- [x] Password Strength Validation
- [ ] Forgot Password
    - [ ] OTP for Password Reset
    - [ ] Magic Link for Password Reset
- [ ] Password Change (for logged-in users)
- [ ] ***Prevent Password Reuse***
- [ ] ***Password Expiration Policy (optional)***
- [ ] ***Account Lockout after Failed Attempts***
    - [ ] ***Lock Account after multiple failed attempts***
    - [ ] ***Temporary Lockout (allow retry after specific time)***
- [ ] Rate Limiting for Login Attempts
## 5. Token and Session Management
- [x] JWT Verification Middleware
- [ ] ***Session Timeout after Inactivity (e.g., 15-30 minutes)***
- [ ] ***Device-Based Session Management***
    - [ ] ***Track Login Devices***
    - [ ] ***Log Out from Specific Devices***
- [ ] ***Refresh Token Rotation (enhanced security)***
- [ ] ***Token Usage Tracking (for suspicious activity detection)***
## 6. Security Features
- [ ] Cross-Origin Resource Sharing (CORS) Configuration
- [ ] ***Captcha for Registration/Login***
- [ ] ***IP Whitelisting/Blacklisting for Security***
- [ ] ***Single Sign-On (SSO) Integration (for enterprise apps)***
## 7. Auditing and Monitoring
- [ ] ***Logging and Auditing of Login/Logout Attempts***
- [ ] ***Track Failed Attempts***
- [ ] ***Log Token Usage (to detect suspicious activity)***
## 8. Optional Features
- [ ] User Account Deactivation/Deletion
- [ ] ***Multi-Account Linking (link multiple OAuth accounts)***
