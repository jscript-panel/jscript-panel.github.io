**Methods**

## `Clear(colour)`
|Arguments|||
|---|---|---|
|colour|`number`|

Clears entire panel with `colour`.

No return value.

## `DrawBitmap(bitmap, dstX, dstY, dstW, dstH, srcX, srcY, srcW, srcH[, opacity, angle])`
:octicons-tag-24: 3.8.4

|Arguments|||
|---|---|---|
|bitmap|[IJSBitmap](IJSBitmap.md)|
|dstX|`number`|
|dstY|`number`|
|dstW|`number`|
|dstH|`number`|
|srcX|`number`|
|srcY|`number`|
|srcW|`number`|
|srcH|`number`|
|opacity|`number`|Floating point number between `0` and `1`. Default `1`.|
|angle|`number`|Default `0`.|

No return value.

## `DrawEllipse(centreX, centreY, radiusX, radiusY, line_width, colour)`
|Arguments|||
|---|---|---|
|centreX|`number`|
|centreY|`number`|
|radiusX|`number`|
|radiusY|`number`|
|line_width|`number`|
|colour|`number`,`string`|This can be a solid colour or [gradient](../guides/gradients.md).|

No return value.

## `DrawImage(image, dstX, dstY, dstW, dstH, srcX, srcY, srcW, srcH[, opacity, angle])`
|Arguments|||
|---|---|---|
|image|[IJSImage](IJSImage.md)|
|dstX|`number`|
|dstY|`number`|
|dstW|`number`|
|dstH|`number`|
|srcX|`number`|
|srcY|`number`|
|srcW|`number`|
|srcH|`number`|
|opacity|`number`|Floating point number between `0` and `1`. Default `1`.|
|angle|`number`|Default `0`.|

No return value.

## `DrawImageWithMask(image, mask_image, x, y, w, h)`
|Arguments|||
|---|---|---|
|image|[IJSImage](IJSImage.md)|
|mask_image|[IJSImage](IJSImage.md)|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|

!!! example
	Because this method does not support src co-ords,
	this sample makes the original image square first which is more
	suitable for a circular mask. Also included is a text mask example.

	Unlike the previous `ApplyMask`, there should be no white background.
	Just draw black for where you want to keep.

	Mask images don't have to have the same width/height.

	```js

	// ==PREPROCESSOR==
	// @name "DrawImageWithMask"
	// @author "marc2003"
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	var temp_gr;

	var circular_mask = utils.CreateImage(512, 512);
	temp_gr = circular_mask.GetGraphics();
	temp_gr.FillEllipse(256, 256, 256, 256, RGB(0, 0, 0));
	circular_mask.ReleaseGraphics();
	temp_gr = null;

	var text_mask = utils.CreateImage(512, 512);
	temp_gr = text_mask.GetGraphics();
	temp_gr.DrawRectangle(0, 0, 512, 512, 10, RGB(0, 0, 0));
	temp_gr.WriteText("MASK", JSON.stringify({Size:160,Weight:900}), RGB(0, 0, 0), 0, 0, 512, 512, 2, 2);
	text_mask.ReleaseGraphics();
	temp_gr = null;

	var img = utils.LoadImage(fb.ComponentPath + 'samples\\images\\1.webp');
	var square = make_square(img, 300);

	function make_square(img, size) {
		if (!img) return null;

		if (img.Width < img.Height) {
			var src_x = 0;
			var src_w = img.Width;
			var src_h = img.Width;
			var src_y = Math.round((img.Height - src_h) / 4);
		} else {
			var src_y = 0;
			var src_w = img.Height;
			var src_h = img.Height;
			var src_x = Math.round((img.Width - src_w) / 2);
		}

		var square = utils.CreateImage(size, size);
		var temp_gr = square.GetGraphics();
		temp_gr.DrawImage(img, 0, 0, size, size, src_x, src_y, src_w, src_h);
		square.ReleaseGraphics();
		return square;
	}

	function on_paint(gr) {
		gr.Clear(RGB(255, 0, 0));
		// original image as-is
		gr.DrawImage(img, 0, 0, img.Width, img.Height, 0, 0, img.Width, img.Height);
		// squared image, no mask
		gr.DrawImage(square, 0, img.Height, square.Width, square.Height, 0, 0, square.Width, square.Height)
		// squared image, circular mask
		gr.DrawImageWithMask(square, circular_mask, 300, img.Height, square.Width, square.Height);
		// squared image, text mask
		gr.DrawImageWithMask(square, text_mask, 600, img.Height, square.Width, square.Height);
	}
	```

## `DrawLine(x1, y1, x2, y2, line_width, colour)`
|Arguments|||
|---|---|---|
|x1|`number`|
|y1|`number`|
|x2|`number`|
|y2|`number`|
|line_width|`number`|
|colour|`number`,`string`|This can be a solid colour or [gradient](../guides/gradients.md).|

No return value.

## `DrawRectangle(x, y, w, h, line_width, colour)`
|Arguments|||
|---|---|---|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|
|line_width|`number`|
|colour|`number`,`string`|This can be a solid colour or [gradient](../guides/gradients.md).|

No return value.

## `DrawRoundedRectangle(x, y, w, h, radiusX, radiusY, line_width, colour)`
|Arguments|||
|---|---|---|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|
|radiusX|`number`|
|radiusY|`number`|
|line_width|`number`|
|colour|`number`,`string`|This can be a solid colour or [gradient](../guides/gradients.md).|

No return value.

## `FillEllipse(centreX, centreY, radiusX, radiusY, colour)`
|Arguments|||
|---|---|---|
|centreX|`number`|
|centreY|`number`|
|radiusX|`number`|
|radiusY|`number`|
|colour|`number`,`string`|This can be a solid colour or [gradient](../guides/gradients.md).|

No return value.

## `FillRectangle(x, y, w, h, colour)`
|Arguments|||
|---|---|---|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|
|colour|`number`,`string`|This can be a solid colour or [gradient](../guides/gradients.md).|

No return value.

## `FillRoundedRectangle(x, y, w, h, radiusX, radiusY, colour)`
|Arguments|||
|---|---|---|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|
|radiusX|`number`|
|radiusY|`number`|
|colour|`number`,`string`|This can be a solid colour or [gradient](../guides/gradients.md).|

No return value.

## `WriteText(text, font, colour, x, y, w, h[, text_alignment, paragraph_alignment, word_wrapping, trimming_granularity])`
|Arguments|||
|---|---|---|
|text|`string`|As of component version `3.6.0`, this may contain `$rgb` code.
|font|`string`|See note below.|
|colour|`number`, `string`|See note below.|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|
|text_alignment|[DWRITE_TEXT_ALIGNMENT](../flags.md#dwrite_text_alignment)|Default `0`.|
|paragraph_alignment|[DWRITE_PARAGRAPH_ALIGNMENT](../flags.md#dwrite_paragraph_alignment)|Default `0`.|
|word_wrapping|[DWRITE_WORD_WRAPPING](../flags.md#dwrite_word_wrapping)|Default `0`.|
|trimming_granularity|[DWRITE_TRIMMING_GRANULARITY](../flags.md#dwrite_trimming_granularity)|Default `0`.|

No return value.

!!! note
	The `font` must be in string form and this can come directly from using [window.GetFontCUI](../namespaces/window.md#windowgetfontcuitype) / [window.GetFontDUI](../namespaces/window.md#windowgetfontduitype).
	See the dedicated [Fonts](../guides/fonts.md) page for how to create/manipulate your own. Using an array of fonts for styling substrings of the text is also supported. See [Styling Ranges Of Text](../guides/styling-ranges-text.md).

!!! note
	If you want to apply a single colour to all of the text, simply supply a `number`.

	If supplying a `string`, it must be a stringified array. See [Styling Ranges Of Text](../guides/styling-ranges-text.md). `$rgb`
	code in the `text` always takes precedence so if an array is supplied at the same time, it will be ignored.

## `WriteText2(text, font, colour, x, y, w, h[, text_alignment, paragraph_alignment, word_wrapping, trimming_granularity])`
:octicons-tag-24: 3.6.0

|Arguments|||
|---|---|---|
|text|`string`|May contain `$rgb` and `$font` code.
|font|`string`|See note below. Unlike the original `WriteText`, this must be a single font only.|
|colour|`number`|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|
|text_alignment|[DWRITE_TEXT_ALIGNMENT](../flags.md#dwrite_text_alignment)|Default `0`.|
|paragraph_alignment|[DWRITE_PARAGRAPH_ALIGNMENT](../flags.md#dwrite_paragraph_alignment)|Default `0`.|
|word_wrapping|[DWRITE_WORD_WRAPPING](../flags.md#dwrite_word_wrapping)|Default `0`.|
|trimming_granularity|[DWRITE_TRIMMING_GRANULARITY](../flags.md#dwrite_trimming_granularity)|Default `0`.|

No return value.

!!! note
	The `font` must be in string form and this can come directly from using [window.GetFontCUI](../namespaces/window.md#windowgetfontcuitype) / [window.GetFontDUI](../namespaces/window.md#windowgetfontduitype).
	See the dedicated [Fonts](../guides/fonts.md) page for how to create/manipulate your own.

## `WriteTextLayout(text_layout, colour, x, y, w, h, vertical_offset)`
|Arguments|||
|---|---|---|
|text_layout|[ITextLayout](ITextLayout.md)|
|colour|`number`, `string`|See note below.|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|
|vertical_offset|`number`|Default `0`.|

!!! note
	If you want to apply a single colour to all of the text, simply supply a `number`.

	If supplying a `string`, it must be a stringified array. See [Styling Ranges Of Text](../guides/styling-ranges-text.md).

See [utils.CreateTextLayout](../namespaces/utils.md#utilscreatetextlayouttext-font_name-font_size-font_weight-font_style-font_stretch-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity) and
[utils.CreateTextLayout2](../namespaces/utils.md#utilscreatetextlayout2text-fonts-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity) for examples.

## `WriteTextSimple(text, font, colour, x, y, w, h[, text_alignment, paragraph_alignment, word_wrapping, trimming_granularity])`
:octicons-tag-24: 3.6.3

|Arguments|||
|---|---|---|
|text|`string`|`$rgb` and `$font` code will be ignored.
|font|`string`|See note below. Must be a single font only. Also, `Underline` and `Strikethrough` properties are not supported and will be ignored.
|colour|`number`|
|x|`number`|
|y|`number`|
|w|`number`|
|h|`number`|
|text_alignment|[DWRITE_TEXT_ALIGNMENT](../flags.md#dwrite_text_alignment)|Default `0`.|
|paragraph_alignment|[DWRITE_PARAGRAPH_ALIGNMENT](../flags.md#dwrite_paragraph_alignment)|Default `0`.|
|word_wrapping|[DWRITE_WORD_WRAPPING](../flags.md#dwrite_word_wrapping)|Default `0`.|
|trimming_granularity|[DWRITE_TRIMMING_GRANULARITY](../flags.md#dwrite_trimming_granularity)|Default `0`.|

No return value.

!!! note
	The `font` must be in string form and this can come directly from using [window.GetFontCUI](../namespaces/window.md#windowgetfontcuitype) / [window.GetFontDUI](../namespaces/window.md#windowgetfontduitype).
	See the dedicated [Fonts](../guides/fonts.md) page for how to create/manipulate your own.
