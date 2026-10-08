# MCP Pacemaker for Homebrew

The product-specific Homebrew tap for [MCP Pacemaker](https://github.com/girishkvs/mcp-pacemaker), a local MCP process supervisor and transport bridge.

## Install

For a new installation, add the tap and trust this formula once:

```sh
brew tap girishkvs/mcp-pacemaker
brew trust --formula girishkvs/mcp-pacemaker/mcp-pacemaker
```

Then use the short product command:

```sh
brew install mcp-pacemaker
```

Or install with one fully qualified command:

```sh
brew install girishkvs/mcp-pacemaker/mcp-pacemaker
```

The one-command form adds the tap if needed and trusts only this formula. Homebrew 6 requires explicit trust for third-party formulas; `brew tap` alone does not grant it. See [Homebrew's tap trust documentation](https://docs.brew.sh/Tap-Trust).

## Existing Homebrew installations

The original [girishkvs/homebrew-tap](https://github.com/girishkvs/homebrew-tap) remains available. Existing configured users should keep their current installation; this tap is not an automatic migration.

If both `girishkvs/tap` and `girishkvs/mcp-pacemaker` are tapped, they define the same `mcp-pacemaker` formula name. Do not rely on the short name in that case: Homebrew can report an ambiguous formula. A fully qualified name selects a tap, but does not create a separate installation or prove a safe switch between taps.

No retapping, reinstall, upgrade or configured migration procedure is provided here.

## Version and tested scope

This formula installs **2.0.2** from the checksum-pinned npm archive, with Homebrew `node@24` and the original dependency lock from source commit [`a9fd5be23a50d4f3e3b787b678a8e85bdfb45fa2`](https://github.com/girishkvs/mcp-pacemaker/tree/a9fd5be23a50d4f3e3b787b678a8e85bdfb45fa2). It uses `npm ci` and retains Homebrew's cooldown and script restrictions.

These exact formula bytes passed a canary on **macOS 15.7.9 ARM64, Homebrew 6.0.22**: syntax/style/audit, installation, all 48 locked production dependency versions, CLI help, `brew test`, an installed MCP round trip and unconfigured package removal.

Configured launchd setup/teardown, reboot/login, product upgrades, Node upgrades and Cellar cleanup are **not qualified**. Intel macOS and Linux are not qualified. The later process-leak and safe-upgrade fixes are **not included in 2.0.2**; no crash-safety guarantee across abrupt loss is claimed.

## Explicit setup

Package installation adds `mcp-pacemaker` and `mcp-bridge` only. It does not run setup or create a `brew services` job.

Back up your host configuration and review the [2.0.2 setup guide](https://github.com/girishkvs/mcp-pacemaker/blob/a9fd5be23a50d4f3e3b787b678a8e85bdfb45fa2/README.md) before opting in:

```sh
mcp-pacemaker init
```

Setup can change host MCP settings, import server definitions and register OS auto-start.

## Permanent removal

For an installation from this tap, review the [2.0.2 removal notes](https://github.com/girishkvs/mcp-pacemaker/blob/a9fd5be23a50d4f3e3b787b678a8e85bdfb45fa2/README.md#uninstall). If configured, run the installed CLI's teardown before removing the package:

```sh
mcp-pacemaker uninstall
brew uninstall girishkvs/mcp-pacemaker/mcp-pacemaker
```

An unconfigured installation only needs `brew uninstall`. This is permanent removal, not an upgrade or tap-switch procedure.

Product teardown affects managed bridges beyond one port and restores whole available host-file backups, so later edits can be lost. On macOS it unloads auto-start, but the launchd plist can remain. Files without backups and native Claude Code registrations remain unchanged. Data under `~/.mcp-pacemaker` is user data, not package payload.

## License

[MIT](LICENSE).
