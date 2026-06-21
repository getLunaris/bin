# Lunaris Engine Binaries

This repository contains pre-compiled standalone executable binaries for the Lunaris Engine daemon, and the packaged VS Code extension (`.vsix`).

## Recommended Installation

The install script downloads the engine binary, installs the native dependencies, and configures your shell `PATH` automatically:

**macOS / Linux:**
```bash
curl -fsSL https://getlunaris.dev/install.sh | bash
```

**Windows (PowerShell):**
```powershell
Invoke-WebRequest -Uri 'https://getlunaris.dev/install.ps1' -OutFile "$env:TEMP\install.ps1" -UseBasicParsing; & "$env:TEMP\install.ps1"; Remove-Item "$env:TEMP\install.ps1"
```

> [!NOTE]
> If the VS Code extension detects that no engine binary is installed, it will run the install script automatically via an integrated terminal.

---

## VS Code Extension

Each release includes a `.vsix` package. The extension checks for updates on startup (once per 24 hours) against this repository and will prompt you to install new versions directly from the editor.

To install the extension manually from a release:
```bash
code --install-extension getlunaris-v0.0.2.vsix
```

---

## Manual Installation

If you prefer to install the engine binary manually instead of using the install script:

### Supported Platforms

| Binary | OS | Architecture |
|---|---|---|
| `lunaris-linux-x64` | Linux | x86_64 |
| `lunaris-darwin-arm64` | macOS | Apple Silicon (M-series) |
| `lunaris-win32-x64.exe` | Windows | x86_64 |

### 1. Download the Binary

Download the correct binary for your operating system and CPU architecture from the [Releases](https://github.com/getLunaris/bin/releases) page.

### 2. Grant Execution Permissions (macOS / Linux)

```bash
chmod +x lunaris-darwin-arm64
```

### 3. Install Native Dependencies

The engine requires platform-specific native Node modules (LanceDB, node-pty, tree-sitter grammars, etc.) that cannot be embedded into the single executable. Each release includes a companion dependency archive.

Download the matching archive and extract it into `~/.lunaris/`:

**macOS / Linux:**
```bash
mkdir -p ~/.lunaris
tar -xzf lunaris-deps-darwin-arm64.tar.gz -C ~/.lunaris/
```

**Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.lunaris"
Expand-Archive -Path lunaris-deps-win32-x64.zip -DestinationPath "$env:USERPROFILE\.lunaris\"
```

This creates the `~/.lunaris/node_modules/` directory the engine resolves against at runtime.

### 4. Configure the VS Code Extension

Set `lunaris.enginePath` in your VS Code settings to the absolute path of the downloaded binary:

```json
"lunaris.enginePath": "/absolute/path/to/lunaris-darwin-arm64"
```

If the binary is on your system `PATH`, the default value (`lunaris`) resolves it automatically.

### macOS Gatekeeper

If macOS blocks the binary, open **System Settings > Privacy & Security** and click **Allow Anyway**, or run:

```bash
xattr -d com.apple.quarantine lunaris-darwin-arm64
```

---

## Release Artifacts

Each tagged release publishes the following assets:

| Asset | Description |
|---|---|
| `lunaris-linux-x64` | Engine binary (Linux x64) |
| `lunaris-darwin-arm64` | Engine binary (macOS ARM64) |
| `lunaris-win32-x64.exe` | Engine binary (Windows x64) |
| `lunaris-deps-linux-x64.tar.gz` | Native dependencies (Linux x64) |
| `lunaris-deps-darwin-arm64.tar.gz` | Native dependencies (macOS ARM64) |
| `lunaris-deps-win32-x64.zip` | Native dependencies (Windows x64) |
| `getlunaris-*.vsix` | VS Code extension package |
| `playwright-version.txt` | Required Playwright version for browser tools |

## License

This software is proprietary and confidential. All rights reserved. Unauthorized copying, distribution, or modification of these binaries via any medium is strictly prohibited.
