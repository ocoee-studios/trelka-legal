# Trelka — App Store Connect URLs

**Updated:** August 11, 2026

| App Store Connect field | Status | URL |
|---|---|---|
| **Privacy Policy URL** | Required for iOS | `https://ocoee-studios.github.io/trelka-legal/privacy.html` |
| **Support URL** | Use for Trelka support | `https://ocoee-studios.github.io/trelka-legal/support.html` |
| **Marketing URL** | Optional | `https://ocoee-studios.github.io/trelka-legal/` |
| **Terms of Use / custom EULA page** | Optional unless we intentionally choose a custom license arrangement | `https://ocoee-studios.github.io/trelka-legal/terms.html` |
| **Privacy Choices URL** | Optional App Privacy field | `https://ocoee-studios.github.io/trelka-legal/privacy-choices.html` |
| **Public App Privacy summary** | Optional public reference page | `https://ocoee-studios.github.io/trelka-legal/privacy-label.html` |

## Current submission notes

- The Privacy Policy URL should be entered in App Store Connect and is required for the iOS app.
- The Privacy Choices page is available as an optional public explanation of local storage, deletion, permissions, sharing, and support communications.
- The Terms page contains Trelka-specific professional-use disclaimers, report/sharing responsibilities, and local-storage limitations.
- The App Privacy summary is a public-language companion to the internal `trelka-nutrition-label.md` audit worksheet; the actual Nutrition Label is configured in App Store Connect.
- The current privacy audit is version-locked to the release candidate documented in `trelka-nutrition-label.md`.
- If lifetime IAP, subscriptions, accounts, sync, analytics, crash reporting, or another SDK changes the shipping build, re-audit privacy and update the legal pages before submission.

## GitHub Pages

These files are maintained in the public `ocoee-studios/trelka-legal` repository and are intended to publish through the existing GitHub Pages site at `https://ocoee-studios.github.io/trelka-legal/`.
