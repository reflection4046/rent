# RentFlow — Android Studio APK Project (Redesigned)

A native Android WebView shell for the RentFlow web app, with a polished native UI layer:
launch splash screen, branded adaptive app icon, gradient loading bar, and a proper
offline/error screen with a Retry button (instead of a bare toast).

## 🎨 What changed in this redesign
- **New adaptive app icon** — dark slate badge with an ascending "flow" bar-chart + trend
  line mark (`res/drawable/ic_launcher_*.xml`, `res/mipmap-anydpi*/ic_launcher*.xml`).
  The original project had **no launcher icon at all**, which would have failed to build.
- **Native splash screen** using `androidx.core:core-splashscreen`, themed to match the
  brand (`Theme.RentFlow.Splash` in `themes.xml`), held on screen until the web content
  has actually finished painting.
- **Gradient progress bar** (`progress_bar_gradient.xml`) instead of a flat system bar.
- **Real offline/error state** — icon, headline, subtitle, and a rounded "Retry" button,
  swapped in for the WebView instead of a disappearing Toast. Wired to a real
  connectivity check (`ConnectivityManager`) so it triggers before even attempting a load.
- Expanded, consistent color palette (`colors.xml`) — surfaces, text, accent gradient,
  success/error tones — used consistently across the UI instead of one-off hex values.
- Pull-to-refresh spinner recolored to match the brand palette.

The RentFlow screens themselves (login, dashboard, tenant list, payments, etc.) are served
from your existing backend at the URL in `MainActivity.kt` — this project is the native
"frame" around that web app, not the web app itself.

## ⚠️ About the compiled .apk file
Compiling an Android `.apk` requires the Android SDK + Gradle build toolchain, which
isn't available in the sandbox this project was edited in — so no `.apk` binary is
attached here, only the updated source project. You have two easy ways to get a real,
installable APK from it:

### Option A — Automatic build via GitHub Actions (no local setup)
1. Push this folder to a new GitHub repository.
2. GitHub Actions will automatically run `.github/workflows/build-apk.yml` on push
   (or trigger it manually from the **Actions** tab → **Build RentFlow APK** → **Run workflow**).
3. When it finishes (~2 minutes), open the workflow run → **Artifacts** →
   download **RentFlow-debug-apk** → unzip → `app-debug.apk`.
4. Transfer that APK to your phone and install it (enable "Install unknown apps" for
   whichever app you use to open the file).

### Option B — Build locally in Android Studio
1. Unzip this project.
2. Open **Android Studio** (Koala / Ladybug or newer) → **Open** → select this folder.
3. Let Gradle sync (downloads dependencies the first time).
4. **Build** → **Build Bundle(s) / APK(s)** → **Build APK(s)**.
5. Click **locate** on the completion popup, or open:
   `app/build/outputs/apk/debug/app-debug.apk`

### Option C — Command line (requires Android SDK installed)
```bash
# Mac/Linux
./gradlew assembleDebug
# Windows
gradlew.bat assembleDebug
```
Output: `app/build/outputs/apk/debug/app-debug.apk`

## 📱 Installing on your phone
Transfer `app-debug.apk` via USB, Google Drive, or similar, then tap it to install.
You'll need to allow "install unknown apps" for the source you used.

Default Admin Credentials (for the RentFlow backend, unrelated to this shell):
- Username: `admin`
- Password: `admin123`
