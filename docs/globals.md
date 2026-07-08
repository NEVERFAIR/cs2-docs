# globals

`global_vars` is an alias for `globals`.

## get

```lua
globals.get(name: string): any
```

Supported names:

| Name | Type |
| --- | --- |
| `real_time` | number |
| `frame_count` | number |
| `absolute_frame_time` | number |
| `frame_time` | number |
| `current_time` also `curtime` | number |
| `player_time` | number |
| `tick_count` | number |
| `tick_fraction` | number |
| `client_tick` | number |
| `map_name` | string |
| `map_name_short` | string |

```lua
print("tick:", globals.tick_count)
print("map:", global_vars.map_name_short)
```

## snapshot

```lua
globals.snapshot(): table
```

Returns all global values in one table.

```lua
local vars = globals.snapshot()
print(vars.current_time, vars.frame_time)
```
