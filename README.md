game.Players.LocalPlayer.Idled:Connect(function()
    game:GetService("VirtualUser"):CaptureController()
    game:GetService("VirtualUser"):ClickButton2(Vector2.new(0,0))
end)

local Library = {}

function Library:Window(winName,mainColor,hideBind)
    winName = winName or "brought to you by m1kecorp"
    mainColor = mainColor or Color3.fromRGB(104, 186, 227)
    hideBind = hideBind or Enum.KeyCode.RightAlt

    if _G.Library ~= nil then _G.Library:Destroy() end
    
    _G.UISettings = {
        UIBind = hideBind,
        UIConfig = {},
        ElementCache = {},
    }

    local function Tween(which,gui,UDimStuff,time)
        task.spawn(function()
            pcall(function()
                if which == "size" then
                    gui:TweenSize(UDimStuff,Enum.EasingDirection.Out,Enum.EasingStyle.Quad,time)
                elseif which == "pos" then
                    gui:TweenPosition(UDimStuff,Enum.EasingDirection.Out,Enum.EasingStyle.Quad,time)
                else
                    local TweenService = game:GetService("TweenService")
                    TweenService:Create(
                            gui,
                    TweenInfo.new(.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                        UDimStuff
                    ):Play()
                end
            end)
        end)
    end

    local function UpdateFrameSize(scrollframe,listlayout)
        local cS = listlayout.AbsoluteContentSize

        game.TweenService:Create(scrollframe, TweenInfo.new(0.15, Enum.EasingStyle.Linear, Enum.EasingDirection.In), {
            CanvasSize = UDim2.new(0,cS.X,0,cS.Y)
        }):Play()
    end

    local function hidebindConfig()
        local uis = game:GetService("UserInputService")
        uis.InputBegan:Connect(function(input,chat)
            if chat then return end

            if input.KeyCode == hideBind then
                Tabs.ToggleVisiblity()
            end
        end)
    end

    local function dragify(Frame)
    dragToggle = nil
    dragSpeed = .25 -- You can edit this.
    dragInput = nil
    dragStart = nil
    dragPos = nil
    
    function updateInput(input)
    Delta = input.Position - dragStart
    Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + Delta.X, startPos.Y.Scale, startPos.Y.Offset + Delta.Y)
    game:GetService("TweenService"):Create(Frame, TweenInfo.new(.25), {Position = Position}):Play()
    end
    
    Frame.InputBegan:Connect(function(input)
    if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
    dragToggle = true
    dragStart = input.Position
    startPos = Frame.Position
    input.Changed:Connect(function()
    if (input.UserInputState == Enum.UserInputState.End) then
    dragToggle = false
    end
    end)
    end
    end)
    
    Frame.InputChanged:Connect(function(input)
    if (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
    dragInput = input
    end
    end)
    
    game:GetService("UserInputService").InputChanged:Connect(function(input)
    if (input == dragInput and dragToggle) then
    updateInput(input)
    end
    end)
    end

    local function Ripple(obj)... (514 KB left)
