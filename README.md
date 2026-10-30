# Vermeer GKI — CASS

An Android 13 GKI 5.15.123 (2023-11) kernel build with **Capacity Aware Superset Scheduler (CASS)**, **KernelSU-Next**, and **SUSFS**. This repository contains the build workflow and patches; the kernel source is downloaded during the build.

## Features

- **CASS:** Selects CPUs for normal and real-time task wakeups based on capacity and load. It does not control CPU or GPU clock speeds directly.
- **KernelSU-Next:** Kernel-based root support.
- **SUSFS:** Kernel extensions for root-hiding functionality.
- **Runtime statistics:** CPU-selection counters at `/sys/kernel/cass/stats`.

## Sources

- **Kernel:** [Google Android Common Kernel](https://android.googlesource.com/kernel/common/) — Android 13 / 5.15 / 2023-11, synced through the [Android kernel manifest](https://android.googlesource.com/kernel/manifest/).
- **CASS:** Sultan Alsawaf's Capacity Aware Superset Scheduler, adapted from vendor kernel implementations; see [`0001-cass-core-scheduler.patch`](patches/cass/0001-cass-core-scheduler.patch) for provenance.
- **KernelSU-Next:** [pershoot/KernelSU-Next](https://github.com/pershoot/KernelSU-Next) (`dev-susfs`).
- **SUSFS:** [simonpunk/susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu), with [pershoot's compatibility fixes](https://gitlab.com/pershoot/susfs4ksu).
- **Additional patches:** [RiRiRawrZ615/kernel_patches](https://github.com/RiRiRawrZ615/kernel_patches).
- **Flashable ZIP packaging:** [WildPlusKernel/AnyKernel3](https://github.com/WildPlusKernel/AnyKernel3) (`gki-2.0`).
- **Repository foundation:** [WildKernels/GKI_KernelSU_SUSFS](https://github.com/WildKernels/GKI_KernelSU_SUSFS).

## Builds

The [CASS GitHub Actions workflow](.github/workflows/build-a13-5-15-cass.yml) builds the kernel and publishes downloadable artifacts.

To verify CASS is executing on a rooted device:

```sh
su -c 'cat /sys/kernel/cass/stats'
```

Increasing counters confirm CPU-selection calls, not performance improvements.

**Experimental:** Check device compatibility and keep a backup before flashing.

## Credits

CASS by **Sultan Alsawaf**. Thanks to the KernelSU-Next, SUSFS, WildKernels, and Android kernel contributors.
