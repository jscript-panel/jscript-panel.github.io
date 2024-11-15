:octicons-tag-24: 3.8.4

!!! note
	The original `IJSImage` is perfectly fine for most normal usage except when refreshing the panel
	numerous times per second. A `IJSImage` instance is a wrapper around `IWICBitmap` from the `Windows SDK`
	and this has to be converted to an `ID2D1Bitmap` for rendering. Doing this repeatedly is ineffecient so this
	simplified interface creates an `ID2D1Bitmap` once and reuses it.

	See [IJSImage CreateBitmap](IJSImage.md#createbitmap) and [utils.LoadBitmap](../namespaces/utils.md#utilsloadbitmappath-max_size).

**Properties**

|||||
|---|---|---|---|
|Height|`number`|read|
|Width|`number`|read|

**Methods**

## `Dispose()`
No return value.
