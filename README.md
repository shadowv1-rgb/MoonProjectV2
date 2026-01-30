-- Moon Project 🌑 V2
local LPlayer = game.Players.LocalPlayer
local PlayerGui = LPlayer:WaitForChild("PlayerGui")

-- Удаляем старое меню, если оно есть
if PlayerGui:FindFirstChild("MoonGui") then
    PlayerGui.MoonGui:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MoonGui"
ScreenGui.Parent = PlayerGui
ScreenGui.ResetOnSpawn = false

-- Иконка луны (Кнопка открытия)
local OpenBtn = Instance.new("ImageButton")
OpenBtn.Name = "OpenBtn"
OpenBtn.Parent = ScreenGui
OpenBtn.Size = UDim2.new(0, 50, 0, 50)
OpenBtn.Position = UDim2.new(0.05, 0, 0.15, 0)
OpenBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
OpenBtn.Image = "rbxassetid://6031080990" -- Картинка луны
OpenBtn.Draggable = true
OpenBtn.Active = true

local Corner = Instance.new("UICorner", OpenBtn)
Corner.CornerRadius = UDim.new(0, 10)

-- Главное окно
local Main = Instance.new("Frame")
Main.Name = "MainFrame"
Main.Parent = ScreenGui
Main.Size = UDim2.new(0, 300, 0, 250)
Main.Position = UDim2.new(0.5, -150, 0.5, -125)
Main.BackgroundColor3 = Color3.fromRGB(10, 10, 15)
Main.Visible = false
Main.BorderSizePixel = 0

local MainCorner = Instance.new("UICorner", Main)

-- Заголовок
local Title = Instance.new("TextLabel", Main)
Title.Size = UDim2.new(1, 0, 0, 45)
Title.Text = "moon project 🌑"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 20
Title.BackgroundTransparency = 1

-- Кнопка закрытия
local Close = Instance.new("TextButton", Main)
Close.Size = UDim2.new(0, 30, 0, 30)
Close.Position = UDim2.new(1, -35, 0, 7)
Close.Text = "✕"
Close.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
Close.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", Close)

-- Функционал
OpenBtn.MouseButton1Click:Connect(function()
    Main.Visible = not Main.Visible
    OpenBtn.Visible = not Main.Visible
end)

Close.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

print("Moon Project 🌑 Loaded!")
