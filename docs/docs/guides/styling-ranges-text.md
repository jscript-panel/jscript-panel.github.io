!!! note
	As of component version `3.6.0`, `gr.WriteText`, `utils.CreateTextLayout` and `utils.CreateTextLayout2`
	support `$rgb` code natively and you may it find it easier to use than the methods described below.
	But these techniques can be useful when not using title formatting.

	None of this is supported in `gr.WriteText2` as it has native `$rgb` and `$font` support.

## Using `IJSGraphics WriteText`

This first example uses [IJSGraphics WriteText](../interfaces/IJSGraphics.md#writetexttext-font-colour-x-y-w-h-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity)
where you can apply custom fonts/colours to a single string. The limitation here is that
scrolling text vertically is not supported so if you need that, you'll need to use
the `utils.CreateTextLayout` / `utils.CreateTextLayout2` examples below.

!!! note
	You can load this directly from the [Configuration Window](../configuration-window.md) `Samples` button `basic/WriteTextStyles`.

!!! example
	```js
	// ==PREPROCESSOR==
	// @name "WriteTextStyles"
	// @author "marc2003"
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	/*
	This sample splits a string in to whole words and then randomly
	styles each one. Every element of the array which is used for
	styling must have a valid start/length value. You can see
	how the start value is incremented for each word.
	*/

	var installed_fonts = utils.ListFonts().toArray();
	var text = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.';

	var colour_string = '';
	var font_string = '';

	// split text in to whole words for styling
	var words = text.split(' ');

	refresh();

	function refresh() {
		var fonts = [], colours = [];
		var start = 0;

		words.forEach(function(word, i) {
			// length of word plus following space
			var len = word.length + 1;

			colours.push({
				// when using an array of colours, Start and Length are mandatory
				Start : start,
				Length : len,
				Colour : RGB(Math.random() * 200, Math.random() * 200, Math.random() * 200),
			});

			fonts.push({
				// when using an array of fonts, Start and Length are mandatory
				Start : start,
				Length : len,
				// the following are all optional and may be omitted. Segoe UI/16px will be used if Name/Size are not specified.
				Name : installed_fonts[Math.floor(Math.random() * installed_fonts.length)],
				Size : 12 + Math.floor(Math.random() * 20),
				Weight : Math.round(Math.random() * 800) + 100, // values between 100-900
				Underline : Math.random() < 0.1,
				Strikethrough : Math.random() < 0.1,
			});

			// increment start position for next word
			start += len;
		});

		colour_string = JSON.stringify(colours);
		font_string = JSON.stringify(fonts);
	}

	function on_paint(gr) {
		gr.WriteText(text, font_string, colour_string, 10, 10, window.Width - 20, window.Height - 20);
	}
	```

## Using `utils.CreateTextLayout`
Use something like this if you want scrollable text, a single font and to apply different colours.

!!! note
	You can load this directly from the [Configuration Window](../configuration-window.md) `Samples` button `basic/SimpleScroll + Coloured Text`.

!!! example
	```js
	// ==PREPROCESSOR==
	// @name "SimpleScroll + Coloured Text"
	// @author "marc2003"
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	var text = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.';
	var layout = utils.CreateTextLayout(text, 'Segoe UI', 24);
	var offset = 0;
	var text_height = 0;

	// split text in to whole words for colouring
	var words = text.split(' ');
	var colour_string = '';

	refresh();

	function refresh() {
		var colours = [];
		var start = 0;
		words.forEach(function(word, i) {
			var len = word.length + 1;
			colours.push({
				// when using an array, Start and Length are mandatory
				Start : start,
				Length : len,
				Colour : RGB(Math.random() * 200, Math.random() * 200, Math.random() * 200),
			});
			start += len;
		});
		colour_string = JSON.stringify(colours);
	}

	var box = {
		x : 50,
		y : 50,
		w : 0,
		h : 0,
	}

	function on_paint(gr) {
		gr.Clear(RGB(255, 255, 255));
		gr.DrawRectangle(box.x, box.y, box.w, box.h, 1, RGB(255, 0, 0));
		gr.WriteTextLayout(layout, colour_string, box.x, box.y, box.w, box.h, offset);
	}

	function on_mouse_wheel(step) {
		if (text_height < box.h) return;
		offset += step * 60;
		if (offset > 0) offset = 0;
		else if (offset < box.h - text_height) offset = box.h - text_height;
		window.Repaint();
	}

	function on_size() {
		box.w = window.Width / 2;
		box.h = window.Height / 2;
		text_height = layout.CalcTextHeight(box.w);
		if (text_height < box.h) offset = 0;
		else if (offset < box.h - text_height) offset = box.h - text_height;
	}
	```

## Using `utils.CreateTextLayout2`
Use something like this if you want scrollable text, custom fonts and to apply different colours.

!!! note
	You can load this directly from the [Configuration Window](../configuration-window.md) `Samples` button `basic/SimpleScroll + Styled Text`.

!!! example
	```js
	// ==PREPROCESSOR==
	// @name "SimpleScroll + Styled Text"
	// @author "marc2003"
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	var installed_fonts = utils.ListFonts().toArray();
	var text = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.';
	var layout = null;
	var offset = 0;
	var text_height = 0;
	var colour_string = '';

	// split text in to whole words for styling
	var words = text.split(' ');

	refresh();

	function refresh() {
		var fonts = [];
		var colours = [];
		var start = 0;
		words.forEach(function(word, i) {
			// length of word plus following space
			var len = word.length + 1;

			fonts.push({
				// When using an array of fonts, Start and Length are mandatory
				Start : start,
				Length : len,
				// The following are all optional and may be omitted.
				// Segoe UI/16px will be used if Name/Size are not specified.
				Name : installed_fonts[Math.floor(Math.random() * installed_fonts.length)],
				Size : 12 + Math.floor(Math.random() * 20),
				Weight : Math.round(Math.random() * 800) + 100, // values between 100-900
				Underline : Math.random() < 0.1,
				Strikethrough : Math.random() < 0.1,
			});

			colours.push({
				// When using an array of colours, Start and Length are mandatory
				Start : start,
				Length : len,
				Colour : RGB(Math.random() * 200, Math.random() * 200, Math.random() * 200),
			});

			// increment start position for next word
			start += len;
		});

		// Stringify the fonts and create the text layout
		var font_string = JSON.stringify(fonts);
		layout = utils.CreateTextLayout2(text, font_string);

		// Stringify the colours. This is passed to WriteTextLayout inside on_paint
		colour_string = JSON.stringify(colours);
	}

	var box = {
		x : 50,
		y : 50,
		w : 0,
		h : 0,
	}

	function on_paint(gr) {
		gr.Clear(RGB(255, 255, 255));
		gr.DrawRectangle(box.x, box.y, box.w, box.h, 1, RGB(255, 0, 0));

		/*
		The 2nd arg of gr.WriteTextLayout is the colour which can be a
		number if you want the same colour for the whole range of text.

		In this example, we're using the stringified colours array created in the
		refresh method above.
		*/
		gr.WriteTextLayout(layout, colour_string, box.x, box.y, box.w, box.h, offset);
	}

	function on_mouse_wheel(step) {
		if (text_height < box.h) return;
		offset += step * 60;
		if (offset > 0) offset = 0;
		else if (offset < box.h - text_height) offset = box.h - text_height;
		window.Repaint();
	}

	function on_size() {
		box.w = window.Width / 2;
		box.h = window.Height / 2;
		text_height = layout.CalcTextHeight(box.w);
		if (text_height < box.h) offset = 0;
		else if (offset < box.h - text_height) offset = box.h - text_height;
	}
	```
