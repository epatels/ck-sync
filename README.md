# CK Sync

**Keeps two folders in step, safely.** CK Sync shows you what it is about to do and why, before it changes
anything. Whatever it replaces or deletes is kept in a backup folder. It can also sync by itself on a
schedule, even when nobody is logged in.

[**Download the latest version**](https://github.com/epatels/ck-sync/releases/latest) · Windows 10 or 11, 64-bit

```
winget install epatels.CKSync
```

*(The winget command works once the package has been approved in the Windows Package Manager catalogue.)*

## What it does

- **Two-way sync of folder pairs.** Pick a left and a right folder: a local folder, a pen drive, an external
  disk, or a network share. New and changed files are carried both ways, and a deletion on one side is carried
  to the other.
- **Preview first.** *Preview* lists every file CK Sync would copy, replace, keep or delete, with the reason
  for each. Nothing changes until you press *Sync* and confirm.
- **Safe by design.**
  - Anything replaced or deleted is moved to a hidden `.cksyncbackup` folder next to it and kept for 60 days.
  - If both sides changed the same file, **both versions are kept**; nothing is overwritten silently.
  - A sync that would delete or replace a large share of your files (more than 20 percent, and at least 10
    files) is stopped for you to check first.
  - A folder that is suddenly empty, or a drive that is not connected, is never treated as "everything was
    deleted".
  - It checks free space first, and skips files that changed while it was working.
- **Live status for every pair.** The pair list shows a turning ring while a pair is being checked or synced,
  a green tick when it is finished or already in step, and a clear warning when something needs a look.
- **Sync by itself, even when logged out.** Choose which pairs to keep in step and how often (from every 15
  minutes to once a day). It runs through Windows Task Scheduler, also with nobody logged in. If anything looks
  wrong it holds that pair back and changes nothing.
- **Command line.** `CK_Sync_cli.exe` does the same without a window, for scripts and schedulers.
- **Updates itself.** It checks this page once a day. An update is installed only if it carries the
  developer's signature and matches its checksum, and never while a sync is running.
- **Private.** No usage statistics, no tracking, no accounts. The only thing CK Sync ever contacts is GitHub,
  to ask whether a newer version exists.

## Install

1. Download `CK_Sync_Setup_<version>.exe` from the [Releases page](https://github.com/epatels/ck-sync/releases/latest).
2. Run it. No administrator rights are needed unless you choose to install for all users.
3. The program is not code-signed, so Windows SmartScreen may show *Windows protected your PC* the first
   time. Choose **More info**, then **Run anyway**.

Every release lists a checksum in `SHA256SUMS.txt`, so you can check your download:

```
certutil -hashfile CK_Sync_Setup_<version>.exe SHA256
```

## Quick start

1. Open CK Sync and press **Add**. Choose a name and the two folders.
2. Press **Preview** and read what it would do.
3. Press **Sync** and confirm.

**Try it on two test folders first**, before pointing it at anything important.

## Keeping pairs in sync automatically

Choose **Settings, Background sync**, tick the pairs, pick how often, and keep *Run even when I am not logged
in*. Windows asks for your Windows password once, to run the sync while you are logged out; CK Sync never
stores it. Each run is noted in `%APPDATA%\CK Sync\logs\background.log`, and a pair that needs your attention
shows an amber warning in the window.

## Command line

Run from the `cli` folder inside the program folder (for example `%LOCALAPPDATA%\Programs\CK Sync\cli`).

| Command | What it does |
| --- | --- |
| `CK_Sync_cli.exe sync` | Sync the pairs chosen for background sync (`--all` for every pair, `--pair NAME` for one) |
| `CK_Sync_cli.exe status` | List the pairs and how each last sync went |
| `CK_Sync_cli.exe preview LEFT RIGHT` | Show what a sync of two folders would do (changes nothing) |
| `CK_Sync_cli.exe schedule on --every 30` | Run the background sync every 30 minutes, also when logged out |
| `CK_Sync_cli.exe schedule status` / `off` / `run-now` | Look at, switch off, or start the background sync |
| `CK_Sync_cli.exe --version` | Print the version |

Exit codes of `sync`: `0` all fine or nothing to do, `1` some files had problems, `2` a pair needs your review,
`3` a pair could not be checked.

## Updates

CK Sync checks this repository's [Releases](https://github.com/epatels/ck-sync/releases) when it starts and
once a day, downloads a newer version quietly, and installs it the next time you close or start the program.
**Settings, Updates** switches this to "tell me, and let me choose". A download that does not match its signed
checksum is deleted and never run.

## Uninstall

Use **Settings, Apps** in Windows and remove *CK Sync*. This also removes the background-sync schedule. Your
pairs, settings and logs stay in `%APPDATA%\CK Sync` until you delete that folder. The `.cksyncbackup`
folders next to your files are yours to keep or delete.

## Problems and questions

Please open an issue on this repository (the **Issues** tab). It helps to say which version you have (it is
in the title bar) and what you did. Do not paste private file names or passwords.

## About this repository

This repository holds the downloads. CK Sync is closed-source software and its source code is not published.
It is provided as is, without warranty. CK Sync keeps a backup of anything it replaces or deletes, but that is
no substitute for a real backup of files that matter to you.
