## 3.5.4
- Add `fb.CustomVolume` for compatibility with `UPnP` output devices. See the note [here](../namespaces/fb.md).
- Update `fb.Volume` to suppress errors if a `UPnP` device is active.
- Update the following samples with `$rgb` support:
```
Track Info + Seekbar + Buttons + Volume
Track Info + Seekbar + Buttons
Track Info + Spectrogram Seekbar + Buttons
```
Existing users will need to re-import using the `Samples` button in the [Configuration Window](../configuration-window.md).
- Reduce height of `utils.TextBox` (used by `Text Display`) so it works on a `1080p` display at `150%` `DPI`.

## 3.5.3
- Fix bug when using `window.Reload()` from inside the `on_mouse_rbtn_up` callback.

## 3.5.2
- Fix issue introduced in `3.4.20` where main menu items created as keyboard shortcuts only (never displayed) were not executed by `fb.RunMainMenuCommand`.
- Fix `Smooth Playlist Manager` bug where it didn't auto scroll to the active playlist on startup.

## 3.5.1
- Add [fb.IsLibraryInitialised](../namespaces/fb.md#fbislibraryinitialised).
- Add [on_library_initialised](../callbacks/foobar2000.md#on_library_initialised) callback.

## 3.5.0
- The new minimum requirement for `foobar2000` is now `2.1`. `Windows 10` or later is also required. Previous versions are available [here](https://github.com/jscript-panel/release/releases/tag/legacy).
- `fb.IsV2` has been removed. As it was a property, script errors will not be thrown if used but it will always be `undefined`.
- The [IMetadbHandle GetFileInfo](../interfaces/IMetadbHandle.md#getfileinfo) method no longer accepts a `full_info` parameter. It was previously required for `foobar2000` `1.x` users but full info is always returned in `foobar2000` `2.x`.
- Update `Spectrogram Seekbar` samples to skip certain file types which `ffmpeg` tries to process but uses excessive amounts of memory leading to possible crashes.
- Fix `JS Playlist` drag/drop bug.
