!!! note
	Component version `3.5.0` and later require at least `foobar2000` `2.1` and `Windows 10`.

## 3.6.2
- Fix long standing bug where `Underline` and `Strikethrough` properties in a single font passed to `gr.WriteText` were ignored.
- `Text Display` amd `Text Display + Album Art + Seekbar + Buttons` have been updated so the album art is no longer locked to the front cover.
- Allow `Text Display + Album Art + Seekbar + Buttons` background image to be toggled via the right click menu.

## 3.6.1
- Fix possible bug passing a stringified array of colours to `gr.WriteTextLayout`.
- Add [fb.EnableAdvancedLogging](../namespaces/fb.md/#fbenableadvancedlogging). See link for usage notes.

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
