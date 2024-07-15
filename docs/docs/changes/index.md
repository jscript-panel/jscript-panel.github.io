!!! note
	Component version `3.5.0` and later require at least `foobar2000` `2.1` and `Windows 10`.

## 3.6.0-Beta.3
- `gr.WriteText` now has full `$rgb` support built in making `DrawColouredText` provided in
`helpers.txt` obsolete. It has been removed so if you encounter any script errors,
please use the `Samples` button to re-import any affected script.
- A new `gr.WriteText2` method has been added. In addition to supporting `$rgb` code, this also supports
`$font` natively. See `Samples\basic\$font + $rgb`. Because of this, `DrawStyledText` in `helpers.txt`
has been removed.
- `utils.CreateTextLayout` now supports `$font` and `$rgb` code contained in the text.
- `utils.CreateTextLayout2` now supports `$rgb` only.

You can read more about `$font` and `$rgb` [here](../guides/font-rgb.md).
