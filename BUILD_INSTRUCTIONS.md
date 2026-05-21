# 📦 SNAPBOX — Android APK Build Instructions

## Requirements
- Android Studio Hedgehog (2023.1.1) or newer → https://developer.android.com/studio
- JDK 17+ (bundled with Android Studio)
- ~4GB disk space for Android SDK

---

## Step 1 — Open the project
1. Open Android Studio
2. **File → Open** → select the `snapbox-android` folder
3. Wait for Gradle sync to complete (~3-5 min first time)

---

## Step 2 — Build Debug APK (for testing)
```
Build → Build Bundle(s) / APK(s) → Build APK(s)
```
APK will be at:
```
app/build/outputs/apk/debug/app-debug.apk
```
Install on your phone with:
```bash
adb install app-debug.apk
```

---

## Step 3 — Build Release APK (for Play Store)

### 3a. Create a Keystore (one time only!)
```
Build → Generate Signed Bundle / APK → APK → Create new...
```
Fill in:
- **Key store path**: save somewhere safe (NOT in the project folder)
- **Password**: strong password
- **Key alias**: snapbox
- **Key password**: strong password
- **Validity**: 25 years
- **Name/Org**: your info

⚠️ **NEVER lose this keystore file** — you need it for every update!

### 3b. Build Signed APK
```
Build → Generate Signed Bundle / APK
→ APK → Next → select your keystore → Release → Finish
```

Signed APK at:
```
app/build/outputs/apk/release/app-release.apk
```

---

## Step 4 — Build AAB (recommended for Play Store)
```
Build → Generate Signed Bundle / APK → Android App Bundle → Next
→ select keystore → Release → Finish
```

AAB at:
```
app/build/outputs/bundle/release/app-release.aab
```
✅ Use **AAB** for Play Store — smaller downloads for users

---

## Step 5 — Publish to Google Play

1. Go to → https://play.google.com/console
2. Create new app → **SnapBox**
3. Fill in:
   - **App name**: SnapBox — Puzzle Adventure
   - **Category**: Puzzle
   - **Content rating**: Everyone
4. Upload your `.aab` file
5. Upload graphics from `play-store-assets/` folder:
   - `icon_512.png` → App icon
   - `feature_graphic.png` → Feature graphic
6. Write description (see below)
7. **Pricing**: Free
8. Submit for review (~3-7 days)

---

## Play Store Description (copy-paste)

**Short (80 chars):**
> Pack shapes into crates. 100 levels. 4 worlds. 4 epic bosses!

**Full description:**
> SNAPBOX is a satisfying hyper-casual puzzle game where you pack uniquely shaped pieces into crates.
>
> 🧪 BIO LAB — Pack crates in the laboratory before Dr. Chaos drops toxic tubes!
> ⚙️ MEGA FACTORY — Beat MACH-9000 as it bolts cells shut one by one!
> 🚀 DEEP SPACE — Fight the Void King's rocket barrage in zero gravity!
> 🏺 LOST TEMPLE — Race the Pharaoh's crumbling curse before it destroys everything!
>
> ✦ 100 handcrafted levels
> ✦ 4 themed worlds with unique music & visuals
> ✦ 4 boss battles with special mechanics
> ✦ Coins, skins & leaderboards
> ✦ Daily challenge
> ✦ Boosters: hints, slow-motion, auto-place

**Keywords:**
puzzle, packing, shapes, casual, brain, block, tetris, drag, fun, kids, family

---

## Minimum SDK Info
- **Min Android**: 7.0 (API 24) — covers 98%+ of devices
- **Target**: Android 14 (API 34)
- **Orientation**: Portrait only
- **Internet**: Required for fonts (first launch only)

---

## Troubleshooting

**Gradle sync fails?**
→ File → Invalidate Caches → Restart

**Build fails with "SDK not found"?**
→ Tools → SDK Manager → install Android 14 (API 34)

**App crashes on launch?**
→ Check logcat for errors. Usually a WebView permission issue.
→ Make sure `index.html` is in `app/src/main/assets/`

**White screen on launch?**
→ The HTML file needs internet for fonts. Test with WiFi first.
→ Or embed fonts locally in the HTML file.
