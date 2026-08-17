local player=game.Players.LocalPlayer
local uis=game:GetService("UserInputService")
local run=game:GetService("RunService")
local players=game:GetService("Players")
local flying=false
local speedOn=false
local jumpOn=false
local espOn=false
local noclipOn=false
local aimOn=false
local flySpeed=150
local walkSpeed=150
local jumpPower=150
local aimRange=100
local connection
flying=false
speedOn=false
jumpOn=false
espOn=false
noclipOn=false
aimOn=false

local gui=Instance.new("ScreenGui")
gui.Name="Vanh"
gui.ResetOnSpawn=false
gui.ZIndexBehavior=Enum.ZIndexBehavior.Sibling
gui.Parent=player:WaitForChild("PlayerGui")

local function corner(obj,r)
    local c=Instance.new("UICorner")
    c.CornerRadius=UDim.new(0,r)
    c.Parent=obj
end

local function stroke(obj,color,thickness,transparency)
    local s=Instance.new("UIStroke")
    s.Color=color
    s.Thickness=thickness or 1
    s.Transparency=transparency or 0
    s.Parent=obj
    return s
end

local purple=Color3.fromRGB(137,75,255)
local purple2=Color3.fromRGB(105,54,205)
local bg=Color3.fromRGB(9,8,17)
local panel=Color3.fromRGB(15,13,27)
local panel2=Color3.fromRGB(20,17,34)
local text=Color3.fromRGB(242,240,248)
local muted=Color3.fromRGB(145,139,160)
local discordUrl="https://discord.gg/DzmYysnRN"

local open=Instance.new("TextButton")
open.Size=UDim2.new(0,90,0,42)
open.Position=UDim2.new(0,20,.5,-21)
open.BackgroundColor3=panel2
open.Text="VANH"
open.TextColor3=text
open.TextSize=16
open.Font=Enum.Font.GothamBold
open.Parent=gui
corner(open,10)
stroke(open,purple,1,.2)

local frame=Instance.new("Frame")
frame.Size=UDim2.new(0,760,0,560)
frame.Position=UDim2.new(.5,-380,.5,-280)
frame.BackgroundColor3=bg
frame.BorderSizePixel=0
frame.Visible=false
frame.Parent=gui
corner(frame,16)
stroke(frame,purple,1.2,.05)

local top=Instance.new("Frame")
top.Size=UDim2.new(1,0,0,70)
top.BackgroundColor3=Color3.fromRGB(11,10,20)
top.BorderSizePixel=0
top.Parent=frame
corner(top,16)

local title=Instance.new("TextLabel")
title.Size=UDim2.new(0,90,1,0)
title.Position=UDim2.new(0,36,0,0)
title.BackgroundTransparency=1
title.Text="vanh"
title.TextColor3=Color3.fromRGB(161,91,255)
title.TextSize=27
title.Font=Enum.Font.GothamBold
title.TextXAlignment=Enum.TextXAlignment.Left
title.Parent=top

local by=Instance.new("TextLabel")
by.Size=UDim2.new(0,100,1,0)
by.Position=UDim2.new(0,130,0,0)
by.BackgroundTransparency=1
by.Text="by vanh"
by.TextColor3=Color3.fromRGB(110,103,128)
by.TextSize=13
by.Font=Enum.Font.Gotham
by.TextXAlignment=Enum.TextXAlignment.Left
by.Parent=top

local close=Instance.new("TextButton")
close.Size=UDim2.new(0,46,0,46)
close.Position=UDim2.new(1,-74,0,12)
close.BackgroundColor3=Color3.fromRGB(19,17,31)
close.Text="×"
close.TextColor3=Color3.fromRGB(205,201,215)
close.TextSize=29
close.Font=Enum.Font.Gotham
close.Parent=top
corner(close,12)
stroke(close,Color3.fromRGB(70,65,86),1,.25)

local line=Instance.new("Frame")
line.Size=UDim2.new(1,-2,0,1)
line.Position=UDim2.new(0,1,0,69)
line.BackgroundColor3=Color3.fromRGB(40,34,58)
line.BorderSizePixel=0
line.Parent=frame

local sidebar=Instance.new("Frame")
sidebar.Size=UDim2.new(0,150,0,452)
sidebar.Position=UDim2.new(0,18,0,88)
sidebar.BackgroundColor3=Color3.fromRGB(13,12,23)
sidebar.BorderSizePixel=0
sidebar.Parent=frame
corner(sidebar,15)
stroke(sidebar,Color3.fromRGB(55,48,76),1,.35)

local function sideButton(icon,caption,y)
    local b=Instance.new("TextButton")
    b.Size=UDim2.new(1,-20,0,54)
    b.Position=UDim2.new(0,10,0,y)
    b.BackgroundColor3=Color3.fromRGB(18,16,30)
    b.Text=""
    b.AutoButtonColor=false
    b.Parent=sidebar
    corner(b,12)
    local ic=Instance.new("TextLabel")
    ic.Size=UDim2.new(0,38,1,0)
    ic.Position=UDim2.new(0,9,0,0)
    ic.BackgroundTransparency=1
    ic.Text=icon
    ic.TextColor3=Color3.fromRGB(226,222,237)
    ic.TextSize=23
    ic.Font=Enum.Font.GothamBold
    ic.Parent=b
    local tx=Instance.new("TextLabel")
    tx.Size=UDim2.new(1,-55,1,0)
    tx.Position=UDim2.new(0,51,0,0)
    tx.BackgroundTransparency=1
    tx.Text=caption
    tx.TextColor3=Color3.fromRGB(201,197,211)
    tx.TextSize=15
    tx.Font=Enum.Font.Gotham
    tx.TextXAlignment=Enum.TextXAlignment.Left
    tx.Parent=b
    local bar=Instance.new("Frame")
    bar.Name="ActiveBar"
    bar.Size=UDim2.new(0,4,0,45)
    bar.Position=UDim2.new(0,-2,0,4)
    bar.BackgroundColor3=purple
    bar.BorderSizePixel=0
    bar.Visible=false
    bar.Parent=b
    corner(bar,3)
    return b,bar,tx
end

local support,supportBar,supportText=sideButton("◉","Discord",70)
local settings,settingsBar,settingsText=sideButton("⚙","Settings",134)
local aim,aimBar,aimText=sideButton("◎","Aim",198)

local version=Instance.new("TextLabel")
version.Size=UDim2.new(1,-30,0,22)
version.Position=UDim2.new(0,15,1,-30)
version.BackgroundTransparency=1
version.Text="v1"
version.TextColor3=Color3.fromRGB(111,104,128)
version.TextSize=11
version.Font=Enum.Font.Gotham
version.TextXAlignment=Enum.TextXAlignment.Center
version.Parent=sidebar
local content=Instance.new("Frame")
content.Size=UDim2.new(1,-184,1,-88)
content.Position=UDim2.new(0,176,0,88)
content.BackgroundTransparency=1
content.Parent=frame

local settingsPage=Instance.new("Frame")
settingsPage.Size=UDim2.new(1,0,1,0)
settingsPage.BackgroundTransparency=1
settingsPage.Visible=false
settingsPage.Parent=content

local aimPage=Instance.new("Frame")
aimPage.Size=UDim2.new(1,0,1,0)
aimPage.BackgroundTransparency=1
aimPage.Visible=false
aimPage.Parent=content

local supportPage=Instance.new("Frame")
supportPage.Size=UDim2.new(1,0,1,0)
supportPage.BackgroundTransparency=1
supportPage.Visible=true
supportPage.Parent=content

local function pageHeader(parent,titleText,subText)
    local t=Instance.new("TextLabel")
    t.Size=UDim2.new(1,0,0,38)
    t.Position=UDim2.new(0,0,0,12)
    t.BackgroundTransparency=1
    t.Text=titleText
    t.TextColor3=Color3.fromRGB(151,91,255)
    t.TextSize=24
    t.Font=Enum.Font.GothamBold
    t.TextXAlignment=Enum.TextXAlignment.Center
    t.Parent=parent
    local s=Instance.new("TextLabel")
    s.Size=UDim2.new(1,0,0,22)
    s.Position=UDim2.new(0,0,0,50)
    s.BackgroundTransparency=1
    s.Text=subText
    s.TextColor3=muted
    s.TextSize=12
    s.Font=Enum.Font.Gotham
    s.TextXAlignment=Enum.TextXAlignment.Center
    s.Parent=parent
    local deco=Instance.new("Frame")
    deco.Size=UDim2.new(0,120,0,1)
    deco.Position=UDim2.new(.5,-60,0,75)
    deco.BackgroundColor3=purple
    deco.BorderSizePixel=0
    deco.Parent=parent
end

pageHeader(settingsPage,"Settings","Configure the features")

local function makeToggle(parent,text,y,desc)
    local card=Instance.new("Frame")
    card.Size=UDim2.new(1,0,0,92)
    card.Position=UDim2.new(0,0,0,y)
    card.BackgroundColor3=Color3.fromRGB(18,16,29)
    card.BorderSizePixel=0
    card.Parent=parent
    corner(card,12)
    stroke(card,Color3.fromRGB(58,49,79),1,.35)
    local icon=Instance.new("TextLabel")
    icon.Size=UDim2.new(0,42,0,42)
    icon.Position=UDim2.new(0,12,0,12)
    icon.BackgroundColor3=Color3.fromRGB(38,23,65)
    icon.BackgroundTransparency=.1
    icon.TextColor3=purple
    icon.TextSize=21
    icon.Font=Enum.Font.GothamBold
    icon.Text=text=="Fly" and "✈" or text=="Speed" and "ϟ" or text=="Jump" and "↑" or text=="ESP" and "◉" or "♟"
    icon.Parent=card
    corner(icon,9)
    local title=Instance.new("TextLabel")
    title.Size=UDim2.new(1,-100,0,24)
    title.Position=UDim2.new(0,64,0,11)
    title.BackgroundTransparency=1
    title.Text=text
    title.TextColor3=textColor or Color3.fromRGB(242,239,248)
    title.TextSize=14
    title.Font=Enum.Font.GothamBold
    title.TextXAlignment=Enum.TextXAlignment.Left
    title.Parent=card
    local sub=Instance.new("TextLabel")
    sub.Size=UDim2.new(1,-100,0,20)
    sub.Position=UDim2.new(0,64,0,34)
    sub.BackgroundTransparency=1
    sub.Text=desc
    sub.TextColor3=muted
    sub.TextSize=10
    sub.Font=Enum.Font.Gotham
    sub.TextXAlignment=Enum.TextXAlignment.Left
    sub.Parent=card
    local toggle=Instance.new("TextButton")
    toggle.Size=UDim2.new(0,35,0,20)
    toggle.Position=UDim2.new(1,-48,0,15)
    toggle.BackgroundColor3=Color3.fromRGB(55,48,70)
    toggle.Text=""
    toggle.AutoButtonColor=false
    toggle.Parent=card
    corner(toggle,10)
    local knob=Instance.new("Frame")
    knob.Size=UDim2.new(0,16,0,16)
    knob.Position=UDim2.new(0,2,0,2)
    knob.BackgroundColor3=Color3.fromRGB(235,232,242)
    knob.BorderSizePixel=0
    knob.Parent=toggle
    corner(knob,8)
    local function set(v)
        toggle.BackgroundColor3=v and purple or Color3.fromRGB(55,48,70)
        knob.Position=v and UDim2.new(1,-18,0,2) or UDim2.new(0,2,0,2)
    end
    return card,toggle,set
end

local function makeSlider(parent,title,y,initial,minValue,maxValue,onChanged)
    local card=Instance.new("Frame")
    card.Size=UDim2.new(1,0,0,88)
    card.Position=UDim2.new(0,0,0,y)
    card.BackgroundColor3=Color3.fromRGB(18,16,29)
    card.BorderSizePixel=0
    card.Parent=parent
    corner(card,12)
    stroke(card,Color3.fromRGB(58,49,79),1,.35)
    local icon=Instance.new("TextLabel")
    icon.Size=UDim2.new(0,42,0,42)
    icon.Position=UDim2.new(0,12,0,12)
    icon.BackgroundColor3=Color3.fromRGB(38,23,65)
    icon.TextColor3=purple
    icon.TextSize=21
    icon.Font=Enum.Font.GothamBold
    icon.Text=title=="Fly" and "✈" or title=="Speed" and "ϟ" or "↑"
    icon.Parent=card
    corner(icon,9)
    local name=Instance.new("TextLabel")
    name.Size=UDim2.new(1,-100,0,23)
    name.Position=UDim2.new(0,64,0,10)
    name.BackgroundTransparency=1
    name.Text=title
    name.TextColor3=Color3.fromRGB(242,239,248)
    name.TextSize=14
    name.Font=Enum.Font.GothamBold
    name.TextXAlignment=Enum.TextXAlignment.Left
    name.Parent=card
    local desc=Instance.new("TextLabel")
    desc.Size=UDim2.new(1,-100,0,18)
    desc.Position=UDim2.new(0,64,0,32)
    desc.BackgroundTransparency=1
    desc.Text="Enable or disable "..string.lower(title)
    desc.TextColor3=muted
    desc.TextSize=10
    desc.Font=Enum.Font.Gotham
    desc.TextXAlignment=Enum.TextXAlignment.Left
    desc.Parent=card
    local toggle=Instance.new("TextButton")
    toggle.Size=UDim2.new(0,35,0,20)
    toggle.Position=UDim2.new(1,-48,0,15)
    toggle.BackgroundColor3=purple
    toggle.Text=""
    toggle.AutoButtonColor=false
    toggle.Parent=card
    corner(toggle,10)
    local knob=Instance.new("Frame")
    knob.Size=UDim2.new(0,16,0,16)
    knob.Position=UDim2.new(0,2,0,2)
    knob.BackgroundColor3=Color3.fromRGB(245,243,248)
    knob.BorderSizePixel=0
    knob.Parent=toggle
    corner(knob,8)
    local label=Instance.new("TextLabel")
    label.Size=UDim2.new(0,90,0,22)
    label.Position=UDim2.new(0,12,0,67)
    label.BackgroundTransparency=1
    label.Text=title=="Speed" and "Walk Speed" or title=="Jump" and "Jump Power" or "Fly Speed"
    label.TextColor3=Color3.fromRGB(232,228,240)
    label.TextSize=11
    label.Font=Enum.Font.Gotham
    label.TextXAlignment=Enum.TextXAlignment.Left
    label.Parent=card
    local minLabel=Instance.new("TextLabel")
    minLabel.Size=UDim2.new(0,25,0,20)
    minLabel.Position=UDim2.new(0,90,0,67)
    minLabel.BackgroundTransparency=1
    minLabel.Text=tostring(minValue)
    minLabel.TextColor3=Color3.fromRGB(218,213,228)
    minLabel.TextSize=11
    minLabel.Font=Enum.Font.Gotham
    minLabel.Parent=card
    local bar=Instance.new("Frame")
    bar.Size=UDim2.new(1,-250,0,5)
    bar.Position=UDim2.new(0,112,0,76)
    bar.BackgroundColor3=Color3.fromRGB(42,39,53)
    bar.BorderSizePixel=0
    bar.Parent=card
    corner(bar,3)
    local fill=Instance.new("Frame")
    fill.Size=UDim2.new((initial-minValue)/(maxValue-minValue),0,1,0)
    fill.BackgroundColor3=purple
    fill.BorderSizePixel=0
    fill.Parent=bar
    corner(fill,3)
    local knobSlider=Instance.new("TextButton")
    knobSlider.Size=UDim2.new(0,18,0,18)
    knobSlider.AnchorPoint=Vector2.new(.5,.5)
    knobSlider.Position=UDim2.new((initial-minValue)/(maxValue-minValue),0,.5,0)
    knobSlider.BackgroundColor3=purple
    knobSlider.Text=""
    knobSlider.AutoButtonColor=false
    knobSlider.Parent=bar
    corner(knobSlider,9)
    local maxLabel=Instance.new("TextLabel")
    maxLabel.Size=UDim2.new(0,30,0,20)
    maxLabel.Position=UDim2.new(1,-228,0,67)
    maxLabel.BackgroundTransparency=1
    maxLabel.Text=tostring(maxValue)
    maxLabel.TextColor3=Color3.fromRGB(218,213,228)
    maxLabel.TextSize=11
    maxLabel.Font=Enum.Font.Gotham
    maxLabel.Parent=card
    local box=Instance.new("TextBox")
    box.Size=UDim2.new(0,67,0,30)
    box.Position=UDim2.new(1,-83,0,62)
    box.BackgroundColor3=Color3.fromRGB(25,22,38)
    box.Text=tostring(initial)
    box.TextColor3=purple
    box.TextSize=13
    box.Font=Enum.Font.GothamBold
    box.ClearTextOnFocus=false
    box.TextXAlignment=Enum.TextXAlignment.Center
    box.Parent=card
    corner(box,7)
    stroke(box,Color3.fromRGB(76,55,116),1,.15)
    local draggingSlider=false
    local function setValue(v)
        v=math.clamp(math.floor(v+0.5),minValue,maxValue)
        fill.Size=UDim2.new((v-minValue)/(maxValue-minValue),0,1,0)
        knobSlider.Position=UDim2.new((v-minValue)/(maxValue-minValue),0,.5,0)
        box.Text=tostring(v)
        onChanged(v)
    end
    local function fromMouse(x)
        local alpha=math.clamp((x-bar.AbsolutePosition.X)/bar.AbsoluteSize.X,0,1)
        setValue(minValue+(maxValue-minValue)*alpha)
    end
    knobSlider.MouseButton1Down:Connect(function() draggingSlider=true end)
    bar.InputBegan:Connect(function(input)
        if input.UserInputType==Enum.UserInputType.MouseButton1 then
            draggingSlider=true
            fromMouse(input.Position.X)
        end
    end)
    uis.InputEnded:Connect(function(input)
        if input.UserInputType==Enum.UserInputType.MouseButton1 then draggingSlider=false end
    end)
    uis.InputChanged:Connect(function(input)
        if draggingSlider and input.UserInputType==Enum.UserInputType.MouseMovement then
            fromMouse(input.Position.X)
        end
    end)
    box.FocusLost:Connect(function()
        local v=tonumber(box.Text)
        if v then setValue(v) else box.Text=tostring(math.clamp(initial,minValue,maxValue)) end
    end)
    return card,box,setValue
end

local flyCard,flyBox,setFly=makeSlider(settingsPage,"Fly",72,flySpeed,1,300,function(v)
    flySpeed=v
end)
local speedCard,speedBox,setSpeed=makeSlider(settingsPage,"Speed",168,walkSpeed,1,300,function(v)
    walkSpeed=v
    if speedOn then
        local char=player.Character
        local humanoid=char and char:FindFirstChildOfClass("Humanoid")
        if humanoid then humanoid.WalkSpeed=v end
    end
end)
local jumpCard,jumpBox,setJump=makeSlider(settingsPage,"Jump",264,jumpPower,1,300,function(v)
    jumpPower=v
    if jumpOn then
        local char=player.Character
        local humanoid=char and char:FindFirstChildOfClass("Humanoid")
        if humanoid then humanoid.UseJumpPower=true humanoid.JumpPower=v end
    end
end)

local espCard,espToggle,setESP=makeToggle(settingsPage,"ESP",360,"Enable or disable esp")
espCard.Size=UDim2.new(.5,-5,0,64)
espCard.Position=UDim2.new(0,0,0,356)
local noclipCard,noclipToggle,setNoClip=makeToggle(settingsPage,"NoClip",360,"Enable or disable noclip")
noclipCard.Size=UDim2.new(.5,-5,0,64)
noclipCard.Position=UDim2.new(.5,5,0,356)

local flyToggle=flyCard:FindFirstChildOfClass("TextButton")
local speedToggle=speedCard:FindFirstChildOfClass("TextButton")
local jumpToggle=jumpCard:FindFirstChildOfClass("TextButton")

flyToggle.BackgroundColor3=Color3.fromRGB(55,48,70)
speedToggle.BackgroundColor3=Color3.fromRGB(55,48,70)
jumpToggle.BackgroundColor3=Color3.fromRGB(55,48,70)
for _,tg in ipairs({flyToggle,speedToggle,jumpToggle}) do
    local kb=tg:FindFirstChildOfClass("Frame")
    if kb then kb.Position=UDim2.new(0,2,0,2) end
end

local function setSliderToggle(toggle,on)
    local knob=toggle:FindFirstChildOfClass("Frame")
    toggle.BackgroundColor3=on and purple or Color3.fromRGB(55,48,70)
    if knob then knob.Position=on and UDim2.new(1,-18,0,2) or UDim2.new(0,2,0,2) end
end

flyToggle.MouseButton1Click:Connect(function()
    flying=not flying
    setSliderToggle(flyToggle,flying)
    if not flying then
        local char=player.Character
        local root=char and char:FindFirstChild("HumanoidRootPart")
        local bv=root and root:FindFirstChild("FlyVelocity")
        if bv then bv:Destroy() end
    end
end)
speedToggle.MouseButton1Click:Connect(function()
    speedOn=not speedOn
    setSliderToggle(speedToggle,speedOn)
    local char=player.Character
    local hrp=char and char:FindFirstChild("HumanoidRootPart")
    local humanoid=char and char:FindFirstChildOfClass("Humanoid")
    if speedOn then
        if humanoid then humanoid.WalkSpeed=walkSpeed end
        if hrp then
            local bv=hrp:FindFirstChild("SpeedVel")
            if not bv then
                bv=Instance.new("BodyVelocity")
                bv.Name="SpeedVel"
                bv.MaxForce=Vector3.new(math.huge,0,math.huge)
                bv.Velocity=Vector3.zero
                bv.Parent=hrp
            end
            task.spawn(function()
                while speedOn and hrp and hrp.Parent and bv and bv.Parent do
                    if humanoid and humanoid.MoveDirection.Magnitude>0 then
                        bv.Velocity=humanoid.MoveDirection*(math.max(walkSpeed-16,0))
                    else
                        bv.Velocity=Vector3.zero
                    end
                    task.wait()
                end
                if bv and bv.Parent then bv:Destroy() end
            end)
        end
    else
        if humanoid then humanoid.WalkSpeed=16 end
        if hrp then
            local bv=hrp:FindFirstChild("SpeedVel")
            if bv then bv:Destroy() end
        end
    end
end)
jumpToggle.MouseButton1Click:Connect(function()
    jumpOn=not jumpOn
    setSliderToggle(jumpToggle,jumpOn)
    local char=player.Character
    local humanoid=char and char:FindFirstChildOfClass("Humanoid")
    if humanoid then
        humanoid.UseJumpPower=true
        humanoid.JumpPower=jumpOn and jumpPower or 50
    end
end)
espToggle.MouseButton1Click:Connect(function()
    espOn=not espOn
    setESP(espOn)
    if espOn then updateESP() else clearESP() end
end)
noclipToggle.MouseButton1Click:Connect(function()
    noclipOn=not noclipOn
    setNoClip(noclipOn)
end)

local espFolder=Instance.new("Folder")
espFolder.Name="VanhESP"
espFolder.Parent=gui

local function clearESP()
    for _,v in ipairs(espFolder:GetChildren()) do
        v:Destroy()
    end
end

local function updateESP()
    clearESP()
    if not espOn then return end
    for _,p in ipairs(players:GetPlayers()) do
        if p~=player and p.Character then
            local char=p.Character
            local hum=char:FindFirstChildOfClass("Humanoid")
            local head=char:FindFirstChild("Head")
            if hum then
                local h=Instance.new("Highlight")
                h.Adornee=char
                h.FillTransparency=.65
                h.OutlineTransparency=0
                h.Parent=espFolder
                if head then
                    local bb=Instance.new("BillboardGui")
                    bb.Adornee=head
                    bb.Size=UDim2.new(0,250,0,55)
                    bb.StudsOffset=Vector3.new(0,3,0)
                    bb.AlwaysOnTop=true
                    bb.Parent=espFolder
                    local t=Instance.new("TextLabel")
                    t.Size=UDim2.new(1,0,1,0)
                    t.BackgroundTransparency=1
                    t.TextColor3=Color3.fromRGB(255,255,255)
                    t.TextStrokeTransparency=0
                    t.TextSize=14
                    t.Font=Enum.Font.GothamBold
                    t.Text=p.DisplayName.." ["..p.Name.."]\nHP: "..math.floor(hum.Health).."/"..math.floor(hum.MaxHealth)
                    t.Parent=bb
                end
            end
        end
    end
end

local function button(parent,textValue,pos,size)
    local b=Instance.new("TextButton")
    b.Size=size
    b.Position=pos
    b.BackgroundColor3=Color3.fromRGB(35,31,48)
    b.BorderSizePixel=0
    b.Text=textValue
    b.TextColor3=Color3.fromRGB(245,243,248)
    b.TextSize=13
    b.Font=Enum.Font.GothamBold
    b.AutoButtonColor=false
    b.Parent=parent
    corner(b,9)
    stroke(b,Color3.fromRGB(70,58,95),1,.25)
    return b
end

pageHeader(aimPage,"Aim","Automatically focus the nearest player")

local aimCard=Instance.new("Frame")
aimCard.Size=UDim2.new(1,0,0,190)
aimCard.Position=UDim2.new(0,0,0,92)
aimCard.BackgroundColor3=panel2
aimCard.BorderSizePixel=0
aimCard.Parent=aimPage
corner(aimCard,14)
stroke(aimCard,Color3.fromRGB(76,59,105),1,.2)
local aimTitle=Instance.new("TextLabel")
aimTitle.Size=UDim2.new(1,-30,0,28)
aimTitle.Position=UDim2.new(0,15,0,15)
aimTitle.BackgroundTransparency=1
aimTitle.Text="AIM • PLAYER"
aimTitle.TextColor3=Color3.fromRGB(225,222,235)
aimTitle.TextSize=15
aimTitle.Font=Enum.Font.GothamBold
aimTitle.TextXAlignment=Enum.TextXAlignment.Left
aimTitle.Parent=aimCard
local aimStatus=Instance.new("TextLabel")
aimStatus.Size=UDim2.new(1,-30,0,55)
aimStatus.Position=UDim2.new(0,15,0,48)
aimStatus.BackgroundTransparency=1
aimStatus.Text="Status: OFF\nTarget: NONE"
aimStatus.TextColor3=muted
aimStatus.TextSize=12
aimStatus.Font=Enum.Font.Gotham
aimStatus.TextYAlignment=Enum.TextYAlignment.Top
aimStatus.TextXAlignment=Enum.TextXAlignment.Left
aimStatus.Parent=aimCard
local aimButton=button(aimCard,"AIM OFF",UDim2.new(0,15,1,-52),UDim2.new(1,-30,0,38))
aimButton.MouseButton1Click:Connect(function()
    aimOn=not aimOn
    aimButton.Text=aimOn and "AIM ON" or "AIM OFF"
    aimButton.BackgroundColor3=aimOn and Color3.fromRGB(45,170,90) or Color3.fromRGB(35,31,48)
    if not aimOn then
        aimStatus.Text="Status: OFF\nTarget: NONE"
    end
end)

local discordLink=Instance.new("TextLabel")
discordLink.Size=UDim2.new(1,0,0,30)
discordLink.Position=UDim2.new(0,0,0,52)
discordLink.BackgroundTransparency=1
discordLink.Text="🔗  "..discordUrl
discordLink.TextColor3=Color3.fromRGB(146,83,255)
discordLink.TextSize=15
discordLink.Font=Enum.Font.GothamBold
discordLink.TextXAlignment=Enum.TextXAlignment.Center
discordLink.Parent=supportPage

local discordCard=Instance.new("Frame")
discordCard.Size=UDim2.new(1,-56,0,247)
discordCard.Position=UDim2.new(0,28,0,94)
discordCard.BackgroundColor3=Color3.fromRGB(18,15,31)
discordCard.BorderSizePixel=0
discordCard.Parent=supportPage
corner(discordCard,15)
stroke(discordCard,Color3.fromRGB(111,68,184),1,.15)

local DISCORD_AVATAR_ASSET="rbxassetid://YOUR_DISCORD_AVATAR_ASSET_ID" -- thay bang asset id avatar Vanh Hub || HM

local discordAvatar=Instance.new("ImageLabel")
discordAvatar.Size=UDim2.new(0,145,0,145)
discordAvatar.Position=UDim2.new(0,18,0,20)
discordAvatar.BackgroundColor3=Color3.fromRGB(9,8,16)
discordAvatar.BorderSizePixel=0
discordAvatar.Image=DISCORD_AVATAR_ASSET
discordAvatar.ScaleType=Enum.ScaleType.Crop
discordAvatar.Parent=discordCard
corner(discordAvatar,72)
stroke(discordAvatar,Color3.fromRGB(111,72,181),1.5,.05)

local serverName=Instance.new("TextLabel")
serverName.Size=UDim2.new(1,-190,0,35)
serverName.Position=UDim2.new(0,190,0,39)
serverName.BackgroundTransparency=1
serverName.Text="Vanh Hub || HM  ✓"
serverName.TextColor3=text
serverName.TextSize=22
serverName.Font=Enum.Font.GothamBold
serverName.TextXAlignment=Enum.TextXAlignment.Left
serverName.Parent=discordCard

local serverSub=Instance.new("TextLabel")
serverSub.Size=UDim2.new(1,-190,0,25)
serverSub.Position=UDim2.new(0,190,0,78)
serverSub.BackgroundTransparency=1
serverSub.Text="Join for support and updates"
serverSub.TextColor3=muted
serverSub.TextSize=13
serverSub.Font=Enum.Font.Gotham
serverSub.TextXAlignment=Enum.TextXAlignment.Left
serverSub.Parent=discordCard

local joinDiscord=button(discordCard,"◉  JOIN DISCORD",UDim2.new(0,18,1,-57),UDim2.new(0,488,0,42))
joinDiscord.BackgroundColor3=purple2
joinDiscord.TextColor3=Color3.fromRGB(255,255,255)
joinDiscord.TextSize=14
stroke(joinDiscord,purple,1,.05)


local credits=Instance.new("Frame")
credits.Size=UDim2.new(1,-56,0,97)
credits.Position=UDim2.new(0,28,0,365)
credits.BackgroundColor3=Color3.fromRGB(18,16,29)
credits.BorderSizePixel=0
credits.Parent=supportPage
corner(credits,14)
stroke(credits,Color3.fromRGB(51,45,69),1,.25)
local creditIcon=Instance.new("TextLabel")
creditIcon.Size=UDim2.new(0,48,0,48)
creditIcon.Position=UDim2.new(0,18,0,24)
creditIcon.BackgroundColor3=Color3.fromRGB(35,22,61)
creditIcon.Text="★"
creditIcon.TextColor3=Color3.fromRGB(153,91,255)
creditIcon.TextSize=23
creditIcon.Font=Enum.Font.GothamBold
creditIcon.Parent=credits
corner(creditIcon,24)
stroke(creditIcon,Color3.fromRGB(82,52,130),1,.2)
local creditsTitle=Instance.new("TextLabel")
creditsTitle.Size=UDim2.new(1,-90,0,25)
creditsTitle.Position=UDim2.new(0,83,0,20)
creditsTitle.BackgroundTransparency=1
creditsTitle.Text="Credits For Someone Peoples"
creditsTitle.TextColor3=Color3.fromRGB(228,224,237)
creditsTitle.TextSize=15
creditsTitle.Font=Enum.Font.GothamBold
creditsTitle.TextXAlignment=Enum.TextXAlignment.Left
creditsTitle.Parent=credits
local creditsSub=Instance.new("TextLabel")
creditsSub.Size=UDim2.new(1,-90,0,22)
creditsSub.Position=UDim2.new(0,83,0,50)
creditsSub.BackgroundTransparency=1
creditsSub.Text="Creator: Rafael and animewaze"
creditsSub.TextColor3=Color3.fromRGB(130,123,147)
creditsSub.TextSize=12
creditsSub.Font=Enum.Font.Gotham
creditsSub.TextXAlignment=Enum.TextXAlignment.Left
creditsSub.Parent=credits

local confirm=Instance.new("Frame")
confirm.Size=UDim2.new(0,320,0,160)
confirm.Position=UDim2.new(.5,-160,.5,-80)
confirm.BackgroundColor3=Color3.fromRGB(20,17,32)
confirm.Visible=false
confirm.ZIndex=10
confirm.Parent=gui
corner(confirm,14)
stroke(confirm,purple,1,.15)
local question=Instance.new("TextLabel")
question.Size=UDim2.new(1,-20,0,70)
question.Position=UDim2.new(0,10,0,12)
question.BackgroundTransparency=1
question.Text="Bạn có xác định tắt script?"
question.TextColor3=text
question.TextSize=16
question.Font=Enum.Font.GothamBold
question.TextWrapped=true
question.ZIndex=11
question.Parent=confirm
local yes=button(confirm,"CÓ",UDim2.new(0,25,0,103),UDim2.new(0,120,0,38))
yes.BackgroundColor3=Color3.fromRGB(135,55,85)
yes.ZIndex=11
local no=button(confirm,"KHÔNG",UDim2.new(0,175,0,103),UDim2.new(0,120,0,38))
no.ZIndex=11

local function selectTab(active)
    settingsPage.Visible=active==settings
    aimPage.Visible=active==aim
    supportPage.Visible=active==support
    supportBar.Visible=active==support
    settingsBar.Visible=active==settings
    aimBar.Visible=active==aim
    support.BackgroundColor3=active==support and Color3.fromRGB(27,21,45) or Color3.fromRGB(18,16,30)
    settings.BackgroundColor3=active==settings and Color3.fromRGB(27,21,45) or Color3.fromRGB(18,16,30)
    aim.BackgroundColor3=active==aim and Color3.fromRGB(27,21,45) or Color3.fromRGB(18,16,30)
    supportText.TextColor3=active==support and text or Color3.fromRGB(201,197,211)
    settingsText.TextColor3=active==settings and text or Color3.fromRGB(201,197,211)
    aimText.TextColor3=active==aim and text or Color3.fromRGB(201,197,211)
end
selectTab(support)

local function setState(b,onText,offText,state)
    b.Text=state and onText or offText
    b.BackgroundColor3=
        state
        and Color3.fromRGB(45,170,90)
        or Color3.fromRGB(90,90,100)
end
local function nearestPlayer()
    local char=player.Character
    local root=char and char:FindFirstChild("HumanoidRootPart")
    if not root then
        return nil
    end
    local target=nil
    local distance=aimRange
    for _,p in ipairs(players:GetPlayers()) do
        if p~=player then
            local c=p.Character
            local r=c and c:FindFirstChild("HumanoidRootPart")
            local h=c and c:FindFirstChildOfClass("Humanoid")
            if r and h and h.Health>0 then
                local d=(r.Position-root.Position).Magnitude
                if d<distance then
                    distance=d
                    target=p
                end
            end
        end
    end
    return target
end
open.MouseButton1Click:Connect(function()
    frame.Visible=not frame.Visible
end)
settings.MouseButton1Click:Connect(function()
    selectTab(settings)
end)
aim.MouseButton1Click:Connect(function()
    selectTab(aim)
end)
support.MouseButton1Click:Connect(function()
    selectTab(support)
end)
close.MouseButton1Click:Connect(function()
    confirm.Visible=true
end)
no.MouseButton1Click:Connect(function()
    confirm.Visible=false
end)
yes.MouseButton1Click:Connect(function()
    flying=false
    speedOn=false
    jumpOn=false
    espOn=false
    noclipOn=false
    aimOn=false
    local char=player.Character
    local root=char and char:FindFirstChild("HumanoidRootPart")
    local hum=char and char:FindFirstChildOfClass("Humanoid")
    if root then
        local bv=root:FindFirstChild("FlyVelocity")
        if bv then bv:Destroy() end
        local sv=root:FindFirstChild("SpeedVel")
        if sv then sv:Destroy() end
    end
    if hum then
        hum.WalkSpeed=16
        hum.UseJumpPower=true
        hum.JumpPower=50
    end
    if connection then
        connection:Disconnect()
        connection=nil
    end
    clearESP()
    gui:Destroy()
end)
joinDiscord.MouseButton1Click:Connect(function()
    local copied=false
    if setclipboard then
        local ok=pcall(function()
            setclipboard(discordUrl)
        end)
        copied=ok
    end
    if copied then
        joinDiscord.Text="✓  COPIED"
        joinDiscord.BackgroundColor3=Color3.fromRGB(46,160,80)
        stroke(joinDiscord,Color3.fromRGB(80,210,110),1,.05)
    else
        joinDiscord.Text="✓  OPEN DISCORD"
        joinDiscord.BackgroundColor3=Color3.fromRGB(46,160,80)
        stroke(joinDiscord,Color3.fromRGB(80,210,110),1,.05)
    end
    pcall(function()
        if syn and syn.request then
            syn.request({Url=discordUrl,Method="GET"})
        end
    end)
end)

local dragging=false
local dragStart
local startPos
top.InputBegan:Connect(function(input)
    if input.UserInputType==Enum.UserInputType.MouseButton1 then
        dragging=true
        dragStart=input.Position
        startPos=frame.Position
    end
end)
top.InputEnded:Connect(function(input)
    if input.UserInputType==Enum.UserInputType.MouseButton1 then
        dragging=false
    end
end)
uis.InputChanged:Connect(function(input)
    if dragging and input.UserInputType==Enum.UserInputType.MouseMovement then
        local delta=input.Position-dragStart
        frame.Position=UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset+delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset+delta.Y
        )
    end
end)
local openDragging=false
local openDragStart
local openStartPos
open.InputBegan:Connect(function(input)
    if input.UserInputType==Enum.UserInputType.MouseButton1 then
        openDragging=true
        openDragStart=input.Position
        openStartPos=open.Position
    end
end)
open.InputEnded:Connect(function(input)
    if input.UserInputType==Enum.UserInputType.MouseButton1 then
        openDragging=false
    end
end)
uis.InputChanged:Connect(function(input)
    if openDragging and input.UserInputType==Enum.UserInputType.MouseMovement then
        local delta=input.Position-openDragStart
        open.Position=UDim2.new(
            openStartPos.X.Scale,
            openStartPos.X.Offset+delta.X,
            openStartPos.Y.Scale,
            openStartPos.Y.Offset+delta.Y
        )
    end
end)
player.CharacterAdded:Connect(function(char)
    local humanoid=char:WaitForChild("Humanoid")
    if speedOn then
        humanoid.WalkSpeed=walkSpeed
    end
    if jumpOn then
        humanoid.UseJumpPower=true
        humanoid.JumpPower=jumpPower
    end
end)
players.PlayerAdded:Connect(function(p)
    p.CharacterAdded:Connect(function()
        task.wait(.3)
        if espOn then
            updateESP()
        end
    end)
end)
players.PlayerRemoving:Connect(function()
    if espOn then
        updateESP()
    end
end)
connection=run.RenderStepped:Connect(function()
    local char=player.Character
    local hrp=char and char:FindFirstChild("HumanoidRootPart")
    if flying and hrp then
        local bv=hrp:FindFirstChild("FlyVelocity")
        if not bv then
            bv=Instance.new("BodyVelocity")
            bv.Name="FlyVelocity"
            bv.MaxForce=Vector3.new(math.huge,math.huge,math.huge)
            bv.Parent=hrp
        end
        local cam=workspace.CurrentCamera
        local move=Vector3.zero
        if uis:IsKeyDown(Enum.KeyCode.W) then
            move+=cam.CFrame.LookVector
        end
        if uis:IsKeyDown(Enum.KeyCode.S) then
            move-=cam.CFrame.LookVector
        end
        if uis:IsKeyDown(Enum.KeyCode.A) then
            move-=cam.CFrame.RightVector
        end
        if uis:IsKeyDown(Enum.KeyCode.D) then
            move+=cam.CFrame.RightVector
        end
        if uis:IsKeyDown(Enum.KeyCode.Space) then
            move+=Vector3.new(0,1,0)
        end
        if uis:IsKeyDown(Enum.KeyCode.LeftControl) then
            move-=Vector3.new(0,1,0)
        end
        bv.Velocity = move.Magnitude > 0 and move.Unit * flySpeed or Vector3.zero
    end
    if speedOn and hrp then
        local humanoid=char and char:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.WalkSpeed=walkSpeed
            local bv=hrp:FindFirstChild("SpeedVel")
            if not bv then
                bv=Instance.new("BodyVelocity")
                bv.Name="SpeedVel"
                bv.MaxForce=Vector3.new(math.huge,0,math.huge)
                bv.Parent=hrp
            end
            if humanoid.MoveDirection.Magnitude>0 then
                bv.Velocity=humanoid.MoveDirection*(math.max(walkSpeed-16,0))
            else
                bv.Velocity=Vector3.zero
            end
        end
    end
    if noclipOn and char then
        for _,v in ipairs(char:GetDescendants()) do
            if v:IsA("BasePart") then
                v.CanCollide=false
            end
        end
    end
    if aimOn then
        local target=nearestPlayer()
        local cam=workspace.CurrentCamera
        local targetRoot=
            target
            and target.Character
            and target.Character:FindFirstChild("HumanoidRootPart")
        if targetRoot and cam then
            cam.CFrame=CFrame.lookAt(
                cam.CFrame.Position,
                targetRoot.Position
            )
            aimStatus.Text=
                "Status: ON\nTarget: "..target.Name
        else
            aimStatus.Text="Status: ON\nTarget: NONE"
        end
    end
end)
task.spawn(function()
    while gui.Parent do
        if espOn then
            updateESP()
        end
        task.wait(.35)
    end
end)
task.spawn(function()
    while gui.Parent do
        local char=player.Character
        local humanoid=char and char:FindFirstChildOfClass("Humanoid")
        if humanoid then
            if speedOn and humanoid.WalkSpeed~=walkSpeed then
                humanoid.WalkSpeed=walkSpeed
            end
            if jumpOn and humanoid.JumpPower~=jumpPower then
                humanoid.UseJumpPower=true
                humanoid.JumpPower=jumpPower
            end
        end
        task.wait(.1)
    end
end)

