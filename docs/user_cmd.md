# user_cmd

`user_cmd` objects are passed to `register_callback("create_move", function(cmd) ... end)`.

## command_number

```lua
cmd.command_number: number
```

Read-only command sequence number.

## get_button

```lua
cmd:get_button(button: number): boolean
```

Returns whether a button from `input_bit_mask_t` is pressed.

## set_button

```lua
cmd:set_button(button: number)
```

Adds a button to the command.

## remove_button

```lua
cmd:remove_button(button: number)
```

Removes a button from the command.

## get_viewangles

```lua
cmd:get_viewangles(): vector
cmd:get_input_viewangles(): vector
```

Returns the current game input viewangles from `csgo_input`.

## get_command_viewangles

```lua
cmd:get_command_viewangles(): vector
cmd:get_base_viewangles(): vector
```

Returns the command viewangles from `mutable_base`.

## set_viewangles

```lua
cmd:set_viewangles(angles: vector)
```

Writes viewangles into the command `mutable_base`.

## lock_angles

```lua
cmd:lock_angles()
```

Copies command viewangles into the game input view.

## movement

```lua
cmd:get_forward_move(): number
cmd:get_left_move(): number
cmd:set_forward_move(value: number)
cmd:set_left_move(value: number)
cmd:rotate_movement(yaw: number)
```

Movement values are clamped to `-1.0..1.0`. `rotate_movement` rotates movement toward a yaw without changing command viewangles.

## example

```lua
register_callback("create_move", function(cmd)
    if menu.is_open() then
        cmd:remove_button(input_bit_mask_t.in_attack)
    end

    local view = cmd:get_command_viewangles()
    cmd:set_forward_move(1.0)
    cmd:rotate_movement(view.y)
end)
```
