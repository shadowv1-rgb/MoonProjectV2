-- Moon Project 🌑 Optimized for skibX, Delta, Xeno
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local LPlayer = Players.LocalPlayer

-- Ждем загрузки интерфейса игрока
local PlayerGui = LPlayer:WaitForChild("PlayerGui")

-- Удаляем старое меню, если оно уже запущено
if PlayerGui:FindFirstChild("MoonProjectV2") then
    PlayerGui.MoonProjectV2:Destroy()
end

-- Создаем основной контейнер
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MoonProjectV2"
ScreenGui.Parent = PlayerGui
ScreenGui.ResetOnSpawn = false

-- 1. ИКОНКА ЛУНЫ (Кнопка открытия)
local OpenBtn = Instance.new("TextButton")
OpenBtn.Name = "OpenBtn"
OpenBtn.Parent = ScreenGui
OpenBtn.Size = UDim2.new(0, 50, 0, 50)
OpenBtn.Position = UDim2.new(0.1, 0, 0.4, 0)
OpenBtn.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
OpenBtn.Text = "🌑"
OpenBtn.TextSize = 30
OpenBtn.TextColor3 = Color3.new(1, 1, 1)
OpenBtn.ZIndex = 10

local Corner = Instance.new("UICorner", OpenBtn)
Corner.CornerRadius = UDim.new(0, 15)

-- Делаем кнопку перетаскиваемой (Drag) для iOS/Android
local dragging, dragInput, dragStart, startPos
OpenBtn.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = OpenBtn.Position
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        OpenBtn.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)

-- 2. ГЛАВНОЕ МЕНЮ (Квадрат)
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.Size = UDim2.new(0, 260, 0, 220)
MainFrame.Position = UDim2.new(0.5, -130, 0.5, -110)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
MainFrame.BorderSizePixel = 0
MainFrame.Visible = false
MainFrame.ClipsDescendants = true

local MainCorner = Instance.new("UICorner", MainFrame)

-- Звезды и Размытие (Визуальный эффект)
local BgEffect = Instance.new("Frame", MainFrame)
BgEffect.Size = UDim2.new(1, 0, 1, 0)
BgEffect.BackgroundTransparency = 1

for i = 1, 20 do
    local star = Instance.new("Frame", BgEffect)
    star.Size = UDim2.new(0, 2, 0, 2)
    star.Position = UDim2.new(math.random(), 0, math.random(), 0)
    star.BackgroundColor3 = Color3.new(1, 1, 1)
    star.BackgroundTransparency = 0.5
end

-- Заголовок
local Title = Instance.new("TextLabel", MainFrame)
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Text = "moon project 🌑"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 18
Title.BackgroundTransparency = 1

-- Кнопка закрытия (Крестик)
local CloseBtn = Instance.new("TextButton", MainFrame)
CloseBtn.Size = UDim2.new(0, 30, 0, 30)
CloseBtn.Position = UDim2.new(1, -35, 0, 5)
CloseBtn.Text = "✕"
CloseBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 55)
CloseBtn.TextColor3 = Color3.fromRGB(255, 100, 100)
CloseBtn.Font = Enum.Font.GothamBold
Instance.new("UICorner", CloseBtn)

-- Логика кнопок
OpenBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
    OpenBtn.Visible = false
end)

CloseBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
    OpenBtn.Visible = true
end)

print("Moon Project 🌑 успешно запущен на " .. (UserInputService.TouchEnabled and "Mobile" or "PC"))
