# DresOS-The-Android-Defensive-Security-System
**A Complete Rooted DeGoogling + Operational Security Guide**
**TWRP + Magisk + MicroG + Fossify + iVizblePro + DresOS App Suite – For 2026**

---

> **Project Goal:** Turn any stock Android phone into a fully private, hardened, FOSS-only device with no Google tracking, no Google Services, no hidden data harvesting, and only open-source replacements — then layer on a full defensive security stack to protect against surveillance, malware, censorship, and network-level attacks.
>
> **Why:** Because of all the restrictions Google is bringing into place over the open-source communities, to bring you back your privacy, to stop your data being sold, and to give you full operational security on a device you actually control.

---

## ⚠️ EXTREME WARNING

Rooting and flashing can **brick** your device, void your warranty, trip Knox/SafetyNet, and wipe all data.
**Back up everything** (photos, apps, files) before starting.
This is advanced — if you're not comfortable with ADB/fastboot or device-specific guides, stop and use a non-root method.
Proceed at your own risk.

**Make a full TWRP backup after rooting** (Boot + System + Data + Vendor) before any debloating.

---

## Table of Contents

### Part 1 — DeGoogling (Full Root Method)

* [What You Will Need](#what-you-will-need)
* [Replacement Overview](#replacement-overview)
* [Step 1: Unlock the Bootloader](#step-1-unlock-the-bootloader)
* [Step 2: Install TWRP](#step-2-install-twrp)
* [Step 3: Install Magisk](#step-3-install-magisk)
* [Step 4: Install Core FOSS Apps](#step-4-install-core-foss-apps)
* [Step 5: Install Magisk Modules](#step-5-install-magisk-modules)
* [Step 6: Set Up Noogle microG](#step-6-set-up-noogle-microg)
* [Step 7: Change System WebView to AOSmium](#step-7-change-system-webview-to-aosmium)
* [Step 8: Set Up Shizuku](#step-8-set-up-shizuku)
* [Step 9: Fine-Tune Debloat & Cleanup](#step-9-fine-tune-debloat--cleanup)
* [Step 10: Replace System File Manager, Package Installer & Download Manager](#step-10-replace-system-file-manager-package-installer--download-manager)
* [Step 11: Final Setup & Defaults](#step-11-final-setup--defaults)
* [Step 12: Test & Backup](#step-12-test--backup)

### Part 2 — Operational Security (OPSEC Stack)

* [OPSEC Overview](#opsec-overview)
* [OPSEC Step 1: Configure DNS and MAC Randomization](#opsec-step-1-configure-dns-and-mac-randomization)
* [OPSEC Step 2: Set Up iVizblePro — Your All-in-One Privacy Engine](#opsec-step-2-set-up-ivizplepro--your-all-in-one-privacy-engine)
* [OPSEC Step 3: Set Up Secure Email with Tuta](#opsec-step-3-set-up-secure-email-with-tuta)
* [OPSEC Step 4: Spoof Location with Fake Traveler](#opsec-step-4-spoof-location-with-fake-traveler)
* [OPSEC Step 5: Final Checks and Hardening Tips](#opsec-step-5-final-checks-and-hardening-tips)

### Part 3 — DresOS Defensive App Suite

* [Apps Overview](#apps-overview)
* [ZArchiver Pro](#1-zarchiver-pro--file-manager--aes-encryption)
* [IYPS](#2-iyps--password-strength-analyser--generator)
* [RedReader](#3-redreader--private-reddit-client)
* [URL Check](#4-url-check--link-scanner)
* [Hypatia](#5-hypatia--open-source-antivirus)
* [OONI Probe](#6-ooni-probe--network-censorship-detector)
* [iVizblePro](#7-ivizplepro--all-in-one-proxy-firewall--vpn)
* [Metrolist](#8-metrolist--private-youtube-music-client)
* [Arcane Chat](#9-arcane-chat--decentralized-encrypted-messaging)
* [Aurora Store](#10-aurora-store--anonymous-app-store)
* [Fossify Suite](#11-fossify-suite--complete-foss-system-apps)
* [HeliBoard](#12-heliboard--offline-keyboard)
* [Tuta Mail](#13-tuta-mail--encrypted-email)
* [AOSmium Browser](#14-aosmium-browser--privacy-first-web-browser)

### Appendix

* [Compatible Devices](#compatible-devices)
* [Contact DresOS](#contact-dresoS)

---

---

# PART 1 — DEGOOGLING

## What You Will Need

Download **only** from these official links (2026). Install **F-Droid** first — it is the backbone of your FOSS ecosystem.

| Tool | Purpose | Link |
|---|---|---|
| **F-Droid** | Main FOSS app store | [Download APK](https://f-droid.org/F-Droid.apk) / [Site](https://f-droid.org/) |
| **Inure App Manager** | Debloat + app management | [GitHub Releases](https://github.com/Hamza417/Inure/releases) |
| **Shizuku** | Root-like advanced system permissions | [GitHub Releases](https://github.com/RikkaApps/Shizuku/releases) |
| **TWRP** | Custom recovery (full backups + flashing) | [twrp.me](https://twrp.me/) → search your exact device model |
| **Magisk** | Root + module framework | [GitHub Releases](https://github.com/topjohnwu/Magisk/releases) |
| **De-Bloater** | Fine-tune system app removal | [F-Droid](https://f-droid.org/packages/com.sunilpaulmathew.debloater/) / [GitHub](https://github.com/sunilpaulmathew/De-Bloater) |
| **Noogle microG** | Magisk module — replaces Google Play Services | [GitHub Releases](https://github.com/SelfRef/noogle-magisk/releases) |
| **LSPosed** | Advanced Xposed-style module framework | [GitHub Releases](https://github.com/LSPosed/LSPosed/releases) |
| **Open WebView** | Magisk module — makes WebView switching permanent | [GitHub](https://github.com/Magisk-Modules-Alt-Repo/open_webview) |
| **SD Maid SE** | Deep system cleaner + remnant finder | [F-Droid](https://f-droid.org/packages/eu.darken.sdmse/) |
| **Fossify Suite** | Phone, Messages, Gallery, Calendar, Files, Launcher, Contacts, Music | [fossify.org/apps](https://www.fossify.org/apps/) (all via F-Droid) |
| **AOSmium** | System WebView only (replaces Google's Android System WebView) | [AXP.OS F-Droid Repo](https://axpos.org/F-Droid) / [Manual Releases](https://codeberg.org/AXP-OS/app_aosmium/releases) |
| **DuckDuckGo Privacy Browser** | Primary browser (Chrome replacement) | [F-Droid](https://f-droid.org/packages/com.duckduckgo.mobile.android/) |
| **Aurora Store** | Anonymous Play Store alternative | [F-Droid](https://f-droid.org/packages/com.aurora.store/) |
| **HeliBoard** | Fully offline keyboard (no Gboard) | [F-Droid](https://f-droid.org/packages/helium314.keyboard/) |
| **Tuta Mail** | End-to-end encrypted email (no Gmail) | [F-Droid](https://f-droid.org/packages/de.tutao.tutanota/) |
| **Download Navi** | FOSS download manager (no Google Downloads) | [F-Droid](https://f-droid.org/packages/com.tachibana.downloader/) |
| **SAI** | Split APK Installer — FOSS package installer | [F-Droid](https://f-droid.org/packages/com.aefyr.sai.fdroid/) |
| **Fake Traveler** | GPS location spoofer | [F-Droid](https://f-droid.org/repo/cl.coders.faketraveler_222.apk) |

---

## Replacement Overview

Here is exactly what each core app replaces and why it is better for privacy:

| App | Replaces | Why It's Better |
|---|---|---|
| Fossify Phone | Stock Phone / Dialer | Fully open source, zero telemetry |
| Fossify Messages | Stock SMS | Privacy-first, no Google tracking |
| Fossify Files | Google Files / Stock File Manager | Open source, no cloud sync, no telemetry |
| DuckDuckGo Privacy Browser | Chrome | Private search engine, tracker blocking, zero Google telemetry |
| AOSmium WebView | Android System WebView (Google) | Blocks ads & trackers in **every** app that loads web content |
| Tuta Mail | Gmail | End-to-end encrypted email (no Google account or content scanning) |
| HeliBoard | Gboard | Completely offline keyboard, no data sent anywhere, ever |
| Aurora Store | Google Play Store | Anonymous downloads, no Google account required |
| Noogle microG | Google Play Services | Full app compatibility without any Google tracking infrastructure |
| Fossify Gallery / Calendar / Launcher / Contacts / Music | Stock Google equivalents | All open source, no cloud sync or telemetry |
| Download Navi | Google Download Manager | FOSS download manager, zero Google components |
| SAI (Split APK Installer) | Google Package Installer | FOSS installer with signature verification, no Google calls home |
| iVizblePro | Orbot + VPN apps + DNS apps + Firewall apps | Single app combining Tor, I2P, DNSCrypt, and firewall — uses Android VPN slot directly |

---

## Step 1: Unlock the Bootloader

**Device-specific** — required for TWRP + Magisk. Usually wipes all data.

1. Enable **Developer Options**: Settings → About phone → tap **Build number** 7 times.
2. Turn on **OEM unlocking** + **USB debugging**.
3. Install ADB & Fastboot on your PC (Android Platform Tools from Android Developers).
4. Connect phone via USB.
5. Run: `adb reboot bootloader`
6. Run: `fastboot flashing unlock` (or `fastboot oem unlock` on older devices).
7. Confirm on phone screen — **this will factory reset the device**.

**Samsung:** Use Download Mode + Odin with official or unofficial unlock.
**Huawei / carrier-locked phones:** Use the official unlock code process for your carrier.
**Exact instructions:** Search `[your exact model] unlock bootloader XDA Developers` and follow **that** device's specific guide.

Phone will factory reset. Set it up again and re-enable USB debugging before continuing.

---

## Step 2: Install TWRP (Custom Recovery)

TWRP gives you full device backups and easy module/zip flashing.

1. Go to [twrp.me](https://twrp.me/) and search your **exact** device model and variant.
2. Download the latest `.img` (and `.zip` if available).
3. Follow the **exact instructions** on that device's TWRP page — they are device-specific.

Typical commands:

```
adb reboot bootloader
fastboot boot twrp-xxxx.img           # Temporary boot into TWRP
# Inside TWRP: Install → select TWRP .zip to make it permanent
# Or: Advanced → Install Recovery Ramdisk
```

Reboot to recovery to confirm TWRP is permanently installed.

**No TWRP for your device?** Use Magisk direct patching method only (see Step 3 below) or check XDA for unofficial TWRP builds. Search `[model] unofficial TWRP`.

---

## Step 3: Install Magisk (Root)

Two methods — pick one based on your situation.

### Recommended: Magisk Patching Method (works on almost everything)

1. Download the latest Magisk APK from GitHub.
2. Extract your device's `boot.img` (or `init_boot.img`) from the stock firmware ZIP for your exact model and Android version.
3. Install the Magisk app on your phone.
4. Open Magisk app → **Install** → **Select and Patch a File** → choose `boot.img`.
5. `magisk_patched_xxxx.img` will appear in your Downloads folder.
6. Pull it to your PC: `adb pull /sdcard/Download/magisk_patched_xxxx.img`
7. `adb reboot bootloader`
8. `fastboot flash boot magisk_patched_xxxx.img` (or `init_boot` if your device uses it).
9. On some devices you also need to flash a patched `vbmeta.img` with flags: `fastboot flash vbmeta vbmeta.img --disable-verity --disable-verification`
10. Reboot. Open Magisk app — it should show "Installed."

### Alternative: Via TWRP

1. Rename the Magisk APK file from `.apk` to `.zip`
2. Boot to TWRP → Install → select and flash the `.zip`
3. Reboot system

**Samsung-specific:** Use Recovery mode + Odin with a patched AP.tar file.

Reboot → open Magisk app → you are rooted. Keep Magisk app installed — you need it for everything that follows.

---

## Step 4: Install Core FOSS Apps

1. Transfer the **F-Droid APK** to your phone and install it (allow installs from unknown sources when prompted).
2. Open F-Droid and from the search/browse install **all** of these:
   * **Inure App Manager**
   * **Shizuku**
   * **SD Maid SE**
   * **All Fossify apps** (Phone, Messages, Gallery, Calendar, Files, Launcher, Contacts, Music)
   * **HeliBoard**
   * **DuckDuckGo Privacy Browser**
   * **Aurora Store**
   * **Tuta Mail**
   * **Download Navi**
   * **SAI (Split APK Installer)**
   * **Fake Traveler**
3. Add the **AXP.OS F-Droid repo** to install AOSmium (see Step 7 for details).

Do **not** open or configure these apps yet — follow each step in order.

---

## Step 5: Install Magisk Modules

Open **Magisk app** → **Modules** → **Install from storage** and flash each of these one at a time, rebooting between them if instructed:

1. **Noogle microG** — replaces Google Play Services
2. **LSPosed** — advanced Xposed module framework (Zygisk version)
3. **Open WebView** — makes third-party WebView switching permanent across reboots

Reboot after flashing all three.

---

## Step 6: Set Up Noogle microG (Replaces Google Services)

Noogle microG is a Magisk module that installs a clean, privacy-respecting replacement for Google Play Services. Apps that require Play Services (push notifications, maps, logins) will work through microG with zero Google data harvesting.

1. Open **Magisk** → tap the action button on Noogle microG → grant root permissions.
2. Open the **microG Settings** app (should appear in your app drawer after reboot).
3. Go to **Self Check** → work through every unticked item until all show green/ticked.
4. **Signature spoofing** must say "OK" — this is handled by LSPosed + Zygisk automatically.
5. microG is now active. Apps that previously needed Google Play Services will route through it.

**Note:** If the Self Check still shows issues after LSPosed is installed, reboot once more. If microG fails entirely, try uninstalling the LSPosed module from Magisk and retrying — some devices have compatibility quirks.

---

## Step 7: Change System WebView to AOSmium

### What is the System WebView?

The **Android System WebView** is a browser engine embedded into the Android OS itself. It is not just for your browser — it is used by hundreds of apps (Facebook, Amazon, Spotify, Slack, CNN apps, microG sign-in pages, email apps, and countless others) any time they need to display web content within the app. By default this is Google's WebView, which phones home to Google for every piece of web content any app renders.

**AOSmium** is the WebView built by the [AXP.OS Project](https://axpos.org/). It is a Chromium-based fork of Mulch (by Divested Computing Group), hardened with Vanadium's (GrapheneOS) security patches, with Google services and anti-features minimized. Replacing the system WebView with AOSmium means that **every single app** on your phone that renders web content does so through a privacy-hardened, Google-free engine — not just your browser.

**AOSmium is the System WebView only.** Your primary browser is **DuckDuckGo Privacy Browser** (installed in Step 4). Keep DuckDuckGo's **App Tracking Protection feature turned OFF** — that feature uses the Android VPN slot, which iVizblePro (your full privacy engine, covered in Part 2) requires exclusively. The DuckDuckGo browser itself works perfectly without that feature enabled — iVizblePro already handles all traffic-level privacy for every app system-wide.

### Installation

**Method 1 — Via AXP.OS F-Droid Repo (Recommended — auto-updates):**

1. Open **F-Droid** → **Settings** → **Repositories** → tap the **+** button.
2. Add the AXP.OS repo URL from [axpos.org/F-Droid](https://axpos.org/F-Droid).
3. Update F-Droid repo list.
4. Search for **AOSmium** → install it.

**Method 2 — Manual APK:**

1. Go to [codeberg.org/AXP-OS/app_aosmium/releases](https://codeberg.org/AXP-OS/app_aosmium/releases).
2. Download the latest release APK for your architecture (arm64 for most modern devices).
3. Install via **SAI** (Split APK Installer) — the FOSS package installer you installed in Step 4.

### Activating AOSmium as System WebView

1. Go to **Settings → System → Developer Options**.
   * (If Developer Options is not visible: Settings → About phone → tap Build number 7 times.)
2. Scroll to **WebView implementation** → tap it → select **AOSmium**.
3. Reboot.

**If AOSmium does not appear in the WebView list:**

* The **Open WebView** Magisk module (installed in Step 5) should resolve this automatically by unlocking the WebView selection system.
* If it still does not appear, search for your specific device and Android version with the query `[model] change system webview third party` on XDA.

**Test it:** Open Aurora Store or any news app — web content rendered inside apps should now have tracking and ad elements blocked at the WebView level.

---

## Step 8: Set Up Shizuku

Shizuku gives apps like **Inure App Manager** powerful system-level access — specifically the ability to deeply debloat and manage system apps — without requiring every individual operation to go through a full root prompt. It is safer, more granular, and lighter than running everything root, and it works perfectly alongside your existing Magisk root.

### Why Use Shizuku?

* Lets Inure and other tools debloat safely and deeply at the system level.
* Survives reboots when configured correctly.
* Uses Android's ADB-equivalent permission layer — no need to expose full root for every operation.
* Works with several other FOSS tools that support it.

### Step-by-Step Root Setup (Recommended — Device Already Rooted)

1. Open the **Shizuku** app.
2. When Magisk prompts for root permission, grant it to Shizuku **permanently**.
3. On the main Shizuku screen where it shows the root option, tap **Start** (the big button).
4. You will briefly see a black screen with white text confirming the service has started.
5. Go to **Shizuku settings** → enable **Auto start on boot** and **Keep alive**.

### Grant Permissions to Apps

* When you open **Inure App Manager** for the first time it will automatically request Shizuku access — approve it and grant **all** requested permissions.
* You can view and manage all apps that have been granted Shizuku access under Shizuku → **Authorized apps**.

**Test:** Reboot your phone. Open Shizuku — it should auto-start and show "Running" with root status. If it shows "Not running," open Shizuku and tap Start again.

You are now ready for the deepest, safest debloating possible.

---

## Step 9: Fine-Tune Debloat & Cleanup

Now we remove every trace of Google and system bloat safely.

### 9.1 Inure App Manager (Recommended Bulk Removal)

1. Open **Inure App Manager**.
2. Grant it **full access** — choose **Root** and **Shizuku**. Approve **everything** it asks for.
3. Go to the **Debloat** tab.
4. Tap the **select all** icon.
5. Select the **Recommended** debloat list.
6. This automatically selects everything your device does not need: Google bloat, carrier apps, unused system services, etc.
7. Review the list carefully. Uncheck anything you want to keep. Then tap **Debloat** to remove everything.
8. Restart the phone.

> **Note:** If Inure looks like it is doing nothing after you tap Debloat — leave it running. It is digging through your system to safely remove everything. This can take several minutes.

### 9.2 De-Bloater App (Fine-Tuning Pass)

1. Open the **De-Bloater** app (it will detect Magisk root automatically).
2. Scan system apps.
3. Remove **all** remaining Google system apps, including:
   * Gmail
   * Google Search
   * Chrome
   * Google Play Services remnants (anything not replaced by microG)
   * Any other carrier or OEM bloat
4. Apply changes and reboot.

### ⚠️ CRITICAL WARNING

You **must** have installed all replacement apps **before** removing their Google equivalents. Specifically:
* Install **Tuta Mail** before removing Gmail
* Install **Fossify Phone** before removing the stock dialer
* Install **Fossify Messages** before removing the stock SMS app
* Install **AOSmium** before removing Chrome and the Google WebView
* Install **Download Navi** before removing Google Download Manager
* Install **SAI** before removing the Google Package Installer

Removing a system app without a replacement can break core phone functions until you restore a TWRP backup.

### 9.3 Final Cleanup with SD Maid SE

Open **SD Maid SE** → run **Full Scan** + **CorpseFinder** → delete every Google remnant, leftover data folder, and orphaned system file.

---

## Step 10: Replace System File Manager, Package Installer & Download Manager

A truly de-Googled phone requires replacing not just apps but the system-level utilities Google embeds for file management, app installation, and downloading. Here is the full FOSS replacement stack — zero Google components:

### File Management: Fossify Files

**Fossify Files** is already included in the Fossify suite you installed in Step 4. It is a direct open-source replacement for Google Files (Files by Google). It provides:

* Full local file browsing (internal storage and SD card)
* Copy, move, delete, rename, compress operations
* Support for ZIP archives
* No cloud sync, no analytics, no Google dependencies whatsoever
* Completely offline and self-contained

Set **Fossify Files** as your default file manager in Settings → Apps → Default apps.

For **encrypted archiving, AES-encrypted backups, and powerful archive management**, use **ZArchiver Pro** from the DresOS app suite (covered in Part 3). These two work together: Fossify Files for everyday browsing, ZArchiver Pro for anything requiring encryption or complex archive formats.

### Package Installer: SAI (Split APK Installer)

**SAI** (Split APK Installer) is a fully open-source replacement for Google's PackageInstaller. It supports:

* Standard APK installation
* Split APK packages (.apks / .xapk files) — the format many apps use
* APK signature verification before installing
* Batch installation from ZIP archives
* Root and Shizuku installation modes for seamless installs without confirmation prompts
* Zero Google components, zero network calls home

Install from F-Droid: `https://f-droid.org/packages/com.aefyr.sai.fdroid/`

Set SAI as the default app opener for `.apk` files in Settings → Apps → Default apps → Opening links, or by long-pressing an APK in Fossify Files and selecting SAI.

### Download Manager: Download Navi

**Download Navi** is a fully open-source download manager — a complete replacement for Google's hidden Download Manager service that normally handles all file downloads on Android. It provides:

* Parallel and resumable downloads
* Browser integration (set as default download handler)
* File hash verification (MD5/SHA-256) to confirm download integrity
* Support for batch downloads and download queues
* A clean, modern interface
* Zero Google dependencies — it does not call home anywhere

Install from F-Droid: `https://f-droid.org/packages/com.tachibana.downloader/`

After installing, go to **Settings → Apps → Default apps → Opening links** and make sure Download Navi handles download intents. In **AOSmium browser**, go to Settings and set Download Navi as the external download manager if prompted.

> **Why This Matters:** Google's Download Manager is a hidden background service that most users never interact with directly — but it silently handles every file download on the phone and can report metadata to Google. Download Navi replaces it entirely with zero tracking.

### APK Manager: F-Droid + Aurora Store

For sourcing and updating apps:

* **F-Droid** handles all open-source apps from its repository and any added repos (like AXP.OS for AOSmium). F-Droid verifies all APK signatures against developer keys.
* **Aurora Store** provides anonymous access to the Google Play Store catalogue without a Google account. Use **Anonymous** login mode only.

Together, these two replace the Google Play Store ecosystem completely.

---

## Step 11: Final Setup & Defaults

Go to **Settings → Apps → Default apps** and set:

| Function | Default App |
|---|---|
| Browser | **DuckDuckGo Privacy Browser** |
| Keyboard / Input method | **HeliBoard** |
| Home / Launcher | **Fossify Launcher** |
| Phone app | **Fossify Phone** |
| SMS / Messages | **Fossify Messages** |
| Email | **Tuta Mail** (also set for `mailto:` links) |
| File manager | **Fossify Files** |
| Package installer | **SAI** |
| Download manager | **Download Navi** |

**Aurora Store:** Open it → Settings → set **Anonymous** login mode. Do not log in with any Google account.

**DuckDuckGo Privacy Browser:** Open it and complete initial setup. **Do NOT enable App Tracking Protection** — that feature uses the Android VPN slot, which iVizblePro requires exclusively. The browser works perfectly without it; iVizblePro already handles all traffic-level privacy for the entire device system-wide.

**LSPosed modules (optional hardening):**
* **Hide My Applist** — prevents apps from detecting other apps installed on your phone
* **Play Integrity Fix** — helps microG pass SafetyNet/Play Integrity checks for apps that require it

---

## Step 12: Test & Backup

* Make and receive a test phone call via **Fossify Phone**
* Send and receive a test SMS via **Fossify Messages**
* Send and receive a test email via **Tuta Mail**
* Open a website in **DuckDuckGo Privacy Browser** — confirm it is working and App Tracking Protection is off
* Open **Aurora Store** — verify apps load and anonymous mode works
* Open an APK via **SAI** — confirm it installs correctly
* Download a file in **DuckDuckGo** — confirm it opens in **Download Navi**
* Everything working through microG and AOSmium WebView as expected

**TWRP Backup (if not done already):** Boot to TWRP → Backup → select Boot + System + Data + Vendor → swipe to back up. This is your emergency restore point. Store the backup folder in a safe location off-device.

**If anything breaks:** Boot to TWRP → Restore → select your backup → swipe. Your full system is back in minutes.

---

---

# PART 2 — OPERATIONAL SECURITY (OPSEC STACK)

## OPSEC Overview

This repository provides a guide to enhancing operational security (OPSEC) and cybersecurity on Android devices. It focuses on protecting against phishing, malware, IP tracking, data mining, device fingerprinting, censorship detection, and network surveillance — using free, open-source tools only.

This method creates a layered privacy setup: encrypted DNS at the OS level, Tor + I2P routing + DNSCrypt + firewall at the network level (all via a single app), and location spoofing at the sensor level. The result is an extremely hardened device suitable for privacy-conscious individuals who previously relied on paid VPNs, Cloudflare DNS, or Google DNS.

**Compatibility:** Android 10 or later. The degoogling steps in Part 1 are recommended but most OPSEC steps work on stock Android too.

> **VPN Slot Note:** Android only allows one VPN-mode app to run at a time. **iVizblePro** (InviZible Pro) requires exclusive use of the Android VPN slot to provide Tor + I2P + DNSCrypt + Firewall. **DuckDuckGo's App Tracking Protection feature** also uses the VPN slot — keep it turned OFF. The DuckDuckGo browser itself (without App Tracking Protection) works perfectly alongside iVizblePro, as iVizblePro already handles all traffic-level privacy for every app on the device.

---

## OPSEC Step 1: Configure DNS and MAC Randomization

This is the baseline privacy layer — applied at the OS level, before any apps run.

### DNS over TLS (Quad9)

1. Go to **Settings → Network & Internet → Private DNS**.
2. Select **Private DNS provider hostname**.
3. Enter: `dns.quad9.net`
4. Save.

**What this does:** Quad9 DNS blocks malicious domains, protects against malware and phishing at the DNS resolution level, and does not log or collect user data — unlike Google DNS (8.8.8.8) or Cloudflare DNS (1.1.1.1) which both log queries. Quad9 is operated by a Swiss nonprofit. All DNS queries are now encrypted via DNS-over-TLS and filtered against Quad9's threat intelligence database.

> Note: Once iVizblePro is running in VPN mode (Step 2), it takes over DNS resolution entirely via DNSCrypt, which is even more private than system-level DNS-over-TLS. The Quad9 setting here serves as a fallback for when iVizblePro is not active.

### MAC Address Randomization

1. Go to **Settings → Network & Internet → Internet** → tap your Wi-Fi network.
2. Tap **Network usage** → set to **Treat as unmetered** (reduces certain monitoring behaviors).
3. Go to **Privacy** (within the same network settings).
4. Enable **Use randomized MAC address**.
5. Disable **Send device name**.

**What this does:** Every Wi-Fi device has a hardware MAC address that uniquely identifies it. By default, this allows any network operator to track your device across time even if you change your IP. Randomized MAC changes your device's hardware identifier on each network, preventing this form of persistent tracking. Your device might appear as a completely random hardware identifier — preventing physical location tracking via Wi-Fi network logs.

### Developer Options Hardening

1. Go to **Settings → About phone** → tap **Build number** seven times to unlock Developer Options.
2. In **Developer options**:
   * Enable **Non-persistent MAC** (complements the randomization above across reboots)
   * Enable **Tethering hardware acceleration** (improves performance when hotspot is used)

---

## OPSEC Step 2: Set Up iVizblePro — Your All-in-One Privacy Engine

**iVizblePro** (InviZible Pro) is the centerpiece of the DresOS OPSEC stack. It is a single application that combines **Tor**, **I2P**, **DNSCrypt**, and a **built-in firewall** — all operating together through the Android VPN interface. It replaces what would otherwise require four separate apps (Orbot for Tor, a separate I2P client, a separate DNSCrypt resolver, and a separate firewall app), and it does this without root requirements (though root is supported for enhanced firewall control on rooted devices like yours).

**Download:** `https://f-droid.org/repo/pan.alexander.tordnscrypt.stable_26603.apk`

Or search **InviZible Pro** in F-Droid directly.

### What Each Component Does

**DNSCrypt:**
DNS (Domain Name System) is the phone book of the internet — it converts domain names (like `example.com`) into IP addresses. Normally this happens in plain text, letting your ISP, network operator, and any intermediary see every domain you visit. DNSCrypt encrypts and authenticates these DNS queries so that:
* Your ISP cannot see what domains you are looking up
* Your queries cannot be tampered with or redirected (DNS spoofing / MITM attacks)
* You can use a privacy-respecting DNS resolver of your choice

**Tor (The Onion Router):**
Tor routes your internet traffic through a network of volunteer-operated relays (typically three: entry guard, middle relay, exit node). Each relay only knows the previous and next hop — no single relay knows both who you are and what you are accessing. This provides:
* Strong anonymity against network-level surveillance
* Bypass of censorship and geo-blocks
* Protection against your ISP logging your traffic
* Access to `.onion` hidden services

**I2P (Invisible Internet Project):**
I2P is a separate anonymizing network layer, distinct from Tor, that uses a garlic routing protocol (bundling multiple messages together). It is particularly suited for:
* Anonymous peer-to-peer communication
* Accessing I2P-specific hidden services (eepsites)
* Additional anonymity layer when combined with Tor
* Resistant to timing correlation attacks in different ways than Tor

**Built-in Firewall (iptables / nftables):**
On rooted devices, iVizblePro can control iptables/nftables directly to:
* Block specific apps from accessing the internet entirely
* Force specific apps to route only through Tor or I2P
* Block all traffic that is not routed through the privacy tunnels (kill switch behavior)
* Prevent data leaks if Tor or DNSCrypt temporarily drops

### Full Setup: VPN Mode with Tor + I2P + DNSCrypt + Firewall

Follow these steps exactly, in order:

#### Phase 1: Initial Configuration

1. Install iVizblePro via F-Droid using the link above.
2. Open iVizblePro.
3. On first launch, allow any permission prompts (notifications, etc.).
4. **Do not tap Start yet.** Configure everything first.

#### Phase 2: Configure DNSCrypt

1. Tap the **DNSCrypt** tab at the bottom.
2. Tap the **settings gear** icon for DNSCrypt.
3. Under **Servers**, tap **DNS servers** → review the list. The app comes with a curated list of privacy-respecting resolvers. Good defaults include:
   * `quad9-dnscrypt-ip4-filter-pri` (Quad9 with malware filtering)
   * `cloudflare` (fast, but logs) — **avoid this one**
   * `mullvad-adblock-doh` or any resolver marked with `nolog nofilter`
4. Select at least one `nolog` resolver. Multiple can be active for redundancy.
5. Under **DNSCrypt settings**:
   * Enable **DNSSEC** (cryptographic validation of DNS responses)
   * Enable **Block IPv6** if you do not use IPv6 (reduces attack surface)
   * Enable **Require DNSSEC** for all queries
   * Enable **Require no logging** — this filters the server list to only non-logging resolvers
   * Enable **Require no filtering** — unless you want malware filtering (Quad9 has this built in)
6. Go back to the DNSCrypt main tab.

#### Phase 3: Configure Tor

1. Tap the **Tor** tab at the bottom.
2. Tap the **settings gear** icon for Tor.
3. Under **Tor settings**:
   * Enable **Isolate destination addresses** — this makes each destination use a separate Tor circuit, preventing correlation between your visits to different sites
   * Enable **Isolate destination ports** — further isolation by port
   * Enable **Isolate SOCKS auth** if present
4. Under **Bridges** (optional but recommended if you are in a censored region):
   * Enable **Use bridges**
   * Select **obfs4** as the bridge type (obfuscates Tor traffic to look like normal HTTPS traffic, defeating deep packet inspection)
   * Tap **Request new bridges** or enter manual bridges from [bridges.torproject.org](https://bridges.torproject.org/)
5. Leave **Entry/Guard nodes** and **Exit nodes** on default unless you have specific requirements.
6. Go back to the Tor main tab.

#### Phase 4: Configure I2P

1. Tap the **I2P** tab at the bottom.
2. Tap the **settings gear** icon for I2P.
3. Under **I2P settings**:
   * Leave defaults for most users
   * If you want to use I2P hidden services (eepsites) specifically, ensure the I2P HTTP proxy is enabled on port `4444`
   * Enable **Tunnel bandwidth** management if your device is battery-constrained
4. I2P requires an initial bootstrap period (building its routing table) of approximately 10–20 minutes on first run — this is normal.
5. Go back to the I2P main tab.

#### Phase 5: Configure the Firewall (Root Mode)

Since your device is rooted with Magisk, iVizblePro can use root for enhanced firewall control:

1. Tap the **≡ hamburger menu** (top left) → **Settings** → **Common settings**.
2. Under **Root settings**:
   * Enable **Run modules with root** — this enables the enhanced iptables firewall
   * Enable **Fix TTL for tethering** (useful if you use hotspot)
3. Go to **Firewall** tab (in the main navigation):
   * You will see a list of all installed apps
   * Apps with a **green checkmark** are allowed through the tunnel
   * Apps with a **red X** are completely blocked from the internet
   * Apps with a **Tor icon** are forced to route exclusively through Tor
4. Recommended firewall rules:
   * **Block** all apps that do not need internet (games, offline tools, etc.)
   * **Force Tor** for your browser (AOSmium), Tuta Mail, Arcane Chat, OONI Probe
   * **Allow direct** (through DNSCrypt only, not Tor) for apps that need fast connections but not full anonymity (Aurora Store updates, Hypatia signature updates)
   * **Block completely** any Google services remnants, advertising frameworks, or telemetry services

#### Phase 6: Enable VPN Mode and Start All Services

1. Tap the **≡ hamburger menu** → **Settings** → **Common settings**.
2. Under **VPN settings**:
   * Enable **VPN mode** — this is what routes all phone traffic through iVizblePro's stack
   * Enable **Start on boot** — ensures protection is always active
   * Enable **Block internet when VPN is down** (kill switch) — prevents any traffic from leaking if iVizblePro restarts
3. Go back to the main screen.
4. On the main **Fast Start** screen (or the individual tabs), start services in this order:
   a. **DNSCrypt** — tap Start. Wait for "Running" status.
   b. **Tor** — tap Start. Wait for "Running" status (bootstrapping to 100% takes 30–60 seconds).
   c. **I2P** — tap Start. Wait for initial bootstrap (may take 10–20 minutes on first run).
5. Android will prompt you to confirm the VPN connection — tap **OK** / **Connect**.
6. You will see a key icon in your notification bar — iVizblePro's VPN tunnel is now active.

#### Phase 7: Verify Everything Is Working

1. In iVizblePro, check the main screen — all three services (DNSCrypt, Tor, I2P) should show green/running.
2. Open **AOSmium** browser.
3. Visit `https://check.torproject.org` — it should confirm **"Congratulations. This browser is configured to use Tor."**
4. Visit `https://dnsleaktest.com` — run the extended test. Your DNS should resolve through your selected DNSCrypt resolver, **not** your ISP.
5. The key icon should remain in your notification bar at all times.

#### Ongoing Usage Tips

* iVizblePro starts automatically on boot (if configured above) and the kill switch prevents any traffic from bypassing it.
* If Tor is slow (common during high-load periods), you can temporarily disable I2P to free up bandwidth for Tor — or vice versa if you are accessing I2P services specifically.
* Check the **Logs** tab regularly to see what your firewall is blocking and what circuits Tor is using.
* Update iVizblePro via F-Droid to keep Tor, I2P, and DNSCrypt binaries current.
* For maximum anonymity, do not log into any personal accounts (Google, Facebook, etc.) while Tor is active — the anonymity Tor provides can be defeated by account-level identification.

---

## OPSEC Step 3: Set Up Secure Email — Tuta + Duck Addresses

This two-layer setup gives you the strongest available email privacy. Tuta Mail is your real, encrypted inbox. Duck Addresses are disposable forwarding aliases you hand out to every app, website, and service instead of your real address — so your actual Tuta inbox is never exposed.

### Part A — Set Up Tuta Mail

1. Open **Tuta Mail** and create a new account.
2. Use a `.de` domain address (e.g., `yourname@tuta.de`) — German privacy laws (DSGVO/GDPR) provide strong legal protections for accounts hosted in Germany.
3. **No phone number is required.** Tuta only asks for an email address and an **encryption key / recovery code** — write this down and store it somewhere physically safe. This recovery code is how you regain access to your account if you ever lose access. Guard it the same way you would guard a physical key to your home.
4. Enable **biometric lock** or a strong PIN within Tuta Mail's security settings.
5. All emails between Tuta accounts are automatically end-to-end encrypted. Emails to external recipients (Gmail, etc.) can be password-encrypted using Tuta's "secure external password" feature.

**What Tuta does:** End-to-end encrypted email with zero trackers, zero ads, and zero data mining. Unlike Gmail, Tuta cannot read your emails. Unlike most providers, Tuta also encrypts subject lines and metadata — not just the body. Your encryption key means only you can access your account, even if Tuta's servers were ever compromised.

### Part B — Set Up Duck Addresses (DuckDuckGo Email Protection)

**Duck Addresses** are free, private email aliases provided by DuckDuckGo. The idea is simple: instead of giving any website, app, or service your real Tuta address, you give them a Duck Address like `yourname@duck.com`. DuckDuckGo strips all email trackers from messages and forwards them clean to your real Tuta inbox. If a service gets breached, sells your data, or starts spamming you — you just deactivate that alias. Your real Tuta address is never exposed.

**Setup:**

1. Open **DuckDuckGo Privacy Browser**.
2. Tap the **≡ menu** → **Settings** → **Email Protection**.
3. Tap **Get Started** and follow the setup flow.
4. When asked for your forwarding address, enter your **Tuta Mail address** — all forwarded emails will arrive in your Tuta inbox, stripped of trackers.
5. You will receive a **Duck Address** (e.g., `yourname@duck.com`). This is your primary alias. **No phone number required** — just your Tuta address to receive forwarded mail.
6. You will also be given an **encryption key / personal Duck Key** — store this safely alongside your Tuta recovery code. This is how you manage your account if needed.

**Using Duck Addresses everywhere:**

* Whenever any app, website, or form asks for your email address, tap the DuckDuckGo keyboard suggestion **"Use Duck Address"** — or manually enter your `@duck.com` address
* DuckDuckGo can also **auto-generate unique one-time aliases** for each service (e.g., `yourname_amazon_5k3j@duck.com`) — these appear as autofill suggestions in DuckDuckGo browser when you tap an email field
* Each unique alias forwards to your Tuta inbox with all trackers removed
* If a specific service starts sending spam or your alias appears in a breach, go to **DuckDuckGo Settings → Email Protection → Manage** and deactivate just that alias — without touching your real address

**What this stops:**
* **Phishers** — they only have a disposable alias, never your real Tuta address
* **Doxxers** — your real inbox cannot be searched for, looked up, or correlated across services
* **Data brokers** — even if five different companies share your email address, they each have a different alias and cannot link your accounts together
* **Email trackers** — DuckDuckGo strips tracking pixels, spy links, and hidden tracking code from every forwarded email before it reaches Tuta

### Part C — Auto-Generated Passwords in DuckDuckGo

DuckDuckGo's browser also includes a **built-in password manager** that integrates with Duck Address setup. Once you have Email Protection enabled:

* When you create a new account on any website in the DuckDuckGo browser, it will **automatically suggest a strong, randomly generated password** for the password field — tap to accept and it is saved to DuckDuckGo's encrypted local password storage
* Saved passwords are stored on-device, encrypted, and sync only to other devices you control via your Duck account (optional)
* On returning to a site, DuckDuckGo autofills both the Duck Address alias and your saved password
* This means for most sign-ups you never manually type or choose a password — the browser generates, saves, and fills it all automatically

**Use IYPS** (App #2) to analyse the strength of any existing passwords you want to migrate, then replace weak ones with DuckDuckGo-generated passwords going forward.

**The complete email security chain:**
```
Website/App → Duck Address alias (unique per service)
    → DuckDuckGo strips email trackers
        → Forwards clean to your Tuta Mail address
            → Tuta decrypts with your encryption key
                → You read it
```
Your real address never appears anywhere outside of the DuckDuckGo Email Protection settings on your own device.

---

## OPSEC Step 4: Spoof Location with Fake Traveler

Physical location is one of the most sensitive data points your phone broadcasts constantly. Fake Traveler lets you replace your real GPS coordinates with any location in the world.

1. Open **Fake Traveler**.
2. Browse the map and select a fake location (tap to pin it, or search for a city/place).
3. Tap **Apply** or **Start mocking**.
4. Go to **Settings → About phone** → tap **Build number** seven times to ensure Developer Options is open.
5. In **Developer Options** → scroll to **Select mock location app** → choose **Fake Traveler**.
6. Your device's GPS will now report the fake location to all apps that request it.

**What this does:** Spoofs your device's geolocation, preventing apps from determining your real position. This defeats location-based targeting, check-in tracking, and local services that attempt to correlate your physical movements with your online activity. Combined with iVizblePro's Tor routing (which hides your IP and therefore your approximate location from network observers), this gives you both network-level and sensor-level location protection.

---

## OPSEC Step 5: Final Checks and Hardening Tips

**iVizblePro / VPN conflicts:**
* Ensure no other app is using the Android VPN slot simultaneously. Check Settings → Network → VPN — only iVizblePro should show as "Connected."
* Allow iVizblePro background network access and disable any battery optimization that would kill it.

**Background app management:**
* Allow background network and battery usage for iVizblePro and Tuta Mail (for push notifications).
* Check Settings → Battery → Battery optimization → find both apps → set to "Not optimized."

**Network preference:**
* Use Wi-Fi over mobile data where possible — Tor performance is significantly better on Wi-Fi.
* On public Wi-Fi, iVizblePro's kill switch ensures no traffic leaks even on untrusted networks.

**Periodic maintenance:**
* Run **Hypatia** (from the DresOS app suite) weekly to scan for malware.
* Run **OONI Probe** to monitor for censorship or network manipulation in your area.
* Run **SD Maid SE** monthly to clear any leftover data from removed apps.
* Update all apps via F-Droid regularly — security patches are critical.

**Your device now has a hardened, layered cybersecurity posture reducing risks from surveillance, phishing, malware, censorship, and network-level attacks.**

---

---

# PART 3 — DRESOS DEFENSIVE APP SUITE

## Apps Overview

The following apps form the complete DresOS defensive security application suite. Every single one is open-source, has zero Google dependencies, and is sourced directly from verified developer releases or F-Droid. Together they cover encrypted file storage, password management, private social media, link safety scanning, malware detection, network censorship monitoring, privacy routing, private media, and secure communications — building a complete defensive security ecosystem on your device.

---

## 1. ZArchiver Pro — File Manager & AES Encryption

**Download:** [zarchiver-pro.apk](https://github.com/Nekorey/Zarchiver-Pro/releases/download/Zarchiver/zarchiver-pro.apk)

### What It Is

ZArchiver Pro is a powerful file management and archive tool with strong AES-256 encryption capabilities. While Fossify Files handles everyday file browsing, ZArchiver Pro is your tool whenever you need to compress, encrypt, archive, or securely package files. It supports a wide range of archive formats and can create password-protected, AES-256-encrypted archives.

### Key Features

* **AES-256 encryption** for 7z archives — the same encryption standard used by security professionals and government agencies
* Create and extract ZIP, 7z, TAR, GZ, BZ2, XZ, RAR (extract only), and many other formats
* Password-protect any archive with AES-256 or ZipCrypto
* Split large archives across multiple parts
* Preview files within archives before extracting
* Batch operations (compress multiple files at once)
* Full support for SD card, USB OTG storage, and internal storage

### Setup and Usage

1. Install via SAI from the direct APK link above.
2. Grant storage permission when prompted.
3. **Creating an encrypted backup:**
   * Long-press files/folders in ZArchiver → select **Compress**
   * Choose format: **7z** (for AES-256 encryption support)
   * Enable **Encrypt archive** → set a strong password (use IYPS from the next app to check its strength, or use DuckDuckGo's built-in password generator)
   * Select **Encryption method: AES-256**
   * Tap **OK** — your encrypted archive is created
4. **Extracting an encrypted archive:** tap the archive → enter password → extract
5. **Use case — Secure Backups:** Before performing any major system changes (flashing, debloating), compress your important files into an AES-256-encrypted 7z archive and store it on an SD card or secure off-device location.

### Why It's in the DresOS Suite

Sensitive files (personal documents, cryptographic keys, backup configurations) should never sit unencrypted on a device. ZArchiver Pro's AES-256 encryption means even if someone extracts your SD card or gains physical access to your storage, they cannot read protected archives without the password.

---

## 2. IYPS — Password Strength Analyser & Generator

**Download:** [IYPS_v1.5.6.apk](https://github.com/StellarSand/IYPS/releases/download/v1.5.6/IYPS_v1.5.6.apk)

### What It Is

IYPS (It's Your Password Security) is an open-source password strength analyser and generator. It does **not** store passwords — that job is handled by DuckDuckGo's built-in password manager (covered in App #14). What IYPS does is tell you exactly how strong or weak any given password is, with real-world crack-time estimates across different attack scenarios, and generate strong random passwords on demand.

### Key Features

* **Password strength analyser** — paste any existing password and get a detailed breakdown: entropy score, estimated crack time under online attack, offline attack, and distributed cracking scenarios
* **Password generator** — creates strong, random passwords with customisable length and character sets
* **Completely offline** — no password ever leaves your device during analysis
* No storage, no vault, no sync — purely an analysis and generation tool
* No ads, no trackers, no telemetry

### Setup and Usage

1. Install via SAI from the direct APK link above.
2. Open IYPS — no account or setup required.
3. **Check an existing password:**
   * Paste it into the analyser field
   * IYPS shows the entropy score and estimated crack time across attack scenarios (online throttled, offline fast hash, distributed brute-force)
   * Anything under "centuries" for an offline attack is worth replacing
4. **Generate a strong password:**
   * Go to the **Generator** tab
   * Set desired length (20+ characters recommended) and character set (uppercase, lowercase, numbers, symbols)
   * Tap generate — copy the result and save it in DuckDuckGo's password manager (see App #14)

### Why It's in the DresOS Suite

Most people massively overestimate how strong their passwords are. IYPS shows you in concrete terms exactly how quickly your password would fall — making it a practical tool for auditing your existing passwords before migrating them to DuckDuckGo's password manager. Use IYPS to generate and vet, DuckDuckGo to store.

---

## 3. RedReader — Private Reddit Client

**Download:** [RedReader-v1.25.1.apk](https://github.com/QuantumBadger/RedReader/releases/download/v1.25.1/RedReader-v1.25.1.apk)

### What It Is

RedReader is a free, open-source Reddit client that removes all advertising, tracking, data collection, and analytics present in the official Reddit app and other third-party clients.

### Key Features

* **No ads whatsoever** — not even Reddit's own promoted posts
* **No tracking or analytics** — no telemetry sent to Reddit or any third party
* **No account required** to browse — full anonymous access to Reddit content
* Optional account login for commenting/voting without Reddit app telemetry
* Clean, fast, highly readable interface
* Full image, GIF, and video support
* Offline reading mode — cache posts for reading without connectivity
* Night mode and customizable text sizes

### Setup and Usage

1. Install via SAI from the direct APK link above.
2. Open RedReader — no setup required to start reading anonymously.
3. **Browse without account:** You can immediately browse subreddits, search, and read posts without logging in.
4. **Optional account login:**
   * Settings → Accounts → Add Account
   * Log in with your Reddit credentials — RedReader does not store these beyond the session token
5. **Customize feed:**
   * Add subreddits to your front page by searching (magnifying glass) and subscribing
   * If not logged in, subreddits are stored locally in the app

### Why It's in the DresOS Suite

The official Reddit app is one of the most aggressive data-harvesting apps available — it requests extensive device permissions, tracks your reading behavior, and feeds data to advertising networks. RedReader provides the same content access with none of the surveillance.

---

## 4. URL Check — Link Scanner

**Download:** [URLCheck-3.4.1.apk](https://github.com/TrianguloY/URLCheck/releases/download/v3.4.1/URLCheck-3.4.1.apk)

### What It Is

URL Check is an open-source link analysis and scanning tool. Before opening any link, URL Check intercepts it and scans it for IP loggers, tracking parameters, malware indicators, phishing patterns, and URL redirects — showing you exactly where a link actually leads before you visit it.

### Key Features

* **IP logger detection** — identifies links from known IP-logging services (grabify, iplogger, etc.)
* **Phishing detection** — flags domains that impersonate legitimate services
* **Malware link scanning** — checks against known malicious URL databases
* **URL unshortener** — expands bit.ly, t.co, and all other shorteners to reveal the real destination
* **Tracking parameter stripping** — removes `utm_source`, `fbclid`, `gclid`, and all other tracking tags from URLs automatically
* **Redirect following** — shows the full redirect chain so you can see every server a link passes through
* VirusTotal integration (optional) — submit URLs to VirusTotal's multi-engine scanner
* Clipboard monitoring (optional) — automatically checks any URL you copy

### Setup and Usage

1. Install via SAI from the direct APK link above.
2. Open URL Check → go through the initial permissions setup (allow it to handle link intents).
3. **Set as default link opener:**
   * In URL Check settings → enable "Intercept links"
   * Android will prompt you to set URL Check as the handler for links — confirm
4. **How it works in practice:**
   * Someone sends you a link in a chat app or email
   * Instead of opening directly in the browser, URL Check intercepts it
   * A screen appears showing: the original URL, expanded URL, any trackers detected, any malware flags
   * Tap **Open** to proceed (if clean) or **Copy** to share the cleaned URL
5. **Tracking removal:**
   * Enable "Remove tracking parameters" in settings
   * All UTM tags, Facebook click IDs, Google analytics parameters, etc. are stripped automatically

### Why It's in the DresOS Suite

Phishing and IP logging are two of the most common attack vectors in targeted surveillance. A single click on an IP logger reveals your real IP address, approximate location, device type, and OS — even if you are using a VPN. URL Check prevents this by scanning every link before it is opened.

---

## 5. Hypatia — Open-Source Antivirus

**Download:** [hypatia_v3.18.apk](https://github.com/MaintainTeam/Hypatia/releases/download/v3.18/hypatia_v3.18.apk)

### What It Is

Hypatia is a fully open-source antivirus and malware scanner for Android, powered by ClamAV signature databases. It scans APKs before installation, scans files on your storage, and can perform full-device scans to detect known malware, trojans, ransomware, and other threats.

### Key Features

* **ClamAV-powered** — uses the same signature database as the industry-standard ClamAV engine trusted by organizations worldwide
* **APK scanning** — scans any APK file before you install it, including those from Aurora Store and direct downloads
* **File scanning** — scans documents, archives, downloaded files, and any other content on your storage
* **Full-device scan** — scans all installed apps and accessible storage in one pass
* **Real-time protection** (optional) — monitors new files as they are created or downloaded
* **Offline capable** — signatures are downloaded locally; scanning does not require internet once signatures are updated
* Zero telemetry, no cloud scanning, no data sent to any server during scans
* Regular signature updates via the app (or F-Droid)

### Setup and Usage

1. Install via SAI from the direct APK link above.
2. Open Hypatia → grant storage permission.
3. **Update signatures first:**
   * Settings → Update signatures → tap Update All
   * Wait for ClamAV, MSRT, and other signature databases to download
4. **Scan a specific APK before installing:**
   * Download an APK via Download Navi
   * Open Hypatia → Scan file → navigate to the downloaded APK → scan
   * If clean: green result → install with SAI
   * If flagged: do not install — delete the file
5. **Full device scan:**
   * Tap the **Scan** button on the main screen → select Full Scan
   * Hypatia scans all installed apps and storage
6. **Real-time monitoring:**
   * Settings → Real-time protection → Enable
   * Hypatia monitors new files as they land on your device and alerts you if anything malicious is detected
7. **Scheduled scans:**
   * Set up weekly scans in Settings → Schedule to run automatically

### Why It's in the DresOS Suite

Side-loading APKs (which is necessary on a de-Googled phone without Play Protect) requires you to take responsibility for your own malware screening. Hypatia with ClamAV signatures provides robust detection of known threats in every APK you install — a critical piece of the defensive stack.

---

## 6. OONI Probe — Network Censorship Detector

**Download:** [ooniprobe_274.apk](https://f-droid.org/repo/org.openobservatory.ooniprobe_274.apk)

### What It Is

OONI Probe (Open Observatory of Network Interference) is a network measurement tool developed by the Tor Project and independent researchers. It detects censorship, surveillance infrastructure, and network manipulation on your internet connection — telling you exactly what your ISP or government is blocking or tampering with.

### Key Features

* **Website blocking detection** — tests whether specific websites are blocked on your network
* **Censorship measurement** — detects DNS manipulation, HTTP blocking, TCP/IP blocking, and TLS interference
* **Surveillance infrastructure detection** — identifies middleboxes (equipment used for network surveillance)
* **VPN and Tor reachability** — tests whether Tor, VPNs, and circumvention tools are blocked
* **Global network data** — contributes your test results to OONI's public database, helping document censorship worldwide
* Runs automatic tests at scheduled intervals
* Completely open-source (Tor Project affiliated)

### Setup and Usage

1. Install from F-Droid using the link above (or search "OONI Probe" in F-Droid).
2. Open OONI Probe → complete the onboarding (agree to data sharing terms — your test results are contributed to the public OONI database anonymously).
3. **Run immediate tests:**
   * Tap **Run** on the main dashboard
   * OONI Probe runs the full test suite: websites, instant messaging, circumvention tools, middleboxes
4. **View results:**
   * Results appear under the **Test Results** tab
   * Green checkmarks = no blocking detected
   * Red X = blocking or manipulation detected
   * Orange warning = anomaly (possible interference)
5. **Automated testing:**
   * Settings → Automated testing → Enable
   * Set a schedule (e.g., daily at 3am on Wi-Fi only)
6. **Interpret results:**
   * If websites you expect to be accessible show as blocked → your ISP/government is censoring them → use iVizblePro's Tor routing to bypass
   * If circumvention tools (Tor, VPNs) show as blocked → use iVizblePro's Tor bridge mode (obfs4 bridges)

### Why It's in the DresOS Suite

Understanding your threat environment is the first step in defending against it. OONI Probe tells you exactly what your network operator is doing to your traffic — whether you are in a heavily censored country or simply want to know if your ISP is silently blocking certain content.

---

## 7. iVizblePro — All-in-One Proxy, Firewall & VPN

**Download:** [pan.alexander.tordnscrypt.stable_26603.apk](https://f-droid.org/repo/pan.alexander.tordnscrypt.stable_26603.apk)

*(Full setup instructions in Part 2 — OPSEC Step 2)*

### What It Is

iVizblePro (InviZible Pro) is the most important privacy tool in the DresOS stack. It is a single application that replaces what would otherwise require an entire stack of separate tools: Orbot (Tor), a standalone I2P client, a DNSCrypt resolver, and a firewall. It operates through the Android VPN interface, routing all traffic through its combined privacy stack.

### Summary of Features

* **Tor** — routes traffic through the onion network for strong anonymity; supports bridges and obfs4 for censored regions
* **I2P** — separate garlic-routing anonymity network for I2P hidden services and enhanced privacy
* **DNSCrypt** — encrypts and authenticates all DNS queries; prevents ISP surveillance via DNS
* **DNSSEC** — validates DNS responses cryptographically to prevent DNS spoofing
* **Built-in Firewall** — per-app firewall rules with kill switch; forces specific apps through Tor; blocks untrusted apps from the internet entirely
* **VPN mode** — routes all Android traffic through the above stack via the native VPN interface
* **Root support** — uses iptables for enhanced firewall control on rooted devices
* **Start on boot + kill switch** — ensures protection is always on; no traffic leaks if the app restarts

*(For complete step-by-step setup including Tor bridge configuration, DNSCrypt server selection, I2P bootstrap, firewall rules, and VPN mode activation, see Part 2 — OPSEC Step 2.)*

---

## 8. Metrolist — Private YouTube Music Client

**Download:** [Metrolist.apk](https://github.com/MetrolistGroup/Metrolist/releases/download/v13.3.0/Metrolist.apk)

### What It Is

Metrolist is a privacy-focused, modded YouTube Music client. It provides access to YouTube Music's full catalogue — including all your existing playlists and library if you have a YouTube Music account — without Google's tracking, advertising, or data collection.

### Key Features

* **Ad-free YouTube Music** — no pre-roll ads, no mid-song interruptions, no audio ads
* **No tracking** — Google Analytics, advertising identifiers, and telemetry calls are removed
* **Background playback** — music plays when the screen is off or when using other apps (normally requires a paid YouTube Music Premium subscription)
* **Audio quality control** — select specific bitrates and codec preferences
* **Offline capability** — cache songs locally for offline listening
* **Account support** — optionally log in with a YouTube/Google account to access your playlists and liked songs (note: if you log in, Google still knows what you are listening to — use without account for maximum privacy)
* Custom theme support, AMOLED dark mode

### Setup and Usage

1. Install via SAI from the direct APK link above.
2. Open Metrolist.
3. **Without account (maximum privacy):**
   * Browse and search the full YouTube Music catalogue freely
   * Your listening history is stored locally only
4. **With account (access your library):**
   * Tap the account icon → sign in via AOSmium browser with your Google account
   * Your playlists, liked songs, and subscriptions will sync
   * Understand that YouTube/Google will still log your listening activity server-side when you are logged in
5. **Background playback:**
   * Just minimize the app — music continues playing without needing any subscription
6. **Cache for offline listening:**
   * Long-press a song or playlist → Download → select audio quality
   * Downloaded files are stored in your chosen directory (manage with Fossify Files or ZArchiver Pro)

### Why It's in the DresOS Suite

Music streaming should not come with a surveillance apparatus. Metrolist gives you full access to YouTube Music's catalogue without surrendering your listening habits to Google's advertising engine.

---

## 9. Arcane Chat — Decentralized Encrypted Messaging

**Download:** [ArcaneChat-foss-arm64-v8a-2.43.0.apk](https://github.com/ArcaneChat/android/releases/download/v2.43.0/ArcaneChat-foss-arm64-v8a-2.43.0.apk)

### What It Is

Arcane Chat is a fully decentralized, end-to-end encrypted messaging application built on the **Delta Chat** protocol, which uses **email as the transport layer** with **OpenPGP end-to-end encryption**. This means your messages are transmitted over email infrastructure — making them extremely difficult to block, and giving you full control of your identity (your email address) without depending on any centralized messaging server.

### Key Features

* **End-to-end encryption** via OpenPGP (Autocrypt standard) — messages are encrypted on your device before transmission and can only be decrypted by the recipient
* **Decentralized** — no central Arcane Chat server; messages route through standard email servers. There is no single point of failure or surveillance
* **No phone number required** — your identity is your email address (use your Tuta Mail address for full privacy)
* **No metadata harvesting** — unlike Signal, WhatsApp, or Telegram, there is no central server collecting who you talk to, when, or how frequently
* **Censorship resistant** — email infrastructure is nearly impossible to block globally; even in censored regions, email typically works
* Group chats, image/file sharing, voice messages
* Multiple accounts (use different email addresses for different contexts)
* FOSS (fully open-source), no ads, no tracking

### Setup and Usage

1. Install via SAI from the direct APK link above.
2. Open Arcane Chat.
3. **Configure with Tuta Mail (recommended):**
   * Tap **Add Account**
   * Enter your Tuta Mail address
   * Arcane Chat will attempt auto-configuration; for Tuta you may need to enter IMAP/SMTP settings manually:
     * IMAP server: `imap.tuta.com` | Port: `993` | Security: TLS
     * SMTP server: `smtp.tuta.com` | Port: `465` | Security: TLS
   * Enter your Tuta password → Connect
4. **Start a conversation:**
   * Tap the **+** button → enter a contact's email address → write message → send
   * If the recipient also uses Arcane Chat (or any Autocrypt-compatible app), messages are automatically end-to-end encrypted — look for the **lock icon**
5. **Verify encryption:**
   * Open a chat → tap the contact name → **Encryption info**
   * Verify the displayed fingerprint matches your contact's (do this via a separate channel, e.g., in person or via phone call)
6. **Group chats:**
   * Tap + → New Group → add contacts by email → name the group → create
7. **Disappearing messages:**
   * Open a chat → Settings → Disappearing Messages → set a timer

### Why It's in the DresOS Suite

Most encrypted messengers require you to trust a central server (Signal's servers, Telegram's servers, WhatsApp/Meta's servers). Arcane Chat removes this trust requirement entirely — your messages flow over email infrastructure you choose, encrypted with OpenPGP that only you and your recipient hold keys for. Using it with Tuta Mail combines the strongest available email privacy with the strongest available decentralized messaging protocol.

---

## 10. Aurora Store — Anonymous App Store

**Download:** Install via F-Droid — search "Aurora Store" or go to `https://f-droid.org/packages/com.aurora.store/`

### What It Is

Aurora Store is an open-source, unofficial Google Play Store client that lets you browse, download, and update apps from Google's Play catalogue **without a Google account** and without any Google Play Services telemetry. It is a full Google Play replacement with complete anonymity.

### Key Features

* **Anonymous mode** — browse and download apps using randomly generated anonymous credentials. Google sees an anonymous device, not your account.
* No Google account login required
* Full Play Store catalogue access — any app available on Google Play can be downloaded
* App update management — check for updates for all Play-sourced apps
* **Exodus Privacy integration** — shows you a detailed tracker and permission report for every app before you install it
* Block automatic app updates for specific apps
* Spoofed device profile — can present as a different Android device to access region-locked apps
* No ads, no telemetry, zero Google components in the Aurora app itself

### Setup and Usage

1. Install via F-Droid.
2. Open Aurora Store → select **Anonymous** mode during setup. **Do not log in with a Google account.**
3. Browse, search, and install apps exactly as you would on the Play Store.
4. **Before installing any app, check its tracker report:**
   * Tap the app → scroll down to **Privacy** → check the Exodus Privacy report
   * Apps with many trackers (advertising, analytics, fingerprinting) should be avoided or replaced with FOSS alternatives
5. **Manage updates:**
   * Aurora Store → Updates tab → review available updates
   * Update FOSS apps via F-Droid instead (F-Droid verifies signatures; Aurora Store does not independently verify)

### Why It's in the DresOS Suite

Completely removing Play Store access is impractical for many users — some apps (banking, 2FA, essential services) only exist on Google Play. Aurora Store provides access to this catalogue without surrendering your identity or using Google Play Services. The Exodus Privacy integration helps you make informed decisions about which apps are safe to install.

---

## 11. Fossify Suite — Complete FOSS System Apps

**Download:** All via F-Droid — search each app name or visit [fossify.org/apps](https://www.fossify.org/apps/)

### What It Is

Fossify is a suite of open-source replacements for every core Android system app that Google ships with proprietary, tracking-laden stock versions. Together, the Fossify suite replaces the entire Google-provided app layer with fully open-source, zero-telemetry equivalents.

### Apps in the Suite

| App | Replaces | Features |
|---|---|---|
| **Fossify Phone** | Google/Stock Dialer | Open-source dialer, call blocking, call recording (where legal), no analytics |
| **Fossify Messages** | Google Messages | Open-source SMS/MMS, no Google RCS, no message scanning |
| **Fossify Files** | Files by Google | Local file manager, no cloud sync, no Google One integration |
| **Fossify Gallery** | Google Photos | Local gallery, no cloud backup to Google, no AI face scanning |
| **Fossify Calendar** | Google Calendar | Local calendar, optional CalDAV sync with your own server |
| **Fossify Launcher** | Pixel Launcher | Open-source home screen, no Google Feed integration |
| **Fossify Contacts** | Google Contacts | Local contacts, no sync to Google's servers |
| **Fossify Music** | YouTube Music / Play Music | Fully local music player, supports all common audio formats |
| **Fossify Clock** | Google Clock | Alarm, timer, stopwatch — zero telemetry |
| **Fossify Notes** | Google Keep | Local encrypted notes, no cloud sync |

### Setup

1. Install all Fossify apps via F-Droid (search individually or visit the Fossify F-Droid page).
2. Set each as the default for its function in **Settings → Apps → Default apps**.
3. Transfer your data:
   * **Contacts:** Export from old app as `.vcf` → import into Fossify Contacts
   * **Calendar:** Export as `.ics` → import into Fossify Calendar
   * **Photos:** Already on your storage — open with Fossify Gallery
   * **Music:** Already on your storage — open with Fossify Music

### Why It's in the DresOS Suite

Every stock Google app (Dialer, Messages, Files, Gallery, Calendar) contains telemetry that reports usage data, contact metadata, and behavioral information back to Google's servers. Fossify apps are clean replacements with identical functionality and zero reporting.

---

## 12. HeliBoard — Offline Keyboard

**Download:** F-Droid — search "HeliBoard" or visit `https://f-droid.org/packages/helium314.keyboard/`

### What It Is

HeliBoard is a fully open-source, completely offline keyboard for Android. It is a direct replacement for Google's Gboard, which is one of the most invasive data-collection tools on Android — it can capture everything you type (passwords, messages, searches) and transmit it to Google's servers for "personalization" and other undisclosed purposes.

### Key Features

* **Completely offline** — zero network access, zero data transmission
* Full multilingual support with offline dictionaries
* Swipe typing (gesture input)
* Auto-correction and predictive text (fully local)
* Customizable themes, layouts, and key sizes
* Voice input support via local speech-to-text (no cloud)
* No analytics, no crash reporting, no permissions beyond keyboard input
* Actively developed and maintained

### Setup and Usage

1. Install via F-Droid.
2. Open HeliBoard → follow the setup wizard to enable it as a system keyboard.
3. Go to **Settings → General management → Keyboard list and default** → select HeliBoard.
4. Disable Gboard (or remove it during the debloating step).
5. Download offline language dictionaries for your languages within HeliBoard settings.

---

## 13. Tuta Mail — Encrypted Email

**Download:** F-Droid — `https://f-droid.org/packages/de.tutao.tutanota/`

*(Full setup in Part 2 — OPSEC Step 3)*

### What It Is

Tuta Mail (formerly Tutanota) is an end-to-end encrypted email service operated by a German company under German and EU privacy law. It is a full Gmail replacement with zero data mining, zero ads, and full content encryption.

### Key Features

* **End-to-end encryption** for all emails (both subject and body, not just body like most providers)
* **Zero-knowledge** — Tuta cannot read your emails; they are encrypted before leaving your device
* **Encrypted contacts and calendar** included in the free plan
* Encrypted search (searches happen locally on your device, never on the server)
* **Email aliases** for compartmentalization (use different aliases for different purposes)
* Secure external email (password-protected messages to non-Tuta recipients)
* German/EU jurisdiction — GDPR compliance, no US FISA court exposure
* Free plan available; paid plans add more aliases and storage
* Fully open-source client (iOS and Android)

---

## 14. DuckDuckGo Privacy Browser — Primary Browser

**Download:** F-Droid — `https://f-droid.org/packages/com.duckduckgo.mobile.android/`

### What It Is

DuckDuckGo Privacy Browser is a privacy-focused web browser with built-in tracker blocking, a private search engine as default, a one-tap Fire Button to wipe all browsing data, a built-in password manager, and **Duck Address** email protection. It is the primary browser in the DresOS setup, replacing Chrome entirely.

### Key Features

* **Private search by default** — DuckDuckGo search engine, no user profiles, no search history tracking
* **Tracker blocking** — blocks known advertising and analytics trackers on every page
* **HTTPS upgrading** — automatically upgrades connections to HTTPS where available
* **Fire Button** — one tap destroys all tabs, cookies, and browsing history instantly
* **Cookie pop-up management** — automatically handles GDPR cookie banners
* **Duck Address / Email Protection** — generates private `@duck.com` forwarding aliases; strips trackers from forwarded emails before they reach your Tuta inbox; no phone number required, just your encryption key
* **Built-in password manager** — stores encrypted passwords locally; auto-generates strong unique passwords when you create accounts on websites
* **GPC (Global Privacy Control)** — broadcasts a legal opt-out signal to websites
* No Google account required, no telemetry

### ⚠️ Critical Setup Rule — App Tracking Protection

DuckDuckGo includes a feature called **App Tracking Protection** that monitors tracker activity in other apps by using the Android VPN slot. **Do NOT enable this feature.** iVizblePro already handles all traffic-level privacy for every app on the device, and it requires exclusive use of the Android VPN slot. If App Tracking Protection is enabled at the same time as iVizblePro, one of them will be forced off.

**The DuckDuckGo browser itself (without App Tracking Protection) is completely compatible with iVizblePro.**

### Setup and Usage

1. Install via F-Droid.
2. Open DuckDuckGo → complete onboarding.
3. When it asks about App Tracking Protection → **skip or decline**.
4. Set as default browser: Settings → Apps → Default apps → Browser → DuckDuckGo.

**Setting up Duck Address (Email Protection):**

5. Tap **≡ menu → Settings → Email Protection → Get Started**.
6. When prompted for a forwarding address, enter your **Tuta Mail address**.
7. You will receive a `@duck.com` alias. **No phone number required** — your account is secured with an encryption key only. Write that key down and store it safely.
8. From now on, use your Duck Address (or auto-generated per-site aliases) for every sign-up on every app and website — see full setup guide in OPSEC Step 3.

**Using the built-in password manager:**

9. When you create an account on any website, DuckDuckGo will **automatically suggest a strong generated password** in the password field — tap to accept.
10. The password is saved to DuckDuckGo's encrypted on-device storage automatically.
11. Next time you visit that site, DuckDuckGo autofills both your Duck Address alias and your saved password — you never have to remember or type either one.
12. Use **IYPS** (App #2) to analyse the strength of any older passwords you want to check before migrating them.

**Fire Button:**

13. Tap the flame icon at any time to wipe all tabs, cookies, and browsing history instantly — useful before handing your phone to someone or when switching contexts.

---

## 15. AOSmium — System WebView (Privacy-Hardened WebView Engine)

**Download:** AXP.OS F-Droid repo (see Step 7) or [codeberg.org/AXP-OS/app_aosmium/releases](https://codeberg.org/AXP-OS/app_aosmium/releases)

*(Full setup and activation in Part 1 — Step 7)*

### What It Is

AOSmium is the **System WebView replacement** in the DresOS stack — not a browser you open directly. Built by the AXP.OS Project, it is a Chromium fork built on Mulch (Divested Computing Group) with GrapheneOS/Vanadium security patches, minimized Google anti-features, and privacy hardening throughout.

The **Android System WebView** is used by hundreds of apps whenever they need to render web content inside themselves — social media apps, news apps, email clients, microG sign-in pages, shopping apps, and more. By replacing it with AOSmium, all of that embedded web content is rendered through a privacy-hardened, Google-free engine rather than Google's stock WebView.

**DuckDuckGo Privacy Browser** is your everyday browser. **AOSmium** runs silently in the background as the engine powering web content in every other app.

### Features

* Chromium-based with Vanadium (GrapheneOS) security patches
* Fork of Mulch (Divested Computing Group)
* Google anti-features minimized throughout
* Auto-updates via AXP.OS F-Droid repository
* Hardens web content rendering for every app on the device, not just the browser

---

---

# APPENDIX

## Compatible Devices

Tested and confirmed working for the full DeGoogling + OPSEC stack:

```
- Motorola Moto G32 (custom TWRP recovery available on DresOS GitHub profile)
- Motorola Moto G7 Plus
- Samsung Galaxy A05s
```

**If this works on your device, please report it with proof to the DresOS team** so we can add it to the official compatibility list. Include: device model, Android version, TWRP version used, and which steps you completed.

Device-specific debloat lists and flashable ZIPs are available for the above devices. Drop your exact model in the Issues tab and the DresOS team will add a custom guide or resource for your device.

---

## Contact DresOS

* **Website:** https://dresoperatingsystems.github.io/
* **Issues & Device Requests:** Use the GitHub Issues tab on this repository

---

## License

MIT License — see [LICENSE](LICENSE) file.

---

## Made with ❤️ for privacy by DresOS

**You now have a 100% de-Googled DresOS, operationally secure Android device** — no Google apps, no Google Services, AOSmium WebView system-wide, Tor + I2P + DNSCrypt + Firewall via iVizblePro, and a complete defensive security app suite. Every tool is open-source, every APK is sourced directly from verified developers, and every component is designed to give you control of your own device, your own data, and your own privacy.

---

**tbis is an update to both the degoogled and opsec project*
