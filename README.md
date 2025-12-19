--[[ 
    CHEAP HUB - VERSÃO FINALIZADA
    ID Brookhaven: 4924922222
    Créditos: @cattenak
]]

repeat task.wait() until game:IsLoaded()

local TeleportService = game:GetService("TeleportService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local MarketplaceService = game:GetService("MarketplaceService")
local Players = game:GetService("Players")
local lp = Players.LocalPlayer

-- IDs DEFINIDOS POR VOCÊ
local MEU_ID_MAPA = 121187380014929 
local BROOK_ID = 4924922222 

local IDS = {
    ["VIP"] = 1636719609,
    ["Premium"] = 1636799690,
    ["Houses"] = 1637139769
}

-- Limpar Interface Antiga
if game:GetService("CoreGui"):FindFirstChild("CheapHubCattenak") then
    game:GetService("CoreGui").CheapHubCattenak:Destroy()
end

-- Criando a Interface
local ScreenGui = Instance.new("ScreenGui", game:GetService("CoreGui"))
ScreenGui.Name = "CheapHubCattenak"

local Main = Instance.new("Frame", ScreenGui)
Main.Size = UDim2.new(0, 300, 0, 350)
Main.Position = UDim2.new(0.5, -150, 0.5, -150)
Main.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Main.Active = true
Main.Draggable = true
Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 15)

local Title = Instance.new("TextLabel", Main)
Title.Size = UDim2.new(1, 0, 0, 60)
Title.BackgroundTransparency = 1
Title.Text = "CHEAP GAMEPASS"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.LuckiestGuy
Title.TextSize = 28

-- Função de Ação (Ir para o Mapa ou Acionar Gatilho)
local function ProcessarClique(id)
    if game.PlaceId == MEU_ID_MAPA or game.GameId == MEU_ID_MAPA then
        local Gatilho = ReplicatedStorage:FindFirstChild("GatilhoCompra")
        if Gatilho then
            Gatilho.Value = tostring(id)
        else
            Title.Text = "ERRO: SEM GATILHO"
            Title.TextColor3 = Color3.fromRGB(255, 0, 0)
            task.wait(2)
            Title.Text = "CHEAP GAMEPASS"
            Title.TextColor3 = Color3.fromRGB(255, 255, 255)
        end
    else
        Title.Text = "TELEPORTANDO..."
        TeleportService:Teleport(MEU_ID_MAPA, lp)
    end
end

-- Criar os Botões (VIP, Premium, Houses)
local function CriarBtn(nome, cor, pos, gpID)
    local btn = Instance.new("TextButton", Main)
    btn.Size = UDim2.new(0.8, 0, 0, 55)
    btn.Position = pos
    btn.BackgroundColor3 = cor
    btn.Text = "CHEAP " .. nome:upper()
    btn.Font = Enum.Font.LuckiestGuy
    btn.TextSize = 22
    btn.TextColor3 = Color3.fromRGB(0, 0, 0)
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 10)
    
    btn.MouseButton1Click:Connect(function()
        ProcessarClique(gpID)
    end)
end

CriarBtn("VIP", Color3.fromRGB(255, 255, 0), UDim2.new(0.1, 0, 0.22, 0), IDS["VIP"])
CriarBtn("Premium", Color3.fromRGB(0, 255, 255), UDim2.new(0.1, 0, 0.42, 0), IDS["Premium"])
CriarBtn("Houses", Color3.fromRGB(0, 255, 0), UDim2.new(0.1, 0, 0.62, 0), IDS["Houses"])

-- CRÉDITOS (A parte que você pediu)
local Credits = Instance.new("TextLabel", Main)
Credits.Size = UDim2.new(1, 0, 0, 40)
Credits.Position = UDim2.new(0, 0, 0.85, 0)
Credits.BackgroundTransparency = 1
Credits.Text = "by @cattenak"
Credits.TextColor3 = Color3.fromRGB(255, 255, 255)
Credits.Font = Enum.Font.LuckiestGuy
Credits.TextSize = 18
