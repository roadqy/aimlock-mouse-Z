--[[
    ROAD AIMLOCK
    Coloque no executor (Xeno/Synapse/etc)
    
    ⚠️ Use por sua conta e risco.
]]

-- ==================== PROTEÇÕES ANTI-DETECÇÃO ====================

if game:GetService("CoreGui"):FindFirstChild("RoadAimlock") then
    game:GetService("CoreGui"):FindFirstChild("RoadAimlock"):Destroy()
end

local function RandomString(len)
    local chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
    local str = ""
    for i = 1, len do
        local idx = math.random(1, #chars)
        str = str .. chars:sub(idx, idx)
    end
    return str
end

local RANDOM_NAME = RandomString(12)

local function SafeCall(fn, ...)
    local success, result = pcall(fn, ...)
    if not success then
        return nil
    end
    return result
end

local function AntiInspect()
    pcall(function()
        if getfenv then
            local env = getfenv(1)
            if env and env.script then
                env.script = nil
            end
        end
    end)
end

task.wait(math.random(1, 3) / 10)

-- ==================== CRIA A GUI ====================

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = RANDOM_NAME
ScreenGui.Parent = game:GetService("CoreGui")

pcall(function()
    ScreenGui.Parent = game:GetService("CoreGui")
end)

-- ==================== UI ====================
local function CreateUI()
    local MainPanel = Instance.new("Frame")
    MainPanel.Name = RandomString(8)
    MainPanel.Size = UDim2.new(0, 300, 0, 360)
    MainPanel.Position = UDim2.new(0.5, -150, 0.5, -180)
    MainPanel.AnchorPoint = Vector2.new(0.5, 0.5)
    MainPanel.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
    MainPanel.BackgroundTransparency = 0.05
    MainPanel.ClipsDescendants = true
    MainPanel.Draggable = true
    MainPanel.Active = true
    MainPanel.Parent = ScreenGui
    
    local PanelCorner = Instance.new("UICorner")
    PanelCorner.CornerRadius = UDim.new(0, 12)
    PanelCorner.Parent = MainPanel
    
    local TitleBar = Instance.new("Frame")
    TitleBar.Size = UDim2.new(1, 0, 0, 40)
    TitleBar.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
    TitleBar.BackgroundTransparency = 0.3
    TitleBar.Parent = MainPanel
    
    local TitleCorner = Instance.new("UICorner")
    TitleCorner.CornerRadius = UDim.new(0, 12)
    TitleCorner.Parent = TitleBar
    
    local TitleLabel = Instance.new("TextLabel")
    TitleLabel.Size = UDim2.new(1, -20, 0, 40)
    TitleLabel.Position = UDim2.new(0, 10, 0, 0)
    TitleLabel.BackgroundTransparency = 1
    TitleLabel.Text = "🛣️ Road Aimlock"
    TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    TitleLabel.TextSize = 18
    TitleLabel.Font = Enum.Font.GothamBold
    TitleLabel.TextXAlignment = Enum.TextXAlignment.Left
    TitleLabel.Parent = TitleBar
    
    local CloseButton = Instance.new("TextButton")
    CloseButton.Size = UDim2.new(0, 30, 0, 30)
    CloseButton.Position = UDim2.new(1, -35, 0, 5)
    CloseButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
    CloseButton.Text = "✕"
    CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    CloseButton.TextSize = 16
    CloseButton.Font = Enum.Font.GothamBold
    CloseButton.Parent = TitleBar
    
    local CloseCorner = Instance.new("UICorner")
    CloseCorner.CornerRadius = UDim.new(0, 6)
    CloseCorner.Parent = CloseButton
    
    local Divider = Instance.new("Frame")
    Divider.Size = UDim2.new(1, -20, 0, 2)
    Divider.Position = UDim2.new(0, 10, 0, 45)
    Divider.BackgroundColor3 = Color3.fromRGB(60, 60, 80)
    Divider.BackgroundTransparency = 0.5
    Divider.Parent = MainPanel
    
    local ConfigContainer = Instance.new("Frame")
    ConfigContainer.Size = UDim2.new(1, -20, 0, 190)
    ConfigContainer.Position = UDim2.new(0, 10, 0, 55)
    ConfigContainer.BackgroundTransparency = 1
    ConfigContainer.Parent = MainPanel
    
    local function CreateConfigRow(parent, yPos, labelText, defaultValue)
        local Label = Instance.new("TextLabel")
        Label.Size = UDim2.new(0.55, -5, 0, 28)
        Label.Position = UDim2.new(0, 0, 0, yPos)
        Label.BackgroundTransparency = 1
        Label.Text = labelText
        Label.TextColor3 = Color3.fromRGB(200, 200, 210)
        Label.TextSize = 13
        Label.Font = Enum.Font.Gotham
        Label.TextXAlignment = Enum.TextXAlignment.Left
        Label.Parent = parent
        
        local TextBox = Instance.new("TextBox")
        TextBox.Size = UDim2.new(0.4, 0, 0, 28)
        TextBox.Position = UDim2.new(0.6, 0, 0, yPos)
        TextBox.BackgroundColor3 = Color3.fromRGB(45, 45, 60)
        TextBox.Text = defaultValue
        TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
        TextBox.TextSize = 13
        TextBox.Font = Enum.Font.Gotham
        TextBox.ClearTextOnFocus = false
        TextBox.Parent = parent
        
        local BoxCorner = Instance.new("UICorner")
        BoxCorner.CornerRadius = UDim.new(0, 6)
        BoxCorner.Parent = TextBox
        
        return TextBox
    end
    
    local fovBox = CreateConfigRow(ConfigContainer, 0, "FOV Radius:", "400")
    local smoothBox = CreateConfigRow(ConfigContainer, 38, "Smoothness (0-1):", "0.4")
    local distBox = CreateConfigRow(ConfigContainer, 76, "Max Distance:", "2000")
    local speedBox = CreateConfigRow(ConfigContainer, 114, "Lock Speed:", "20")
    local offsetBox = CreateConfigRow(ConfigContainer, 152, "Aim Offset Y:", "40")
    
    local ButtonContainer = Instance.new("Frame")
    ButtonContainer.Size = UDim2.new(1, -20, 0, 80)
    ButtonContainer.Position = UDim2.new(0, 10, 0, 255)
    ButtonContainer.BackgroundTransparency = 1
    ButtonContainer.Parent = MainPanel
    
    local AimlockButton = Instance.new("TextButton")
    AimlockButton.Size = UDim2.new(1, 0, 0, 40)
    AimlockButton.Position = UDim2.new(0, 0, 0, 0)
    AimlockButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
    AimlockButton.Text = "Aimlock: OFF"
    AimlockButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    AimlockButton.TextSize = 15
    AimlockButton.Font = Enum.Font.GothamBold
    AimlockButton.Parent = ButtonContainer
    
    local AimlockCorner = Instance.new("UICorner")
    AimlockCorner.CornerRadius = UDim.new(0, 8)
    AimlockCorner.Parent = AimlockButton
    
    local InfoLabel = Instance.new("TextLabel")
    InfoLabel.Size = UDim2.new(1, 0, 0, 25)
    InfoLabel.Position = UDim2.new(0, 0, 0, 45)
    InfoLabel.BackgroundTransparency = 1
    -- ✅ TEXTO ATUALIZADO
    InfoLabel.Text = "Z: Toggle | RightShift: Abrir/Fechar"
    InfoLabel.TextColor3 = Color3.fromRGB(150, 150, 170)
    InfoLabel.TextSize = 11
    InfoLabel.Font = Enum.Font.Gotham
    InfoLabel.Parent = ButtonContainer
    
    return {
        MainPanel = MainPanel,
        AimlockButton = AimlockButton,
        CloseButton = CloseButton,
        FOVBox = fovBox,
        SmoothBox = smoothBox,
        DistBox = distBox,
        SpeedBox = speedBox,
        OffsetBox = offsetBox
    }
end

-- ==================== CONFIGURAÇÕES ====================
local Config = {
    FOVSize = 400,
    Smoothness = 0.4,
    MaxDistance = 2000,
    LockSpeed = 20,
    TargetPart = "Head",
    AimOffsetY = 40,
    Enabled = false,
    Active = false
}

local UI = CreateUI()

-- ==================== VARIÁVEIS ====================
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local GuiService = game:GetService("GuiService")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera
local panelVisible = true
local currentConnection = nil
local isTyping = false

-- ==================== FUNÇÕES ====================

local function MoveMouseRelative(dx, dy)
    pcall(function()
        if syn and syn.mousemoverel then
            syn.mousemoverel(dx, dy)
        elseif mousemoverel then
            mousemoverel(dx, dy)
        elseif fluxus and fluxus.mousemoverel then
            fluxus.mousemoverel(dx, dy)
        end
    end)
end

local function GetClosestTargetInFOV()
    local closestTarget = nil
    local closestDistance = math.huge
    
    local character = LocalPlayer.Character
    if not character then return nil end
    
    local rootPart = character:FindFirstChild("HumanoidRootPart")
    if not rootPart then return nil end
    
    local screenCenter = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)
    
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            local targetChar = player.Character
            if targetChar and targetChar:FindFirstChild("Humanoid") and targetChar.Humanoid.Health > 0 then
                local targetRoot = targetChar:FindFirstChild("HumanoidRootPart")
                if targetRoot then
                    local distance3D = (rootPart.Position - targetRoot.Position).Magnitude
                    if distance3D <= Config.MaxDistance then
                        local targetPart = targetChar:FindFirstChild(Config.TargetPart) or targetRoot
                        local screenPos, onScreen = Camera:WorldToScreenPoint(targetPart.Position)
                        
                        if onScreen then
                            local screenVector = Vector2.new(screenPos.X, screenPos.Y) - screenCenter
                            local screenDistance = screenVector.Magnitude
                            
                            if screenDistance <= Config.FOVSize / 2 then
                                if screenDistance < closestDistance then
                                    closestDistance = screenDistance
                                    closestTarget = {
                                        Player = player,
                                        Character = targetChar,
                                        RootPart = targetRoot,
                                        TargetPart = targetPart,
                                        ScreenDistance = screenDistance,
                                        Distance3D = distance3D
                                    }
                                end
                            end
                        end
                    end
                end
            end
        end
    end
    
    return closestTarget
end

local function AimlockLoop()
    if not Config.Enabled then
        Config.Active = false
        return
    end
    
    local target = GetClosestTargetInFOV()
    if not target then
        Config.Active = false
        return
    end
    
    Config.Active = true
    
    local targetScreenPos, onScreen = Camera:WorldToScreenPoint(target.TargetPart.Position)
    if not onScreen then return end
    
    targetScreenPos = Vector2.new(targetScreenPos.X, targetScreenPos.Y + Config.AimOffsetY)
    
    local mouseLocation = UserInputService:GetMouseLocation()
    local topbarOffset = GuiService:GetGuiInset().Y
    
    local dx = targetScreenPos.X - mouseLocation.X
    local dy = targetScreenPos.Y - mouseLocation.Y - topbarOffset
    
    local smoothFactor = 1 - Config.Smoothness
    local speedFactor = Config.LockSpeed / 10
    
    local distance = math.sqrt(dx*dx + dy*dy)
    
    local distanceMultiplier = 1
    if distance > 10 then
        distanceMultiplier = math.min(distance / 10, 15)
    end
    
    local moveX = dx * smoothFactor * speedFactor * distanceMultiplier / 10
    local moveY = dy * smoothFactor * speedFactor * distanceMultiplier / 10
    
    local maxMove = 200
    moveX = math.clamp(moveX, -maxMove, maxMove)
    moveY = math.clamp(moveY, -maxMove, maxMove)
    
    if math.abs(moveX) > 0.1 or math.abs(moveY) > 0.1 then
        MoveMouseRelative(moveX, moveY)
    end
end

local function ToggleAimlock()
    Config.Enabled = not Config.Enabled
    
    if Config.Enabled then
        if not currentConnection then
            currentConnection = RunService.RenderStepped:Connect(AimlockLoop)
        end
        UI.AimlockButton.Text = "Aimlock: ON"
        UI.AimlockButton.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
    else
        if currentConnection then
            currentConnection:Disconnect()
            currentConnection = nil
        end
        UI.AimlockButton.Text = "Aimlock: OFF"
        UI.AimlockButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
        Config.Active = false
    end
end

local function TogglePanel()
    panelVisible = not panelVisible
    UI.MainPanel.Visible = panelVisible
end

-- ==================== EVENTOS ====================
UI.AimlockButton.MouseButton1Click:Connect(ToggleAimlock)
UI.CloseButton.MouseButton1Click:Connect(TogglePanel)

-- ✅ TECLA ALTERADA DE N PARA Z
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if input.KeyCode == Enum.KeyCode.Z and input.UserInputType == Enum.UserInputType.Keyboard then
        if isTyping then return end
        ToggleAimlock()
    end
end)

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if input.KeyCode == Enum.KeyCode.RightShift and input.UserInputType == Enum.UserInputType.Keyboard then
        TogglePanel()
    end
end)

for _, box in pairs({UI.FOVBox, UI.SmoothBox, UI.DistBox, UI.SpeedBox, UI.OffsetBox}) do
    box.Focused:Connect(function()
        isTyping = true
    end)
    box.FocusLost:Connect(function()
        isTyping = false
    end)
end

UI.FOVBox.FocusLost:Connect(function()
    local value = tonumber(UI.FOVBox.Text)
    if value and value > 0 then Config.FOVSize = value
    else UI.FOVBox.Text = tostring(Config.FOVSize) end
end)

UI.SmoothBox.FocusLost:Connect(function()
    local value = tonumber(UI.SmoothBox.Text)
    if value and value >= 0 and value <= 1 then Config.Smoothness = value
    else UI.SmoothBox.Text = tostring(Config.Smoothness) end
end)

UI.DistBox.FocusLost:Connect(function()
    local value = tonumber(UI.DistBox.Text)
    if value and value > 0 then Config.MaxDistance = value
    else UI.DistBox.Text = tostring(Config.MaxDistance) end
end)

UI.SpeedBox.FocusLost:Connect(function()
    local value = tonumber(UI.SpeedBox.Text)
    if value and value > 0 then Config.LockSpeed = value
    else UI.SpeedBox.Text = tostring(Config.LockSpeed) end
end)

UI.OffsetBox.FocusLost:Connect(function()
    local value = tonumber(UI.OffsetBox.Text)
    if value then Config.AimOffsetY = value
    else UI.OffsetBox.Text = tostring(Config.AimOffsetY) end
end)

pcall(function()
    AntiInspect()
end)

print("✅ Road Aimlock carregado!")
print("🖱️ Z = Ativar/Desativar")
print("🔓 Right Shift = Abrir/Fechar painel")
