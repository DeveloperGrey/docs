---
layout: doc
title: "Marai — Privacy policy"
heading: "Marai — Privacy policy"
description: "A local-first, zero-knowledge secrets manager: what it stores, where, and why we cannot read it."
icon: /marai/icon.png
tile_style: "--tile:#fdf0ef; --tile-pad:0.4rem"
---

_Last updated 23 September 2026_

Marai is built on a single principle: your secrets are yours alone. We cannot
see, access, or recover any data you store in the app — ever.

## 1. Introduction

This Privacy Policy describes how Marai ("the App", "we", "our") handles
information when you use our mobile application. Marai is a local-first,
zero-knowledge password and secrets manager. Your data never leaves your
device unless you explicitly choose to back it up to your own Google Drive
account.

## 2. Information we collect

**We collect no personal information.** The App does not transmit any data to
our servers because we do not operate any servers that receive your data.

All information you enter into Marai — passwords, usernames, tokens, notes,
and any other secrets — is:

- Stored exclusively on your device
- Encrypted before being written to storage, except for the entry's title,
  username and site address, which stay readable so that search and folders
  can work on your device
- Never sent to us or any third party by the App itself

## 3. How your data is stored

All vault data is stored in an encrypted SQLite database on your device.
Sensitive fields are individually encrypted using **AES-256-GCM** before being
written to the database.

| Data | Storage location | Encrypted? |
|---|---|---|
| Passwords, tokens, secrets | On-device SQLite database | Yes — AES-256-GCM |
| Notes, TOTP codes | On-device SQLite database | Yes — AES-256-GCM |
| Derived encryption key | Kept in memory while the vault is open; stored only while biometric unlock or autofill needs it | Yes — wrapped by a device-held key the system releases only after a recent fingerprint, face or PIN check |
| Your master password (Super Key) | Not stored anywhere | Never persisted |
| Entry titles, usernames and site addresses | On-device SQLite database | No — kept readable so search and folders work on the device |

## 4. Encryption

Marai uses industry-standard cryptography to protect your data:

- **Key derivation:** Your Super Key is run through PBKDF2-SHA256 with 600,000
  iterations and a random 32-byte salt to produce a 256-bit encryption key.
  (Vaults created before July 2026 used 100,000 iterations and are upgraded
  automatically the next time you unlock with your Super Key.)
- **Encryption:** AES-256-GCM with a unique random 12-byte nonce per field,
  providing both confidentiality and integrity (tamper detection).
- **Verification:** A SHA-256 hash of the derived key is stored to verify your
  Super Key on unlock — the key itself is never stored in plaintext.
- **Your Super Key is never stored.** If you lose it, your data cannot be
  recovered — by you or by us. It must be at least 12 characters.
- **The key at rest:** while the vault is open the derived key is held in
  memory and wiped when it locks. It is written down only when biometric
  unlock or autofill needs it, and then only wrapped by a key the device
  releases after a fresh fingerprint, face or PIN check. Turning biometric
  unlock off discards it. Adding a new fingerprint to the phone resets
  biometric unlock, so your Super Key is asked for again.
- **Screenshot protection:** The App blocks screenshots and screen recording of
  vault contents, and hides its contents in the app switcher.
- **Clipboard protection:** Anything you copy from the App (passwords, tokens,
  codes) is marked sensitive, so Android's clipboard preview masks it, and is
  cleared from the clipboard after 30 seconds.
- **No copies off the device:** Android's own cloud backup and
  device-to-device transfer are turned off for Marai. Entry titles, usernames
  and addresses are stored readable so search works, so a copied vault would
  have exposed the list of accounts even without the secrets.

## 5. Google Drive backup (optional)

Marai offers an optional backup feature that saves an encrypted copy of your
vault to your personal Google Drive account. This feature:

- Is entirely optional and must be explicitly enabled by you
- Saves data to _your_ Google Drive, not to our servers
- Uploads your vault in its fully encrypted `.marai` format — the backup file
  is unreadable without your Super Key, by us or by anyone who reaches your
  Drive
- Keeps one file per vault, named after that vault, so another device of yours
  can find it, and merges entry by entry rather than replacing the vault
- Carries deletions as dated records, so an entry deleted on one device does
  not return from another; those records are pruned after 180 days
- Requires you to sign in with your Google account — we receive only the OAuth
  token needed to write to your Drive

When you use Google Drive backup, Google's own
[Privacy Policy](https://policies.google.com/privacy) applies to the storage of
that file.

## 6. Biometric authentication (optional)

If you enable biometric unlock (fingerprint or Face ID), the App uses your
device's built-in biometric hardware. Marai never accesses raw biometric data —
authentication is handled entirely by the operating system (Android Biometric
API / iOS Local Authentication). The App only receives a pass/fail result.

## 7. Autofill (optional, Android)

You can set Marai as your device's autofill service to fill saved logins into
other apps and websites. When you do:

- Filling always requires **a strong biometric or your device PIN** first —
  the system prompt appears over the app you're filling; your vault is never
  opened silently. Weak face unlock is not accepted
- Only the **single username and password you explicitly pick** are handed to
  the requesting app via the Android Autofill Framework — nothing else in your
  vault is exposed
- A login is offered only to the site or app it was saved for: web addresses
  are matched on the registered domain, apps on the exact package and its
  signing certificate. Never a partial or fuzzy match
- Marai receives only the requesting app's package name or website domain, used
  locally to suggest matching entries; this is never transmitted anywhere. The
  index that makes this fast holds those domains and package names only —
  never titles, usernames or anything encrypted
- The feature is off until you enable it in your device settings, and Marai
  never offers to fill its own screens

## 8. Permissions

| Permission | Purpose |
|---|---|
| INTERNET | Required for optional Google Drive backup and Google Sign-In |
| USE_BIOMETRIC / USE_FINGERPRINT | Optional biometric unlock and autofill authentication |
| CAMERA | Optional QR-code scanning (2FA/TOTP setup) and entry icon photos |
| BIND_AUTOFILL_SERVICE | Optional autofill of logins into other apps (system-managed) |
| Face ID (iOS) | Optional biometric unlock on iPhone |

Marai asks for no photo-library permission: picking a custom icon goes through
the system photo picker, which hands over only the image you chose.

## 9. Third-party services

Marai does not integrate any analytics, advertising, crash reporting, or
tracking SDKs. The only optional third-party service is Google Drive for
backup, which is governed by Google's Privacy Policy.

## 10. Data retention and deletion

All your data resides on your device. You can delete it at any time by:

- Deleting individual entries or folders within the App
- Uninstalling the App (removes all local data)
- Manually deleting your `.marai` backup file from Google Drive

We have no copies of your data and cannot delete it on your behalf.

## 11. Children's privacy

Marai is not directed at children under the age of 13. We do not knowingly
collect personal information from children. Since we collect no data from any
user, this applies equally to all age groups.

## 12. Changes to this policy

We may update this Privacy Policy from time to time. Any changes will be
reflected by updating the "Last updated" date at the top of this page. We
encourage you to review this policy periodically.

## 13. Contact

Questions about this Privacy Policy:
[developer.greywolf@gmail.com](mailto:developer.greywolf@gmail.com)
