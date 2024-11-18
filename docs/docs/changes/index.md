!!! note
	Component version `3.5.0` and later require at least `foobar2000` `2.1` and `Windows 10`.

## 3.8.5
- Add [IJSGraphics PushLayer](../interfaces/IJSGraphics.md#pushlayerx-y-w-h) and [IJSGraphics PopLayer](../interfaces/IJSGraphics.md#poplayer).
- Fix `IJSImage` `Clone` and `CreateBitmap` bugs.
- Update various samples to use `IJSBitmap` added in the previous release. 

## 3.8.4
- Add [IJSBitmap](../interfaces/IJSBitmap.md) interface. This is for performance over the original `IJSImage`.
- Add [IJSImage CreateBitmap](../interfaces/IJSImage.md#createbitmap) and [utils.LoadBitmap](../namespaces/utils.md#utilsloadbitmappath-max_size) methods.
- Add [IJSGraphics DrawBitmap](../interfaces/IJSGraphics.md#drawbitmapbitmap-dstx-dsty-dstw-dsth-srcx-srcy-srcw-srch-opacity-angle). This takes the same arguments as the original `DrawImage`.
- [utils.TextBox](../namespaces/utils.md#utilstextboxprompt-title-default_value-help_text) now takes an
optional `help_text` argument which can be viewed via a `Help` button in the dialog.

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
