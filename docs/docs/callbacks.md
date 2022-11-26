!!! note
	You should only use callbacks that contain code
	you want to run.

	It's not good practice to include empty callbacks like this:
	```js
	function on_always_on_top_changed(state) {

	}
	```

## `on_always_on_top_changed(state)`
|Arguments|||
|---|---|---|
|state|`boolean`|

Called when `Always On Top` state is changed.

## `on_char(code)`
|Arguments|||
|---|---|---|
|code|`number`|UTF16 encoded char|

## `on_colours_changed()`
Called when colours are changed via Default UI/Columns UI preferences.

## `on_console_refresh`
:octicons-tag-24: 3.1.0

Called whenever new messages appear in the [foobar2000](https://foobar2000.org) `Console`.

## `on_cursor_follow_playback_changed(state)`
|Arguments|||
|---|---|---|
|state|`boolean`|

Called when `Cursor follow playback` state is changed.

## `on_download_file_done(path, success, error_text)`
|Arguments|||
|---|---|---|
|path|`string`|The path that was originally supplied to [utils.DownloadFileAsync](../namespaces/utils/#utilsdownloadfileasyncwindow_id-url-path).|
|success|`boolean`|If `true` it means the web request was succesful and the file was saved correctly.|
|error_text|`string`|Empty if success is `true`. If success is `false`, it should describe what went wrong.|

Called when thread created by [utils.DownloadFileAsync](../namespaces/utils/#utilsdownloadfileasyncwindow_id-url-path) is done.

## `on_drag_drop(action, x, y, mask)`
|Arguments|||
|---|---|---|
|action|[IDropAction](../interfaces/IDropAction/)|
|x|`number`|
|y|`number`|
|mask|`number`|

## `on_drag_enter(action, x, y, mask)`
|Arguments|||
|---|---|---|
|action|[IDropAction](../interfaces/IDropAction/)|
|x|`number`|
|y|`number`|
|mask|`number`|

## `on_drag_leave()`

## `on_drag_over(action, x, y, mask)`
|Arguments|||
|---|---|---|
|action|[IDropAction](../interfaces/IDropAction/)|
|x|`number`|
|y|`number`|
|mask|`number`|

## `on_dsp_preset_changed()`
Called when DSP preset changes but does not get called when presets are added or removed.

## `on_focus(is_focused)`
|Arguments|||
|---|---|---|
|is_focused|`boolean`|

Called when the panel gets/loses focus.

## `on_font_changed()`
Called when fonts are changed via Default UI/Columns UI preferences.

## `on_get_album_art_done(handle, art_id, image)`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](../interfaces/IMetadbHandle/)|
|art_id|`number`|
|image|[IJSImage](../interfaces/IJSImage/)|Could be `null` on failure.|

Called when thread created by [IMetadbHandle GetAlbumArtAsync](../interfaces/IMetadbHandle/#getalbumartasyncwindow_id-art_id-want_stub) is done.

## `on_http_request_done(task_id, success, response_text)`
|Arguments|||
|---|---|---|
|task_id|`number`|The return value from the original [utils.HTTPRequestAsync](../namespaces/utils/#utilshttprequestasyncwindow_id-type-url-user_agent_or_headers-post_data-content_type) call.|
|success|`boolean`|If `true`, it doesn't necessarily mean http status 200 but it indicates the request was completed succesfully so the response text is from the server.|
|response_text|`string`|

Called when thread created by [utils.HTTPRequestAsync](../namespaces/utils/#utilshttprequestasyncwindow_id-type-url-user_agent_or_headers-post_data-content_type) is done.

## `on_item_focus_change(playlistIndex, from, to)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|
|from|`number`|
|to|`number`|

Called when playlist focus has changed.

## `on_item_played(handle)`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](../interfaces/IMetadbHandle/)|

Called when at least one minute of the track has been played or the track has reached its end after at least one third of it has been played.

## `on_key_down(vkey)`
|Arguments|||
|---|---|---|
|vkey|`number`|[https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes)|

Keyboard shortcuts defined in the main preferences are always executed first and are not passed to this callback.

## `on_key_up(vkey)`
|Arguments|||
|---|---|---|
|vkey|`number`|[https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes)|

## `on_library_items_added(handle_list)`
|Arguments|||
|---|---|---|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList/)|

## `on_library_items_changed(handle_list, fromhook)`
||Arguments|||
|----|---|---|---|
||handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList/)|
|:octicons-tag-24: 3.1.14, [foobar2000](https://foobar2000.org) `2.0 Beta 13`|fromhook|`boolean`|`true` if changes comes from `Playback Statistics` or other components that utilise the same DB functionality.

## `on_library_items_removed(handle_list)`
|Arguments|||
|---|---|---|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList/)|

## `on_load_image_done(image_path, image)`
|Arguments|||
|---|---|---|
|image_path|`string`|The path that was originally supplied to [utils.LoadImageAsync](../namespaces/utils/#utilsloadimageasyncwindow_id-path).|
|image|[IJSImage](../interfaces/IJSImage/)|Could be `null` on failure.|

Called when thread created by [utils.LoadImageAsync](../namespaces/utils/#utilsloadimageasyncwindow_id-path) is done.

## `on_locations_added(task_id, handle_list)`
|Arguments|||
|---|---|---|
|task_id|`number`|The return value from the original [fb.AddLocationsAsync](../namespaces/fb/#fbaddlocationsasyncwindow_id-paths) call.|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList/)|

Called when thread created by [fb.AddLocationsAsync](../namespaces/fb/#fbaddlocationsasyncwindow_id-paths) is done.

## `on_main_menu(index)`
:octicons-tag-24: 3.1.0

|Arguments|||
|---|---|---|
|index|`number`|

On the main menu `File>JScript Panel 3`, there are 10 menu items and
whichever number is selected is sent as the `index` to this callback.

Being main menu items now means you can bind them to global keyboard
shortcuts, standard toolbar buttons, panel stack splitter buttons,
etc.

Remember to think carefully about where you use this code as you
probably only want it to run once so don't include it in common files
and scripts where you might have multiple instances. Also, you should
avoid sharing scripts containing this code so as not to conflict with
what other users may already be using.

!!! example
	```js
	function on_main_menu(index) {
		switch (index) {
		case 1: // triggered when File>JScript Panel 3>1 is run
			do_something();
			break;
		case 2: // triggered when File>JScript Panel 3>2 is run
			do_something_else();
			break;
		}
	}
	```

## `on_metadb_changed(handle_list, fromhook)`
||Arguments|||
|---|---|---|---|
||handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList/)|
|:octicons-tag-24: 3.1.1|fromhook|`boolean`|`true` if changes comes from `Playback Statistics` or other components that utilise the same DB functionality.

Called when metadb contents change. This can be tag updates or database changes from `Playback Statistics` etc.

## `on_mouse_lbtn_dblclk(x, y, mask)`
## `on_mouse_lbtn_down(x, y, mask)`
## `on_mouse_lbtn_up(x, y, mask)`
## `on_mouse_leave()`
## `on_mouse_mbtn_dblclk(x, y, mask)`
## `on_mouse_mbtn_down(x, y, mask)`
## `on_mouse_mbtn_up(x, y, mask)`
## `on_mouse_move(x, y, mask)`
## `on_mouse_rbtn_dblclk(x, y, mask)`
## `on_mouse_rbtn_down(x, y, mask)`

## `on_mouse_rbtn_up(x, y, mask)`
You must return `true` if you want to suppress the default context menu. Use the ++shift+windows++ keys to bypass user code and open default context menu.

## `on_mouse_wheel(step)`
|Arguments|||
|---|---|---|
|step|`number`|

## `on_mouse_wheel_h(step)`
|Arguments|||
|---|---|---|
|step|`number`|

## `on_notify_data(name, info)`
|Arguments|||
|---|---|---|
|name|`string`|
|info|`string`, `number`, `array`, `object`|

Called in other panels after [window.NotifyOthers](../namespaces/window/#windownotifyothersname-info) is executed.

## `on_output_device_changed()`
Called when output device changes.

## `on_paint(gr)`
|Arguments|||
|---|---|---|
|gr|[IJSGraphics](../interfaces/IJSGraphics/)|

Called when window is ready to draw.

## `on_playback_follow_cursor_changed(state)`
|Arguments|||
|---|---|---|
|state|`boolean`|

Called when `Playback follow cursor` state is changed.

## `on_playback_dynamic_info()`
Called when dynamic info such as VBR bitrate changes.

## `on_playback_dynamic_info_track(type)`
|Arguments|||
|---|---|---|
|type|`number`|`0` stream metadata update, `1` stream album art update|

## `on_playback_edited(handle)`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](../interfaces/IMetadbHandle/)|

Called when currently playing file gets edited.

## `on_playback_new_track(handle)`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](../interfaces/IMetadbHandle/)|

## `on_playback_order_changed(new_order_index)`
|Arguments|||
|---|---|---|
|new_order_index|[PlaybackOrder](../flags/#playbackorder)|

Called when playback order is changed.

## `on_playback_pause(state)`
|Arguments|||
|---|---|---|
|state|`boolean`|

## `on_playback_queue_changed(origin)`
|Arguments|||
|---|---|---|
|origin|[PlaybackQueueOrigin](../flags/#playbackqueueorigin)|

## `on_playback_seek(time)`
|Arguments|||
|---|---|---|
|time|`number`|

## `on_playback_starting(cmd, is_paused)`
|Arguments|||
|---|---|---|
|cmd|[PlaybackStartingCMD](../flags/#playbackstartingcmd)
|is_paused|`boolean`|

## `on_playback_stop(reason)`
|Arguments|||
|---|---|---|
|reason|[PlaybackStopReason](../flags/#playbackstopreason)|

## `on_playback_time(time)`
|Arguments|||
|---|---|---|
|time|`number`|

Called every second for time display.

## `on_playlist_items_added(playlistIndex)`
## `on_playlist_items_removed(playlistIndex, new_count)`
## `on_playlist_items_reordered(playlistIndex)`

## `on_playlist_items_selection_change()`
Workaround for some 3rd party playlist viewers not working with [on_selection_changed](#on_selection_changed).

## `on_playlist_stop_after_current_changed(state)`
|Arguments|||
|---|---|---|
|state|`boolean`|

Called when `Stop after current` state is changed.

## `on_playlist_switch()`

## `on_playlists_changed()`
Called when

 * playlists are added/removed/reordered/renamed.
 * a playlist's lock status changes through the use of the built-in playlist lock methods or other components such as [foo_utils](https://foosion.foobar2000.org/components/?id=utils&version=0.6.2+beta+6) or [foo_playlist_attributes](https://www.foobar2000.org/components/view/foo_playlist_attributes).

## `on_replaygain_mode_changed(new_mode)`
|Arguments|||
|---|---|---|
|new_mode|[ReplaygainMode](../flags/#replaygainmode)|

## `on_run_cmd_async_done(task_id)`
:octicons-tag-24: 3.1.0

|Arguments|||
|---|---|---|
|task_id|`number`|The return value from the original [utils.RunCmdAsync](../namespaces/utils/#utilsruncmdasyncwindow_id-app-params) call.|

## `on_script_unload()`
Should always be called when:

 * scripts are reloaded from the context menu / window.Reload
 * the OK/Apply buttons are used in the Configure dialog.
 * panels are removed/replaced in layout editing mode
 * [foobar2000](https://foobar2000.org) exits normally

It will not be called if a script throws an error or [foobar2000](https://foobar2000.org) terminates abnormally.

!!! note
	You do not need to clear timers or deactivate tooltips here. The component handles this automatically.

## `on_selection_changed()`
Called when selection changes based on `File>Preferences>Display>Selection viewers`.

## `on_size()`
Called when panel is resized.

## `on_volume_change(volume)`
|Arguments|||
|---|---|---|
|volume|`number`|Floating point value in dB. Minimum is `-100`, maximum is `0`.|
