local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Tools to be removed
local BadTools = {
    "Power Stone", "Time Stone", "Teleport Power", "Meteor Attack", "Web Attack", "Web Hook", "Web Trap", 
    "Big Web Ball", "Shock", "Axe Smash", "Lightning Strike", "Throwing Axe", "Super Attack", "Laser Eyes", 
    "Ice Breath", "Throwing Car", "Staff Attack", "Tesseract", "Soul Watcher", "Invisible Power", "Energy Attack", 
    "Sword Strike", "Devil Hell", "Giant Sword Attack", "Spike Attack", "Spike Hook", "Spike Trap", "Spike Hell", 
    "Acid Attack", "Throwing Bomb", "Red Explosion", "Insanity", "Throwing Rock", "Giant Smash", "Air Power", 
    "Mega Giant Smash", "Laser Blast", "Mini Rockets", "Giant Laser Blast", "Hyper Blast"
}

-- Support for bad executors
local touchinterest = {}
local firetouchinterest = firetouchinterest or function(part, part2, value)
    if part and part2 then
        if value == 0 then
            touchinterest[1] = part.CFrame
            part.CFrame = part2.CFrame
        else
            part.CFrame = touchinterest[1]
            touchinterest[1] = nil
        end
    end
end

local GetTools = function()
    local Root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    for _, v in next, workspace.Tycoons:GetDescendants() do
        if v:IsA("TouchTransmitter") and v.Parent.Parent.Name:find("GearGiver1") then
            firetouchinterest(Root, v.Parent, 0)
            firetouchinterest(Root, v.Parent, 1)
        end
    end
end

local InstantRespawn = function()
    spawn(function()
        repeat
            RunService.Stepped:Wait()
        until LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid") ~= nil

        LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid").Died:Connect(function()
            ReplicatedStorage:WaitForChild("Guide"):FireServer()
        end)
    end)
end

-- Check if a value exists in a table
local FindInTable = function(tbl, val)
    if tbl == nil then return false end
    for _, v in pairs(tbl) do
        if v == val then return true end
    end 
    return false
end

-- Remove unwanted tools from backpack
local CleanBackpack = function()
    local Backpack = LocalPlayer:FindFirstChildWhichIsA("Backpack")
    if Backpack then
        Backpack.ChildAdded:Connect(function(obj)
            if FindInTable(BadTools, obj.Name) then
                obj:Destroy()
            end
        end)
    end
end

LocalPlayer.CharacterAdded:Connect(function()
    LocalPlayer.Character:WaitForChild("HumanoidRootPart")
    RunService.Stepped:Wait()
    InstantRespawn()
    GetTools()
end)

CleanBackpack()
InstantRespawn()
GetTools()
