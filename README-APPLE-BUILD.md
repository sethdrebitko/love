# Apple nightly builds in your fork (arm64 only)

This workflow builds LÖVE 12 nightly for Apple platforms (arm64 only):
- macOS app zip (unsigned by default; optional signing + notarization)
- iOS Simulator app zip
- iOS device .ipa (requires signing secrets)

## Safe to use
- Putting this file in .github/workflows in your fork affects only your fork. It cannot break the upstream repo.

## How to use
1) Ensure Actions are enabled in this fork: Settings → Actions → General → Allow all actions and reusable workflows.
2) Run the workflow from the Actions tab (choose branch 12.x), or wait for the nightly cron at 03:00 UTC.

## iOS signing (.ipa)
Add these repo secrets (Settings → Secrets and variables → Actions):
- **IOS_CERT_P12_BASE64**: Base64 of your .p12 (Distribution for Ad Hoc/App Store; Developer for Development).
- **IOS_CERT_PASSWORD**: Password for the .p12.
- **IOS_PROVISIONING_PROFILE_BASE64**: Base64 of your .mobileprovision matching your bundle ID and export method.
- **APPLE_TEAM_ID**: Your Team ID (e.g., ABCDE12345).
- **IOS_BUNDLE_ID**: Your bundle ID (e.g., com.yourdomain.love12). You can also pass it as a workflow input per run.

## Optional macOS signing
- **MACOS_CERT_P12_BASE64**, **MACOS_CERT_PASSWORD**, **MACOS_SIGNING_IDENTITY** for Developer ID signing.
- **APPLE_NOTARY_KEY_ID**, **APPLE_NOTARY_ISSUER_ID**, **APPLE_NOTARY_PRIVATE_KEY_BASE64** for notarization.

## Artifacts produced
- love-macos-arm64-<sha>.zip (unsigned; signed/notarized variants if secrets provided)
- love-ios-simulator-arm64-<sha>.zip
- love-ios-arm64-<sha>.ipa (when iOS signing secrets are set)

## Troubleshooting
- **iOS signing errors**: ensure IOS_BUNDLE_ID matches the profile's App ID; profile not expired; export method matches the profile type.
- **Notarization**: ensure Developer ID Application cert and correct API key credentials.

## Need help?
- Share your desired bundle IDs and preferred export method (ad-hoc/development/app-store) and I can wire defaults into the workflow for you.