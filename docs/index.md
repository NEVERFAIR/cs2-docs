# Home

Neverfair uses LuaJIT for runtime scripts. Scripts can call the Lua API, draw UI elements, read offsets, use FFI, listen to callbacks, and work with game events.

## Loading Lua scripts

1. Drop script into `%APPDATA%\neverfair\scripts`.
2. Open `Configs` -> `Scripts`.
3. Select the script and press `Load`.

## Minimal script

```lua
print("hello from neverfair")
```

## Runtime script

```lua
register_callback("draw", function()
    render.text(24, 24, "neverfair lua", color_t(0.2, 0.75, 1.0, 1.0), 16)
end)
```

## API modules

| Module | Description |
| --- | --- |
| `engine` | Connection state, commands, offset lookup |
| `entitylist` | Local player, entities, controller and pawn helpers |
| `render` / `imgui` | Background draw list primitives |
| `cvars` | Console variables |
| `events` | Game event callbacks through `register_callback` |
| `ffi` | LuaJIT FFI |
