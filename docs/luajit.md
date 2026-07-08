# LuaJIT

Neverfair embeds LuaJIT 2.1 statically, so users do not need external `lua51.dll` or `luajit.dll` files.

## FFI

```lua
local ffi = require("ffi")
```

The JIT compiler is disabled for stability, but LuaJIT FFI remains available.

## Pointer style

Pointers returned by the API are usually FFI-friendly. Pawn objects also support pointer arithmetic.

```lua
local ffi = require("ffi")
local pawn = entitylist.get_local_player_pawn()
local health_offset = engine.get_netvar_offset("client.dll", "C_BaseEntity", "m_iHealth")

if pawn and health_offset then
    local health = ffi.cast("int*", pawn + health_offset)[0]
    print("health:", health)
end
```

## Compiled scripts

LuaJIT bytecode can be generated with a compatible LuaJIT compiler.

```text
luajit.exe -b script.lua compiled.lua
```
