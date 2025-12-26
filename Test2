local UiManager = loadstring(game:HttpGet("https://github.com/Footagesus/WindUI/releases/latest/download/main.lua"))()
local PrimaryColor = Color3.fromHex("#FFFFFF")
local SecondaryColor = Color3.fromHex("#FF0000")
function gradient(Text, StartColor, EndColor)
    local TextLength = # Text
    local GradientString = ""
    for LoopCounter = 1, TextLength do
        local GradientProgress = (LoopCounter - 1) / math.max(TextLength - 1, 1)
        GradientString = GradientString .. "<font color=\"rgb(" .. math.floor((StartColor.R + (EndColor.R - StartColor.R) * GradientProgress) * 255) .. "," .. math.floor((StartColor.G + (EndColor.G - StartColor.G) * GradientProgress) * 255) .. "," .. math.floor((StartColor.B + (EndColor.B - StartColor.B) * GradientProgress) * 255) .. ")\">" .. Text:sub(LoopCounter, LoopCounter) .. "</font>"
    end
    return GradientString
end
local IsPopupClosed = false
local UiInstance = UiManager
UiManager.Popup(UiInstance, {
    Title = gradient("WYMS MM2 Hub", PrimaryColor, SecondaryColor),
    Icon = "info",
    Content = gradient("Enhanced MM2 Script with WYMS Features!", PrimaryColor, SecondaryColor) .. "<br/>" .. gradient("https://discord.gg/g63GNv3eHy", PrimaryColor, SecondaryColor),
    Buttons = {
        {
            Title = gradient("Exit", PrimaryColor, SecondaryColor),
            Callback = function()
            end,
            Variant = "Tertiary"
        },
        {
            Title = gradient("Copy ur own epik dc", PrimaryColor, SecondaryColor),
            Callback = function()
                setclipboard("put here boii")
                UiManager:Notify({
                    Title = "Discord Copied!",
                    Content = "Discord invite copied to clipboard!",
                    Icon = "check-circle",
                    Duration = 3
                })
                IsPopupClosed = true
            end,
            Variant = "Secondary"
        },
        {
            Title = gradient("Continue", PrimaryColor, SecondaryColor),
            Callback = function()
                IsPopupClosed = true
            end,
            Variant = "Secondary"
        }
    }
})
local UiManagerInstance = UiManager
repeat
    task.wait()
until IsPopupClosed
local MainWindow = UiManagerInstance:CreateWindow({
    Title = "Wym\'s MM2 Hub",
    Author = "Wym\'s Hub",
    Transparent = false,
    Theme = "Dark"
})
local PlayersService = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = PlayersService.LocalPlayer
local AutoFarmTab = {
    AutoFarmTab = MainWindow:Tab({
        Title = gradient("AutoFarm", PrimaryColor, SecondaryColor),
        Icon = "ghost"
    }),
    AntiAFKTab = MainWindow:Tab({
        Title = gradient("Anti AFK", PrimaryColor, SecondaryColor),
        Icon = "moon"
    }),
    SocialsTab = MainWindow:Tab({
        Title = gradient("SOCIALS", PrimaryColor, SecondaryColor),
        Icon = "star"
    })
}
local Player = LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
local PartName = Character
local HumanoidRootPart = Character.WaitForChild(PartName, "HumanoidRootPart")
local EmptyTable = {}
local IsInitialized = false
local Timeout = 15
local IsReady = false
local function Func(TargetPosition, Speed)
    if HumanoidRootPart then
        local Distance = (TargetPosition - HumanoidRootPart.Position).Magnitude / Speed
        local Tween = TweenService:Create(HumanoidRootPart, TweenInfo.new(Distance, Enum.EasingStyle.Linear), {
            CFrame = CFrame.new(TargetPosition)
        })
        Tween:Play()
        Tween.Completed:Wait()
    end
end
ReplicatedStorage.Remotes.Gameplay.CoinCollected.OnClientEvent:Connect(function(UnusedParameter, Parameter1, Parameter2)
    if IsReady and Parameter1 == Parameter2 then
        Player.Character:BreakJoints()
    end
end)
local function Func1()
    EmptyTable = {}
    IsInitialized = true
    task.spawn(function()
        while IsInitialized do
            Character = Player.Character or Player.CharacterAdded:Wait()
            HumanoidRootPart = Character:FindFirstChild("HumanoidRootPart")
            if HumanoidRootPart then
                local MaxValue = math.huge
                local Descendant1, Descendant2, Descendant3 = ipairs(workspace:GetDescendants())
                local DefaultValue = nil
                while true do
                    local Orb
                    Descendant3, Orb = Descendant1(Descendant2, Descendant3)
                    if Descendant3 == nil then
                        break
                    end
                    if Orb:IsA("BasePart") and (Orb.Name == "BeachBall" or Orb.Name == "Coin_Server") then
                        local OrbDistance = (Orb.Position - HumanoidRootPart.Position).Magnitude
                        if OrbDistance < MaxValue and OrbDistance < 250 then
                            if not EmptyTable[Orb] then
                                DefaultValue = Orb
                                MaxValue = OrbDistance
                            end
                        end
                    end
                end
                if DefaultValue then
                    Func(DefaultValue.Position, Timeout)
                    EmptyTable[DefaultValue] = true
                end
            end
            task.wait(0.1)
        end
    end)
end
local function Func2()
    IsInitialized = false
    EmptyTable = {}
end
AutoFarmTab.AutoFarmTab:Section({
    Title = gradient("Auto Farm", PrimaryColor, SecondaryColor)
})
AutoFarmTab.AutoFarmTab:Toggle({
    Title = gradient("Fastest Auto Farm", PrimaryColor, SecondaryColor),
    Default = false,
    Callback = function(Arg1)
        if Arg1 then
            Func1()
        else
            Func2()
        end
    end
})
AutoFarmTab.AutoFarmTab:Slider({
    Title = gradient("Auto Farm Speed", PrimaryColor, SecondaryColor),
    Value = {
        Min = 5,
        Max = 25,
        Default = 15
    },
    Callback = function(Arg2)
        Timeout = Arg2
    end
})
AutoFarmTab.AutoFarmTab:Toggle({
    Title = gradient("Auto Reset When Full", PrimaryColor, SecondaryColor),
    Default = false,
    Callback = function(Arg3)
        IsReady = Arg3
    end
})
AutoFarmTab.AntiAFKTab:Section({
    Title = gradient("Anti AFK Protection", PrimaryColor, SecondaryColor)
})
AutoFarmTab.AntiAFKTab:Button({
    Title = gradient("Enable Anti AFK", PrimaryColor, SecondaryColor),
    Callback = function()
        pcall(function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/hassanxzayn-lua/Anti-afk/main/antiafkbyhassanxzyn"))()
        end)
    end
})
AutoFarmTab.SocialsTab:Paragraph({
    Title = gradient("WYM Scripts", PrimaryColor, SecondaryColor),
    Desc = "My socials",
    Image = "bird",
    Buttons = {
        {
            Title = "YouTube",
            Callback = function()
                setclipboard("https://www.youtube.com/@ur own")
            end
        }
    }
})
AutoFarmTab.SocialsTab:Paragraph({
    Title = gradient("Wym\'s Hub", PrimaryColor, SecondaryColor),
    Image = "star",
    Buttons = {
        {
            Title = "TikTok",
            Callback = function()
                setclipboard("http://tiktok.com/@ur own")
            end
        }
    }
})
UiManagerInstance:Notify({
    Title = "Wym\'s MM2 Hub",
    Content = "Loaded successfully.",
    Icon = "check-circle",
    Duration = 5
})
