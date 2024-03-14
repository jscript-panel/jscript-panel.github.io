## `BuildMenu(parentMenu, base_id)`
|Arguments|||
|---|---|---|
|parentMenu|[IMenuObj](IMenuObj.md)|
|base_id|`number`|

No return value.

## `Dispose()`
No return value.

## `ExecuteByID(id)`
|Arguments|||
|---|---|---|
|id|`number`|

Returns a `boolean` value.

!!! example
	```js
	// ==PREPROCESSOR==
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	// Click anywhere in the panel to open the menu.

	function on_mouse_lbtn_up(x, y) {
		var menu = window.CreatePopupMenu();
		var file_popup = window.CreatePopupMenu();
		var edit_popup = window.CreatePopupMenu();
		var view_popup = window.CreatePopupMenu();
		var playback_popup = window.CreatePopupMenu();
		var library_popup = window.CreatePopupMenu();
		var help_popup = window.CreatePopupMenu();

		var file = fb.CreateMainMenuManager('File');
		var edit = fb.CreateMainMenuManager('Edit');
		var view = fb.CreateMainMenuManager('View');
		var playback = fb.CreateMainMenuManager('Playback');
		var library = fb.CreateMainMenuManager('Library');
		var help = fb.CreateMainMenuManager('Help');

		file.BuildMenu(file_popup, 1000);
		edit.BuildMenu(edit_popup, 2000);
		view.BuildMenu(view_popup, 3000);
		playback.BuildMenu(playback_popup, 4000);
		library.BuildMenu(library_popup, 5000);
		help.BuildMenu(help_popup, 6000);

		file_popup.AppendTo(menu, MF_STRING, 'File');
		edit_popup.AppendTo(menu, MF_STRING, 'Edit');
		view_popup.AppendTo(menu, MF_STRING, 'View');
		playback_popup.AppendTo(menu, MF_STRING, 'Playback');
		library_popup.AppendTo(menu, MF_STRING, 'Library');
		help_popup.AppendTo(menu, MF_STRING, 'Help');

		var idx = menu.TrackPopupMenu(x, y);
		menu.Dispose();

		switch (true) {
		case idx == 0:
			break;
		case idx < 2000:
			file.ExecuteByID(idx - 1000);
			break;
		case idx < 3000:
			edit.ExecuteByID(idx - 2000);
			break;
		case idx < 4000:
			view.ExecuteByID(idx - 3000);
			break;
		case idx < 5000:
			playback.ExecuteByID(idx - 4000);
			break;
		case idx < 6000:
			library.ExecuteByID(idx - 5000);
			break;
		case idx < 7000:
			help.ExecuteByID(idx - 6000);
			break;
		}

		file.Dispose();
		edit.Dispose();
		view.Dispose();
		playback.Dispose();
		library.Dispose();
		help.Dispose();
	}
	```
