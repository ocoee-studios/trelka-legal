# Trelka — App Store Privacy Nutrition Label

**Prepared:** August 7, 2026
**Basis:** read-only audit of `ocoee-studios/trelka` @ `4804bdb173132d76a2a8933428f4c8632793c913` (origin/master)
**App:** Trelka, bundle ID `com.ocoeestudios.trelka`, publisher Ocoee Studios LLC

---

## Recommended top-level answer

> ### ✅ No, we do not collect data from this app

This is recommended **because the audit verified there is no off-device transmission path**, not because data is stored locally.

### Why this is justified

Apple defines "collect" as transmitting data off the device and retaining it beyond the transient processing needed to service a request. The audit confirmed:

| Requirement for "No collection" | Verified? | Evidence |
|---|---|---|
| No network transmission in app code | ✅ | Zero `fetch`, `XMLHttpRequest`, `WebSocket`, `axios`, or `sendBeacon` calls anywhere in `src/`, `app/`, `index.ts` |
| No analytics / telemetry SDK | ✅ | Absent from `package.json` **and** from the full resolved dependency tree in `package-lock.json` |
| No crash / diagnostic reporting | ✅ | No Sentry, Bugsnag, Crashlytics anywhere in the resolved tree |
| No advertising or attribution SDK | ✅ | No AdMob, Facebook, Adjust, AppsFlyer, Branch, OneSignal in the resolved tree |
| No backend / cloud storage | ✅ | No API base URL, no cloud DB client, no Supabase/Firebase/AWS |
| No accounts or authentication | ✅ | No auth, sign-in, token, or credential code |
| No third party receives data | ✅ | No third-party service is contacted at runtime at all |

The only `http://` string in the entire codebase is the SVG XML namespace declaration
(`xmlns="http://www.w3.org/2000/svg"` in `src/utils/spike-data.ts:29`) — an identifier, not a request.

---

## Category-by-category answers

### Contact Info — **Not collected**
The app stores a seller name, a seller contact detail, and agent/brokerage profile details. All of it is written to the local SQLite database only. Nothing transmits it. **Not "collected" in Apple's sense.**

### User Content (photos, notes, property records) — **Not collected**
Photos, room notes, property records, tasks, and generated PDFs are stored in the app's local container. `expo-print` renders PDFs locally; every `<img src>` in the report HTML points at a local URI (`localUri`, `reportUri`, `headshotLocalUri`, `logoLocalUri`) — no remote asset is fetched during rendering.

### Photos / Camera — **Permission used, not collected**
- `NSCameraUsageDescription` and `NSPhotoLibraryUsageDescription` are declared and accurate.
- Camera is reached via `ImagePicker.launchCameraAsync` (`app/property/[id]/walkthrough.tsx:423`).
- Photo library via `ImagePicker.launchImageLibraryAsync` (walkthrough + `app/profile.tsx:152`).
- **Requesting a permission is not collection.** Captured images never leave the device except by user-initiated share.

### Identifiers — **Not collected**
No advertising identifier (IDFA), no vendor identifier, no device ID, no user ID is read or transmitted. `expo-crypto`'s `randomUUID` generates local database primary keys only — these never leave the device and are not tied to a person.

### Diagnostics — **Not collected**
No crash reporting and no performance telemetry. `expo-constants` is read only to display the app version/build in the UI and to prefill a support email body the user composes and sends themselves.

### Usage Data — **Not collected**
No analytics events, no session tracking, no screen-view instrumentation.

### Location, Contacts, Microphone, Health, Financial, Browsing History — **Not collected**
None of these capabilities exist in the app. `expo-location`, `expo-contacts`, `expo-av`/`expo-audio`, and `expo-notifications` are absent from the entire resolved dependency tree.

### Purchases — **Not collected**
No in-app purchase implementation. No StoreKit usage, no RevenueCat.

---

## Tracking

**Answer: No.** Trelka does not track. There is no advertising identifier access, no advertising or attribution SDK, no third-party data broker, and no cross-app or cross-website linkage. **No App Tracking Transparency prompt is required**, and `expo-tracking-transparency` is correctly absent.

## Third-party data receipt

**Answer: None.** No third party receives any data from Trelka. There is no analytics vendor, no backend, no payment processor, and no SDK that phones home.

---

## User-initiated data egress (disclose in policy, but NOT "collection")

These paths exist, are all explicitly user-initiated, and none send anything to Ocoee Studios. They belong in the privacy policy — which they are in — but they do **not** change the nutrition-label answer, because the developer never receives the data.

| Path | Location | Notes |
|---|---|---|
| Share generated PDF report | `app/property/[id]/report.tsx:224` | via `Sharing.shareAsync`, iOS share sheet |
| Export data as JSON | `app/settings.tsx:234` | property records, rooms, tasks, seller details, agent profile; **photo files deliberately excluded** |
| Support email | `app/help.tsx:92`, `app/settings.tsx:253` | `Linking.openURL` opens a hardcoded `mailto:support@ocoeestudios.com`; body prefilled with app version/build only. User reviews and sends. |
| iOS device / iCloud backup | OS-level | outside app control, governed by user's Apple settings |

`Linking.openURL` is only ever called with a `mailto:` URL built by `supportMailto()` (`src/services/onboarding.ts:136`). It cannot open an arbitrary URL.

---

## ⚠️ Items to note before submitting

1. **Seller contact field.** The app has a `sellerContact` column and UI field (`app/property/new.tsx:158`, displayed at `app/property/[id]/index.tsx:255`) — third-party personal information. This does **not** affect the nutrition label (never transmitted), but it is a real privacy-policy obligation and has been documented on the public privacy page. Worth confirming this field is intended to ship.

2. **`expo-camera` is an unused dependency.** It is in `package.json` and configured as a config plugin in `app.json`, but is never imported in `src/` or `app/`. Camera access actually happens through `expo-image-picker`. The camera permission string is still required and accurate, so **this does not change any answer** — but it is dead weight and, if a reviewer greps dependencies, an unnecessary question to invite. Read-only audit, so no change was made.

3. **Audit point vs. local HEAD.** The audit covers pushed `origin/master` @ `4804bdb`. The local working copy was one commit ahead (`333d874`, accessibility layout work). Those commits are UI-layout only and introduce no network or SDK changes, but **re-verify if anything beyond accessibility work lands before submission.**

4. **This answer is version-locked.** Adding accounts, sync, analytics, crash reporting, or purchases in any future build requires revisiting this worksheet before that build ships.

---

## No ambiguity flagged

Every category above resolved cleanly against verified code. There is no category where I had to guess.
