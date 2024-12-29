-- Script de voo para Roblox

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

local flying = false
local bodyGyro = Instance.new("BodyGyro")
local bodyVelocity = Instance.new("BodyVelocity")

bodyGyro.P = 9e4
bodyGyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
bodyGyro.cframe = humanoidRootPart.CFrame

bodyVelocity.velocity = Vector3.new(0, 0, 0)
bodyVelocity.maxForce = Vector3.new(9e9, 9e9, 9e9)

local function startFlying()
    bodyGyro.Parent = humanoidRootPart
    bodyVelocity.Parent = humanoidRootPart
    flying = true
    while flying do
        bodyGyro.cframe = workspace.CurrentCamera.CFrame
        bodyVelocity.velocity = workspace.CurrentCamera.CFrame.LookVector * 50
        wait()
    end
end

local function stopFlying()
    flying = false
    bodyGyro:Destroy()
    bodyVelocity:Destroy()
end

local function toggleFly()
    if flying then
        stopFlying()
    else
        startFlying()
    end
end

-- Atalho para ativar/desativar o voo (tecla "F")
game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.F then
        toggleFly()
    end
end)

