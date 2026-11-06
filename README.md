# homebrew-maccrab

Official Homebrew tap for **[MacCrab](https://github.com/peterhanily/maccrab)** — a local-first macOS threat-detection engine.

## Install

```bash
brew install --cask peterhanily/maccrab/maccrab
```

That single command taps this repo automatically, trusts the cask (required by
Homebrew 6.0+), installs the signed, notarized app into `/Applications`, and
links `maccrabctl` and `maccrab-mcp` into Homebrew's `bin` directory. MacCrab
needs macOS 13 Ventura or later.

## First launch

1. Open `/Applications/MacCrab.app`. On first launch it asks macOS to load its
   Endpoint Security extension; the setup sheet ends with **Enable Protection**.
2. Approve the extension in **System Settings → General → Login Items &
   Extensions → Endpoint Security Extensions** (macOS 15 and later), or in
   **System Settings → Privacy & Security** (macOS 13 and 14).
3. For full detection coverage, grant **Full Disk Access** to MacCrab.app in
   **System Settings → Privacy & Security → Full Disk Access**.

## Updates

MacCrab updates itself. Its built-in updater checks once a day and, by
default, asks before installing; Homebrew installs get the same prompts as DMG
installs. Each release is offered to every Mac running MacCrab within about a
week. To update straight away, choose **Check for Updates…** from the MacCrab
menu-bar menu; in v1.22.6 and earlier, choose **Show Dashboard** first, or
Check for Updates… does nothing.

Homebrew can also upgrade it:

```bash
brew upgrade --cask peterhanily/maccrab/maccrab
```

Homebrew does not see an in-app update, so a later `brew upgrade` may reinstall
the version you already have.

## Uninstall

The cask deliberately leaves the system extension registered, because Homebrew
runs the same uninstall steps on every upgrade. Remove the extension first:

1. In MacCrab, open **Settings → General**, click **Remove System Extension**,
   confirm, and approve the macOS request.
2. Wait until `systemextensionsctl list` no longer shows a MacCrab entry,
   including a pending-removal entry. Restart first if macOS asks.
3. Uninstall the app:

   ```bash
   brew uninstall --cask peterhanily/maccrab/maccrab
   ```

Your alerts, baselines and settings stay in
`/Library/Application Support/MacCrab`. To move them to the Trash as well,
uninstall with `--zap`:

```bash
brew uninstall --zap --cask peterhanily/maccrab/maccrab
```

## Verifying what you install

The cask pins the DMG's SHA-256, and Homebrew refuses a download that does not
match. The same digest appears on the
[GitHub release page](https://github.com/peterhanily/maccrab/releases) and in
<https://maccrab.com/release.json>. [maccrab.com](https://maccrab.com) publishes
signature, notarization and update-signature checks for recent releases under
**Checks & known gaps**.

## About this repo

This is a **dedicated, append-only Homebrew tap**. It contains only the cask
definition; the application source lives at
[peterhanily/maccrab](https://github.com/peterhanily/maccrab). The cask here is
published automatically on each release from the app repo's release pipeline via
the GitHub Contents API — every update is a clean, forward-only commit, so
`brew update` always fast-forwards (this tap is never force-pushed/rebased).

If you previously tapped the application repo directly
(`brew tap peterhanily/maccrab https://github.com/peterhanily/maccrab`) and hit a
`could not apply …` rebase error on update, switch to this clean tap. First
check which version Homebrew recorded:

```bash
brew list --cask --versions maccrab
```

If it shows 1.3.7 or earlier, copy `/Library/Application Support/MacCrab`
somewhere safe first: Homebrew uninstalls with the cask it installed, and those
casks delete that folder. Then untap and reinstall. Recent Homebrew offers to
uninstall MacCrab before untapping; accept. Older versions refuse instead, so
run `brew uninstall --cask peterhanily/maccrab/maccrab` first.

```bash
brew untap peterhanily/maccrab
brew install --cask peterhanily/maccrab/maccrab
```

The system extension stays registered, and the reinstalled app activates it
again on first launch.
