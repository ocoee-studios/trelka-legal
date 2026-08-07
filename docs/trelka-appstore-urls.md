# Trelka — App Store Connect URLs

All URLs verified live (HTTP 200) on August 7, 2026.

| App Store Connect field | Required? | URL | Where it lives |
|---|---|---|---|
| **Privacy Policy URL** | **Required** | `https://ocoee-studios.github.io/trelka-legal/privacy.html` | App Store Connect → App Privacy → Privacy Policy |
| **Support URL** | **Required** | `https://ocoee-studios.github.io/trelka-legal/support.html` | App Store Connect → App Information (localizable) |
| **Marketing URL** | Optional | `https://ocoee-studios.github.io/trelka-legal/` | App Store Connect → App Information (localizable) |
| **Terms of Use (EULA)** | Optional* | `https://ocoee-studios.github.io/trelka-legal/terms.html` | App Store Connect → App Information → License Agreement (custom EULA) |
| **Privacy Choices URL** | Optional | `https://ocoee-studios.github.io/trelka-legal/privacy-choices.html` | App Store Connect → App Privacy → Privacy Choices URL |

\* **Terms of Use is required if the app offers auto-renewable subscriptions.** Trelka has no in-app purchases at all, so it is optional here — Apple's standard EULA applies unless you supply this custom one. Providing it is still recommended, since the disclaimers about professional advice and outcome guarantees are meaningful for a real-estate tool.

## Notes

- **Privacy Policy URL** and **Support URL** are the two that will block submission if empty.
- The **Privacy Choices URL** field only appears in App Store Connect once you have completed the App Privacy questionnaire.
- All pages are static HTML on GitHub Pages with HTTPS enforced, so they satisfy Apple's requirement that these URLs be publicly reachable without a login.
- If a custom domain is added later (e.g. `trelka.ocoeestudios.com`), update all five fields together.
