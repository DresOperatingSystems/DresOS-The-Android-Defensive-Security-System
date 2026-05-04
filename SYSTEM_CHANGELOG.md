# DresOS Android Defensive Security System - Changelog

## May 2026 Update

---

### File Management - Replaced ZArchiver Pro and Fossify Files with Amaze File Manager

ZArchiver Pro has been removed from the DresOS app suite entirely. It was sourced from an unofficial GitHub mirror, is not available on F-Droid, and is not fully open-source in the form distributed. Fossify Files has been removed as a separate install because it has no encryption capability.

Both are replaced by **Amaze File Manager**, available directly from F-Droid at `https://f-droid.org/packages/com.amaze.filemanager/`.

Amaze File Manager (GPL-3.0, built by Team Amaze) covers both use cases in one app:

- Full file management with cut, copy, move, delete, compress, extract across internal storage, SD card, and USB OTG
- Built-in AES-256 encryption and decryption of files and folders with .aes output files
- Biometric lock (fingerprint and face unlock) for the entire app
- Root explorer for advanced system access on rooted devices
- Built-in APK reader, installer, and App Manager for backing up or uninstalling apps
- Multiple tabs, bookmarks, search, and SMB/SSH/FTP/SFTP network share support
- No ads, no trackers, no Google dependencies, actively maintained

The file management section in Step 10 and the Part 3 app suite entry have both been updated to reflect this change.

---

### WebView - DresOS Magisk Modules Repo Now Live

The DresOS Magisk Modules repository is now live at `https://github.com/DresOperatingSystems/DresOS-Magisk-Modules`.

The AOSmium WebView module (`dresoswv`) v1.0.0 is the first release. It installs AOSmium (Chromium 147.0.7727.49, hardened with GrapheneOS/Vanadium patches) as the system WebView in a single Magisk flash. The guide now links directly to this repo rather than describing a manual build process.

What the module does:

- Validates device (Android 10+, ARM/ARM64)
- Removes data-partition updates of Chrome, Google WebView, AOSP WebView, TrichromeLibrary, and OEM WebView packages
- Systemlessly hides all competing system WebView packages via Magisk .replace files
- Installs AOSmium to system/app (or system/product/app on LineageOS) and registers via pm install
- Places a compiled RRO overlay that patches the config_webview_packages allowlist so Android accepts AOSmium as a valid WebView provider
- Writes install and activation logs to /data/adb/modules/dresoswv/ for diagnostics

After flashing: Settings -> Developer Options -> WebView implementation -> select AOSmium WebView.

---

### Security Architecture Update

The security architecture document has been updated to reflect:

- WebView layer: install path corrected to system/app (not system/priv-app)
- Threat map: added "Sensitive files on device -> AES-256 encrypted by Amaze File Manager"
---

### Magisk Modules Roadmap

The following modules are planned to automate further steps of the DresOS build:

- dresosmicrog: Noogle microG installer
- dresosdebloat: Core Google app and system bloat removal
- dresosperms: Dangerous permission revocation from system apps
- dresosafwall: AFWall+ pre-configured iptables rules
- dresosoverlay: System-level telemetry and advertising ID disabling
- dresosfossify: Fossify suite system app installer
- dresosheliboard: HeliBoard default keyboard installer
