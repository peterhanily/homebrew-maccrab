# homebrew-maccrab

Official Homebrew tap for **[MacCrab](https://github.com/peterhanily/maccrab)** — a local-first macOS threat-detection engine.

## Install

```bash
brew install --cask peterhanily/maccrab/maccrab
```

That single command taps this repo automatically, trusts the cask (required by
Homebrew 6.0+), and installs the signed, notarized app into `/Applications`.

Then open `/Applications/MacCrab.app`, click **Enable Protection** on the
Overview tab, and approve the Endpoint Security extension in **System Settings →
General → Login Items & Extensions**. For full coverage, also grant **Full Disk
Access** in **System Settings → Privacy & Security**.

## Updating / uninstalling

```bash
brew upgrade --cask maccrab      # or use the in-app Sparkle auto-update
brew uninstall --cask maccrab    # add --zap to also remove app data
```

## About this repo

This is a **dedicated, append-only Homebrew tap**. It contains only the cask
definition; the application source lives at
[peterhanily/maccrab](https://github.com/peterhanily/maccrab). The cask here is
published automatically on each release from the app repo's release pipeline via
the GitHub Contents API — every update is a clean, forward-only commit, so
`brew update` always fast-forwards (this tap is never force-pushed/rebased).

If you previously tapped the application repo directly
(`brew tap peterhanily/maccrab https://github.com/peterhanily/maccrab`) and hit a
`could not apply …` rebase error on update, switch to this clean tap:

```bash
brew untap peterhanily/maccrab
brew install --cask peterhanily/maccrab/maccrab
```
