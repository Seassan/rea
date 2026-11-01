# REA: remember it as “Reverse Engineer Anything”

**Use this repo when you want to understand how an existing app or binary works, even without its source code.**

REA gives Codex and other AI agents a shared set of reverse-engineering tools through MCP (Model Context Protocol). You can also use those tools from the terminal.

Examples of questions to ask:

- “Explain the structure of this Electron app and find where it handles updates.”
- “Inspect this binary with Ghidra and explain the relevant functions.”
- “Inspect this Android APK with JADX and explain its classes.”

Analysis results include evidence and limitations. Available operations depend on the installed providers and the target.

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

## Origin

This project comes from [morluto/rea](https://github.com/morluto/rea) and is licensed under the [MIT license](LICENSE). A personal fork preserves the original project and provides a place for your own changes.
