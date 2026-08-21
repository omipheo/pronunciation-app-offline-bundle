# Offline development bundle

Split archive of the development environment for
[pronunciation-app](https://github.com/omipheo/pronunciation-app) — JDK, Android SDK, Gradle,
Python packages, espeak-ng and the generated speech models.

Split into 50 MB volumes because GitHub rejects any file over 100 MB.

## Extract

Download **every** `.rar` part into one folder, then open the first volume with
[WinRAR](https://www.win-rar.com/) or [7-Zip](https://www.7-zip.org/). The rest are found
automatically:

```powershell
7z x pronunciation-offline.part001.rar
```

## Check the set first

A missing volume makes the archive unextractable:

```powershell
7z t pronunciation-offline.part001.rar
```

`Everything is Ok` means the set is complete.

## Install

```powershell
cd pronunciation-offline
.\offline-install.ps1 -ProjectDir C:\pronunciation-app
```

Then, in a **new** terminal:

```powershell
cd C:\pronunciation-app
.\gradlew.bat assembleDebug --offline
```

Anything not present in the archive can be re-fetched from the main repository:

```powershell
python tools/fetch_offline_sources.py C:\pronunciation-offline
```

## Third-party software and licences

This bundle redistributes unmodified third-party software; each remains under its own licence:

| Component | Licence |
|---|---|
| Eclipse Temurin JDK 17 | GPLv2 with Classpath Exception |
| Gradle | Apache 2.0 |
| Python | PSF License |
| espeak-ng | GPLv3 |
| MinGit | GPLv2 |
| CMUdict | BSD-style |
| wav2vec2 models | see their HuggingFace model cards |
| **Android SDK, emulator and system images** | **Google's Android SDK Terms and Conditions** |

The Android SDK components are Google's, and Google's terms restrict redistribution. They are
included for convenience only — obtain them from Google directly at
<https://developer.android.com/studio>, or run `python tools/fetch_offline_sources.py` from the
main repository, which downloads them from Google's own servers.
