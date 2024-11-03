**Properties**

|||||
|---|---|---|---|
|window.DPI|`number`|read|This value is fixed when [foobar2000](https://www.foobar2000.org) starts. It will not change even if Windows display settings are updated.
|window.Height|`number`|read|
|window.ID|`number`|read|Unique identifier for the panel. Use in various `async` methods.|
|window.IsDark|`boolean`|read|
|window.IsDefaultUI|`boolean`|read|
|window.IsVisible|`boolean`|read|Only returns `false` when panel is hidden in a tab. When covered by other windows, it still returns `true`.
|window.MaxHeight|`number`|read, write|
|window.MaxWidth|`number`|read, write|
|window.MinHeight|`number`|read, write|
|window.MinWidth|`number`|read, write|
|[window.Name](../preprocessors.md#name)|`string`|read|
|window.Width|`number`|read|

**Methods**

## `window.ClearInterval(timerID)`
|Arguments|||
|---|---|---|
|timerID|`number`|

No return value.

## `window.ClearTimeout(timerID)`
|Arguments|||
|---|---|---|
|timerID|`number`|

No return value.

## `window.CreatePopupMenu()`
Returns an [IMenuObj](../interfaces/IMenuObj.md) instance.

## `window.CreateTooltip([font_name, font_size_px)`
|Arguments|||
|---|---|---|
|font_name|`string`|Default `Segoe UI`.|
|font_size_px|`number`|Default `16`.|

Returns an [ITooltip](../interfaces/ITooltip.md) instance.

!!! note
	Since it's not permitted to call this more than once
	in a panel, see the additional [window.SetTooltipFont](#windowsettooltipfontfont_name-font_size_px)
	method too.

## `window.GetColourCUI(type)`
|Arguments|||
|---|---|---|
|type|[ColourTypeCUI](../flags.md#colourtypecui)|

Returns a `number` which can used as the `colour` in many methods.

## `window.GetColourDUI(type)`
|Arguments|||
|---|---|---|
|type|[ColourTypeDUI](../flags.md#colourtypedui)|

Returns a `number` which can used as the `colour` in many methods.

## `window.GetFontCUI(type)`
|Arguments|||
|---|---|---|
|type|[FontTypeCUI](../flags.md#fonttypecui)|

Returns a `string` which can be passed directly to [IJSGraphics WriteText](../interfaces/IJSGraphics.md#writetexttext-font-colour-x-y-w-h-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity).

!!! example
	```js
	var font = window.GetFontCUI(0);
	var colour = ...

	function on_paint(gr) {
		gr.WriteText("some text", font, colour, 0, 0, window.Width, window.Height);
	}
	```

See the [Fonts](../guides/fonts.md) page for how font properties can be accessed or modified.

## `window.GetFontDUI(type)`
|Arguments|||
|---|---|---|
|type|[FontTypeDUI](../flags.md#fonttypedui)|

See above for the return value.

## `window.GetProperty(name[, default_value])`
|Arguments|||
|---|---|---|
|name|`string`|
|default_value|`string`,`number`,`boolean`|Default `null`.|

Returns the value of `name` from the panel properties. If no value is
present and `default_value` is not `null` or `undefined`, it will be
stored and returned.

!!! example
	```js
	// ==PREPROCESSOR==
	// @name "ColourPicker + Persistent Properties"
	// @author "marc2003"
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	var default_colour = RGB(255, 0, 0);

	// Default colour is used on first run, otherwise colour
	// saved on previous use.
	var colour = window.GetProperty('BASIC.COLOUR.PICKER.COLOUR', default_colour);

	function on_paint(gr) {
		gr.Clear(colour);
		gr.FillRectangle(0, 0, window.Width, 24, RGB(0, 0, 0));
		gr.WriteText('Click to open ColourPicker', '', RGB(255, 255, 255), 0, 0, window.Width, 24, 2, 0);
	}

	function on_mouse_lbtn_up() {
		colour = utils.ColourPicker(colour);

		/*
		Save the new colour and it will be read the next
		time the script starts. These properties are stored
		as part of your layout either in theme.fth (Default UI)
		or foo_ui_columns.cfg (Columns UI),
		*/
		window.SetProperty('BASIC.COLOUR.PICKER.COLOUR', colour);
		window.Repaint();
	}
	```

## `window.NotifyOthers(name, info)`
|Arguments|||
|---|---|---|
|name|`string`|
|info|`string`, `number`, `array`, `object`|

Listen for notifications in other panels with [on_notify_data](../callbacks/component.md#on_notify_dataname-info).

## `window.Reload([clear_properties])`
|Arguments|||
|---|---|---|
|clear_properties|`boolean`|Default `false`.|

No return value.

## `window.Repaint()`
No return value.

## `window.RepaintRect(x, y, w, h)`
No return value.

!!! note
	Use this instead of `window.Repaint` on frequently updated areas
	such as time, bitrate, seekbar, etc.

## `window.SetCursor(id)`
|Arguments|||
|---|---|---|
|id|[SetCursorID](../flags.md#setcursor-values)|Use `-1` if you want to hide the cursor.|

No return value.

!!! note
	This would usually be used inside the [on_mouse_move](../callbacks/windows.md#on_mouse_movex-y-mask) callback.

## `window.SetInterval(func, delay)`
|Arguments|||
|---|---|---|
|function|`function`|
|delay|`number`|milliseconds

The return value is the `timerID` which can be used
to cancel it.

Creates a timer that will run indefinitely unless cancelled.

!!! example
	```js
	// This runs every 500ms forever because the return
	// was ignored!
	window.SetInterval(function () {
		// do something
	}, 500);
	```

No return value.

## `window.SetPlaylistSelectionTracking()`
No return value.

Sets selected items to the active playlist selection and enables tracking.
When the playlist selection changes, the stored selection is automatically
updated.

!!! example
	```js
	// Playlist view example

	function on_focus(is_focused) {
		if (is_focused) {
			// Updates the selection when panel regains focus
			// but not on every click
			window.SetPlaylistSelectionTracking();
		}
	}
	```

## `window.SetPlaylistTracking()`
No return value.

## `window.SetProperty(name, value)`
|Arguments|||
|---|---|---|
|name|`string`|
|value|`string`,`number`,`boolean`|

No return value.

Sets a persistent property value. To remove an existing property, you
can supply `null` as the `value`.

See [window.GetProperty](#windowgetpropertyname-default_value) for an example.

## `window.SetSelection(handle_list[, type])`
|Arguments|||
|---|---|---|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList.md)|
|type|[SelectionType](../flags.md#selectiontype)|Default `0`.|

!!! example
	```js
	// Library viewer example

	function on_mouse_lbtn_up(x, y) {
		// Presumably going to select something here...
		handle_list = ...;
		window.SetSelection(handle_list, 6);
	}
	```

## `window.SetTimeout(func, delay)`
|Arguments|||
|---|---|---|
|function|`function`|
|delay|`number`|milliseconds

The return value is the `timerID` which can be used
to cancel it.

!!! example
	```js
	window.SetTimeout(function () {
		// code here will run after 10 seconds, once.
	}, 10000);
	```

## `window.SetTooltipFont(font_name, font_size_px)`
|Arguments|||
|---|---|---|
|font_name|`string`|
|font_size_px|`number`|

No return value.

## `window.ShowConfigure()`

No return value.

Shows the [Configuration Window](../configuration-window.md).

## `window.ShowProperties()`

No return value.

Shows the `Properties Window` of the current panel.
