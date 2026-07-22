# menu

## is_open

```lua
menu.is_open(): boolean
```

Returns whether the Neverfair menu is currently open.

## get_pos

```lua
menu.get_pos(): table
```

Returns menu position as `{ x = number, y = number }`.

## get_size

```lua
menu.get_size(): table
```

Returns DPI-normalized menu size as `{ x = width, y = height }`. Use this value as `w/h` for render functions.

## get_rect

```lua
menu.get_rect(): table
```

Returns menu bounds:

| Field | Description |
| --- | --- |
| `x` | Left edge in screen pixels |
| `y` | Top edge in screen pixels |
| `z` | Right edge in screen pixels |
| `w` | Bottom edge in screen pixels |
| `width` | DPI-normalized width for render functions |
| `height` | DPI-normalized height for render functions |
| `pixel_width` | Raw pixel width |
| `pixel_height` | Raw pixel height |

```lua
local rect = menu.get_rect()
render.rect_filled(rect.x, rect.y, rect.width, rect.height, color_t(0, 0, 0, 0.5))
```

## get_binds

```lua
menu.get_binds(): table
binds.get_all(): table
```

Both functions return the same bind list.

Each bind entry contains:

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | Bind name |
| `value` | boolean, number | Bound value |
| `preview` | string | Display-ready value |
| `key` | number | Virtual key code |
| `key_name` | string | Display key name |
| `mode` | string | `hold`, `toggle`, or `always_on` |
| `active` | boolean | Current bind state |
| `visible` | boolean | Whether bind is shown in active list |
| `type` | string | `boolean`, `integer`, `float`, `combo`, or `multi_selection` |
| `owner` | string | `none`, `rage`, or `legit` |
| `index` | number | Bind slot index |

```lua
register_callback("draw", function()
    local y = 120

    for _, bind in ipairs(binds.get_all()) do
        if bind.active and bind.visible then
            render.text(24, y, bind.name .. ": " .. bind.preview .. " [" .. bind.mode .. "]", color_t(1, 1, 1, 1), 13, render.fonts.verdana)
            y = y + 16
        end
    end
end)
```

## notify

```lua
menu.notify(text: string, color: color | nil)
```

Sends a Neverfair devlog notification.

```lua
menu.notify("script loaded", color_t(0.2, 0.75, 1.0, 1.0))
```

## get_username

```lua
menu.get_username(): string
```

Returns the current Neverfair username.

## get_cheat_name

```lua
menu.get_cheat_name(): string
```

Returns the current cheat name.

## create_tab

```lua
menu.create_tab(label: string): menu_tab
```

Creates a script-owned tab in the Neverfair menu. The tab and all of its elements are removed automatically when the script is unloaded or reloaded.

Values, colors, multi-selection states, and all bind slots belonging to Lua menu elements are stored in Neverfair configs. During config loading, scripts are loaded first and their menu state is restored afterward.

## menu_tab:add_groupbox

```lua
tab:add_groupbox(label: string, x: number | nil, y: number | nil, width: number | nil, height: number | nil): menu_groupbox
```

Adds a groupbox to the tab. `x` and `y` are relative to the beginning of the tab content. Position and size values are DPI-normalized. The default width is `295`; a height of `0` enables automatic height. When the position is omitted, groupboxes use the automatic two-column layout.

## add_checkbox

```lua
container:add_checkbox(label: string, default_value: boolean, bindable: boolean, popup_width: number | nil, popup_height: number | nil): menu_checkbox
```

`default_value` sets the initial checkbox value. `bindable` enables the Neverfair bind editor. Passing a positive `popup_width` creates a settings popup; the returned checkbox then accepts every `add_*` method listed below.

## add_combo

```lua
container:add_combo(label: string, default_index: number, bindable: boolean, items: table, popup_width: number | nil, popup_height: number | nil): menu_combo
```

Creates a zero-based combo. Passing a positive popup width creates a settings popup and makes the returned combo an element container.

## add_color_checkbox

```lua
container:add_color_checkbox(label: string, default_value: boolean, bindable: boolean, r: number, g: number, b: number, a: number): menu_checkbox
```

Creates the checkbox and color-picker

## add_color_combo

```lua
container:add_color_combo(label: string, default_index: number, bindable: boolean, items: table, r: number, g: number, b: number, a: number): menu_combo
```

Creates the combo and color-picker

## add_multi

```lua
container:add_multi(label: string, items: table, bindable: boolean): menu_multi
```

Creates a multi-selection box. Its getter and setter use one-based item indices. Set `bindable` to `true` to enable the bind popup.

## add_color

```lua
container:add_color(label: string, r: number, g: number, b: number, a: number): menu_color
```

Creates a label with the Neverfair color picker. Components use the `0.0` to `1.0` range.

## add_int_slider

```lua
container:add_int_slider(label: string, default_value: number, minimum: number, maximum: number, step: number, bindable: boolean): menu_int_slider
```

## add_float_slider

```lua
container:add_float_slider(label: string, default_value: number, minimum: number, maximum: number, step: number, bindable: boolean): menu_float_slider
```

## add_label

```lua
container:add_label(label: string)
```

## add_separator

```lua
container:add_separator(thickness: number, padding: number)
```

`container` can be a groupbox, a popup checkbox, or a popup combo. Elements are rendered in creation order.

## Element methods

```lua
checkbox:get_value(): boolean
checkbox:get_base_value(): boolean
checkbox:set_value(value: boolean)
checkbox:get_bind(): boolean
checkbox:get_color(): table
checkbox:set_color(r: number, g: number, b: number, a: number | nil)

combo:get_value(): number
combo:set_value(index: number)
combo:get_bind(): boolean
combo:get_color(): table
combo:set_color(r: number, g: number, b: number, a: number | nil)

multi:get_value(index: number): boolean
multi:set_value(index: number, value: boolean)
multi:get_bind(): boolean

color:get_value(): table
color:set_value(r: number, g: number, b: number, a: number | nil)

int_slider:get_value(): number
int_slider:set_value(value: number)
int_slider:get_bind(): boolean

float_slider:get_value(): number
float_slider:set_value(value: number)
float_slider:get_bind(): boolean
```

`get_value()` returns the effective value after the active bind is applied. `get_base_value()` returns the stored checkbox state without bind overrides. `get_bind()` returns whether one of the checkbox binds is currently active and returns `false` for a non-bindable checkbox.

```lua
local tab = menu.create_tab("Example")
local general = tab:add_groupbox("General", 0, 0, 295, 0)
local advanced = tab:add_groupbox("Advanced", 305, 0, 295, 180)
local enabled = general:add_checkbox("Enabled", false, true)
local mode = general:add_combo("Mode", 0, true, { "Default", "Fast", "Safe" })
local targets = general:add_multi("Targets", { "Players", "World", "Effects" })
local accent = general:add_color("Accent", 0.35, 0.65, 1.0, 1.0)
local amount = general:add_int_slider("Amount", 25, 0, 100, 1, true)
local scale = general:add_float_slider("Scale", 1.0, 0.1, 2.0, 0.05, false)
local colored_toggle = general:add_color_checkbox("Colored toggle", false, true, 0.2, 0.8, 1.0, 1.0)
local colored_mode = general:add_color_combo("Colored mode", 0, false, { "One", "Two" }, 1.0, 0.4, 0.2, 1.0)

local popup_checkbox = advanced:add_checkbox("Advanced settings", true, true, 230, 0)
popup_checkbox:add_int_slider("Limit", 10, 1, 64, 1, false)
popup_checkbox:add_color("Highlight", 1.0, 0.3, 0.2, 1.0)

local popup_combo = advanced:add_combo("Profile", 0, false, { "A", "B" }, 230, 0)
popup_combo:add_checkbox("Profile option", false, false)
popup_combo:add_separator(1, 0)
popup_combo:add_label("Profile settings")

register_callback("draw", function()
    if enabled:get_value() then
        render.text(24, 120, "Lua checkbox is enabled", color_t(1, 1, 1, 1), 13)
    end

    if enabled:get_bind() then
        render.text(24, 138, "Checkbox bind is active", color_t(0.4, 0.8, 1, 1), 13)
    end
end)
```

## example

```lua
register_callback("draw", function()
    local rect = menu.get_rect()
    local text = menu.get_cheat_name() .. " / " .. menu.get_username()
    render.text(rect.x + 16, rect.y + 16, text, color_t(1, 1, 1, 1), 14)
end)
```
