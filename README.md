# Customise the controls of fabric.js
Implementation of a way of changing the icon / cursor / action of the fabric.js corner controls.

# How to install

## Bower

```
bower install fabric-customise-controls --save
```

## npm

```
npm install fabric-customise-controls --save
```

# Note on versions
if you support the latest version of fabric.js 1.6.x use the release 0.1.0 of this extension. Otherwise all older releases have
downward compatibility for fabric.js 1.5.0.

# Live Demo Page
http://pixolith.github.io/fabricjs-customise-controls-extension/example/index.html

## What is this?
This is an extension which overwrites certain functions in the fabric.js core to enable you to customise the controls
through easy settings in your fabric.js project preserving the opportunity to update the fabric.js libary in the future.

## Why would you want this?
Well, i have felt the need to adapt the fabric.js UI to the project is is put in. Especially special actions and icons for the
controls were needed. Since you can't do that without massively hacking the core, it seemed cleaner to create this for future use.

## How to use
Add customiseControls.js (or its minified version) to your fabric.js project and reference in your html:
```
<script defer src="../path-to/fabric.min.js"></script>
<script defer src="../path-to/customiseControls.js"></script>
```

### Customising the Controls:
```
fabric.Canvas.prototype.customiseControls({
    tl: {
        action: 'rotate',
        cursor: 'cow.png'
    },
    tr: {
        action: 'scale'
    },
    bl: {
        action: 'remove',
        cursor: 'pointer'
    },
    br: {
        action: 'moveUp',
        cursor: 'pointer'
    },
    mb: {
        action: 'moveDown',
        cursor: 'pointer'
    },
    mt: {
        action: {
            'rotateByDegrees': 45
        }
    },
    mr: {
        action: function( e, target ) {
            target.set( {
                left: 200
            } );
            canvas.renderAll();
        }
     }
});
```

This will overwrite the actions and cursor handler for adding custom actions.

* **tl: object**

top-left corner passing an object consisting of corner action (see Actions) and cursor (see Cursors)

#### Actions:

currently the following actions are possible:

* drag
* scale
* scaleX
* scaleY
* rotate
* remove (custom)
* moveUp (z-index, custom) since 0.0.3
* moveDown (z-index, custom) since 0.0.3
* rotateByDegrees: int (custom) since 0.0.4 (origin can now be set to anything)
* define your own functions so i don't have to do it since 0.1.2 ( see the example above, returned are always the event and the target for you to use )

**Default action is: 'scale'**


#### Cursors:

currently the native cursors are possible as well as a custom cursor url.

Depending on what you set the javascript will detect if you have set an image which needs to be loaded or a native cursor.

**Default is: resize direction cursor**

### Customising the Corner Icons

```
fabric.Object.prototype.customiseCornerIcons({
    settings: {
        borderColor: 'black',
        cornerSize: 25,
        cornerShape: 'rect',
        cornerBackgroundColor: 'black',
        cornerPadding: 10
    },
    tl: {
        icon: 'icons/rotate.svg'
    },
    tr: {
        icon: 'icons/resize.svg'
    },
    bl: {
        icon: 'icons/remove.svg'
    },
    br: {
        icon: 'icons/up.svg'
    },
    mb: {
        icon: 'icons/down.svg'
    }
});
```

This will overwrite the controls handler (for all Objects) for adding custom icons and corresponding background-shapes and colors (since 0.0.3).

* **cornerSize: int**

size in pixels of the corner control box

* **cornerShape: string ('rect', 'circle')**

shape of the corner control box

* **borderColor: string (color)**

color of the bounding box border

* **cornerBackgroundColor: string (color)**

color of the background shape

* **cornerPadding: int**

inner Padding between icon image and background shape

* **tl: object**

corner-type passing an object with the desired icon url


You can also set these settings **Object specific** using inheritance of this prototype (since 0.0.3):

```
yourFabricObject.customiseCornerIcons({
    settings: {
        borderColor: 'black',
        cornerSize: 25,
        cornerShape: 'rect',
        cornerBackgroundColor: 'black',
        cornerPadding: 10
    },
    tl: {
        icon: 'icons/rotate.svg'
    },
    tr: {
        icon: 'icons/resize.svg'
    },
    bl: {
        icon: 'icons/remove.svg'
    },
    br: {
        icon: 'icons/up.svg'
    },
    mb: {
        icon: 'icons/down.svg'
    }
});
```

**Default is: currently not drawing anything but displaying a warning that your image might be corrupt unless cornerShape is set.
Then it will draw the Shape and display a console warn about the image url.**

You can set the size of the control icons or the border color with the standard setter too if you like to, yet it is also included in
the function above.

```
fabric.Object.prototype.set( {
    borderColor: '#000000',
    cornerSize: 34,
    } );
```

That should be it, feel free to contact me concerning bugs or improvements.

## Note

American english can be used too, so calling:
```
fabric.Object.prototype.customizeCornerIcons
fabric.Canvas.prototype.customizeControls
```
works too.

## Example Implementation
There is an example implementation in the example folder, just open the index file and check out how the custom handles look like
when applied to the test images. The source for that is also provided in the example.js.

## Usage
Licensed under the MIT license.
