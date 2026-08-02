# Repository Cleanup Candidates — kernel_samsung_a04s_portbase

Audit date: 2026-08-01

This document lists files and directories that appear safe to remove before
publishing this repository, plus items that need manual review. It is a
**report only** — nothing here has been deleted.

Confidence legend:

- **HIGH** — generated content, safely regenerable, not referenced by any
  build input or tracked source.
- **MEDIUM** — very likely safe, but verify the specific use before removal.
- **LOW** — plausible but requires judgement; listed for completeness.

---

## Build artifacts

No build artifacts (.o, .a, .ko, .cmd, .dtb, .dtbo, vmlinux, Image, etc.)
were found in the working tree. All kernel build outputs were produced in
out-of-tree directories (`kernel_porting/work/`, outside this repository)
and were removed after the final verification build. The root `.gitignore`
now prevents them from re-entering the tree.

## Python cache

| Path | Why remove | Confidence |
|---|---|---|
| `scripts/fmp/__pycache__/` (contains `ELF.cpython-312.pyc`, `IntegrityRoutine.cpython-312.pyc`, `Utils.cpython-312.pyc`) | Byte-compiled Python cache, regenerated automatically from `ELF.py`, `IntegrityRoutine.py`, `Utils.py`. Not a build input. | HIGH |

## Editor / IDE files

| Path | Why remove | Confidence |
|---|---|---|
| `KernelSU-Next/kernel/.clangd` | IDE (clangd) configuration, not part of the KernelSU source or kernel build; currently untracked/ignored. | HIGH |

## Temporary files

None found (no `*.tmp`, `*.log`, `*.orig`, `*.rej`, `*.bak`, `*~`, `*.swp`
files in the tree).

## Merge leftovers

None found.

## Backup files

None found.

## Cache

None found (no `.cache/`, `.ccache/`).

## Logs

None found in-tree (all build logs were written under
`/home/mike/android/kernel_porting/work/`, outside this repository).

## Generated kernel outputs

None found in-tree. All generated outputs were out-of-tree and removed.

## Empty directories

None found.

## Deleted tracked files (already staged for removal)

The following files are tracked in git but have been deleted from the
working tree by the port (the arm64 dts Makefile now builds the A04s
overlays instead):

| Path | Why remove | Confidence |
|---|---|---|
| `arch/arm64/boot/dts/samsung/a21s/a21s_eur_open_w00_r00.dts` | Obsolete A21s device-tree source; no longer referenced by `arch/arm64/boot/dts/Makefile` (0 references). | HIGH |
| `arch/arm64/boot/dts/samsung/a21s/a21s_eur_open_w00_r01.dts` | Same | HIGH |
| `arch/arm64/boot/dts/samsung/a21s/a21s_eur_open_w00_r02.dts` | Same | HIGH |
| `arch/arm64/boot/dts/samsung/a21s/a21s_eur_open_w00_r03.dts` | Same | HIGH |
| `arch/arm64/boot/dts/samsung/a21s/a21s_eur_open_w00_r06.dts` | Same | HIGH |

These are already deleted on disk; completing the removal is a
`git rm` / `git commit` away.

## Firmware blobs not referenced by `firmware/Makefile` (manual review)

The following blobs exist in the tree but are **not** referenced by the
firmware `Makefile` for the current A04s configuration. They were carried
in with the A13 firmware set (which serves the whole Exynos850 family:
A12s/A13/A14/M12/M13/XCover5/A04s). The A04s kernel does not build them.
Deleting them is safe for the A04s-only build, but confirm you do not
intend to support the other family devices before removing.

| Path | Why remove | Confidence |
|---|---|---|
| `firmware/npu/NPU.bin.ihex` | No `CONFIG_*` entry in `firmware/Makefile` references `npu/NPU.bin`; NPU firmware is not loaded by this kernel config. | MEDIUM |
| `firmware/sensorhub/shub_nacho_a12s.bin.ihex` | SHUB Makefile list does not include a12s; A12s device not in this tree. | MEDIUM |
| `firmware/sensorhub/shub_nacho_m12.bin.ihex` | Not in SHUB Makefile list. | MEDIUM |
| `firmware/sensorhub/shub_nacho_xcover5.bin.ihex` | Not in SHUB Makefile list. | MEDIUM |
| `firmware/tsp_novatek/nt36525c_a13x_boe.bin.ihex` | A13x panel, not referenced for the A04s build. | MEDIUM |
| `firmware/tsp_novatek/nt36525c_a13x_bringup.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36525c_a13x_mp_boe.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36525c_a13x_mp_bringup.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36525c_a13x_mp_sharp.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36525c_a13x_sharp.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36672_a13ve_csot.bin.ihex` | A13VE panel, not referenced. | MEDIUM |
| `firmware/tsp_novatek/nt36672_a13ve_csot_mp.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36672_a23_csot.bin.ihex` | A23 panel, not referenced. | MEDIUM |
| `firmware/tsp_novatek/nt36672_a23_csot_mp.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36672_a23_sharp.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36672_a23_sharp_mp.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36672_m23xq_csot.bin.ihex` | M23XQ panel, not referenced. | MEDIUM |
| `firmware/tsp_novatek/nt36672_m23xq_csot_mp.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36672_m23xq_tianma.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_novatek/nt36672_m23xq_tianma_mp.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_sec/hero.bin.ihex` | SEC touch panel firmware, not referenced (SEC_TS not enabled). | MEDIUM |
| `firmware/tsp_sec/hero_ub.bin.ihex` | Same | MEDIUM |
| `firmware/tsp_sec/y661_grace.fw.ihex` | Same | MEDIUM |
| `firmware/tsp_sec/y761_dream1.fw.ihex` | Same | MEDIUM |
| `firmware/tsp_synaptics/synaptics_b0_fac.fw.ihex` | Synaptics firmware, not referenced by the current config. | MEDIUM |
| `firmware/tsp_synaptics/synaptics_b0_h.fw.ihex` | Same | MEDIUM |
| `firmware/tsp_synaptics/synaptics_s5100_a2_k.fw.ihex` | Same | MEDIUM |
| `firmware/tsp_synaptics/synaptics_s5100_a2_k_FHD.fw.ihex` | Same | MEDIUM |
| `firmware/tsp_synaptics/synaptics_s5100_a2_k_WQHD.fw.ihex` | Same | MEDIUM |
| `firmware/tsp_synaptics/synaptics_s5100_a3_k_FHD.fw.ihex` | Same | MEDIUM |

## Unknown items requiring manual review

| Path | Why review | Confidence |
|---|---|---|
| `KernelSU-Next/kernel/KernelSU-Next` (symlink) | Broken symlink (points to a non-existent `../KernelSU-Next`). It matches the A04s stock KernelSU-Next layout, so it may be intentional; the build does not follow it. Decide whether to keep the stock layout or drop it. | LOW |
| `drivers/kernelsu` (symlink → `../KernelSU-Next/kernel`) | This is the committed, intentional layout (matches A04s stock) and the Kconfig/Makefile resolve through it — **do not remove**; listed only so the symlink structure is documented. | LOW |

## Notes

- The root `.gitignore` was regenerated to ignore generated content only
  (build artifacts, images, caches, logs, editor files, out-of-tree build
  directories). It anchors `/build/` and `/out/` to the repository root so
  tracked sources under `tools/build/` remain tracked, and it was verified
  to match **zero** tracked files (the 11 files reported as "ignored
  tracked" by `git ls-files -ci` are ignored by pre-existing
  subdirectory `.gitignore` files, not by the root file).
