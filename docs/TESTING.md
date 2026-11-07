# Verification plan

## Phase 0 / 5.9 acceptance

- Confirm every supplied 5.8 file remains in the repository.
- Confirm app ID is `com.clubapp8.eightvpn`, version code is 60 and version name is 5.9.0.
- Confirm Kotlin namespace remains `app.vpn8`.
- Confirm GitHub updater queries `clubapp8/8vpn`.
- Confirm debug APK CI does not require release signing secrets.
- Confirm tagged release builds fail closed if release signing secrets are absent.
- Confirm no Xray dependency or protocol claim is added in 5.9.

## Regression matrix

Run on Android 10+ devices, including at least one Android 13+ device:

| Area | Required checks |
|---|---|
| VPN mode | Connect, disconnect, revoke permission, reconnect |
| Proxy-only | SOCKS5 and optional HTTP listener; local-only default |
| Routes | Aether, Psiphon, Tor and supported route combinations |
| TUN | sing-box, hev and available fallback |
| Split tunnel | Include and exclude app lists |
| Network changes | Wi-Fi/mobile transitions and captive network behavior |
| Recovery | Core crash, gateway timeout, repeated failed probes |
| Telemetry | Ping, transfer rates, exit IP and logs |
| Localization | English, Persian, RTL and dark/light themes |
| Startup | Boot receiver and Quick Settings tile |
| Sharing | Explicit LAN proxy sharing, hotspot and USB tethering per device |
| Security | DNS/IPv6 leaks, kill switch, listener exposure and log redaction |

A successful CI build is not a substitute for device-level VPN and leak testing.
