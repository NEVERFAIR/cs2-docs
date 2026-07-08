# cvars

Console variables are available through the `cvars` table.

```lua
print("Current sensitivity:", cvars.sensitivity:get_float())
```

## get_bool

```lua
cvars.name:get_bool(): boolean
```

## get_int

```lua
cvars.name:get_int(): number
```

## get_float

```lua
cvars.name:get_float(): number
```

## get_string

```lua
cvars.name:get_string(): string
```

## set_bool

```lua
cvars.name:set_bool(value: boolean)
```

## set_int

```lua
cvars.name:set_int(value: number)
```

## set_float

```lua
cvars.name:set_float(value: number)
```

## Example

```lua
local sensitivity = cvars.sensitivity

if sensitivity then
    print("sensitivity:", sensitivity:get_float())
end
```
