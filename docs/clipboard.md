# clipboard

The `clipboard` module reads and writes Unicode text through the Windows clipboard.

## get

```lua
clipboard.get(): string | nil
```

Returns the current clipboard text as a UTF-8 string. Returns `nil` when the clipboard cannot be opened, does not contain Unicode text, or its data cannot be read.

```lua
local text = clipboard.get()

if text then
	print(text)
end
```

## set

```lua
clipboard.set(text: string): boolean
```

Writes a UTF-8 string to the clipboard as Unicode text. Returns `true` on success and `false` when the clipboard operation fails. A string containing a null byte raises a Lua error.

```lua
if not clipboard.set("neverfair") then
	print("failed to update clipboard")
end
```
