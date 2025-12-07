# 📱 MBA MobileWala - Flutter Mobile App Deployment Guide

## Android & iOS App Store Deployment

**Backend API is LIVE at**: https://mbamobilewala.onrender.com

---

## PART 1: BUILD FLUTTER APP FOR ANDROID

### Step 1: Generate Keystore (ONE-TIME ONLY)

```bash
# This creates a signing key for your Android app
keytool -genkey -v -keystore mbamobilewala.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias mbamobilewala
```

**When prompted, enter:**
- Password: (create a strong password, save it!)
- Full name: Your Name
- Organization: MBA MobileWala
- City: Pune
- State: Maharashtra
- Country: IN

**Save this keystore file securely! You'll need it forever.**

### Step 2: Create Key Properties File

**File**: `android/key.properties`

```properties
storePassword=YOUR_KEYSTORE_PASSWORD
keyPassword=YOUR_KEY_PASSWORD
keyAlias=mbamobilewala
storeFile=/full/path/to/mbamobilewala.jks
```

### Step 3: Update Gradle Configuration

**File**: `android/app/build.gradle`

```gradle
android {
    compileSdkVersion 33
    
    defaultConfig {
        applicationId "com.mbamobilewala.app"
        minSdkVersion 21
        targetSdkVersion 33
        versionCode 1
        versionName "1.0.0"
    }
    
    signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile file(keystoreProperties['storeFile'])
            storePassword keystoreProperties['storePassword']
        }
    }
    
    buildTypes {
        release {
            signingConfig signingConfigs.release
        }
    }
}
```

### Step 4: Update API Endpoint

**File**: `lib/utils/server_configuration.dart`

```dart
class ServerConfiguration {
  static const String baseDomain = 'https://mbamobilewala.onrender.com/graphql';
  // Rest of configuration
}
```

### Step 5: Build Release APK

```bash
# Clean before building
flutter clean

# Get dependencies
flutter pub get

# Build release APK
flutter build apk --release

# Output: build/app/outputs/apk/release/app-release.apk
```

### Step 6: Build App Bundle (RECOMMENDED for Play Store)

```bash
flutter build appbundle --release

# Output: build/app/outputs/bundle/release/app-release.aab
```

---

## PART 2: UPLOAD TO GOOGLE PLAY STORE

### Step 1: Create Developer Account

1. Go to: https://play.google.com/console
2. Pay $25 registration fee (ONE-TIME)
3. Complete business verification
4. Accept developer agreement

### Step 2: Create App Listing

1. Click **Create app**
2. **App name**: MBA MobileWala
3. **Default language**: English
4. **App type**: App
5. **Category**: Shopping
6. **Content rating**: Declare (fill questionnaire)

### Step 3: Prepare Store Assets

**Required:**
- **App icon**: 512x512 PNG
- **Feature graphic**: 1024x500 PNG
- **Screenshots**: Minimum 2, max 8 (1080x1920 or 1440x2560)
- **Privacy policy**: Required (create at: https://www.privacypolicies.com/)
- **Contact email**: Your email

**Recommended:**
- **Short description** (80 chars): "Buy and sell mobile phones easily"
- **Full description**: Describe features, benefits, marketplace concept
- **Video**: Optional promo video

### Step 4: Upload APK/AAB

1. Go to **Release** → **Production**
2. Click **Create release**
3. Upload `.aab` file
4. Add release notes: "Initial release"
5. Review all information
6. Click **Review release**
7. Click **Start rollout to production**

### Step 5: Google Play Review

- Google reviews your app: 24-48 hours typically
- Check **Testing** section for feedback
- Fix any issues if rejected
- Resubmit for review
- Once approved, app becomes LIVE!

---

## PART 3: BUILD FOR iOS (macOS ONLY)

**Requirements:**
- macOS computer
- Xcode 15+
- Apple Developer account ($99/year)

### Step 1: Update iOS Configuration

**File**: `ios/Runner/Info.plist`

```xml
<dict>
    <key>CFBundleDisplayName</key>
    <string>MBA MobileWala</string>
    <key>CFBundleIdentifier</key>
    <string>com.mbamobilewala.app</string>
    <key>CFBundleVersion</key>
    <string>1</string>
    <key>CFBundleShortVersionString</key>
    <string>1.0.0</string>
</dict>
```

### Step 2: Build iOS App

```bash
flutter build ios --release
```

### Step 3: Archive in Xcode

1. Open: `ios/Runner.xcworkspace`
2. Select: **Product** → **Archive**
3. Wait for archive to complete
4. Click **Distribute App**
5. Choose **Apple ID**
6. Select **App Store Connect**
7. Follow prompts to upload

### Step 4: Upload to App Store Connect

1. Go to: https://appstoreconnect.apple.com
2. Create app listing
3. Upload build
4. Add screenshots and description
5. Submit for review

---

## STEP-BY-STEP CHECKLIST

### Android/Google Play Store

- [ ] Generate keystore file (`keytool`)
- [ ] Create `key.properties` file
- [ ] Update `build.gradle` with signing config
- [ ] Update API endpoint in `server_configuration.dart`
- [ ] Run `flutter build appbundle --release`
- [ ] Create Google Play Developer account ($25)
- [ ] Create app listing on Play Console
- [ ] Prepare store assets (icon, screenshots, etc.)
- [ ] Create privacy policy
- [ ] Upload `.aab` file
- [ ] Submit for review
- [ ] Wait for approval (24-48 hours)
- [ ] App goes LIVE on Google Play Store!

### iOS/App Store (macOS only)

- [ ] Get Apple Developer account ($99/year)
- [ ] Update iOS configuration files
- [ ] Run `flutter build ios --release`
- [ ] Create app listing on App Store Connect
- [ ] Prepare iOS store assets
- [ ] Archive in Xcode
- [ ] Upload to App Store
- [ ] Submit for review
- [ ] Wait for approval (typically 24 hours)
- [ ] App goes LIVE on Apple App Store!

---

## PRODUCTION APP URLS

**Once approved:**

### Google Play Store
```
https://play.google.com/store/apps/details?id=com.mbamobilewala.app
```

### Apple App Store
```
https://apps.apple.com/in/app/mba-mobilewala/id1234567890
```

---

## TESTING BEFORE UPLOAD

### Test on Real Device

```bash
# Connect Android device via USB
flutter run --release

# Or iOS
flutter run --release -t ios
```

### Test API Connection

1. Open app
2. Try to browse products
3. Verify data loads from: https://mbamobilewala.onrender.com
4. Test login/registration
5. Test add to cart

---

## TROUBLESHOOTING

### APK Build Errors

```bash
# Clear and rebuild
flutter clean
flutter pub get
flutter build apk --release
```

### Keystore Issues

```bash
# List keystore contents
keytool -list -v -keystore mbamobilewala.jks

# If password forgotten, regenerate
keytool -genkey -v -keystore new.jks -keyalg RSA -keysize 2048 -validity 10000 -alias mbamobilewala
```

### API Connection Failed

1. Verify backend is running: https://mbamobilewala.onrender.com
2. Check `server_configuration.dart` has correct URL
3. Ensure CORS is enabled in backend
4. Test with: `curl https://mbamobilewala.onrender.com/graphql`

---

## COSTS

| Platform | Cost | Duration |
|----------|------|----------|
| Google Play | $25 | One-time |
| Apple App Store | $99 | Per year |
| DigitalOcean (backend) | $0 | 12 months (free credit) |
| **TOTAL** | **$124** | **1 year** |

---

## YOUR BACKEND IS READY!

✅ **API URL**: https://mbamobilewala.onrender.com
✅ **Status**: LIVE and RUNNING
✅ **Cost**: $0 (using GitHub Student Pack)
✅ **Database**: PostgreSQL included
✅ **Auto-Deploy**: From GitHub main branch

**Now build your Flutter app and deploy to app stores!**

---

**For detailed Flutter setup, see**: FLUTTER_APP_SETUP.md
**For complete guide, see**: README.md
