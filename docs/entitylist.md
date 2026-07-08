# entitylist

## get_local_player_pawn

```lua
entitylist.get_local_player_pawn(): pawn | nil
```

Returns local pawn wrapper or `nil`.

```lua
local pawn = entitylist.get_local_player_pawn()
if not pawn then
    return
end
```

## pawn:get_weapon_name

```lua
pawn:get_weapon_name(): string | nil
```

Returns active weapon name.

```lua
local weapon_name = pawn:get_weapon_name()
print("weapon:", weapon_name)
```

## pawn:get_weapon_id

```lua
pawn:get_weapon_id(): number | nil
```

Returns active weapon definition index.

```lua
local weapon_id = pawn:get_weapon_id()
print("weapon id:", weapon_id)
```

## pawn:get_bone_position

```lua
pawn:get_bone_position(index: number): table | nil
```

Returns bone world position as `{ x = number, y = number, z = number }`.

```lua
local head = pawn:get_bone_position(6)
if head then
    local screen = render.world_to_screen(head.x, head.y, head.z)
end
```

## pawn:get_hitbox_position

```lua
pawn:get_hitbox_position(index: number): table | nil
```

Returns hitbox world position as `{ x = number, y = number, z = number }`.

## pawn:as_ptr

```lua
pawn:as_ptr(): uint8_t*
```

Returns raw FFI pointer.

```lua
local ptr = pawn:as_ptr()
```

## get_local_player_controller

```lua
entitylist.get_local_player_controller(): uint8_t* | nil
```

Returns local controller pointer or `nil`.

## get_local_player_name

```lua
entitylist.get_local_player_name(): string | nil
```

Returns local sanitized player name.

## get_local_weapon

```lua
entitylist.get_local_weapon(): uint8_t* | nil
```

Returns local active weapon pointer.

## get_local_weapon_name

```lua
entitylist.get_local_weapon_name(): string | nil
```

Returns local active weapon name.

## get_local_weapon_index

```lua
entitylist.get_local_weapon_index(): number | nil
```

Returns local active weapon definition index.

## get

```lua
entitylist.get(class_name: string): table
```

Returns entities by class name.

```lua
local players = entitylist.get("cs_player_controller")
for i = 1, #players do
    print(players[i])
end
```
