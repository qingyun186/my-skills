---
name: rea-reverse-engineering
description: "Reverse engineering tool powered by rea-agents (morluto/rea, 416k stars). Use when analyzing JavaScript/Electron apps, inspecting binaries, understanding app behavior without source code, or tracing how features work. Supports static JS analysis, .NET assemblies, APK resources, and website inspection via CLI. Installed globally via npm."
---

# Rea Reverse Engineering

## Quick Start

Rea is installed globally as `rea` CLI. Run `rea --help` to see all commands.

```bash
# Check environment readiness
rea doctor

# Analyze a local JavaScript/Electron app directory
rea analyze-javascript-application /path/to/app --json

# Get an overview of an app
rea analyze /path/to/app
```

## Core Capabilities

### JavaScript / Electron Analysis
Static analysis of local JS/Electron applications without running them. Returns modules, imports, IPC boundaries, and source relationships.

```bash
rea analyze-javascript-application /absolute/path/to/app --json
```

Requirements: Node.js 22.x+. No native analysis engine needed.

### App Overview
High-level inventory of an application: runtime candidates, supporting files, component markers.

```bash
rea analyze /path/to/app
```

### Other Supported Targets
- **.NET assemblies** - metadata, CIL instructions (static only, no engine needed)
- **Android APKs** - manifest, resources (requires JADX + JDK)
- **Websites** - page structure, scripts, network observations (requires Chrome browser)
- **Native binaries** - pseudocode, assembly (requires Hopper/Ghidra/IDA/Kuna)

### Environment Check
```bash
rea doctor
```
Shows which providers are installed and ready. Native analysis engines (Hopper, Ghidra, IDA) are optional; static JS and .NET analysis work without them.

## Common Workflows

### Understand how an Electron feature works
1. Point rea at the app directory
2. Run `analyze-javascript-application` to get the module graph
3. Use `decompile` or `decompile-jeb-item` to read specific parts
4. Trace IPC calls from renderer to main process

### Analyze a downloaded APK
1. Ensure JADX and JDK are installed
2. Run `rea analyze` on the APK file
3. Use `decode-android-resources` for manifest and strings

## Limitations

- Native binary analysis requires external tools (Hopper, Ghidra, IDA, Kuna) - not bundled
- Website analysis requires a Chrome-family browser
- APK analysis requires JADX + full JDK
- All analysis runs locally; no data uploaded

## Installation

Already installed globally via `npm install -g rea-agents`. Version: 6.7.0.

Update: `rea update` or `npm install -g rea-agents@latest`.
