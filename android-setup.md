# Android App Setup Guide

## What We've Done

1. ✅ Installed Capacitor core, CLI, and Android platform
2. ✅ Initialized Capacitor with app details:
   - **App Name**: Loud Radio
   - **App ID**: com.loudradio.sakata
   - **Web Directory**: dist
3. ✅ Built the web app for production
4. ✅ Added Android platform
5. ✅ Copied web assets to native project

## Next Steps

### 1. Open Android Studio
Run this command to open the project in Android Studio:
```bash
npx cap open android
```

### 2. Configure Android Studio
When Android Studio opens:
- Wait for Gradle sync to complete
- Make sure you have Android SDK installed
- Set up an Android Virtual Device (AVD) or connect a physical device

### 3. Test the App
- Click the "Run" button (green play icon) in Android Studio
- Select your device/emulator
- The app should launch with your Loud Radio interface

### 4. Customize App Settings

#### App Icon
- Place your app icons in `android/app/src/main/res/mipmap-*` folders
- Use different sizes: 48x48, 72x72, 96x96, 144x144, 192x192

#### Splash Screen
- Customize in `android/app/src/main/res/drawable/splash.xml`
- Add splash images to `android/app/src/main/res/drawable-*` folders

#### App Permissions
Edit `android/app/src/main/AndroidManifest.xml` to add permissions:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
```

### 5. Build Release APK

#### Generate Keystore (First Time Only)
```bash
keytool -genkey -v -keystore my-release-key.keystore -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias
```

#### In Android Studio:
1. Go to **Build** → **Generate Signed Bundle/APK**
2. Choose **APK**
3. Select your keystore file
4. Enter keystore and key passwords
5. Choose **release** build variant
6. Click **Finish**

### 6. Update Web Code
When you make changes to your web app:
```bash
npm run build
npx cap copy
```
Then rebuild in Android Studio.

### 7. Useful Capacitor Commands
```bash
# Sync changes
npx cap sync

# Open Android Studio
npx cap open android

# Run on device
npx cap run android

# Check doctor for issues
npx cap doctor
```

## Troubleshooting

### Common Issues:
1. **Gradle sync fails**: Update Android Studio and SDK
2. **App crashes**: Check Android Studio logcat for errors
3. **White screen**: Ensure web build is successful and copied
4. **Network issues**: Check CORS settings and HTTPS requirements

### Audio Streaming Notes:
- Test audio streaming on real device (emulator may have audio issues)
- Ensure your stream URL supports HTTPS
- Consider adding audio focus handling for better user experience

## Production Checklist
- [ ] Test on multiple Android versions
- [ ] Test audio streaming functionality
- [ ] Verify PWA features work in native app
- [ ] Test offline capabilities
- [ ] Optimize app size and performance
- [ ] Set up proper app signing
- [ ] Test installation and updates