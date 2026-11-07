# 8 VPN — Android

**Repository:** https://github.com/clubapp8/8vpn  
**Current delivery:** Phase 0 + 5.9.0 baseline  
**Platform:** Android 10+ · Kotlin · Jetpack Compose · Material 3  
**Languages:** English and Persian (RTL)

## Preserved 5.8 capabilities

This repository is based on the supplied 8vpn-5.8 source archive. Existing VPN and
proxy-only modes, Aether/Psiphon/Tor routes, TUN engines, split tunneling, reconnect
behavior, ping/speed/exit-IP diagnostics, logs, boot startup, Quick Settings tile,
English/Persian UI, custom endpoints, routing options and proxy sharing remain in the
source tree. See `baseline/BASELINE.md` and the original feature documentation below.

## 5.9.0 identity

- Android application ID: `com.clubapp8.eightvpn`
- Kotlin namespace: `app.vpn8` (retained to avoid unnecessary package changes)
- Version code: `60`
- Version name: `5.9.0`
- Xray/VLESS/VMess/Trojan additions: deferred by decision; not included in 5.9.0.

Because the application ID is new, 5.9 installs as a separate app and does not update
an installed 5.8 package. The old app can remain installed alongside it.

## Build through GitHub

1. Create or open `https://github.com/clubapp8/8vpn`.
2. Upload the repository contents from this ZIP to the repository root, or push this
   directory using Git.
3. Enable **Actions** in repository settings.
4. Push to `main` or `master`, open a pull request, or run **Actions → 8 VPN Android CI**.
5. Download the `8VPN-5.9.0-build` artifact from the workflow run.

The workflow builds native dependencies (Aether, Psiphon/Lyrebird, hev and sing-box
libbox) and then assembles debug APKs. The first run may take a long time.

### Signed release

Debug APKs are for validation. To publish a signed release, create and safely back up
one persistent Android release keystore, then add these repository secrets:

- `KEYSTORE_BASE64`: base64-encoded keystore bytes
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

Never rotate or lose the key after distributing a signed production APK. A tag such as
`v5.9.0` publishes a GitHub Release; the workflow intentionally fails if the signing
secrets are missing.

## Local build

The repository intentionally uses the GitHub Actions build path because native
dependencies and `libbox.aar` are generated in CI. A plain local Gradle build requires
the matching native libraries in `app/src/main/jniLibs` and `app/libs/libbox.aar`.

## Configuration

No VPN server or backend is bundled. Users must import a valid provider profile or
configure a supported gateway. GitHub is used for source, CI and release metadata only.

## Deployment

See `.github/workflows/main.yml`. The workflow creates debug validation APKs on normal
CI runs and signed release APKs when the signing secrets are present.

## Architecture and security

- `docs/ARCHITECTURE.md` — 6.0 target architecture and engine ownership
- `docs/SECURITY.md` — secrets, network security and release gates
- `docs/TESTING.md` — regression and device test matrix
- `docs/LICENSES.md` — preliminary third-party license inventory
- `baseline/` — provenance and hashes of the supplied 5.8 source archive

## Original 5.8 documentation

The original README is preserved at `baseline/5.8-original/README.md`; screenshots and banners
remain in their original directories. The root README documents the 5.9 GitHub workflow.
