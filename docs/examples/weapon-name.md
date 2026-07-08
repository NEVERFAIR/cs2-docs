# Clantag based on weapon name

This script changes player name to include active weapon name.

```lua
local last_set_name = ""
local last_update_time = 0
local update_delay = 0.35

local function normalize_weapon_name(name)
    if name == nil or name == "" then
        return nil
    end

    name = tostring(name)
    name = name:gsub("^weapon_", "")
    name = name:gsub("^item_", "")
    name = name:gsub("_", " ")

    if name == "" then
        return nil
    end

    return name
end

local function quote_cmd(value)
    value = tostring(value or "")
    value = value:gsub("\\", "\\\\")
    value = value:gsub("\"", "'")
    return "\"" .. value .. "\""
end

local function set_name(value)
    if value == nil or value == "" or value == last_set_name then
        return
    end

    last_set_name = value
    engine.client_cmd("setinfo name " .. quote_cmd(value))
end

register_callback("draw", function()
    if not engine.is_connected() or not engine.is_in_game() then
        return
    end

    local now = os.clock()
    if now - last_update_time < update_delay then
        return
    end

    last_update_time = now

    local pawn = entitylist.get_local_player_pawn()
    local player_name = entitylist.get_local_player_name()

    if pawn == nil or player_name == nil or player_name == "" then
        return
    end

    local weapon_name = normalize_weapon_name(pawn:get_weapon_name())
    if weapon_name == nil then
        return
    end

    set_name("[" .. weapon_name .. "] " .. player_name)
end)

register_callback("unload", function()
    if not engine.is_connected() or not engine.is_in_game() then
        return
    end

    local player_name = entitylist.get_local_player_name()
    if player_name ~= nil and player_name ~= "" then
        engine.client_cmd("setinfo name " .. quote_cmd(player_name))
    end
end)
```
