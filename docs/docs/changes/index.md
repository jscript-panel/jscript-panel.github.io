!!! note "Note for JScript Panel v2 users"
	Because of the massive changes, this component is named
	`JScript Panel 3 (foo_jscript_panel3.dll)`.

	For `x86` users, it will not override any previous
	`JScript Panel` installation. It will install side by
	side.

	There is no way to upgrade and scripts will require significant
	changes to be compatible. If you have complex scripts of your
	own, it probably isn't worth the effort.

	The biggest change is the reworking of all graphics and image
	handling which are detailed [here](3-0-0/).

	`JScript Panel v2` is still available for download [here](https://github.com/marc2k3/fb2k-archive/releases).

## For `foobar2000` `2.0`

!!! note
	While `foobar2000` `2.0` is `Beta`, it's strongly recommended that you use the latest version. `Beta 18` is already required for some component features.

### 3.2.2
- Update `window.GetFontCUI` / `window.GetFontDUI` so they properly handle font names which contain properties like `SemiBold`, `Condensed`, `Light` etc.
- Fix bug with `plman.AddLocations` so items are added to the correct playlist if other playlist operations during the async process cause the `playlistIndex` of the destination playlist to change.
- Various sample fixes.

### 3.2.1
- The `Thumbs` sample has been limited to loading no more than 64MB of images from disk.

### 3.2.0
- See this [page](3-2-0/).

### 3.1.18
- Fix regression from `3.1.17` where resources may not have been freed correctly on shut down. This would only affect scripts that used `utils.LoadSVG`.

### 3.1.17
- The `SVG` renderer now supports `text`.

### 3.1.16
- Fix `JS Playlist` bug which prevented setting a custom group header height.
- Other minor bug fixes.

### 3.1.15
- Update `utils.LoadSVG` to use a better rendering library.

### 3.1.14
- Fix bugs with `IJSGraphics` `FillGradientRectangle` / `FillGradientRectangleAdvanced`.
- `on_library_items_changed` has a new `fromhook` argument. Will be `true` if changes comes from `Playback Statistics` or other components that utilise the same DB functionality. Requires [foobar2000](https://foobar2000.org) `2.0 Beta 13` or later.

### 3.1.13
- Fix `Thumbs` sample so existing images are not downloaded again.

### 3.1.12
- This is just a maintenance release with some bug fixes.

### 3.1.11
- The `Text Display` sample has been updated with simple scroll support. Existing users must re-import the script using the `Samples` button in the [Configuration Window](../configuration-window/).
- Add [utils.CreateTextLayout2](../namespaces/utils/#utilscreatetextlayout2text-fonts-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity). This allows the scrolling of styled text.
- Update [utils.CreateTextLayout](../namespaces/utils/#utilscreatetextlayouttext-font_name-font_size-font_weight-font_style-font_stretch-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity) with `trimming_granularity` argument.

### 3.1.10
- Fix `Text Display` bug where the `$font` parsing code was broken if `$rgb` code was not also present.

### 3.1.9
- The `Text Display` sample has been updated to support custom `$font` title formatting. See [this](../../gallery/text-display/#title-formatting) page for full details.

### 3.1.8
- Fix `utils.ReplaceIllegalChars` regression in `3.1.7`.

### 3.1.7
- If you use `Columns UI`, the component now requires the latest [2.0.0-alpha.5](https://foobar2000.org/components/view/foo_ui_columns).
Dialogs now respect the `Columns UI` `Dark Mode` settings and the `on_colours_changed` / `on_font_changed` callbacks also require it to function properly.
- [fb.GetLibraryItems](../namespaces/fb/#fbgetlibraryitemsquery) now accepts an optional `query` argument which utilises new [foobar2000](https://foobar2000.org) `2.0` code. Unlike
`IMetadbHandleList GetQueryItems`, no errors are thrown and all items will be returned if the `query` is invalid.
- Various sample fixes.

### 3.1.6
- `plman.IsPlaylistLocked` and `plman.IsAutoPlaylist` have been updated so the supplied `playlistIndex` no longer has to
be valid. This should fix `JS Playlist` and `Smooth Playlist Manager` from occasionally throwing errors when playlists are removed.

### 3.1.5
- Changing the [Editor Properties](../configuration-window/#editor-properties) is now done via a new `Style`
button in the [Configuration Window](../configuration-window/).

### 3.1.4
- Fix issue where `WebP` album art wasn't handled internally.

### 3.1.3
- Support for `WebP` images is now built in to the component. Using the `Windows Imaging Component (WIC)`
was not reliable and may have caused display issues in recent changes to the `Spectrogram Seekbar` scripts.

### 3.1.2
- Update [Text Display](../../gallery/text-display/) with album art background option. Existing users must re-import from the `Samples` button.

### 3.1.1
- [on_metadb_changed](../callbacks/#on_metadb_changedhandle_list-fromhook) has had the `fromhook` argument restored.
- Hopefully prevent `Smooth Browser` from updating itself when plays are recorded by `Playback Statistics`.

### 3.1.0
See this [page](3-1-0/).

## For `foobar2000` `1.6.6` - `1.6.14`

### 3.0.16
- Restore the `on_main_menu` callback.
- Restore the `fromhook` argument to `on_metadb_changed`.

### 3.0.15
- Update `window.GetFontCUI` / `window.GetFontDUI` so they properly handle font names which contain properties like `SemiBold`, `Condensed`, `Light` etc.
- Fix bug with `plman.AddLocations` so items are added to the correct playlist if other playlist operations during the async process cause the `playlistIndex` of the destination playlist to change.
- Various sample fixes.

### 3.0.14
- The `Thumbs` sample has been limited to loading no more than 64MB of images from disk.

### 3.0.13
- Backport some fixes from the latest version.

### 3.0.12
- Various bug fixes.

### 3.0.11
- Fix regression from `3.0.10` where resources may not have been freed correctly on shut down. This would only affect scripts that used `utils.LoadSVG`.

### 3.0.10
- The `SVG` renderer now supports `text`.

### 3.0.9
- Update `utils.LoadSVG` to use a better rendering library.

### 3.0.8
- Fix bugs with `IJSGraphics` `FillGradientRectangle` / `FillGradientRectangleAdvanced`.

### 3.0.7
- Fix `Thumbs` sample so existing images are not downloaded again.

### 3.0.6
- Built in support for `WebP` images was backported from version `3.1.3`.

### 3.0.5
- Restore [Configuration Window](../configuration-window/) menu and editor presets that were unintentionally replaced in `3.0.4`.
- `Smooth Playlist Manager` and `JS Playlist` bug fixes.

### 3.0.4
- The minimum requirement for [foobar2000](https://foobar2000.org) is now `1.6.6`.
- The [IMetadbHandle](../interfaces/IMetadbHandle/) interface now has a `LastModified` property. Unlike `%last_modified%`, this is a timestamp.
- Fixes broken `$rgb` support in `JS Playlist`. It should be usable in columns again.
- Fixes a bug with `Last.fm Bio` and `Thumbs` not being able to download and save files if the artist ended with a period character.
- The `Spectrogram` seekbar scripts have been updated to save as `WebP` which are much smaller images.
- The `Last.fm Artist Info + User Info (previously Similar Artists)` can now display `Top tracks` and `Top tags`. Also, a bug which prevented `Recent Tracks` from updating has been fixed but the script needs reloading from the `Samples` button.

### 3.0.3
- Fixes a bug with `JS Playlist` `state` and `mood` column alignment where the `right` and `centre` options were inverted.

### 3.0.2
- Fix crash if [Configuration Window](../configuration-window/) `Goto` dialog was empty when clicking `OK`.

### 3.0.1
- Calling [DrawImage](../interfaces/IJSGraphics/#drawimageimage-dstx-dsty-dstw-dsth-srcx-srcy-srcw-srch-opacity-angle) with bad `srcW` or `srcH` arguments now silently fails instead of turning the whole panel black.

### 3.0.0
See this [page](3-0-0/).
