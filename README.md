# NaijaTools Android — Play Store Ready Build

Free all-in-one digital toolkit for Nigerians. Packaged as a native Android app.

## 🚀 Quick Start — Get Your APK in 5 Minutes

1. Upload this folder to a new GitHub repo
2. Click **Actions** tab → wait for green ✅ (~5 min)
3. Download the **debug APK** artifact → install on Android

## 📦 Files in This Project

```
├── .github/workflows/build.yml     ← Builds APK + AAB automatically
├── app/
│   ├── src/main/assets/www/        ← Your PWA (index.html, sw.js, manifest.json)
│   ├── java/com/naijatools/app/    ← Native Android wrapper (MainActivity.java)
│   ├── res/                        ← Icons, themes, layouts
│   └── build.gradle                ← App config
├── store-assets/
│   ├── icon-512.png                ← Play Store icon (512×512)
│   ├── feature-graphic-1024x500.png← Play Store banner
│   ├── screenshot-phone-1/2/3.png  ← Play Store screenshots
│   ├── privacy-policy.html         ← Host this on GitHub Pages
│   └── PLAY-STORE-LISTING.txt      ← Copy-paste store description
└── README.md
```

## 🔐 Setting Up Signing (Required for Play Store)

### Step 1 — Generate Keystore (once only, keep it safe!)
```bash
keytool -genkey -v -keystore naijatools.jks \
  -alias naijatools -keyalg RSA -keysize 2048 -validity 10000
```

### Step 2 — Convert to Base64
```bash
# Linux / Mac
base64 -w 0 naijatools.jks

# Windows (PowerShell)
[Convert]::ToBase64String([IO.File]::ReadAllBytes("naijatools.jks"))
```

### Step 3 — Add GitHub Secrets
Go to: GitHub repo → Settings → Secrets and variables → Actions → New secret

| Secret Name | Value |
|---|---|
| `KEYSTORE_BASE64` | Base64 output from step 2 |
| `KEYSTORE_PASSWORD` | Your keystore password |
| `KEY_ALIAS` | `naijatools` |
| `KEY_PASSWORD` | Your key password |

### Step 4 — Push & Download
Push any commit → Actions builds 3 artifacts:
- `NaijaTools-debug-apk` — for direct install/testing
- `NaijaTools-release-apk` — signed APK for sharing
- `NaijaTools-release-aab` — **upload this to Play Store**

## 🌐 Host the Privacy Policy
1. Enable GitHub Pages on your repo (Settings → Pages → Deploy from branch: main)
2. Move `store-assets/privacy-policy.html` to the repo root
3. Your privacy policy URL: `https://[username].github.io/[repo]/privacy-policy.html`
4. Paste this URL in Google Play Console → App Content → Privacy Policy

## 📋 Play Store Checklist
See `store-assets/PLAY-STORE-LISTING.txt` for the full step-by-step checklist.

## 🔄 Updating the App
Edit `app/src/main/assets/www/index.html` → push → GitHub Actions rebuilds everything.
