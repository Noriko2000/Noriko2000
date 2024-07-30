-- Lua script for searching and teleporting to bots in Roblox

local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")

local player = Players.LocalPlayer

-- Function to find bots by name
local function findBotByName(botName)
    local foundBots = {}
    
    for _, instance in pairs(Workspace:GetDescendants()) do
        if instance:IsA("Model") and instance.Name == botName and instance:FindFirstChild("HumanoidRootPart") then
            table.insert(foundBots, instance)
        end
    end
    
    return foundBots
end

-- Function to teleport to a bot
local function teleportToBot(bot)
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        player.Character.HumanoidRootPart.CFrame = bot.HumanoidRootPart.CFrame
    end
end

-- Create GUI for bot search
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "BotFinderUI"

local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0, 250, 0, 300)
frame.Position = UDim2.new(0, 10, 0, 10)
frame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
frame.BorderSizePixel = 0
frame.BackgroundTransparency = 0.3

local searchButton = Instance.new("TextButton", frame)
searchButton.Size = UDim2.new(0, 200, 0, 50)
searchButton.Position = UDim2.new(0, 25, 0, 10)
searchButton.Text = "Search Bot"
searchButton.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
searchButton.TextColor3 = Color3.new(1, 1, 1)
searchButton.TextScaled = true

local botNameInput = Instance.new("TextBox", frame)
botNameInput.Size = UDim2.new(0, 200, 0, 50)
botNameInput.Position = UDim2.new(0, 25, 0, 70)
botNameInput.Text = "Enter Bot Name"
botNameInput.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
botNameInput.TextColor3 = Color3.new(1, 1, 1)
botNameInput.TextScaled = true
botNameInput.ClearTextOnFocus = true

local resultLabel = Instance.new("TextLabel", frame)
resultLabel.Size = UDim2.new(0, 200, 0, 120)
resultLabel.Position = UDim2.new(0, 25, 0, 130)
resultLabel.Text = "Results will be displayed here."
resultLabel.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
resultLabel.TextColor3 = Color3.new(1, 1, 1)
resultLabel.TextScaled = true
resultLabel.TextWrapped = true

local teleportButton = Instance.new("TextButton", frame)
teleportButton.Size = UDim2.new(0, 200, 0, 50)
teleportButton.Position = UDim2.new(0, 25, 0, 260)
teleportButton.Text = "Teleport to Bot"
teleportButton.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
teleportButton.TextColor3 = Color3.new(1, 1, 1)
teleportButton.TextScaled = true
teleportButton.Visible = false

local foundBots = {}

-- Function to be called when the search button is clicked
searchButton.MouseButton1Click:Connect(function()
    local botName = botNameInput.Text
    foundBots = findBotByName(botName)
    
    if #foundBots > 0 then
        local resultText = "Found Bots:\n"
        for _, bot in pairs(foundBots) do
            resultText = result
