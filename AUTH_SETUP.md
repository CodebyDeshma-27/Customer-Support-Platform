# Authentication Setup Guide

## Quick Setup Steps

### 1. Configure Environment Variables

Create a `.env.local` file in the root directory with your Firebase configuration:

```
VITE_FIREBASE_API_KEY=AIzaSyCLOJncCsDPC8SZgfC5JG1U9epIcrCabrg
VITE_FIREBASE_AUTH_DOMAIN=voice-digest-vt.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=voice-digest-vt
VITE_FIREBASE_STORAGE_BUCKET=voice-digest-vt.firebasestorage.app
VITE_FIREBASE_MESSAGING_SENDER_ID=453620742933
VITE_FIREBASE_APP_ID=1:453620742933:web:e67e63eadc6e1ddf9d471c
VITE_API_BASE_URL=http://localhost:5000
```

**⚠️ IMPORTANT**: Never commit `.env.local` to version control!

### 2. Verify Login Flow

The authentication works as follows:
1. User enters email and password
2. Form validates input (email format, password length)
3. Firebase authenticates the user
4. Role is stored in localStorage
5. User is redirected based on their role

### 3. Test Credentials

Use these credentials to test:
- **Admin**: admin@company.in (password: test123456)
- **Caller**: caller@company.in (password: test123456)
- **Email Team**: email@company.in (password: test123456)
- **Customer**: customer@company.in (password: test123456)

> Note: You need to create these accounts first in Firebase Console or via the Sign Up form

### 4. Role-Based Redirection

After login, users are redirected to:
- `admin` → `/dashboard`
- `caller` → `/priority-calls`
- `email_team` → `/templates`
- `customer` → `/` (customer portal)

## Troubleshooting

### Problem: "Firebase Configuration Error"

**Solution**: 
- Check that `.env.local` exists
- Verify all environment variables are set
- Check Firebase Console for correct credentials

### Problem: "Network error" during login

**Solution**:
- Check browser console (F12) for detailed errors
- Verify Firebase project is active
- Check internet connection
- Try disabling browser extensions (especially ad blockers)

### Problem: Login successful but page doesn't redirect

**Solution**:
- Check localStorage (DevTools → Application → Local Storage)
- Verify `userRole` is saved
- Clear browser cache and try again
- Check if routes are properly configured in App.tsx

### Problem: "Too many failed attempts"

**Solution**:
- Wait 15 minutes before trying again
- This is a Firebase security feature to prevent brute force attacks

## Security Improvements Made

✅ Moved Firebase credentials to environment variables
✅ Added input validation
✅ Added better error messages
✅ Improved error handling in AuthContext
✅ Increased navigation timing (1000ms instead of 500ms)

## Next Steps

1. Create `.env.local` with your Firebase config
2. Test login with valid credentials
3. Check browser console for any errors
4. Implement backend authentication endpoints (see backend/AUTH_SETUP.md)
