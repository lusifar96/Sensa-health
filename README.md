# Sensa Health — Android App (Capacitor project)

This is a ready-to-build native Android wrapper around the Sensa Health web app.
It uses **Capacitor**, which packages your existing HTML/CSS/JS (`www/index.html`)
inside a real Android WebView app — so the app behaves exactly like the browser
version but installs from the Play Store, has a real app icon, and can request
device permissions (location, for the ambulance tracking screen).

## Update: new logo applied
- Your uploaded "Sensa Health by SP Industries" logo now replaces the old
  placeholder cross icon everywhere: the app launcher icon (all densities),
  the header/nav logo, the footer logo, and the browser favicon.
- The launcher icon uses just the "S" mark (cropped from your logo) since
  full logos with text don't read well at small icon sizes — this is
  standard practice (see any app icon on your phone).
- The full logo with "Sensa Health by SP Industries" text still appears in
  the app's header and footer.

## What's already done for you
- App ID: `com.spindustries.sensahealth`
- App name: **Sensa Health**
- Contact number updated to **+91 75859 40696** (site footer)
- Admin login popup no longer displays the password on screen
- Admin password changed to **Sensa@2026**
- Footer credit updated to **"Built and maintained by SP Industries"**
- Android permissions added: Internet, Network State, Fine/Coarse Location
  (needed for the ambulance live-tracking map)
- Your uploaded logo (the "S" mark) generated as the app icon for all
  densities, plus a 512×512 Play Store icon in `store-assets/`

## Important — why there's no .apk/.aab file included
Building the final installable file requires the **Android SDK and Gradle**,
which need internet access to Google's Maven repository and the Gradle
distribution server. Those aren't available in the sandbox this project was
prepared in, so I can't compile the final APK/AAB here. Everything else —
code, config, icons, manifest, permissions — is done and ready. You just need
to open the project on a machine with Android Studio and click Build.

## Get an actual .apk file — no coding, no Android Studio (recommended, free)

This project includes a **GitHub Actions workflow** that automatically
compiles a real, installable `app-debug.apk` file for you on GitHub's own
servers. You just upload the folder — no commands, no local build tools.

1. Go to https://github.com and create a free account (if you don't have one).
2. Click the **+** in the top right → **New repository**. Name it
   `sensa-health` (any name works), keep it **Private** or **Public**,
   click **Create repository**.
3. On the new repo's page, click **uploading an existing file** (or
   **Add file → Upload files**).
4. Unzip `sensa-app-android.zip` on your computer, then drag the **entire
   contents** of the unzipped `sensa-app` folder (the `android` folder,
   `www` folder, `.github` folder, `package.json`, everything) into the
   GitHub upload box. Commit the upload.
5. Click the **Actions** tab at the top of your repo. You'll see a build
   running automatically (triggered by your upload) — it takes about
   3–5 minutes.
6. Once it shows a green checkmark, click into that workflow run, scroll
   down to **Artifacts**, and download **sensa-health-apk**. Unzip it —
   inside is `app-debug.apk`.
7. Transfer that `.apk` file to your phone (email it to yourself, upload to
   Google Drive and download on the phone, or use a USB cable).
8. On your phone, tap the `.apk` file. Android will ask to allow install
   from this source (Settings → allow) — approve it, then tap **Install**.

That's your real, working Sensa Health app installed with your new logo —
entirely free, no computer software installed, no Play Store fee.

## Alternative: build locally in Android Studio (also free)

This is the fastest path if you just want the app running on your phone —
no Play Store, no $25 fee, no signing keystore needed.

1. **Install Android Studio** on a Windows/Mac/Linux computer (free):
   https://developer.android.com/studio
2. Unzip this project, then in Android Studio choose **Open** and select the
   `android/` folder from the unzipped project.
3. Let Gradle sync finish — this can take a few minutes the first time as
   Android Studio downloads build tools automatically.
4. On your phone: go to **Settings → About phone**, tap **Build number**
   7 times to unlock **Developer options**. Then go to
   **Settings → Developer options** and turn on **USB debugging**.
5. Plug your phone into the computer with a USB cable. Your phone will show
   a popup asking to allow USB debugging — tap **Allow**.
6. Back in Android Studio, your phone's name should appear in the device
   dropdown at the top (next to the Run button). Select it.
7. Click the green **Run ▶** button. Android Studio installs the app
   directly onto your phone and opens it automatically — usually done in
   under a minute.

That's it — the Sensa Health app icon (your new logo) will now be on your
phone's home screen/app drawer, just like any installed app. Every time you
change the code and click Run again, it reinstalls the updated version.

### If you don't have a USB cable handy
Android Studio also supports installing over Wi-Fi — under
**Pair devices using Wi-Fi** in the device dropdown, following the on-screen
QR code pairing steps. Same result, no cable.

### Alternative: build an APK file and install it manually
If you'd rather not keep the phone plugged into a computer, build a
standalone install file instead:
   - Menu: **Build → Generate Signed Bundle / APK**
   - Choose **Android App Bundle (.aab)** — this is what Play Store requires
   - Create a new **keystore** (a signing key) the first time — save this
     file and its passwords somewhere safe. You will need the *same* keystore
     for every future update of this app, forever. Losing it means you can
     never update the app again under the same listing.
   - Build type: **release**
   - This produces `app-release.aab` in `android/app/release/`

If you'd rather not install Android Studio yourself, any freelance Android
developer can open this project and produce the signed `.aab` in a few
minutes — the app itself is already fully built and configured.

## Publishing to the Google Play Store

1. Create a Google Play Console developer account (one-time **$25 USD** fee):
   https://play.google.com/console
2. Create a new app → fill in title ("Sensa Health"), description, category
   (Medical or Health & Fitness).
3. Upload the `app-release.aab` under **Production → Create new release**.
4. Upload store graphics:
   - App icon: use `store-assets/play_store_icon_512.png` (512×512, already generated)
   - Feature graphic: 1024×500 banner (not included — needs original design work)
   - At least 2 phone screenshots (take these from the running app)
5. Fill in the required **Data safety** form — since this app collects name,
   phone number, and location (for ambulance tracking), disclose that
   accurately.
6. Add a **Privacy Policy URL** — Play Store requires this for any app that
   collects personal data. You'll need to host a privacy policy page
   somewhere (even a simple hosted page works) before Google will approve
   the listing.
7. Since this app currently uses simulated/prototype payments, doctor
   listings, and WhatsApp notifications (not connected to real backends —
   see note below), make sure your store listing doesn't claim capabilities
   the app doesn't yet actually have; Google reviews for this.
8. Submit for review. First-time app reviews typically take a few days to
   a week.

## One thing worth knowing before you publish
Looking at the code, this build is still a **prototype/demo**: bookings,
payments (UTR/UPI verification), doctor approvals, and WhatsApp
notifications are all simulated in the browser's memory — nothing is sent
to a real server, database, or WhatsApp API, and all data resets when the
app restarts (nothing persists between sessions). That's fine for a demo
or investor walkthrough, but if real patients are meant to book real
doctors, pay real money, or get real ambulance dispatch through this app,
it needs a real backend (server, database, payment gateway, WhatsApp
Business API) before it goes live on the Play Store. Submitting it in its
current form to the public would risk real users trusting a booking flow
that doesn't actually reach anyone.

I'm glad to help build that backend piece by piece if that's the direction
you want to take this next.

## Project structure
```
sensa-app/
├── www/index.html          ← the web app (edited: contact, admin password, footer)
├── android/                 ← native Android project (open this in Android Studio)
├── store-assets/            ← 512×512 Play Store icon
├── capacitor.config.json    ← app ID / name config
└── package.json
```

## Making further edits later
If you edit `www/index.html` again, re-sync it into the Android project with:
```
npm install
npx cap sync android
```
then rebuild in Android Studio.
