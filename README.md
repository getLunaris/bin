# Lunaris Engine Binaries

This repository contains the pre-compiled, standalone executable binaries for the engine daemon.

## Installation & Usage

1. Download the correct binary for your host operating system and CPU architecture from the [Releases](https://github.com/getLunaris/bin/releases) page:
   - `lunaris-linux-x64`
   - `lunaris-darwin-arm64` (Apple Silicon macOS)

2. Grant execution permissions to the downloaded binary:
   ```bash
   chmod +x lunaris-darwin-arm64
   ```

3. Configure your VS Code extension settings (`lunaris.enginePath`) to point to the absolute path of the downloaded binary:
   ```json
   "lunaris.enginePath": "/absolute/path/to/lunaris-darwin-arm64"
   ```

