# OrangeFox Recovery Device Tree for Xiaomi 14 Ultra (aurora)

This repository contains the device tree to build OrangeFox Recovery for the Xiaomi 14 Ultra (Snapdragon 8 Gen 3). 

## 📱 Device Specifications

| Device       | Xiaomi 14 Ultra |
| :---         | :--- |
| **Codename** | `aurora` |
| **SoC**      | Qualcomm Snapdragon 8 Gen 3 (SM8650-AB) |
| **Release**  | February 2024 |
| **Boot**     | Android 14 GKI (Boot Header v4) |

## 🚀 Current Status

**Working:**
* Booting & UI rendering
* Touchscreen (using isolated prebuilt Synaptics modules)
* ADB & Fastbootd
* Sideloading

**Not Working:**
* Android 14 FBE Decryption (Internal storage cannot be mounted). Use ADB Sideload as a workaround.

## 🛠 How to Build

If you want to compile this recovery yourself, you need to set up an OrangeFox Android 12.1 build environment.

**1. Initialize the OrangeFox workspace:**
```bash
repo init -u https://gitlab.com/OrangeFox/manifest.git -b fox_12.1
repo sync -j$(nproc --all) --force-sync
```

**2. Clone this device tree:**
```bash
git clone https://github.com/mls0x1/android_device_xiaomi_aurora.git device/xiaomi/aurora
```

**3. Build the recovery:**
```bash
# Export necessary variables
export ALLOW_MISSING_DEPENDENCIES=true
export FOX_BUILD_DEVICE=aurora
export LC_ALL=C  # Required to prevent locale code-generation bugs

# Set up build environment
source build/envsetup.sh
lunch twrp_aurora-eng

# Clean and build (Clean is mandatory after config changes!)
mka clean recoveryimage
mka adbd recoveryimage
```

The compiled image will be output to `out/target/product/aurora/recovery.img`.

## 🤝 Credits & Thanks
* [OrangeFox Recovery Team](https://gitlab.com/OrangeFox)
* [SebaUbuntu's TWRP device tree generator](https://github.com/SebaUbuntu/TWRP-device-tree-generator) for the initial skeleton
* Gemini and Claude Opus for debugging assistance
