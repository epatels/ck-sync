# CK Sync

**Keeps two folders in step, safely.** CK Sync shows you what it is about to do and why, before it changes
anything. Whatever it replaces or deletes is kept in a backup folder, and every copy is checked after it is
made. It follows renames, can keep a pair one-way, and can sync by itself on a schedule, even when nobody is
logged in.

[**Download the latest version**](https://github.com/epatels/ck-sync/releases/latest) · Windows 10, Windows 11 and Windows Server 2022 or 2025 (with a desktop), 64-bit

```
winget install epatels.CKSync
```



## What it does

- **Get files back (new in 2.1).** *Get files back…* lists what CK Sync kept when it replaced or deleted files, by day,
  on disk or in the cloud. Tick files, press *Put back*, or save a copy to another folder. A file in the way is kept too.
- **Alerts (new in 2.1).** Settings, Alerts: a Windows message and/or e-mail when a pair keeps failing (after 3 runs
  in a row by default), told once, and again when it works again.
- **Save a report (new in 2.1).** *Save report…* writes a preview as a page to print or a spreadsheet; also `preview --report`.
- **Faster, controllable cloud (new in 2.1).** A cloud helper that stays running makes syncs with many small files many
  times faster; speed limits with a "no limit at night" period; storage used and free per account; per pair, sync only
  some files (for example `*.docx`) or skip files over a size.
- **Copy pair, groups, history (new in 2.1).** Copy a pair, collect pairs in groups (show one group, set its background
  sync together), and see a plain-words history of each pair.
- **Background conditions and pause (new in 2.1).** Run only when plugged in, on an unmetered network, or when a share is
  reachable; pause all background sync for an hour, until tomorrow or until you resume; a tray icon shows the status.
- **`status --json` (new in 2.1)** for scripts and monitoring.
- **Cloud storage (new in 2.0).** Either side of a pair can be a folder in **Google Drive, OneDrive or Dropbox**
  (or another service under *Other provider*: Box, pCloud, WebDAV, SFTP, S3, MEGA and more). Sign in once under
  *Settings, Cloud accounts*; CK Sync never sees your password. Cloud to cloud pairs work too. Replaced or deleted
  cloud files are kept in a `.cksyncbackup` folder inside the cloud folder. Cloud access is done by the bundled
  [rclone](https://rclone.org/) (MIT licence).
- **Two files, not just two folders (new in 2.0).** A pair can keep one file in step with another file, with the same
  or a different name, on disk or in the cloud, with the same preview, backups and keep-both rules.
- **Background sync per pair (new in 2.0).** Each pair can follow the global schedule, be off, or have its own
  schedule (every N minutes or daily at a time). *Use for all pairs* applies the global schedule to every pair that
  has no choice of its own, including pairs added later.

- **Two-way sync of folder pairs.** Pick a left and a right folder: a local folder, a pen drive, an external
  disk, or a network share. New and changed files are carried both ways, and a deletion on one side is carried
  to the other.
- **Preview first.** *Preview* lists every file CK Sync would copy, move, replace, keep or delete, with the
  reason for each. Nothing changes until you press *Sync* and confirm.
- **Follows renames and moves.** Rename a file, or move it to another folder, on one side and CK Sync makes the
  same rename on the other side, without copying the file again or deleting anything.
- **One-way pairs.** Make a pair a *mirror* (the destination becomes a copy of the source) or *add and update
  only* (nothing is ever deleted on the destination), in either direction. The source side is never changed.
- **Safe by design.**
  - Anything replaced or deleted is moved to a hidden `.cksyncbackup` folder next to it and kept for 60 days.
  - If both sides changed the same file, **both versions are kept**; nothing is overwritten silently.
  - A sync that would delete or replace a large share of your files (more than 20 percent, and at least 10
    files) is stopped for you to check first.
  - A folder that is suddenly empty, or a drive that is not connected, is never treated as "everything was
    deleted".
  - Every copy is read back and compared with the original before it is put in place; a bad copy is discarded
    and tried again next time.
  - It checks free space first, and skips files that changed while it was working.
- **Data safety.** Copies are flushed to disk before they are put in place, the old version is kept with no gap, the
  pair database is checked and backed up daily, and damage is repaired from the newest good backup.
- **Network folders work when logged out.** A mapped drive such as `Z:` is saved as the full `\\SERVER\share` path.
- **Shows when the next sync is due** for each pair with background sync, and the direction (▶ ◀) of every copy.
- **Fast.** Folders are scanned together, small files are copied several at a time, and two files with the same
  size and date are not read again and again. The time left counts deletions, moves and the checking of copies too,
  so it counts down steadily instead of showing 0 and climbing. Details and the trade-offs are in the manual
  (`INSTRUCTIONS.md`, *Speed, and the time left*); both speed-ups can be switched off under *Settings*.
- **Pen drives.** Plug in a drive that has a pair on it while CK Sync is open and it offers to preview that pair.
- **Getting-started wizard.** The first time you run it, a short guide explains pairs in plain words and helps you
  make your first one.
- **Live status for every pair.** The pair list shows a turning ring while a pair is being checked or synced,
  a green tick when it is finished or already in step, and a clear warning when something needs a look.
- **Sync by itself, even when logged out.** Choose which pairs to keep in step and how often (from every 15
  minutes to once a day). It runs through Windows Task Scheduler, also with nobody logged in. If anything looks
  wrong it holds that pair back and changes nothing.
  It can also sync **when Windows starts**, **when Windows shuts down** (best effort: Windows does not wait for
  background tasks) and **soon after files change**.
- **Smooth.** The window stays responsive while thousands of files are copied, and the mouse wheel glides.
- **Command line.** `CK_Sync_cli.exe` does the same without a window, for scripts and schedulers.
- **Updates itself.** It checks this page once a day. An update is installed only if it carries the
  developer's signature and matches its checksum, and never while a sync is running.
- **Private.** No usage statistics, no tracking, no accounts of ours. CK Sync contacts GitHub to ask whether a newer
  version exists, and, only if you add a cloud account, that cloud service. Cloud sign-in details are stored encrypted on your PC.

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

`CK_Sync_cli.exe` does everything below without opening a window, for scripts and schedulers. It is in the
`cli` folder inside the program folder (for example `%LOCALAPPDATA%\Programs\CK Sync\cli`). From the source
files use `python -m syncapp` instead. Add `-h` to any command for help.

| Command | What it does |
| --- | --- |
| `CK_Sync_cli.exe sync` | Sync the pairs chosen for background sync. This is what the schedule runs |
| `CK_Sync_cli.exe sync --all` | Sync every saved pair |
| `CK_Sync_cli.exe sync --pair NAME` | Sync one pair, by name (any letter case) or number. Repeat `--pair` for more |
| `CK_Sync_cli.exe sync --no-verify` | Sync without reading each copy back to check it (faster, less safe) |
| `CK_Sync_cli.exe sync --thorough` | Read both files to compare them even when size and date match |
| `CK_Sync_cli.exe sync --threads N` | Handle up to N small files at once (default 4; 1 = one at a time) |
| `CK_Sync_cli.exe status` | List the pairs, whether each is in the background sync, their direction if one-way, and how the last sync went |
| `CK_Sync_cli.exe preview LEFT RIGHT` | Show what a sync of two folders would do and why. Changes nothing and uses no saved pair |
| `CK_Sync_cli.exe schedule on` | Create or update the background schedule (Windows only) |
| `CK_Sync_cli.exe schedule off` | Remove the schedule |
| `CK_Sync_cli.exe schedule status` | Show whether it is on, when it runs next, and how the last run ended |
| `CK_Sync_cli.exe schedule run-now` | Start one background run now, the way the schedule does |
| `CK_Sync_cli.exe --version` (`-V`) | Print the version |
| `CK_Sync_cli.exe -h` (`--help`) | Help; also works after a command, for example `schedule -h` |

**Options**

- `sync`: `--all` (every saved pair); `--pair NAME_OR_NUMBER` (one pair; repeat for more); `--no-verify` (skip the
  read-back check of each copy; otherwise the *Verify copies* setting of the window is used); `--thorough`;
  `--threads N`;
  `--db FILE` (use another saved-pairs file, for testing).
- `status`: `--db FILE`.
- `preview`: `--quick` (compare size and date only, faster); `--thorough`; `--threads N`; `--exclude PATTERN` (leave out files such as
  `Thumbs.db`; repeat for more); `--direction` (`two_way`, the default, or one-way: `lr_mirror`, `lr_add`,
  `rl_mirror`, `rl_add`).
- `schedule on`: `--every MINUTES` (1 to 1440, default 60) **or** `--daily HH:MM` (once a day, 24-hour clock);
  `--wake` (wake the PC from sleep); `--logged-in-only` (no password needed, but it runs only while you are logged
  in); `--password-env NAME` (read your Windows password from this environment variable instead of asking);
  `--pair NAME_OR_NUMBER` (repeatable) or `--all-pairs`; `--db FILE`. Without `--logged-in-only` it asks for your
  Windows password, which is handed to Windows and never stored by CK Sync.

The directions for `--direction` are: `two_way` (both sides keep each other up to date), `lr_mirror` (the right
side becomes a copy of the left), `lr_add` (new and changed files go left to right; nothing is deleted on the
right), `rl_mirror` and `rl_add` (the same, right to left). The old form `CK_Sync_cli.exe LEFT RIGHT` (without the
word `preview`) also still works.

**Examples**

```
CK_Sync_cli.exe preview "D:\Documents" "E:\Documents" --exclude Thumbs.db
CK_Sync_cli.exe preview "D:\Photos" "E:\Photos" --direction lr_add
CK_Sync_cli.exe sync --pair "Documents" --pair 3
CK_Sync_cli.exe status
CK_Sync_cli.exe schedule on --every 30
CK_Sync_cli.exe schedule on --daily 02:00 --wake --pair Documents
CK_Sync_cli.exe schedule on --every 60 --logged-in-only
CK_Sync_cli.exe schedule status
```

**Exit codes of `sync`** (Task Scheduler shows them as *Last Run Result*): `0` all fine or nothing to do, `1` some
files had problems (they are retried next time), `2` a pair needs your review (it was held back and nothing was
changed), `3` a pair could not be checked at all, or a bad command. The other commands use `0` for success and `3`
for an error; `preview` returns `2` if it cannot be done (for example a folder is missing).

`sync` never asks a question: when something looks wrong (a missing drive, a very large number of deletions, no
free space) it holds that pair back and changes nothing. What each run did is written to
`%APPDATA%\CK Sync\logs\background.log`.

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
