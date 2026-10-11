# selene-releases

Release container and download page for **Phrolova Kernel**, a custom Linux 4.14 kernel for the **Xiaomi Redmi 10 2022** (`selene`). This repository holds no kernel source — its Releases page is where the flashable build artifacts are published.

## Supported device

| Device | Codename | SoC |
| ------ | -------- | --- |
| Xiaomi Redmi 10 2022 | `selene` | MediaTek Helio G88 / MT6768 (Linux 4.14) |

## Related repositories

- **Kernel source:** [naidrahiqa/android_kernel_xiaomi_selene](https://github.com/naidrahiqa/android_kernel_xiaomi_selene) — Phrolova Kernel development, changelog, and CI builds (branch `phrolova`).
- **Build tooling:** [naidrahiqa/kernel-ci-kit](https://github.com/naidrahiqa/kernel-ci-kit) — reusable GitHub Actions toolkit (cached Clang toolchain, ccache, AnyKernel3 packaging, release publishing) used to produce the kernel builds.

## Downloads

- [Releases of this repository](../../releases) — build artifacts published here.
- [Kernel repository releases](https://github.com/naidrahiqa/android_kernel_xiaomi_selene/releases) — CI builds (`Phrolova-selene-<tag>-<hash>.zip`, AnyKernel3 format).

## How to flash

Summarized from the [kernel repository README](https://github.com/naidrahiqa/android_kernel_xiaomi_selene#flash):

1. **Unlock the bootloader** (UBL) — required.
2. Download the latest `Phrolova-selene-*.zip` from a Releases page above.
3. Flash via a custom recovery (TWRP / OrangeFox), or `adb reboot recovery` and sideload the AnyKernel3 zip. The zip is A/B slot aware (`block=auto`).
4. Install a matching root manager: **ReSukiSU** manager (recommended) or any supported multi-manager build (KernelSU / MKSU / RKSU / SukiSU-Ultra).
5. **NoMount** users: install the NoMount module **v2.0.0+** and verify with `nm version` (should return `20`).

For full build instructions, feature list, and security notes, see the [kernel repository](https://github.com/naidrahiqa/android_kernel_xiaomi_selene).
