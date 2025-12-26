
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local lp = Players.LocalPlayer
local rs = ReplicatedStorage
local WindUI = loadstring(game:HttpGet("https://github.com/Footagesus/WindUI/releases/latest/download/main.lua"))()
local Window = WindUI:CreateWindow({
    Title = "Wym's MM2 Hub",
    SubTitle = "Enhanced MM2 Script with WYMS Features!",
    Author = "Wym's Hub",
    Theme = "Dark",
    Transparency = true
})
WindUI:Notify({
    Title = "WYMS MM2 Hub",
    Content = "Loaded successfully.",
    Icon = "check-circle",
    Duration = 5
})
local AutoFarmTab = Window:CreateTab({
    Name = "AutoFarm",
    Icon = "ghost"
})

local AntiAFKTab = Window:CreateTab({
    Name = "Anti AFK",
    Icon = "moon"
})

local SocialsTab = Window:CreateTab({
    Name = "SOCIALS",
    Icon = "star"
})
local AutoFarmSection = AutoFarmTab:CreateSection("Auto Farm")
local AutoFarmToggle = AutoFarmSection:CreateToggle({
    Name = "Fastest Auto Farm",
    Description = "Automatically collects coins",
    Default = false,
    Callback = function(Value)
        _G.AutoFarmEnabled = Value
        if Value then
            StartAutoFarm()
        else
            StopAutoFarm()
        end
    end
})

local AutoFarmSpeedSlider = AutoFarmSection:CreateSlider({
    Name = "Auto Farm Speed",
    Description = "Speed of auto farm",
    Default = 50,
    Min = 10,
    Max = 100,
    Callback = function(Value)
        _G.AutoFarmSpeed = Value
    end
})

local AutoResetToggle = AutoFarmSection:CreateToggle({
    Name = "Auto Reset When Full",
    Description = "Automatically reset when coin bag is full",
    Default = false,
    Callback = function(Value)
        _G.AutoReset = Value
    end
})
local AntiAFKSection = AntiAFKTab:CreateSection("Anti AFK Protection")

local AntiAFKToggle = AntiAFKSection:CreateToggle({
    Name = "Enable Anti AFK",
    Description = "Prevents you from being kicked for AFK",
    Default = false,
    Callback = function(Value)
        if Value then
            EnableAntiAFK()
        else
            DisableAntiAFK()
        end
    end
})

local SocialsSection = SocialsTab:CreateSection("WYM Scripts")

local Description = SocialsSection:CreateParagraph({
    Title = "My socials",
    Content = "Follow for more scripts!"
})

local DiscordButton = SocialsSection:CreateButton({
    Name = "Copy Discord",
    Callback = function()
        setclipboard("https://discord.gg/g63GNv3eHy")
        WindUI:Notify({
            Title = "Discord Copied!",
            Content = "Discord invite copied to clipboard!",
            Icon = "check-circle",
            Duration = 3
        })
    end
})

local YouTubeButton = SocialsSection:CreateButton({
    Name = "YouTube",
    Callback = function()
        setclipboard("https://www.youtube.com/@W.1ts")
    end
})

local TikTokButton = SocialsSection:CreateButton({
    Name = "TikTok",
    Callback = function()
        setclipboard("http://tiktok.com/@wymisthebest/")
    end
})
local AutoFarmConnection
local CharacterRootPart
function StartAutoFarm()
    if AutoFarmConnection then
        AutoFarmConnection:Disconnect()
    end
    AutoFarmConnection = game:GetService("RunService").Heartbeat:Connect(function()
        if not _G.AutoFarmEnabled or not lp.Character or not lp.Character:FindFirstChild("HumanoidRootPart") then
            return
        end
        CharacterRootPart = lp.Character.HumanoidRootPart
        local closestCoin = nil
        local closestDistance = math.huge
        for _, obj in ipairs(workspace:GetDescendants()) do
            if obj:IsA("BasePart") and (obj.Name == "Coin_Server" or obj.Name == "BeachBall") then
                local distance = (CharacterRootPart.Position - obj.Position).Magnitude
                if distance < closestDistance then
                    closestDistance = distance
                    closestCoin = obj
                end
            end
        end
        if closestCoin and closestDistance < 100 then
            local speed = _G.AutoFarmSpeed or 50
            local tweenInfo = TweenInfo.new(closestDistance / speed, Enum.EasingStyle.Linear)
            local tween = TweenService:Create(CharacterRootPart, tweenInfo, {
                CFrame = CFrame.new(closestCoin.Position)
            })
            tween:Play()
        end
    end)
end
function StopAutoFarm()
    if AutoFarmConnection then
        AutoFarmConnection:Disconnect()
        AutoFarmConnection = nil
    end
end
local AntiAFKScript
function EnableAntiAFK()
    pcall(function()
        AntiAFKScript = loadstring(game:HttpGet("https://raw.githubusercontent.com/hassanxzayn-lua/Anti-afk/main/antiafkbyhassanxzyn"))()
    end)
end
function DisableAntiAFK()
    AntiAFKScript = nil
end
lp.CharacterAdded:Connect(function(char)
    char:WaitForChild("HumanoidRootPart")
    CharacterRootPart = char.HumanoidRootPart
end)
local Remotes = rs:WaitForChild("Remotes")
local Gameplay = Remotes:WaitForChild("Gameplay")
local CoinCollected = Gameplay:WaitForChild("CoinCollected")
CoinCollected.OnClientEvent:Connect(function()
    if _G.AutoReset and lp.Character then
        task.wait(1)
        lp.Character:BreakJoints()
    end
end)
if lp.Character then
    CharacterRootPart = lp.Character:WaitForChild("HumanoidRootPart")
end
task.spawn(function()
    while task.wait(1) do
        if _G.AntiAFKEnabled then
            pcall(function()
                lp:GetMouse().Target = lp.Character.HumanoidRootPart
            end)
        end
    end
end)
