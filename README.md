# 💬 Chattr — Secure Personal Chat App

A full Android chat application built with **Kotlin + Jetpack Compose + Firebase**, featuring **fingerprint biometric authentication**.

---

## ✨ Features

- 🔐 **Fingerprint / Biometric Login** — Uses Android BiometricPrompt API (real hardware fingerprint sensor)
- 👤 **Username-based accounts** — No phone number or email needed
- 💬 **Real-time messaging** — Powered by Firebase Realtime Database
- ✓✓ **Read receipts** — Single tick (sent) and double tick (read)
- 🌙 **Dark luxury UI** — Custom dark theme with amber & teal accents
- 🔒 **Secure auth** — Biometric-derived keys, Firebase Auth backend
- 📱 **Edge-to-edge** — Supports Android 12+ gesture navigation

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Kotlin |
| UI | Jetpack Compose + Material 3 |
| Auth | Firebase Authentication + BiometricPrompt |
| Database | Firebase Realtime Database |
| Architecture | MVVM (ViewModel + StateFlow) |
| Navigation | Animated content switching |
| Min SDK | 26 (Android 8.0) |

---

## 🚀 Setup Instructions

### Step 1 — Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click **"Add project"** → name it `Chattr`
3. Disable Google Analytics (optional) → **Create project**

### Step 2 — Add Android App to Firebase

1. In Firebase Console → **Project Settings** → **Add app** → Android icon
2. Enter package name: `com.chattr.app`
3. Enter app nickname: `Chattr`
4. Click **Register app**
5. **Download `google-services.json`**
6. Place it at: `Chattr/app/google-services.json`

### Step 3 — Enable Firebase Authentication

1. Firebase Console → **Authentication** → **Get started**
2. **Sign-in method** tab → Enable **Email/Password**
3. Click **Save**

### Step 4 — Enable Firebase Realtime Database

1. Firebase Console → **Realtime Database** → **Create database**
2. Choose a region → Start in **test mode** (we'll add rules next)
3. Click **Enable**

### Step 5 — Set Database Security Rules

1. In Realtime Database → **Rules** tab
2. Replace the default rules with the contents of `firebase-database-rules.json`
3. Click **Publish**

### Step 6 — Open in Android Studio

1. Open **Android Studio** (Electric Eel or newer recommended)
2. **File → Open** → Select the `Chattr` folder
3. Wait for Gradle sync to complete
4. Make sure `google-services.json` is in the `app/` folder

### Step 7 — Run the App

1. Connect a physical Android device (API 26+) **OR** start an emulator
2. Click the ▶️ **Run** button
3. For fingerprint on emulator: **Extended Controls → Fingerprint**

---

## 📁 Project Structure

```
Chattr/
├── app/
│   └── src/main/
│       ├── java/com/chattr/app/
│       │   ├── MainActivity.kt          ← Entry point + navigation
│       │   ├── data/
│       │   │   └── ChatRepository.kt    ← Firebase operations + models
│       │   ├── viewmodel/
│       │   │   ├── AuthViewModel.kt     ← Register/login logic
│       │   │   └── ChatViewModel.kt     ← Messaging logic
│       │   └── ui/
│       │       ├── theme/
│       │       │   ├── Color.kt         ← Color palette
│       │       │   └── Theme.kt         ← Compose theme
│       │       ├── components/
│       │       │   ├── Components.kt    ← Reusable UI (Avatar, FingerprintButton…)
│       │       │   └── BiometricHelper.kt ← Fingerprint prompt wrapper
│       │       └── screens/
│       │           ├── AuthScreen.kt    ← Login / Register UI
│       │           ├── ContactsScreen.kt ← Users list
│       │           └── ChatScreen.kt   ← Conversation UI
│       ├── AndroidManifest.xml
│       └── res/values/themes.xml
├── build.gradle.kts
├── settings.gradle.kts
├── gradle/libs.versions.toml
├── firebase-database-rules.json        ← Paste into Firebase Console
└── README.md
```

---

## 🔐 How Fingerprint Auth Works

1. User enters a **username**
2. App calls **Android BiometricPrompt** → device shows native fingerprint dialog
3. On biometric success, a **deterministic password** is derived from the username using SHA-256
4. This password is used with **Firebase Email/Password Auth** (`username@chattr.app`)
5. Only someone who can pass the biometric check on that device can log in

> On devices without a fingerprint sensor, the app falls back to username-only login automatically.

---

## 🧪 Testing on Emulator

To test fingerprint on an Android emulator:
1. In AVD, set up a PIN first: **Settings → Security → Screen Lock**
2. In Android Studio: **Extended Controls (⋯) → Fingerprint**
3. Click **"Touch the sensor"** when the fingerprint prompt appears

---

## 📦 Build Release APK

```bash
./gradlew assembleRelease
```
APK will be at: `app/build/outputs/apk/release/app-release.apk`

---

## 🔮 Planned Features

- [ ] Push notifications (FCM)
- [ ] Image/file sharing
- [ ] Group chats
- [ ] Message reactions (emoji)
- [ ] Online/offline status
- [ ] Profile pictures
- [ ] Message deletion

---

## 📄 License

MIT License — free to use and modify.
