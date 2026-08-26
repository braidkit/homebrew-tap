# Braid Homebrew tap

Homebrew cask for the Braid CLI.

> **Nothing is published here yet.** The macOS cask ships with signed and
> notarized binaries, tracked in [braidkit/braid#282](https://github.com/braidkit/braid/issues/282).
> Everything below is the intended contract, not something that works today.

## What gets installed

Braid runs as a version-matched pair, and the cask installs both halves:

| Binary | Role |
| --- | --- |
| `braid` | the CLI you invoke |
| `braid-daemon` | the local daemon that holds lifecycle state |

Both report the same version, commit, and build date. Two halves that disagree
are a broken install, and `braid doctor` reports it as one.

## Install

```sh
brew tap braidkit/tap
brew install --cask braid
```

macOS on Intel and Apple Silicon. On Linux, use `install.sh` instead.

## What installing does not do

The cask places two binaries and an installation receipt. It does not:

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

`braid doctor` only reads, so it is safe against a live install.

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

Your work survives this. Uninstalling removes the binaries and the receipt.
`~/.braid` and every repository's `.braid` directory stay where they are, so
removing them has to be something you choose to do.

## Provenance

Casks in this tap point at [braidkit/braid-releases](https://github.com/braidkit/braid-releases).
Every version there publishes `checksums.txt`, an SPDX SBOM, and SLSA build
provenance next to the archives, so you can check what you downloaded against
the build that produced it.
