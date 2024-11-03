This page is specifically for working with fonts that are passed
to [IJSGraphics WriteText](../interfaces/IJSGraphics.md#writetexttext-font-colour-x-y-w-h-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity).

Unlike previous versions of `JScript Panel`, fonts need to be supplied as strings. They can be created manually by
using `JSON.stringify` on an object or returned from `window.GetFontCUI` and `window.GetFontDUI`.

These are all of the supported properties but none are mandatory.

```js
var font = JSON.stringify({
	Name : name, // string
	Size : size, // number
	Weight : weight, // number
	Style : style, // number
	Stretch : stretch, // number
	Underline : underline, // boolean
	Strikethrough : strikethrough, // boolean
});
```

See [Flags](../flags.md) for supported `Weight`, `Style` and `Stretch` values.

You can even supply an empty string and defaults
of `Segoe UI` and `16px` will be used.

!!! example
	```js
	var font_str = "";
	var colour = RGB(0, 0, 0);
	gr.WriteText("some text", font_str, colour, 0, 0, window.Width, window.Height);
	```

## Using `window.GetFontCUI` / `window.GetFontDUI`.

!!! example
	```js
	var font_str = window.GetFontDUI(0);
	console.log(font_str);
	```

	``` markdown title="Example output"
	{
		"Name": "Segoe UI",
		"Size": 12,
		"Stretch": 5,
		"Style": 0,
		"Weight": 400
	}
	```

`font_str` can be passed directly to `gr.WriteText` without modification.

!!! example
	```js
	var font_str = window.GetFontDUI(0);
	var colour = RGB(0, 0, 0);

	function on_paint(gr) {
		gr.WriteText("some text", font_str, colour, 0, 0, window.Width, window.Height);
	}
	```


!!! note
	Not all fonts supported by `Default UI` / `Columns UI` can be used by this component. This
	is because they use older `GDI` graphics whereas this component uses `DirectWrite`. If
	an unsupported font is detected, the method will fallback to returning `Segoe UI`. The most
	likely cause of this happening would be using `Raster` fonts like `System` or `Small Fonts`.

If you want to manipulate any of the properties, you can use `JSON.parse` on the string, make the changes
and then stringify it again.

!!! example
	```js
	var font_str = window.GetFontDUI(0);
	var font_obj = JSON.parse(font_str);

	// double the size, leave other properties untouched.
	font_obj.Size = font_obj.Size * 2;

	font_str = JSON.stringify(font_obj);
	```

## Creating your own from scratch

Writing your own `JSON.stringify` statement for every font you create would be a bit cumbersome
so you should consider writing your own helper function.

This is a simple one to give you an idea:

!!! example
	```js
	// ==PREPROCESSOR==
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	function create_font_string(name, size, bold) {
		return JSON.stringify({
			Name : name,
			Size : size,
			Weight : bold ? DWRITE_FONT_WEIGHT_BOLD : DWRITE_FONT_WEIGHT_NORMAL,
		});
	}

	// Now it's easier to write...

	var font = create_font_string("Verdana", 16);
	var large_bold_font = create_font_string("Verdana", 24, true);
	```

## Advanced usage

You can also create an array of fonts and apply them to a single string. You can style each word or even character
independently. See [Styling Ranges Of Text](styling-ranges-text.md).
