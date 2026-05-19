# Freya

**A desktop app for orchestrating multi-repo GitHub Actions executions.** Plan a batch of `workflow_dispatch` triggers, run them in parallel or sequentially, handle approvals inline, and tail live logs — without leaving the app.

[![Latest release](https://img.shields.io/github/v/release/Falcighol/freya-app?label=latest&color=6366f1)](https://github.com/Falcighol/freya-app/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Falcighol/freya-app/total?color=6366f1)](https://github.com/Falcighol/freya-app/releases)
![Platforms](https://img.shields.io/badge/platforms-macOS%20%7C%20Windows%20%7C%20Linux-6366f1)

<!-- TODO: replace with a real screenshot before publishing the first release -->
<!-- ![Freya screenshot](docs/screenshot.png) -->

---

## What does Freya do?

If your release process involves triggering several `workflow_dispatch` workflows in a specific order — possibly with approval gates, scheduled timing, or different inputs per repo — the GitHub Actions UI starts to feel like a wall of tabs. Freya replaces those tabs with:

- **Plans**: named batches of workflow dispatches you run as a single unit.
- **Three plan types**:
  - **One-time** for a specific event (release night, hotfix).
  - **Recurring** for cadenced runs (nightly deploys) with a one-click "Run again".
  - **Template** for cloning into new plans — fill blanks once, reuse forever.
- **Parallel or sequential execution**, with sequential stopping on first failure.
- **Scheduled runs** (one-shot at a future time, or cron).
- **Inline log streaming** — tail GitHub Actions job logs without opening a browser tab.
- **Pre-flight checks** — verifies the ref exists, the workflow is active, and required inputs are filled *before* anything dispatches.
- **Approval handling** — environments with required reviewers surface inline; approve or reject from the app.
- **Run history** snapshots every terminal transition, so recurring plans build up a timeline.
- **Tag picker** for workflow inputs — search a repo's tags + commits with copy-to-clipboard.
- **Desktop notifications** on completion and on approval-required states.
- **Command palette** (⌘K / Ctrl+K) for jumping between plans and configs.
- **Auto-updates** built in — new releases roll out automatically.

---

## Download

Grab the latest version for your platform from the [latest release](https://github.com/Falcighol/freya-app/releases/latest).

### macOS

- **Apple Silicon (M1/M2/M3)** — download `Freya-<version>-arm64.dmg`.
- **Intel** — download `Freya-<version>-x64.dmg`.

Open the DMG and drag Freya into your Applications folder.

> First-launch note: Freya is currently distributed unsigned. macOS Gatekeeper will warn that "Freya can't be opened because Apple cannot check it for malicious software." To allow it: right-click `Freya.app` in Applications, choose **Open**, then click **Open** in the dialog. macOS remembers this for future launches.

### Windows

Download `Freya Setup <version>.exe` and run it. Windows SmartScreen may flag it as unrecognized; click **More info → Run anyway**. (We're working on code signing.)

### Linux

Download `Freya-<version>.AppImage`, make it executable, and run it:

```bash
chmod +x Freya-*.AppImage
./Freya-*.AppImage
```

---

## First-run setup

Freya needs a **GitHub Personal Access Token** to talk to the GitHub Actions API.

1. Generate a token at [github.com/settings/tokens](https://github.com/settings/tokens).
2. Required scopes:
   - **`repo`** — read repos, read workflows, read pending executions.
   - **`workflow`** — trigger `workflow_dispatch` events.
3. Open Freya → **Settings** → paste the token → **Save**.
4. Pick the organization or user account whose repos you want to work with.

Your token is stored locally on your machine. **Freya never sends it anywhere except `api.github.com`.**

---

## Auto-updates

Once you've installed Freya, you don't need to come back here. On every launch the app checks this releases page for a newer version, downloads it in the background, and prompts you to restart when it's ready. If you click **Later**, the update installs automatically the next time you quit the app — so you'll never end up on a stale version.

You can also trigger a manual check from **Settings → About → Check for updates**.

---

## Privacy & data handling

Freya is offline-first and zero-telemetry:

- **No backend.** There is no Freya server. The app talks directly to `api.github.com` from your machine.
- **No analytics.** Nothing about your usage leaves your device.
- **Local storage only.** Plans, saved configs, run history, and your GitHub token live in a JSON file under your OS's user-data directory:
  - macOS: `~/Library/Application Support/Freya/`
  - Windows: `%APPDATA%\Freya\`
  - Linux: `~/.config/Freya/`
- **Token scope.** The PAT you provide is the *only* credential the app uses. It's used for direct GitHub API calls; nothing else.

Want to clean up everything Freya stored? Delete the directory above and uninstall the app.

---

## Reporting issues

Found a bug, or want a feature? **[Open an issue](https://github.com/Falcighol/freya-app/issues/new)** on this repo. Include:

- Your OS + version
- Freya version (Settings → About)
- What you expected vs. what happened
- Steps to reproduce, if possible

The source code lives in a private repo, so PRs aren't open right now — but feedback is welcome.

---

## License & acknowledgments

Freya is a personal project by [@Falcighol](https://github.com/Falcighol). It would not exist without these excellent open-source projects: [Electron](https://www.electronjs.org/), [React](https://react.dev/), [Vite](https://vitejs.dev/), [Tailwind CSS](https://tailwindcss.com/), [Octokit](https://github.com/octokit), [Lucide](https://lucide.dev/), and [electron-builder](https://www.electron.build/).
