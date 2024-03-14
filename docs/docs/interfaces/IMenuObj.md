!!! example
	```js
	// ==PREPROCESSOR==
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	// Click anywhere to open menu and change background colour.

	var colours = [
		RGB(255, 0, 0),
		RGB(0, 255, 0),
		RGB(0, 0, 255)
	];

	var colour_index = 0;

	function on_mouse_lbtn_down(x, y) {
		var menu = window.CreatePopupMenu();

		// start at 1, not 0
		menu.AppendMenuItem(MF_STRING, 1, 'Red');
		menu.AppendMenuItem(MF_STRING, 2, 'Green');
		menu.AppendMenuItem(MF_STRING, 3, 'Blue');

		// mark current selection
		menu.CheckMenuRadioItem(1, 3, colour_index + 1);

		var idx = menu.TrackPopupMenu(x, y);
		menu.Dispose();

		switch (idx) {
			case 0:
				// user dismissed menu by clicking elsewhere. that's why you can't use 0 when building menu items
				break;
			case 1:
			case 2:
			case 3:
				colour_index = idx - 1;
				window.Repaint();
				break;
		}
	}

	function on_paint(gr) {
		gr.Clear(colours[colour_index]);
	}
	```

**Methods**

## `AppendMenuItem(flags, item_id, text)`
|Arguments|||
|---|---|---|
|flags|[AppendMenuItem Flags](../flags.md#appendmenuitem-flags)|
|item_id|`number`|Must not be zero. Each id must be unique.|
|text|`string`|

No return value.

## `AppendMenuSeparator()`
No return value.

## `AppendTo(parentMenu, flags, text)`
|Arguments|||
|---|---|---|
|parentMenu|[IMenuObj](IMenuObj.md)|
flags|[AppendMenuItem Flags](../flags.md#appendmenuitem-flags)|
|text|`string`|

No return value.

## `CheckMenuItem(item_id, check)`
|Arguments|||
|---|---|---|
|item_id|`number`|
|check|`boolean`|

No return value.

## `CheckMenuRadioItem(first_item_id, last_item_id, selected_item_id)`
|Arguments|||
|---|---|---|
|first_item_id|`number`|
|last_item_id|`number`|
|selected_item_id|`number`|

No return value.

## `Dispose()`
No return value.

## `SetDefault(item_id)`
|Arguments|||
|---|---|---|
|item_id|`number`|

Setting a menu item as default enables a bold font. You'd typically use it for a
default action such as a `Play` command for a selected playlist item which you
could also trigger by pressing the ++enter++ key.

!!! note
	You can only set a single item as the default. Any further attempt on the same
	menu object will result in a script error.

## `TrackPopupMenu(x, y[, flags])`
|Arguments|||
|---|---|---|
|x|`number`|
|y|`number`|
|flags|[TrackPopupMenu Flags](../flags.md#trackpopupmenu-flags)|Default `0`.|

Returns a `number`.
