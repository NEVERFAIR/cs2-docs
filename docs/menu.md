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

Returns menu size as `{ x = number, y = number }`.

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
