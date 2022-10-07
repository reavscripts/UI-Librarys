repeat wait() until game:IsLoaded()
--antiafk
local VirtualUser=game:service'VirtualUser'
	game:service'Players'.LocalPlayer.Idled:connect(function()
	warn("anti-afk")
	VirtualUser:CaptureController()
	VirtualUser:ClickButton2(Vector2.new())
end)

local library = loadstring(game:HttpGet(('https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/wall%20v3')))()
local player = game.Players.LocalPlayer

function fireButton1(button)
	for i,signal in next, getconnections(button.MouseButton1Click) do 
		signal:Fire()
	end
	for i,signal in next, getconnections(button.MouseButton1Down) do 
		signal:Fire()
	end
	for i,signal in next, getconnections(button.Activated) do 
		signal:Fire()
	end
end

local w = library:CreateWindow("Roguelike Prototype") 
local b = w:CreateFolder("AutoFarm")
local lab = b:Label("Counting Enemies",{
    TextSize = 18; 
    TextColor = Color3.fromRGB(255,255,255); 
    BgColor = Color3.fromRGB(69,69,69); 
    
}) 

local autofarm
b:Toggle("ON/OFF",function(af)
    autofarm = af
end)
local addstat
b:Toggle("AutoStats",function(as)
    addstat = as
end)

local distance = -50
b:Slider("Distance",{
    min = -1000; 
    max = 1000; 
    precise = false; 
},function(value)
    distance = value
end)
local skip = false
b:Toggle("Skip Rewards",function(sk)
    skip = sk
end)


local function FARM()
    for i,v in pairs(workspace.Enemies:GetChildren()) do
        player.Character.HumanoidRootPart.CFrame=v.Hitbox.CFrame+Vector3.new(0,distance,0)
    end
end
local function ATTACK()
    game:GetService("ReplicatedStorage").Remotes.WeaponStateChanged:FireServer("Light", true)
end
local function DOOR()
    for i,v in pairs(workspace.Dungeon:GetChildren()) do
        if v.Name == "DungeonEncounterGoal" then
            pcall(function()
            player.Character.HumanoidRootPart.CFrame=v.CFrame
            end)
        end
    end
end
local function door()
    for i,v in pairs(workspace.Dungeon:GetChildren()) do
        if v.Name == "Door" and v:FindFirstChild("Root") then
            player.Character.HumanoidRootPart.Position=v.Root.Position
        elseif v.Name == "Door" and v:FindFirstChild("Door") then
            player.Character.HumanoidRootPart.Position=v.Door.Position
        end
    end
end
local function PASS()
    for i,v in pairs(player.PlayerGui.Gui:GetChildren()) do
        if v.Name == "RewardFrame" then
            fireButton1(v.ButtonsFrame.PassButton)
            fireButton1(v.ButtonsFrame.ConfirmButton)
        end
    end
end

local function ADDSTAT()
    for i,v in pairs(player.PlayerGui.Gui:GetChildren()) do
        if v.Name == "StatPointsPrompt" then
            for u,z in pairs(v:GetDescendants()) do
                if z.Name == "Strength" and z:FindFirstChild("Stroke") or z.Name == "Agility" and z:FindFirstChild("Stroke") or z.Name == "Dominance" and z:FindFirstChild("Stroke") or z.Name == "Constitution" and z:FindFirstChild("Stroke") or z.Name == "Perseverance" and z:FindFirstChild("Stroke") or z.Name == "Compassion" and z:FindFirstChild("Stroke") then
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(z.Buttons.Plus)
                    fireButton1(v.Content.Buttons.Confirm)
                end
            end
        end
    end
end

spawn(function()
    while wait(.1) do
        if autofarm then
            ATTACK()
        end
    end
end)
local enemycount = 0
local function COUNT()
    for i,v in pairs(workspace.Enemies:GetChildren()) do
        if v.ClassName == "Model" then
            enemycount = enemycount + 1
            lab:Refresh("Enemy Remaining:  "..tostring(enemycount))
        end
    end
    enemycount = 0
end


spawn(function()
    while wait() do
        if autofarm then
            COUNT()
        end
    end
end)
spawn(function()
    while wait(.5) do
        if autofarm then
            door()
            DOOR()
        end
    end
end)

spawn(function()
    while wait(.5) do
        if skip and autofarm then
            PASS()
        end
    end
end)
        
spawn(function()
    while wait(.5) do
        if addstat and autofarm then
            ADDSTAT()
        end
    end
end)

            
spawn(function()
    game.RunService.Heartbeat:Connect(function()
        if autofarm then
            FARM()
        end
    end)
end)





