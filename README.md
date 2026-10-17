# BannerlordCoop-Optimized

An independent development edition of the Mount & Blade II: Bannerlord co-op campaign mod, maintained by [emreetosunn](https://github.com/emreetosunn).

[Report an issue](https://github.com/emreetosunn/BannerlordCoop-Optimized/issues) · [Source code](https://github.com/emreetosunn/BannerlordCoop-Optimized/tree/development) · [License](LICENSE)

## Overview

Play a shared Bannerlord campaign with other players, each controlling their own character and party. The codebase includes campaign synchronization, multiplayer battles, client connections, and dedicated server support.

This repository is based on [BannerlordCoop](https://github.com/Bannerlord-Coop-Team/BannerlordCoop). Development and issue tracking for this edition take place here.

## Current status

This is a source-code development repository. No downloadable release has been published for this edition yet.

The initial code import is complete. Performance and stability improvements are planned; no new gameplay optimizations or measured performance gains have been delivered by this edition yet. The project name describes the development goal.

## Development priorities

- Establish reproducible build and test results.
- Measure networking, serialization, and frame-time costs before changing behavior.
- Reduce unnecessary allocations and repeated work where measurements justify it.
- Validate campaign synchronization and multiplayer stability after changes.
- Publish release notes with tested changes and known limitations.

These are planned areas of work, not a list of completed features.

## Getting started

Clone the development branch:

```sh
git clone --branch development https://github.com/emreetosunn/BannerlordCoop-Optimized.git
cd BannerlordCoop-Optimized
```

Building the mod requires a Windows development environment, a local Bannerlord installation, Visual Studio/MSBuild, and the .NET tooling required by the projects. The main solution is `source/Coop.sln`. Game references are resolved through an `mb2` junction to the game installation.

Review `prepare-links.ps1` and `runmefirst.cmd` before running the repository setup. The setup also configures optional local testing tools; see the [testing tool setup](doc/automated-testing/mcp-setup.md).

To build the mod without deploying it into the game installation, run from a Visual Studio Developer Command Prompt after restoring dependencies and configuring the game path:

```bat
nuget restore source\Coop.sln
MSBuild.exe source\Coop\Coop.csproj /p:Configuration=Release /p:Platform=AnyCPU /p:ModName=
```

Builds with deployment enabled can write into the game's `Modules` directory. Full game-dependent builds and multiplayer testing have not yet been validated for this edition.

## Testing and compatibility

Use identical mod builds and game versions on all participating machines. The imported project documentation targets Bannerlord **v1.4.8**, with other mods and the War Sails DLC disabled; this edition has not independently verified that compatibility baseline.

Test projects are located alongside the application projects under `source/`. Game-dependent tests require the corresponding game assemblies and runtime environment.

Useful technical references:

- [Client and connection states](doc/ClientAndConnectionStates.md)
- [Server data locations](doc/ServerDataLocations.md)
- [Server-side Steam bans](doc/SteamBans.md)
- [Proximity voice](doc/ProximityVoice.md)

These documents were imported with the codebase and may describe upstream behavior or tooling.

## Bug reports and contributions

Use [this repository's issue tracker](https://github.com/emreetosunn/BannerlordCoop-Optimized/issues) for this edition. Include the commit or build used, game version, player count, reproduction steps, expected and actual behavior, and relevant client/server logs. Remove passwords and other private information before uploading logs.

Keep contributions focused. Performance changes should include a reproducible comparison; synchronization changes should include tests or a concrete multiplayer verification procedure.

## Credits and license

Original code: the BannerlordCoop contributors. Independent repository maintenance: [emreetosunn](https://github.com/emreetosunn). NoHarmony: [Salminar](https://github.com/Salminar/NoHarmony).

The existing source-available license is unchanged. See [LICENSE](LICENSE), [NOTICE.md](NOTICE.md), and the bundled [third-party notices](deploy/ThirdPartyNotices/README.txt). Public source access does not itself grant unrestricted reuse or redistribution rights.
