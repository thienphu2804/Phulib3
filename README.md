--// PhuLib Final Pro by Phú
local PhuLib = {}

function PhuLib:Win(title)
    local sg = Instance.new("ScreenGui", game:GetService("CoreGui"))
    sg.Name = "PhuLib_UI"

    local frame = Instance.new("Frame", sg)
    frame.Size = UDim2.new(0, 420, 0, 300)
    frame.Position = UDim2.new(0.5, -210, 0.5, -150)
    frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    frame.BorderSizePixel = 0
    frame.Active = true frame.Draggable = true
    frame.ClipsDescendants = true
    frame.Name = "MainFrame"

    local uicorner = Instance.new("UICorner", frame)
    uicorner.CornerRadius = UDim.new(0, 10)

    local shadow = Instance.new("ImageLabel", frame)
    shadow.Size = UDim2.new(1, 60, 1, 60)
    shadow.Position = UDim2.new(0, -30, 0, -30)
    shadow.BackgroundTransparency = 1
    shadow.Image = "rbxassetid://5028857084"
    shadow.ImageColor3 = Color3.fromRGB(0,0,0)
    shadow.ImageTransparency = 0.4
    shadow.ScaleType = Enum.ScaleType.Slice
    shadow.SliceCenter = Rect.new(24,24,276,276)

    local titleBar = Instance.new("Frame", frame)
    titleBar.Size = UDim2.new(1, 0, 0, 35)
    titleBar.BackgroundColor3 = Color3.fromRGB(45,45,45)
    Instance.new("UICorner", titleBar).CornerRadius = UDim.new(0,10)

    local tl = Instance.new("TextLabel", titleBar)
    tl.Size = UDim2.new(1, -35, 1, 0)
    tl.Position = UDim2.new(0, 10, 0, 0)
    tl.BackgroundTransparency = 1
    tl.Text = title
    tl.TextColor3 = Color3.fromRGB(255,255,255)
    tl.Font = Enum.Font.GothamBold
    tl.TextSize = 18
    tl.TextXAlignment = Enum.TextXAlignment.Left

    -- Minimize Button
    local mini = Instance.new("TextButton", titleBar)
    mini.Size = UDim2.new(0, 25, 0, 25)
    mini.Position = UDim2.new(1, -30, 0.5, -12)
    mini.BackgroundColor3 = Color3.fromRGB(70,70,70)
    mini.Text = "-"
    mini.TextColor3 = Color3.fromRGB(255,255,255)
    mini.Font = Enum.Font.GothamBold
    mini.TextSize = 20
    Instance.new("UICorner", mini).CornerRadius = UDim.new(0,6)

    local cont = Instance.new("Frame", frame)
    cont.Size = UDim2.new(1, -15, 1, -45)
    cont.Position = UDim2.new(0, 7, 0, 40)
    cont.BackgroundTransparency = 1

    local layout = Instance.new("UIListLayout", cont)
    layout.Padding = UDim.new(0,5)

    -- Minimize logic
    local minimized = false
    mini.MouseButton1Click:Connect(function()
        minimized = not minimized
        if minimized then
            frame:TweenSize(UDim2.new(0,420,0,35), "Out", "Quad", 0.3, true)
        else
            frame:TweenSize(UDim2.new(0,420,0,300), "Out", "Quad", 0.3, true)
        end
    end)

    local win = {}
    function win:Tab(name)
        local tab = {}

        function tab:Btn(txt, cb)
            local b = Instance.new("TextButton", cont)
            b.Size = UDim2.new(1,0,0,30)
            b.BackgroundColor3 = Color3.fromRGB(55,55,55)
            b.Text = txt
            b.TextColor3 = Color3.fromRGB(255,255,255)
            b.Font = Enum.Font.GothamBold
            b.TextSize = 16
            Instance.new("UICorner", b).CornerRadius = UDim.new(0,6)
            b.MouseButton1Click:Connect(cb)
        end

        function tab:Tog(txt, state, cb)
            local b = Instance.new("TextButton", cont)
            b.Size = UDim2.new(1,0,0,30)
            b.BackgroundColor3 = Color3.fromRGB(55,55,55)
            b.Text = txt.." : "..tostring(state)
            b.TextColor3 = Color3.fromRGB(255,255,255)
            b.Font = Enum.Font.GothamBold
            b.TextSize = 16
            Instance.new("UICorner", b).CornerRadius = UDim.new(0,6)
            b.MouseButton1Click:Connect(function()
                state = not state
                b.Text = txt.." : "..tostring(state)
                cb(state)
            end)
        end

        function tab:Sld(txt, min, max, cb)
            local val = min
            local slider = Instance.new("TextButton", cont)
            slider.Size = UDim2.new(1,0,0,30)
            slider.BackgroundColor3 = Color3.fromRGB(55,55,55)
            slider.Text = txt..": "..val
            slider.TextColor3 = Color3.fromRGB(255,255,255)
            slider.Font = Enum.Font.GothamBold
            slider.TextSize = 16
            Instance.new("UICorner", slider).CornerRadius = UDim.new(0,6)
            slider.MouseButton1Click:Connect(function()
                val = (val + 1 > max) and min or val + 1
                slider.Text = txt..": "..val
                cb(val)
            end)
        end

        return tab
    end

    return win
end

return PhuLib
