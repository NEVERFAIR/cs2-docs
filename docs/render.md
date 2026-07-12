# render

`imgui` is an alias for `render`. All primitives draw into the background draw list.

Render sizes are DPI-aware. Coordinates stay in screen pixels, while text size, line thickness, rectangle size, rounding, circle radius, and texture size are scaled automatically.

## screen_size

```lua
render.screen_size(): vec2_t
```

Returns current screen size. `render.get_screen_size()` is kept for compatibility.

See [`vec2_t`](types.md#vec2_t).

## frame_count

```lua
render.frame_count(): number
```

Returns current ImGui frame count.

## frame_time

```lua
render.frame_time(): number
```

Returns frame delta time.

## setup_texture

```lua
render.setup_texture(path: string): image_t | nil
```

Loads a texture from disk.

## setup_texture_rgba

```lua
render.setup_texture_rgba(bytes: string, width: number, height: number): image_t | nil
```

Creates a texture from raw RGBA bytes.

## setup_texture_from_memory

```lua
render.setup_texture_from_memory(bytes: string): image_t | nil
```

Loads an encoded image from memory.

## setup_font

```lua
render.setup_font(path: string, size: number, weight: number = 400): string | nil
```

Loads a custom font from disk and returns a font id that can be passed into `render.text` and `render.calc_txt_size`.

## calc_txt_size

```lua
render.calc_txt_size(text: string, size: number, font: string): vec2_t
```

Returns text size. `render.calc_text_size()` and `render.text_size()` are kept for compatibility.

## world_to_screen

```lua
render.world_to_screen(pos: vec3_t): vec2_t | nil
render.world_to_screen(x: number, y: number, z: number): vec2_t | nil
```

Returns screen position or `nil`.

## texture

```lua
render.texture(image: image_t, x: number, y: number, w: number, h: number, color: color_t)
```

Draws a texture. `render.image()` is kept for compatibility.

## text

```lua
render.text(x: number, y: number, text: string, color: color_t, size: number, font: string, flags: number)
```

```lua
render.text(24, 24, "neverfair", color_t(1, 1, 1, 1), 16, render.fonts.verdana, render.flags.outline)
```

## line

```lua
render.line(x1: number, y1: number, x2: number, y2: number, color: color_t, thickness: number)
```

## rect

```lua
render.rect(x: number, y: number, w: number, h: number, color: color_t, thickness: number, rounding: number)
```

## rect_filled

```lua
render.rect_filled(x: number, y: number, w: number, h: number, color: color_t, rounding: number)
```

## rect_filled_fade

```lua
render.rect_filled_fade(x: number, y: number, w: number, h: number, first: color_t, second: color_t, direction: string, rounding: number)
```

`direction` can be `"vertical"` or `"horizontal"`.

## circle

```lua
render.circle(x: number, y: number, radius: number, color: color_t, thickness: number, segments: number)
```

## circle_filled

```lua
render.circle_filled(x: number, y: number, radius: number, color: color_t, segments: number)
```

## circle_fade

```lua
render.circle_fade(x: number, y: number, radius: number, inner: color_t, outer: color_t, segments: number)
```

## arc

```lua
render.arc(x: number, y: number, radius: number, min_angle: number, max_angle: number, color: color_t, thickness: number, segments: number)
```

Angles are in degrees.

## polygon

```lua
render.polygon(points: vec2_t[], color: color_t)
```

Draws a filled convex polygon.

## poly_line

```lua
render.poly_line(points: vec2_t[], color: color_t, closed: boolean, thickness: number)
```

## push_clip_rect

```lua
render.push_clip_rect(x: number, y: number, w: number, h: number, intersect: boolean)
```

Pushes a draw clip rectangle.

## pop_clip_rect

```lua
render.pop_clip_rect()
```

Pops the current draw clip rectangle.

## circle_3d

```lua
render.circle_3d(pos: vec3_t, radius: number, color: color_t, thickness: number, normal: vec3_t, segments: number)
```

Draws a world-space circle in the plane defined by `normal`.

## circle_filled_3d

```lua
render.circle_filled_3d(pos: vec3_t, radius: number, color: color_t, normal: vec3_t, segments: number)
```

## circle_fade_3d

```lua
render.circle_fade_3d(pos: vec3_t, radius: number, outer: color_t, inner: color_t, normal: vec3_t, segments: number)
```

Draws a world-space radial gradient circle.

## fonts

```lua
render.fonts.default
render.fonts.main
render.fonts.pixel
render.fonts.picto
render.fonts.verdana
render.fonts.eventlog
render.fonts.icon
render.fonts.weapon
```

## flags

```lua
render.flags.center
render.flags.outline
render.flags.dropshadow
```

See [`color_t`](types.md#color_t), [`vec2_t`](types.md#vec2_t), [`vec3_t`](types.md#vec3_t), and [`image_t`](types.md#image_t).
