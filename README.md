-- Create the UI
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local TabHolder = Instance.new("Frame")
local MainTab = Instance.new("TextButton")
local WorkspaceTab = Instance.new("TextButton")
local ContentFrame = Instance.new("Frame")
local WorkspaceFrame = Instance.new("Frame")
local PreventionFrame = Instance.new("Frame")
local PublishTab = Instance.new("TextButton")
local LearnTab = Instance.new("TextButton")

-- Elements for "Workspace"
local ScriptBox = Instance.new("TextBox")
local RunButton = Instance.new("TextButton")
local PublishButton = Instance.new("TextButton")

-- Elements for Preventions
local PreventionList = {}
local preventionTypes = {
    "Void Prevention",
    "Fling Prevention",
    "Hacking Prevention",
    "Moving Prevention",
    "Bang Prevention",
    "Saving Prevention",
}

-- Parent to Player GUI
ScreenGui.Name = "UnstoppableUI"
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- MainFrame
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.Size = UDim2.new(0.5, 0, 0.7, 0)
MainFrame.Position = UDim2.new(0.25, 0, 0.15, 0)

-- TabHolder
TabHolder.Name = "TabHolder"
TabHolder.Parent = MainFrame
TabHolder.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
TabHolder.Size = UDim2.new(1, 0, 0.1, 0)

MainTab.Name = "MainTab"
MainTab.Parent = TabHolder
MainTab.Text = "Main"
MainTab.Size = UDim2.new(0.33, 0, 1, 0)
MainTab.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
MainTab.Font = Enum.Font.SourceSansBold
MainTab.TextColor3 = Color3.fromRGB(255, 255, 255)
MainTab.TextSize = 20

WorkspaceTab.Name = "WorkspaceTab"
WorkspaceTab.Parent = TabHolder
WorkspaceTab.Text = "Workspace"
WorkspaceTab.Size = UDim2.new(0.34, 0, 1, 0)
WorkspaceTab.Position = UDim2.new(0.33, 0, 0, 0)
WorkspaceTab.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
WorkspaceTab.Font = Enum.Font.SourceSansBold
WorkspaceTab.TextColor3 = Color3.fromRGB(255, 255, 255)
WorkspaceTab.TextSize = 20

PublishTab.Name = "PublishTab"
PublishTab.Parent = TabHolder
PublishTab.Text = "Published"
PublishTab.Size = UDim2.new(0.33, 0, 1, 0)
PublishTab.Position = UDim2.new(0.67, 0, 0, 0)
PublishTab.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
PublishTab.Font = Enum.Font.SourceSansBold
PublishTab.TextColor3 = Color3.fromRGB(255, 255, 255)
PublishTab.TextSize = 20

-- ContentFrame
ContentFrame.Name = "ContentFrame"
ContentFrame.Parent = MainFrame
ContentFrame.Size = UDim2.new(1, 0, 0.9, 0)
ContentFrame.Position = UDim2.new(0, 0, 0.1, 0)
ContentFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)

-- Workspace Frame
WorkspaceFrame.Name = "WorkspaceFrame"
WorkspaceFrame.Parent = ContentFrame
WorkspaceFrame.Visible = false
WorkspaceFrame.Size = UDim2.new(1, 0, 1, 0)

ScriptBox.Name = "ScriptBox"
ScriptBox.Parent = WorkspaceFrame
ScriptBox.PlaceholderText = "Write your prevention script here..."
ScriptBox.Size = UDim2.new(0.9, 0, 0.2, 0)
ScriptBox.Position = UDim2.new(0.05, 0, 0.1, 0)
ScriptBox.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
ScriptBox.TextColor3 = Color3.fromRGB(255, 255, 255)
ScriptBox.TextSize = 18

RunButton.Name = "RunButton"
RunButton.Parent = WorkspaceFrame
RunButton.Text = "Run"
RunButton.Size = UDim2.new(0.4, 0, 0.1, 0)
RunButton.Position = UDim2.new(0.05, 0, 0.4, 0)
RunButton.BackgroundColor3 = Color3.fromRGB(50, 150, 50)
RunButton.Font = Enum.Font.SourceSansBold
RunButton.TextColor3 = Color3.fromRGB(255, 255, 255)
RunButton.TextSize = 18

PublishButton.Name = "PublishButton"
PublishButton.Parent = WorkspaceFrame
PublishButton.Text = "Publish"
PublishButton.Size = UDim2.new(0.4, 0, 0.1, 0)
PublishButton.Position = UDim2.new(0.55, 0, 0.4, 0)
PublishButton.BackgroundColor3 = Color3.fromRGB(50, 100, 200)
PublishButton.Font = Enum.Font.SourceSansBold
PublishButton.TextColor3 = Color3.fromRGB(255, 255, 255)
PublishButton.TextSize = 18

-- Prevention Frame
PreventionFrame.Name = "PreventionFrame"
PreventionFrame.Parent = ContentFrame
PreventionFrame.Size = UDim2.new(1, 0, 1, 0)
PreventionFrame.Visible = true

-- Dynamically Create Prevention Tabs
for i, preventionName in ipairs(preventionTypes) do
    local PreventionButton = Instance.new("TextButton")
    PreventionButton.Parent = PreventionFrame
    PreventionButton.Text = preventionName
    PreventionButton.Size = UDim2.new(0.9, 0, 0.1, 0)
    PreventionButton.Position = UDim2.new(0.05, 0, 0.1 * (i - 1), 0)
    PreventionButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
    PreventionButton.Font = Enum.Font.SourceSansBold
    PreventionButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    PreventionButton.TextSize = 18

    PreventionButton.MouseButton1Click:Connect(function()
        print("Selected prevention: " .. preventionName)
    end)
end

-- Tab Switching
local function switchTab(tabName)
    ContentFrame:ClearAllChildren()
    if tabName == "Workspace" then
        WorkspaceFrame.Visible = true
        WorkspaceFrame.Parent = ContentFrame
    elseif tabName == "Preventions" then
        PreventionFrame.Visible = true
        PreventionFrame.Parent = ContentFrame
    end
end

WorkspaceTab.MouseButton1Click:Connect(function()
    switchTab("Workspace")
end)

MainTab.MouseButton1Click:Connect(function()
    switchTab("Preventions")
end)-- Functions for each prevention type

local function voidPrevention()
    print("Void Prevention Activated")
    -- Example: Creates infinite platforms in the void
    local voidPlatform = Instance.new("Part")
    voidPlatform.Size = Vector3.new(50, 1, 50)
    voidPlatform.Position = Vector3.new(0, -500, 0)
    voidPlatform.Anchored = true
    voidPlatform.Parent = workspace
    voidPlatform.BrickColor = BrickColor.new("Really black")
end

local function flingPrevention()
    print("Fling Prevention Activated")
    -- Example: Creates a protective angled box around the player
    local character = game.Players.LocalPlayer.Character
    if character then
        local shield = Instance.new("Part")
        shield.Size = Vector3.new(10, 10, 1)
        shield.Position = character.HumanoidRootPart.Position + Vector3.new(0, 5, 0)
        shield.Anchored = true
        shield.Parent = workspace
        shield.BrickColor = BrickColor.new("Bright blue")
    end
end

local function hackingPrevention()
    print("Hacking Prevention Activated")
    -- Example: Teleports exploiters to a jail
    local hackerJail = Instance.new("Part")
    hackerJail.Size = Vector3.new(20, 20, 20)
    hackerJail.Position = Vector3.new(1000, 50, 1000)
    hackerJail.Anchored = true
    hackerJail.Parent = workspace
    hackerJail.BrickColor = BrickColor.new("Bright red")
    hackerJail.Name = "HackerJail"
    print("Jail created for exploiters")
end

local function movingPrevention()
    print("Moving Prevention Activated")
    -- Example: Detects and jails players following you
    local jail = Instance.new("Part")
    jail.Size = Vector3.new(20, 20, 20)
    jail.Position = Vector3.new(500, 50, 500)
    jail.Anchored = true
    jail.Parent = workspace
    jail.BrickColor = BrickColor.new("Bright green")

    local playerPosition = game.Players.LocalPlayer.Character.HumanoidRootPart.Position

    for _, otherPlayer in pairs(game.Players:GetPlayers()) do
        if otherPlayer ~= game.Players.LocalPlayer then
            local distance = (otherPlayer.Character.HumanoidRootPart.Position - playerPosition).Magnitude
            if distance < 10 then
                otherPlayer.Character.HumanoidRootPart.CFrame = jail.CFrame
                print(otherPlayer.Name .. " has been jailed for following.")
            end
        end
    end
end

local function bangPrevention(targetName)
    print("Bang Prevention Activated")
    -- Example: Sends target player to the void
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Name == targetName then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(0, -1000, 0)
            print(player.Name .. " has been sent to the void.")
        end
    end
end

local function savingPrevention()
    print("Saving Prevention Activated")
    -- Example: Teleports you to a safe floating platform
    local safePlatform = Instance.new("Part")
    safePlatform.Size = Vector3.new(50, 1, 50)
    safePlatform.Position = Vector3.new(0, 200, 0)
    safePlatform.Anchored = true
    safePlatform.Parent = workspace
    safePlatform.BrickColor = BrickColor.new("Bright yellow")

    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = safePlatform.CFrame + Vector3.new(0, 3, 0)
end

-- Connect the buttons to their functions
local function connectButtons()
    -- Example for Void Prevention
    RunButton.MouseButton1Click:Connect(function()
        voidPrevention()
    end)

    -- Fling Prevention
    PreventionList["Fling Prevention"] = function()
        flingPrevention()
    end

    -- Hacking Prevention
    PreventionList["Hacking Prevention"] = function()
        hackingPrevention()
    end

    -- Moving Prevention
    PreventionList["Moving Prevention"] = function()
        movingPrevention()
    end

    -- Bang Prevention
    PreventionList["Bang Prevention"] = function()
        local targetName = ScriptBox.Text -- Assumes target name is typed into the ScriptBox
        bangPrevention(targetName)
    end

    -- Saving Prevention
    PreventionList["Saving Prevention"] = function()
        savingPrevention()
    end
end

connectButtons()
