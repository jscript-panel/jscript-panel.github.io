## 3.4.19
- `Smooth Browser` has been updated so `Albums` are now sorted in alphabetical order and tracks without `%album%` tags are shunted to the end of the list. They are grouped by `%directory%`.

## 3.4.18
- Add [IMetadbHandleList AttachImage2](../interfaces/IMetadbHandleList.md#attachimage2image-art_id-type). This method allows attaching images from memory rather than file path.
- Update `Smooth Browser` group settings so the full `%date%` is displayed in `Album` mode.

## 3.4.17
- Add new `Menu + Playback Buttons + Custom Colours` sample. This is mainly for `Columns UI` because you cannot hide the menu toolbar in `Default UI`.
- Various `Status Bar` fixes and improvements. Existing users will need to re-import using the `Samples` button. Title formatting can now be configured via the right click menu and `$rgb` is supported.

## 3.4.16
- Update `Scintilla` library used for code highlighting. The last release may have had a bug related to undo/redo.
- `JSPlaylist` and `Smooth Playlist` have been updated so you can right click in a blank area and `Paste` clipboard items. Previously, you had to select a valid playlist item and it was impossible to `Paste` in an empty playlist.
- Update `Smooth Playlist` context menu so the settings are always shown no matter where you right click.
- Various other playlist fixes.

## 3.4.15
- Minor component bug fixes.
- Fix bugs with `Minimal Seekbar` and `Text Display + Album Art + Seekbar + Buttons` samples where the seekbars were not centred and playback time was not displayed when listening to streams. Existing users will need to re-import using the `Samples` button.
- Fix bugs with the `basic\WriteTextStyles` and `basic\SimpleScroll + Styled Text` samples. The [corresponding documentation](https://jscript-panel.github.io/docs/guides/styling-ranges-text/) has also been fixed.

## 3.4.14
- Add [utils.CopyFile](../namespaces/utils.md#utilscopyfilefrom-to-overwrite).
- Add [utils.CopyFolder](../namespaces/utils.md#utilscopyfolderfrom-to-overwrite-recur).
- Add [utils.RenamePath](../namespaces/utils.md#utilsrenamepathfrom-to).

## 3.4.13
- Add new `Text Display + Album Art + Seekbar + Buttons` sample.
- Fix bug with original `Text Display` where the fonts/rgb internet link was broken.
- Fix bug with `Minimal Seekbar` where the seekbar knob overlapped the length text at the end of a track. Existing users will need to re-import using the `Samples` button.

## 3.4.12
- Add [IMetadbHandleList Reverse](../interfaces/IMetadbHandleList.md#reverse).
- Add `Playback Order` button to the following scripts. The original `Playback Buttons` has been left untouched.
```
Playback Buttons + Playback Order
Track Info + Seekbar + Buttons
Track Info + Seekbar + Buttons + Volume
Track Info + Spectrogram Seekbar + Buttons
```
Existing users will need to re-import using the `Samples` button. If it's not immediately obvious which mode each icon represents, tooltips give the full name.

## 3.4.11
- Fix bad change to `helpers.txt` in `3.4.8` which caused 3rd party scripts to break. Apologies for the inconvenience.

## 3.4.10
- Various internal improvements.
- `JSPlaylist` / `Smooth` sample optimisations.

## 3.4.9
- Update `window.GetFontCUI` to gracefully handle a font with zero size being defined in the `Preferences`.

## 3.4.8
~~- Internal font handling changes which may help debugging in future.~~

## 3.4.7
- `FontAwesome` is no longer required. `Segoe Fluent Icons` is now used across all included samples. `Windows 11` users will already have this installed. Everyone else can get it [here](https://download.microsoft.com/download/8/f/c/8fc7cbc3-177e-4a22-af48-2a85e1c5bffb/Segoe-Fluent-Icons.zip).
- For existing users of any included button scripts, the following will need re-importing from the `Samples` button:
```
Playback Buttons
Track Info + Seekbar + Buttons
Track Info + Seekbar + Buttons + Volume
Track Info + Spectrogram Seekbar + Buttons
```

## 3.4.6
- ~~Transparency is now reserved exclusively for genuine `Columns UI` toolbars. Adding as a `Toolbar` via the `Columns UI` `Layout` settings will have no effect and it will be a normal panel with a solid colour background.~~ Reverted in `3.4.10`.
- Add new `Minimal Seekbar`. It's just a seekbar with playback time/length and no buttons. It's `Dark Mode` aware and will update itself when toggled.
- Fix bug with `Status Bar` sample.

## 3.4.5
- Add workaround for strange menu manager bug.

## 3.4.4
- `$jsp3_since` has been updated with proper `Today` / `Yesterday` handling and never returns `0d` any more.
- Minor sample fixes.

## 3.4.3
- `fb.AcquireSelectionHolder` and the `ISelectionHolder` interface have been removed due to bugs affecting other components. Their replacement
is the 3 `ISelectionHolder` methods being moved to [window](../namespaces/window.md). See how the included samples were updated [here](https://github.com/jscript-panel/component/commit/f4d4175d39f33da15450db8080bfd77118fa86a6).
- Add [utils.Now](../namespaces/utils.md#utilsnow).

## 3.4.2
- Fix [Configuration Window](../configuration-window.md) editor regression in `3.4.1`.

## 3.4.1
- Remove the `want_stub` argument from `IMetadbHandle` `GetAlbumArtAsync`. It was marked as deprecated in `3.3.10` and was meant to be removed in `3.4.0` but I forgot. See [fb.GetAlbumArtStub](../namespaces/fb.md#fbgetalbumartstubart_id).

## 3.4.0
- This release drops support for `Windows 7` and `Windows 8`. `Windows 8.1` is the new minimum requirement.
- Restore [utils.RemoveFolderRecursive](../namespaces/utils.md#utilsremovefolderrecursivepath-option).
- `window.IsThemed`, `window.CreateThemeManager` and the `IThemeManager` interface have all been removed.
- `IJSGraphics` `FillGradientRectangle` and `FillGradientRectangleAdvanced` have been removed. The standard `FillRectangle` and all other Draw/Fill methods now support [gradients](../guides/gradients.md).
- The `Edge Style` option has been removed for `Columns UI` panels.
- Existing `Text Display` users will need to re-import using the `Samples` button in the [Configuration Window](../configuration-window.md).
    * It now supports `%jsp3_playlist_name%` for displaying the playing/active playlist depending on selection settings. Note the playing track doesn't have to belong to a playlist so use of `$if` or `[]` is recommended.
    * When in `text only` mode, the margin can be configured from the right click menu. Also, the default value is reduced.
    * The [Gallery](../../gallery/text-display.md#title-formatting) page has been updated with more notes on exclusive title formatting features only available in this component.
