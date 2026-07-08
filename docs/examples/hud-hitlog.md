# HUD + hitlog

```lua
local ffi = require("ffi")

local accent = color_t(0.2, 0.75, 1.0, 1.0)
local white = color_t(1, 1, 1, 1)
local red = color_t(1, 0.25, 0.25, 1)
local green = color_t(0.35, 1, 0.45, 1)
local dark = color_t(0.03, 0.03, 0.04, 0.72)
local logs = {}

local offsets = {
    health = engine.get_netvar_offset("client.dll", "C_BaseEntity", "m_iHealth"),
    velocity = engine.get_netvar_offset("client.dll", "C_BaseEntity", "m_vecVelocity"),
    name = engine.get_netvar_offset("client.dll", "CCSPlayerController", "m_sSanitizedPlayerName")
}

local hitgroups = { [0] = "generic", [1] = "head", [2] = "chest", [3] = "stomach", [4] = "left arm", [5] = "right arm", [6] = "left leg", [7] = "right leg", [10] = "gear" }

local function read_name(controller)
    if controller == nil or offsets.name == nil then
        return "unknown"
    end

    local ptr = ffi.cast("char**", controller + offsets.name)[0]
    if ptr == nil then
        return "unknown"
    end

    return ffi.string(ptr)
end

local function get_health()
    local pawn = entitylist.get_local_player_pawn()
    if pawn == nil or offsets.health == nil then
        return 0
    end

    return ffi.cast("int*", pawn + offsets.health)[0]
end

local function get_velocity()
    local pawn = entitylist.get_local_player_pawn()
    if pawn == nil or offsets.velocity == nil then
        return 0
    end

    local vel = ffi.cast("float*", pawn + offsets.velocity)
    local speed = math.sqrt(vel[0] * vel[0] + vel[1] * vel[1] + vel[2] * vel[2])
    return math.floor(speed + 0.5)
end

local function add_log(parts)
    table.insert(logs, 1, { parts = parts, time = os.clock() })
    while #logs > 8 do
        table.remove(logs)
    end
end

register_callback("player_hurt", function(event)
    local local_controller = entitylist.get_local_player_controller()
    local target = event:get_controller("userid")
    local attacker = event:get_controller("attacker")

    if local_controller == nil or target == nil or attacker == nil then
        return
    end

    local damage = event:get_int("dmg_health")
    if damage <= 0 then
        return
    end

    local remaining = event:get_int("health")
    local hitgroup = hitgroups[event:get_int("hitgroup")] or "generic"

    if attacker == local_controller then
        local target_name = read_name(target)
        add_log({ { text = "Hit ", color = white }, { text = target_name .. " ", color = accent }, { text = "for ", color = white }, { text = damage .. " ", color = accent }, { text = "in the ", color = white }, { text = hitgroup .. " ", color = accent }, { text = "(" .. remaining .. " hp)", color = white } })
    elseif target == local_controller then
        local attacker_name = read_name(attacker)
        add_log({ { text = "Harmed by ", color = white }, { text = attacker_name .. " ", color = red }, { text = "for ", color = white }, { text = damage .. " ", color = red }, { text = "in the ", color = white }, { text = hitgroup .. " ", color = red }, { text = "(" .. remaining .. " hp)", color = white } })
    end
end)

register_callback("draw", function()
    local hp = get_health()
    local speed = get_velocity()
    local x = 24
    local y = 80
    local w = 235
    local h = 76

    imgui.rect_filled(x, y, w, h, dark, 7)
    imgui.rect(x, y, w, h, accent, 1, 7)
    imgui.text(x + 12, y + 10, "neverfair lua hud", accent, 16)

    local hp_color = hp > 65 and green or hp > 30 and accent or red
    imgui.text(x + 12, y + 34, "health: " .. hp, hp_color, 14)
    imgui.text(x + 12, y + 52, "velocity: " .. speed, white, 14)

    local bar_w = math.max(0, math.min(1, hp / 100)) * (w - 24)
    imgui.rect_filled(x + 12, y + h - 9, w - 24, 3, color_t(0, 0, 0, 0.55), 2)
    imgui.rect_filled(x + 12, y + h - 9, bar_w, 3, hp_color, 2)

    local now = os.clock()
    for i = #logs, 1, -1 do
        local log = logs[i]
        local age = now - log.time

        if age > 5.0 then
            table.remove(logs, i)
        else
            local alpha = age > 4.2 and (1.0 - ((age - 4.2) / 0.8)) or 1.0
            local cursor_x = 24
            local row_y = 170 + (i - 1) * 20

            imgui.rect_filled(18, row_y - 3, 520, 18, color_t(0.02, 0.02, 0.025, 0.48 * alpha), 4)

            for _, part in ipairs(log.parts) do
                local c = part.color
                imgui.text(cursor_x, row_y, part.text, color_t(c.r, c.g, c.b, c.a * alpha), 14)
                cursor_x = cursor_x + (#part.text * 7)
            end
        end
    end
end)

print("neverfair lua: hud + hitlog loaded")
```
