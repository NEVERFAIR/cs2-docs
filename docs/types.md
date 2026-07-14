# types

## color_t

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

## vec2_t

Screen positions returned by `render.get_screen_size` and `render.world_to_screen`.

| Field | Type |
| --- | --- |
| `x` | number |
| `y` | number |

## vec3_t

World position, direction vector, or angle-like three-component table.

| Field | Type |
| --- | --- |
| `x` | number |
| `y` | number |
| `z` | number |

## angle_t

Angle table. Uses the same shape as [`vec3_t`](#vec3_t).

| Field | Type |
| --- | --- |
| `x` | number |
| `y` | number |
| `z` | number |

## ray_t

Ray object created by `ray_t()`.

| Field | Type | Description |
| --- | --- | --- |
| `start` | [`vec3_t`](#vec3_t) | Start point |
| `end` | [`vec3_t`](#vec3_t) | End point |
| `mins` | [`vec3_t`](#vec3_t) | Shape minimum bounds |
| `maxs` | [`vec3_t`](#vec3_t) | Shape maximum bounds |
| `type` | number | Ray type |

## trace_filter_t

Trace filter object created by `trace_filter_t(mask, layer, skip)`.

| Field | Type | Description |
| --- | --- | --- |
| `mask` | number | Trace mask |
| `layer` | number | Collision layer |

## trace_t

Trace result returned by `trace.shape`, `trace.line`, and `engine.trace_shape`.

| Field | Type | Description |
| --- | --- | --- |
| `hit` | boolean | Trace hit something |
| `fraction` | number | Trace fraction |
| `pos` | [`vec3_t`](#vec3_t) | Hit position |
| `end_pos` | [`vec3_t`](#vec3_t) | End position |
| `normal` | [`vec3_t`](#vec3_t) | Hit normal |
| `entity` | userdata | Hit entity pointer |
| `contents` | number | Contents mask |
| `hitbox` | number | Hitbox id |
| `hitgroup` | number | Hitgroup id |
| `all_solid` | boolean | Trace started or ended inside solid |
| `hit_world` | boolean | Hit world geometry |

## bullet_trace_t

Bullet trace result returned by `trace.fire_bullet` and `engine.trace_bullet`.

| Field | Type | Description |
| --- | --- | --- |
| `valid` | boolean | Bullet data is valid |
| `damage` | number | Scaled damage |
| `hitgroup` | number | Hitgroup id |
| `hitbox` | number | Hitbox id |
| `penetrated` | boolean | Bullet penetrated material |

## image_t

Texture object returned by `render.setup_texture`, `render.setup_texture_rgba`, `render.setup_texture_from_memory`, and `render.create_panorama_svg_texture`.

| Method | Returns | Description |
| --- | --- | --- |
| `get_size()` | [`vec2_t`](#vec2_t) | Texture size |

## pawn_t

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
| `get_eye_pos()` | Eye position, using prediction data for the local pawn |
| `is_scoped()` | Scoped state, using prediction data for the local pawn |
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
