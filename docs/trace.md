# trace

## line

```lua
trace.line(start: vector, finish: vector, options: table | nil): table | nil
```

Runs an engine trace from `start` to `finish`.

Options:

| Field | Type | Description |
| --- | --- | --- |
| `mask` | number | Trace mask, defaults to shot mask |
| `layer` | number | Collision layer, defaults to `4` |
| `skip` | userdata | Entity to skip, defaults to local pawn |

Result fields:

| Field | Type | Description |
| --- | --- | --- |
| `hit` | boolean | Trace hit something |
| `fraction` | number | Trace fraction |
| `pos` | vector | Hit position |
| `end_pos` | vector | End position |
| `normal` | vector | Hit normal |
| `entity` | userdata | Hit entity pointer |
| `contents` | number | Contents mask |
| `hitbox` | number | Hitbox id |
| `hitgroup` | number | Hitgroup id |
| `all_solid` | boolean | Trace started or ended inside solid |
| `hit_world` | boolean | Hit world geometry |

## fire_bullet

```lua
trace.fire_bullet(start: vector, finish: vector, target: userdata | nil): table
```

Runs autowall bullet tracing with the local weapon data.

Result fields:

| Field | Type | Description |
| --- | --- | --- |
| `valid` | boolean | Bullet data is valid |
| `damage` | number | Scaled damage |
| `hitgroup` | number | Hitgroup id |
| `hitbox` | number | Hitbox id |
| `penetrated` | boolean | Bullet penetrated material |

## example

```lua
register_callback("draw", function()
    local pawn = entitylist.get_local_player_pawn()
    if pawn == nil then
        return
    end

    local start = pawn:get_bone_position(6)
    local finish = { x = start.x + 256, y = start.y, z = start.z }
    local result = trace.line(start, finish)

    if result and result.hit then
        local screen = render.world_to_screen(result.pos)
        if screen then
            render.circle_filled(screen.x, screen.y, 4, color_t(1, 0.2, 0.2, 1))
        end
    end
end)
```
