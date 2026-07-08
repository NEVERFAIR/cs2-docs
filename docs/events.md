# events

Game events are registered with `register_callback`.

```lua
register_callback("player_hurt", function(event)
    print(event:get_name())
end)
```

## event:get_name

```lua
event:get_name(): string
```

## event:get_bool

```lua
event:get_bool(name: string): boolean
```

## event:get_int

```lua
event:get_int(name: string): number
```

## event:get_float

```lua
event:get_float(name: string): number
```

## event:get_string

```lua
event:get_string(name: string): string
```

## event:get_controller

```lua
event:get_controller(name: string): uint8_t* | nil
```

Returns player controller from event field.

```lua
register_callback("player_hurt", function(event)
    local attacker = event:get_controller("attacker")
    local target = event:get_controller("userid")

    if attacker == nil or target == nil then
        return
    end
end)
```

## Any event

```lua
register_callback("game_event", function(event)
    print("event:", event:get_name())
end)
```
