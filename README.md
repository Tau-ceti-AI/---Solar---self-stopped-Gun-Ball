
-- Verificación de identidad del usuario
local allowedUserId = 4188421075 -- Tu UserId de Roblox

if game.Players.LocalPlayer.UserId ~= allowedUserId then
    error("No tienes permiso para usar este script.")
    return
end

-- Información del script y GitHub
-- Script: Tau Ceti (AI) 🚀🤖
-- Canal de YouTube: ☀️--Solar--☀️
-- Más información y actualizaciones: https://github.com/Tau-ceti-AI/Tau-ceti-AI/blob/main/README.md

-- Cargar la biblioteca de interfaz de usuario Orion
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

-- Crear la ventana principal
local Window = OrionLib:MakeWindow({
    Name = "Gun Ball | ☀️--Solar--☀️",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TauCetiConfig"
})

-- Crear la pestaña principal
local Tab = Window:MakeTab({
    Name = "Main",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Variables de configuración
local autoParry = false
local infinityRangeParry = false

-- Función para disparar (maneja los eventos de defensa)
local function shoot()
    if infinityRangeParry then
        local args = {
            [1] = {
                ["success"] = false,
                ["reason"] = "blocked"
            }
        }

        local remoteEvent = game:GetService("ReplicatedStorage").resources.assets.balls.communication.network_remote_event
        remoteEvent:FireServer(unpack(args))
        remoteEvent:FireServer(unpack(args))
    end

    -- Evento de defensa
    game:GetService("ReplicatedStorage").RemoteEvent:FireServer(
        {["name"] = "defense", ["origin"] = "balltargets"},
        {}
    )
end

-- Agregar opciones de configuración (toggles)
Tab:AddToggle({
    Name = "Tau Ceti AutoParry",
    Default = false,
    Callback = function(value)
        autoParry = value
    end
})

Tab:AddToggle({
    Name = "Tau Ceti Infinity Range Parry",
    Default = false,
    Callback = function(value)
        infinityRangeParry = value
    end
})

-- Bucle principal para manejar Auto Parry
task.spawn(function()
    while task.wait() do
        if autoParry then
            task.spawn(shoot)
            task.spawn(shoot)
            task.spawn(shoot)
        end
    end
end)
