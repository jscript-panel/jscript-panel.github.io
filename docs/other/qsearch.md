# QSearch
[Download :material-download:](https://github.com/marc2k3/marc2k3/releases/tag/2024-03-02){ .md-button }

## Usage
This provides 6 context menu items to create playlists or open a search window
from the selected track's metadata.

```
artist IS
title IS
album IS
artist HAS
title HAS
album HAS
```

If you look under `File>Preferences>Advanced>Tools>QSearch`, there are 5 options.

```
Create Autoplaylist
Create Autoplaylist and switch
Send search results to standard playlist
Send search results to standard playlist and switch
Open Media Library search window
```

## Changes

### 1.0.5
- Add advanced preferences for sending search results to standard playlists.

### 1.0.4
- Fix regression in `1.0.3` where the search term was not made lower case.
- If you hold the ++shift++ key when selecting a menu item, it will always open the `Media Library` search window.

### 1.0.3
- Change advanced preferences default.

### 1.0.2
- Add advanced preferences.

### 1.0.1
- Prevent creation of playlist when tag used for search term was missing/empty.

### 1.0.0
- Initial release.
