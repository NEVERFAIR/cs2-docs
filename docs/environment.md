# environment

This page describes Neverfair-specific globals. Standard Lua libraries are available through LuaJIT.

## print

```lua
print(...)
```

Sends text to Neverfair notifications.

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

Sends colored text to Neverfair notifications. End the text with `\0` to continue the same line without a newline.

```lua
local accent = color_t(0.2, 0.75, 1.0, 1.0)
local white = color_t(1, 1, 1, 1)

color_print("[neverfair] \0", accent)
color_print("loaded", white)
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
| `create_move` | `cmd` | Called with the current `user_cmd` |
| `override_view` | `view` | Called with the current camera view setup |
| `frame_stage` | `stage` | Called on frame stage updates |
| `frame_stage_notify` | `stage` | Alias for `frame_stage` |
| `miss` | `miss` | Called when the cheat resolves a shot miss reason |
| `aim_miss` | `miss` | Alias for `miss` |
| `shot_miss` | `miss` | Alias for `miss` |
| `unload` | none | Called before script unload |
| event name | `event` | Called for game event |

```lua
register_callback("draw", function()
    render.text(24, 24, "runtime", color_t(1, 1, 1, 1), 16)
end)
```

```lua
register_callback("create_move", function(cmd)
    if cmd:get_button(input_bit_mask_t.in_use) then
        print("use pressed on command", cmd.command_number)
    end
end)
```

```lua
register_callback("miss", function(miss)
    print("missed due to", miss.reason, "hc", miss.hitchance)
end)
```

The `miss` table contains `reason`, `hitchance`, `backtrack_ticks`, `force_shoot`, `aimpunch`, `tick`, `impact_tick`, `command_number`, `target_index`, `target_handle`, `hitbox`, `target_velocity`, `record_simulation_time`, `record_tick_valid`, `rage_shot`, `processed`, `aim_point`, `aim_angles`, `aim_punch`, `shoot_position`, and `impact_position`.
