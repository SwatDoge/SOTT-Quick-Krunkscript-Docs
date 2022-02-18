# 2D Rendering

## Overlay canvas <Badge type="tip" text="client-side" vertical="middle" /> 
Krunker has a 2d overlay called *the canvas*. It allows you to render shapes and text on top of a 2d overlay.

```krunkscript
# Get dimensions of overlay obj{x, y} 
GAME.OVERLAY.getSize();
```
```krunkscript
# Move entire overlay 
GAME.OVERLAY.offset(
    10,     # num x offset
    0       # num y offset
);             
```
```krunkscript
# Scale overlay
GAME.OVERLAY.scale(
    0.1     #num scale
);                
```

```krunkscript
# Get text width (num) on overlay based on font size
GAME.OVERLAY.measureText(
    10,     #num font size
    "Test"  #str text
);
```

```krunkscript
# Clear overlay
GAME.OVERLAY.clear();
```

## Render loop <Badge type="tip" text="client-side" vertical="middle" />
You can draw on the overlay using the [render](/unmerged/scripting.html#render) hook.

:::tip
The render hook runs after the update hook, see [order of execution](/unmerged/game_logic.html#order-of-execution)
:::

```krunkscript
action render(num delta) {
    # Create a red triangle
    GAME.OVERLAY.drawRect(0, 0, 20, 15, 0, "#ff0000", 1);
}
```

## 2D shapes <Badge type="tip" text="client-side" vertical="middle" /> 

:::tip
Canvas shapes start at the top left of your screen, setting position will offset it to the bottom right
:::

### Text

:::tip
You can use a custom font-family from a mod for the canvas, as shown in the example below
:::

:::warning
Keep in mind that default browser font families may differ for other browsers
:::

```krunkscript

# Draw text on screen
GAME.OVERLAY.drawText(
    "Hello world",  # str text
    0,              # num x position
    0,              # num y position
    0,              # num rotation (0 - 360)
    20,             # num font size
    "center",       # str alignment ("left", "center", "right")
    "#FFF",         # str color
    0.9,            # num opacity
    "comic sans"    # str font
);

# Get canvas text width
num textWidth = GAME.OVERLAY.measureText(
    24, # num fontsize
    "Testing" # string text
);
```

### Rectangles

```krunkscript
GAME.OVERLAY.drawRect(
    0,            # num x position
    0,            # num y position
    100,          # num width
    100,          # num height
    0,            # num rotation (0 - 360)
    "#FFF",       # str color
    0.9,          # num opacity (0 - 1)
    false         # bool center
);
```

### Circles

```krunkscript
GAME.OVERLAY.drawCircle(
    0,           # num x position
    0,           # num y position
    100,         # num width
    100,         # num height
    0,           # num rotation (0 - 360)
    "#FFF",      # str color
    0.9,         # num opacity (0 - 1)
    false        # bool center
);
```

### Line

```krunkscript
GAME.OVERLAY.drawLine(
    0,           # num x start position
    0,           # num y start position
    100,         # num x end position
    100,         # num y end position
    20,          # num thickness
    "#FFF",      # str color
    0.9          # num opacity (0 - 1)
);
```

### Images

```krunkscript
GAME.OVERLAY.drawImage(
    "28142",    # str texture asset id
    0,          # num x position
    0,          # num y position
    256,        # num width
    256,        # num height
    0,          # num rotation (0 - 360)
    0.9         # num opacity (1 - 0)
);
```

## Direct canvas drawing <Badge type="tip" text="client-side" vertical="middle" />
In javascript, you can draw on the canvas using the `CanvasRenderingContext2D` API. Krunkscript also allows you to do this, and works mostly the same.

To create one of these drawings, you first make a path by moving the cursor and pathing shapes. After that you "stroke" (draw) the path. These lines and shapes can be modified in several ways to fit your needs.

:::warning
- These features are not officially documented, there might be mistakes
- This part of the doc is not final
:::

### Creating a basic line
```krunkscript
# Starting the path
GAME.OVERLAY.beginPath();

# Move cursor to a position
GAME.OVERLAY.moveTo(50, 140);

# Draw line
GAME.OVERLAY.lineTo(150, 60);

# Closing the path
GAME.OVERLAY.closePath();

# Drawing out the path
GAME.OVERLAY.stroke();
```

### Moving & drawing
```krunkscript
# Move the cursor
GAME.OVERLAY.moveTo(
    50,     # num x position
    140     # num y position
);
```

```krunkscript
# Set line width
GAME.OVERLAY.lineWidth(
    20       # num pixel width
);

# Set line dash width
GAME.OVERLAY.lineDashOffset(
    5        # num space between dashes on line
);

# Set corners where two lines meet
GAME.OVERLAY.lineJoin(
    "round"     #str type ("round", "bevel", "miter")
);

# Draw a line from cursor
GAME.OVERLAY.lineTo(
    150,     # num x position
    60       # num y position
);
```

### Filling & filling style
You can fill a shape with a certain color.

```krunkscript
# Set filling style
GAME.OVERLAY.fillStyle(
    "#FFF"  # str color
);

# Fill a path (before stroke)
GAME.OVERLAY.fill();
```

### Stroke & stroke style
Stroke style is the color of stroke lines.

```krunkscript
# Set stroke style
GAME.OVERLAY.strokeStyle(
    "#FFF"  # str color
);
```

```krunkscript
# Stroke a path
GAME.OVERLAY.stroke();
```

### Transforming & translating paths
You can modify a paths properties using translation.

```krunkscript
# Move path relative to itself
GAME.OVERLAY.translate(
    20,     # num x direction
    20      # num y direction
);
```

```krunkscript
# Transform allows you to translate an object thru a matrix
GAME.OVERLAY.transform(
    1,      # horizontal scaling
    0,      # horizontal skewing
    1,      # vertical skewing
    1,      # vertical scaling
    0,      # horizontal moving
    0       # vertical moving
);
```

```krunkscript
# Resets the current transform and reapplies using transform()
GAME.OVERLAY.setTransform(
    1,      # horizontal scaling
    0,      # horizontal skewing
    1,      # vertical skewing
    1,      # vertical scaling
    0,      # horizontal moving
    0       # vertical moving
);
```

### Saving & restoring drawing styles
```krunkscript
# Save a drawing state
GAME.OVERLAY.save();
```

```krunkscript
# Rollback a drawing state
GAME.OVERLAY.restore();
```