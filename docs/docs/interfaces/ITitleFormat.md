This will be used in the examples below:

```js
var tfo = fb.TitleFormat("%artist%");
```

**Methods**

## `Dispose()`

No return value.

## `Eval()`

Returns a `string`. It will be empty if [foobar2000](https://www.foobar2000.org) is not playing.

## `EvalActivePlaylistItem(playlistItemIndex)`
|Arguments|||
|---|---|---|
|playlistItemIndex|`number`|

Returns a `string`.

Use if you want access to playlist specific fields such as `%list_index%`, `%list_total%`, `%isplaying%` etc.
Full details [here](https://wiki.hydrogenaud.io/index.php?title=Foobar2000:Title_Formatting_Reference#Playlist-only_fields).

## `EvalPlaylistItem(playlistIndex, playlistItemIndex)`
|Arguments|||
|---|---|---|
|playlistIndex|`number`|
|playlistItemIndex|`number`|

Returns a `string`.

Use if you want access to playlist specific fields such as `%list_index%`, `%list_total%`, `%isplaying%` etc.
Full details [here](https://wiki.hydrogenaud.io/index.php?title=Foobar2000:Title_Formatting_Reference#Playlist-only_fields).

## `EvalWithMetadb(handle)`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](IMetadbHandle.md)|

Returns a `string`.

!!! example
	```js
	var artist = tfo.EvalWithMetadb(fb.GetFocusItem());
	```

!!! note
	You should try and avoid using this method inside a loop. It's preferable
	to use the `EvalWithMetadbs` method just below.

## `EvalWithMetadbs(handle_list)`
|Arguments|||
|---|---|---|
|handle_list|[IMetadbHandleList](IMetadbHandleList.md)|

Returns a `VBArray` so you need to use `.toArray()` on the result.

!!! example
	```js
	var handle_list = fb.GetLibraryItems();
	var artists = tfo.EvalWithMetadbs(handle_list).toArray();
	console.log(handle_list.Count === artists.length); // True
	```
