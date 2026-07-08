# netvars

Schema offsets can be requested through `engine.get_netvar_offset`.

```lua
local health_offset = engine.get_netvar_offset("client.dll", "C_BaseEntity", "m_iHealth")
```

## Reading health

```lua
local ffi = require("ffi")
local pawn = entitylist.get_local_player_pawn()
local health_offset = engine.get_netvar_offset("client.dll", "C_BaseEntity", "m_iHealth")

if pawn and health_offset then
    local health = ffi.cast("int*", pawn + health_offset)[0]
    print("health:", health)
end
```

## Reading velocity

```lua
local ffi = require("ffi")
local pawn = entitylist.get_local_player_pawn()
local velocity_offset = engine.get_netvar_offset("client.dll", "C_BaseEntity", "m_vecVelocity")

if pawn and velocity_offset then
    local velocity = ffi.cast("float*", pawn + velocity_offset)
    local speed = math.sqrt(velocity[0] * velocity[0] + velocity[1] * velocity[1] + velocity[2] * velocity[2])
    print("speed:", math.floor(speed + 0.5))
end
```
