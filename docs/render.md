# render

`imgui` is an alias for `render`. Drawing is done through the background draw list.

## get_screen_size

```lua
render.get_screen_size(): table
```

Returns `{ x = width, y = height }`.

## text

```lua
render.text(x: number, y: number, text: string, color: color, size: number)
```

```lua
render.text(24, 24, "neverfair", color_t(1, 1, 1, 1), 16)
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

## circle

```lua
render.circle(x: number, y: number, radius: number, color: color, thickness: number, segments: number)
```

## circle_filled

```lua
render.circle_filled(x: number, y: number, radius: number, color: color, segments: number)
render.filled_circle(x: number, y: number, radius: number, color: color, segments: number)
```

## world_to_screen

```lua
render.world_to_screen(x: number, y: number, z: number): table | nil
```

Returns `{ x = screen_x, y = screen_y }` or `nil`.
