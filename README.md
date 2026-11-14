# GORA AI — private, offline Android assistant

Native Kotlin, minSdk 26, tuned for Android 12 / low-RAM phones (POCO M3).
Dependencies: androidx core, appcompat, recyclerview. Nothing else.

## Privacy
- **No INTERNET permission** (only RECORD_AUDIO, SET_ALARM). The app UI re-checks this at runtime.
- No analytics, ads, cloud, or background services. Backups disabled.
- Memory: AES-256-GCM, key in Android Keystore, stored in app-private storage.
- Speech-to-text: on-device recognizer only (Android 12+). No cloud fallback — if the offline pack is missing, voice is disabled with an explanation.
- Text-to-speech: only voices that do not require a network are used.

## Build (GitHub — no installs needed)
1. Create an empty GitHub repo, upload all files in this folder (keep `.github/`).
2. Open the **Actions** tab → "Build GORA AI APK" runs automatically (or press *Run workflow*).
3. Download `GORA-AI.apk` from **Releases** (right side of the repo page) or from the run's Artifacts.
4. Install on the phone (allow "install unknown apps" for your browser/file manager).

## Build locally
Android Studio (Koala+) → Open this folder → Run. Or: `gradle assembleDebug` (JDK 17, Gradle 8.7).

## Offline speech setup (once)
Phone Settings → Google → (Voice) → Offline speech recognition → download English (India), Hindi, Bengali.

## Honest limitations of this version
- No LLM is bundled: the "brain" is a rule-based engine (commands, calculator, summarizer, small phrasebook).
  Open-ended Q&A / real translation need a local model (e.g. llama.cpp + GGUF) which cannot be shipped here.
- Wake word works only while the app is open (screen on), by design, to avoid a battery-draining background service.
  It auto-pauses after 5 minutes of silence.
- Voice is "male-leaning" (offline male voice if installed, else lowered pitch).
- Not yet tested on a device — it was written without an Android SDK available. Expect to fix small issues on first build.
