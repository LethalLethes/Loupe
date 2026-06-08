# How to build the Loupe IPA with GitHub Actions

## Step 1 — Fork the Loupe repo

Go to https://github.com/mysk-research/loupe and click **Fork**.

## Step 2 — Add these 6 secrets to your forked repo

Go to your repo → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

| Secret name | How to get it |
|---|---|
| `SIGNING_CERT_BASE64` | On your Mac: open **Keychain Access**, find your *Apple Distribution* certificate, right-click → Export → save as `.p12` with a password, then run `base64 -i MyCert.p12 \| pbcopy` and paste |
| `SIGNING_CERT_PASSWORD` | The password you chose when exporting the `.p12` above |
| `KEYCHAIN_PASSWORD` | Any random password, e.g. `MyBuildKeychain123` |
| `PROVISIONING_PROFILE_BASE64` | On [developer.apple.com](https://developer.apple.com) → Certificates, IDs & Profiles → create a **Distribution** profile → download `.mobileprovision` → run `base64 -i Loupe.mobileprovision \| pbcopy` |
| `DEVELOPMENT_TEAM` | Your **Team ID** — find it at developer.apple.com → Account → Membership → Team ID (looks like `AB12CD34EF`) |
| `BUNDLE_ID` | The Bundle Identifier you registered, e.g. `com.yourname.loupe` |

## Step 3 — Add the workflow file

Copy `build-loupe-ipa.yml` into `.github/workflows/` in your forked repo.

## Step 4 — Push or trigger manually

Either push a commit to `main`, or go to **Actions** → **Build Loupe IPA** → **Run workflow**.

## Step 5 — Download the IPA

When the workflow finishes, go to **Actions** → click the run → scroll down to **Artifacts** → download `Loupe-N.ipa`.

## Requirements checklist

- [ ] Paid Apple Developer account ($99/year)
- [ ] App ID registered at developer.apple.com
- [ ] Distribution certificate in your Keychain
- [ ] Distribution provisioning profile downloaded

## Optional: send directly to TestFlight

Uncomment the last step in the workflow and add three more secrets:
- `APP_STORE_CONNECT_KEY_ID`
- `APP_STORE_CONNECT_ISSUER_ID`
- `APP_STORE_CONNECT_KEY_BASE64`

Get these from App Store Connect → Users and Access → Integrations → App Store Connect API.
