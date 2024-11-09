!!! note
	Component version `3.5.0` and later require at least `foobar2000` `2.1` and `Windows 10`.

## 3.8.3
- Add `VU Meter 2` sample. This automatically updates the bar orientation on panel resize
like built-in `Default UI` elements. There are no labels. Most other options are still
available on the right click menu.

## 3.8.2
- Add [fb.EnumerateMainMenuCommands](../namespaces/fb.md#fbenumeratemainmenucommands).

## 3.8.1
- Add [fb.GetActiveDSPs](../namespaces/fb.md#fbgetactivedsps).

## 3.8.0
- Fix various `gr.WriteTextLayout` bugs that affected vertical alignment when text needed scrolling support.
- Existing users of the various `Text Display` samples will need to update the scripts in their
panels. There were many script bugs that needed fixing in addition to the component bug mentioned above.
