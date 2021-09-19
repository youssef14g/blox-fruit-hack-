local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("By Zox_gg", "DarkTheme")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Only InCombat")
Section:NewButton("SafeMode", "ButtonInfo", function()
    local LocalPlayer = game:GetService("Players").LocalPlayer 
 _G.copy = true
 while _G.copy do
 wait(0.1)    
 if LocalPlayer.PlayerGui.Main.InCombat.Visible == false then      
   game.Players.LocalPlayer:Kick("GOOD BYE")     
  elseif LocalPlayer.PlayerGui.Main.InCombat.Visible == true then   
      print("safe mode work now")   
  end  
  end
end)
local Section = Tab:NewSection("Player + Esp ")
Section:NewButton("Ctrl + Click = Tp", "ButtonInfo", function()
local Plr = game:GetService("Players").LocalPlayer
local Mouse = Plr:GetMouse()
 
Mouse.Button1Down:connect(
    function()
        if not game:GetService("UserInputService"):IsKeyDown(Enum.KeyCode.LeftControl) then
            return
        end
        if not Mouse.Target then
            return
        end
        Plr.Character:MoveTo(Mouse.Hit.p)
    end
)
 
end)
Section:NewButton("Esp", "ButtonInfo", function()
local Holder = Instance.new("Folder", game.CoreGui)
Holder.Name = "ESP"

local Box = Instance.new("BoxHandleAdornment")
Box.Name = "nilBox"
Box.Size = Vector3.new(4, 7, 4)
Box.Color3 = Color3.new(100 / 255, 100 / 255, 100 / 255)
Box.Transparency = 0.7
Box.ZIndex = 0
Box.AlwaysOnTop = true
Box.Visible = true

local NameTag = Instance.new("BillboardGui")
NameTag.Name = "nilNameTag"
NameTag.Enabled = false
NameTag.Size = UDim2.new(0, 200, 0, 50)
NameTag.AlwaysOnTop = true
NameTag.StudsOffset = Vector3.new(0, 1.8, 0)
local Tag = Instance.new("TextLabel", NameTag)
Tag.Name = "Tag"
Tag.BackgroundTransparency = 1
Tag.Position = UDim2.new(0, -50, 0, 0)
Tag.Size = UDim2.new(0, 300, 0, 20)
Tag.TextSize = 20
Tag.TextColor3 = Color3.new(100 / 255, 100 / 255, 100 / 255)
Tag.TextStrokeColor3 = Color3.new(0 / 255, 0 / 255, 0 / 255)
Tag.TextStrokeTransparency = 0.4
Tag.Text = "nil"
Tag.Font = Enum.Font.SourceSansBold
Tag.TextScaled = false

local LoadCharacter = function(v)
	repeat wait() until v.Character ~= nil
	v.Character:WaitForChild("Humanoid")
	local vHolder = Holder:FindFirstChild(v.Name)
	vHolder:ClearAllChildren()
	local b = Box:Clone()
	b.Name = v.Name .. "Box"
	b.Adornee = v.Character
	b.Parent = vHolder
	local t = NameTag:Clone()
	t.Name = v.Name .. "NameTag"
	t.Enabled = true
	t.Parent = vHolder
	t.Adornee = v.Character:WaitForChild("Head", 5)
	if not t.Adornee then
		return UnloadCharacter(v)
	end
	t.Tag.Text = v.Name
	b.Color3 = Color3.new(v.TeamColor.r, v.TeamColor.g, v.TeamColor.b)
	t.Tag.TextColor3 = Color3.new(v.TeamColor.r, v.TeamColor.g, v.TeamColor.b)
	local Update
	local UpdateNameTag = function()
		if not pcall(function()
			v.Character.Humanoid.DisplayDistanceType = Enum.HumanoidDisplayDistanceType.None
			local maxh = math.floor(v.Character.Humanoid.MaxHealth)
			local h = math.floor(v.Character.Humanoid.Health)
			t.Tag.Text = v.Name .. "\n" .. ((maxh ~= 0 and tostring(math.floor((h / maxh) * 100))) or "0") .. "%  " .. tostring(h) .. "/" .. tostring(maxh)
		end) then
			Update:Disconnect()
		end
	end
	UpdateNameTag()
	Update = v.Character.Humanoid.Changed:Connect(UpdateNameTag)
end

local UnloadCharacter = function(v)
	local vHolder = Holder:FindFirstChild(v.Name)
	if vHolder and (vHolder:FindFirstChild(v.Name .. "Box") ~= nil or vHolder:FindFirstChild(v.Name .. "NameTag") ~= nil) then
		vHolder:ClearAllChildren()
	end
end

local LoadPlayer = function(v)
	local vHolder = Instance.new("Folder", Holder)
	vHolder.Name = v.Name
	v.CharacterAdded:Connect(function()
		pcall(LoadCharacter, v)
	end)
	v.CharacterRemoving:Connect(function()
		pcall(UnloadCharacter, v)
	end)
	v.Changed:Connect(function(prop)
		if prop == "TeamColor" then
			UnloadCharacter(v)
			wait()
			LoadCharacter(v)
		end
	end)
	LoadCharacter(v)
end

local UnloadPlayer = function(v)
	UnloadCharacter(v)
	local vHolder = Holder:FindFirstChild(v.Name)
	if vHolder then
		vHolder:Destroy()
	end
end

for i,v in pairs(game:GetService("Players"):GetPlayers()) do
	spawn(function() pcall(LoadPlayer, v) end)
end

game:GetService("Players").PlayerAdded:Connect(function(v)
	pcall(LoadPlayer, v)
end)

game:GetService("Players").PlayerRemoving:Connect(function(v)
	pcall(UnloadPlayer, v)
end)

game:GetService("Players").LocalPlayer.NameDisplayDistance = 0

end)
Section:NewButton("No Clip Press E", "ButtonInfo", function()
    

        noclip = false
        game:GetService('RunService').Stepped:connect(function()
        if noclip then
        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
        end
        end)
        plr = game.Players.LocalPlayer
        mouse = plr:GetMouse()
        mouse.KeyDown:connect(function(key)
         
        if key == "e" then
        noclip = not noclip
        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
        end
        end)
        print('Loaded')
        print('Press "E" to noclip')


end)
Section:NewButton("Fly", "ButtonInfo", function()
    repeat wait() 
	until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("Head") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid") 
local mouse = game.Players.LocalPlayer:GetMouse() 
repeat wait() until mouse
local plr = game.Players.LocalPlayer 
local torso = plr.Character.Head 
local flying = false
local deb = true 
local ctrl = {f = 0, b = 0, l = 0, r = 0} 
local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
local maxspeed = 400 
local speed = 5000 

function Fly() 
local bg = Instance.new("BodyGyro", torso) 
bg.P = 9e4 
bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
bg.cframe = torso.CFrame 
local bv = Instance.new("BodyVelocity", torso) 
bv.velocity = Vector3.new(0,0.1,0) 
bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
repeat wait() 
plr.Character.Humanoid.PlatformStand = true 
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then 
speed = speed+.10+(speed/maxspeed) 
if speed > maxspeed then 
speed = maxspeed 
end 
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then 
speed = speed-1 
if speed < 0 then 
speed = 0 
end 
end 
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then 
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
else 
bv.velocity = Vector3.new(0,0.1,0) 
end 
bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
until not flying 
ctrl = {f = 0, b = 0, l = 0, r = 0} 
lastctrl = {f = 0, b = 0, l = 0, r = 0} 
speed = 0 
bg:Destroy() 
bv:Destroy() 
plr.Character.Humanoid.PlatformStand = false 
end 
mouse.KeyDown:connect(function(key) 
if key:lower() == "f" then 
if flying then flying = false 
else 
flying = true 
Fly() 
end 
elseif key:lower() == "w" then 
ctrl.f = 1 
elseif key:lower() == "s" then 
ctrl.b = -1 
elseif key:lower() == "a" then 
ctrl.l = -1 
elseif key:lower() == "d" then 
ctrl.r = 1 
end 
end) 
mouse.KeyUp:connect(function(key) 
if key:lower() == "w" then 
ctrl.f = 0 
elseif key:lower() == "s" then 
ctrl.b = 0 
elseif key:lower() == "a" then 
ctrl.l = 0 
elseif key:lower() == "d" then 
ctrl.r = 0 
end 
end)
Fly()
end)




local Section = Tab:NewSection(" Devil Fruit")

Section:NewButton("Bring Fruit", "ButtonInfo", function()
    game:GetService("RunService").Stepped:Connect(function()
    pcall(function()
      for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
            if v:IsA("Tool") then
              v.Handle.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
            print("Fruit Found")
            else
            print("No Fruits In Server")
            end
        end
    end)
end)
end)

local Tab = Window:NewTab("Chest")
local Section = Tab:NewSection(" Farm Chest")
Section:NewButton("Chest Tp", "ButtonInfo", function()
while wait() do
for _,a in pairs(game.Workspace:GetChildren()) do 
    if string.find(a.Name,"Chest") then 
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = a.CFrame
    end
    end
    end
end)
local Tab = Window:NewTab("Items")
local Section = Tab:NewSection("Get Items")
Section:NewButton("AutoPoleV1 + Hop", "ButtonInfo", function()
_G.SelectWeapon = "Superhuman" 
_G.AutoPolev1 = true
loadstring(game:HttpGet("https://raw.githubusercontent.com/StormSKz12/AutoPoleV1/main/AutoPoleandServerHop"))()

end)
Section:NewButton("Auto Buy LegendarySword + Hop", "ButtonInfo", function()
_G.LegendarySword_Hop = true
loadstring(game:HttpGet("https://raw.githubusercontent.com/StormSKz12/Autobuylegendarysword/main/ServerHop"))()
end)
Section:NewButton("AutoBuy Enchantment + Hop", "ButtonInfo", function()
_G.AutoEnchantment_Hop = true
loadstring(game:HttpGet("https://raw.githubusercontent.com/StormSKz12/Strikehub/main/AutoBuyEnchantment_Hop"))()

end)
Section:NewButton("AutoBuy Enchantment + Hop", "ButtonInfo", function()
_G.Weapon = "Superhuman" -- "Combat","Black Leg","Electro","Fishman Karate","Dragon Claw","Superhuman","Sharkman Karate","Shisui","Wando","Saddi","True Tripple Katana","Dark Blade", "Electric Claw", "Tushita"
_G.AutoEliteHunter = true
_G.ServerHop = true
loadstring(game:HttpGet("https://raw.githubusercontent.com/StormSKz12/StrikeHub11/main/AutoEliteHunter_Hop"))
end)
