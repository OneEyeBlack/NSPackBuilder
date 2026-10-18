# NSPackBuilder

[English](README.md) · [Português (Brasil)](README.pt-BR.md)

![NSPackBuilder banner](https://github.com/OneEyeBlack/NSPackBuilder/assets/153041521/5c4eeadb-d6b3-4cbd-8d73-9b4699d5a515)

**NSPackBuilder** is a Windows desktop utility for assembling, maintaining and deploying Nintendo Switch homebrew/CFW packages. It downloads selected components, builds a local package and can optionally copy it to an SD card or send it to a Switch over FTP.

> [!WARNING]
> This tool can format drives, erase SD-card data, write directly to physical NAND devices and inject payloads. These operations can cause irreversible data loss or render a device unusable when performed incorrectly. Always verify the selected drive, keep independent backups and use the software only with hardware and files you are authorized to use.

## What it does

- Select packages, sysmodules, homebrew applications and configuration files.
- Download release assets from configured repositories and show versions/download counts where available.
- Build a local package directory with progress and size information.
- Copy the package to a selected drive, optionally preserving selected folders.
- Format a drive as FAT32 or erase its contents while retaining selected data.
- Create and restore SD-card image files.
- Add a boot logo using the bundled Python scripts.
- Send a completed package to a Switch-compatible FTP server.
- Detect a Switch in RCM mode and inject a selected payload.
- Back up and restore NAND partitions through Hekate, with optional 7-Zip compression.
- Dump keys over FTP and migrate an emuNAND between key sets when required files are available.

## Package contents

The **Packages** area provides configured complete distributions such as Kefir, Ultra, CNX, GNX and HATS.

The **Sysmodules** area provides optional system modules and overlays such as Tesla Menu, Ultrahand Overlay, sys-clk, MissionControl, SaltyNX, NX-ovlloader, Sys-FTPD and Status Monitor.

The **Homebrew and files** area provides applications and supporting files such as DBI, Goldleaf, Hekate Toolbox, Linkalho, NX Activity Log, NX Dump Tool, NX Gallery, theme installers, hosts files, Hekate IPL files, boot files, patches and embedded configuration archives.

Available items and versions are defined by the configured repositories and may change over time.

## Typical workflow

1. Select the components to include.
2. Choose a local working directory.
3. Optionally enable **Release Versions** to query current release metadata.
4. Click **Start** to download assets and build the package.
5. Inspect the result with **Open Pack Folder**, copy it to an SD card with **Copy Pack to Drive**, or upload it with **Send over FTP**.
6. Verify the generated package before using it on a console.

**Repo** downloads the latest release of selected repository items without running the complete SD-card workflow. **Stop** cancels an active download operation, and **Restart** resets the current state.

## SD-card operations

The SD-card page provides:

- **Format now** — formats the selected drive as FAT32 and deletes all data on it.
- **Create Image** — creates an image file from the selected drive.
- **Restore Image** — writes an image file back to the selected drive.
- Drive-list refresh and safe-eject actions.

During package creation, **Format SDCard** and **Erase SDcard / Keep emuMMC** are separate options. Formatting uses the Windows formatting API; erasing removes package data while allowing configured folders such as emuMMC, Nintendo, atmosphere\contents, DBISaves, bootloader\nyx.ini and theme data to be retained.

Always verify the selected drive letter. Removable-drive letters can change when media is connected or disconnected.

## Boot logos and payloads

The **Bootlogo** page adds a bundled boot-logo asset to a selected firmware package. NSPackBuilder invokes the included Python runtime/scripts to generate the required files.

The **Boot / Payload** page monitors USB for a Switch in RCM mode, lists .bin payloads found in the application's payloads directory and uses TegraRcmSmash.exe to inject the selected payload.

## NAND and emuNAND tools

Advanced tools can:

- Back up selected NAND partitions with progress, speed and ETA information.
- Restore a NAND partition from a backup after explicit confirmation.
- Validate NAND backups and report detected partition information.
- Inject Hekate, wait for the NAND device to appear in Windows and perform the requested operation.
- Dump Switch keys with Lockpick_RCM_Pro, retrieve them over FTP and save prod.keys/title.keys.
- Convert an emuNAND using old and new key sets.

These operations require the appropriate Hekate, Lockpick and TegraRcmSmash files, a compatible Switch setup and, for physical NAND access, elevated Windows privileges. Read the bundled user guide first.

## FTP transfer

The FTP dialog supports anonymous or authenticated connections, configurable host/port, remote-directory navigation, overwrite/skip decisions and recursive package upload. Preferences are stored in SendFTP.ini beside the executable. Treat that file as sensitive when it contains credentials.

## Requirements

- Windows 10 or later is recommended.
- A 32-bit Windows build of NSPackBuilder and its accompanying files.
- Internet access for repository and release downloads.
- A local working directory with sufficient free space.
- Administrator privileges for formatting, physical-drive access and some NAND operations.
- A compatible SD-card reader for SD-card workflows.
- Required payloads and helper executables for RCM/NAND features.

Keep the expected folder structure intact when moving the executable. The distributed Win32\\Debug/Win32\\Release folders contain helper files such as TegraRcmSmash.exe, fat32format.exe, payloads, DLLs and the bundled Python runtime.

## Building from source

NSPackBuilder is a Delphi VCL application. The main project file is NSPackBuilder.dproj, the entry point is NSPackBuilder.dpr, and source units are in the sources directory.

To build in RAD Studio:

1. Open NSPackBuilder.dproj.
2. Select the **Win32** target platform.
3. Configure the Delphi and DevExpress dependencies referenced by the project.
4. Verify that the docs, resources, payload and helper-runtime paths are available.
5. Build the **Release** configuration and distribute the executable with its required runtime files.

The project embeds some resources into the executable while other assets remain external. A successful compilation alone does not produce a complete portable distribution.

## Project layout

| Path | Purpose |
| --- | --- |
| sources/ | Delphi forms, UI logic, download/package workflow and NAND/FTP code |
| resources/ | Embedded package archives and configuration resources |
| Python/ | Bundled Python runtime and boot-image scripts |
| docs/ | User guides and guide images |
| image/, icons/ | UI artwork and application icons |
| Win32/Debug/, Win32/Release/ | Build output and runtime distribution files |
| Dcu/ | Delphi compiled unit output |

## Credits and support

NSPackBuilder combines files and release assets from multiple independent open-source projects. Their licenses and usage conditions continue to apply to the corresponding components.

For suggestions, bug reports or feedback, use the project's [GitHub repository](https://github.com/OneEyeBlack/NSPackBuilder).

![Downloads](https://img.shields.io/github/downloads/OneEyeBlack/NSPackBuilder/total)
![Stars](https://img.shields.io/github/stars/OneEyeBlack/NSPackBuilder)

