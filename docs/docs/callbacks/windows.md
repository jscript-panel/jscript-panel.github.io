## `on_char(code)`
|Arguments|||
|---|---|---|
|code|`number`|UTF16 encoded char|

## `on_drag_drop(action, x, y, mask)`
|Arguments|||
|---|---|---|
|action|[IDropAction](../interfaces/IDropAction.md)|
|x|`number`|
|y|`number`|
|mask|`number`|

## `on_drag_enter(action, x, y, mask)`
|Arguments|||
|---|---|---|
|action|[IDropAction](../interfaces/IDropAction.md)|
|x|`number`|
|y|`number`|
|mask|`number`|

## `on_drag_leave()`

## `on_drag_over(action, x, y, mask)`
|Arguments|||
|---|---|---|
|action|[IDropAction](../interfaces/IDropAction.md)|
|x|`number`|
|y|`number`|
|mask|`number`|

## `on_focus(is_focused)`
|Arguments|||
|---|---|---|
|is_focused|`boolean`|

Called when the panel gets/loses focus.

## `on_key_down(vkey)`
|Arguments|||
|---|---|---|
|vkey|`number`|[https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes)|

Keyboard shortcuts defined in the main preferences are always executed first and are not passed to this callback.

## `on_key_up(vkey)`
|Arguments|||
|---|---|---|
|vkey|`number`|[https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes)|

## `on_mouse_lbtn_dblclk(x, y, mask)`
## `on_mouse_lbtn_down(x, y, mask)`
## `on_mouse_lbtn_up(x, y, mask)`
## `on_mouse_leave()`
## `on_mouse_mbtn_dblclk(x, y, mask)`
## `on_mouse_mbtn_down(x, y, mask)`
## `on_mouse_mbtn_up(x, y, mask)`
## `on_mouse_move(x, y, mask)`
## `on_mouse_rbtn_dblclk(x, y, mask)`
## `on_mouse_rbtn_down(x, y, mask)`

## `on_mouse_rbtn_up(x, y, mask)`
You must return `true` if you want to suppress the default context menu. Use the ++shift+windows++ keys to bypass user code and open default context menu.

## `on_mouse_wheel(step)`
|Arguments|||
|---|---|---|
|step|`number`|

## `on_mouse_wheel_h(step)`
|Arguments|||
|---|---|---|
|step|`number`|

## `on_paint(gr)`
|Arguments|||
|---|---|---|
|gr|[IJSGraphics](../interfaces/IJSGraphics.md)|

Called when window is ready to draw.

## `on_size()`
Called when panel is resized.
