# Playlist Fix
[Download :material-download:](https://github.com/marc2k3/marc2k3/releases){ .md-button }

## Overview
This aims to provide similar functionality to `foo_playlist_revive`. It uses
title formatting to match dead playlist items against library items and updates
the playlist entries.

## Usage
Before using, check the main `Preferences>Tools>Playlist Fix`. You can view/add your
own title formatting presets.

There are 4 main menu commands under `File>Playlist Fix`.

```
Fix active playlist
Fix all playlists
Check active playlist
Check all playlists
```

!!! note
	The `check` options will generate a report without making any changes.

Because playlist operations are only permitted in the main thread, it may appear
to block the UI if used on large libraries/playlists. There is no way around that.

The report may look something like [this](images/playlist-fix.png).

## Changes

### 1.1.6
- Compiled with latest `foobar2000` `SDK`.
- The minimum requirement is now `foobar2000` `2.1`.

### 1.1.5
- Internal changes only.

### 1.1.4
- Compiled with latest `foobar2000` `SDK`.

### 1.1.3
- The report dialog has been updated so both path columns are auto-sizing. Also, the paths are no longer prefixed with `file://`.

### 1.1.2
- Fixes a bug where the report dialog list control had an ugly white border in `Dark Mode`.

### 1.1.1
- The report dialog is now resizeable.

### 1.1.0
- You can now save your own `Presets` under `File>Preferences>Tools>Playlist Fix`. The old setting under `Advanced` has been removed.

### 1.0.1
- Bug fix.

### 1.0.0
- Initial release.
