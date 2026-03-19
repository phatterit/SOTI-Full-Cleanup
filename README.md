# SOTI MobiControl Deep Cleaner for Windows CE/Mobile

A powerful, automated MortScript utility designed to completely uninstall and eradicate all traces of the SOTI MobiControl agent from legacy Windows CE and Windows Mobile devices (e.g., Motorola MC9090).

When migrating legacy devices to a new SOTI server or troubleshooting connection issues (like SHA-1/SHA-256 certificate mismatch), standard uninstallation often leaves behind hidden configurations, locked `.ini` files, and watchdog processes. This script ensures a clean slate for re-enrollment.

## Features

* **Aggressive Process Termination:** Safely exits and forcefully kills persistent background watchdogs (`CommLoader.exe`, `PkCtrlSv.exe`, `MobiControl.exe`) that block file deletion.
* **Attribute Stripping:** Automatically removes `Read-Only`, `System`, and `Hidden` attributes from configuration files before attempting deletion.
* **Deep Wipe:** Scans and removes agent remnants (`pdb.ini`, `.log`, `.pcg`, `.dll`) across multiple common storage partitions (`\Application`, `\IPSM`, `\Flash`, `\Windows`).
* **ASCII-Only:** 100% standard ASCII text, ensuring compatibility with old Windows CE interpreters without encoding errors.

## Requirements

* A Windows CE / Windows Mobile device.
* **MortScript** engine installed or bundled with the script.

## Usage

1. Copy `MortScript.exe`, your compiled `CleanSoti.exe` (autorun), and the `CleanSoti.mscr` script to a directory on the device (e.g., `\Application\CleanSoti`).
2. Run the executable.
3. Follow the on-screen prompts. The script will guide you through 3 steps:
   * **Step 1:** Terminating processes.
   * **Step 2:** Running the native uninstaller and sweeping directories.
   * **Step 3:** Final prompt.
   
**Important Note:** The Windows CE OS will sometimes place an unbreakable "file lock" on the `pdb.ini` or `pdb` database file. If this happens, the script will notify you in Step 3 to manually delete this file via the device's File Explorer before rebooting.

## Deployment via SOTI Package Studio

This script is highly suitable for remote deployment via the old MDM server prior to migration:
1. Open SOTI Package Studio.
2. Create a package targeting `Windows CE` / `ALL` processors.
3. Do **NOT** add this script as a "Pre-Install" or "Post-Install" script (it will kill the agent mid-download).
4. Simply deploy the files to a local directory and create a shortcut in `\Windows\Start Menu\Programs` for the local administrator to trigger manually.

## License
MIT License. Feel free to fork and modify for your specific device architecture.
