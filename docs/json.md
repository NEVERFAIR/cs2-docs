# json

The `json` module converts between JSON text and Lua values.

| JSON value | Lua value |
| --- | --- |
| object | table |
| array | table with 1-based integer keys |
| string | string |
| number | number |
| boolean | boolean |
| null | `json.null` |

## encode

```lua
json.encode(value: any, pretty: boolean = false): string
```

Encodes a Lua value as JSON. When `pretty` is `true`, the result uses four-space indentation.

Tables with contiguous integer keys starting at `1` are encoded as arrays. Other tables are encoded as objects and must only have string keys. Empty unmarked tables are encoded as objects.

```lua
local payload = {
	name = "neverfair",
	enabled = true,
	weapons = { "ak47", "deagle" },
	optional = json.null
}

local compact = json.encode(payload)
local pretty = json.encode(payload, true)
```

Encoding raises a Lua error for recursive tables, non-finite numbers, unsupported value types, object tables with non-string keys, and forced arrays with missing or invalid indexes.

## decode

```lua
json.decode(data: string): any
```

Parses JSON text and returns the corresponding Lua value. JSON arrays use 1-based indexes, and JSON `null` values become `json.null`. Invalid JSON raises a Lua error.

```lua
local payload = json.decode('{"name":"neverfair","values":[10,20],"optional":null}')

print(payload.name)
print(payload.values[1])

if payload.optional == json.null then
	print("optional is null")
end
```

Decoded arrays and objects preserve their JSON container type when encoded again, including empty containers.

## array

```lua
json.array(value: table | nil = nil): table
```

Creates an empty table marked as a JSON array, or marks and returns the supplied table. A marked array must contain contiguous integer keys starting at `1`.

```lua
local empty_array = json.array()
local values = json.array({ "first", "second" })

print(json.encode(empty_array))
print(json.encode(values))
```

## object

```lua
json.object(value: table | nil = nil): table
```

Creates an empty table marked as a JSON object, or marks and returns the supplied table. Object keys must be strings.

```lua
local empty_object = json.object()
local settings = json.object({ enabled = true })

print(json.encode(empty_object))
print(json.encode(settings))
```

## null

```lua
json.null: userdata
```

Represents a JSON `null` value. Use it when a null must be retained inside a table, since assigning Lua `nil` removes the table entry.

```lua
local payload = json.array({ 1, json.null, 3 })
local encoded = json.encode(payload)
```
