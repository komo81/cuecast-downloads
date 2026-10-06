# CueCast downloads

Official installation packages for **CueCast**, a camera, CueScore overlay and live-streaming application for Windows and Raspberry Pi.

Website: [cuecast.freeward.dev](https://cuecast.freeward.dev) · Contact: [info@freeward.dev](mailto:info@freeward.dev)

This public repository contains releases and installation instructions only. The application's source repository is maintained separately and is not made public by these releases. No user settings, stream keys or sign-in tokens are included in the packages.

## Windows 10/11 x64

1. Download [cuecast-windows-x64.zip](https://github.com/komo81/cuecast-downloads/releases/latest/download/cuecast-windows-x64.zip).
2. Extract it to a temporary folder and run **Install.cmd**.
3. Keep your internet connection available: the online installer downloads pinned versions of FFmpeg, GStreamer, Chromium and Microsoft Visual C++ Runtime directly from their distributors. Archive checksums are verified. This may download several hundred MB and take a few minutes.
4. Accept Microsoft's Visual C++ Runtime installation prompt if required.
5. Use the **CueCast** desktop / Start menu shortcut next time. You can delete the extracted installer folder after successful installation.

No separate Node.js, video tools or browser installation is required. Windows ARM64 is not supported. The installer is not digitally signed. Obtain it only from this repository and verify its checksum if in doubt.

Stop broadcasts and close CueCast before installing an update. Settings are preserved in `%LOCALAPPDATA%/CueCast/data`; back up that entire directory before updating. It contains sensitive account data and stream keys.

## Raspberry Pi OS 64-bit / Debian 13 Trixie ARM64

Use standard **Raspberry Pi OS Lite 64-bit (Trixie)** on Raspberry Pi 4 or a compatible device. The package requires internet access to install dependencies from your system repositories.

```sh
curl -fL https://github.com/komo81/cuecast-downloads/releases/latest/download/cuecast-raspberry-pi-arm64.deb -o cuecast-raspberry-pi-arm64.deb
sudo apt update
sudo apt install ./cuecast-raspberry-pi-arm64.deb
```

Open `http://DEVICE-HOSTNAME.local:8787` or `http://DEVICE-IP:8787` on the same local network. The application starts automatically as `cuecast.service`.

For updates, first stop broadcasts and back up `/var/lib/cuecast`; then install the new DEB using the same procedure. The configuration is preserved. A service restart interrupts previews and broadcasts.

The package does not contain the full Raspberry Pi OS image and does not format your SD card. It is not intended for 32-bit OS or Debian 12 Bookworm.

## Multiple tables and security

The original configuration becomes the first table automatically. Add further tables from the overview, configure their camera and output separately and use different stream keys for simultaneous broadcasts. An IP camera can be read by several tables if it supports multiple clients; a local USB/CSI camera is reserved to one active table at a time. Performance depends on the device and available hardware encoder sessions. Raspberry Pi can continue using one table.

The local web interface has no user authentication. Keep it on a trusted network; do not expose ports 8787 or 8554 directly to the public internet. Remote access requires an appropriately secured connection. Video is processed locally and sent directly to your chosen output, not through the sign-in website.

## Verification and third-party software

Each release includes **SHA256SUMS.txt**, version notes and package information. On Windows, use `Get-FileHash FILE -Algorithm SHA256`; on Linux, use `sha256sum FILE` and compare the result with the release file.

The public Windows ZIP includes Node.js and MediaMTX with their original MIT license notices, plus production JavaScript dependencies and their license files. GPL/LGPL video tools and Chromium are downloaded from upstream on your device rather than redistributed in this ZIP. The Pi package installs system video tools using APT. Third-party licenses and notices remain with their respective runtimes. The proprietary Microsoft Visual C++ Runtime is obtained from Microsoft.

## Stručný český návod

- **Windows:** stáhněte ZIP, rozbalte, spusťte `Install.cmd`. Instalace potřebuje internet a může trvat několik minut. Potom spouštějte zástupcem CueCast.
- **Raspberry Pi:** použijte Raspberry Pi OS Lite 64-bit Trixie, stáhněte DEB a spusťte výše uvedené příkazy. Web je na `http://ADRESA-ZARIZENI:8787`.
- **Aktualizace:** zastavte vysílání, zazálohujte celý adresář dat, zavřete CueCast (Windows) a spusťte nový instalátor. U Pi instalace restartuje službu.
- **Síť:** aplikace nemá místní přihlašování; zpřístupněte ji pouze důvěryhodným uživatelům a nevystavujte její porty veřejně.
