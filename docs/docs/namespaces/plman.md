**Properties**

|||||
|---|---|---|---|
|plman.ActivePlaylist|`number`|read, write|Could be `-1` if reading value and no playlist is active.|
|plman.PlaybackOrder|[PlaybackOrder](../flags.md#playbackorder)|read, write|
|plman.PlayingPlaylist|`number`|read|Could be `-1` if not playing or playing item doesn't belong to any playlist.|
|plman.PlaylistCount|`number`|read|
|plman.RecyclerCount|`number`|read|

**Methods**

!!! note
	Most methods require that the `playlistIndex` argument is valid. That means
	not `-1` and less than `plman.PlaylistCount`.

## `plman.AddLocations(playlistIndex, paths[, select])`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid. Also, it must not be an autoplaylist or have a lock in place preventing the addition of new files.|
|paths|`array`|Can be file paths/urls/playlists.|
|select|`boolean`|Default `false`. If `true`, the active playlist will be set to the `playlistIndex`, the items will be selected and focus will be set to the first new item.|

No return value.

!!! note
	This operation is asynchronous and may take some time to complete if it's a large array.

!!! example
	```js
	var arr = ["e:\\1.mp3"];
	plman.AddLocations(plman.ActivePlaylist, arr);
	```

## `plman.AddPlaylistLock(playlistIndex, mask)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|mask|[PlaylistLockFilterMask](../flags.md#playlistlockfiltermask)|

Returns `true` on success, `false` if playlist already locked.

See [plman.ShowPlaylistLockUI](#plmanshowplaylistlockuiplaylistindex) first as that provides
a dialog and is much more user friendly!

!!! note
	Before you can add a playlist lock, you must check
	there is no lock present already. If another component
	owns the lock, you have to use that component to
	remove it. If the lock is owned by `JScript Panel 3` then
	you must remove it first. This is because locks cannot be
	edited. You have to remove it and then add a new one
	with a new mask value.

!!! example
	```js
	function add_playlist_lock(playlistIndex, mask) {
		// check if playlistIndex is valid
		if (playlistIndex >= 0 && playlistIndex < plman.PlaylistCount) {
			if (plman.IsPlaylistLocked(playlistIndex)) {
				if (plman.GetPlaylistLockName(playlistIndex) == 'JScript Panel 3') {
					// We own this lock so we can remove it.
					plman.RemovePlaylistLock(playlistIndex);
				} else {
					// Locked but not ours. Nothing we can do.
					return false;
				}
			}

			return plman.AddPlaylistLock(playlistIndex, mask);
		}
		return false;
	}

	// Available mask values
	var PlaylistLockFilterMask = {
		filter_add : 1,
		filter_remove : 2,
		filter_reorder : 4,
		filter_replace : 8,
		filter_rename : 16,
		filter_remove_playlist : 32,
	};

	// Setting a single value:
	var mask = PlaylistLockFilterMask.filter_add;

	// To set multiple values at once, use | like this:
	var mask2 = PlaylistLockFilterMask.filter_add | PlaylistLockFilterMask.filter_remove;

	// You may add a value to an existing mask using a bitwise operator like this:
	mask |= PlaylistLockFilterMask.filter_replace;

	//To remove a value, use &= and ~ like this:
	mask &= ~PlaylistLockFilterMask.filter_replace;
	```

## `plman.ClearPlaylist(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

No return value.

## `plman.ClearPlaylistSelection(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

No return value.

## `plman.CreateAutoPlaylist(playlistIndex, name, query[, sort, flags])`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|
|name|`string`|
|query|`string`|
|flags|`number`|Default `0`. Use `1` to force sort.

Returns the index of the newly created `Autoplaylist`
or `-1` on failure. The most likely cause of that
would be an invalid query.

## `plman.CreatePlaylist([playlistIndex, name])`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Optional|
|name|`string`|Optional|

Returns the index of the newly created playlist.

!!! example
	```js
	/*
	Creates a new playlist last in the list and it
	will be named `New playlist` or have numbers appended if
	there are existing playlists with the same name. Using
	the return value, you can switch to it.
	*/

	var new_index = plman.CreatePlaylist();
	plman.ActivePlaylist = new_index;
	```

## `plman.DuplicatePlaylist(playlistIndex, name)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|name|`string`|If you supply an empty string, the name of the original playlist is used.|

Returns the index of the newly created playlist
which will be directly after the original. Only the content
is duplicated, not the properties.

## `plman.ExecutePlaylistDefaultAction(playlistIndex, playlistItemIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|playlistItemIndex|`number`|Must be valid.|

No return value.

Starts playback by executing the default doubleclick action unless
overridden by a lock to do something else.

## `plman.FindByGUID(str)`
!!! note
	Requires `foobar2000` `2.0`.

|Arguments|||
|---|---|---|
|str|`string`|

Returns the index or `-1` on failure. Only strings returned by `plman.GetGUID` would be valid.

## `plman.FindOrCreatePlaylist(name, unlocked)`
|Arguments|||
|---|---|---|
|name|`string`|
|unlocked|`boolean`|If `true`, locked playlists are ignored when looking for existing playlists.

Returns index of named playlist or newly created playlist.

## `plman.FindPlaylist(name)`
|Arguments|||
|---|---|---|
|name|`string`|Not case senstive.|

Returns the found index or `-1` on failure.

## `plman.GetGUID(playlistIndex)`
!!! note
	Requires `foobar2000` `2.0`.

|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

Returns a `string` which is a unique persistent property of the playlist.

## `plman.GetPlaybackOrders()`
Returns a `VBArray` so you need to use `.toArray()` on the result.

This is an array of playback order names which can be iterated
or used with `plman.PlaybackOrder`.

!!! example
	=== "Current"
		```js
		console.log(plman.GetPlaybackOrders().toArray()[plman.PlaybackOrder]);
		```

	=== "Loop"
		```js
		var arr = plman.GetPlaybackOrders().toArray();
		for (var i = 0; i < arr.length; i++) {
			console.log(arr[i]);
		}
		```

## `plman.GetPlayingItemLocation()`
Returns an [IPlayingItemLocation](../interfaces/IPlayingItemLocation.md) instance.

## `plman.GetPlaylistFocusItemIndex(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns index or `-1` if nothing is selected.

## `plman.GetPlaylistItemCount(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns a `number`.

## `plman.GetPlaylistItems(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns an [IMetadbHandleList](../interfaces/IMetadbHandleList.md) instance.

## `plman.GetPlaylistLockFilterMask(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns a [PlaylistLockFilterMask](../flags.md#playlistlockfiltermask) or
`-1` if supplied with an invalid `playlistIndex`.

Use this to determine the type(s) of locks applied to the specified playlist.

!!! example
	```js
	var PlaylistLockFilterMask = {
		filter_add : 1,
		filter_remove : 2,
		filter_reorder : 4,
		filter_replace : 8,
		filter_rename : 16,
		filter_remove_playlist : 32,
	};

	var mask = plman.GetPlaylistLockFilterMask(plman.ActivePlaylist)
	if (mask & PlaylistLockFilterMask.filter_add) {
		console.log("Can't add files to this playlist");
	}
	```

For convenience, these methods are included in `helpers.txt`.

```js
function playlist_can_add_items(playlistIndex) {
	return !(plman.GetPlaylistLockFilterMask(playlistIndex) & PlaylistLockFilterMask.filter_add);
}

function playlist_can_remove_items(playlistIndex) {
	return !(plman.GetPlaylistLockFilterMask(playlistIndex) & PlaylistLockFilterMask.filter_remove);
}

function playlist_can_reorder(playlistIndex) {
	return !(plman.GetPlaylistLockFilterMask(playlistIndex) & PlaylistLockFilterMask.filter_reorder);
}

function playlist_can_replace_items(playlistIndex) {
	return !(plman.GetPlaylistLockFilterMask(playlistIndex) & PlaylistLockFilterMask.filter_replace);
}

function playlist_can_rename(playlistIndex) {
	return !(plman.GetPlaylistLockFilterMask(playlistIndex) & PlaylistLockFilterMask.filter_rename);
}

function playlist_can_remove(playlistIndex) {
	return !(plman.GetPlaylistLockFilterMask(playlistIndex) & PlaylistLockFilterMask.filter_remove_playlist);
}
```

## `plman.GetPlaylistLockName(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns the name of the component that implemented
the playlist lock or an empty string if the playlist
is not locked.

## `plman.GetPlaylistName(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns a `string`.

## `plman.GetPlaylistSelectedIndexes(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

Returns a `VBArray` so you need to use `.toArray()` on the result.

## `plman.GetPlaylistSelectedItems(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns an [IMetadbHandleList](../interfaces/IMetadbHandleList.md) instance.

## `plman.GetQueryItems(playlistIndex, query)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|query|`string`|

Returns an [IMetadbHandleList](../interfaces/IMetadbHandleList.md) instance.

!!! note
	Errors will be thrown on invalid queries so if you're not
	using predefined safe queries and are accepting user
	input, you should use this inside a try/catch statement.
	An empty handle list will be returned if the query is valid but there are no results.

## `plman.GetRecyclerItems(index)`
|Arguments|||
|---|---|---|
|index|`number`|Must be valid.|

Returns an [IMetadbHandleList](../interfaces/IMetadbHandleList.md) instance.

!!! example
	```js
	var count = plman.RecyclerCount;
	if (count > 0) {
		// retrieve handles from first deleted playlist
		var handle_list = plman.GetRecyclerItems(0);
	}
	```

## `plman.GetRecyclerName(index)`
|Arguments|||
|---|---|---|
|index|`number`|Must be valid.|

!!! example
	```js
	var count = plman.RecyclerCount;
	if (count > 0) {
		// output name of first deleted playlist
		console.log(plman.GetRecyclerName(0));
	}
	```

## `plman.InsertPlaylistItems(playlistIndex, base, handle_list[, select])`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|base|`number`|Position in playlist.|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList.md)|
|select|`boolean`|Default `false`.

No return value.

## `plman.InsertPlaylistItemsFilter(playlistIndex, base, handle_list[, select])`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|base|`number`|Position in playlist.|
|handle_list|[IMetadbHandleList](../interfaces/IMetadbHandleList.md)|
|select|`boolean`|Default `false`.

No return value.

Same as above except any duplicates contained in `handle_list` are removed.

## `plman.InvertSelection(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

No return value.

## `plman.IsAutoPlaylist(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns a `boolean` value.

## `plman.IsPlaylistItemSelected(playlistIndex, playlistItemIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|
|playlistItemIndex|`number`|

Returns a `boolean` value.

## `plman.IsPlaylistLocked(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|

Returns a `boolean` value.

!!! note
	It's advisable to use [plman.GetPlaylistLockFilterMask](#plmangetplaylistlockfiltermaskplaylistindex)
	as this will let you determine what kind of locks
	are in place. For example, if a playlist only has a
	lock preventing you from deleting it, you can still
	add/remove files which you wouldn't be able determine
	from using `plman.IsPlaylistLocked` alone.

## `plman.MovePlaylist(from, to)`
|Arguments|||
|---|---|---|
|from|`number`|Must be valid.|
|to|`number`|Must be valid and not equal to `from`.|

No return value.

## `plman.MovePlaylistSelection(playlistIndex, delta)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|delta|`number`|

No return value.

!!! note
	Only useful when the selection is contiguous. See the improved version just below.

## `plman.MovePlaylistSelectionV2(playlistIndex, new_pos)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|new_pos|`number`|

No return value.

Unlike `plman.MovePlaylistSelection`, this has
full support for non-contiguous selections and
all you have to do is supply the new position index.

## `plman.RecyclerPurge(affectedItems)`
|Arguments|||
|---|---|---|
|affectedItems|`array`|

No return value.

Purges deleted playlists so they cannot be restored.

!!! example
	```js
	// first only
	plman.RecyclerPurge([0]);

	// first and third only
	plman.RecyclerPurge([0,2]);

	// purges all deleted playlists
	var arr = [];
	var count = plman.RecyclerCount;
	for (var i = 0; i < count; i++) {
		arr.push(i);
	}
	plman.RecyclerPurge(arr);
	```

## `plman.RecyclerRestore(index)`
|Arguments|||
|---|---|---|
|index|`number`|Must be valid.|

No return value.

!!! example
	```js
	var count = plman.RecyclerCount;
	if (count > 0) {
		// restore first deleted playlist
		plman.RecyclerRestore(0);
	}
	```

## `plman.RemovePlaylist(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

No return value.

!!! note
	If removing the active playlist, no playlist
	will be active after using this. You'll need to
	set it manually or use [plman.RemovePlaylistSwitch](#plmanremoveplaylistswitchplaylistindex)
	instead.

## `plman.RemovePlaylistLock(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

Returns a `boolean` value.

!!! note
	You can only remove a playlist lock if it's
	owned by `JScript Panel 3`. You can check
	this with [plman.GetPlaylistLockName](#plmangetplaylistlocknameplaylistindex). See
	[plman.AddPlaylistLock](#plmanaddplaylistlockplaylistindex-mask) for an example.

## `plman.RemovePlaylists(playlistIndexes)`
|Arguments|||
|---|---|---|
|playlistIndexes|`array`|

No return value.

!!! example
	```js
	// This would remove all empty playlists.
	var arr = [];
	for (var i = 0; i < plman.PlaylistCount; i++) {
		if (plman.GetPlaylistItemCount(i) == 0) arr.push(i);
	}
	if (arr.length) plman.RemovePlaylists(arr);
	```

## `plman.RemovePlaylistSelection(playlistIndex[, crop])`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|crop|`boolean`|Default `false`.|

No return value.

!!! example
	```js
	// Removes selected items from playlist.
	plman.RemovePlaylistSelection(plman.ActivePlaylist);

	// Removes items that are NOT selected.
	plman.RemovePlaylistSelection(plman.ActivePlaylist, true);
	```

## `plman.RemovePlaylistSwitch(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

No return value.

This automatically sets another playlist as
active if removing the active playlist.

## `plman.RenamePlaylist(playlistIndex, name)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|name|`string`|

No return value.

## `plman.ReplacePlaylistItem(playlistIndex, playlistItemIndex, handle)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|playlistItemIndex|`number`|Must be valid.|
|handle|[IMetadbHandle](../interfaces/IMetadbHandle.md)|

No return value.

## `plman.SelectQueryItems(playlistIndex, query)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|query|`string`|

This selects playlist items in a similar manner to
the `foobar2000` native playlist search.

Returns a `VBArray` so you need to use `.toArray()` on the result.

## `plman.SetActivePlaylistContext()`
No return value.

Workaround so you can use the `Edit` menu
when your panel has focus and a dedicated
playlist viewer doesn't.

!!! example
	```js
	// Once on startup.
	plman.SetActivePlaylistContext();

	function on_focus(is_focused) {
		if (is_focused) {
			// When the panel gets focus but not on every click.
			plman.SetActivePlaylistContext();
		}
	}
	```

## `plman.SetPlaylistFocusItem(playlistIndex, playlistItemIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|playlistItemIndex|`number`|Must be valid.|

No return value.

## `plman.SetPlaylistSelection(playlistIndex, affectedItems, state)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|affectedItems|`array`|
|state|`boolean`|

No return value.

!!! example
	```js
	// Selects first, third and fifth tracks in playlist.
	// This does not affect other selected items.

	var arr = [0, 2, 4];
	plman.SetPlaylistSelection(plman.ActivePlaylist, arr, true);
	```

## `plman.SetPlaylistSelectionSingle(playlistIndex, playlistItemIndex, state)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|playlistItemIndex|`number`|Must be valid.|
|state|`boolean`|

No return value.

!!! example
	```js
	// Deselects first playlist item.
	// Only works when it is already selected!

	plman.SetPlaylistSelectionSingle(plman.ActivePlaylist, 0, false);
	```

!!! example
	```js
	// Selects last item in playlist.
	// This does not affect other selected items.

	var ap = plman.ActivePlaylist;
	var count = plman.GetPlaylistItemCount(ap);
	plman.SetPlaylistSelectionSingle(ap, count - 1, true);
	```

## `plman.ShowAutoPlaylistUI(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

No return value.

## `plman.ShowPlaylistLockUI(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

Shows popup window letting you toggle the
various lock options on/off.

No return value.

## `plman.SortByFormat(playlistIndex, pattern[, selected_items_only])`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|pattern|`string`|Title formatting pattern to sort by. Use "" to randomise the order.
|selected_items_only|`boolean`|Default `false`.|

No return value.

## `plman.SortByFormatV2(playlistIndex, pattern[, direction])`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|
|pattern|`string`|Title formatting pattern to sort by.
|direction|`number`|Default `1`. Use `1` for ascending, `-1` for descending.|

No return value.

## `plman.SortPlaylistsByName([direction])`
|Arguments|||
|---|---|---|
|direction|`number`|Default `1`. Use `1` for ascending, `-1` for descending.|

No return value.

## `plman.UndoBackup(playlistIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|Must be valid.|

No return value.

Call before using other `plman` methods that
add/remove/reorder playlist items so a history
will be available from the `Edit` menu.
