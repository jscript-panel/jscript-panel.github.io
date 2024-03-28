# Run Main
[Download :material-download:](https://github.com/marc2k3/marc2k3/releases){ .md-button }

## Overview
Unlike the built in command line handler/`foo_runcmd`, this component has
full support for dynamically generated menu commands meaning you can
use `Edit` commands and switch playlists, change output devices etc.

![run main](images/run-main.gif)

## Usage

To avoid ambiguity with common names that might appear more than once
under different sub menus, you must supply the full path to the command.

!!! example
	```
	foobar2000.exe /run_main:Edit/Sort/Randomize
	foobar2000.exe /run_main:Library/Search

	// use double quotes when command contains spaces
	foobar2000.exe /run_main:"Playback/Device/Primary Sound Driver"
	```

## Changes

### 1.0.2
- Compiled with latest `foobar2000` `SDK`.

### 1.0.1
- Initial release.
