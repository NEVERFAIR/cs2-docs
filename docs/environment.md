# environment

This page describes Neverfair-specific globals. Standard Lua libraries are available through LuaJIT.

## print

```lua
print(...)
```

Writes text to the Neverfair console.

```lua
print("Current sensitivity:", cvars.sensitivity:get_float())
```

## color_t

```lua
color_t(r: number, g: number, b: number, a: number): color
```

Creates a color table for API functions. Values can be passed as `0..1` floats or `0..255` numbers.

```lua
local accent = color_t(0.2, 0.75, 1.0, 1.0)
render.text(24, 24, "neverfair", accent, 16)
```

## color_print

```lua
color_print(text: string, color: color)
```

Prints colored text into the Neverfair console.

```lua
color_print("[neverfair] ", color_t(0.2, 0.75, 1.0, 1.0))
color_print("loaded", color_t(1, 1, 1, 1))
```

## register_callback

```lua
register_callback(name: string, func: function)
```

Registers runtime callbacks. Supported built-in callback names:

| Name | Arguments | Description |
| --- | --- | --- |
| `draw` | none | Called every frame |
| `paint` | none | Alias for `draw` |
| `frame_stage` | `stage` | Called on frame stage updates |
| `frame_stage_notify` | `stage` | Alias for `frame_stage` |
| `unload` | none | Called before script unload |
| event name | `event` | Called for game event |

```lua
register_callback("draw", function()
    render.text(24, 24, "runtime", color_t(1, 1, 1, 1), 16)
end)
```
