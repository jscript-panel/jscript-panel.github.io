!!! note
	Component version `3.5.0` and later require at least `foobar2000` `2.1` and `Windows 10`.

## 3.6.14
- `Album Art` has a new custom mode available from the right click menu. When enabled you can set multiple artwork types to be checked in order such as front first and if not found, use artist etc.
- Various internal bug fixes.

## 3.6.11
- Add [utils.CalcTextWidth2](../namespaces/utils.md#utilscalctextwidth2text-font_str) which takes a font as a string.
- Add `Text Display + Album Art + Rating` sample. Supports `Playback Statistics` or writing any custom file tag you like. Right click to customise.
- Update `VU Meter` with custom `Peak` colour option.

## 3.6.10
- `VU Meter` now has support for gradient bar colours set via the right click menu.
- Fix `Thumbs` bug where the underlying background colour may have dominated blurred images.
- Various other bug fixes.

## 3.6.9
- Update `VU Meter` to respect `DPI` settings and add full custom colour support to the right click menu. Existing users must update using the `Samples` button in the [Configuration Window](../configuration-window.md).

## 3.6.8
- `VU Meter` sample tweaks:
    * There is now only one block style (by dB).
    * These variables are now obsolete: `rms_block_count`, `rms_block_db`, `rms_3db`. Use the right click menu instead.

## 3.6.7
- Add `VU Meter` sample created by [Case](https://hydrogenaud.io/index.php?action=profile;u=322).

## 3.6.6
- Add [fb.GetAudioChunk](../namespaces/fb.md#fbgetaudiochunkrequested_length-offset).
- Add [IAudioChunk](../interfaces/IAudioChunk.md) interface.
- Tidy up `JS Playlist` settings and fix bug where the word `null` was displayed incorrectly. Fields should now be left empty when you don't want anything displayed.

## 3.6.5
- `Smooth Browser` has been updated to support multi-value artist tags.
- Add [IMetadbHandleList GroupByTag](../interfaces/IMetadbHandleList.md#groupbytagtag).
- Add [utils.HashString](../namespaces/utils.md#utilshashstringstr).
- Fix regression in `3.5.1` where `on_library_items_changed` stopped working.

!!! note
	Because of `Smooth` sample changes, the `js_smooth_cache` folder inside your `foobar2000`
	profile is now obsolete and may be deleted. Images are now cached inside `js_data\smooth_cache`.

## 3.6.4
- Attempt to fix repaint glitch when using `Default UI` tabs and hardware accelerated `Default UI` visualisations.

## 3.6.3
- Add [gr.WriteTextSimple](../interfaces/IJSGraphics.md#writetextsimpletext-font-colour-x-y-w-h-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity).
Only a single font/colour is supported and `$rgb`/`$font` code in `text` will be ignored. Also, the `font` will not support `Underline` or `Strikethrough` properties.
- Update [utils.CalcTextWidth](../namespaces/utils.md#utilscalctextwidthtext-font_name-font_size-font_weight-font_style-font_stretch) to handle `$font` code in the text.

## 3.6.2
- Fix long standing bug where `Underline` and `Strikethrough` properties in a single font passed to `gr.WriteText` were ignored.
- `Text Display` and `Text Display + Album Art + Seekbar + Buttons` have been updated so the album art is no longer locked to the front cover.
- Allow `Text Display + Album Art + Seekbar + Buttons` background image to be toggled via the right click menu.

## 3.6.1
- Fix possible bug passing a stringified array of colours to `gr.WriteTextLayout`.
- Add [fb.EnableAdvancedLogging](../namespaces/fb.md#fbenableadvancedlogging). See link for usage notes.

## 3.6.0
- `gr.WriteText` now has full `$rgb` support built in making `DrawColouredText` provided in
`helpers.txt` obsolete. It has been removed so if you encounter any script errors,
please use the `Samples` button to re-import any affected script.
- A new [gr.WriteText2](../interfaces/IJSGraphics.md#writetext2text-font-colour-x-y-w-h-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity) method has been added. In addition to supporting `$rgb` code, this also supports
`$font` natively. See `Samples\basic\$font + $rgb`. Because of this, `DrawStyledText` in `helpers.txt`
has been removed.
- `utils.CreateTextLayout` now supports `$font` and `$rgb` code contained in the text.
- `utils.CreateTextLayout2` now supports `$rgb` only.
- Add new `Minimal Seekbar + Playback Buttons`. See this [updated page](../../gallery/seekbar-button.md) for sreenshots.

You can read more about `$font` and `$rgb` [here](../guides/font-rgb.md).
