# CASS GKI Kernel

Android 13 GKI 5.15.123 kernel with the Capacity Aware Superset Scheduler (CASS), KernelSU-Next, and SUSFS.

## Features

- **CASS:** Capacity-aware CPU selection for fair and real-time tasks.
- **KernelSU-Next:** Kernel-based root access.
- **SUSFS:** Kernel support for root hiding.
- **Runtime statistics:** CASS CPU-selection counters at `/sys/kernel/cass/stats`.

## Sources

- **Kernel:** [Android Common Kernel](https://android.googlesource.com/kernel/common/) via the [Android kernel manifest](https://android.googlesource.com/kernel/manifest/) (`common-android13-5.15-2023-11`).
- **CASS:** Sultan Alsawaf's scheduler, adapted from [dev-sm8350](https://github.com/dev-sm8350/kernel_oneplus_sm8350) and [ChicKernel](https://github.com/ChicKernel/device_xiaomi_gemstones-kernel/tree/android13-5.15-lts).
- **KernelSU-Next:** [pershoot/KernelSU-Next](https://github.com/pershoot/KernelSU-Next) (`dev-susfs`).
- **SUSFS:** [simonpunk/susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu) with [pershoot's fixes](https://gitlab.com/pershoot/susfs4ksu).
- **Additional patches:** [RiRiRawrZ615/kernel_patches](https://github.com/RiRiRawrZ615/kernel_patches).
- **Flashable ZIPs:** [WildPlusKernel/AnyKernel3](https://github.com/WildPlusKernel/AnyKernel3) (`gki-2.0`).
- **Build workflow foundation:** [WildKernels/GKI_KernelSU_SUSFS](https://github.com/WildKernels/GKI_KernelSU_SUSFS).

## Build and verify

The [GitHub Actions workflow](.github/workflows/build-a13-5-15-cass.yml) builds the kernel and uploads ZIPs and boot images as artifacts.

Check CASS activity on a rooted device:

```sh
su -c 'cat /sys/kernel/cass/stats'
```

Increasing counters confirm that CASS CPU selection is running.

**Experimental:** Confirm device compatibility and back up your original boot image before flashing.
