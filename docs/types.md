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
| `as_ptr()` | Raw `uint8_t*` |

Pawn supports FFI pointer arithmetic:

```lua
local value = ffi.cast("int*", pawn + offset)[0]
```
