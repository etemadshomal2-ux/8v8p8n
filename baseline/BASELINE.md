# 8 VPN 5.8 baseline preservation

The supplied `8vpn-5.8.zip` was extracted as the starting source tree for this repository.
All files from the archive are retained in the active repository, including the `8vpn-fix5`,
`backup-old-ui`, banners, screenshots, native build inputs, Kotlin sources and license.

The SHA-256 inventory in `8vpn-5.8-SHA256SUMS.txt` records the exact original bytes from
the supplied archive. The following intentional 5.9 identity changes are applied to the
active source tree:

- `app/build.gradle.kts`: application ID changed to `com.clubapp8.eightvpn`,
  version code 60, version name 5.9.0.
- `app/src/main/java/app/vpn8/Updater.kt` and `OtherScreens.kt`: GitHub release and
  repository links changed to `clubapp8/8vpn`.
- `.github/workflows/main.yml`: CI now always produces debug validation APKs;
  signed release APKs require a persistent keystore supplied through GitHub Secrets.

The original Kotlin namespace `app.vpn8` is retained to avoid unnecessary source/package
renames. The new application ID intentionally makes 5.9 a separate Android installation
from 5.8; it cannot update the old package in place.
