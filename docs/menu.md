# menu

## is_open

```lua
menu.is_open(): boolean
```

Returns whether the Neverfair menu is currently open.

## get_pos

```lua
menu.get_pos(): table
```

Returns menu position as `{ x = number, y = number }`.

## get_size

```lua
menu.get_size(): table
```

Returns DPI-normalized menu size as `{ x = width, y = height }`. Use this value as `w/h` for render functions.

## get_rect

```lua
menu.get_rect(): table
```

Returns menu bounds:

| Field | Description |
| --- | --- |
| `x` | Left edge in screen pixels |
| `y` | Top edge in screen pixels |
| `z` | Right edge in screen pixels |
| `w` | Bottom edge in screen pixels |
| `width` | DPI-normalized width for render functions |
| `height` | DPI-normalized height for render functions |
| `pixel_width` | Raw pixel width |
| `pixel_height` | Raw pixel height |

```lua
local rect = menu.get_rect()
render.rect_filled(rect.x, rect.y, rect.width, rect.height, color_t(0, 0, 0, 0.5))
```

## get_binds

```lua
menu.get_binds(): table
binds.get_all(): table
```

Both functions return the same bind list.

Each bind entry contains:

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | Bind name |
| `value` | boolean, number | Bound value |
| `preview` | string | Display-ready value |
| `key` | number | Virtual key code |
| `key_name` | string | Display key name |
| `mode` | string | `hold`, `toggle`, or `always_on` |
| `active` | boolean | Current bind state |
| `visible` | boolean | Whether bind is shown in active list |
| `type` | string | `boolean`, `integer`, `float`, `combo`, or `multi_selection` |
| `owner` | string | `none`, `rage`, or `legit` |
| `index` | number | Bind slot index |

```lua
register_callback("draw", function()
    local y = 120

    for _, bind in ipairs(binds.get_all()) do
        if bind.active and bind.visible then
            render.text(24, y, bind.name .. ": " .. bind.preview .. " [" .. bind.mode .. "]", color_t(1, 1, 1, 1), 13, render.fonts.verdana)
            y = y + 16
        end
    end
end)
```

## notify

```lua
menu.notify(text: string, color: color | nil)
```

Sends a Neverfair devlog notification.

```lua
menu.notify("script loaded", color_t(0.2, 0.75, 1.0, 1.0))
```

## get_username

```lua
menu.get_username(): string
```

Returns the current Neverfair username.

## get_cheat_name

```lua
menu.get_cheat_name(): string
```

Returns the current cheat name.

## example

```lua
register_callback("draw", function()
    local rect = menu.get_rect()
    local text = menu.get_cheat_name() .. " / " .. menu.get_username()
    render.text(rect.x + 16, rect.y + 16, text, color_t(1, 1, 1, 1), 14)
end)
```
