# Trelka — App Store Privacy Nutrition Label

**Prepared:** August 11, 2026  
**Basis:** read-only audit of `ocoee-studios/trelka` release candidate `feat/walkthrough-navigation` @ `cc59e4ab0b86f0276fbcca8a1933d7aeb4f1cc09`  
**App:** Trelka  
**Bundle ID:** `com.ocoeestudios.trelka`  
**Publisher:** Ocoee Studios LLC

> This worksheet describes the current release candidate. Re-run the audit against the exact App Store submission commit before answering App Store Connect, especially if monetization or any new SDK is added.

---

## Recommended App Store Connect top-level answer

> ### ✅ No, we do not collect data from this app

Apple defines collection as transmitting data off the device in a way that allows the developer or integrated third-party partners to access it for longer than is necessary to service the request in real time. Data processed only on device is not considered collected for the App Privacy label.

For the audited Trelka release candidate, property records, seller details, notes, tasks, photos, agent-profile content, and generated reports remain local unless the user explicitly chooses to share, email, print, save, or export them.

### Current verification basis

| Check | Result |
|---|---|
| Network primitives in app source (`fetch`, `XMLHttpRequest`, `WebSocket`, `axios`, `sendBeacon`) | None found |
| Analytics / telemetry / crash-reporting SDKs | None found |
| Advertising / attribution SDKs | None found |
| Accounts / authentication / cloud sync | None present |
| Ocoee Studios backend receiving property or seller content | None present |
| Runtime purchase / subscription SDK | None present in this release candidate |
| User-directed PDF/email/share/export | Present; initiated by the user |

Current package dependencies include Expo modules for local storage, camera/photo picking, file/PDF creation, sharing, and the system mail composer. `expo-mail-composer` prepares a system Mail message; it does not create an Ocoee Studios backend or analytics channel.

---

## Category-by-category answers

### Contact Info — **Not collected**
Trelka may store seller names/contact details and agent/brokerage profile fields locally. The developer does not receive those fields through an app server. A valid seller email may be passed into the system mail composer only when the user taps **Email Seller**.

### User Content — **Not collected**
Property details, room notes, tasks, free-form notes, photos, and generated PDF reports are stored and processed locally. They leave Trelka only through user-directed sharing/export destinations.

### Photos / Camera — **Permission used, not collected**
Trelka uses camera/photo-library permissions for property photos and optional profile imagery. Requesting or using those permissions does not by itself mean the developer collects the images. The audited app has no upload service for those files.

### Identifiers — **Not collected**
No advertising identifier, vendor identifier, device identifier, or developer user identifier is transmitted to Ocoee Studios. Locally generated UUIDs are used as app database identifiers.

### Diagnostics — **Not collected**
No crash-reporting or performance-telemetry SDK is present in the audited release candidate.

### Usage Data — **Not collected**
No analytics events, session tracking, screen-view telemetry, or behavioral measurement SDK is present.

### Location, Contacts, Microphone, Health, Financial Info, Browsing History — **Not collected**
The audited app does not request or implement these data categories as app features.

### Purchases — **Not collected in the audited release candidate**
No StoreKit/IAP implementation is present in `cc59e4a`. If the planned lifetime purchase is implemented before submission, this section must be re-audited against the final purchase library and Apple framework behavior before the App Privacy questionnaire is submitted.

---

## Tracking

**Answer: No.**

Trelka does not link app data with third-party data for advertising or advertising measurement, does not share data with a data broker, and does not include an advertising/attribution SDK. No App Tracking Transparency prompt is required for the audited release candidate.

---

## User-initiated data leaving the app

These flows are deliberate user actions and do not send content to an Ocoee Studios backend:

| Flow | What happens |
|---|---|
| **Email Seller** | Trelka generates the seller PDF and opens the iOS system mail composer. A parseable seller email may be prefilled. The user reviews and sends. |
| **Share PDF** | Opens the iOS share sheet for the generated report. |
| **Preview / Print / Save to Files** | Uses local/system destinations selected by the user. |
| **JSON export** | Creates a local export for the user to save or share. |
| **Contact Support** | Opens a user-controlled support email to `support@ocoeestudios.com`; the user chooses whether to send it. |
| **iOS / iCloud backup** | Controlled by the user's Apple/device settings, not an Ocoee Studios sync service. |

Once a user deliberately sends or shares content to another recipient/app/service, that destination's own privacy practices apply.

---

## App Store Connect answers for this release candidate

- **Does this app collect data?** → **No**
- **Data linked to the user?** → **None declared, because no data is collected by the developer/integrated partners in this release candidate**
- **Data used to track the user?** → **No**
- **Tracking / ATT?** → **No**
- **Privacy Policy URL** → `https://ocoee-studios.github.io/trelka-legal/privacy.html`
- **Privacy Choices URL (optional)** → `https://ocoee-studios.github.io/trelka-legal/privacy-choices.html`
- **Support URL** → `https://ocoee-studios.github.io/trelka-legal/support.html`
- **Public App Privacy summary** → `https://ocoee-studios.github.io/trelka-legal/privacy-label.html`

---

## Submission checklist

Before final App Store submission:

1. Audit the exact shipping commit, not an older branch.
2. Re-scan source and resolved dependencies for network, analytics, advertising, crash-reporting, attribution, auth, cloud, and purchase SDKs.
3. Confirm the privacy policy still matches the shipping feature set.
4. If StoreKit/lifetime Pro is added, review the purchase SDK and update this worksheet before answering App Store Connect.
5. Generate/review Xcode's privacy report/privacy manifests for the archive as an additional check.

---

## Current conclusion

For `feat/walkthrough-navigation` @ `cc59e4a`, the evidence supports Apple's **“Data Not Collected”** presentation. This conclusion is intentionally version-locked and must be refreshed if the shipping build changes its data flows or SDKs.
