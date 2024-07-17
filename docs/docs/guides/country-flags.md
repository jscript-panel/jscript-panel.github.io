!!! note
	This requires that you have the [Twemoji Mozilla](https://github.com/mozilla/twemoji-colr/releases/latest) font installed.

While it has always been possible to display flags with images or writing your own scripts
to make use of emoji, this details some helper methods which have been added to make it
easier.

First of all, there is a simple `utils.GetCountryFlag` method which accepts a 2 letter country
code or the full country name. See [supported values](#supported-values). An empty string
will be returned on failure.

!!! example
	```js
	// ==PREPROCESSOR==
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	var font = CreateFontString("Twemoji Mozilla", 24);
	var flag = utils.GetCountryFlag("GB");

	function on_paint(gr) {
		gr.WriteText(flag, font, 0, 0, 0, window.Width, window.Height, 2, 2);
	}
	```

## Title formatting

!!! note
	These examples assume you have a [supported value](#supported-values) inside a `%country%` tag. Adjust as
	necessary.

A `$country_flag` function has been added and you can use it like this:

```
$font(Twemoji Mozilla,16)$country_flag(%country%)
```

If using the `Text Display` sample, the `$font` parsing is handled automatically.

!!! note
	The use of `$font` is detailed [here](font-rgb.md). If you want to
	utilise `$font` in your own scripts, you can use `gr.WriteText2`.
	It also supports `$rgb` if you want to combine that for other text.

!!! example
	```js
	// ==PREPROCESSOR==
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	// $font() with no args resets back to the default_font supplied to
	// DrawStyledText in on_paint
	// also includes $rgb example
	var tfo = fb.TitleFormat(
		"[$font(Twemoji Mozilla,18)$country_flag(%country%)$font() ]$rgb(255,0,0)%artist%"
	);
	var str = "";

	refresh();

	function refresh() {
		var item = fb.GetFocusItem();
		if (item) {
			str = tfo.EvalWithMetadb(item);
		} else {
			str = "";
		}
	}

	function on_item_focus_change() {
		refresh();
		window.Repaint();
	}

	function on_playlist_switch() {
		refresh();
		window.Repaint();
	}

	function on_paint(gr) {
		// default_font is an empty string, defaulting to Segoe UI, 16px
		gr.WriteText2(str, "", 0, 0, 0, window.Width, window.Height, 2, 2);
	}
	```

## Supported values

Case is not important. You can supply the code or full name. A few examples:

|||
|---|---|
|gb|United Kingdom|
|fr|France|
|de|Germany|

A complete list of supported values can be found in this file: [countries.json](../../files/countries.json)
