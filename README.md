# NSSM — Non-Sucking Service Manager

NSSM runs any Windows program as a service: start it at boot, restart it if it dies, capture logs.

The original project and documentation lived at [nssm.cc](http://nssm.cc/). That site is largely unmaintained and is not a source of current binaries or source. **Build from this repository:** [github.com/korygill/nssm](https://github.com/korygill/nssm).

This tree does **not** ship prebuilt `nssm.exe`. Build it locally with Visual Studio (see below), then copy `nssm.exe` onto your `PATH`.

Command-line usage, registry keys, and I/O redirection are documented in [README.txt](README.txt).

NSSM is public domain. You may unconditionally use it and/or its source code for any purpose.

## Build with Visual Studio

You need:

- [Visual Studio](https://visualstudio.microsoft.com/) with the **Desktop development with C++** workload (MSVC, Windows SDK). This solution uses toolset **v145** (Visual Studio 18). Older VS releases may need the Platform Toolset changed under Project → Properties → General.
- Git (the pre-build step runs `git describe` for the version stamp).

### IDE

1. Clone this repo and open `nssm.sln`.
2. Configuration: **Release**. Platform: **x64** (or Win32 if you need 32-bit).
3. Build → Build Solution (`Ctrl+Shift+B`).
4. The exe is `out\Release\win64\nssm.exe` (or `out\Release\win32\nssm.exe`).

Copy that `nssm.exe` to a directory on your `PATH`. There is no installer and no GitHub Releases upload.

### Developer PowerShell / MSBuild

From a **Developer PowerShell for Visual Studio** (or any shell where `msbuild` is on `PATH`):

```text
cd path\to\nssm
msbuild nssm.sln /p:Configuration=Release /p:Platform=x64
```

Output: `out\Release\win64\nssm.exe`.

`tmp\` and `out\` are build artifacts (gitignored). `version.h` is generated at build time from git tags.

## Smoke test

```text
nssm version
nssm install
```

The second command opens the GUI installer if you omit further arguments.

A worked example of wrapping a Python script as a service is [SetVolumeService](https://github.com/korygill/SetVolumeService) (quiet-hours volume). Same pattern as any other `nssm install <name> <exe> <args>`.
