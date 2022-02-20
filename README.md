![All Downloads](https://img.shields.io/github/downloads/tues/fvtt-resource-icons/total?style=for-the-badge)

![Latest Release Download Count](https://img.shields.io/github/downloads/tues/fvtt-resource-icons/latest/RI.zip)

# Resource Icons x4

Resource Icons x4 is a Foundry VTT module that adds 4 customizable icons to tokens to track resources.

## Fork

This is a fork I made quickly to allow having 4 icons instead of 3 because the system we play with my group nowadays has 4 basic resources. I don't intend to maintain this long-term except making sure it suits my group's needs, so please don't rely on this fork unless you know what you're doing.

Thanks to [Jesse Vo](https://github.com/jessev14) for creating the [original module](https://github.com/jessev14/resource-icons).

## Screenshot (from the original version with 3 icons)

<img src="/img/demo.png" width="500"/>

## Usage

Resource Icons are configured in the Resources tab of the Token Configuration window.

To activate an icon, select a resource for it to track. To deactivate an icon, select "None."

If no icon image is selected, the default icon image is a white circle.

The border, background, and tint of each icon can be individually set.

<img src="/img/config2.png" width="500"/>

The border shape (circle/square), where the resource icons are anchored (above/below/left of/right of token), and icon alignemnt (inside/outside of token) can be changed in the module settings (per user with an option to use world default set by GM).

## Technical Notes

Resource Icons patches (via lib-wrapper) `CONFIG.Token.objectClass.prototype.draw` to implement resource icon drawing. This drawing is handled by a new method added to the Token object class: `drawResourceIcons`. This method adds four PIXI container children to the token. Each of these PIXI containers themselves are assigned three PIXI children (based on resource icon configuration): background (which encompasses border), icon image, and value text.

Resource Icons also patches `CONFIG.Token.objectClass.prototype._onUpdate` to handle changes to resource icon configuration (in which case `drawResourceIcons` is called to re-draw the icons) and to handle changes to resoure values when a token's actor is updated. This updated is handled by another new method added to the Token object class: `updateResourceIconValues`. This method simply changes the value text child of each PIXI container to the new value of the assigned resource.
