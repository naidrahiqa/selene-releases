# selene-releases

Release page for **PawwwNunungggg Kernel** — a custom **Linux 4.19.325** kernel for the **Xiaomi Redmi 10 / Redmi 10 2022 / Redmi 10 Prime** (codename `selene`, MediaTek Helio G88 / MT6768).

This repository holds **no kernel source**. Its Releases page is where the flashable AnyKernel3 zips are published: every push to the kernel source's `PawwwNunungggg24.0` branch produces one release here, numbered sequentially (`R01`, `R02`, …).

## Supported device

| Device | Codename | SoC | Kernel |
| --- | --- | --- | --- |
| Xiaomi Redmi 10 / Redmi 10 2022 / Redmi 10 Prime | `selene` | MediaTek Helio G88 (MT6768) | Linux 4.19.325 |

## What is in a release

Every release ships one kernel source compiled into **4 variants**:

| Asset suffix | Root solution | NoMount | Notes |
| --- | --- | --- | --- |
| `xxksu-nomount` | xxKSU `v3.3.0-70` (`KSU_VERSION 32670`) | ✅ | systemless path redirection on |
| `xxksu` | xxKSU `v3.3.0-70` | ❌ | NoMount compiled out |
| `bakasu-nomount` | BakaSU `v4.2.0-rc3` (`KSU_VERSION 35223`) | ✅ | multi-manager support + `/system/etc/hosts` redirect |
| `bakasu` | BakaSU `v4.2.0-rc3` | ❌ | NoMount compiled out |

Asset naming: `PawwwNunungggg-<variant>-R<##>-<sha7>-<YYYYMMDD>.zip`

Each release body also lists **Build Statistics** — per-variant build time, zip size and md5 — plus the exact commit the release was built from, and the latest changelog entry.

## Kernel highlights

- **Root:** xxKSU or BakaSU, both in manual-hook mode (no legacy-module path)
- **NoMount v2.1** — systemless path redirection (keyring-based, isolated-UID blocking)
- **I/O:** ADIOS scheduler (BFQ available), Dynamic Fsync 2.0
- **Network:** BBR + FQ-CoDel, TTL 64 (tethering TTL bypass), BPF JIT
- **Memory:** ZRAM (LZ4) with a device-appropriate cap, `vm.swappiness` tuned for 6 GB RAM
- **Misc:** hardware KCAL color control, touch-to-wake, Boeffla Wakelock Blocker
- **Toolchain:** Greenforce Clang 24.0.0 (LLVM, ThinLTO/O3), ccache-accelerated CI

## Root managers

| Variant | Manager |
| --- | --- |
| `xxksu-*` | [xxKSU Manager](https://github.com/backslashxx/KernelSU/releases) (KernelSU Official compatible) |
| `bakasu-*` | BakaSU multi-manager build — accepts KernelSU Official / KOWSU / BakaSU |

Any variant pairs with the NoMount module **v2.1+** (verify with `nm version` → `21`).

## How to flash

1. **Unlock the bootloader** — required.
2. Download the zip matching your variant from the Releases page below.
3. Flash from a custom recovery (TWRP / OrangeFox), or `adb reboot recovery` then sideload the AnyKernel3 zip.
4. **⚠️ Flash the `boot` partition only.** Never flash `lk`, `dtbo`, or any bootloader/DTB image — MediaTek Little Kernel is a second-stage bootloader, and a bad `lk`/`dtbo` can hard brick the device.
5. Install the root manager for your variant (see table above), then reboot.

## Related repositories

- **Kernel source:** [naidrahiqa/android_kernel_xiaomi_mt6768-k419](https://github.com/naidrahiqa/android_kernel_xiaomi_mt6768-k419) — PawwwNunungggg development, changelog and CI (branch `PawwwNunungggg24.0`).
- **Build tooling:** [naidrahiqa/kernel-ci-kit](https://github.com/naidrahiqa/kernel-ci-kit) — reusable GitHub Actions toolkit (cached Clang toolchain, ccache, AnyKernel3 packaging, Telegram notifications).
- **NoMount:** [maxsteeel/nomount](https://github.com/maxsteeel/nomount) — systemless path redirection module.
- **xxKSU:** [backslashxx/KernelSU](https://github.com/backslashxx/KernelSU) — root solution used by the `xxksu-*` variants.