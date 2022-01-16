local DiscordLib = loadstring(game:HttpGet"https://raw.githubusercontent.com/dawid-scripts/UI-Libs/main/discord%20lib.txt")()
local win = DiscordLib:Window("Radion Project : One Piece Millennium ( II )")

local serv = win:Server("Function", "")
local tab = serv:Channel("Auto Farm")

	local TOOLS = {}
	for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v:IsA("Tool") then
			table.insert(TOOLS,v.Name)
		end
	end


tab:Slider("[ ! ] Distance",0,10,3,function(t)
    _G.Distance = t
end)

tab:Toggle("Auto Farm Level",false,function(t)
    _G.AutoFarm = t
while _G.AutoFarm do wait()
pcall(function()
for i,v in pairs(game:GetService("Workspace")["WorldMap"]["Enemys"]:GetChildren()) do
    if v.Name == "Bandit" and v.Humanoid.Health > 0 and v:FindFirstChild("HumanoidRootPart") then
        equip()
        game:GetService'VirtualUser':CaptureController()
		game:GetService'VirtualUser':Button1Down(Vector2.new(2540, 242))
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,0,_G.Distance)
    end
end
end)
end
end)



function equip()
	pcall(function()
		for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
			if v.Name == SelectedWeapon then
				game.Players.LocalPlayer.Character.Humanoid:EquipTool(v)
			end
		end
	end)
end

local rdropdwon = tab:Dropdown("Select Weapon",TOOLS,function(t)
	SelectedWeapon = t
end)


tab:Button("Refresh Weapon",function()
	rdropdwon:Clear()
	for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v:IsA("Tool") then
			rdropdwon:Add(v.Name)
		end
	end
	for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
		if v:IsA("Tool") then
			rdropdwon:Add(v.Name)
		end
	end
end)
 
