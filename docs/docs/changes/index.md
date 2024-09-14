!!! note
	Component version `3.5.0` and later require at least `foobar2000` `2.1` and `Windows 10`.

## 3.7.9
- Fix an ugly timer related crash. Apologies to anyone affected by this.
- `Smooth Playlist Manager` and the playlist manager built in to `JS Playlist` now show a distinction
between autoplaylists and playlists that are locked. Previously, they shared the same icon.

## 3.7.8
- Fix `Last.fm` web request bugs after changing the api key. The bug would have fixed itself
after restarting `foobar2000` but that shouldn't have been necessary.

## 3.7.7
- This is just a further refinement of the bug fix in `3.7.6`.

## 3.7.6
- Fix deadlock when using `Columns UI` to switch themes containing `JScript Panel 3` instances.

## 3.7.5
- Update [utils.DownloadFileAsync](../namespaces/utils.md#utilsdownloadfileasyncwindow_id-url-path-verify_image) with
new `verify_image` argument.
- Update `Thumbs` and `Images` samples to use the above method as it has been noticed that `Last.fm` can serve files which are not images.

## 3.7.4
- Update various samples with image display improvements.
- Various bug fixes.

## 3.7.3
- Users of `Last.fm Bio`, `Last.fm Bio + Images` and `Last.fm Artist Info + User Info` now need to set their own Last.fm API key via
the right click menu. You can get one from this link: [https://www.last.fm/api/account/create](https://www.last.fm/api/account/create)

## 3.7.2
- Fix `Properties` and `Properties + Other Info` throwing script errors on empty playlists. This was a regression in `3.7.0`.
- Various other sample fixes.

## 3.7.1
- This update exposes all `Album Art` options in the various `Text Display` samples. And once again, they need reloading
from the `Samples` button.

## 3.7.0
- There has been a large rewrite of some included samples which means existing users will need to reload these from the
`Samples` button:
```
Allmusic + Album Art
Allmusic
Console
Last.fm Artist Info + User Info
Last.fm Bio
Last.fm Bio + Images
MusicBrainz
Play Log
Properties
Properties + Other Info
Text Reader
```
Apologies for the inconvenience.
- Add [IMetadHandle ShowPictureViewer2](../interfaces/IMetadbHandle.md#showalbumartviewer2art_id-type).
- With the addition of the above method, the `Album Art` sample picture viewer now works in `Custom` mode.
- A simplified script named `Images` has been added for displaying multiple images without thumbnails. If
you use `Thumbs` with thumbnails turned off, it's recommended that you switch to this. It has
no limitations on the the size/number of images in a given folder because it only loads one image in memory
at a time. Like `Thumbs`, it has custom folder and `Last.fm ` support. Scroll with your mouse or use
the `Cycle` timer on the right click menu.
