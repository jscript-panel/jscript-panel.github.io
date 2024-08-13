!!! note
	This is experimental and subject to change. I'm providing raw data only and I have no idea how to use this.

**Properties**

|||||
|---|---|---|---|
|ChannelConfig|`number`|
|ChannelCount|`number`|
|Data|`VBArray`|You need to use `toArray()` on this before using.
|SampleCount|`number`|
|SampleRate|`number`|

!!! note
	You must check the return value from `fb.GetAudioChunk` is valid before using.

	```js
	// offset is optional, defaults to zero
	var chunk = fb.GetAudioChunk(requested_length, offset);

	if (chunk) {
		// chunk now has the following properties
		// chunk.ChannelConfig
		// chunk.ChannelCount
		// chunk.SampleRate
		// chunk.SampleCount
		// chunk.Data

		var data = chunk.Data.toArray();

		var channel_count = chunk.ChannelCount;
		for (var i = 0; i < data.length; i += channel_count) {
			// assuming stereo
			var l = data[i];
			var r = data[i + 1];
		}
	}
	```

	The source code for `fb.GetAudioChunk` is basically this:

	```cpp
	// visualisation_stream_v2::ptr
	if (m_vis.is_valid())
	{
		double time{};
		if (m_vis->get_absolute_time(time))
		{
			audio_chunk_impl chunk;
			if (m_vis->get_chunk_absolute(chunk, time + offset, requested_length))
			{
				*out = new ComObject<AudioChunk>(chunk);
			}
		}
	}
	```

	`get_absolute_time` and `get_chunk_absolute` and their arguments are described here:

	[https://github.com/marc2k3/foobar2000-sdk/blob/main/foobar2000/SDK/vis.h](https://github.com/marc2k3/foobar2000-sdk/blob/main/foobar2000/SDK/vis.h)

	`IAudioChunk` is a simplified wrapper around this:

	[https://github.com/marc2k3/foobar2000-sdk/blob/main/foobar2000/SDK/audio_chunk.h](https://github.com/marc2k3/foobar2000-sdk/blob/main/foobar2000/SDK/audio_chunk.h)
