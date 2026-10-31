# ONU Config Generator (VSOL and C-Data GPON)

A free browser tool for making ONU configuration commands for **VSOL** and **C-Data** GPON OLTs, and for cleaning up duplicate ONUs.

Live site: https://eleashs.github.io/OlT-Config-Vsol-And-C-Data/

## What it does

- **Config Generator**: builds the ONU config commands for VSOL or C-Data. Use *Single ONU* for one ONU or *Batch Mode* for many at once.
- **Index Finder**: finds free ONU index numbers (1 to 128).
- **Duplicate Finder**: finds an ONU serial number (SN) that is registered on more than one PON, and prepares delete commands for the inactive copy.
- **Saved Presets** and **ONU Work Log**: keep your commands and records, with CSV export.
- **Login**: tags the operator name in the work log. It can use Firebase so your data follows you across devices.
- **Colour themes**: pick a theme with the dots at the bottom right of the page.

## Duplicate Finder

1. Choose the OLT brand (VSOL or C-Data).
2. Paste the ONU list from the OLT. All PONs can be pasted together.
3. Press **Find Duplicates**.

How the active copy is chosen:

| OLT | How state is read |
|---|---|
| VSOL | A model shown as `unknown` is treated as offline (inactive). A known model is active. |
| C-Data | The Online / Offline column is used. |

Delete commands are built only when one copy is active and the others are inactive. If every copy is inactive, or more than one is active, you decide by hand. You get one command box per PON, plus a CSV list of what will be deleted.

Command formats:

```
VSOL                        C-Data
interface gpon 0/2          interface gpon 0/0
no onu 5                    ont delete 1 5
exit                        exit
```

Always check the commands against your own OLT before running them, and save the OLT configuration afterwards.

## Run it

It is a single `index.html` file. Open it in a browser, or publish it with GitHub Pages.

## Optional: Firebase login and cloud sync

Without Firebase the site works fully offline with a local login. To turn on cloud login:

1. Create a Firebase project and add a **Web app**.
2. Enable **Authentication > Email/Password**.
3. Add your `github.io` domain under **Authentication > Settings > Authorized domains**.
4. Create a **Firestore** database and publish these rules:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

5. Put your config values (`apiKey`, `authDomain`, `projectId`, `appId`) into `FIREBASE_CONFIG` near the bottom of `index.html`.

A Firebase web config is not a secret. Your data is protected by the rules above, so each user can only read and write their own document.

## Privacy

The generators and the Duplicate Finder run in your browser and send nothing anywhere. Saved presets and the work log are kept in your browser. If you log in with Firebase, they are also stored in your own user document.

Copyright 2026 Elias Hossen. All rights reserved.
