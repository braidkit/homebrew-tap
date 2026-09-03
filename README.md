# Braid Homebrew tap

Homebrew casks for the Braid CLI.

> No cask has been published to this tap yet. The macOS cask ships once the
> binaries are signed and notarized.

## Install

```sh
brew tap braidkit/tap
brew install --cask braid
```

macOS on Intel and Apple Silicon. On Linux, use the installer:

```sh
curl -fsSL https://braidkit.io/cli/install.sh | bash
```

## What gets installed

Braid runs as a version-matched pair, and the cask installs both halves:

| Binary | Role |
| --- | --- |
| `braid` | the CLI you invoke |
| `braid-daemon` | the local daemon that holds lifecycle state |

Shell completions for bash, zsh, and fish are installed alongside them.

Both report the same version, commit, and build date. An install where they
disagree is a broken install, and `braid doctor` reports it as one.

## What installing does not do

The cask places two binaries and their completions. Homebrew records the
install in its own receipt; nothing writes a Braid installation receipt, which
is why `braid uninstall` leaves a Homebrew installation to Homebrew. The cask
does not:

- create `~/.braid`, which the first stateful Braid command creates with
  owner-only permissions
- start `braid-daemon`, or register it as a launch service
- edit your shell profile
- install agent hooks

## Verify

```sh
braid --version
braid-daemon --version
braid doctor
```

`braid doctor` only reads, so it is safe to run against a live install.

## Update

```sh
brew update
brew upgrade --cask braid
```

## Uninstall

```sh
brew uninstall --cask braid
brew untap braidkit/tap
```

Use Homebrew rather than `braid uninstall`, which reads a receipt this
installation never wrote and will decline to touch it.

Your work survives this. Uninstalling removes the binaries and their
completions. `~/.braid` and each repository's `.braid` directory stay where they
are, so removing them has to be something you choose to do.

## Provenance

Casks in this tap point at `https://braidkit.io/cli/releases/<tag>/`, the same
artifacts the installer downloads. Each version publishes `checksums.txt` next
to its archives, and every cask pins the exact SHA-256 of the archive it
installs, so Homebrew rejects a download whose bytes have changed.
