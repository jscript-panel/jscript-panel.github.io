!!! note
	Component version `3.5.0` and later require at least `foobar2000` `2.1` and `Windows 10`.

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
- With the additon of the above method, the `Album Art` sample picture viewer now works in `Custom` mode.
- A simplified script named `Images` has been added for displaying multiple images without thumbnails. If
you use `Thumbs` with thumbnails turned off, it's recommended that you switch to this. It has
no limitations on the the size/number of images in a given folder because it only loads one image in memory
at a time. Like `Thumbs`, it has custom folder and `Last.fm ` support. Scroll with your mouse or use
the `Cycle` timer on the right click menu.
