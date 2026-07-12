# engine

## is_connected

```lua
engine.is_connected(): boolean
```

Returns whether the engine is connected.

## is_in_game

```lua
engine.is_in_game(): boolean
```

Returns whether the client is currently in game.

```lua
if not engine.is_connected() or not engine.is_in_game() then
    return
end
```

## client_cmd

```lua
engine.client_cmd(cmd: string)
```

Runs a client command.

```lua
engine.client_cmd("setinfo name \"neverfair\"")
```

## get_netvar_offset

```lua
engine.get_netvar_offset(module: string, class_name: string, field_name: string): number | nil
```

Returns an offset or `nil`.

```lua
local offset = engine.get_netvar_offset("client.dll", "C_BaseEntity", "m_iHealth")
```

## camera_in_thirdperson

```lua
engine.camera_in_thirdperson(): boolean
```

Returns whether the local camera is currently in thirdperson.

## trace_shape

```lua
engine.trace_shape(ray: ray_t, start: vec3_t, finish: vec3_t, filter: trace_filter_t): trace_t | nil
```

Runs `engine_trace->trace_shape`.

```lua
local forward = math.angle_vectors(g_camera_angles)
local filter = trace_filter_t(0x2800100001, 3, true)
local result = engine.trace_shape(ray_t(), g_camera_origin, g_camera_origin + forward * 10000, filter)
```

See [`ray_t`](types.md#ray_t), [`trace_filter_t`](types.md#trace_filter_t), and [`trace_t`](types.md#trace_t).

## trace_bullet

```lua
engine.trace_bullet(start: vec3_t, finish: vec3_t, target: userdata | nil): bullet_trace_t
```

Runs bullet tracing with the local weapon data.

See [`bullet_trace_t`](types.md#bullet_trace_t).
