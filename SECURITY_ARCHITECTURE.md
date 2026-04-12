# DresOS Android Defensive Security System
## Full Security Architecture

---

```
╔══════════════════════════════════════════════════════════════════╗
║              DRESOS SECURITY STACK — FULL ARCHITECTURE           ║
╚══════════════════════════════════════════════════════════════════╝

┌─────────────────────────────────────────────────────────────────┐
│  LAYER 1 — KERNEL (AFWall+)                                     │
│                                                                  │
│  AFWall+ — iptables firewall running at Linux kernel level      │
│  ├── Default-deny whitelist: all apps blocked unless approved   │
│  ├── Per-app rules: separate Wi-Fi / mobile data / VPN toggle   │
│  ├── Custom iptables: redirects mobile data HTTP/HTTPS          │
│  │   traffic → 127.0.0.1:8118 (InviZible Pro Tor proxy)        │
│  ├── Logs every blocked connection attempt                      │
│  └── PIN-locked so nothing can disable it accidentally          │
│                                                                  │
│  Cannot be bypassed by any app. Works below all other layers.   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 2 — NETWORK (InviZible Pro — Proxy + Root Mode)          │
│                                                                  │
│  DNS — DNSCrypt                                                  │
│  ├── iptables rule: ALL outbound DNS (port 53) → port 5354      │
│  ├── DNSCrypt encrypts and authenticates every DNS query        │
│  ├── DNSSEC: cryptographic validation — rejects spoofed answers │
│  ├── Resolvers: nolog + nodump + dnssec required                │
│  │   Recommended: Quad9 (Swiss non-profit) / Mullvad            │
│  │   Blocked: Cloudflare, Google DNS                            │
│  └── Your ISP cannot see any domain you visit                   │
│                                                                  │
│  Traffic Anonymisation — Tor                                     │
│  ├── Local HTTP proxy: 127.0.0.1:8118                           │
│  ├── Local SOCKS5 proxy: 127.0.0.1:9050                         │
│  ├── Three-hop onion routing: entry → middle → exit             │
│  ├── Each hop knows only previous + next — no full picture      │
│  ├── Circuit isolation: each destination = separate circuit     │
│  ├── Your IP to all websites = Tor exit node IP                 │
│  ├── Real IP: hidden. ISP IP: hidden. Location: hidden.         │
│  └── obfs4 bridges available for censored networks              │
│                                                                  │
│  Hidden Services — I2P                                          │
│  ├── Local HTTP proxy: 127.0.0.1:4444                           │
│  ├── Garlic routing: independent of Tor network                 │
│  ├── Access .i2p hidden services (eepsites)                     │
│  └── Different anonymity model — resists timing correlation     │
│                                                                  │
│  No VPN slot used. Android VPN slot remains completely free.    │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 3 — ANDROID SYSTEM PROXY                                 │
│                                                                  │
│  Wi-Fi proxy: hostname 127.0.0.1 / port 8118                   │
│  └── All apps respecting system proxy route through Tor         │
│                                                                  │
│  Mobile data: covered by AFWall+ custom iptables (Layer 1)      │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 4 — VPN SLOT (DuckDuckGo App Tracking Protection)        │
│                                                                  │
│  ├── Uses Android VPN slot (free because InviZible Pro doesn't) │
│  ├── Monitors all installed apps for tracker connections        │
│  ├── Blocks advertising, analytics, and fingerprinting trackers │
│  │   inside apps before they can phone home                     │
│  └── Runs simultaneously with InviZible Pro — no conflict       │
│                                                                  │
│  Independent of Layers 1–3. Adds app-layer tracker blocking     │
│  on top of network-level anonymity.                             │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 5 — SYSTEM WEBVIEW                                       │
│                                                                  │
│  What it is: the browser engine used by every app that displays │
│  web content internally — news apps, social media, email        │
│  clients, shopping apps, microG sign-in pages, and hundreds     │
│  more. By default this is Google's WebView, phoning home on     │
│  every render. We replace it entirely via Magisk.               │
│                                                                  │
│  PRIMARY — AOSmium (AXP.OS Project)                             │
│  ├── Chromium-based fork of Mulch (Divested Computing Group)    │
│  ├── Hardened with Vanadium patches (GrapheneOS)                │
│  ├── Google services and anti-features stripped out             │
│  ├── Installed via custom-built Magisk module ZIP               │
│  │   (AOSmium APK → module structure → flash via Magisk)        │
│  └── Appears in Developer Options → WebView implementation      │
│                                                                  │
│  BACKUP — Vanadium (GrapheneOS Project)                         │
│  ├── The WebView that ships on GrapheneOS itself                │
│  ├── GrapheneOS's full exploit mitigation suite applied         │
│  ├── Hardened memory allocator + hardened compiler flags        │
│  ├── Installed via Open WebView Magisk module v2.5.2            │
│  │   → select Vanadium during installation menu                 │
│  └── Use if AOSmium does not appear on your device              │
│                                                                  │
│  NOT USED — Mulch: EOL since Dec 2024, no more security updates │
│  NOT USED — Cromite: package name conflicts on some OEM builds  │
│                                                                  │
│  Decision flow:                                                  │
│  Flash Open WebView → select Vanadium                           │
│  Build + flash AOSmium module → reboot                          │
│  Developer Options → WebView implementation                     │
│  AOSmium visible? → select AOSmium ✓                           │
│  AOSmium not visible? → select Vanadium ✓                      │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 6 — BROWSER (DuckDuckGo Privacy Browser)                 │
│                                                                  │
│  ├── Private search by default — no user profiles               │
│  ├── Tracker blocking on every page                             │
│  ├── HTTPS upgrading — forces secure connections                │
│  ├── App Tracking Protection — enabled (uses VPN slot)          │
│  ├── Duck Address: @duck.com aliases → forward to Tuta Mail     │
│  │   └── Real email address never given to any service          │
│  ├── Built-in password manager: auto-generates strong passwords │
│  │   per site, encrypted local storage, autofill               │
│  ├── Fire Button: one tap destroys all tabs + browsing data     │
│  └── GPC (Global Privacy Control) signal sent to all sites      │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 7 — EMAIL (Tuta Mail + Duck Addresses)                   │
│                                                                  │
│  Tuta Mail                                                       │
│  ├── End-to-end encrypted: subject + body + metadata            │
│  ├── Zero-knowledge: Tuta cannot read your emails               │
│  ├── German jurisdiction (DSGVO/GDPR)                           │
│  ├── No phone number required — secured by encryption key only  │
│  └── Recovery: encryption key stored physically off-device      │
│                                                                  │
│  Duck Address (DuckDuckGo Email Protection)                     │
│  ├── Unique @duck.com alias generated per service               │
│  ├── Real Tuta address never given to any website or app        │
│  ├── DuckDuckGo strips email trackers before forwarding         │
│  ├── Any alias can be deactivated independently if compromised  │
│  └── No phone number required — secured by encryption key only  │
│                                                                  │
│  Flow:                                                           │
│  Website → Duck alias → tracker stripped → Tuta inbox           │
│  └── Real address never exposed anywhere                        │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 8 — OS BASELINE                                          │
│                                                                  │
│  Private DNS                                                     │
│  └── Quad9 DNS-over-TLS (dns.quad9.net) — fallback when        │
│      InviZible Pro is not active                                │
│                                                                  │
│  MAC Randomisation                                               │
│  ├── Randomised MAC per Wi-Fi network                           │
│  ├── Non-persistent MAC enabled in Developer Options            │
│  └── Device name broadcast disabled                             │
│                                                                  │
│  GPS Spoofing — Fake Traveler                                    │
│  ├── Mock GPS location set to anywhere in the world             │
│  └── All apps requesting location receive the fake coordinates  │
│                                                                  │
│  Google Services — Noogle microG                                │
│  ├── Full replacement for Google Play Services                  │
│  ├── Apps requiring Play Services work without Google tracking  │
│  └── Signature spoofing via LSPosed + Zygisk                   │
└─────────────────────────────────────────────────────────────────┘


╔══════════════════════════════════════════════════════════════════╗
║                    RESILIENCE MODEL                              ║
╚══════════════════════════════════════════════════════════════════╝

Every layer is independent. If one layer is temporarily
unavailable, all others continue protecting you.

  AFWall+ down?          → InviZible Pro + DDG ATP still active
  InviZible Pro down?    → AFWall+ still blocking unauthorised apps
                           Quad9 DNS-over-TLS still active as fallback
  DDG ATP down?          → InviZible Pro Tor routing still active
  Wi-Fi proxy bypassed?  → AFWall+ iptables catches it at kernel level
  WebView breached?      → Network layers contain any damage
  Email alias exposed?   → Deactivate alias, real address untouched

No single point of failure in the stack.


╔══════════════════════════════════════════════════════════════════╗
║                  WHAT EACH THREAT HITS                          ║
╚══════════════════════════════════════════════════════════════════╝

  Your real IP address        → Blocked by InviZible Pro (Tor)
  DNS surveillance            → Blocked by DNSCrypt + DNSSEC (iptables)
  In-app trackers             → Blocked by DDG App Tracking Protection
  WebView data harvesting     → Blocked by AOSmium / Vanadium
  GPS tracking                → Blocked by Fake Traveler
  Wi-Fi MAC tracking          → Blocked by MAC randomisation
  Phishing via email          → Blocked by Duck Address aliases
  Email tracker pixels        → Stripped by DuckDuckGo before delivery
  Unauthorised app internet   → Blocked by AFWall+ whitelist
  Weak/reused passwords       → Prevented by DDG password manager
  Google Play Services spying → Replaced by Noogle microG
  Malware in APKs             → Scanned by Hypatia (ClamAV)
  Censorship / Tor blocking   → Bypassed by obfs4 bridges
  IP logging links            → Scanned by URL Check before opening
```

---

**Full setup guide:** https://dresoperatingsystems.github.io/
**The DresOS Team**
