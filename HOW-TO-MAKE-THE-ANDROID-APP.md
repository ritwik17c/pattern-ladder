# Turning "Pattern Ladder" into an Android app

This folder is a complete Android project. The app itself is one web page
(`www/index.html`). A free tool called **Capacitor** wraps that page inside a
real Android app, so it works offline and installs like any other app.

You only need to do this once. After that, every time the lessons change you
repeat Step 3 and download a fresh app.

---

## What is in this folder

```
www/index.html              the whole app: lessons, questions, screens
www/manifest.webmanifest    app name and colours
assets/                     the app icon and splash screen pictures
capacitor.config.json       app ID and name used by Android
package.json                the list of tools Capacitor needs
.github/workflows/          instructions that let GitHub build the APK for you
```

---

## Route A — let GitHub build it (nothing to install)

An **APK** is the file Android phones install apps from.
GitHub (free) can build it for you on its own computers.

1. **Make a GitHub account** at github.com if you do not have one.
2. **Create a new repository.** Click the **+** at the top right, then
   *New repository*. Name it `pattern-ladder`. Choose *Private* or
   *Public*. Click *Create repository*.
3. **Upload this folder.** On the new repository page click
   *uploading an existing file*. Drag in **everything inside this folder**,
   including the hidden `.github` folder. (On Windows, turn on
   *View → Show → Hidden items* in File Explorer to see it.)
   Click *Commit changes*.
4. **Wait for the build.** Open the *Actions* tab. A job called
   *Build Android APK* starts by itself. It takes about 5–8 minutes.
   A green tick means it worked.
5. **Download the app.** On the repository's main page, click *Releases*
   (right-hand side) and download `pattern-ladder.apk` from the newest one.
   Each build makes a new numbered release (1.0.3, 1.0.4 …).
6. **Install on a phone.** Copy `pattern-ladder.apk` to the phone (WhatsApp to
   yourself, Google Drive, or a USB cable). Tap it. Android will ask you to
   allow installing from this source; allow it once.

If a step shows a red cross, open it, copy the last few lines of the error,
and paste them to Claude.

---

## Route B — build it on your own laptop (Android Studio)

Use this route later, when you want to publish on the Google Play Store.

1. Install **Node.js (LTS)** from nodejs.org and **Android Studio** from
   developer.android.com/studio.
2. Open a terminal (*Command Prompt* on Windows) inside this folder and run,
   one line at a time:

   ```
   npm install
   npx cap add android
   npx capacitor-assets generate --android
   npx cap sync android
   npx cap open android
   ```

3. Android Studio opens the project. Wait for it to finish "Gradle sync",
   then choose *Build → Build App Bundle(s) / APK(s) → Build APK(s)*.

---

## Changing the lessons later

All lessons and questions live in one list inside `www/index.html`
(search for `window.UNITS`). Each unit looks like this:

```
{ id: "u01", level: 1, vp: "VP 21", title: "Subject + Verb",
  formula: "S + V",
  explain: "...",
  ex: ["The bell rang.", ...],            examples (also used for word-order drills)
  qs: [ { t: "m", q: "...", o: [...], a: 0, e: "..." },   multiple choice: a = number of the right option
        { t: "f", q: "...", a: ["answer"], e: "..." } ]   fill in the blank: a = accepted answers
}
```

Edit, save, then upload the changed file to GitHub (Route A, Step 3). A new
APK is built automatically.

## Before the Play Store

The APK from Route A is a "debug" build: perfect for students and staff to
install directly. The Play Store needs a "signed release" build, a
developer account (one-time fee), a privacy note and screenshots. Ask Claude
for help with that step when you are ready.
