# Progress Forge

This public repository distributes Progress Forge CLI releases. The source code is maintained separately.

## Install Forge

The release installers have stable asset names, so the latest release can be installed directly.

Linux or macOS:

```bash
curl -fsSL https://github.com/telerik/forge/releases/latest/download/install.sh | sh
```

Windows with PowerShell 7:

```powershell
Invoke-WebRequest -Uri 'https://github.com/telerik/forge/releases/latest/download/install.ps1' -OutFile install.ps1
.\install.ps1
```

Open a new terminal after installation, then verify:

```bash
frg --version
```

## Documentation

Read the [Forge documentation](https://www.telerik.com/forge/documentation).

## Releases

GitHub Releases contain the Forge CLI binaries, installers (`install.sh` and `install.ps1`), packages, checksums, and signatures.
