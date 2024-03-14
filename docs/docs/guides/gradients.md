!!! note
	`gr` on this page refers to [IJSGraphics](../interfaces/IJSGraphics.md)

## Changes in `3.4.0`
`gr.FillGradientRectangle` and `gr.FillGradientRectangleAdvanced` have been removed.
This is because all `Draw`/`Fill` methods now support gradients.

A quick and easy replacement for `gr.FillGradientRectangle` has been added in `helpers.txt`
and this lets you create a simple vertical or horizontal gradient with 2 colours.

```js
// removed component method
gr.FillGradientRectangle(x, y, w, h, direction, colour1, colour2);

// new JS method
FillGradientRectangle(gr, x, y, w, h, direction, colour1, colour2);
```

If you used `gr.FillGradientRectangleAdvanced` previously, you can now supply
the stringified `brush` in place of a single colour when using `gr.FillRectangle`.

```js
// removed component method
gr.FillGradientRectangleAdvanced(x, y, w, h, brush);

// now you can do this...
gr.FillRectangle(x, y, w, h, brush);

// and continue doing this...
gr.FillRectangle(x, y, w, h, RGB(255, 0, 0));
```

## Stops
Before creating a `brush`, we need to define the colours we want to use. So the first
thing to do is create an array of [stops](https://learn.microsoft.com/en-us/windows/win32/api/d2d1/nn-d2d1-id2d1gradientstopcollection#remarks).
In this component, an array of `stops` must be at least `2` in length.

A `stop` is a `position` and a `colour`. The min/max values for a `position` is `0` and `1`.
Anyone reading this should be familiar with valid `colour` values!

So the simplest example can be:

```js
var stops = [
	[0, RGB(255, 0, 0)],
	[1, RGB(0, 0, 255)],
];
```

If you want to insert more colours:

```js
var stops = [
	[0, RGB(255, 0, 0)],
	[0.2, RGB(0, 255, 0)],
	[1, RGB(0, 0, 255)],
];
```

`0.5` might be a more desirable `position` for the second `stop` but it's just an example
that anything between `0` and `1` is valid.

## Brushes
Now we know what `stops` are, we can create a brush. This can be [Linear](https://learn.microsoft.com/en-us/windows/win32/direct2d/direct2d-brushes-overview#using-linear-gradient-brushes) or [Radial](https://learn.microsoft.com/en-us/windows/win32/direct2d/direct2d-brushes-overview#using-radial-gradient-brushes).

!!! note
	There are 2 samples in the `basic` folder you may want to check out first. Look for `LinearGradients` and `RadialGradient`.

### Linear
A linear brush must have 3 properties: `Start`, `End` and `Stops`.

```js
var linear_brush = {
	Start : [0, 0], // x and y values
	End : [0, 0], // x and y values
	Stops: stops
};
```

The `Start` and `End` values are relative the `x` and `y` positions of the rectangle. If we lift
`FillGradientRectangle` from `helpers.txt`, we can inspect a working example.

```js
function FillGradientRectangle(gr, x, y, w, h, direction, colour1, colour2) {
	var stops = [[0, colour1], [1, colour2]];
	var brush = {Start : [0, 0], Stops: stops};
	if (direction == 0) brush.End = [0, h];
	else brush.End = [w, 0];
	gr.FillRectangle(x, y, w, h, JSON.stringify(brush));
}
```

!!! note
	See the final step there is to use `JSON.stringify` on the `brush` object. `JavaScript` objects
	can not be passed directly to the component so it must be a `string`.

The `Start` `x` and `y` values never change. The `End` positions change depending on the effect you want.

While that example is fixed to vertical or horizontal, there are no limitations when creating your
own.

So for a diagonal effect, we can write our own code like this.

```js
// ==PREPROCESSOR==
// @import "%fb2k_component_path%helpers.txt"
// ==/PREPROCESSOR==

var stops = [
	[0, RGB(255, 0, 0)],
	[1, RGB(0, 0, 255)],
];

var linear_brush = {
	Stops: stops,
	Start: [0, 0]
};

function on_paint(gr) {
	linear_brush.End = [window.Width, window.Height];
	gr.FillRectangle(0, 0, window.Width, window.Height, JSON.stringify(linear_brush));
}
```

### Radial
A radial brush must have 3 properties: `Centre`, `Radius` and `Stops`.

```js
var radial_brush = {
	Centre : [0, 0], // x and y values
	Radius : [0, 0], // x and y values
	Stops: stops
};
```

This is the code from an included `basic` sample:

```js
// ==PREPROCESSOR==
// @import "%fb2k_component_path%helpers.txt"
// ==/PREPROCESSOR==

var stops = [
	[ 0.0, RGB(227, 9, 64) ],
	[ 0.33, RGB(231, 215, 2) ],
	[ 0.66, RGB(15, 168, 149) ],
	[ 1.0, RGB(19, 115, 232) ]
];

var radial_brush = {
	Centre : [0, 0], // x and y values
	Radius : [0, 0], // x and y values
	Stops: stops
};

function on_paint(gr) {
	radial_brush.Centre = [window.Width / 2, window.Height / 2];
	radial_brush.Radius = [window.Width / 2, window.Height / 2];
	gr.FillRectangle(0, 0, window.Width, window.Height, JSON.stringify(radial_brush));
}
```

This silly example updates the `Centre` values on mouse move.

```js
// ==PREPROCESSOR==
// @import "%fb2k_component_path%helpers.txt"
// ==/PREPROCESSOR==

var mouse_x = 0; mouse_y = 0;

var stops = [
	[ 0.0, RGB(227, 9, 64) ],
	[ 0.33, RGB(231, 215, 2) ],
	[ 0.66, RGB(15, 168, 149) ],
	[ 1.0, RGB(19, 115, 232) ]
];

var radial_brush = {
	Centre : [0, 0], // x and y values
	Radius : [0, 0], // x and y values
	Stops: stops
};

function on_paint(gr) {
	radial_brush.Centre = [mouse_x, mouse_y];
	radial_brush.Radius = [window.Width / 2, window.Height / 2];
	gr.FillRectangle(0, 0, window.Width, window.Height, JSON.stringify(radial_brush));
}

function on_mouse_move(x, y) {
	mouse_x = x;
	mouse_y = y;
	window.Repaint();
}
```
