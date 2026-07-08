# types

## color

Color is a Lua table created by `color_t`.

```lua
local white = color_t(1, 1, 1, 1)
local accent = color_t(0.2, 0.75, 1.0, 1.0)
```

Fields:

| Field | Type |
| --- | --- |
| `r` | number |
| `g` | number |
| `b` | number |
| `a` | number |

## vec2

Screen positions returned by `render.get_screen_size` and `render.world_to_screen`.

| Field | Type |
| --- | --- |
| `x` | number |
| `y` | number |

## pawn

Pawn wrapper returned by `entitylist.get_local_player_pawn`.

```lua
local pawn = entitylist.get_local_player_pawn()
```

Methods:

| Method | Description |
| --- | --- |
| `get_weapon_name()` | Active weapon name |
| `get_weapon_id()` | Active weapon definition index |
| `get_bone_position(index)` | Bone world position |
| `get_hitbox_position(index)` | Hitbox world position |
| `as_ptr()` | Raw `uint8_t*` |

Pawn supports FFI pointer arithmetic:

```lua
local value = ffi.cast("int*", pawn + offset)[0]
```

## input_bit_mask_t

Button bit masks used by `user_cmd`.

| Name | Description |
| --- | --- |
| `in_attack` | Primary attack |
| `in_attack2` | Secondary attack |
| `in_jump` | Jump |
| `in_duck` | Duck |
| `in_forward` | Move forward |
| `in_back` | Move backward |
| `in_moveleft` | Move left |
| `in_moveright` | Move right |
| `in_use` | Use |
| `in_reload` | Reload |
| `in_speed` | Walk |
| `in_score` | Scoreboard |
| `in_zoom` | Zoom |

```lua
register_callback("create_move", function(cmd)
    if cmd:get_button(input_bit_mask_t.in_jump) then
        menu.notify("jump")
    end
end)
```
