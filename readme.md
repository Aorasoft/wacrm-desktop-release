# Install Aora WACRM Desktop

One-line install scripts for macOS and Windows. They download the latest **published** release from
`Aorasoft/wacrm-desktop-release`. If no release is published yet (only a draft), the scripts fail with a 404.

The scripts download with `curl` or PowerShell, which do not add the browser mark that triggers the macOS
"cannot verify the developer" prompt or the Windows SmartScreen "unknown publisher" screen.

## macOS

Open **Terminal** and run:

```bash
curl -fsSL https://github.com/Aorasoft/wacrm-desktop-release/releases/latest/download/install.sh | bash
```

- Installs the app into `/Applications` and opens it.
- Works on Apple silicon and Intel.
- Options (environment variables): `WACRM_REPO` (another releases repository), `WACRM_APPS_DIR` (install folder, default `/Applications`), `WACRM_NO_OPEN=1` (do not open the app after install).

Example with options:

```bash
WACRM_APPS_DIR="$HOME/Applications" WACRM_NO_OPEN=1 \
  curl -fsSL https://github.com/Aorasoft/wacrm-desktop-release/releases/latest/download/install.sh | bash
```

## Windows

Open **PowerShell** and run:

```powershell
irm https://github.com/Aorasoft/wacrm-desktop-release/releases/latest/download/install.ps1 | iex
```

- Downloads the latest installer and runs it silently.
- Options (environment variables): `WACRM_REPO` (another releases repository), `WACRM_INTERACTIVE=1` (show the installer wizard).

Example with the wizard:

```powershell
$env:WACRM_INTERACTIVE = "1"
irm https://github.com/Aorasoft/wacrm-desktop-release/releases/latest/download/install.ps1 | iex
```

## Install by hand (shows a warning)

Download from the [latest release](https://github.com/Aorasoft/wacrm-desktop-release/releases/latest):

- macOS: the `.dmg` for your chip (Apple silicon or Intel). If macOS blocks it, right-click the app, choose Open, then confirm.
- Windows: the `.exe` installer. If SmartScreen shows "unknown publisher", choose More info, then Run anyway.

## Updates

Installed apps check for updates 20 seconds after start and then every 4 hours, and install them from the same releases repository. You do not run the scripts again.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| `404` or "not found" from the script | No release is published yet, or the repository is private. A draft release is not visible. |
| `curl: command not found` (macOS) | Use the `.dmg` download by hand. |
| PowerShell blocks the script | Run PowerShell as normal user and use the exact `irm ... \| iex` line; do not save and run a `.ps1` file. |
| App does not update | Check the app version in Settings, Updates, Check for updates. Updates need a published release newer than the installed version. |

Release process for maintainers: [wacrm-desktop-release.md](wacrm-desktop-release.md).
