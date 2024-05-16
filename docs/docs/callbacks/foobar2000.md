## `on_always_on_top_changed(state)`
|Arguments|||
|---|---|---|
|state|`boolean`|

Called when `Always On Top` state is changed.

## `on_colours_changed()`
Called when colours are changed via `Default UI` / `Columns UI` preferences.

## `on_console_refresh`
!!! note
	Requires `foobar2000` `2.0`.

Called whenever new messages appear in the [foobar2000](https://www.foobar2000.org) `Console`.

## `on_cursor_follow_playback_changed(state)`
|Arguments|||
|---|---|---|
|state|`boolean`|

Called when `Cursor follow playback` state is changed.

## `on_dsp_preset_changed()`
Called when DSP preset changes but does not get called when presets are added or removed.

## `on_font_changed()`
Called when fonts are changed via `Default UI` / `Columns UI` preferences.

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
|handle|[IMetadbHandle](../interfaces/IMetadbHandle.md)|

Called when at least one minute of the track has been played or the track has reached its end after at least one third of it has been played.

## `on_library_initialised()`
Called when the `foobar2000` library is initialised on startup. Prior to `foobar2000` `2.0`, the library was always ready immediately but that is not the case now.

## `on_library_items_added(handle_list)`
|Arguments|||
|---|---|---|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList.md)|

## `on_library_items_changed(handle_list, fromhook)`
||Arguments|||
|----|---|---|---|
||handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList.md)|
|Requires `foobar2000` `2.0`.|fromhook|`boolean`|`true` if changes comes from `Playback Statistics` or other components that utilise the same DB functionality.

## `on_library_items_removed(handle_list)`
|Arguments|||
|---|---|---|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList.md)|

## `on_metadb_changed(handle_list, fromhook)`
|Arguments|||
|---|---|---|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList.md)|
|fromhook|`boolean`|`true` if changes comes from `Playback Statistics` or other components that utilise the same DB functionality.

Called when metadb contents change. This can be tag updates or database changes from `Playback Statistics` etc.

## `on_output_device_changed()`
Called when output device changes.

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
|handle|[IMetadbHandle](../interfaces/IMetadbHandle.md)|

Called when currently playing file gets edited.

## `on_playback_new_track(handle)`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](../interfaces/IMetadbHandle.md)|

## `on_playback_order_changed(new_order_index)`
|Arguments|||
|---|---|---|
|new_order_index|[PlaybackOrder](../flags.md#playbackorder)|

Called when playback order is changed.

## `on_playback_pause(state)`
|Arguments|||
|---|---|---|
|state|`boolean`|

## `on_playback_queue_changed(origin)`
|Arguments|||
|---|---|---|
|origin|[PlaybackQueueOrigin](../flags.md#playbackqueueorigin)|

## `on_playback_seek(time)`
|Arguments|||
|---|---|---|
|time|`number`|

## `on_playback_starting(cmd, is_paused)`
|Arguments|||
|---|---|---|
|cmd|[PlaybackStartingCMD](../flags.md#playbackstartingcmd)
|is_paused|`boolean`|

## `on_playback_stop(reason)`
|Arguments|||
|---|---|---|
|reason|[PlaybackStopReason](../flags.md#playbackstopreason)|

## `on_playback_time(time)`
|Arguments|||
|---|---|---|
|time|`number`|

Called every second while playing for time display.

## `on_playlist_item_ensure_visible(playlistIndex, playlistItemIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|
|playlistItemIndex|`number`|

Called when the status bar is double clicked while playing. Also called by the main menu `View/Show now playing in playlist`.

## `on_playlist_items_added(playlistIndex)`
## `on_playlist_items_changed(playlistIndex)`
## `on_playlist_items_removed(playlistIndex, new_count)`
## `on_playlist_items_reordered(playlistIndex)`
## `on_playlist_items_replaced(playlistIndex)`

## `on_playlist_items_selection_change()`
Called when playlist item selection changes.

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
|new_mode|[ReplaygainMode](../flags.md#replaygainmode)|

## `on_selection_changed()`
Called when selection changes based on `File>Preferences>Display>Selection viewers`.

## `on_volume_change(volume)`
|Arguments|||
|---|---|---|
|volume|`number`|Floating point value in dB. Minimum is `-100`, maximum is `0`.|
