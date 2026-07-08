# render

`imgui` is an alias for `render`. All primitives draw into the background draw list.

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

## world_to_screen

```lua
render.world_to_screen(x: number, y: number, z: number): table | nil
```

Returns `{ x = screen_x, y = screen_y }` or `nil`.
