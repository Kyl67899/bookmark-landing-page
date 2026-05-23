# 🔒 Security Policy & Admin Authentication Setup

## 🚨 Critical: Initial Configuration Required

Your Recipe_App now includes enterprise-grade security features. Follow these steps immediately:

### Step 1: Set Up Environment Variables

1. Copy `.env.example` to `.env.local`:
```bash
cp .env.example .env.local
```

2. Edit `.env.local` and set secure values:
```
NEXT_PUBLIC_ADMIN_EMAIL=your-secure-email@domain.com
NEXT_PUBLIC_ADMIN_PASSWORD=YourStrongPassword123!@#
PASSWORD_SALT=your-super-secret-random-salt-here
```

### Step 2: Create Strong Admin Password

Your admin password MUST meet these requirements:
- ✅ At least 8 characters
- ✅ Contains uppercase letter (A-Z)
- ✅ Contains lowercase letter (a-z)
- ✅ Contains number (0-9)
- ✅ Contains special character (!@#$%^&*)

**Example strong password:** `RecipeAdmin@2024!`

### Step 3: Generate Random Salt

Generate a cryptographically secure salt:

**On macOS/Linux:**
```bash
openssl rand -hex 32
```

**Using Node.js:**
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

---

## 🛡️ Security Features Implemented

### 1. **Password Hashing**
- Passwords hashed using SHA-256 with salt
- Never stored in plain text
- Original password never transmitted

### 2. **Rate Limiting**
- Max 5 login attempts per email in 15-minute window
- Prevents brute force attacks
- Auto-clears after successful login

### 3. **Account Lockout**
- Account locked after 5 failed attempts
- Prevents unauthorized access attempts
- Lock reason: "Account is locked. Contact support."

### 4. **Session Management**
- Sessions expire after 24 hours
- Unique session tokens for each login
- Automatic cleanup of expired sessions

### 5. **Input Validation & Sanitization**
- Email format validation (RFC 5322)
- Password strength validation
- Input length limits (255 chars max)
- XSS prevention (removes dangerous characters)

### 6. **Security Logging**
- All login attempts logged (success/failure)
- Rate limit violations tracked
- Account lockouts recorded
- Suspicious activity monitored

### 7. **Protected Routes**
- Admin routes require admin role
- User routes require authentication
- Automatic redirect to login if unauthorized

---

## 🚀 Admin Login Instructions

### First Time Login

1. Go to: `http://localhost:3000/login`
2. Email: `admin@recipehub.dev` (or your configured email)
3. Password: `Admin@12345` (or your configured password)
4. ✅ You'll be redirected to `/admin` dashboard

### Accessing Admin Dashboard

- URL: `http://localhost:3000/admin`
- Manage recipes, users, and analytics
- View security logs
- Monitor user activity

---

## ⚠️ Security Best Practices

### For Development:
- ✅ Use unique password different from production
- ✅ Store `.env.local` locally only
- ✅ Never commit `.env.local` to git
- ✅ Test rate limiting and lockout features
- ✅ Monitor security logs during testing

### For Production:
- ✅ Use HTTPS/TLS encryption
- ✅ Implement environment secrets management
- ✅ Set up 2FA/MFA for admin accounts
- ✅ Enable security audit logging to database
- ✅ Implement password expiration policy
- ✅ Rate limit by IP address + email
- ✅ Add CAPTCHA after 3 failed attempts
- ✅ Monitor unusual login patterns

---

## 🆘 Troubleshooting

### "Account is locked. Contact support."
**Cause:** 5 failed login attempts exceeded
**Solution:** Reset lockout in development or contact admin

### "Too many login attempts. Try again in 15 minutes."
**Cause:** Rate limit active
**Solution:** Wait 15 minutes before retrying

### "Password must contain..."
**Cause:** Password doesn't meet strength requirements
**Solution:** Use uppercase, lowercase, numbers, and special characters

---

## Reporting a Vulnerability

If you discover a security vulnerability in this application:

1. **DO NOT** publicly disclose the vulnerability
2. Email: security@recipehub.dev
3. Include:
   - Description of vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if available)

4. You will receive:
   - Acknowledgment within 24 hours
   - Status updates every 3 days
   - Credit in security advisory (if desired)

---

## Supported Versions

| Version | Security Updates | Status |
| ------- | --------------- | ------ |
| 2.0.x   | ✅ Yes          | Active |
| 1.x.x   | ⚠️ Limited      | Deprecated |
| < 1.0.0 | ❌ No           | Unsupported |

---

## Security Checklist for Admins

Before going to production:
- [ ] `.env.local` file created with secure values
- [ ] Strong admin password set (8+ chars, mixed case, numbers, symbols)
- [ ] PASSWORD_SALT randomized (minimum 32 hex characters)
- [ ] HTTPS/TLS enabled
- [ ] Security headers configured
- [ ] Rate limiting tested
- [ ] Account lockout tested
- [ ] Login form tested
- [ ] Protected routes tested
- [ ] Security logs reviewed
- [ ] 2FA implementation planned
- [ ] Password reset flow planned
- [ ] Database backup automated
- [ ] Security audit completed

---

**Last Updated:** 2026-05-12 | **Status:** Active Protection 🔒