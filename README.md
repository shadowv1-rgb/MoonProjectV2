-- Moon Project Mini 🌑
local player = game.Players.LocalPlayer
local pgui = player:WaitForChild("PlayerGui")

-- Создаем GUI вручную, без лишних наворотов
local sg = Instance.new("ScreenGui", pgui)
sg.Name = "MoonTest"

local frame = Instance.new("Frame", sg)
frame.Size = UDim2.new(0, 200, 0, 200)
frame.Position = UDim2.new(0.5, -100, 0.5, -100)
frame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
frame.Active = true
frame.Draggable = true -- Включаем стандартный драг для теста

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 50)
title.Text = "MOON PROJECT 🌑"
title.TextColor3 = Color3.new(1, 1, 1)
title.BackgroundTransparency = 1

local close = Instance.new("TextButton", frame)
close.Size = UDim2.new(0, 100, 0, 40)
close.Position = UDim2.new(0.5, -50, 0.8, 0)
close.Text = "CLOSE"
close.MouseButton1Click:Connect(function()
    sg:Destroy()
end)

print("Moon Project Test Loaded!")
