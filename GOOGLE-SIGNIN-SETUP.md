# Google Sign-In Setup Guide

## Quick Overview
Set up Google authentication in 5 minutes - no backend needed, completely free.

---

## Step 1: Create Firebase Project

### 1. Go to Firebase Console
- Visit: https://console.firebase.google.com/
- Click **"Add project"**

### 2. Project Setup
- **Project name**: `referral-system` (or any name)
- **Google Analytics**: Optional (can skip)
- Click **"Create project"**
- Wait 30 seconds for creation

### 3. Register Web App
- Click the **Web icon** `</>`
- **App nickname**: `Referral App`
- **Don't** check Firebase Hosting (unless you want it)
- Click **"Register app"**

---

## Step 2: Get Firebase Configuration

### Copy Your Config
After registering, you'll see this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789012",
  appId: "1:123456789012:web:xxxxxxxxxxxxx"
};
```

### Update index.html
1. Open `index.html`
2. Find line ~165: `const firebaseConfig = {`
3. Replace with YOUR values
4. Save file

---

## Step 3: Enable Google Sign-In

### 1. Go to Authentication
- In Firebase Console left sidebar
- Click **"Authentication"**
- Click **"Get started"**

### 2. Enable Google Provider
- Click **"Sign-in method"** tab
- Find **"Google"** in the provider list
- Click on **"Google"**
- Toggle **"Enable"**
- **Project support email**: Select your email
- Click **"Save"**

**That's it! Google Sign-In is now enabled.**

---

## Step 4: Test Locally

### Run Local Server
```bash
# Option 1: Python
python3 -m http.server 8000

# Option 2: Node.js
npx serve

# Option 3: PHP
php -S localhost:8000
```

### Test the Flow
1. Open `http://localhost:8000`
2. Click **"Continue with Google"**
3. Select your Google account
4. Should redirect to `choice.html`
5. See your name and profile picture

---

## Step 5: Deploy to Production

### Option 1: Netlify (Easiest)
```bash
1. Go to https://app.netlify.com/drop
2. Drag all 5 HTML files into the drop zone
3. Get URL: https://yoursite.netlify.app
4. Done!
```

### Option 2: Firebase Hosting
```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login
firebase login

# Initialize
firebase init
# Select: Hosting
# Public directory: . (current)
# Single-page app: No

# Deploy
firebase deploy
```

### Option 3: Vercel
```bash
npm i -g vercel
vercel --prod
```

### Option 4: GitHub Pages
```bash
1. Create new GitHub repository
2. Upload all HTML files
3. Settings > Pages
4. Source: main branch
5. Access at: username.github.io/repo-name
```

---

## Step 6: Add Domain to Firebase

After deploying, add your domain to Firebase:

1. Firebase Console > **Authentication** > **Settings**
2. Scroll to **"Authorized domains"**
3. Click **"Add domain"**
4. Enter: `yoursite.netlify.app` (or your domain)
5. Click **"Add"**

**Common domains to add:**
- `yoursite.netlify.app`
- `yoursite.vercel.app`
- `yourdomain.com`
- `localhost` (already added by default)

---

## What Users See

### Login Flow
1. Click "Continue with Google"
2. Google popup appears
3. Select account
4. Redirected to choice page
5. See profile picture and name

### User Info Stored
```javascript
sessionStorage.setItem('userId', user.uid);
sessionStorage.setItem('userEmail', user.email);
sessionStorage.setItem('userName', user.displayName);
sessionStorage.setItem('userPhoto', user.photoURL);
```

---

## Features

### ✅ What Works
- One-click Google login
- No password needed
- Profile picture shown
- Email address captured
- Secure Firebase authentication
- Works on all devices
- Free (unlimited users)

### ❌ What's Not Needed
- No backend server
- No database setup
- No SMS costs
- No phone verification
- No email verification
- No password management

---

## Troubleshooting

### "Popup blocked"
**Solution**: Allow popups for your site
- Chrome: Click popup icon in address bar
- Or try different browser

### "Unauthorized domain"
**Solution**: Add domain to Firebase
- Go to Authentication > Settings
- Add your deployment domain
- Include both www and non-www if needed

### "Network error"
**Solution**: 
- Check internet connection
- Verify Firebase config is correct
- Clear browser cache
- Try incognito mode

### "Configuration not found"
**Solution**:
- Double-check you copied entire config
- Ensure no typos in apiKey
- Make sure quotes are correct

---

## Security & Privacy

### Is it secure?
✅ Yes! Firebase handles all security:
- OAuth 2.0 protocol
- Encrypted connections
- No passwords stored
- Google's security standards

### What data is collected?
- Email address
- Display name
- Profile picture URL
- Unique user ID

### Can users sign out?
Yes! Click "Logout" button - clears all session data.

---

## Cost

### Completely FREE
- ✅ Unlimited users
- ✅ Unlimited sign-ins
- ✅ No credit card required
- ✅ No hidden costs
- ✅ No expiration

### If you scale big
Firebase's free tier is extremely generous:
- 50,000 authentications/month free
- After that: Still mostly free
- Only pay if you have millions of users

---

## Error Codes

| Error | Meaning | Fix |
|-------|---------|-----|
| popup-closed-by-user | User closed popup | Normal - user changed mind |
| popup-blocked | Browser blocked popup | Allow popups |
| unauthorized-domain | Domain not authorized | Add to Firebase console |
| network-request-failed | No internet | Check connection |

---

## Testing Tips

### Test Users
No special setup needed - any Google account works!
- Your personal Gmail
- Work accounts (@company.com)
- School accounts (@university.edu)

### Multiple Accounts
Want to test with different users?
- Open incognito window
- Sign in with different Google account
- Each has separate session

---

## Admin Panel Access

The admin panel (admin.html) uses password auth:
- **URL**: yoursite.com/admin.html
- **Password**: `admin123`
- **Change password**: Edit line in admin.html

Recommendation: Change default password!

---

## Production Checklist

- [ ] Firebase project created
- [ ] Google sign-in enabled
- [ ] Config copied to index.html
- [ ] Tested locally (works on localhost)
- [ ] Deployed to hosting
- [ ] Domain added to Firebase authorized domains
- [ ] Tested on production URL
- [ ] Login flow works end-to-end
- [ ] User info displays correctly
- [ ] Logout works
- [ ] Changed admin password

---

## Quick Commands

```bash
# Test locally
python3 -m http.server 8000

# Deploy to Firebase
firebase deploy --only hosting

# Deploy to Netlify (via CLI)
npm install -g netlify-cli
netlify deploy --prod

# Check what's in sessionStorage (browser console)
console.log(sessionStorage);
```

---

## Comparison: Google Sign-In vs Phone OTP

| Feature | Google Sign-In | Phone OTP |
|---------|---------------|-----------|
| Setup time | 5 minutes | 20 minutes |
| User friction | 1 click | Type phone + OTP |
| Cost | Free | $0.01 per SMS |
| Backend needed | No | Yes (for SMS) |
| Maintenance | None | SMS provider account |
| User trust | High (Google) | Medium |
| Spam/bots | Low risk | Higher risk |

**Recommendation**: Google Sign-In is simpler, faster, and free.

---

## Support Resources

- **Firebase Docs**: https://firebase.google.com/docs/auth
- **Firebase Console**: https://console.firebase.google.com/
- **Firebase Status**: https://status.firebase.google.com/
- **Google Sign-In Guide**: https://developers.google.com/identity

---

## Next Steps

After setup is working:
1. ✅ Test referral code generation
2. ✅ Test code redemption
3. ✅ Check admin panel
4. ✅ Customize discount rates
5. ✅ Share with first users
6. Monitor usage in Firebase Console

---

## Common Questions

**Q: Do users need a Google account?**  
A: Yes, but 90%+ of internet users have one.

**Q: Can I add other sign-in methods later?**  
A: Yes! Firebase supports email, Facebook, Twitter, etc.

**Q: Will sign-in work on mobile?**  
A: Yes! Works on all devices and browsers.

**Q: Can I customize the Google button?**  
A: Yes! Edit the HTML/CSS in index.html.

**Q: Is user data stored in Firebase?**  
A: Only authentication. Referral codes are in localStorage.

**Q: What if Google is down?**  
A: Rare, but users can't sign in. Check status.firebase.google.com

---

## Success! 🎉

Your referral system is now live with Google Sign-In!

Users can:
- ✅ Sign in with 1 click
- ✅ Generate referral codes
- ✅ Share codes with friends
- ✅ Redeem discounts
- ✅ Track referral history

Admins can:
- ✅ View all codes
- ✅ See usage statistics
- ✅ Adjust discount rates
- ✅ Filter active/used codes
