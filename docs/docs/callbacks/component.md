## `on_download_file_done(path, success, error_text)`
|Arguments|||
|---|---|---|
|path|`string`|The path that was originally supplied to [utils.DownloadFileAsync](../namespaces/utils.md#utilsdownloadfileasyncwindow_id-url-path-verify_image).|
|success|`boolean`|If `true` it means the web request was succesful and the file was saved correctly.|
|error_text|`string`|Empty if success is `true`. If success is `false`, it should describe what went wrong.|

Called when thread created by [utils.DownloadFileAsync](../namespaces/utils.md#utilsdownloadfileasyncwindow_id-url-path-verify_image) is done.

## `on_download_image_done(url, image)`
|Arguments|||
|---|---|---|
|url|`string`|The url that was originally supplied to [utils.DownloadImageAsync](../namespaces/utils.md#utilsdownloadimageasyncwindow_id-url).|
|image|[IJSImage](../interfaces/IJSImage.md)|Could be `null` on failure.|

Called when thread created by [utils.DownloadImageAsync](../namespaces/utils.md#utilsdownloadimageasyncwindow_id-url) is done.

## `on_get_album_art_done(handle, art_id, image)`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](../interfaces/IMetadbHandle.md)|
|art_id|`number`|
|image|[IJSImage](../interfaces/IJSImage.md)|Could be `null` on failure.|

Called when thread created by [IMetadbHandle GetAlbumArtAsync](../interfaces/IMetadbHandle.md#getalbumartasyncwindow_id-art_id) or [IMetadbHandle GetAlbumArtThumbAsync](../interfaces/IMetadbHandle.md#getalbumartthumbasyncwindow_id-art_id-max_size) is done.

## `on_http_request_done(task_id, success, response_text, status, response_headers)`
|Arguments|||
|---|---|---|
|task_id|`number`|The return value from the original [utils.HTTPRequestAsync](../namespaces/utils.md#utilshttprequestasyncwindow_id-type-url-user_agent_or_headers-post_data) call.|
|success|`boolean`|If `true`, it doesn't necessarily mean `HTTP` status `200` but it indicates the request was completed succesfully so the response text is from the server.|
|response_text|`string`|
|status|`number`|Will be `0` if `success` is `false` otherwise it will the `HTTP` status code from the server.|
|response_headers|`string`|This is a stringified `JSON` object so you need to use `JSON.parse` to access it. It's only valid if `success` was `true`.|

Called when thread created by [utils.HTTPRequestAsync](../namespaces/utils.md#utilshttprequestasyncwindow_id-type-url-user_agent_or_headers-post_data) is done.

See [Web Requests](../guides/web-requests.md) for examples.

## `on_load_image_done(image_path, image)`
|Arguments|||
|---|---|---|
|image_path|`string`|The path that was originally supplied to [utils.LoadImageAsync](../namespaces/utils.md#utilsloadimageasyncwindow_id-path).|
|image|[IJSImage](../interfaces/IJSImage.md)|Could be `null` on failure.|

Called when thread created by [utils.LoadImageAsync](../namespaces/utils.md#utilsloadimageasyncwindow_id-path) is done.

## `on_locations_added(task_id, handle_list)`
|Arguments|||
|---|---|---|
|task_id|`number`|The return value from the original [fb.AddLocationsAsync](../namespaces/fb.md#fbaddlocationsasyncwindow_id-paths) call.|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList.md)|

Called when thread created by [fb.AddLocationsAsync](../namespaces/fb.md#fbaddlocationsasyncwindow_id-paths) is done.

## `on_main_menu(index)`
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

## `on_notify_data(name, info)`
|Arguments|||
|---|---|---|
|name|`string`|
|info|`string`, `number`, `array`, `object`|

Called in other panels after [window.NotifyOthers](../namespaces/window.md#windownotifyothersname-info) is executed.

## `on_run_cmd_async_done(task_id)`
|Arguments|||
|---|---|---|
|task_id|`number`|The return value from the original [utils.RunCmdAsync](../namespaces/utils.md#utilsruncmdasyncwindow_id-app-params) call.|

## `on_script_unload()`
Should always be called when:

 * scripts are reloaded from the context menu / `window.Reload`
 * the OK/Apply buttons are used in the [Configuration Window](../configuration-window.md).
 * panels are removed/replaced in layout editing mode
 * [foobar2000](https://www.foobar2000.org) exits normally

It will not be called if a script throws an error or [foobar2000](https://www.foobar2000.org) terminates abnormally.

!!! note
	You do not need to clear timers or deactivate tooltips here. The component handles this automatically.

!!! note
	Do not try to use `window.SetProperty` here. When shutting down, the layout data which stores persistent
	properties has already been written to file and changes will not be saved.
