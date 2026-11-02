# Xiaomi 15 (dada) local manifests

Device, vendor, kernel, firmware, and MiuiCamera trees for building custom ROMs
on Xiaomi 15 (`dada`, SM8750 / `sun`).

Blobs re-extracted from HyperOS 4 CN **OS4.0.0.22.XOCCNXM** (Android 17).

## Sync

Drop `dada.xml` into `.repo/local_manifests/` of an Android 15/16/17 ROM tree
(Lineage 23.2, DerpFest 17, …), then:

```bash
git lfs install
repo sync -c -j$(nproc)
```

Vendor and kernel repos use **git-lfs**. Do not set `GIT_LFS_SKIP_SMUDGE=1`.

## Repositories

| Path | Repo |
| --- | --- |
| `device/xiaomi/dada` | [android_device_xiaomi_dada](https://github.com/devine-machinery/android_device_xiaomi_dada) |
| `device/xiaomi/sm8750-common` | [android_device_xiaomi_sm8750-common](https://github.com/devine-machinery/android_device_xiaomi_sm8750-common) |
| `device/xiaomi/dada-kernel` | [android_device_xiaomi_dada-kernel](https://github.com/devine-machinery/android_device_xiaomi_dada-kernel) |
| `device/xiaomi/dada-miuicamera` | [android_device_xiaomi_dada-miuicamera](https://github.com/devine-machinery/android_device_xiaomi_dada-miuicamera) |
| `vendor/xiaomi/dada` | [android_vendor_xiaomi_dada](https://github.com/devine-machinery/android_vendor_xiaomi_dada) |
| `vendor/xiaomi/sm8750-common` | [android_vendor_xiaomi_sm8750-common](https://github.com/devine-machinery/android_vendor_xiaomi_sm8750-common) |
| `vendor/xiaomi/dada-firmware` | [android_vendor_xiaomi_dada-firmware](https://github.com/devine-machinery/android_vendor_xiaomi_dada-firmware) |
| `vendor/xiaomi/dada-miuicamera` | [android_vendor_xiaomi_dada-miuicamera](https://github.com/devine-machinery/android_vendor_xiaomi_dada-miuicamera) |

Branch: `lineage-23.2`.

Dolby stays at `dada-devel/hardware_dolby` (`revision="16"`).

## Notes for other ROMs

- Product is `lineage_dada` / lunch `lineage_dada-cp2a-user` on DerpFest 17. Adapt `AndroidProducts.mk` and the product makefile for your ROM.
- Fingerprint HAL is the **vendor prebuilt** `android.hardware.biometrics.fingerprint-service.xiaomi_prebuilt`. `sm8750-common` sets `XIAOMI_BIOMETRICS_FINGERPRINT DISABLE_SOURCE` so a source HAL in `hardware/xiaomi` is not built for dada.
- CAF sm8750 display prebuilts that collide with `hardware/qcom-caf/sm8750` are `enabled: false` in vendor `Android.bp`: `libdisplayconfig.qti`, `libqdMetaData`, `libsdmutils`, `vendor.qti.hardware.display.snapalloc-impl`.
- `BOARD_SUPPORTS_OPENSOURCE_STHAL := false` because vendor already ships `libsoundtriggerhal.qti`.
- Radio images live only in `vendor/xiaomi/dada-firmware`. `extract-files.py` has `add_firmware_proprietary_file=False`.
- Prebuilt kernel: `6.6.118-android15-8-gb9cc6ec16bc8-abogki536571621-4k` (vermagic `6.6.57-android15-8-4k`).
- MiuiCamera overrides Aperture and Camera2.

Stock dump used for the re-extract:
`dada-ota_full-OS4.0.0.22.XOCCNXM-user-17.0-348446ddf9.zip`
