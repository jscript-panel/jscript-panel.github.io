!!! note
	For sample users, `Text Display` handles `$font` code automatically.

	As of component version `3.6.0`, `$rgb` works wherever custom title
	title formatting is supported. Also, a new `gr.WriteText2` method has been added
	which supports `$font` and `$rgb`.

### $rgb

You can use these colour methods which are documented [here](https://wiki.hydrogenaud.io/index.php?title=Foobar2000:Title_Formatting_Reference#Historical_and_Columns_UI_color_functions).

```
$rgb(r,g,b) // only the 3 value variant is supported
$rgb()
$hsl(h,s,l) // only the 3 value variant is supported
$hsl()
$blend(colour1,colour2,part,total)
$transition(string,colour1,colour2)
```

### $font

This is not a common function and is exclusive to `JScript Panel 3`. It takes up to 6 values.

`$font(name,size,weight,style,underline,strikethrough)`

If changing the font, you must the supply the `name` and `size` values. The rest are optional.

|Value||
|---|---|
|size|Supported values are `8` - `144`.
|weight|Default `400`, `700` is bold. Supported values are `100` - `950`.|
|style|Default `0`. Use `1` for `oblique` or `2` for `italic`.|
|underline|Default `0`. Use `1` to enable.|
|strikethrough|Default `0`. Use `1` to enable.|

You can use `$font()` with no values to reset back to default.

### Using in your own scripts.

See the `basic` samples `$rgb` and `$rgb + $font`.
