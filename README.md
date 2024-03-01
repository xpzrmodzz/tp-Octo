local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Fonction pour envoyer l'événement pour chaque objet B_OCTO_L de 0 à 10
local function sendEvents()
    for i = 0, 10 do
        -- Envoyer l'événement "carry" pour l'objet B_OCTO_L correspondant
        local carryArgs = {
            [1] = "carry",
            [2] = "B_OCTO_L" .. i
        }
        ReplicatedStorage.Events.RobotQuestEvent:FireServer(unpack(carryArgs))
        wait(1) -- Attendre 1 seconde entre chaque envoi d'événement "carry"

        -- Envoyer l'événement "pass" pour l'objet B_OCTO_L correspondant
        local passArgs = {
            [1] = "pass"
        }
        ReplicatedStorage.Events.RobotQuestEvent:FireServer(unpack(passArgs))
        wait(1) -- Attendre 1 seconde entre chaque envoi d'événement "pass"
    end
end

-- Appeler la fonction pour envoyer les événements
sendEvents()
