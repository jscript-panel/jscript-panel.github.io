# Play Track
[Download :material-download:](https://github.com/marc2k3/marc2k3/releases){ .md-button }

## Usage
This adds a `Play Track` submenu to the main `Playback` menu.

From there, you can play tracks from the `1st` to the `30th`. There is a also
a command for the `Last` track.

There are also `Random` and `Focused` commands. These are specifically for
people who have `Playback follows cursor` disabled because they function on the
active playlist even when `foobar2000` is playing from another.

### Command-line support
There is also built in command line support where you can supply any valid number for
the track index. If the supplied index exceeds the track count, the last track will always be played.

!!! example
	```
	foobar2000.exe /play_track:12
	```

## Changes

### 1.0.3
- Add new `Focused` command. This is mainly for people who have `Playback follows cursor` disabled.
It always plays the focused track from the active playlist regardless of current settings/where the
current track is playing from.

### 1.0.2
- Add new `Random` command. This differs from the built-in command because it can play from the active
playlist even if `Playback follows cursor` is disabled and `foobar2000` is currently playing
from another playlist.

### 1.0.1
- Fix potential menu ID conflicts.

### 1.0.0
- Initial release.
