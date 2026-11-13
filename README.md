# Xiaomi Redmi 7 / Redmi Y3 (onclite) — UniXNU device port

Follow [Port a device](https://unixnu.com/porting/) from input collection
through publication. Complete the [driver adaptation
checklist](https://unixnu.com/porting/drivers) before selecting board-dependent
components.

## Hardware

- Codename: `onclite` (Redmi 7 / Redmi Y3)
- SoC: Qualcomm MSM8953 / Snapdragon 632 (ARMv8-A, Kryo 250)
- Display: 720 × 1520, 19:9 (~269 ppi)
- Storage: eMMC
- RAM: 2 / 3 / 4 GiB LPDDR3 (variant dependent)

## Repository setup

1. Copy this directory to `UniXNU-onclite` next to the UniXNU checkout.
2. Set the board name, firmware paths, and complete component selection in
   `board.toml`. Pin a reviewed SoC commit in `feeds.toml`.
3. Rename `configs/onclite_defconfig` and `dts/onclite.dts` values for the
   board; fill the memory map, CPU selection and peripherals in the DTS.
4. Pin the official firmware archive in `board.toml` `[firmware.image]` and
   list extracted inputs and hashes in `proprietary-files.txt`.
5. Set partition geometry and payload inputs from the device's records.
6. Match `porting.toml` identity to `board.toml`. Cover every selected
   component and dependency with board-specific ownership paths, findings and
   completion criteria.
7. Set `example = false` in `board.toml`, then run the packaging script and
   fix what it reports. Commit the generated `unixnu.lock`; keep local
   overrides in the ignored `local.toml`.

## Firmware reference

UEFI bring-up for MSM8953/onclite is tracked in
[ishakumari5/edk2-msm](../edk2-msm), which already carries onclite device
support (`Platform/Xiaomi/msm8953/onclite.dsc`, `onclite.fdf.inc`,
`Silicon/Qualcomm/msm8953/`, `FdtBlob_compat/onclite.dtb`). Build it with:

```sh
./edk2-msm/build.sh --device onclite
```

That repository is edk2-porting/Renegade based and is built with its own
`build.sh`; integrating it into the UniXNU Mu-Silicium firmware step
(`./unixnu build firmware --uefi ...`) is part of the onclite port.

## Local builds

From the UniXNU checkout:

```sh
./unixnu defconfig onclite_defconfig -D ../UniXNU-onclite
./unixnu fetch -D ../UniXNU-onclite
./unixnu status --json -D ../UniXNU-onclite
```

Read [boot arguments](https://unixnu.com/xnu/boot-arguments#apply-arguments)
before changing the command line. Rebuild the payload and boot image after
argument changes.

- [Device repository](https://unixnu.com/porting/device-repository)
- [Device tree](https://unixnu.com/porting/device-tree)
- [Component catalog](https://unixnu.com/reference/components)
- [UEFI firmware](https://unixnu.com/porting/uefi-firmware)
