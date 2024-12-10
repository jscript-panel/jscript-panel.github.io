**Methods**

## `console.GetLines([with_timestamp])`
|Arguments|||
|---|---|---|
|with_timestamp|`boolean`|Default `false`.|

Returns a `VBArray` so you need to use `.toArray()` on the result.

Use in conjunction with [on_console_refresh](../callbacks/foobar2000.md#on_console_refresh).

## `console.ClearBacklog()`
No return value.

## `console.log(message)`
|Arguments|||
|---|---|---|
|message|`string`, `number`, `boolean`, `array`, `object`|

No return value.

!!! example
	```js
	console.log("blah"); // blah

	console.log(2 < 3); // True
	console.log(2 > 3); // False

	console.log(1,2,3); // 1 2 3
	console.log([1,2,3]); // 1,2,3

	var obj = {a:1};
	console.log(obj); // [object Object]
	console.log(JSON.stringify(obj)); // {"a":1}

	// multiple args are split by single spaces
	console.log("put", "a", "donk", "on", "it"); // put a donk on it
	console.log("a", 2, 3.5); // a 2 3.5
	```
