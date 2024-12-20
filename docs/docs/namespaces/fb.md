**Properties**

|||||
|---|---|---|---|
|fb.AlwaysOnTop|`boolean`|read, write|
|fb.ComponentPath|`string`|read|
|fb.CursorFollowPlayback|`boolean`|read, write|
|fb.CustomVolume|`number`|read|See note below.
|fb.FoobarPath|`string`|read|
|fb.IsPaused|`boolean`|read|
|fb.IsPlaying|`boolean`|read|
|fb.PlaybackFollowCursor|`boolean`|read, write|
|fb.PlaybackLength|`number`|read|
|fb.PlaybackTime|`number`|read, write|
|fb.ProfilePath|`string`|read|
|fb.ReplaygainMode|[ReplaygainMode](../flags.md#replaygainmode)|read, write|
|fb.StopAfterCurrent|`boolean`|read, write|
|fb.VersionString|`string`|read|
|fb.Volume|`number`|read, write|See note below.

!!! example
	```js
	fb.AlwaysOnTop = !fb.AlwaysOnTop; // toggles the current value
	console.log(fb.FoobarPath); // Z:\foobar2000\
	fb.PlaybackTime = 60; // jump to the one minute mark
	```

!!! note "Custom Volume"
	`fb.CustomVolume` can be used for displaying the volume from `UPnP` devices. It will return
	a value of `-1` when using a normal device and that also indicates that `fb.Volume` is writable.
	When a custom volume control is active, you can not use `fb.Volume` and must use `fb.VolumeUp()` / `fb.VolumeDown()` / `fb.VolumeMute()`.

**Methods**

## Shortcuts to main menu commands

||
|---|
|fb.AddDirectory()|
|fb.AddFiles()|
|fb.Exit()|
|fb.LoadPlaylist()|
|fb.Next()|
|fb.Pause()|
|fb.Play()|
|fb.PlayOrPause()|
|fb.Prev()|
|fb.Random()|
|fb.SavePlaylist()|
|fb.ShowConsole()|
|fb.ShowPreferences()|
|fb.Stop()|
|fb.VolumeDown()|
|fb.VolumeMute()|
|fb.VolumeUp()|

The above methods have no return value.

## `fb.AddLocationsAsync(window_id, paths)`
|Arguments|||
|---|---|---|
|window_id|[window.ID](window.md)|
|paths|`array`|An array of strings which could be files, urls, playlists.|

Returns a unique `task_id`.

Similar to [plman.AddLocations](plman.md#plmanaddlocationsplaylistindex-paths-select) except rather than specifiying a target playlist, you get a handle list generated
from the supplied paths/urls which are sent to a new [on_locations_added](../callbacks/component.md#on_locations_addedtask_id-handle_list) callback.

!!! example
	```js
	var files = ["z:\\1.mp3", "z:\\2.flac"];

	function on_mouse_lbtn_dblclk() {
		var task_id = fb.AddLocationsAsync(window.ID, files);
		console.log("got task_id", task_id);
	}

	function on_locations_added(task_id, handle_list) {
		console.log("callback task_id", task_id);
		console.log(handle_list.Count);
	}
	```

## `fb.CheckClipboardContents()`
Returns a `boolean` value.

Checks clipboard contents are handles or a file selection
from `Windows Explorer`. Use in conjunction	with
[fb.GetClipboardContents](#fbgetclipboardcontents).

## `fb.CheckComponent(name)`
|Arguments|||
|---|---|---|
|name|`string`|

Returns a `boolean` value.

Use this if your script depends on other components.

!!! example
	```js
	if (!fb.CheckComponent("foo_playcount")) {
		utils.ShowPopupMessage("This script requires foo_playcount.", "Rating");
	}
	```

## `fb.ClearPlaylist()`
No return value.

Clears active playlist. If you wish to clear a specific playlist, use [plman.ClearPlaylist](plman.md#plmanclearplaylistplaylistindex).

## `fb.CreateContextMenuManager()`
Returns an [IContextMenuManager](../interfaces/IContextMenuManager.md) instance.

## `fb.CreateHandleList([handle])`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](../interfaces/IMetadbHandle.md), optional|

Returns an [IMetadbHandleList](../interfaces/IMetadbHandleList.md) instance.

!!! example
	```js
	var handle = fb.GetFocusItem();
	var handle_list = fb.CreateHandleList(handle);
	var image_path = ...
	handle_list.AttachImage(image_path, 0);
	handle_list.Dispose();
	```

## `fb.CreateMainMenuManager(root_name)`
|Arguments|||
|---|---|---|
|root_name|`string`|Must be one of `File`, `Edit`, `View`, `Playback`, `Library`, `Help`.

Returns an [IMainMenuManager](../interfaces/IMainMenuManager.md) instance.

## `fb.EnableAdvancedLogging()`
:octicons-tag-24: 3.6.1

No return value.

Only enable this if you're having problems diagnosing your own script errors. The setting persists
until `foobar2000` is closed. To disable this advanced logging, remove this method and restart
`foobar2000`.

Console messages will point directly at the `C++` source code and this is something that you can
ask about in the [main support thread](https://hydrogenaud.io/index.php/topic,110499.0.html).

## `fb.EnumerateMainMenuCommands()`
:octicons-tag-24: 3.8.2

Returns a `JSON` array in string form so you need to use `JSON.parse` on the result.

Every item of the array has the following properties:
```
Checked // boolean
Disabled // boolean
FullPath // string, the same full path you'd supply to fb.RunMainMenuCommand
HiddenByDefault // boolean
Radio // boolean
Type // string "Fixed" or "Dynamic"
Visible // boolean
```

!!! example

	```js
	var menu_commands = JSON.parse(fb.EnumerateMainMenuCommands());

	// list all checked commands in the Console
	menu_commands.filter(function (command) {
		return command.Checked;
	}).forEach(function (command) {
		console.log(command.FullPath);
	});
	```

## `fb.GetActiveDSPs()`
:octicons-tag-24: 3.8.1

Returns a `VBArray` so you need to use `.toArray()` on the result.

## `fb.GetAlbumArtStub([art_id])`
|Arguments|||
|---|---|---|
|art_id|[AlbumArtId](../flags.md#albumartid)|Default `0`.|

Returns an [IJSImage](../interfaces/IJSImage.md) instance or `null` on failure.

## `fb.GetAudioChunk(requested_length[, offset])`
:octicons-tag-24: 3.6.6

|Arguments|||
|---|---|---|
|requested_length|`number`|seconds|
|offset|`number`|Default `0`|

Returns an [IAudioChunk](../interfaces/IAudioChunk.md) instance or `null` on failure.

The source code is basically this:

```cpp
STDMETHODIMP Fb::GetAudioChunk(double requested_length, double offset, IAudioChunk** out)
{
	RETURN_HR_IF_NULL(E_POINTER, out);

	// return value will be null in JavaScript if the code below fails
	*out = nullptr;

	if (m_vis.is_valid())
	{
		double time{};
		if (m_vis->get_absolute_time(time))
		{
			audio_chunk_impl chunk;
			if (m_vis->get_chunk_absolute(chunk, time + offset, requested_length))
			{
				// success, return value will be a valid audio chunk
				*out = new ComObject<AudioChunk>(chunk);
			}
		}
	}

	return S_OK;
}
```

`get_absolute_time` and `get_chunk_absolute` and their arguments are described here:

[https://github.com/marc2k3/foobar2000-sdk/blob/main/foobar2000/SDK/vis.h](https://github.com/marc2k3/foobar2000-sdk/blob/main/foobar2000/SDK/vis.h)


## `fb.GetClipboardContents()`
Returns an [IMetadbHandleList](../interfaces/IMetadbHandleList.md) instance.

Clipboard contents can be handles copied to the clipboard in
other components, a file selection from Explorer, etc.

!!! example
	```js
	// ==PREPROCESSOR==
	// @import "%fb2k_component_path%helpers.txt"
	// ==/PREPROCESSOR==

	function on_mouse_rbtn_up(x, y) {
		var ap = plman.ActivePlaylist;

		// playlist_can_add_items is defined in helpers.txt, it uses
		// plman.GetPlaylistLockFilterMask to determine if the active playlist
		// permits adding items
		// MF_STRING and MF_GRAYED are also defined there.

		var can_paste_flag = playlist_can_add_items(ap) && fb.CheckClipboardContents() ? MF_STRING : MF_GRAYED;

		var menu = window.CreatePopupMenu();
		menu.AppendMenuItem(can_paste_flag, 1, "Paste");

		var idx = menu.TrackPopupMenu(x, y);
		menu.Dispose();

		if (idx == 1) {
			var handle_list = fb.GetClipboardContents();
			plman.InsertPlaylistItems(ap, plman.GetPlaylistItemCount(ap), handle_list);
			handle_list.Dispose();
		}

		return true;
	}
	```

## `fb.GetDSPPresets()`
Returns a `JSON` array in string form so you need to use `JSON.parse` on the result.

!!! example
	```js
	var str = fb.GetDSPPresets();
	console.log(str);
	```

	``` markdown title="Example output"
	[
		{
			"active": true,
			"name": "two"
		},
		{
			"active": false,
			"name": "three"
		}
	]
	```

	```js
	var arr = JSON.parse(str);
	console.log(arr.length); // number of presets

	for (var i = 0; i < arr.length; i++) {
		if (arr[i].active) {
			// this is the active preset, do something with the name??
		}
	}
	```

## `fb.GetFocusItem()`
Returns an [IMetadbHandle](../interfaces/IMetadbHandle.md) instance.

Handle of the currently selected active playlist item or `null` on failure.

## `fb.GetLibraryItems([query])`
|Arguments|||
|---|---|---|
|query|`string`|Optional. If omitted or invalid, all items will be returned.|

Returns an [IMetadbHandleList](../interfaces/IMetadbHandleList.md) instance.

## `fb.GetNowPlaying()`
Returns an [IMetadbHandle](../interfaces/IMetadbHandle.md) instance.
Now playing item or `null` if [foobar2000](https://www.foobar2000.org) isn't playing.

## `fb.GetOutputDevices()`
Returns a `JSON` array in string form so you need to use `JSON.parse` on the result.

!!! example
	```js
	var str = fb.GetOutputDevices();
	console.log(str);
	```

	``` markdown title="Example output"
	[
		{
			"active": false,
			"device_id": "{5243F9AD-C84F-4723-8194-0788FC021BCC}",
			"name": "Null Output",
			"output_id": "{EEEB07DE-C2C8-44C2-985C-C85856D96DA1}"
		},
		{
			"active": true,
			"device_id": "{00000000-0000-0000-0000-000000000000}",
			"name": "Primary Sound Driver",
			"output_id": "{D41D2423-FBB0-4635-B233-7054F79814AB}"
		},
		{
			"active": false,
			"device_id": "{1C4EC038-97DB-48E7-9C9A-05FDED46847B}",
			"name": "Speakers (Sound Blaster Z)",
			"output_id": "{D41D2423-FBB0-4635-B233-7054F79814AB}"
		},
		{
			"active": false,
			"device_id": "{41B86272-3D6C-4A5A-8907-4FE7EBE39E7E}",
			"name": "SPDIF-Out (Sound Blaster Z)",
			"output_id": "{D41D2423-FBB0-4635-B233-7054F79814AB}"
		},
		{
			"active": false,
			"device_id": "{9CDC0FAE-2870-4AFA-8287-E86099D69076}",
			"name": "3 - BenQ BL3200 (AMD High Definition Audio Device)",
			"output_id": "{D41D2423-FBB0-4635-B233-7054F79814AB}"
		}
	]
	```

	```js
	var arr = JSON.parse(str);
	console.log(arr.length); // number of devices
	```

As you can see, only one of the items in the array has `active`
set to `true` so that is the device you'd want to display the name of
or mark as selected in a menu.

To change device you can use [fb.RunMainMenuCommand](#fbrunmainmenucommandcommand) with the
device name or use [fb.SetOutputDevice](#fbsetoutputdeviceoutput_id-device_id) with the
`device_id`/`output_id`.

!!! example
	=== "RunMainMenuCommand"
		```js
		var str = fb.GetOutputDevices();
		var arr = JSON.parse(str);
		// Assuming same list from above, switch output to the last device.
		fb.RunMainMenuCommand("Playback/Device/" + arr[4].name);
		```

	=== "SetOutputDevice"
		```js
		var str = fb.GetOutputDevices();
		var arr = JSON.parse(str);
		// Assuming same list from above, switch output to the last device.
		fb.SetOutputDevice(arr[4].output_id, arr[4].device_id);
		```

## `fb.GetSelection([flags])`
|Arguments|||
|---|---|---|
|flags|`number`|Default `0`, `1` no now playing|

Returns an [IMetadbHandleList](../interfaces/IMetadbHandleList.md) instance.

## `fb.GetSelectionType()`

Returns a [SelectionType](../flags.md#selectiontype)

## `fb.IsLibraryEnabled()`
Returns a `boolean` value.

## `fb.IsLibraryInitialised()`
:octicons-tag-24: 3.5.1

Returns a `boolean` value.

## `fb.RunContextCommand(command)`
|Arguments|||
|---|---|---|
|command|`string`|The full path to the command must be supplied. Case is not important.|

Returns `true` if a matching command was found, `false` otherwise.

!!! note
	This method is for the currently playing file only. See also: [IMetadbHandleList RunContextCommand](../interfaces/IMetadbHandleList.md#runcontextcommandcommand).

## `fb.RunMainMenuCommand(command)`
|Arguments|||
|---|---|---|
|command|`string`|The full path to the command must be supplied. Case is not important.|

Returns `true` if a matching command was found, `false` otherwise.

## `fb.SetDSPPreset(idx)`
|Arguments|||
|---|---|---|
|idx|`number`|

No return value. See [fb.GetDSPPresets](#fbgetdsppresets).

## `fb.SetOutputDevice(output_id, device_id)`
|Arguments|||
|---|---|---|
|output_id|`string`|
|device_id|`string`|

No return value. See [fb.GetOutputDevices](#fbgetoutputdevices).

## `fb.ShowLibrarySearchUI(query)`
|Arguments|||
|---|---|---|
|query|`string`|

No return value.

Opens the `Library>Search` window populated with the query you set.

## `fb.ShowPictureViewer(path)`
|Arguments|||
|---|---|---|
|path|`string`|

No return value.

## `fb.TitleFormat(pattern)`
|Arguments|||
|---|---|---|
|pattern|`string`|

Returns an [ITitleFormat](../interfaces/ITitleFormat.md) instance.
