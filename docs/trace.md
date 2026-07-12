# trace

## ray_t

```lua
ray_t(options: table | nil): ray_t
```

Creates a ray object for shape traces.

```lua
local ray = ray_t()
local box_ray = ray_t({
    mins = { x = -2, y = -2, z = -2 },
    maxs = { x = 2, y = 2, z = 2 }
})
```

See [`ray_t`](types.md#ray_t).

## trace_filter_t

```lua
trace_filter_t(mask: number = MASK_SHOT, layer: number = 4, skip: userdata | boolean | nil): trace_filter_t
```

Creates an engine trace filter. Passing `true` as `skip` skips the local pawn.

See [`trace_filter_t`](types.md#trace_filter_t).

## shape

```lua
trace.shape(ray: ray_t, start: vec3_t, finish: vec3_t, filter: trace_filter_t): trace_t | nil
```

Runs `engine_trace->trace_shape`.

```lua
local forward = math.angle_vectors(g_camera_angles)
local filter = trace_filter_t(0x2800100001, 3, true)
local result = trace.shape(ray_t(), g_camera_origin, g_camera_origin + forward * 10000, filter)
```

Returns [`trace_t`](types.md#trace_t).

## line

```lua
trace.line(start: vec3_t, finish: vec3_t, options: table | nil): trace_t | nil
```

Compatibility helper for a simple line trace. For new scripts prefer [`trace.shape`](#shape).

## fire_bullet

```lua
trace.fire_bullet(start: vec3_t, finish: vec3_t, target: userdata | nil): bullet_trace_t
```

Runs autowall bullet tracing with the local weapon data.

Returns [`bullet_trace_t`](types.md#bullet_trace_t).

## example

```lua
register_callback("draw", function()
    local pawn = entitylist.get_local_player_pawn()
    if pawn == nil then
        return
    end

    local start = pawn:get_bone_position(6)
    local finish = { x = start.x + 256, y = start.y, z = start.z }
    local filter = trace_filter_t(0x1C300B, 4, true)
    local result = trace.shape(ray_t(), start, finish, filter)

    if result and result.hit then
        local screen = render.world_to_screen(result.pos)
        if screen then
            render.circle_filled(screen.x, screen.y, 4, color_t(1, 0.2, 0.2, 1))
        end
    end
end)
```
