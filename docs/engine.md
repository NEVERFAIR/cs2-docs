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

Runs a client command through `client_cmd_unrestricted`.

```lua
engine.client_cmd("setinfo name \"neverfair\"")
```

## get_netvar_offset

```lua
engine.get_netvar_offset(module: string, class_name: string, field_name: string): number | nil
```

Returns a schema offset or `nil`.

```lua
local offset = engine.get_netvar_offset("client.dll", "C_BaseEntity", "m_iHealth")
```
