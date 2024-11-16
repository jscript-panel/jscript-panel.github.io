!!! note
	If any included sample throws a script error on upgrading, always update
	to the latest version from the `Samples` button in the [Configuration
	Window](../configuration-window.md). Only script authors need to read below.

### Upgrading to 3.6.x from previous versions
Scripts that made use of `DrawColouredText` and `DrawStyledText` in `helpers.txt`
will need to be updated as they have been removed.

`DrawColouredText` can be replaced with the original `gr.WriteText` which now has native
support for `$rgb`. And `DrawStyledText` can be replaced by `gr.WriteText2` which has `$font`
and `$rgb` support built in.

### Upgrading to `3.4.x` from previous versions
`IJSGraphics` `FillGradientRectangle` and `FillGradientRectangleAdvanced` have been removed. See
[Gradients](../guides/gradients.md) for their replacements.

`window.CreateThemeManager`, `window.IsThemed` and the `IThemeManager` interface have
all been removed.

The `want_stub` argument from `IMetadbHandle` `GetAlbumArtAsync` was removed. It was marked
as deprecated in `3.3.10`. See [fb.GetAlbumArtStub](../namespaces/fb.md#fbgetalbumartstubart_id).

A breaking change was made in `3.4.3` because of a bug that affected other components.
`fb.AcquireSelectionHolder` and the `ISelectionHolder` interface were replaced by
the 3 `ISelectionHolder` methods being moved to [window](../namespaces/window.md).
