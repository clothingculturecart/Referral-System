# Firebase OTP Setup - Step by Step

## Step 1: Create Firebase Project

1. **Go to Firebase Console**
   - Visit: https://console.firebase.google.com/
   - Click "Add project" or "Create a project"

2. **Project Setup**
   - Enter project name: `referral-system` (or any name)
   - Enable Google Analytics (optional)
   - Click "Create project"
   - Wait for project creation (30 seconds)

3. **Register Your App**
   - Click on the Web icon `</>`
   - Enter app nickname: `Referral App`
   - Check "Also set up Firebase Hosting" (optional)
   - Click "Register app"

## Step 2: Get Firebase Configuration

1. **Copy Configuration**
   After registering, you'll see a config object like this:
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

2. **Update index.html**
   - Open `index.html`
   - Find the `firebaseConfig` object (around line 165)
   - Replace with YOUR config values
   - Save the file

## Step 3: Enable Phone Authentication

1. **Go to Authentication**
   - In Firebase Console, click "Authentication" in left sidebar
   - Click "Get started"

2. **Enable Phone Sign-in**
   - Click "Sign-in method" tab
   - Find "Phone" in the list
   - Click on "Phone"
   - Toggle "Enable"
   - Click "Save"

3. **Verify Phone Numbers (Testing)**
   - In "Sign-in method" tab
   - Scroll to "Phone numbers for testing"
   - Add test numbers if needed (format: +919876543210, OTP: 123456)
   - Click "Save"

## Step 4: Configure reCAPTCHA

1. **Add Authorized Domains**
   - Still in "Authentication" > "Settings" tab
   - Scroll to "Authorized domains"
   - By default, localhost and your Firebase domain are added
   - Add your custom domain when deploying (e.g., yoursite.com)

2. **reCAPTCHA Configuration**
   - Firebase automatically uses reCAPTCHA v2
   - No additional setup needed
   - The widget appears automatically in your app

## Step 5: Test Locally

1. **Open index.html**
   ```bash
   # Simple local server
   python3 -m http.server 8000
   # Or
   npx serve
   ```

2. **Test Flow**
   - Open http://localhost:8000
   - Enter phone number with country code (+919876543210)
   - Complete reCAPTCHA verification
   - Click "Send OTP"
   - Check your phone for SMS
   - Enter OTP code
   - Should redirect to choice.html

## Step 6: Deploy to Production

### Option 1: Firebase Hosting (Recommended)

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login to Firebase
firebase login

# Initialize project
firebase init

# Select:
# - Hosting
# - Use existing project
# - Select your project
# - Public directory: . (current directory)
# - Single-page app: No
# - Set up automatic builds: No

# Deploy
firebase deploy
```

Your app will be live at: `https://your-project.firebaseapp.com`

### Option 2: Netlify

1. Go to https://app.netlify.com/drop
2. Drag all HTML files
3. Get URL: yoursite.netlify.app
4. Add this URL to Firebase Authorized Domains

### Option 3: Vercel

```bash
npm i -g vercel
vercel --prod
```

## Step 7: Add Your Domain to Firebase

After deployment:

1. Go to Firebase Console > Authentication > Settings
2. Under "Authorized domains"
3. Click "Add domain"
4. Enter your domain (e.g., yoursite.netlify.app)
5. Click "Add"

## Important Notes

### Phone Number Format
```
Correct:
+919876543210 (India)
+14155552671 (USA)
+447911123456 (UK)

Incorrect:
919876543210 (missing +)
9876543210 (missing country code)
+91 9876543210 (has space, might work but inconsistent)
```

### SMS Costs
- **Free tier**: 10,000 verifications/month
- **After free tier**: $0.01 per verification
- No credit card required for free tier
- Check usage: Firebase Console > Usage and billing

### Testing Without Real Phone
Add test numbers in Firebase Console:

1. Authentication > Sign-in method
2. Scroll to "Phone numbers for testing"
3. Add: +919999999999, OTP: 123456
4. These bypass actual SMS sending

### Security Rules
Firebase Phone Auth is secure by default:
- reCAPTCHA prevents bots
- Rate limiting built-in
- No backend code needed
- User authentication handled by Firebase

### Error Codes Reference

| Error Code | Meaning | Solution |
|------------|---------|----------|
| auth/invalid-phone-number | Wrong format | Use +[country][number] |
| auth/too-many-requests | Rate limited | Wait or use test numbers |
| auth/quota-exceeded | Free tier limit | Upgrade plan |
| auth/invalid-verification-code | Wrong OTP | Re-enter correct code |
| auth/code-expired | OTP timeout | Request new OTP |

## Troubleshooting

### "reCAPTCHA verification failed"
- Check domain is in Authorized domains
- Clear browser cache
- Try incognito mode
- Verify Firebase config is correct

### "SMS not received"
- Check phone number format
- Verify country supports Firebase SMS
- Check spam folder
- Use test numbers for development
- Some carriers block automated SMS

### "Network error"
- Check internet connection
- Verify Firebase config
- Check browser console for errors
- Try different browser

### "Quota exceeded"
- You've used 10,000 free verifications
- Upgrade to Blaze (pay-as-you-go) plan
- Or wait until next month

## Production Checklist

- [ ] Firebase project created
- [ ] Phone auth enabled
- [ ] Config copied to index.html
- [ ] Tested locally
- [ ] Deployed to hosting
- [ ] Domain added to Firebase authorized domains
- [ ] Tested on production URL
- [ ] reCAPTCHA working
- [ ] SMS being received
- [ ] Login flow complete

## Cost Estimates

**Free tier (no credit card):**
- 10,000 phone verifications/month
- Enough for small apps

**If you exceed free tier:**
- $0.01 per verification
- 1,000 users/month = $10
- 5,000 users/month = $50
- 10,000 users/month = $100

## Support Resources

- Firebase Docs: https://firebase.google.com/docs/auth/web/phone-auth
- Firebase Console: https://console.firebase.google.com/
- Firebase Status: https://status.firebase.google.com/
- Stack Overflow: Tag [firebase-authentication]

## Quick Commands

```bash
# Serve locally
python3 -m http.server 8000

# Deploy to Firebase
firebase deploy --only hosting

# Check Firebase login
firebase login:list

# View deployment history
firebase hosting:channel:list
```

## Next Steps

After OTP is working:
1. Test the entire referral flow
2. Add analytics tracking
3. Set up error logging
4. Configure email notifications (optional)
5. Add customer support contact info
6. Create terms of service
7. Monitor usage in Firebase Console
