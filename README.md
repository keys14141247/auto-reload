	if script.Parent.Text == "Auto-reload" then
		script.Parent.Text = "UnAuto-reload"
		script.Parent.Check.Image = "rbxassetid://10221330509"



		--start
		_G.drop = true
		repeat wait()
			if _G.drop == true then

				local sucess = nil
				while wait(0.5) do
					for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
						if v:FindFirstChild("Ammo") and v.Ammo.Value ~= 0 then
							v.Parent = game.Players.LocalPlayer.Character
						end
					end
					for ii, vv in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
						if vv:FindFirstChild("Ammo") and vv.Ammo.Value == 0 then
							game.Players.LocalPlayer.Character.Humanoid:UnequipTools()
						end
					end
					for iii, vvv in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
						if vvv:FindFirstChild("Ammo") and vvv.Ammo.Value ~= 0 then 
							sucess = true
						end
					end
					if not sucess ==  true then
						for iiii, vvvv in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do 
							if vvvv:FindFirstChild("Ammo") and vvvv.Ammo.Value == 0 then
								game.Players.LocalPlayer.Character.Humanoid:UnequipTools()
								game.Players.LocalPlayer.Character.Humanoid:EquipTool(vvvv)
								game.ReplicatedStorage.MainEvent:FireServer("Reload", vvvv)
								repeat wait() until vvvv.Ammo.Value ~= 0
							end
						end
					end
					sucess = nil
				end

			end
		until _G.drop == false



	else
		script.Parent.Text = "Auto-reload"
		script.Parent.Check.Image = "rbxassetid://10221453823"
		_G.drop = false
	end
