## Minimum requirements & download
|Download|Release Date|Windows|foobar2000||
|:---|:---|:----|:---|:---|
|[:material-download: 3.4.18](https://github.com/jscript-panel/release/releases/latest)|24th March 2024|Windows 8.1+|1.6.6+|32bit/64bit

!!! note
	The last version compatible with `Windows 7/8` is available [here](https://github.com/jscript-panel/release/releases/tag/legacy).

## Required fonts
As of `3.4.7`, `FontAwesome` is no longer used by any included samples. [Segoe Fluent Icons](https://download.microsoft.com/download/8/f/c/8fc7cbc3-177e-4a22-af48-2a85e1c5bffb/Segoe-Fluent-Icons.zip) is now required. `Windows 11` users will already have this installed.

To display [Country Flags](./guides/country-flags.md), you should install the [Twemoji Mozilla](https://github.com/mozilla/twemoji-colr/releases/latest) font. This requires `Windows 10` or later.

## Installation
[https://wiki.hydrogenaud.io/index.php?title=Foobar2000:How_to_install_a_component](https://wiki.hydrogenaud.io/index.php?title=Foobar2000:How_to_install_a_component)

It is assumed you know how to add panels to your layout. Basic guides
can be found below.

[Default UI](http://wiki.hydrogenaud.io/index.php?title=Foobar2000:Layout_Editing_Mode)

[Columns UI](https://wiki.yuo.be/columns_ui:config:layout)

## Samples
Since the learning curve for writing your own scripts is quite steep, there
are many included samples that don't require any knowledge at all. You
can simply pick the one you want to use from the `Samples` button in
the [Configuration Window](configuration-window.md).

The [Gallery](../gallery/index.md) has recently been updated with more detailed
setup notes / usage instructions.

## Extra requirements
- The [IJSimage ApplyEffect](interfaces/IJSImage.md#applyeffecteffect) method requires `Windows 10` or later.
- Displaying coloured emoji requires `Windows 10` or later.
- The following require `foobar2000` `2.0`:
    * `console.ClearBacklog`
    * `console.GetLines`
    * `plman.FindByGUID`
    * `plman.GetGUID`
    * `plman.GetQueryItems`
    * `IMetadbHandle` `FileCreated`
    * `on_console_refresh`
