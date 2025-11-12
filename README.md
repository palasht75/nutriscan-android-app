# NutriScan AI PoC

This is a simple Capacitor app that captures a photo, uploads it to S3 using temporary credentials, and sends the image to Gemini for analysis. 

---

## File Structure
* A `www/` folder with a single page app
* Android project files created by Capacitor after you run the commands below

**Folder layout**

```
project-root/
  www/
    index.html      # main app file you will edit for keys and region
  android/          # created by Capacitor (after you add Android)
  package.json
  capacitor.config.ts or capacitor.config.json
```

---

## Requirements on your machine

* Node.js 18 or newer, npm
* Java JDK 17
* Android Studio with Android SDK and an emulator device

---

## One time setup

From the project root:

```bash
npm i -g @capacitor/cli
npm i @capacitor/core @capacitor/android
```

Initialize Capacitor if the project is not already initialized:

```bash
npx cap init nutriscan-ai com.example.nutriscan
# When asked for webDir, answer: www
```

Add the Android platform:

```bash
npx cap add android
```

---

## Put in the credentials

Open `www/index.html`, find the config constants near the top of the `<script>` tag, and replace the placeholders.

```js
// AWS
const AWS_REGION = "us-east-1";                    // use the region I shared if different
const COGNITO_IDENTITY_POOL_ID = "us-east-1:...";                  

// Gemini
const GEMINI_API_KEY = "paste_the_key_from_email"; // for this class PoC only
```

You do not need to create Cognito or S3. The values are already active. Only need to paste them.

---

## Build and run

Copy web assets into the native project and open Android Studio:

```bash
npx cap copy
npx cap sync android
npx cap open android
```

Run the app from Android Studio on an emulator or a USB Android device.

### After you change `www/index.html`

```bash
npx cap copy
npx cap sync android
```

Then click Run again in Android Studio.

---

## Create a shareable APK

In Android Studio:

* Menu: Build → Build Bundle or APKs → Build APKs
* The file will appear under `app/build/outputs/apk/`

If you cannot install directly, you may need to allow installs from unknown sources on the phone.
---

## How to use the app

1. Open the app
2. Tap **Scan Your Meal**
3. On an emulator, use the virtual camera or pick an image from file when prompted
4. Tap **Analyze Meal with AI** to send the image to Gemini
5. Results will show on the Results screen

---

## Troubleshooting

* **Camera button does nothing on emulator**: some emulators have no camera feed. Use the file picker fallback or switch to a physical device.
* **CORS error**: wait a minute and try again. The bucket is already configured for PUT and GET.

---

## What modules are installed

* `@capacitor/cli` (global)
* `@capacitor/core` and `@capacitor/android` (local)

CDN scripts already included in `index.html`:

* Tailwind CSS
* Lucide icons
* `capacitor.js` bridge
* AWS SDK v2 for JavaScript

You do not need any other npm libraries for this PoC.

---
