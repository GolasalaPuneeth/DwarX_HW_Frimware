# DwarX HW Firmware

ESP32 firmware for remote over-the-air (OTA) updates, designed to keep devices updated with the latest firmware securely and efficiently.

This repository contains firmware binaries and an OTA version manifest used to check for updates and deploy new firmware remotely to ESP32-based hardware.

## Overview

DwarX HW Firmware is built for ESP32 devices that need a reliable update mechanism without requiring manual flashing through a physical cable. The firmware update flow is based on a version manifest that tells the device which firmware image is the latest and where it can be downloaded.

This setup is useful for:
- Remote firmware deployment
- Device maintenance without physical access
- Version tracking and controlled rollout
- Simplified firmware management for ESP32 devices

## Features

- ESP32 OTA update support
- Remote firmware download via GitHub-hosted binary
- Version-based upgrade checks
- Easy firmware update management
- Prebuilt firmware binaries included in the repo
- Lightweight manifest-driven update workflow

## Repository Structure

- `main_fa.ino.bin` - Main firmware binary
- `mytest_OTA.bin` - OTA test firmware binary
- `ESP_IDF_ARDUINO.bin` - ESP-IDF/Arduino firmware image
- `Test_app_components.bin` - Testing firmware image
- `Test_learn.bin` - Learning/test build
- `Version_manifest.json` - OTA version and binary URL manifest
- `LICENSE` - Repository license

## OTA Update Flow

The repository uses a simple version manifest pattern:

```json
{
  "VERSION": 2,
  "FIRMWARE": "https://raw.githubusercontent.com/GolasalaPuneeth/DwarX_HW_Frimware/main/main_fa.ino.bin"
}
```

A device using this firmware:
1. Reads `Version_manifest.json`
2. Compares the local version with the manifest `VERSION`
3. Downloads the new firmware image if an update is available
4. Installs the firmware using the ESP32 OTA mechanism
5. Reboots and starts the new version

## Getting Started

### Requirements

- ESP32 development board
- Arduino IDE or ESP-IDF environment
- Stable internet connection for OTA downloads
- Compatible firmware client implementation for OTA checks

### Flashing the Initial Firmware

Use one of the provided `.bin` files to flash the device initially, depending on your target build and hardware setup.

### Updating Firmware Over the Air

Update the version manifest when a new firmware build is ready:

- Increase the `VERSION` value
- Point `FIRMWARE` to the new binary URL
- Push the updated manifest and binary to the repository
- The ESP32 device checks for updates and applies the new firmware automatically

## Versioning

This project uses a simple numeric `VERSION` in the manifest to indicate the firmware revision. Increasing the version ensures the device recognizes a newer release and downloads the matching binary.

## Security Considerations

For production use, it is recommended to:
- Only download firmware from trusted sources
- Validate firmware integrity before flashing
- Use HTTPS and authenticated endpoints where possible
- Implement signature verification or secure update validation
- Restrict OTA access to authorized devices


## Notes

This repository currently includes compiled firmware binary images and an OTA manifest, which makes it suitable for rapid deployment and testing on ESP32 hardware. For production applications, consider adding:
- secure signing
- rollback support
- version history tracking
- device authentication checks

## Contributing

Contributions, firmware improvements, and OTA workflow enhancements are welcome. Please update the manifest and document any changes to the firmware architecture or deployment process.

---

Made for ESP32-based OTA firmware deployment and remote device update management.
