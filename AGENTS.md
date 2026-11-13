# onclite device agent guide

This repository owns the board DTS, peripheral wiring, component selections,
firmware inputs, partition layout, and packaging for the Xiaomi Redmi 7
(onclite, MSM8953).

## Read first

Read this README and the following UniXNU documentation before changing the port:

| Task | Required reading |
| --- | --- |
| Every port | [Porting](https://unixnu.com/porting/), [device repository](https://unixnu.com/porting/device-repository), [component catalog](https://unixnu.com/reference/components), UniXNU `components.toml` |
| Hardware | [Device tree](https://unixnu.com/porting/device-tree), [matching](https://unixnu.com/drivers/device-tree-matching), selected SoC README/AGENTS/soc.toml/DTSI |
| Component | Its site page, README, catalog build command, dependencies and source |
| Kernel | [Source and patches](https://unixnu.com/xnu/source-and-patches), [patch reference](https://unixnu.com/xnu/patch-reference), selected OS profile |
| Images | [Prelink](https://unixnu.com/concepts/prelink), [payload](https://unixnu.com/concepts/payload), [UEFI](https://unixnu.com/porting/uefi-firmware) |
| Verification | [Building](https://unixnu.com/building), [bring-up](https://unixnu.com/porting/bring-up) |

## Work

Search the catalog and inspect existing component interfaces before adding code.
Match hardware scope, OS ABI, and board dependencies. Shared SoC resources belong
in UniXNU-msm8953-common. Reusable drivers belong in their component
repositories. Use canonical component IDs.

Replace every `REQUIRED_` value, set the board name and firmware paths, and
select the complete dependency set. Verify memory ranges, CPU affinities,
interrupts, firmware hashes, and partition geometry from board evidence.
Set `example = false` after completing the inputs. Pin the SoC commit and
inspect resolved profiles.

The firmware reference is ishakumari5/edk2-msm (onclite support), built with
`build.sh --device onclite`; integrating it into the UniXNU firmware step is
part of this port.
