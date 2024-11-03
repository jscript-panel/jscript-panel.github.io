!!! note
	This is a topic for intermediate/advanced users with a good understanding of how `JScript Panel 3`
	works with relation to `handles` and `handle lists` and you're familiar with
	`callbacks`.

	It uses the same mechanism for data storage as [foo_playcount](https://www.foobar2000.org/components/view/foo_playcount),
	and data is remembered for up to 4 weeks when no matching track is part of the `Media Library` or any playlist.

	Unlike previous implementaions in other scripting components, this allows you to customise the
	title formatting that database records are bound to.

	The default is `$lower($meta(artist,0) - %title%)` but it can be changed via
	`File>Preferences>Advanced>Tools>JScript Panel 3>Playback Statistics Title Format`.

	Note that changing this requires an immediate `foobar2000` restart and any previously
	saved data is lost forever. Be careful!

	Remember that if you think of using `%path%`, you must also include `%subsong%`. One
	physical file can have the same path for multiple handles if it's a cuesheet or
	other type of track with multiple chapters.

## Overview

First of all, there are 6 fields available through title formatting in any component and search.

```
%jsp3_playcount%
%jsp3_loved%
%jsp3_first_played%
%jsp3_last_played%
%jsp3_rating%
%jsp3_skipcount% // added in component version 3.3.14
```

To write these values, 6 `handle` methods can be used.

```js
var handle = fb.GetFocusItem();
if (handle) {
	// Must be a whole number, use 0 to clear.
	handle.SetPlayCount(12);
	// Must be a whole number, use 0 to clear.
	handle.SetLoved(1);
	// Must be a whole number, use 0 to clear.
	handle.SetFirstPlayed(unix_timestamp);
	// Must be a whole number, use 0 to clear.
	handle.SetLastPlayed(unix_timestamp);
	// Must be a whole number, use 0 to clear.
	// Obviously there are no restrictions on the maximum value
	handle.SetRating(5);
	// Added in 3.3.14. Must be a whole number, use 0 to clear.
	handle.SetSkipcount(skipcount);
}
```

Although first played and last played are written/stored as unix timestamps, they are retrieved as
strings in the usual [foobar2000](https://www.foobar2000.org) `YYYY-MM-DD HH:MM:SS` format,
adjusted to your local time zone.

Helper methods already exist for converting between them.

[utils.DateStringToTimestamp(str)](../namespaces/utils.md#utilsdatestringtotimestampstr)

[utils.TimestampToDateString(ts)](../namespaces/utils.md#utilstimestamptodatestringts)

To get the current time as a unix timestamp, you can use this:

```js
var now = utils.Now();
```

After updating value(s) for a `handle`, you must use `RefreshStats` so the [foobar2000](https://www.foobar2000.org) core
and all other components are made aware of the changes. There is a `IMetadbHandleList` `RefreshStats()` method for this.

```js
var handle = fb.GetFocusItem();
handle.SetRating(5);

// creating a handle list from a single handle can be done like this...
var handles = fb.CreateHandleList(handle);
handles.RefreshStats();
```

Finally there is also `IMetadbHandleList` `ClearStats()` which should be self explanatory.
This method calls `RefreshStats()` internally so there is no need to call it after.

## Example

Here's a crude example that updates as you play using the same rules as [Last.fm](https://last.fm)
for the amount of time you have to play a track. Of course it can be modified in any way you like.

```js
var time_elapsed = 0;
var target_time = 0;

var tf_fp = fb.TitleFormat("%jsp3_first_played%");

// if a track hasn't been played yet, we want zero
// so it can be easily incremented
var tf_pc = fb.TitleFormat("$if2(%jsp3_playcount%,0)");

function on_playback_new_track() {
	// reset
	time_elapsed = 0;

	// this example uses the same rule as last.fm
	// half the track length or 4 minutes - whichever is lower
	target_time = Math.min(Math.ceil(fb.PlaybackLength / 2), 240);
}

function on_playback_time() {
	time_elapsed++;
	if (time_elapsed == target_time) {
		var now = Math.round(new Date().getTime() / 1000);
		var handle = fb.GetNowPlaying();

		// the return value from title format functions is always a string
		// but we want a number
		var playcount = Number(tf_pc.Eval());

		// increment playcount by 1
		handle.SetPlaycount(playcount + 1)

		// only write first played if it's currently empty
		if (tf_fp.Eval() == "") {
			handle.SetFirstPlayed(now);
		}

		// always write last played
		handle.SetLastPlayed(now)

		// notify foobar2000 core / other components
		fb.CreateHandleList(handle).RefreshStats();
	}
}
```
