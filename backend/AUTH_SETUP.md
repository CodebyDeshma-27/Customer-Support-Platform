# Backend Authentication Setup

## Current Status

The backend currently has:
- ✅ Flask server with CORS enabled
- ✅ Google API integration starting
- ❌ Missing authentication endpoints
- ❌ Missing user management routes

## Recommended Authentication Endpoints

Add these endpoints to your Flask backend:

```python
# GET /api/auth/verify
# Verify Firebase token and return user info
@app.route('/api/auth/verify', methods=['POST'])
def verify_token():
    """Verify Firebase ID token"""
    try:
        token = request.headers.get('Authorization', '').split('Bearer ')[-1]
        if not token:
            return jsonify({'error': 'No token provided'}), 401
        
        # Verify with Firebase Admin SDK
        decoded = firebase_admin.auth.verify_id_token(token)
        return jsonify({'valid': True, 'user_id': decoded['uid']}), 200
    except Exception as e:
        return jsonify({'error': str(e)}), 401

# POST /api/auth/logout
# Handle logout (optional, mainly frontend-side)
@app.route('/api/auth/logout', methods=['POST'])
def logout():
    """Handle user logout"""
    # Perform any backend cleanup if needed
    return jsonify({'message': 'Logged out successfully'}), 200

# GET /api/user/profile
# Get current user's profile
@app.route('/api/user/profile', methods=['GET'])
def get_user_profile():
    """Get user profile"""
    token = request.headers.get('Authorization', '').split('Bearer ')[-1]
    if not token:
        return jsonify({'error': 'Unauthorized'}), 401
    
    try:
        decoded = firebase_admin.auth.verify_id_token(token)
        user_id = decoded['uid']
        # Fetch user profile from database
        return jsonify({'user_id': user_id, 'email': decoded.get('email')}), 200
    except Exception as e:
        return jsonify({'error': str(e)}), 401
```

## Setup Firebase Admin SDK

1. Install Firebase Admin SDK:
```bash
pip install firebase-admin
```

2. Download service account key from Firebase Console:
   - Go to Project Settings → Service Accounts
   - Click "Generate New Private Key"
   - Save it as `backend/firebase-key.json`

3. Initialize in your Flask app:
```python
import firebase_admin
from firebase_admin import credentials, auth

# Initialize Firebase Admin
cred = credentials.Certificate('firebase-key.json')
firebase_admin.initialize_app(cred)
```

## Environment Variables

Add to your backend `.env`:
```
FLASK_ENV=development
GOOGLE_API_KEY=your_key_here
FIREBASE_PROJECT_ID=voice-digest-vt
```

## CORS Configuration

Your current CORS setup is:
```python
CORS(app)  # Allows all origins
```

For production, restrict it:
```python
from flask_cors import CORS

CORS(app, resources={
    r"/api/*": {
        "origins": ["http://localhost:5173", "https://yourdomain.com"],
        "methods": ["GET", "POST", "PUT", "DELETE"],
        "allow_headers": ["Content-Type", "Authorization"]
    }
})
```

## Testing

Test endpoints with curl:
```bash
# Verify token
curl -X POST http://localhost:5000/api/auth/verify \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json"

# Get user profile  
curl -X GET http://localhost:5000/api/user/profile \
  -H "Authorization: Bearer YOUR_TOKEN"
```

## Security Checklist

- [ ] Service account key is in `.gitignore`
- [ ] CORS is restricted to known origins
- [ ] API keys are in environment variables
- [ ] All endpoints validate tokens
- [ ] Rate limiting is implemented
- [ ] HTTPS is enforced in production
