# Referral System Documentation

## How the Referral System Works

### Key Concept
**The person who REFERS gets the discount code, not the person being referred.**

### Example Flow:
1. **Alice** (logged in) wants to refer her friend **Bob**
2. Alice enters Bob's email in the Customer Portal
3. System generates a discount code for **ALICE** (not Bob)
4. Alice can use this code on her next purchase
5. Alice earned this code by referring Bob

### Why This Makes Sense:
- **Rewards the referrer** for bringing in new customers
- Alice is incentivized to refer multiple friends
- Each referral gives Alice a new discount code
- Bob doesn't get anything automatically - he needs to refer someone too

---

## User Flows

### For Referrers (Getting Discount Codes)

**Step 1:** Login with Google  
**Step 2:** Go to Customer Portal  
**Step 3:** Enter friend's email (must be different from yours)  
**Step 4:** Click "Refer Friend & Get My Discount Code"  
**Step 5:** Receive YOUR discount code  
**Step 6:** Use the code on your purchase  

### For Code Redemption

**Step 1:** Login with Google  
**Step 2:** Go to Redeem Code  
**Step 3:** Enter the code you received (from referring someone)  
**Step 4:** Get discount applied  

---

## Validation Rules

### Email Validation
✅ **Allowed:**
- Any valid email format
- Different from your own email

❌ **Blocked:**
- Your own email address
- Invalid email formats
- Empty fields

### Example Errors:
```
You: alice@gmail.com
Friend: alice@gmail.com
❌ Error: "You cannot refer yourself!"

You: alice@gmail.com  
Friend: bob@gmail.com
✅ Success: Code generated for Alice
```

---

## Features

### Customer Portal
- See your email (read-only)
- Enter friend's email
- Self-referral prevention
- Generate discount codes for yourself
- View referral history
- Scratch card animation for new codes

### Redeem Portal
- Enter discount codes
- Single-use validation
- Visual discount display
- Code usage tracking

### Admin Panel
- View all codes
- See code ownership clearly
- Filter active/used codes
- Update discount rates
- Track referral statistics

---

## Technical Details

### Data Structure
```javascript
{
  code: "REFABC123",
  discount: 10,
  referrer: "alice@gmail.com",    // Person who OWNS the code
  referee: "bob@gmail.com",        // Person being referred
  codeOwner: "alice@gmail.com",    // Explicit ownership
  used: false,
  createdAt: "2025-02-06T10:30:00Z",
  usedAt: null,
  usedBy: null
}
```

### Code Generation
- Format: `REF` + 8 random characters
- Guaranteed unique (checks against all existing codes)
- Uppercase for readability
- Example: `REFX7K2M9PQ`

---

## Setup Instructions

### 1. Firebase Configuration
- Create Firebase project
- Enable Google Sign-In
- Copy config to index.html
- Add authorized domains

### 2. Deploy
- Upload all 5 HTML files
- Use Netlify, Vercel, or Firebase Hosting
- Free hosting available

### 3. Admin Access
- URL: yoursite.com/admin.html
- Password: `admin123` (change this!)

---

## File Structure

```
/
├── index.html          # Google Sign-In login
├── choice.html         # Portal selection
├── customer.html       # Generate referrals
├── redeem.html         # Redeem codes
├── admin.html          # Admin panel
└── README.md           # This file
```

---

## Common Questions

**Q: Who gets the discount code?**  
A: The person doing the referring (referrer), not the person being referred.

**Q: Can I refer myself?**  
A: No, the system blocks self-referrals.

**Q: Can I use a code multiple times?**  
A: No, each code is single-use only.

**Q: How many codes can I earn?**  
A: Unlimited - each friend you refer gives you a new code.

**Q: What if my friend doesn't sign up?**  
A: You still get the code - it's based on you entering their email, not them signing up.

---

## Security Features

- Google OAuth authentication
- Self-referral prevention
- Email validation
- Single-use codes
- Unique code generation
- Admin password protection

---

## Customization

### Change Discount Rate
Admin panel → Settings → Update discount percentage

### Change Admin Password
Edit `ADMIN_PASSWORD` in admin.html (line 283)

### Change Code Format
Edit `generateCode()` function in customer.html

---

## Support

For issues or questions:
1. Check browser console for errors
2. Verify Firebase configuration
3. Check authorized domains
4. Review this documentation
