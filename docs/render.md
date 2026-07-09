# render

`imgui` is an alias for `render`. All primitives draw into the background draw list.

Render sizes are DPI-aware. Coordinates stay in screen pixels, while text size, line thickness, rectangle size, rounding, circle radius, and image size are scaled automatically.

## get_dpi_scale

```lua
render.get_dpi_scale(): number
```

Returns current UI DPI scale.

## setup_font

```lua
render.setup_font(path: string, size: number, weight: number = 400): string | nil
```

Loads a custom font from disk and returns a font id that can be passed into `render.text` and `render.calc_text_size`.

`weight` controls custom font thickness. Use values like `300`, `400`, `600`, `700` or `900`.

```lua
local inter = render.setup_font("C:\\Windows\\Fonts\\arial.ttf", 16, 700)

register_callback("draw", function()
    if inter then
        render.text(24, 24, "custom bold font", color_t(1, 1, 1, 1), 16, inter)
    end
end)
```

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

## get_screen_size

```lua
render.get_screen_size(): table
```

Returns `{ x = width, y = height }`.

## text

```lua
render.text(x: number, y: number, text: string, color: color, size: number, font: string, flags: number)
```

```lua
render.text(24, 24, "neverfair", color_t(1, 1, 1, 1), 16, render.fonts.verdana, render.flags.outline)
```

## calc_text_size

```lua
render.calc_text_size(text: string, size: number, font: string): table
render.text_size(text: string, size: number, font: string): table
```

Returns `{ x = width, y = height }`.

## image

```lua
render.load_image(path: string): image | nil
render.load_image_bytes(bytes: string): image | nil
render.image(image: image, x: number, y: number, w: number, h: number, color: color)
render.draw_image(image: image, x: number, y: number, w: number, h: number, color: color)
image:get_size(): table
```

```lua
local logo = render.load_image("C:\\neverfair\\logo.png")

register_callback("draw", function()
    if not logo then
        return
    end

    render.image(logo, 24, 24, 48, 48, color_t(1, 1, 1, 1))
end)
```

## line

```lua
render.line(x1: number, y1: number, x2: number, y2: number, color: color, thickness: number)
```

## rect

```lua
render.rect(x: number, y: number, w: number, h: number, color: color, thickness: number, rounding: number)
```

## rect_filled

```lua
render.rect_filled(x: number, y: number, w: number, h: number, color: color, rounding: number)
render.filled_rect(x: number, y: number, w: number, h: number, color: color, rounding: number)
```

## rect_filled_multicolor

```lua
render.rect_filled_multicolor(x: number, y: number, w: number, h: number, top_left: color, top_right: color, bottom_right: color, bottom_left: color, rounding: number)
render.rect_multicolor(x: number, y: number, w: number, h: number, top_left: color, top_right: color, bottom_right: color, bottom_left: color, rounding: number)
```

## rect_filled_gradient

```lua
render.rect_filled_gradient(x: number, y: number, w: number, h: number, first: color, second: color, direction: string, rounding: number)
render.rect_gradient(x: number, y: number, w: number, h: number, first: color, second: color, direction: string, rounding: number)
```

`direction` can be `"vertical"` or `"horizontal"`.

## circle

```lua
render.circle(x: number, y: number, radius: number, color: color, thickness: number, segments: number)
```

## circle_filled

```lua
render.circle_filled(x: number, y: number, radius: number, color: color, segments: number)
render.filled_circle(x: number, y: number, radius: number, color: color, segments: number)
```

## circle_filled_gradient

```lua
render.circle_filled_gradient(x: number, y: number, radius: number, inner: color, outer: color, segments: number)
render.circle_gradient(x: number, y: number, radius: number, inner: color, outer: color, segments: number)
```

## circle_3d

```lua
render.circle_3d(pos: vec3, radius: number, color: color, thickness: number, normal: vec3, segments: number)
```

Draws a world-space circle in the plane defined by `normal`.

```lua
render.circle_3d({ x = 0, y = 0, z = 64 }, 18, color_t(1, 1, 1, 1), 2, { x = 0, y = 0, z = 1 })
```

## circle_filled_3d

```lua
render.circle_filled_3d(pos: vec3, radius: number, color: color, normal: vec3, segments: number)
render.filled_circle_3d(pos: vec3, radius: number, color: color, normal: vec3, segments: number)
```

## circle_fade_3d

```lua
render.circle_fade_3d(pos: vec3, radius: number, outer: color, inner: color, normal: vec3, segments: number)
render.circle_3d_fade(pos: vec3, radius: number, outer: color, inner: color, normal: vec3, segments: number)
```

Draws a world-space radial gradient circle.

## world_to_screen

```lua
render.world_to_screen(x: number, y: number, z: number): table | nil
```

Returns `{ x = screen_x, y = screen_y }` or `nil`.
