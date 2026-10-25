# Flipper One Demo for Windows

![Platform](https://img.shields.io/badge/platform-Windows%2010%20%2F%2011-0078D6)
![Requires](https://img.shields.io/badge/requires-WSL%202-blue)
![Status](https://img.shields.io/badge/status-unofficial-orange)

Try the **Flipper One** user interface on any Windows PC – no device, no extra hardware, no manual setup.

A single double-click on `Flipper-One-Demo.bat` downloads everything it needs, sets up an isolated Linux environment, starts the FlipCTL test web UI and opens it in your browser.

> **Disclaimer:** This is an unofficial community project. It is **not** affiliated with or endorsed by Flipper Devices. This repository contains no Flipper software – the script only downloads publicly available files from the official servers on first run.

---

## Table of Contents

- [What is this?](#what-is-this)
- [Requirements](#requirements)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [What Gets Installed](#what-gets-installed)
- [Uninstalling](#uninstalling)
- [Troubleshooting](#troubleshooting)
- [Limitations](#limitations)
- [Security Note](#security-note)
- [Contributing](#contributing)
- [License](#license)

---

## What is this?

The Flipper One software is currently under active development and is, by design, meant to be run on the actual device. This project makes it possible to get a first impression of the interface – and to test it – directly on a Windows PC.

The demo runs the **FlipCTL test version** of the Flipper One UI. It is rendered in your browser and talks to a local test server, so everything works without real hardware. Features that depend on physical components (Wi-Fi, modem, battery, etc.) are **dummies**.

## Requirements

| Requirement | Details |
|---|---|
| **OS** | Windows 10 or Windows 11 |
| **WSL 2** | Windows Subsystem for Linux 2 (the script installs it for you if it is missing) |
| **Virtualization** | Must be enabled in the BIOS/UEFI |
| **Browser** | Microsoft Edge or Google Chrome |
| **Disk space** | Several GB. About 6 GB are needed temporarily while the image is unpacked |
| **Internet** | Required on the first run only (large download) |

## Quick Start

1. **Download** `Flipper-One-Demo.bat` from this repository.
2. **Double-click** the file.
3. **Wait** while the first-time setup runs (several GB of downloads, a few minutes).
4. Your browser opens automatically at `http://127.0.0.1:8899/` – done.

> **First time using WSL?** If WSL is not set up yet, the script starts its installation (you will be asked to confirm an administrator prompt). Afterwards **restart your PC** and double-click the `.bat` file again to continue.

## Usage

After the first setup, running the file shows a simple menu:

```
[1] Start and open in the browser (default)
[2] Stop
[3] Uninstall (removes everything again)
[4] Reinstall
[5] Show server log (if something goes wrong)
```

Press **Enter** to accept the default (start), or type a number and confirm.

### Start menu shortcuts

On the first successful run, two shortcuts are created in the Start menu under **Flipper One Demo**:

- **Start Flipper One**
- **Stop Flipper One**

### Command-line arguments

The script can also be run non-interactively:

```bat
Flipper-One-Demo.bat start   :: start the demo and open the browser
Flipper-One-Demo.bat stop    :: stop the server and the background browser
Flipper-One-Demo.bat log     :: show the last lines of the server log
```

### Stopping the demo

The demo keeps running in the background, even if you close the console window. To stop it, use one of the following:

- Start menu → **Flipper One Demo** → **Stop Flipper One**
- Run the `.bat` file again and choose **[2] Stop**
- Type `S` in the console window right after starting

## How It Works

1. **WSL check** – verifies that WSL 2 is available (and installs it if necessary).
2. **Private Linux environment** – imports a small Ubuntu 24.04 base system as a dedicated WSL distribution named `FlipperOne`. Your existing WSL distributions are not touched.
3. **Image extraction** – downloads the public Flipper One Linux image and extracts only the FlipCTL test web UI from it. The large image is deleted afterwards.
4. **Local server** – runs the test server with Node.js inside the private environment, listening on port `8899`.
5. **Device-style rendering** – starts a hidden Edge/Chrome instance that identifies itself like the device's browser, and opens the UI in your normal browser.

## What Gets Installed

On the first run, the following is downloaded from official sources:

| Component | Source |
|---|---|
| Public Flipper One Linux image (used only to extract the FlipCTL test UI) | `dl-linux-images.flipp.dev` |
| Ubuntu 24.04 WSL base system | `cloud-images.ubuntu.com` |
| Node.js 22.11.0 | `nodejs.org` |

Everything is stored in:

- `%LOCALAPPDATA%\FlipperOneDemo`
- a private WSL distribution named `FlipperOne`
- Start menu shortcuts under **Flipper One Demo**

Nothing is installed outside of these locations (apart from WSL itself, if it was missing).

## Uninstalling

Run the `.bat` file and choose **[3] Uninstall**. This stops the demo and removes the WSL distribution, all downloaded files and the Start menu shortcuts.

## Troubleshooting

| Problem | Solution |
|---|---|
| **"WSL could not be installed"** | Open an administrator PowerShell and run `wsl --install --no-distribution`, then restart your PC. |
| **"Import failed"** | Make sure virtualization is enabled in your BIOS/UEFI and that WSL 2 is available. |
| **"Loop devices are not available"** | Run `wsl --update` in PowerShell and try again. |
| **Download fails** | Check your internet connection and run the file again – interrupted downloads are resumed. |
| **Blank page or server not responding** | Choose **[5] Show server log** in the menu, or try **[4] Reinstall**. |
| **No browser found** | Install Microsoft Edge or Google Chrome. One of them is needed to render the UI. |

If the problem persists, please [open an issue](../../issues) and include the output of **[5] Show server log**.

## Limitations

- This is a **test/demo version** – there is no real hardware behind it.
- Wi-Fi, modem, battery and other hardware-related features are **dummies**.
- The demo is based on a specific public Flipper One image. Newer image versions may change the internal structure and require an update of this script.
- Requires WSL 2; not available on systems where virtualization is disabled or unsupported.

## Security Note

The `.bat` file launches an embedded PowerShell script using `-ExecutionPolicy Bypass` (only for this one process) and downloads several large files. As with any script from the internet, **please read it before you run it**. It is plain text and fully commented.

## Contributing

Bug reports, ideas and pull requests are welcome. If you want to contribute:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Open a pull request

## License

Add your license here (e.g. MIT). Note that this license covers **only the script in this repository**. All downloaded software remains under the licenses of its respective authors.

---

<sub>Flipper One and Flipper Devices are trademarks of their respective owners. This project is not affiliated with them.</sub>
