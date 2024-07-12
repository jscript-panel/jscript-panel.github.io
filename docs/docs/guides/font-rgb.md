!!! note
	For sample users, `Text Display` handles `$font` code automatically.
	As of component `3.6.0`, `$rgb` is supported everywhere that supports
	custom title formatting.

	Parsing `$font` code for use in your own scripts can be done with the helper
	method detailed below.

### $rgb

You can use these colour methods which are documented [here](https://wiki.hydrogenaud.io/index.php?title=Foobar2000:Title_Formatting_Reference#Historical_and_Columns_UI_color_functions).

```
$rgb(r,g,b) // only the 3 value variant is supported
$rgb()
$hsl(h,s,l) // only the 3 value variant is supported
$hsl()
$blend(colour1,colour2,part,total)
$transition(string,colour1,colour2)
```

### $font
As of component version `3.1.9`, a `$font` function has been added. This is not a
common function and is exclusive to `JScript Panel 3`. It takes up to 6 values.

`$font(name,size,weight,style,underline,strikethrough)`

If changing the font, you must the supply the `name` and `size` values. The rest are optional.

|Value||
|---|---|
|size|Supported values are `8` - `144`.
|weight|Default `400`, `700` is bold. Supported values are `100` - `950`.|
|style|Default `0`. Use `1` for `oblique` or `2` for `italic`.|
|underline|Default `0`. Use `1` to enable.|
|strikethrough|Default `0`. Use `1` to enable.|

You can use `$font()` with no values to reset back to default.

### Using in your own scripts.

!!! note
	As of component version `3.6.0`, `DrawColouredText` provided in `helpers.txt`
	is obsolete. `gr.WriteText` now has `$rgb` parsing built in. All included
	samples have been updated but some may need reloading from the `Samples` button.

Use `DrawStyledText` when you want to use `$font` or `$font / $rgb` combined.

```
// added in component version 3.3.19
DrawStyledText(gr, text, default_font, default_colour, x, y, w, h[, text_alignment, paragraph_alignment, word_wrapping, trimming_granularity])
```

This is a drop in replacement for `gr.WriteText` and accepts the same arguments in the same order.

!!! example
	=== "$rgb & $font"
		```js
		// ==PREPROCESSOR==
		// @import "%fb2k_component_path%helpers.txt"
		// ==/PREPROCESSOR==

		var tfo = fb.TitleFormat("$font(Segoe UI,24)$rgb(255,0,0)%artist%$font() $font(Segoe UI,32)$rgb(0,255,0)%title%");
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
			DrawStyledText(gr, str, "", 0, 0, 0, window.Width, window.Height, 2, 2, 2);
		}
		```
