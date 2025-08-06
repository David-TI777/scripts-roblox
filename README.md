local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer
local mouse = player:GetMouse()
local camera = workspace.CurrentCamera

-- GUI principal
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TeleportDarkGui"
screenGui.Parent = player:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false

local mainFrame = Instance.new("Frame")
mainFrame.AnchorPoint = Vector2.new(0,0)
mainFrame.Position = UDim2.new(0, 18, 0, 18)
mainFrame.Size = UDim2.new(0, 430, 0, 520)
mainFrame.BackgroundColor3 = Color3.fromRGB(18, 18, 28)
mainFrame.BackgroundTransparency = 0.32
mainFrame.BorderSizePixel = 0
mainFrame.Parent = screenGui
mainFrame.Active = true
mainFrame.Draggable = true

local titleLabel = Instance.new("TextLabel")
titleLabel.Position = UDim2.new(0, 12, 0, 10)
titleLabel.Size = UDim2.new(1, -24, 0, 35)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "TELEPORTE E OPÇÕES"
titleLabel.Font = Enum.Font.GothamBold
titleLabel.TextSize = 27
titleLabel.TextColor3 = Color3.fromRGB(235, 235, 255)
titleLabel.TextStrokeTransparency = 0.7
titleLabel.TextXAlignment = Enum.TextXAlignment.Left
titleLabel.Parent = mainFrame

local descLabel = Instance.new("TextLabel")
descLabel.Position = UDim2.new(0, 12, 0, 47)
descLabel.Size = UDim2.new(1, -24, 0, 22)
descLabel.BackgroundTransparency = 1
descLabel.Text = "Aperte Z para teleportar até onde o mouse aponta."
descLabel.Font = Enum.Font.Gotham
descLabel.TextSize = 17
descLabel.TextColor3 = Color3.fromRGB(180, 180, 220)
descLabel.TextStrokeTransparency = 0.8
descLabel.TextXAlignment = Enum.TextXAlignment.Left
descLabel.Parent = mainFrame

local hintLabel = Instance.new("TextLabel")
hintLabel.Position = UDim2.new(0, 12, 0, 72)
hintLabel.Size = UDim2.new(1, -24, 0, 20)
hintLabel.BackgroundTransparency = 1
hintLabel.Text = "Pressione M para ocultar/mostrar. Arraste para mover."
hintLabel.Font = Enum.Font.Gotham
hintLabel.TextSize = 15
hintLabel.TextColor3 = Color3.fromRGB(120, 120, 180)
hintLabel.TextStrokeTransparency = 0.85
hintLabel.TextXAlignment = Enum.TextXAlignment.Left
hintLabel.Parent = mainFrame

-- Infinite Jump
local infJumpLabel = Instance.new("TextLabel")
infJumpLabel.Position = UDim2.new(0, 12, 0, 102)
infJumpLabel.Size = UDim2.new(0, 110, 0, 28)
infJumpLabel.BackgroundTransparency = 1
infJumpLabel.Text = "Pulo Infinito:"
infJumpLabel.Font = Enum.Font.Gotham
infJumpLabel.TextSize = 18
infJumpLabel.TextColor3 = Color3.fromRGB(200, 255, 200)
infJumpLabel.TextStrokeTransparency = 0.7
infJumpLabel.TextXAlignment = Enum.TextXAlignment.Left
infJumpLabel.Parent = mainFrame

local infJumpButton = Instance.new("TextButton")
infJumpButton.Position = UDim2.new(0, 120, 0, 103)
infJumpButton.Size = UDim2.new(0, 80, 0, 26)
infJumpButton.BackgroundColor3 = Color3.fromRGB(40, 170, 60)
infJumpButton.BackgroundTransparency = 0.2
infJumpButton.BorderSizePixel = 0
infJumpButton.Text = "LIGADO"
infJumpButton.TextColor3 = Color3.fromRGB(245, 255, 245)
infJumpButton.Font = Enum.Font.GothamBold
infJumpButton.TextSize = 16
infJumpButton.Parent = mainFrame

-- Fly
local flyLabel = Instance.new("TextLabel")
flyLabel.Position = UDim2.new(0, 220, 0, 102)
flyLabel.Size = UDim2.new(0, 50, 0, 28)
flyLabel.BackgroundTransparency = 1
flyLabel.Text = "Voo:"
flyLabel.Font = Enum.Font.Gotham
flyLabel.TextSize = 18
flyLabel.TextColor3 = Color3.fromRGB(200, 200, 255)
flyLabel.TextStrokeTransparency = 0.7
flyLabel.TextXAlignment = Enum.TextXAlignment.Left
flyLabel.Parent = mainFrame

local flyButton = Instance.new("TextButton")
flyButton.Position = UDim2.new(0, 265, 0, 103)
flyButton.Size = UDim2.new(0, 80, 0, 26)
flyButton.BackgroundColor3 = Color3.fromRGB(40, 120, 200)
flyButton.BackgroundTransparency = 0.2
flyButton.BorderSizePixel = 0
flyButton.Text = "DESLIGADO"
flyButton.TextColor3 = Color3.fromRGB(225, 235, 255)
flyButton.Font = Enum.Font.GothamBold
flyButton.TextSize = 16
flyButton.Parent = mainFrame

-- Aimbot
local aimbotLabel = Instance.new("TextLabel")
aimbotLabel.Position = UDim2.new(0, 12, 0, 136)
aimbotLabel.Size = UDim2.new(0, 80, 0, 28)
aimbotLabel.BackgroundTransparency = 1
aimbotLabel.Text = "Aimbot:"
aimbotLabel.Font = Enum.Font.Gotham
aimbotLabel.TextSize = 18
aimbotLabel.TextColor3 = Color3.fromRGB(255, 255, 200)
aimbotLabel.TextStrokeTransparency = 0.7
aimbotLabel.TextXAlignment = Enum.TextXAlignment.Left
aimbotLabel.Parent = mainFrame

local aimbotButton = Instance.new("TextButton")
aimbotButton.Position = UDim2.new(0, 90, 0, 137)
aimbotButton.Size = UDim2.new(0, 80, 0, 26)
aimbotButton.BackgroundColor3 = Color3.fromRGB(120,120,40)
aimbotButton.BackgroundTransparency = 0.2
aimbotButton.BorderSizePixel = 0
aimbotButton.Text = "DESLIGADO"
aimbotButton.TextColor3 = Color3.fromRGB(255, 255, 220)
aimbotButton.Font = Enum.Font.GothamBold
aimbotButton.TextSize = 16
aimbotButton.Parent = mainFrame

local aimbotIntensityLabel = Instance.new("TextLabel")
aimbotIntensityLabel.Position = UDim2.new(0, 180, 0, 136)
aimbotIntensityLabel.Size = UDim2.new(0, 75, 0, 28)
aimbotIntensityLabel.BackgroundTransparency = 1
aimbotIntensityLabel.Text = "Intensidade:"
aimbotIntensityLabel.Font = Enum.Font.Gotham
aimbotIntensityLabel.TextSize = 16
aimbotIntensityLabel.TextColor3 = Color3.fromRGB(240,240,180)
aimbotIntensityLabel.TextStrokeTransparency = 0.8
aimbotIntensityLabel.TextXAlignment = Enum.TextXAlignment.Left
aimbotIntensityLabel.Parent = mainFrame

local aimbotSliderFrame = Instance.new("Frame")
aimbotSliderFrame.Position = UDim2.new(0, 260, 0, 143)
aimbotSliderFrame.Size = UDim2.new(0, 130, 0, 12)
aimbotSliderFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 30)
aimbotSliderFrame.BackgroundTransparency = 0.2
aimbotSliderFrame.BorderSizePixel = 0
aimbotSliderFrame.Parent = mainFrame

local aimbotSliderBar = Instance.new("Frame")
aimbotSliderBar.Position = UDim2.new(0, 0, 0, 0)
aimbotSliderBar.Size = UDim2.new(0.5, 0, 1, 0)
aimbotSliderBar.BackgroundColor3 = Color3.fromRGB(180, 200, 80)
aimbotSliderBar.BorderSizePixel = 0
aimbotSliderBar.Parent = aimbotSliderFrame

local aimbotSliderBtn = Instance.new("Frame")
aimbotSliderBtn.Position = UDim2.new(0.5, -5, 0, -2)
aimbotSliderBtn.Size = UDim2.new(0, 14, 0, 16)
aimbotSliderBtn.BackgroundColor3 = Color3.fromRGB(220, 220, 90)
aimbotSliderBtn.BorderSizePixel = 0
aimbotSliderBtn.Parent = aimbotSliderFrame
aimbotSliderBtn.ZIndex = 2

local aimbotIntensityValue = 0.5
local draggingAimbotSlider = false

local function updateAimbotSlider(posX)
    local x = math.clamp(posX - aimbotSliderFrame.AbsolutePosition.X, 0, aimbotSliderFrame.AbsoluteSize.X)
    local percent = x / aimbotSliderFrame.AbsoluteSize.X
    aimbotIntensityValue = percent
    aimbotSliderBar.Size = UDim2.new(percent, 0, 1, 0)
    aimbotSliderBtn.Position = UDim2.new(percent, -5, 0, -2)
end

aimbotSliderFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        draggingAimbotSlider = true
        updateAimbotSlider(input.Position.X)
    end
end)
aimbotSliderFrame.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        draggingAimbotSlider = false
    end
end)
UIS.InputChanged:Connect(function(input)
    if draggingAimbotSlider and input.UserInputType == Enum.UserInputType.MouseMovement then
        updateAimbotSlider(input.Position.X)
    end
end)

-- Infinite Jump
local isInfJumpOn = true
local infJumpConn
local function setInfJump(state)
    isInfJumpOn = state
    if infJumpConn then infJumpConn:Disconnect(); infJumpConn = nil end
    if isInfJumpOn then
        infJumpButton.Text = "LIGADO"
        infJumpButton.BackgroundColor3 = Color3.fromRGB(40, 170, 60)
        infJumpConn = UIS.JumpRequest:Connect(function()
            local character = player.Character
            if character and character:FindFirstChildOfClass("Humanoid") then
                character:FindFirstChildOfClass("Humanoid"):ChangeState(Enum.HumanoidStateType.Jumping)
            end
        end)
    else
        infJumpButton.Text = "DESLIGADO"
        infJumpButton.BackgroundColor3 = Color3.fromRGB(120, 30, 30)
    end
end
setInfJump(true)
infJumpButton.MouseButton1Click:Connect(function() setInfJump(not isInfJumpOn) end)

-- Fly controls
local isFlying = false
local flyConn, velocityObj, gyroObj
local function startFlying()
    local character = player.Character; if not character then return end
    local hrp = character:FindFirstChild("HumanoidRootPart"); if not hrp then return end
    if velocityObj then velocityObj:Destroy(); end
    if gyroObj then gyroObj:Destroy(); end
    velocityObj = Instance.new("BodyVelocity")
    velocityObj.MaxForce = Vector3.new(1,1,1)*1e5
    velocityObj.Velocity = Vector3.new(0,0,0)
    velocityObj.Parent = hrp
    gyroObj = Instance.new("BodyGyro")
    gyroObj.MaxTorque = Vector3.new(1,1,1)*1e5
    gyroObj.CFrame = hrp.CFrame
    gyroObj.Parent = hrp
    flyConn = RunService.RenderStepped:Connect(function()
        if not isFlying then return end
        local dir = Vector3.new()
        local camCF = workspace.CurrentCamera.CFrame
        if UIS:IsKeyDown(Enum.KeyCode.W) then dir += camCF.LookVector end
        if UIS:IsKeyDown(Enum.KeyCode.S) then dir -= camCF.LookVector end
        if UIS:IsKeyDown(Enum.KeyCode.A) then dir -= camCF.RightVector end
        if UIS:IsKeyDown(Enum.KeyCode.D) then dir += camCF.RightVector end
        if UIS:IsKeyDown(Enum.KeyCode.Space) then dir += Vector3.new(0,1,0) end
        if UIS:IsKeyDown(Enum.KeyCode.LeftControl) or UIS:IsKeyDown(Enum.KeyCode.LeftShift) then dir -= Vector3.new(0,1,0) end
        if dir.Magnitude > 0 then dir = dir.Unit end
        velocityObj.Velocity = dir * 60
        gyroObj.CFrame = camCF
    end)
end

local function stopFlying()
    if flyConn then flyConn:Disconnect(); flyConn = nil end
    if velocityObj then velocityObj:Destroy(); velocityObj = nil end
    if gyroObj then gyroObj:Destroy(); gyroObj = nil end
end

local function setFlying(state)
    isFlying = state
    if state then
        flyButton.Text = "LIGADO"
        flyButton.BackgroundColor3 = Color3.fromRGB(40, 170, 60)
        startFlying()
    else
        flyButton.Text = "DESLIGADO"
        flyButton.BackgroundColor3 = Color3.fromRGB(40, 120, 200)
        stopFlying()
    end
end

setFlying(false)
flyButton.MouseButton1Click:Connect(function() setFlying(not isFlying) end)
player.CharacterAdded:Connect(function() setFlying(false) end)

-- Aimbot logic
local isAimbotOn = false
local aimbotConn, isAimbotPressing = nil, false

local function getClosestTarget()
    local best, bestDist = nil, math.huge
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= player and p.Character and p.Character:FindFirstChild("HumanoidRootPart") and p.Character:FindFirstChildOfClass("Humanoid").Health > 0 then
            local pos, onScreen = camera:WorldToViewportPoint(p.Character.HumanoidRootPart.Position)
            if onScreen then
                local dist = (Vector2.new(pos.X,pos.Y) - Vector2.new(mouse.X, mouse.Y)).Magnitude
                if dist < bestDist then best, bestDist = p, dist end
            end
        end
    end
    return best
end

local function setAimbot(state)
    isAimbotOn = state
    if aimbotConn then aimbotConn:Disconnect(); aimbotConn = nil end
    if state then
        aimbotButton.Text = "LIGADO"
        aimbotButton.BackgroundColor3 = Color3.fromRGB(40, 170, 60)
        aimbotConn = RunService.RenderStepped:Connect(function()
            if isAimbotPressing then
                local target = getClosestTarget()
                if target then
                    local camPos = camera.CFrame.Position
                    local targetPos = target.Character.HumanoidRootPart.Position
                    local dir = (targetPos - camPos).Unit
                    local newLook = camera.CFrame.LookVector:Lerp(dir, aimbotIntensityValue)
                    camera.CFrame = CFrame.new(camPos, camPos + newLook)
                end
            end
        end)
    else
        aimbotButton.Text  = "DESLIGADO"
        aimbotButton.BackgroundColor3 = Color3.fromRGB(120,120,40)
    end
end

setAimbot(false)
aimbotButton.MouseButton1Click:Connect(function() setAimbot(not isAimbotOn) end)
UIS.InputBegan:Connect(function(input, gpe)
    if gpe then return end
    if isAimbotOn and input.UserInputType == Enum.UserInputType.MouseButton1 then
        isAimbotPressing = true
    end
    if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.M then
        mainFrame.Visible = not mainFrame.Visible
    end
    if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.Z then
        local character = player.Character or player.CharacterAdded:Wait()
        local hrp = character:FindFirstChild("HumanoidRootPart")
        if hrp and mouse then
            local pos = mouse.Hit.Position
            hrp.CFrame = CFrame.new(pos, pos + hrp.CFrame.LookVector)
            local humanoid = character:FindFirstChildOfClass("Humanoid")
            if humanoid then
                humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
            end
        end
    end
end)
UIS.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        isAimbotPressing = false
    end
end)

-- Teleporte para outro jogador + pulo
local playersLabel = Instance.new("TextLabel")
playersLabel.Position = UDim2.new(0, 12, 0, 225)
playersLabel.Size = UDim2.new(1, -24, 0, 22)
playersLabel.BackgroundTransparency = 1
playersLabel.Text = "Teleportar para outro jogador:"
playersLabel.Font = Enum.Font.Gotham
playersLabel.TextSize = 17
playersLabel.TextColor3 = Color3.fromRGB(180, 180, 220)
playersLabel.TextStrokeTransparency = 0.8
playersLabel.TextXAlignment = Enum.TextXAlignment.Left
playersLabel.Parent = mainFrame

local playersFrame = Instance.new("ScrollingFrame")
playersFrame.Position = UDim2.new(0, 12, 0, 250)
playersFrame.Size = UDim2.new(1, -24, 0, 150)
playersFrame.BackgroundTransparency = 0.3
playersFrame.BackgroundColor3 = Color3.fromRGB(25,25,40)
playersFrame.BorderSizePixel = 0
playersFrame.ScrollBarThickness = 6
playersFrame.CanvasSize = UDim2.new(0,0,0,0)
playersFrame.Parent = mainFrame

local UIListLayout = Instance.new("UIListLayout")
UIListLayout.Parent = playersFrame
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIListLayout.Padding = UDim.new(0,6)

local function teleportToPlayer(p)
    if p and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
        local char = player.Character or player.CharacterAdded:Wait()
        local hrp = char:FindFirstChild("HumanoidRootPart")
        if hrp then
            local targetPos = p.Character.HumanoidRootPart.Position + Vector3.new(2,0,2)
            hrp.CFrame = CFrame.new(targetPos, targetPos + hrp.CFrame.LookVector)
            local humanoid = char:FindFirstChildOfClass("Humanoid")
            if humanoid then humanoid:ChangeState(Enum.HumanoidStateType.Jumping) end
        end
    end
end

local function updatePlayersList()
    for _, child in ipairs(playersFrame:GetChildren()) do
        if child:IsA("TextButton") then child:Destroy() end
    end
    local count = 0
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= player then
            count = count + 1
            local btn = Instance.new("TextButton")
            btn.Size = UDim2.new(1,-8,0,28)
            btn.BackgroundColor3 = Color3.fromRGB(35,35,55)
            btn.BackgroundTransparency = 0.15
            btn.Text = p.DisplayName.." ("..p.Name..")"
            btn.TextColor3 = Color3.fromRGB(225,225,245)
            btn.Font = Enum.Font.Gotham
            btn.TextSize = 17
            btn.Parent = playersFrame
            btn.AutoButtonColor = true
            btn.MouseButton1Click:Connect(function() teleportToPlayer(p) end)
        end
    end
    playersFrame.CanvasSize = UDim2.new(0,0,0, math.max(0, count*34))
end

updatePlayersList()
Players.PlayerAdded:Connect(updatePlayersList)
Players.PlayerRemoving:Connect(updatePlayersList)

-- Chat commands
local function onChatted(msg)
    local lower = string.lower(msg)
    if lower:sub(1,1)==":" then
        local args = {}
        for w in string.gmatch(lower, "%S+") do table.insert(args, w) end
        local cmd = args[1]:sub(2)
        if cmd=="fly" then setFlying(true)
        elseif cmd=="unfly" then setFlying(false)
        elseif cmd=="infjump" then setInfJump(true)
        elseif cmd=="noinfjump" or cmd=="uninfjump" then setInfJump(false)
        elseif cmd=="aimbot" then setAimbot(true)
        elseif cmd=="noaimbot" or cmd=="unaimbot" then setAimbot(false)
        elseif cmd=="gui" then mainFrame.Visible = not mainFrame.Visible
        elseif cmd=="tp" and args[2] then
            for _, p in ipairs(Players:GetPlayers()) do
                if string.lower(p.Name)==args[2] or string.lower(p.DisplayName)==args[2] then
                    teleportToPlayer(p)
                    break
                end
            end
        elseif cmd=="intensidade" and args[2] then
            local v=tonumber(args[2])
            if v and v>=0 and v<=1 then
                aimbotIntensityValue=v
                aimbotSliderBar.Size = UDim2.new(v,0,1,0)
                aimbotSliderBtn.Position = UDim2.new(v,-5,0,-2)
            end
        end
    end
end

player.Chatted:Connect(onChatted)
local TextChatService = game:GetService("TextChatService")
if TextChatService and TextChatService.OnIncomingMessage then
    TextChatService.OnIncomingMessage:Connect(function(m)
        if m.TextSource and m.TextSource.UserId==player.UserId then
            onChatted(m.Text)
        end
    end)
end

player.AncestryChanged:Connect(function(_, parent)
    if not parent then
        if infJumpConn then infJumpConn:Disconnect() end
        stopFlying()
        if aimbotConn then aimbotConn:Disconnect() end
    end
end)

