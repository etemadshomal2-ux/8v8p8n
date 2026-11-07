# Third-party license inventory

The 5.8 README identifies these upstream components. This inventory is preliminary and
must be reconciled against the exact source revisions and binary artifacts shipped in
each release:

| Component | Upstream | License stated by 5.8 source |
|---|---|---|
| Aether | https://github.com/CluvexStudio/Aether | AGPL-3.0 |
| Psiphon tunnel core | https://github.com/Psiphon-Labs/psiphon-tunnel-core | GPL-3.0 |
| Tor | https://www.torproject.org | BSD-3-Clause |
| Lyrebird | https://gitlab.torproject.org/tpo/anti-censorship/pluggable-transports/lyrebird | BSD-3-Clause |
| hev-socks5-tunnel | https://github.com/heiher/hev-socks5-tunnel | MIT |
| tun2socks | https://github.com/xjasonlyu/tun2socks | GPL-3.0 |
| sing-box | https://github.com/SagerNet/sing-box | Verify exact release terms and additional conditions |

Before a public or commercial release, pin immutable commits/tags, archive each upstream
LICENSE and NOTICE file, generate an SBOM, and review AGPL/GPL source-distribution and
corresponding-source obligations. Do not import Hiddify, Rethink DNS, NekoBox or v2rayNG
code until the exact module, license and dependency tree have been reviewed.
