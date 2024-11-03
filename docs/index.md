---
hide: navigation
---

This component for [foobar2000](https://www.foobar2000.org) is based on [WSH Panel Mod](https://code.google.com/archive/p/foo-wsh-panel-mod/).

It allows the creation of customisable panels that can be written with
`JavaScript` rather than the `C++` required by the [foobar2000 SDK](https://www.foobar2000.org/SDK).

Under the hood, it uses `Windows Script Host`. Because of this, JS language
support is limited to `ECMAScript 5`. Nothing newer will ever be supported.

Here are just some of the features provided by the component...

* Custom drawing of text, external images, lines, rectangles, etc.
* Use fonts/colours from the main preferences of whichever user interface you are using.
* Executing main/context menu commands.
* Ability to create custom buttons/menus.
* Capture keystrokes/mouse movement/clicks.
* [Callbacks](docs/callbacks/index.md) can be used to trigger code based on various `foobar2000`, `Windows` and `Component` events.
* Read/[write](docs/interfaces/IMetadbHandleList.md#updatefileinfofromjsonstr) file tags.
* Complete manipulation of playlists.
* Media Library display/sorting/filtering
* [Save settings](docs/namespaces/window.md#windowgetpropertyname-default_value) on a per panel basis. These persist between restarts
and are stored inside the layout configuration file for whichever UI your are using. You can also write your own functions to
load/save settings from `JSON` or plain text files.
* [Built in support](docs/namespaces/utils.md#utilshttprequestasyncwindow_id-type-url-user_agent_or_headers-post_data) for
making `GET / POST` requests which return plain text and there is also a method for downloading binary files. If you prefer, you
can use the `Microsoft.XMLHTTP` `ActiveX` object.
* There are many built in methods for working with the local filesystem, launching external applications etc. Previous
versions / other scripting components rely on `ActiveX` objects but the need for those is greatly reduced.
* And much more...
