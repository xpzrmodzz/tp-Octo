local Players = game:GetService("Players")

-- Fonction pour trouver la position de chaque partie, téléporter le joueur et simuler un clic
local function teleportToParts(player)
    -- Récupérer le personnage du joueur
    local character = player.Character
    if character then
        -- Récupérer l'instance B_OCTO_L0
        local B_OCTO_L0 = game.Workspace.RobotParts:FindFirstChild("B_OCTO_L0")
        if B_OCTO_L0 then
            -- Téléporter le joueur à la position de B_OCTO_L0
            character:SetPrimaryPartCFrame(B_OCTO_L0.CFrame)
            
            -- Téléporter le joueur à chaque partie en passant par les nombres de 0 à 10
            for i = 0, 10 do
                local partName = "B_OCTO_L" .. i
                local part = game.Workspace.RobotParts:FindFirstChild(partName)
                if part then
                    wait(1) -- Attendre 1 seconde entre chaque téléportation (modifiable selon vos besoins)
                    character:SetPrimaryPartCFrame(part.CFrame)
                    
                    -- Vérifier si la partie a un ClickDetector et simuler un clic
                    local clickDetector = part:FindFirstChildOfClass("ClickDetector")
                    if clickDetector then
                        clickDetector:Fire() -- Simuler un clic sur la partie
                    else
                        warn("L'instance " .. partName .. " n'a pas de ClickDetector.")
                    end
                else
                    warn("L'instance " .. partName .. " n'a pas été trouvée.")
                end
            end
        else
            warn("L'instance B_OCTO_L0 n'a pas été trouvée.")
        end
    else
        warn("Le personnage du joueur n'a pas été trouvé.")
    end
    
    -- Téléporter le joueur à workspace.RobotLab.neon après la boucle
    local neon = game.Workspace.RobotLab:FindFirstChild("neon")
    if neon then
        wait(1) -- Attendre 1 seconde avant de se téléporter (modifiable selon vos besoins)
        character:SetPrimaryPartCFrame(neon.CFrame)
    else
        warn("L'instance workspace.RobotLab.neon n'a pas été trouvée.")
    end
end

-- Vous pouvez appeler cette fonction pour téléporter un joueur spécifique
-- Par exemple, pour téléporter le joueur local :
local localPlayer = Players.LocalPlayer
if localPlayer then
    teleportToParts(localPlayer)
else
    warn("Le joueur local n'a pas été trouvé.")
end
