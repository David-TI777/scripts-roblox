local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Interface Setup
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "TeleportMenuGui"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

local Frame = Instance.new("Frame")
Frame.Name = "MainFrame"
Frame.Size = UDim2.new(0, 200, 0, 300)
Frame.Position = UDim2.new(1, -200, 0.5, -150) -- canto direito meio da tela
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
Frame.BorderColor3 = Color3.fromRGB(40, 80, 220)
Frame.BorderSizePixel = 2
Frame.Active = true
Frame.Draggable = true
Frame.Parent = ScreenGui
Frame.ZIndex = 10 -- sempre no topo

local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Size = UDim2.new(1, 0, 0, 30)
Title.BackgroundColor3 = Color3.fromRGB(25, 25, 40)
Title.BorderSizePixel = 0
Title.Text = "Teleport - Selecione um player"
Title.Font = Enum.Font.SourceSansSemibold
Title.TextSize = 18
Title.TextColor3 = Color3.fromRGB(180, 200, 255)
Title.Parent = Frame

local ScrollingFrame = Instance.new("ScrollingFrame")
ScrollingFrame.Name = "PlayerListFrame"
ScrollingFrame.Size = UDim2.new(1, -10, 1, -40)
ScrollingFrame.Position = UDim2.new(0, 5, 0, 35)
ScrollingFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 25)
ScrollingFrame.BorderSizePixel = 0
ScrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
ScrollingFrame.ScrollBarThickness = 6
ScrollingFrame.Parent = Frame
ScrollingFrame.ZIndex = 11

local UIListLayout = Instance.new("UIListLayout")
UIListLayout.Parent = ScrollingFrame
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIListLayout.Padding = UDim.new(0, 3)

local selectedPlayer = nil

local function clearButtons()
	for _, child in ipairs(ScrollingFrame:GetChildren()) do
		if child:IsA("TextButton") then
			child:Destroy()
		end
	end
end

local function refreshPlayerList()
	clearButtons()
	for _, player in ipairs(Players:GetPlayers()) do
		if player ~= LocalPlayer then
			local btn = Instance.new("TextButton")
			btn.Size = UDim2.new(1, -12, 0, 36)
			btn.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
			btn.BorderColor3 = Color3.fromRGB(40, 80, 220)
			btn.BorderSizePixel = 1
			btn.TextColor3 = Color3.fromRGB(220, 220, 255)
			btn.Text = player.Name
			btn.Font = Enum.Font.SourceSansSemibold
			btn.TextSize = 20
			btn.TextWrapped = true
			btn.TextXAlignment = Enum.TextXAlignment.Left
			btn.TextYAlignment = Enum.TextYAlignment.Center
			btn.Parent = ScrollingFrame
			btn.AutoButtonColor = false
			btn.ZIndex = 12

			btn.MouseEnter:Connect(function()
				if selectedPlayer ~= player then
					btn.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
				end
			end)
			btn.MouseLeave:Connect(function()
				if selectedPlayer ~= player then
					btn.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
				end
			end)

			btn.MouseButton1Click:Connect(function()
				selectedPlayer = player
				for _, b in ipairs(ScrollingFrame:GetChildren()) do
					if b:IsA("TextButton") then
						if b.Text == player.Name then
							b.BackgroundColor3 = Color3.fromRGB(60, 90, 220)
							b.TextColor3 = Color3.fromRGB(230, 240, 255)
						else
							b.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
							b.TextColor3 = Color3.fromRGB(180, 200, 255)
						end
					end
				end
			end)
		end
	end
	wait(0.1)
	ScrollingFrame.CanvasSize = UDim2.new(0, 0, 0, UIListLayout.AbsoluteContentSize.Y)
end

refreshPlayerList()

Players.PlayerAdded:Connect(function()
	refreshPlayerList()
end)

Players.PlayerRemoving:Connect(function()
	if selectedPlayer and not Players:FindFirstChild(selectedPlayer.Name) then
		selectedPlayer = nil
	end
	refreshPlayerList()
end)

-- Toggle menu com tecla P
local menuVisible = true
UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if not gameProcessed and input.KeyCode == Enum.KeyCode.P then
		menuVisible = not menuVisible
		Frame.Visible = menuVisible
		if menuVisible then
			refreshPlayerList()
		end
	end
end)

-- Teleport commands :tp e :rp
local function teleportToPlayer(player)
	if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
		LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame + Vector3.new(0, 3, 0)
	end
end

local function teleportToSpawn()
	-- Ajuste conforme o local do spawn no seu mapa
	local spawnLocation = workspace:FindFirstChild("SpawnLocation")
	if spawnLocation and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
		LocalPlayer.Character.HumanoidRootPart.CFrame = spawnLocation.CFrame + Vector3.new(0, 3, 0)
	end
end

LocalPlayer.Chatted:Connect(function(msg)
	if msg:lower() == ":tp" then
		if selectedPlayer then
			teleportToPlayer(selectedPlayer)
		else
			LocalPlayer:Kick("Nenhum player selecionado para teleportar!")
		end
	elseif msg:lower() == ":rp" then
		teleportToSpawn()
	end
end)
