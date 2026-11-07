# 8 VPN architecture

## Current baseline (5.9.0)

The application remains an Android-native Kotlin / Jetpack Compose client. The original
5.8 source tree and its existing routes, VPN/proxy modes, split tunneling, reconnection,
network metrics, logs, boot receiver, quick-settings tile, language support and native
engine integrations are retained.

### Existing data path

```text
Android apps
  -> Android VpnService (TUN)
  -> selected TUN adapter (sing-box libbox / hev / optional tun2socks)
  -> local SOCKS5 bridge
  -> selected existing route (Aether / Psiphon / Tor)
  -> remote network
```

Proxy-only mode keeps the local SOCKS5 / optional HTTP proxy behavior. Proxy sharing is
opt-in and binds to a LAN-facing address only when explicitly enabled.

## Target 6.0 architecture

The 6.0 target is an incremental modularization, not a rewrite:

- `ConnectionManager`: the single owner of VPN lifecycle and state transitions.
- `EngineManager`: starts/stops existing engines behind a stable adapter interface.
- `ProfileRepository`: local profile persistence, import/export and provider subscriptions.
- `GatewayHealth`: bounded health probes, latency/loss measurements and freshness.
- `RoutePolicy`: deterministic route scoring, user pinning and hysteresis.
- `FailoverController`: switches only after a confirmed failure and prevents flapping.
- `DnsPolicy`: resolver configuration and DNS leak policy.
- `FirewallPolicy`: app/domain/IP rules where Android APIs and the packet path support them.
- `Diagnostics`: structured, privacy-aware local logs and metrics.
- `UpdateClient`: GitHub Releases metadata only; no silent APK installation.

## Engine ownership

Android permits only one active VPN service per user/profile. All packet engines must be
orchestrated under one `VpnService`; engines must not race to create independent TUN
interfaces. Existing Aether, Psiphon, Tor, sing-box, hev and tun2socks integrations are
kept until parity tests demonstrate a safe replacement.

Xray protocol support is intentionally deferred. It must be added only after selecting a
pinned upstream release, reviewing its license, verifying Android ABI coverage and writing
integration tests.

## Hybrid infrastructure

The client supports three source types:

1. Public gateways: user-configured or independently verified public endpoints.
2. External providers: provider subscriptions and manually imported profiles.
3. Private gateways: optional customer-operated gateways in a future phase.

No private backend is required for the Android client to start. GitHub hosts source,
CI artifacts and release metadata; it is not a VPN gateway or a live credential database.
