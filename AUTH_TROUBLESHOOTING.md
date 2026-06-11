# Authentication Troubleshooting Guide

## Step 1: Check Console Errors

1. Open Developer Tools: **F12** or **Right-click → Inspect**
2. Go to **Console** tab
3. Look for:
   - Red error messages
   - Firebase initialization messages
   - Login attempt logs

**Expected console output on successful login:**
```
Role stored before login: admin
Role verification after login: admin
User state updated: {id: "...", email: "...", role: "admin", name: "..."}
```

## Step 2: Verify Environment Setup

1. Check if `.env.local` exists in root folder
2. Verify it contains all required variables:
```bash
# On Windows PowerShell
Test-Path .env.local
```

3. Restart dev server after creating/modifying `.env.local`:
```bash
npm run dev
```

## Step 3: Check Firebase Configuration

1. Open browser DevTools → Network tab
2. Look for Firebase API calls
3. Check for CORS errors

**Expected requests:**
- POST to `identitytoolkit.googleapis.com` (authentication)
- Success response: `200 OK`

## Step 4: Verify localStorage

1. Open DevTools → Application → Local Storage
2. Check for these keys:
   - `user` - contains user object
   - `userRole` - contains role string

**If missing:** Authentication failed or not completed

## Step 5: Test Login Steps

### 5a. Test Form Validation
1. Try submitting with empty fields
2. Should see error: "Email is required" or "Password is required"
3. ✅ If working: Validation is OK

### 5b. Test Invalid Email
1. Enter: `notanemail`
2. Try to submit
3. Should see: "Please enter a valid email address"
4. ✅ If working: Email validation is OK

### 5c. Test Short Password  
1. Enter email: `test@test.com`
2. Enter password: `12345` (5 chars)
3. Try to submit
4. Should see: "Password must be at least 6 characters"
5. ✅ If working: Password validation is OK

### 5d. Test Invalid Credentials
1. Enter: `admin@company.in` / `wrongpassword`
2. Should see: "Incorrect password. Please try again."
3. ✅ If working: Firebase auth is OK

### 5e. Test Valid Login
1. Enter: `admin@company.in` / `test123456`
2. Should see: "Successfully signed in!"
3. Should redirect to `/dashboard`
4. ✅ If working: Full auth flow is OK

## Step 6: Check Network Requests

1. Open DevTools → Network tab
2. Filter for: `identitytoolkit` or `firebaseapp`
3. Click on failed request
4. Check response for error details

**Common errors:**
```json
{
  "error": {
    "code": 400,
    "message": "INVALID_PASSWORD",
    "errors": [{"domain": "global", "reason": "invalid"}]
  }
}
```

## Debugging Checklist

| Issue | Solution |
|-------|----------|
| Firebase config not loaded | Check `.env.local` exists and has all variables |
| "Network error" | Check internet connection and Firebase status |
| Can't submit form | Clear form and check browser cache |
| Redirects to login after login | Check localStorage `userRole` is set |
| Role shows as undefined | Check role is passed correctly to login |
| Login works but pages are blank | Check route configuration in App.tsx |

## Enable Debug Logging

Add this to your code for more details:

```typescript
// In AuthContext.tsx
useEffect(() => {
  console.log('Auth state changed:', {
    user,
    isLoading,
    role: localStorage.getItem('userRole')
  });
}, [user, isLoading]);
```

## Contact Firebase Support

If you still have issues:
1. Visit [Firebase Console](https://console.firebase.google.com)
2. Check Authentication → Sign-in method
3. Ensure Email/Password is enabled
4. Check quotas and billing

## Quick Reset

If everything is stuck:
1. Clear browser cache: **Ctrl+Shift+Del**
2. Remove `user` and `userRole` from localStorage
3. Reload page: **Ctrl+R**
4. Try logging in again
