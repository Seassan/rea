# REA: remember it as “Reverse Engineer Anything”

**Use this repo when you want to understand how an existing app or binary works, even without its source code.**

REA gives Codex and other AI agents a shared set of reverse-engineering tools through MCP (Model Context Protocol). You can also use those tools from the terminal.

Examples of questions to ask:

- “Explain the structure of this Electron app and find where it handles updates.”
- “Inspect this binary with Ghidra and explain the relevant functions.”
- “Inspect this Android APK with JADX and explain its classes.”

Analysis results include evidence and limitations. Available operations depend on the installed providers and the target.

## How to ask for REA

In Codex, say **“Use REA from Seassan/rea to inspect this file”** and provide the file or its path. For example:

- “Use REA and Ghidra to explain this Windows EXE or DLL.”
- “Use REA and JADX to inspect this Android APK.”
- “Use ADB to list connected Android devices.”

In a new chat, include the repo URL: <https://github.com/Seassan/rea>. The agent needs access to the file and a configured REA installation.

## Where to start

- [README](README.md): overview and supported targets.
- [Installation](docs/installation.md): MCP registration and provider setup.
- [CLI guide](docs/cli.md): terminal commands.
- [MCP contracts](docs/mcp-contracts.md): tools available to agents.

## This cloud workspace

The checkout lives at `/workspace/rea`. In a new terminal:

```sh
source /workspace/rea-activate.sh
cd /workspace/rea
rea --version
rea mcp doctor --json
```

The initial setup installed the pinned Node.js/npm dependencies, Ghidra, JADX, a full JDK, Python analysis tools, and the Codex MCP registration. The workspace setup report is `/workspace/REA-SETUP.md`.

The activation script, downloaded tools, and client configuration belong to this cloud environment. A GitHub clone does not include those installations. Follow the installation guide to set up another machine.

## Free Windows binary and Android tools

These tools are installed in the Linux cloud workspace:

| Tool                       | Version   | Purpose                                                            |
| -------------------------- | --------- | ------------------------------------------------------------------ |
| Ghidra                     | 12.1.4    | Static analysis and decompilation, including Windows EXE/DLL files |
| Eclipse Temurin JDK        | 21.0.13+9 | Java runtime and compiler used by Ghidra and JADX                  |
| JADX headless MCP          | 0.7.1     | REA's Android APK analysis provider                                |
| Android SDK Platform-Tools | 37.0.1    | Includes ADB and Fastboot for Android device access                |

After activating the workspace shell, verify with:

```sh
java -version
javac -version
adb version
rea doctor --provider ghidra --provider jadx --json
```

Ghidra on Linux can inspect Windows binaries. Running a Windows program or debugging its live Windows process requires a suitable Windows environment. JADX here is the headless MCP provider, rather than the standalone graphical JADX app.

ADB requires a reachable Android device or emulator for device operations. Installing it in the cloud does not connect a phone plugged into your desktop. Static APK analysis with JADX does not need a device.

GitHub stores this guide and REA's source, not a running installation. To prepare another machine, obtain the matching OS downloads from the official projects, then follow [REA installation](docs/installation.md):

- [Ghidra releases](https://github.com/NationalSecurityAgency/ghidra/releases)
- [Temurin JDK downloads](https://adoptium.net/temurin/releases/)
- [JADX headless MCP 0.7.1](https://github.com/1013503897/jadx-headless-mcp/releases/tag/v0.7.1)
- [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools)

Set `JAVA_HOME` to your full JDK directory, `GHIDRA_INSTALL_DIR` to your extracted Ghidra directory, and `REA_JADX_MCP_JAR` to the absolute path of the downloaded JADX MCP JAR. Add the JDK `bin` and Android `platform-tools` directories to `PATH`. Register REA using `rea setup --client codex`, review its plan, and restart Codex.

## Origin

This project comes from [morluto/rea](https://github.com/morluto/rea) and is licensed under the [MIT license](LICENSE). A personal fork preserves the original project and provides a place for your own changes.
