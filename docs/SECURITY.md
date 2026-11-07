# Security policy and implementation requirements

## Secrets

- Never commit keystores, passwords, provider tokens, private keys or production profiles.
- Store release signing values as GitHub Actions repository secrets:
  `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`.
- Keep one stable release keystore in secure offline backup. Losing it prevents updates
  to installations signed with that key.
- Public gateway lists and provider URLs are untrusted input; validate schemes, hosts,
  ports, certificates and response sizes before use.

## Android networking

- Keep proxy listeners on loopback unless the user explicitly enables LAN sharing.
- When LAN sharing is enabled, display the bind address and warn that connected devices
  may access the proxy; require authentication before exposing a proxy on untrusted LANs.
- Do not claim hotspot/USB tether traffic is routed through the VPN unless device-level
  tests prove it for that Android version and OEM.
- Use `VpnService.protect()` for sockets that must reach the remote gateway outside the
  VPN tunnel.
- Apply split-tunnel rules through Android's VpnService.Builder and verify include/exclude
  behavior for every supported Android release.
- Do not log credentials, full subscription URLs, private keys or sensitive payloads.

## Release gates

- Validate AndroidManifest permissions and exported components.
- Run dependency and license inventory for every native and JVM dependency.
- Run static checks for SQL injection, XSS, CSRF, RCE, SSRF and embedded secrets where
  applicable. For this client, SSRF-like risks primarily concern untrusted subscription
  URLs, redirects and local proxy exposure.
- Test DNS and IPv6 leak behavior, kill-switch semantics, reconnect and engine crash
  recovery on physical devices.
- Do not publish a signed release until the persistent signing key is configured.
