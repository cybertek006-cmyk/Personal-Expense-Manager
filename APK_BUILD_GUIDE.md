# How to Build an Android APK — My Expense Control

This project is pre-configured to generate an installable Android `.apk` for **My Expense Control** (`com.mannu.expensecontrol`) with full offline IndexedDB support, Indian Rupee (`₹`) formatting, and custom `192x192` / `512x512` adaptive launcher icons.

Below are the **3 ways** to create your `.apk`, starting with **Option A (Standalone Offline Native APK via Capacitor)**.

---

## Option A — Standalone 100% Offline APK (Capacitor)

Capacitor bundles the compiled `dist/` app directly inside a native Android `.apk`.
- **No web server or hosting required**
- **Works 100% offline immediately after installing the `.apk`**
- **Keeps all IndexedDB financial data private on your phone**

We have already pre-installed `@capacitor/core`, `@capacitor/android`, `@capacitor/cli`, and created `capacitor.config.json`.

### Method A1: Build APK in the Cloud with GitHub Actions (Easiest — No Android Studio Needed!)

If you do not want to install 5 GB of Android Studio and Java SDK on your computer, GitHub will compile the `.apk` for free in ~3 minutes:

1. Create a new (private or public) repository on [GitHub](https://github.com/new).
2. Upload or push all files from this project (make sure the `.github/workflows/build-android-apk.yml` file is included).
3. On your GitHub repository page, click the **Actions** tab at the top.
4. Click **Build Android APK (My Expense Control)** on the left sidebar, then click **Run workflow → Run workflow**.
5. Wait ~2–3 minutes for the green checkmark, open the completed workflow run, and scroll down to **Artifacts**.
6. Click **`My-Expense-Control-APK`** to download the `.zip` file, extract **`app-debug.apk`**, send it to your Android phone (via USB, WhatsApp, or Files), and tap to install!

---

### Method A2: Build APK Locally on Your PC (Android Studio or Terminal)

**Prerequisites on your PC:**
- [Node.js 20+](https://nodejs.org/)
- [Android Studio](https://developer.android.com/studio) (includes Android SDK & Java JDK 21)

**Steps:**
1. Open a terminal in the project folder and build the web app:
   ```bash
   npm install
   npm run build
   ```
2. Generate and sync the native Android project:
   ```bash
   npx cap add android
   npx cap sync android
   ```
3. **To build using Android Studio GUI:**
   - Run `npx cap open android`
   - Wait for Gradle sync to finish at the bottom of Android Studio.
   - In the top menu bar, click **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
   - Click **locate** in the bottom-right notification to get `app-debug.apk`!

4. **Or to build directly from the terminal (macOS / Linux / Windows):**
   - macOS / Linux:
     ```bash
     chmod +x scripts/build-apk.sh && ./scripts/build-apk.sh
     ```
   - Windows (PowerShell / CMD):
     ```bat
     cd android
     gradlew.bat assembleDebug
     ```
   - Your installable `.apk` will be saved at:
     `android/app/build/outputs/apk/debug/app-debug.apk`

5. **Optional — Set Custom Launcher Icons Inside Capacitor Android:**
   If you want Capacitor to replace the default Android Studio icon across all `mipmap-*` densities automatically:
   ```bash
   npx @capacitor/assets generate --iconBackgroundColor '#0f172a' --android
   ```
   *(Place `public/icon-512.png` at `assets/icon.png` first before running `@capacitor/assets`.)*

---

## Alternative No-Code APK — PWABuilder (From a Free Hosted URL in 60 Seconds)

Because `public/manifest.webmanifest` now includes `192x192`, `512x512`, and `maskable` PNG icons alongside `sw.js`, you can also generate a signed Trusted Web Activity (TWA) `.apk` with zero tools:

1. Run `npm run build` to generate the `dist/` folder.
2. Drag and drop the `dist/` folder onto [Netlify Drop](https://app.netlify.com/drop) (or deploy to Vercel / Cloudflare Pages / GitHub Pages) to get an `https://...` link.
3. Go to **[PWABuilder.com](https://www.pwabuilder.com/)**, paste your HTTPS URL, and click **Start**.
4. Click **Package for stores → Android → Download Package**.
5. Unzip the downloaded folder and install the signed `.apk` on your Android phone!

---

## Installing the `.apk` on Your Android Phone

1. Copy `app-debug.apk` (or `My-Expense-Control.apk`) to your Android phone.
2. Tap the `.apk` file in your phone's **Files** manager.
3. If prompted with *"Install unknown apps"*, tap **Settings → Allow from this source**, then tap **Install**.
4. If Google Play Protect asks *"App not recognized / Scan app"* (normal for personal self-built APKs), tap **More details → Install anyway**.
5. Open **My Expense Control** from your home screen!
