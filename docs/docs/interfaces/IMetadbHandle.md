This will be used in the examples below:

```js
var handle = fb.GetFocusItem();
```

!!! note
	In real world code, you should alaways check the return
	values from methods like [fb.GetFocusItem](../namespaces/fb.md#fbgetfocusitem) and
	[fb.GetNowPlaying](../namespaces/fb.md#fbgetnowplaying) are not `null`.

**Properties**

|||||
|---|---|---|---|
|FileCreated|`number`|read|The number of seconds since 00:00:00 Thursday, 1 January 1970 UTC.|
|FileSize|`number`|read|
|LastModified|`number`|read|The number of seconds since 00:00:00 Thursday, 1 January 1970 UTC.|
|Length|`number`|read|
|Path|`string`|read|
|RawPath|`string`|read|
|SubSong|`number`|read|

!!! example
	```js
	console.log(handle.Path); // D:\SomeSong.flac
	console.log(handle.RawPath); // file://D:\SomeSong.flac
	console.log(handle.FileCreated); // 1659753717
	console.log(utils.TimestampToDateString(handle.FileCreated)); // 2022-08-06 03:41:57
	```

**Methods**

## `Compare(handle)`
|Arguments|||
|---|---|---|
|handle|[IMetadbHandle](IMetadbHandle.md)|

Returns a `boolean` value.

!!! example
	```js
	if (handle.Compare(handle2)) {
		// do something
	}
	```

## `Dispose()`

No return value.

## `GetAlbumArt([art_id, want_stub])`
|Arguments|||
|---|---|---|
|art_id|[AlbumArtId](../flags.md#albumartid)|Default `0`.|
|want_stub|`boolean`|Default `true`.|

Returns an [IJSImage](IJSImage.md) instance or `null` on failure.

!!! note
	This method can return album art from certain radio streams
	if the requested type is `Front`. Use [on_playback_dynamic_info_track](../callbacks/foobar2000.md#on_playback_dynamic_info_tracktype)
	to get notified of stream artwork changes.

!!! example
	```js
	var image = handle.GetAlbumArt();
	if (image != null) {
		// The path is now a property of the image.
		console.log(image.Path);
	}
	```

## `GetAlbumArtAsync(window_id[, art_id])`
|Arguments||||
|---|---|---|---|
|window_id|[window.ID](../namespaces/window.md)|
|art_id|[AlbumArtId](../flags.md#albumartid)|Default `0`.|

Use in conjunction with [on_get_album_art_done](../callbacks/component.md#on_get_album_art_donehandle-art_id-image).

!!! note
	This method does not retrieve stub images. See [fb.GetAlbumArtStub](../namespaces/fb.md#fbgetalbumartstubart_id).

## `GetAlbumArtEmbedded([art_id])`
|Arguments|||
|---|---|---|
|art_id|[AlbumArtId](../flags.md#albumartid)|Default `0`.|

Returns an [IJSimage](IJSImage.md) instance or `null` on failure.

## `GetAlbumArtThumbAsync(window_id[, art_id, max_size])`
|Arguments|||
|---|---|---|
|window_id|[window.ID](../namespaces/window.md)|
|art_id|[AlbumArtId](../flags.md#albumartid)|Default `0`.|
|max_size|`number`|Default `300`. The minimum allowed value is `50`. If the original image is smaller than the specified size, it will remain untouched.|

Use in conjunction with [on_get_album_art_done](../callbacks/component.md#on_get_album_art_donehandle-art_id-image).

!!! note
	This method does not retrieve stub images. See [fb.GetAlbumArtStub](../namespaces/fb.md#fbgetalbumartstubart_id).

## `GetFileInfo()`
Returns an [IFileInfo](IFileInfo.md) instance.

## `IsInLibrary()`

Returns a `boolean` value.

## `SetFirstPlayed(first_played)`
See [Playback Statistics](../guides/playback-statistics.md).

## `SetLastPlayed(last_played)`
See [Playback Statistics](../guides/playback-statistics.md).

## `SetLoved(loved)`
See [Playback Statistics](../guides/playback-statistics.md).

## `SetPlaycount(playcount)`
See [Playback Statistics](../guides/playback-statistics.md).

## `SetRating(rating)`
See [Playback Statistics](../guides/playback-statistics.md).

## `SetSkipcount(skipcount)`
See [Playback Statistics](../guides/playback-statistics.md).

## `ShowAlbumArtViewer([art_id, want_stub])`
|Arguments|||
|---|---|---|
|art_id|[AlbumArtId](../flags.md#albumartid)|Default `0`.|
|want_stub|`boolean`|Default `true`.|

No return value.

## `ShowAlbumArtViewer2(art_id, type)`
:octicons-tag-24: 3.7.0

|Arguments|||
|---|---|---|
|art_id|[AlbumArtId](../flags.md#albumartid)|
|type|[AlbumArtType](../flags.md#albumarttype)||

No return value.
