# MBA MobileWala - Flutter App Setup & Configuration

## App Branding Configuration

This guide shows how to configure the Bagisto Flutter mobile app with the name **"MBA MobileWala"** (mbamobilewala).

---

## Step 1: Clone Bagisto Flutter App

```bash
git clone https://github.com/bagisto/opensource-ecommerce-mobile-app.git mbamobilewala-app
cd mbamobilewala-app
flutter pub get
```

---

## Step 2: Configure App Name for Android

### Update AndroidManifest.xml

**File:** `android/app/src/main/AndroidManifest.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.mbamobilewala.app">

    <application
        android:label="MBA MobileWala"
        android:icon="@mipmap/ic_launcher"
        android:roundIcon="@mipmap/ic_launcher_round">
        <!-- Rest of configuration -->
    </application>
</manifest>
```

### Update build.gradle

**File:** `android/app/build.gradle`

```gradle
android {
    compileSdkVersion 33
    ndkVersion "25.1.8937393"

    defaultConfig {
        applicationId "com.mbamobilewala.app"
        minSdkVersion 21
        targetSdkVersion 33
        versionCode 1
        versionName "1.0.0"
    }
}
```

### Update strings.xml

**File:** `android/app/src/main/res/values/strings.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">MBA MobileWala</string>
</resources>
```

---

## Step 3: Configure App Name for iOS

### Update Info.plist

**File:** `ios/Runner/Info.plist`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>CFBundleName</key>
    <string>MBA MobileWala</string>
    <key>CFBundleDisplayName</key>
    <string>MBA MobileWala</string>
    <key>CFBundleIdentifier</key>
    <string>com.mbamobilewala.app</string>
    <!-- Rest of configuration -->
</dict>
</plist>
```

### Update pubspec.yaml

**File:** `pubspec.yaml`

```yaml
name: mbamobilewala
description: "MBA MobileWala - Mobile marketplace for buying and selling phones"
publish_to: 'none'

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  # ... rest of dependencies
```

---

## Step 4: Configure API Endpoint

### Update server_configuration.dart

**File:** `lib/utils/server_configuration.dart`

```dart
class ServerConfiguration {
  // Change this to your Bagisto backend URL
  static const String baseDomain = 'https://api.mbamobilewala.me/graphql';
  
  // App branding
  static const String appName = 'MBA MobileWala';
  static const String appVersion = '1.0.0';
  
  // App features
  static const bool enableSellers = true;  // Multi-vendor marketplace
  static const bool enableReviews = true;  // Product reviews
  static const bool enableWishlist = true; // Wishlist feature
  static const bool enablePayments = true; // Payment integration
}
```

---

## Step 5: App Splash Screen Setup

### Create Assets

```bash
mkdir -p assets/images
mkdir -p assets/lottie
```

**Place your branded assets:**
- `assets/images/splash.png` - Splash screen image
- `assets/images/logo.png` - App logo
- `assets/images/splash_bg.png` - Background
- `assets/lottie/splash_screen.json` - Loading animation (optional)

### Update splash_screen.dart

**File:** `lib/utils/splash_screen.dart`

```dart
class SplashScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Image.asset(
              'assets/images/logo.png',
              width: 200,
              height: 200,
            ),
            SizedBox(height: 20),
            Text(
              'MBA MobileWala',
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),
            SizedBox(height: 10),
            Text(
              'Mobile Marketplace',
              style: TextStyle(
                fontSize: 14,
                color: Colors.grey,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## Step 6: Theme Customization

### Update mobikul_theme.dart

**File:** `lib/utils/mobikul_theme.dart`

```dart
class MobikulTheme {
  // Brand Colors
  static const Color primaryColor = Color(0xFF0066CC);   // Blue
  static const Color accentColor = Color(0xFFFF6B00);    // Orange
  static const Color backgroundColor = Color(0xFFF5F5F5);
  
  // App Name
  static const String appName = 'MBA MobileWala';
  
  // Typography
  static const String appFont = 'Poppins';
  
  static TextStyle headingStyle = TextStyle(
    fontFamily: appFont,
    fontSize: 18,
    fontWeight: FontWeight.bold,
    color: primaryColor,
  );
  
  static TextStyle bodyStyle = TextStyle(
    fontFamily: appFont,
    fontSize: 14,
    color: Colors.black87,
  );
}
```

---

## Step 7: Language Configuration

### Update Language Files

**File:** `assets/language/en.json`

```json
{
  "app_name": "MBA MobileWala",
  "app_tagline": "Buy & Sell Mobile Phones",
  "welcome_message": "Welcome to MBA MobileWala",
  "mobile_marketplace": "Mobile Marketplace",
  "buy_phones": "Buy Mobile Phones",
  "sell_phones": "Sell Mobile Phones",
  "for_buyers": "For Buyers",
  "for_sellers": "For Sellers"
}
```

---

## Step 8: Build APK (Release)

### Build Release APK

```bash
# Get dependencies
flutter pub get
flutter pub run build_runner build --delete-conflicting-outputs

# Build APK
flutter build apk --release

# Output location:
# build/app/outputs/apk/release/app-release.apk
```

### Build App Bundle (for Play Store)

```bash
flutter build appbundle --release

# Output location:
# build/app/outputs/bundle/release/app-release.aab
```

---

## Step 9: Firebase Configuration (Push Notifications)

### Android Firebase Setup

**File:** `android/app/google-services.json`

```json
{
  "type": "service_account",
  "project_id": "mbamobilewala",
  "private_key_id": "your-key-id",
  "private_key": "your-private-key",
  "client_email": "firebase-adminsdk@mbamobilewala.iam.gserviceaccount.com",
  "client_id": "your-client-id",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token"
}
```

### iOS Firebase Setup

**File:** `ios/Runner/GoogleService-Info.plist`

Download from Firebase Console and place in `ios/Runner/` directory.

---

## Step 10: Sign APK with Keystore

### Create Keystore

```bash
keytool -genkey -v -keystore mbamobilewala-key.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias mbamobilewala
```

### Create key.properties

**File:** `android/key.properties`

```properties
storePassword=your_password
keyPassword=your_password
keyAlias=mbamobilewala
storeFile=/path/to/mbamobilewala-key.jks
```

### Update build.gradle

**File:** `android/app/build.gradle`

```gradle
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}

android {
    signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
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

---

## Step 11: Deploy to Google Play Store

### Create Google Play Developer Account

1. Go to: https://play.google.com/console
2. Pay $25 registration fee (one-time)
3. Create new app
4. Fill app details:
   - App name: **MBA MobileWala**
   - Short description: "Buy and sell mobile phones"
   - Full description: "A complete mobile marketplace platform"
   - Category: Shopping

### Upload APK/AAB

1. Go to **Release** → **Production**
2. Upload `app-release.aab` (recommended) or `app-release.apk`
3. Fill required information:
   - Screenshots (minimum 5)
   - Feature graphic (1024x500px)
   - Privacy policy URL
   - Contact email

### App Review Process

- Google Play will review your app
- Typical review time: 24-48 hours
- Once approved, app becomes live

---

## Step 12: Set Backend API URL

### For Production

```bash
# Update server_configuration.dart before building
static const String baseDomain = 'https://api.mbamobilewala.me/graphql';
```

### For Testing

```bash
# During development, use local server
static const String baseDomain = 'http://192.168.1.100:8000/graphql';
```

---

## App Store Connect (iOS)

For iOS deployment (requires macOS and Apple Developer account):

### Build for iOS

```bash
flutter build ios --release
```

### Upload with Xcode

1. Open `ios/Runner.xcworkspace` in Xcode
2. Select Release configuration
3. Go to **Product** → **Archive**
4. Upload to App Store

---

## Troubleshooting

### Build Issues

```bash
# Clean build
flutter clean

# Get dependencies again
flutter pub get

# Run build runner
flutter pub run build_runner build --delete-conflicting-outputs
```

### App Icon Not Showing

```bash
# Use flutter_launcher_icons package
flutter pub add flutter_launcher_icons
```

**File:** `pubspec.yaml`

```yaml
flutter_icons:
  android: "launcher_icon"
  ios: true
  image_path: "assets/images/logo.png"
  adaptive_icon_background: "#0066CC"
  adaptive_icon_foreground: "assets/images/logo.png"
```

```bash
flutter pub run flutter_launcher_icons:main
```

### API Connection Issues

```dart
// Add CORS headers in Bagisto .env
API_CORS_ENABLED=true
API_CORS_ALLOWED_ORIGINS=*
```

---

## Next Steps

1. ✅ Clone Bagisto Flutter app
2. ✅ Rename to mbamobilewala
3. ✅ Update package name to com.mbamobilewala.app
4. ✅ Configure API endpoint
5. ✅ Build APK/AAB
6. ✅ Create Google Play Developer account
7. ✅ Upload and submit for review
8. ✅ Monitor app performance

---

## Resources

- Flutter Docs: https://flutter.dev/docs
- Google Play Console: https://play.google.com/console
- Bagisto Docs: https://bagisto.com/en/documentation/
- Firebase Docs: https://firebase.google.com/docs

---

**Made with ❤️ for MBA MobileWala**
