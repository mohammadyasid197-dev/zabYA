-- [[ ZAB MEGA TOOLKIT v51 - by ZAB ]] --
-- Compact Tabs | Skybox + Decal Grid | Minimize per Tab

if getgenv and getgenv().ZabSrv51 then
    for _, c in pairs(getgenv().ZabSrv51) do
        pcall(function() c:Disconnect() end)
    end
end
getgenv().ZabSrv51 = {}

local spawn = (task and task.spawn) or coroutine.wrap
local wait = (task and task.wait) or (_G.wait or function(t) return t end)

local Players = game:GetService("Players")
local RS = game:GetService("RunService")
local UIS = game:GetService("UserInputService")
local SG = game:GetService("StarterGui")
local WS = game:GetService("Workspace")
local Debris = game:GetService("Debris")
local TS = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")
local LP = Players.LocalPlayer

local function notify(t, x)
    pcall(function()
        SG:SetCore("SendNotification", {Title=t, Text=x, Duration=3})
    end)
end

local function getSafeParent()
    local ok, hui = pcall(function() return gethui() end)
    if ok and hui then return hui end
    local ok2, cg = pcall(function() return game:GetService("CoreGui") end)
    if ok2 and cg then return cg end
    return LP:WaitForChild("PlayerGui")
end

local GuiParent = getSafeParent()
pcall(function()
    for _, n in ipairs({"ZAB_MEGA_V51", "ZAB_MEGA_Password"}) do
        local old = GuiParent:FindFirstChild(n)
        if old then old:Destroy() end
    end
end)

-- ============ TEMA ============
local C = {
    Main   = Color3.fromRGB(255, 40, 40),
    Bright = Color3.fromRGB(255, 120, 120),
    Deep   = Color3.fromRGB(120, 20, 20),
    Dark   = Color3.fromRGB(60, 5, 5),
    Void   = Color3.fromRGB(10, 2, 2),
    Panel  = Color3.fromRGB(30, 8, 8),
    Text   = Color3.fromRGB(255, 230, 230),
    Dim    = Color3.fromRGB(200, 140, 140),
    Gold   = Color3.fromRGB(255, 200, 100),
    Green  = Color3.fromRGB(100, 255, 150),
    Cyan   = Color3.fromRGB(100, 240, 255),
    Purple = Color3.fromRGB(180, 80, 255),
    Pink   = Color3.fromRGB(255, 100, 200),
    Blue   = Color3.fromRGB(100, 150, 255),
}

-- ============ PASSWORD ============
local VALID_PASSWORDS = { "ZABPRIVAT2026", "ZBNPRO999", "VIPZAB1212" }
local MAX_ATTEMPTS = 3
local attempts = 0
local passwordPassed = false

local PwUI = Instance.new("ScreenGui")
PwUI.Name = "ZAB_MEGA_Password"
PwUI.ResetOnSpawn = false
PwUI.IgnoreGuiInset = true
PwUI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
PwUI.Parent = GuiParent

local PwPanel = Instance.new("Frame", PwUI)
PwPanel.Size = UDim2.new(0, 280, 0, 190)
PwPanel.Position = UDim2.new(0.5, -140, 0.5, -95)
PwPanel.BackgroundColor3 = C.Panel
PwPanel.BorderSizePixel = 0
PwPanel.Active = true
Instance.new("UICorner", PwPanel).CornerRadius = UDim.new(0, 10)

local PwStroke = Instance.new("UIStroke", PwPanel)
PwStroke.Thickness = 1.5
PwStroke.Color = C.Main

local PwHeader = Instance.new("Frame", PwPanel)
PwHeader.Size = UDim2.new(1, 0, 0, 42)
PwHeader.BackgroundColor3 = C.Deep
PwHeader.BorderSizePixel = 0
Instance.new("UICorner", PwHeader).CornerRadius = UDim.new(0, 10)

local PwHeaderFix = Instance.new("Frame", PwHeader)
PwHeaderFix.Size = UDim2.new(1, 0, 0, 12)
PwHeaderFix.Position = UDim2.new(0, 0, 1, -12)
PwHeaderFix.BackgroundColor3 = C.Deep
PwHeaderFix.BorderSizePixel = 0

local PwTitle = Instance.new("TextLabel", PwHeader)
PwTitle.Size = UDim2.new(1, -50, 0, 18)
PwTitle.Position = UDim2.new(0, 48, 0, 5)
PwTitle.BackgroundTransparency = 1
PwTitle.Text = "ZAB MEGA v51 🔒"
PwTitle.TextColor3 = C.Bright
PwTitle.Font = Enum.Font.GothamBlack
PwTitle.TextSize = 13
PwTitle.TextXAlignment = Enum.TextXAlignment.Left
PwTitle.ZIndex = 2

local PwSubTitle = Instance.new("TextLabel", PwHeader)
PwSubTitle.Size = UDim2.new(1, -50, 0, 12)
PwSubTitle.Position = UDim2.new(0, 48, 0, 24)
PwSubTitle.BackgroundTransparency = 1
PwSubTitle.Text = "by ZAB"
PwSubTitle.TextColor3 = C.Dim
PwSubTitle.Font = Enum.Font.GothamMedium
PwSubTitle.TextSize = 9
PwSubTitle.TextXAlignment = Enum.TextXAlignment.Left
PwSubTitle.ZIndex = 2

local LockIcon = Instance.new("TextLabel", PwHeader)
LockIcon.Size = UDim2.new(0, 32, 0, 32)
LockIcon.Position = UDim2.new(0, 8, 0.5, -16)
LockIcon.BackgroundTransparency = 1
LockIcon.Text = "🔐"
LockIcon.TextSize = 22
LockIcon.ZIndex = 2

local PwInfo = Instance.new("TextLabel", PwPanel)
PwInfo.Size = UDim2.new(1, -20, 0, 20)
PwInfo.Position = UDim2.new(0, 10, 0, 50)
PwInfo.BackgroundTransparency = 1
PwInfo.Text = "▸ Masukkan password:"
PwInfo.TextColor3 = C.Dim
PwInfo.Font = Enum.Font.GothamMedium
PwInfo.TextSize = 10
PwInfo.TextXAlignment = Enum.TextXAlignment.Left

local PwInput = Instance.new("TextBox", PwPanel)
PwInput.Size = UDim2.new(1, -20, 0, 32)
PwInput.Position = UDim2.new(0, 10, 0, 74)
PwInput.BackgroundColor3 = C.Dark
PwInput.BorderSizePixel = 0
PwInput.PlaceholderText = "••••••••••••"
PwInput.Text = ""
PwInput.PlaceholderColor3 = C.Dim
PwInput.TextColor3 = C.Text
PwInput.Font = Enum.Font.Code
PwInput.TextSize = 13
PwInput.ClearTextOnFocus = false
Instance.new("UICorner", PwInput).CornerRadius = UDim.new(0, 6)
local PwInputStroke = Instance.new("UIStroke", PwInput)
PwInputStroke.Thickness = 1
PwInputStroke.Color = C.Main

local SubmitBtn = Instance.new("TextButton", PwPanel)
SubmitBtn.Size = UDim2.new(1, -20, 0, 34)
SubmitBtn.Position = UDim2.new(0, 10, 0, 112)
SubmitBtn.BackgroundColor3 = C.Panel
SubmitBtn.BorderSizePixel = 0
SubmitBtn.Text = "🔓 UNLOCK"
SubmitBtn.TextColor3 = C.Bright
SubmitBtn.Font = Enum.Font.GothamBold
SubmitBtn.TextSize = 13
SubmitBtn.AutoButtonColor = false
Instance.new("UICorner", SubmitBtn).CornerRadius = UDim.new(0, 6)
local SubmitStroke = Instance.new("UIStroke", SubmitBtn)
SubmitStroke.Thickness = 1
SubmitStroke.Color = C.Main

local PwStatus = Instance.new("TextLabel", PwPanel)
PwStatus.Size = UDim2.new(1, -20, 0, 14)
PwStatus.Position = UDim2.new(0, 10, 1, -20)
PwStatus.BackgroundTransparency = 1
PwStatus.Text = "Sisa: " .. MAX_ATTEMPTS
PwStatus.TextColor3 = C.Dim
PwStatus.Font = Enum.Font.GothamMedium
PwStatus.TextSize = 9
PwStatus.TextXAlignment = Enum.TextXAlignment.Left

local function checkPassword()
    local input = PwInput.Text
    local isValid = false
    for _, pw in ipairs(VALID_PASSWORDS) do
        if input == pw then isValid = true break end
    end
    if isValid then
        passwordPassed = true
        PwStatus.Text = "✅ Access Granted!"
        PwStatus.TextColor3 = C.Green
        PwInputStroke.Color = C.Green
        wait(0.5)
        PwUI:Destroy()
    else
        attempts = attempts + 1
        local left = MAX_ATTEMPTS - attempts
        if left <= 0 then
            PwStatus.Text = "❌ BLOCKED!"
            PwStatus.TextColor3 = C.Main
            wait(1)
            PwUI:Destroy()
            notify("❌", "Access Denied")
        else
            PwStatus.Text = "❌ Salah! Sisa: " .. left
            PwStatus.TextColor3 = C.Main
            PwInput.Text = ""
            wait(0.5)
        end
    end
end

SubmitBtn.MouseButton1Click:Connect(checkPassword)
PwInput.FocusLost:Connect(function(enter)
    if enter then checkPassword() end
end)

repeat wait(0.1) until passwordPassed

-- ============ SOUND DATABASE ============
local SOUNDS = {
    SpookyScarySkeletons = { "rbxassetid://90089940136467", "rbxassetid://138081566" },
    HolyWarFunk = { "rbxassetid://75793040119604", "rbxassetid://136240084994418" },
    JellybeanSmoke = { "rbxassetid://89376395986302" },
    C00lkiddTheme  = { "rbxassetid://9046339732", "rbxassetid://1837879082" },
    C00lkiddLaugh  = { "rbxassetid://1837879082", "rbxassetid://131961136" },
    C00lkiddScream = { "rbxassetid://5571927091", "rbxassetid://6106373814" },
    C00lkiddBoom   = { "rbxassetid://5801257794", "rbxassetid://152577941" },
    Cuber1 = { "rbxassetid://1848354536", "rbxassetid://1845755374" },
    Cuber2 = { "rbxassetid://1845755374", "rbxassetid://1848354536" },
    Cuber3 = { "rbxassetid://1838615501", "rbxassetid://1838353465" },
    Skibidi   = { "rbxassetid://9322658283", "rbxassetid://9046339732" },
    Sus       = { "rbxassetid://5821072041", "rbxassetid://6344122226" },
    Bruh      = { "rbxassetid://6344122226", "rbxassetid://5821072041" },
    OhNo      = { "rbxassetid://9114490800", "rbxassetid://6344122226" },
    MetalPipe = { "rbxassetid://7170380038", "rbxassetid://3475961913" },
    Fart      = { "rbxassetid://1377540676", "rbxassetid://1837879082" },
    VineBoom  = { "rbxassetid://5191585878", "rbxassetid://1836328724" },
    NyanCat   = { "rbxassetid://1836328724", "rbxassetid://1843969161" },
    RobloxOof = { "rbxassetid://1837798062", "rbxassetid://6344122226" },
    SadViolin = { "rbxassetid://1836074665", "rbxassetid://1836328724" },
    AnimeWow  = { "rbxassetid://1843969161", "rbxassetid://1848354536" },
    EmoDamage = { "rbxassetid://9120386436", "rbxassetid://9114490800" },
    SkeletonHorror = { "rbxassetid://6106373814", "rbxassetid://131961136" },
    SkeletonSpooky = { "rbxassetid://131961136", "rbxassetid://6106373814" },
    Ghost          = { "rbxassetid://5153043451", "rbxassetid://131961136" },
    Zombie         = { "rbxassetid://5777363385", "rbxassetid://6106373814" },
    Thunder    = { "rbxassetid://1836328724", "rbxassetid://5801257794" },
    Explosion  = { "rbxassetid://152577941", "rbxassetid://5801257794" },
    GlassBreak = { "rbxassetid://3475961913", "rbxassetid://7170380038" },
    Nuke       = { "rbxassetid://271753204", "rbxassetid://152577941" },
}

local workingCache = {}
local function playSound(idList, vol, pitch)
    if type(idList) == "string" then idList = { idList } end
    if not idList or #idList == 0 then return end
    spawn(function()
        pcall(function()
            if workingCache[idList[1]] then
                local s = Instance.new("Sound")
                s.SoundId = workingCache[idList[1]]
                s.Volume = vol or 5
                s.Pitch = pitch or 1
                s.Parent = WS
                s:Play()
                Debris:AddItem(s, 10)
                return
            end
            for _, id in ipairs(idList) do
                local s = Instance.new("Sound")
                s.SoundId = id
                s.Volume = vol or 5
                s.Pitch = pitch or 1
                s.Parent = WS
                s:Play()
                wait(0.05)
                if s.TimeLength > 0 or s.IsPlaying then
                    workingCache[idList[1]] = id
                    Debris:AddItem(s, 10)
                    return
                else
                    s:Destroy()
                end
            end
        end)
    end)
end

-- ============ SCAN REMOTES ============
local remotes = {}
local function scanAllRemotes()
    remotes = {}
    for _, obj in ipairs(game:GetDescendants()) do
        if obj:IsA("RemoteEvent") or obj:IsA("RemoteFunction") then
            table.insert(remotes, obj)
        end
    end
    return #remotes
end
local totalRemotes = scanAllRemotes()

-- ============ STATE ============
local flingOn, autoAttackOn, flyOn, noclipOn, godmodeOn = false, false, false, false, false
local espOn, antiVoidOn, autoJumpOn, pirateOn, controlRoomOn = false, false, false, false, false
local emoteHandsOn, skybox1On, skybox2On, decalSpamOn = false, false, false, false

-- ============ MOVEMENT ============
local function startFling()
    spawn(function()
        while flingOn and LP.Character do
            local hrp = LP.Character:FindFirstChild("HumanoidRootPart")
            if hrp then
                for _, p in ipairs(Players:GetPlayers()) do
                    if p ~= LP and p.Character then
                        local t = p.Character:FindFirstChild("HumanoidRootPart")
                        local thum = p.Character:FindFirstChildOfClass("Humanoid")
                        if t and thum and thum.Health > 0 and (t.Position - hrp.Position).Magnitude < 30 then
                            pcall(function()
                                local bv = Instance.new("BodyVelocity")
                                bv.Velocity = Vector3.new(999999, 999999, 999999)
                                bv.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                                bv.Parent = t
                                Debris:AddItem(bv, 0.1)
                            end)
                        end
                    end
                end
            end
            wait(0.3)
        end
    end)
end

local function startAutoAttack()
    spawn(function()
        while autoAttackOn do
            local char = LP.Character
            local myRoot = char and char:FindFirstChild("HumanoidRootPart")
            if myRoot then
                for _, p in ipairs(Players:GetPlayers()) do
                    if p ~= LP and p.Character then
                        local t = p.Character:FindFirstChild("HumanoidRootPart")
                        if t and (t.Position - myRoot.Position).Magnitude < 50 then
                            for _, r in ipairs(remotes) do
                                local nm = r.Name:lower()
                                if nm:find("kill") or nm:find("damage") or nm:find("hit") or nm:find("attack") or nm:find("hurt") then
                                    pcall(function()
                                        if r:IsA("RemoteEvent") then
                                            r:FireServer(p)
                                            r:FireServer(p.Name)
                                            r:FireServer(p, 99999)
                                        end
                                    end)
                                end
                            end
                        end
                    end
                end
            end
            wait(1)
        end
    end)
end

local flyBV, flyBG
local function startFly()
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    flyBV = Instance.new("BodyVelocity", hrp)
    flyBV.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
    flyBG = Instance.new("BodyGyro", hrp)
    flyBG.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
    flyBG.P = 1000
    flyBG.D = 50
    spawn(function()
        while flyOn and hrp and hrp.Parent do
            local cam = WS.CurrentCamera
            local move = Vector3.new(0, 0, 0)
            if UIS:IsKeyDown(Enum.KeyCode.W) then move = move + cam.CFrame.LookVector end
            if UIS:IsKeyDown(Enum.KeyCode.S) then move = move - cam.CFrame.LookVector end
            if UIS:IsKeyDown(Enum.KeyCode.A) then move = move - cam.CFrame.RightVector end
            if UIS:IsKeyDown(Enum.KeyCode.D) then move = move + cam.CFrame.RightVector end
            if UIS:IsKeyDown(Enum.KeyCode.Space) then move = move + Vector3.new(0, 1, 0) end
            if UIS:IsKeyDown(Enum.KeyCode.LeftControl) then move = move - Vector3.new(0, 1, 0) end
            flyBV.Velocity = move * 80
            flyBG.CFrame = cam.CFrame
            wait()
        end
    end)
end

local function stopFly()
    if flyBV then flyBV:Destroy() end
    if flyBG then flyBG:Destroy() end
    flyBV, flyBG = nil, nil
end

local function startNoclip()
    spawn(function()
        while noclipOn and LP.Character do
            for _, p in ipairs(LP.Character:GetDescendants()) do
                if p:IsA("BasePart") and p.CanCollide then p.CanCollide = false end
            end
            wait(0.2)
        end
    end)
end

local function startGodmode()
    spawn(function()
        while godmodeOn and LP.Character do
            local hum = LP.Character:FindFirstChildOfClass("Humanoid")
            if hum then
                hum.MaxHealth = math.huge
                hum.Health = math.huge
            end
            wait(0.2)
        end
    end)
end

local function startAntiVoid()
    spawn(function()
        while antiVoidOn and LP.Character do
            local hrp = LP.Character:FindFirstChild("HumanoidRootPart")
            if hrp and hrp.Position.Y < -50 then
                hrp.CFrame = CFrame.new(0, 50, 0)
            end
            wait(0.5)
        end
    end)
end

local function startAutoJump()
    spawn(function()
        while autoJumpOn and LP.Character do
            local hum = LP.Character:FindFirstChildOfClass("Humanoid")
            if hum then hum.Jump = true end
            wait(0.3)
        end
    end)
end

local function makeSuperRing()
    local char = LP.Character
    local hrp = char and char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    pcall(function()
        local ring = Instance.new("Part")
        ring.Shape = Enum.PartType.Ball
        ring.Size = Vector3.new(15, 15, 15)
        ring.Material = Enum.Material.ForceField
        ring.Color = Color3.fromRGB(0, 200, 255)
        ring.Transparency = 0.3
        ring.CanCollide = false
        ring.Parent = char
        local weld = Instance.new("WeldConstraint")
        weld.Part0 = ring
        weld.Part1 = hrp
        weld.Parent = ring
        playSound(SOUNDS.C00lkiddBoom, 6, 1)
    end)
end

local function setSpeed(sp)
    local hum = LP.Character and LP.Character:FindFirstChildOfClass("Humanoid")
    if hum then hum.WalkSpeed = sp end
end

local function setJump(jp)
    local hum = LP.Character and LP.Character:FindFirstChildOfClass("Humanoid")
    if hum then hum.UseJumpPower = true; hum.JumpPower = jp end
end

local espConns = {}
local function startESP()
    pcall(function()
        for _, p in ipairs(Players:GetPlayers()) do
            if p ~= LP then
                local function onChar(char)
                    local hrp = char:WaitForChild("HumanoidRootPart", 3)
                    if not hrp then return end
                    local bb = Instance.new("BillboardGui")
                    bb.Size = UDim2.new(0, 60, 0, 20)
                    bb.StudsOffset = Vector3.new(0, 3, 0)
                    bb.AlwaysOnTop = true
                    bb.Parent = hrp
                    local txt = Instance.new("TextLabel", bb)
                    txt.Size = UDim2.new(1, 0, 1, 0)
                    txt.BackgroundTransparency = 1
                    txt.TextColor3 = C.Main
                    txt.TextStrokeTransparency = 0
                    txt.TextStrokeColor3 = Color3.new(0, 0, 0)
                    txt.Font = Enum.Font.SourceSansBold
                    txt.TextSize = 14
                    txt.Text = "🎯 " .. p.Name
                end
                if p.Character then onChar(p.Character) end
                table.insert(espConns, p.CharacterAdded:Connect(onChar))
            end
        end
    end)
end

local function stopESP()
    for _, c in ipairs(espConns) do pcall(function() c:Disconnect() end) end
    espConns = {}
    for _, p in ipairs(Players:GetPlayers()) do
        if p.Character then
            local hrp = p.Character:FindFirstChild("HumanoidRootPart")
            if hrp then
                local bbg = hrp:FindFirstChildOfClass("BillboardGui")
                if bbg then bbg:Destroy() end
            end
        end
    end
end

-- ============ EMOTE ============
local originalC0, originalC1 = {}, {}

local function savePose()
    local char = LP.Character
    if not char then return end
    local torso = char:FindFirstChild("Torso") or char:FindFirstChild("UpperTorso")
    if not torso then return end
    originalC0, originalC1 = {}, {}
    for _, name in ipairs({"Right Shoulder", "Left Shoulder", "Neck"}) do
        local m = torso:FindFirstChild(name)
        if m and m:IsA("Motor6D") then
            originalC0[name] = m.C0
            originalC1[name] = m.C1
        end
    end
end

local function emotePrayerRight()
    savePose()
    local char = LP.Character
    if not char then return end
    local torso = char:FindFirstChild("Torso") or char:FindFirstChild("UpperTorso")
    if not torso then return end
    local rS, lS, neck = torso:FindFirstChild("Right Shoulder"), torso:FindFirstChild("Left Shoulder"), torso:FindFirstChild("Neck")
    if rS and rS:IsA("Motor6D") then
        rS.C0 = CFrame.new(0.6, 0.2, -0.3) * CFrame.Angles(math.rad(90), math.rad(-30), math.rad(-20))
    end
    if lS and lS:IsA("Motor6D") then
        lS.C0 = CFrame.new(-0.6, 0.2, -0.3) * CFrame.Angles(math.rad(90), math.rad(30), math.rad(20))
    end
    if neck and neck:IsA("Motor6D") then
        neck.C0 = CFrame.new(0, 1.5, 0) * CFrame.Angles(0, 0, math.rad(35))
    end
end

local function emotePrayerLeft()
    savePose()
    local char = LP.Character
    if not char then return end
    local torso = char:FindFirstChild("Torso") or char:FindFirstChild("UpperTorso")
    if not torso then return end
    local rS, lS, neck = torso:FindFirstChild("Right Shoulder"), torso:FindFirstChild("Left Shoulder"), torso:FindFirstChild("Neck")
    if rS and rS:IsA("Motor6D") then
        rS.C0 = CFrame.new(0.6, 0.2, -0.3) * CFrame.Angles(math.rad(90), math.rad(-30), math.rad(-20))
    end
    if lS and lS:IsA("Motor6D") then
        lS.C0 = CFrame.new(-0.6, 0.2, -0.3) * CFrame.Angles(math.rad(90), math.rad(30), math.rad(20))
    end
    if neck and neck:IsA("Motor6D") then
        neck.C0 = CFrame.new(0, 1.5, 0) * CFrame.Angles(0, 0, math.rad(-35))
    end
end

local function emoteReset()
    local char = LP.Character
    if not char then return end
    local torso = char:FindFirstChild("Torso") or char:FindFirstChild("UpperTorso")
    if not torso then return end
    for name, c0 in pairs(originalC0) do
        local m = torso:FindFirstChild(name)
        if m and m:IsA("Motor6D") then m.C0 = c0 end
    end
    for name, c1 in pairs(originalC1) do
        local m = torso:FindFirstChild(name)
        if m and m:IsA("Motor6D") then m.C1 = c1 end
    end
end

local headLoopConn
local function startHeadLoop()
    if headLoopConn then headLoopConn:Disconnect() end
    local toggle = false
    headLoopConn = RS.Heartbeat:Connect(function()
        if not emoteHandsOn then return end
        toggle = not toggle
        local char = LP.Character
        if not char then return end
        local torso = char:FindFirstChild("Torso") or char:FindFirstChild("UpperTorso")
        if not torso then return end
        local neck = torso:FindFirstChild("Neck")
        if neck and neck:IsA("Motor6D") then
            neck.C0 = CFrame.new(0, 1.5, 0) * CFrame.Angles(0, 0, toggle and math.rad(35) or math.rad(-35))
        end
    end)
end

-- ============ SKYBOX & DECAL ============
local SkyboxFolder = Instance.new("Folder", WS)
SkyboxFolder.Name = "ZAB_Skybox"

local function clearSkybox()
    for _, c in ipairs(SkyboxFolder:GetChildren()) do c:Destroy() end
end

local function applySkybox1()
    clearSkybox()
    local ZAB_IMAGE = "rbxassetid://0"
    pcall(function()
        local sky = Lighting:FindFirstChild("ZAB_Sky1") or Instance.new("Sky", Lighting)
        sky.Name = "ZAB_Sky1"
        sky.SkyboxBk = ZAB_IMAGE
        sky.SkyboxDn = ZAB_IMAGE
        sky.SkyboxFt = ZAB_IMAGE
        sky.SkyboxLf = ZAB_IMAGE
        sky.SkyboxRt = ZAB_IMAGE
        sky.SkyboxUp = ZAB_IMAGE
        sky.SunAngularSize = 0
        sky.MoonAngularSize = 0
    end)

    local textParts = {
        {text = "ZAB", pos = Vector3.new(0, 400, -400), color = C.Main},
        {text = "JOIN", pos = Vector3.new(-300, 400, 0), color = C.Gold},
        {text = "TODAY", pos = Vector3.new(0, 400, 400), color = C.Cyan},
    }

    for _, info in ipairs(textParts) do
        local p = Instance.new("Part")
        p.Size = Vector3.new(1, 1, 1)
        p.Position = info.pos
        p.Anchored = true
        p.CanCollide = false
        p.Transparency = 1
        p.Parent = SkyboxFolder

        local sgu = Instance.new("SurfaceGui", p)
        sgu.Face = Enum.NormalId.Front
        sgu.CanvasSize = Vector2.new(2000, 500)
        sgu.LightInfluence = 0
        sgu.AlwaysOnTop = true

        local txt = Instance.new("TextLabel", sgu)
        txt.Size = UDim2.new(1, 0, 1, 0)
        txt.BackgroundTransparency = 1
        txt.Text = info.text
        txt.TextColor3 = info.color
        txt.TextStrokeTransparency = 0
        txt.TextStrokeColor3 = Color3.new(0, 0, 0)
        txt.Font = Enum.Font.GothamBlack
        txt.TextScaled = true
    end

    pcall(function()
        local sphere = Instance.new("Part")
        sphere.Shape = Enum.PartType.Ball
        sphere.Size = Vector3.new(2000, 2000, 2000)
        sphere.Position = Vector3.new(0, 400, 0)
        sphere.Anchored = true
        sphere.CanCollide = false
        sphere.Transparency = 0.7
        sphere.Color = C.Void
        sphere.Material = Enum.Material.Neon
        sphere.Parent = SkyboxFolder
    end)

    Lighting.FogColor = Color3.fromRGB(100, 0, 0)
    Lighting.Ambient = Color3.fromRGB(80, 20, 20)
    notify("🌌", "Skybox 1 ON")
end

local function applySkybox2()
    clearSkybox()
    local userId = LP.UserId
    local avatarUrl = "rbxthumb://type=AvatarHeadShot&id=" .. userId .. "&w=420&h=420"

    pcall(function()
        local sphere = Instance.new("Part")
        sphere.Shape = Enum.PartType.Ball
        sphere.Size = Vector3.new(1500, 1500, 1500)
        sphere.Position = Vector3.new(0, 300, 0)
        sphere.Anchored = true
        sphere.CanCollide = false
        sphere.Transparency = 0.2
        sphere.Parent = SkyboxFolder

        local sgu = Instance.new("SurfaceGui", sphere)
        sgu.Face = Enum.NormalId.Front
        sgu.CanvasSize = Vector2.new(1500, 1500)
        sgu.LightInfluence = 0
        sgu.AlwaysOnTop = true

        local img = Instance.new("ImageLabel", sgu)
        img.Size = UDim2.new(1, 0, 1, 0)
        img.BackgroundTransparency = 1
        img.Image = avatarUrl
        img.ScaleType = Enum.ScaleType.Fit
    end)

    local nameP = Instance.new("Part")
    nameP.Size = Vector3.new(1, 1, 1)
    nameP.Position = Vector3.new(0, 700, 0)
    nameP.Anchored = true
    nameP.CanCollide = false
    nameP.Transparency = 1
    nameP.Parent = SkyboxFolder

    local nSgu = Instance.new("SurfaceGui", nameP)
    nSgu.Face = Enum.NormalId.Bottom
    nSgu.CanvasSize = Vector2.new(1500, 300)
    nSgu.LightInfluence = 0    nSgu.AlwaysOnTop = true

    local nTxt = Instance.new("TextLabel", nSgu)
    nTxt.Size = UDim2.new(1, 0, 1, 0)
    nTxt.BackgroundTransparency = 1
    nTxt.Text = "★ " .. LP.DisplayName .. " ★"
    nTxt.TextColor3 = C.Gold
    nTxt.TextStrokeTransparency = 0
    nTxt.Font = Enum.Font.GothamBlack
    nTxt.TextScaled = true

    Lighting.FogColor = Color3.fromRGB(50, 20, 80)
    Lighting.Ambient = Color3.fromRGB(40, 20, 60)
    notify("🌌", "Skybox 2 ON")
end

local function removeSkybox()
    clearSkybox()
    pcall(function()
        local s1 = Lighting:FindFirstChild("ZAB_Sky1")
        if s1 then s1:Destroy() end
        local s2 = Lighting:FindFirstChild("ZAB_Sky2")
        if s2 then s2:Destroy() end
    end)
    Lighting.FogColor = Color3.fromRGB(192, 192, 192)
    Lighting.FogEnd = 100000
    Lighting.Ambient = Color3.fromRGB(70, 70, 70)
    notify("🌌", "Skybox removed")
end

local DECAL_LIST = {
    "rbxassetid://90089940136467",
    "rbxassetid://75793040119604",
    "rbxassetid://89376395986302",
    "rbxassetid://9046339732",
    "rbxassetid://1837879082",
}

local decalSpamConn
local function startDecalSpam()
    decalSpamOn = true
    if decalSpamConn then decalSpamConn:Disconnect() end
    decalSpamConn = RS.Heartbeat:Connect(function()
        if not decalSpamOn then return end
        for _, obj in ipairs(WS:GetDescendants()) do
            if obj:IsA("BasePart") and obj.Name ~= "Handle" then
                pcall(function()
                    local existing = obj:FindFirstChild("ZAB_Decal")
                    if not existing then
                        local d = Instance.new("Decal")
                        d.Name = "ZAB_Decal"
                        d.Texture = DECAL_LIST[math.random(1, #DECAL_LIST)]
                        d.Face = Enum.NormalId[({"Front", "Back", "Top", "Bottom", "Left", "Right"})[math.random(1, 6)]]
                        d.Parent = obj
                    else
                        existing.Texture = DECAL_LIST[math.random(1, #DECAL_LIST)]
                    end
                end)
            end
        end
    end)
end

local function stopDecalSpam()
    decalSpamOn = false
    if decalSpamConn then decalSpamConn:Disconnect() end
    for _, obj in ipairs(WS:GetDescendants()) do
        if obj:IsA("BasePart") then
            local d = obj:FindFirstChild("ZAB_Decal")
            if d then d:Destroy() end
        end
    end
end

-- ============ PIRATE & CONTROL ============
local AnchorFolder = Instance.new("Folder", WS)
AnchorFolder.Name = "ZAB_Anchor"
local AnchorPart = Instance.new("Part", AnchorFolder)
AnchorPart.Anchored = true
AnchorPart.CanCollide = false
AnchorPart.Transparency = 1
AnchorPart.Size = Vector3.new(1, 1, 1)
AnchorPart.CFrame = CFrame.new(0, 500, 0)
local AnchorAttach = Instance.new("Attachment", AnchorPart)

if not getgenv().ZAB_Net then getgenv().ZAB_Net = {Parts = {}, Active = false} end

local function Manipulate(v)
    if not v or not v.Parent or not v:IsA("BasePart") or v.Anchored then return end
    if v:IsDescendantOf(LP.Character) then return end
    local parent = v.Parent
    if parent and parent:FindFirstChildOfClass("Humanoid") then return end
    if v.Name == "Handle" or v.Name == "AnchorPart" then return end
    pcall(function()
        v.CanCollide = false
        v:SetNetworkOwner(LP)
        if not table.find(getgenv().ZAB_Net.Parts, v) then
            table.insert(getgenv().ZAB_Net.Parts, v)
        end
        local att = v:FindFirstChild("ZB_Att") or Instance.new("Attachment", v)
        att.Name = "ZB_Att"
        local align = v:FindFirstChild("ZB_Align") or Instance.new("AlignPosition", v)
        align.Name = "ZB_Align"
        align.Attachment0 = att
        align.Attachment1 = AnchorAttach
        align.MaxForce = math.huge
        align.MaxVelocity = math.huge
        align.Responsiveness = 500
    end)
end

local function clearAllParts()
    for i = #getgenv().ZAB_Net.Parts, 1, -1 do
        local p = getgenv().ZAB_Net.Parts[i]
        if p and p.Parent then
            pcall(function()
                local a = p:FindFirstChild("ZB_Align"); if a then a:Destroy() end
                local at = p:FindFirstChild("ZB_Att"); if at then at:Destroy() end
            end)
        end
        table.remove(getgenv().ZAB_Net.Parts, i)
    end
end

local ControlFolder = Instance.new("Folder", WS)
ControlFolder.Name = "ZAB_Control"
local ControlPart = Instance.new("Part", ControlFolder)
ControlPart.Anchored = true
ControlPart.Transparency = 1
ControlPart.CanCollide = false
local ControlAttachment = Instance.new("Attachment", ControlPart)

if not getgenv().ZAB_ControlNet then getgenv().ZAB_ControlNet = {Parts = {}} end

local function ForceControlPart(v)
    if v:IsA("BasePart") and not v.Anchored
    and not (v.Parent and v.Parent:FindFirstChildOfClass("Humanoid"))
    and v.Name ~= "Handle" and not (v.Parent and v.Parent:IsA("Tool"))
    and not v:IsDescendantOf(LP.Character) then
        pcall(function()
            v.CanCollide = false
            if not table.find(getgenv().ZAB_ControlNet.Parts, v) then
                table.insert(getgenv().ZAB_ControlNet.Parts, v)
            end
            local att = v:FindFirstChild("Z_Att") or Instance.new("Attachment", v)
            att.Name = "Z_Att"
            local align = v:FindFirstChild("Z_Align") or Instance.new("AlignPosition", v)
            align.Name = "Z_Align"
            align.Attachment0 = att
            align.Attachment1 = ControlAttachment
            align.MaxForce = math.huge
            align.MaxVelocity = math.huge
            align.Responsiveness = 500
        end)
    end
end

local controlTargetPlayer, controlRenderConn
local function startControlRoom()
    controlRoomOn = true
    if controlRenderConn then controlRenderConn:Disconnect() end
    controlRenderConn = RS.RenderStepped:Connect(function()
        if not controlRoomOn then return end
        if controlTargetPlayer and controlTargetPlayer.Character then
            local root = controlTargetPlayer.Character:FindFirstChild("HumanoidRootPart")
            if root then
                ControlAttachment.WorldPosition = root.Position + Vector3.new(math.random(-1, 1), 0, math.random(-1, 1))
            end
        end
    end)
    spawn(function()
        while controlRoomOn do
            for _, v in ipairs(WS:GetDescendants()) do
                if v:IsA("BasePart") and not v.Anchored then ForceControlPart(v) end
            end
            wait(1.5)
        end
    end)
end

local function stopControlRoom()
    controlRoomOn = false
    if controlRenderConn then controlRenderConn:Disconnect() end
    for _, p in ipairs(getgenv().ZAB_ControlNet.Parts) do
        if p and p.Parent then
            pcall(function()
                local a = p:FindFirstChild("Z_Align"); if a then a:Destroy() end
                local at = p:FindFirstChild("Z_Att"); if at then at:Destroy() end
            end)
        end
    end
    getgenv().ZAB_ControlNet.Parts = {}
end

-- ============ GUI ============
local sg = Instance.new("ScreenGui")
sg.Name = "ZAB_MEGA_V51"
sg.ResetOnSpawn = false
sg.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
pcall(function() sg.IgnoreGuiInset = true end)
sg.Parent = GuiParent

local main = Instance.new("Frame", sg)
main.Size = UDim2.new(0, 300, 0, 420)
main.Position = UDim2.new(0.5, -150, 0.5, -210)
main.BackgroundColor3 = C.Void
main.BorderSizePixel = 2
main.BorderColor3 = C.Main
main.Active = true

local titleBar = Instance.new("Frame", main)
titleBar.Size = UDim2.new(1, 0, 0, 30)
titleBar.BackgroundColor3 = C.Deep
titleBar.BorderSizePixel = 2
titleBar.BorderColor3 = C.Main

local titleTxt = Instance.new("TextLabel", titleBar)
titleTxt.Size = UDim2.new(1, -70, 1, 0)
titleTxt.Position = UDim2.new(0, 6, 0, 0)
titleTxt.BackgroundTransparency = 1
titleTxt.Text = "💀 ZAB v51"
titleTxt.TextColor3 = C.Bright
titleTxt.Font = Enum.Font.SourceSansBold
titleTxt.TextSize = 12
titleTxt.TextXAlignment = Enum.TextXAlignment.Left

local hideBtn = Instance.new("TextButton", titleBar)
hideBtn.Size = UDim2.new(0, 22, 0, 22)
hideBtn.Position = UDim2.new(1, -50, 0, 4)
hideBtn.BackgroundColor3 = C.Dark
hideBtn.BorderSizePixel = 2
hideBtn.BorderColor3 = C.Main
hideBtn.Text = "—"
hideBtn.TextColor3 = C.Bright
hideBtn.Font = Enum.Font.SourceSansBold
hideBtn.TextSize = 12

local closeBtn = Instance.new("TextButton", titleBar)
closeBtn.Size = UDim2.new(0, 22, 0, 22)
closeBtn.Position = UDim2.new(1, -26, 0, 4)
closeBtn.BackgroundColor3 = C.Dark
closeBtn.BorderSizePixel = 2
closeBtn.BorderColor3 = C.Main
closeBtn.Text = "X"
closeBtn.TextColor3 = C.Bright
closeBtn.Font = Enum.Font.SourceSansBold
closeBtn.TextSize = 12

-- ============ TAB SYSTEM ============
local tabBar = Instance.new("Frame", main)
tabBar.Size = UDim2.new(1, -8, 0, 22)
tabBar.Position = UDim2.new(0, 4, 0, 34)
tabBar.BackgroundColor3 = C.Panel
tabBar.BorderSizePixel = 1
tabBar.BorderColor3 = C.Main

local tabList = Instance.new("UIListLayout", tabBar)
tabList.FillDirection = Enum.FillDirection.Horizontal
tabList.Padding = UDim.new(0, 2)
tabList.HorizontalAlignment = Enum.HorizontalAlignment.Left

local tabPad = Instance.new("UIPadding", tabBar)
tabPad.PaddingLeft = UDim.new(0, 2)
tabPad.PaddingTop = UDim.new(0, 2)

local content = Instance.new("ScrollingFrame", main)
content.Size = UDim2.new(1, -8, 1, -66)
content.Position = UDim2.new(0, 4, 0, 60)
content.BackgroundColor3 = Color3.fromRGB(20, 5, 5)
content.BorderSizePixel = 2
content.BorderColor3 = C.Main
content.ScrollBarThickness = 4
content.ScrollBarImageColor3 = C.Main
content.CanvasSize = UDim2.new(0, 0, 0, 500)

local uiList = Instance.new("UIListLayout", content)
uiList.Padding = UDim.new(0, 3)
local uiPad = Instance.new("UIPadding", content)
uiPad.PaddingTop = UDim.new(0, 3)
uiPad.PaddingLeft = UDim.new(0, 3)
uiPad.PaddingRight = UDim.new(0, 3)

local tabPages = {}
local currentTab = nil

local function switchTab(name)
    currentTab = name
    for tn, page in pairs(tabPages) do
        page.Visible = (tn == name)
    end
    for _, b in ipairs(tabBar:GetChildren()) do
        if b:IsA("TextButton") then
            if b.Name == name then
                b.BackgroundColor3 = C.Main
                b.TextColor3 = C.Text
            else
                b.BackgroundColor3 = C.Panel
                b.TextColor3 = C.Dim
            end
        end
    end
end

local function makeTab(name, label)
    local page = Instance.new("ScrollingFrame", main)
    page.Name = name
    page.Size = UDim2.new(1, -8, 1, -66)
    page.Position = UDim2.new(0, 4, 0, 60)
    page.BackgroundColor3 = Color3.fromRGB(20, 5, 5)
    page.BorderSizePixel = 2
    page.BorderColor3 = C.Main
    page.ScrollBarThickness = 4
    page.ScrollBarImageColor3 = C.Main
    page.CanvasSize = UDim2.new(0, 0, 0, 500)
    page.Visible = false

    local pList = Instance.new("UIListLayout", page)
    pList.Padding = UDim.new(0, 3)
    local pPad = Instance.new("UIPadding", page)
    pPad.PaddingTop = UDim.new(0, 3)
    pPad.PaddingLeft = UDim.new(0, 3)
    pPad.PaddingRight = UDim.new(0, 3)

    tabPages[name] = page

    local btn = Instance.new("TextButton", tabBar)
    btn.Name = name
    btn.Size = UDim2.new(0, 60, 0, 18)
    btn.BackgroundColor3 = C.Panel
    btn.BorderSizePixel = 0
    btn.Text = label
    btn.TextColor3 = C.Dim
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 9
    btn.AutoButtonColor = false
    btn.MouseButton1Click:Connect(function() switchTab(name) end)

    return page, pList
end

-- ============ BUTTON HELPERS (COMPACT GRID) ============
local function makeSection(parent, txt)
    local l = Instance.new("TextLabel", parent)
    l.Size = UDim2.new(1, 0, 0, 20)
    l.BackgroundColor3 = C.Deep
    l.BorderSizePixel = 1
    l.BorderColor3 = C.Main
    l.Text = "▸ " .. txt
    l.TextColor3 = C.Bright
    l.Font = Enum.Font.SourceSansBold
    l.TextSize = 10
    l.TextXAlignment = Enum.TextXAlignment.Left
    local p = Instance.new("UIPadding", l)
    p.PaddingLeft = UDim.new(0, 5)
end

local function makeBtn(parent, txt, cb, color)
    local b = Instance.new("TextButton", parent)
    b.Size = UDim2.new(1, 0, 0, 24)
    b.BackgroundColor3 = C.Panel
    b.BorderSizePixel = 1
    b.BorderColor3 = C.Dark
    b.Text = "▶ " .. txt
    b.TextColor3 = color or C.Bright
    b.Font = Enum.Font.SourceSansBold
    b.TextSize = 10
    b.AutoButtonColor = false
    b.TextXAlignment = Enum.TextXAlignment.Left
    local p = Instance.new("UIPadding", b)
    p.PaddingLeft = UDim.new(0, 5)
    b.MouseEnter:Connect(function()
        b.BorderColor3 = C.Main
        b.BackgroundColor3 = C.Deep
    end)
    b.MouseLeave:Connect(function()
        b.BorderColor3 = C.Dark
        b.BackgroundColor3 = C.Panel
    end)
    b.MouseButton1Click:Connect(cb)
    return b
end

-- GRID: 3 tombol per baris
local function makeGridRow(parent)
    local row = Instance.new("Frame", parent)
    row.Size = UDim2.new(1, 0, 0, 24)
    row.BackgroundTransparency = 1
    local g = Instance.new("UIListLayout", row)
    g.FillDirection = Enum.FillDirection.Horizontal
    g.Padding = UDim.new(0, 3)
    return row
end

local function makeGridBtn(row, txt, cb, color)
    local b = Instance.new("TextButton", row)
    b.Size = UDim2.new(0.32, 0, 1, 0)
    b.BackgroundColor3 = C.Panel
    b.BorderSizePixel = 1
    b.BorderColor3 = C.Dark
    b.Text = txt
    b.TextColor3 = color or C.Bright
    b.Font = Enum.Font.SourceSansBold
    b.TextSize = 9
    b.AutoButtonColor = false
    b.MouseEnter:Connect(function()
        b.BorderColor3 = C.Main
        b.BackgroundColor3 = C.Deep
    end)
    b.MouseLeave:Connect(function()
        b.BorderColor3 = C.Dark
        b.BackgroundColor3 = C.Panel
    end)
    b.MouseButton1Click:Connect(cb)
    return b
end

-- ============ TAB 1: MAIN ============
local mainPage, mainList = makeTab("Main", "MAIN")

makeSection(mainPage, "🎵 LAGU TIKTOK")
makeBtn(mainPage, "Spooky Scary Skeletons", function() playSound(SOUNDS.SpookyScarySkeletons, 7, 1) end, C.Main)
makeBtn(mainPage, "HOLY WAR FUNK", function() playSound(SOUNDS.HolyWarFunk, 7, 1) end, C.Gold)
makeBtn(mainPage, "JELLYBEAN SMOKE", function() playSound(SOUNDS.JellybeanSmoke, 7, 1) end, C.Purple)

makeSection(mainPage, "🙏 EMOTE")
makeBtn(mainPage, "Salip + Kepala Kanan", function() emotePrayerRight() end, C.Gold)
makeBtn(mainPage, "Salip + Kepala Kiri", function() emotePrayerLeft() end, C.Gold)
makeBtn(mainPage, "Reset Emote", function() emoteReset() end, C.Dim)
local headLoopBtn = makeBtn(mainPage, "Kepala Goyang: OFF", function()
    emoteHandsOn = not emoteHandsOn
    headLoopBtn.Text = "▶ Kepala Goyang: " .. (emoteHandsOn and "ON" or "OFF")
    if emoteHandsOn then
        startHeadLoop()
        emotePrayerRight()
    elseif headLoopConn then
        headLoopConn:Disconnect()
    end
end, C.Cyan)

makeSection(mainPage, "🏃 MOVEMENT")
makeBtn(mainPage, "FLING: OFF", function() flingOn = not flingOn; if flingOn then startFling() end end, C.Main)
makeBtn(mainPage, "FLY: OFF", function() flyOn = not flyOn; if flyOn then startFly() else stopFly() end end, C.Cyan)
makeBtn(mainPage, "NOCLIP: OFF", function() noclipOn = not noclipOn; if noclipOn then startNoclip() end end, C.Purple)
makeBtn(mainPage, "GODMODE: OFF", function() godmodeOn = not godmodeOn; if godmodeOn then startGodmode() end end, C.Green)
makeBtn(mainPage, "ANTI-VOID: OFF", function() antiVoidOn = not antiVoidOn; if antiVoidOn then startAntiVoid() end end, C.Blue)
makeBtn(mainPage, "AUTO JUMP: OFF", function() autoJumpOn = not autoJumpOn; if autoJumpOn then startAutoJump() end end, C.Gold)
makeBtn(mainPage, "ESP: OFF", function() espOn = not espOn; if espOn then startESP() else stopESP() end end, C.Pink)
makeBtn(mainPage, "Super Ring", function() makeSuperRing() end, C.Cyan)

makeBtn(mainPage, "Speed +50", function() setSpeed(50) end, C.Gold)
makeBtn(mainPage, "Speed +100", function() setSpeed(100) end, C.Gold)
makeBtn(mainPage, "Speed Reset", function() setSpeed(16) end, C.Dim)
makeBtn(mainPage, "Jump +100", function() setJump(100) end, C.Gold)
makeBtn(mainPage, "Jump Reset", function() setJump(50) end, C.Dim)

-- ============ TAB 2: SOUND ============
local soundPage, soundList = makeTab("Sound", "SOUND")

makeSection(soundPage, "💀 C00LKIDD")
makeBtn(soundPage, "C00lkidd Theme", function() playSound(SOUNDS.C00lkiddTheme, 6, 1) end, C.Main)
makeBtn(soundPage, "C00lkidd Laugh", function() playSound(SOUNDS.C00lkiddLaugh, 6, 0.8) end, C.Main)
makeBtn(soundPage, "C00lkidd Scream", function() playSound(SOUNDS.C00lkiddScream, 6, 0.9) end, C.Main)

makeSection(soundPage, "🧊 CUBER")
makeBtn(soundPage, "Cuber 1", function() playSound(SOUNDS.Cuber1, 6, 1) end, C.Cyan)
makeBtn(soundPage, "Cuber 2", function() playSound(SOUNDS.Cuber2, 6, 1) end, C.Cyan)
makeBtn(soundPage, "Cuber 3", function() playSound(SOUNDS.Cuber3, 6, 1) end, C.Cyan)

makeSection(soundPage, "🧠 BRAINROT")
makeBtn(soundPage, "Skibidi", function() playSound(SOUNDS.Skibidi, 6, 1) end, C.Pink)
makeBtn(soundPage, "Sus 😳", function() playSound(SOUNDS.Sus, 6, 1) end, C.Pink)
makeBtn(soundPage, "Bruh", function() playSound(SOUNDS.Bruh, 6, 1) end, C.Purple)
makeBtn(soundPage, "Oh No", function() playSound(SOUNDS.OhNo, 6, 1) end, C.Purple)
makeBtn(soundPage, "Metal Pipe", function() playSound(SOUNDS.MetalPipe, 7, 1) end, C.Gold)
makeBtn(soundPage, "Fart 😂", function() playSound(SOUNDS.Fart, 6, 1) end, C.Green)
makeBtn(soundPage, "Vine Boom", function() playSound(SOUNDS.VineBoom, 7, 1) end, C.Gold)
makeBtn(soundPage, "Roblox Oof", function() playSound(SOUNDS.RobloxOof, 6, 1) end, C.Gold)
makeBtn(soundPage, "Sad Violin", function() playSound(SOUNDS.SadViolin, 6, 1) end, C.Dim)
makeBtn(soundPage, "Emotional Damage", function() playSound(SOUNDS.EmoDamage, 6, 1) end, C.Pink)

makeSection(soundPage, "👻 HORROR")
makeBtn(soundPage, "Skeleton Horror", function() playSound(SOUNDS.SkeletonHorror, 7, 0.7) end, C.Main)
makeBtn(soundPage, "Skeleton Spooky", function() playSound(SOUNDS.SkeletonSpooky, 6, 1.2) end, C.Purple)
makeBtn(soundPage, "Ghost", function() playSound(SOUNDS.Ghost, 6, 1) end, C.Purple)
makeBtn(soundPage, "Zombie", function() playSound(SOUNDS.Zombie, 6, 1) end, C.Green)

makeSection(soundPage, "💥 EFFECT")
makeBtn(soundPage, "Thunder", function() playSound(SOUNDS.Thunder, 7, 1) end, C.Blue)
makeBtn(soundPage, "Explosion", function() playSound(SOUNDS.Explosion, 7, 1) end, C.Gold)
makeBtn(soundPage, "Nuke", function() playSound(SOUNDS.Nuke, 8, 1) end, C.Main)
makeBtn(soundPage, "🎲 RANDOM", function()
    local keys = {}
    for k in pairs(SOUNDS) do table.insert(keys, k) end
    local pick = keys[math.random(1, #keys)]
    playSound(SOUNDS[pick], 6, 1)
    notify("🎲", pick)
end, C.Gold)

-- ============ TAB 3: SKYBOX (GRID) ============
local skyPage, skyList = makeTab("Sky", "SKYBOX")

makeSection(skyPage, "🌌 SKYBOX (pilih 1)")

local skyRow1 = makeGridRow(skyPage)
makeGridBtn(skyRow1, "S1: ZAB", function() applySkybox1() end, C.Main)
makeGridBtn(skyRow1, "S2: Avatar", function() applySkybox2() end, C.Gold)
makeGridBtn(skyRow1, "OFF", function() removeSkybox() end, C.Dim)

makeSection(skyPage, "📝 Deskripsi")
local skyDesc = Instance.new("TextLabel", skyPage)
skyDesc.Size = UDim2.new(1, 0, 0, 50)
skyDesc.BackgroundColor3 = C.Panel
skyDesc.BorderSizePixel = 1
skyDesc.BorderColor3 = C.Dark
skyDesc.TextColor3 = C.Dim
skyDesc.Font = Enum.Font.Code
skyDesc.TextSize = 9
skyDesc.TextXAlignment = Enum.TextXAlignment.Left
skyDesc.TextYAlignment = Enum.TextYAlignment.Top
skyDesc.TextWrapped = true
skyDesc.Text = "S1: Tulisan ZAB JOIN TODAY di langit\nS2: Avatar kamu otomatis\nOFF: Hapus semua skybox"
local skyPad = Instance.new("UIPadding", skyDesc)
skyPad.PaddingTop = UDim.new(0, 3)
skyPad.PaddingLeft = UDim.new(0, 4)

makeSection(skyPage, "🌫️ FOG / LIGHTING")
local fogRow = makeGridRow(skyPage)
makeGridBtn(fogRow, "Red", function()
    Lighting.FogColor = Color3.fromRGB(150, 0, 0)
    Lighting.Ambient = Color3.fromRGB(100, 20, 20)
end, C.Main)
makeGridBtn(fogRow, "Purple", function()
    Lighting.FogColor = Color3.fromRGB(80, 0, 120)
    Lighting.Ambient = Color3.fromRGB(60, 20, 100)
end, C.Purple)
makeGridBtn(fogRow, "Black", function()
    Lighting.FogColor = Color3.fromRGB(0, 0, 0)
    Lighting.Ambient = Color3.fromRGB(0, 0, 0)
end, C.Dim)

-- ============ TAB 4: DECAL (GRID) ============
local decalPage, decalList = makeTab("Decal", "DECAL")

makeSection(decalPage, "🎨 DECAL SPAM")

local decalRow1 = makeGridRow(decalPage)
makeGridBtn(decalRow1, "SPAM ON", function() startDecalSpam() end, C.Green)
makeGridBtn(decalRow1, "SPAM OFF", function() stopDecalSpam() end, C.Main)
makeGridBtn(decalRow1, "CLEAR", function()
    for _, obj in ipairs(WS:GetDescendants()) do
        if obj:IsA("BasePart") then
            local d = obj:FindFirstChild("ZAB_Decal")
            if d then d:Destroy() end
        end
    end
end, C.Dim)

makeSection(decalPage, "➕ TAMBAH DECAL ID")
local decalInput = Instance.new("TextBox", decalPage)
decalInput.Size = UDim2.new(1, 0, 0, 26)
decalInput.BackgroundColor3 = C.Panel
decalInput.BorderSizePixel = 1
decalInput.BorderColor3 = C.Dark
decalInput.PlaceholderText = "Ketik ID decal lalu Enter"
decalInput.TextColor3 = C.Text
decalInput.PlaceholderColor3 = C.Dim
decalInput.Font = Enum.Font.Code
decalInput.TextSize = 11
decalInput.ClearTextOnFocus = false

decalInput.FocusLost:Connect(function(enter)
    if enter and decalInput.Text ~= "" then
        local id = decalInput.Text:gsub("%D", "")
        if id ~= "" then
            table.insert(DECAL_LIST, "rbxassetid://" .. id)
            notify("🎨", "Decal ditambah: " .. id)
            decalInput.Text = ""
        end
    end
end)

makeSection(decalPage, "📋 DECAL TERPASANG")
local decalCountLbl = Instance.new("TextLabel", decalPage)
decalCountLbl.Size = UDim2.new(1, 0, 0, 22)
decalCountLbl.BackgroundColor3 = C.Panel
decalCountLbl.BorderSizePixel = 1
decalCountLbl.BorderColor3 = C.Dark
decalCountLbl.TextColor3 = C.Cyan
decalCountLbl.Font = Enum.Font.Code
decalCountLbl.TextSize = 10
decalCountLbl.Text = "Total decal in list: " .. #DECAL_LIST

spawn(function()
    while sg.Parent do
        local count = 0
        for _, obj in ipairs(WS:GetDescendants()) do
            if obj:IsA("Decal") and obj.Name == "ZAB_Decal" then count = count + 1 end
        end
        pcall(function()
            decalCountLbl.Text = "Terpasang: " .. count .. " | ID list: " .. #DECAL_LIST
        end)
        wait(1)
    end
end)

-- ============ TAB 5: TOOLS ============
local toolPage, toolList = makeTab("Tools", "TOOLS")

makeSection(toolPage, "🏴‍☠️ PIRATE")
makeBtn(toolPage, "Activate Pirate: OFF", function()
    pirateOn = not pirateOn
    getgenv().ZAB_Net.Active = pirateOn
    if not pirateOn then clearAllParts() end
end, C.Purple)

makeSection(toolPage, "🎮 CONTROL ROOM")
local crBox = Instance.new("TextBox", toolPage)
crBox.Size = UDim2.new(1, 0, 0, 24)
crBox.BackgroundColor3 = C.Panel
crBox.BorderSizePixel = 1
crBox.BorderColor3 = C.Dark
crBox.PlaceholderText = "Target player..."
crBox.TextColor3 = C.Text
crBox.PlaceholderColor3 = C.Dim
crBox.Font = Enum.Font.Code
crBox.TextSize = 11
crBox.ClearTextOnFocus = false

crBox.FocusLost:Connect(function(enter)
    if not enter then return end
    local k = crBox.Text:lower()
    if k == "" then return end
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LP and (p.Name:lower():find(k) or p.DisplayName:lower():find(k)) then
            controlTargetPlayer = p
            crBox.Text = p.DisplayName
            notify("🎯", p.DisplayName)
            return
        end
    end
end)

makeBtn(toolPage, "Control Room: OFF", function()
    if controlRoomOn then
        stopControlRoom()
    else
        if not controlTargetPlayer then notify("⚠️", "Pilih target") return end
        startControlRoom()
    end
end, C.Green)

makeSection(toolPage, "⚔ AUTO ATTACK")
makeBtn(toolPage, "AUTO ATTACK: OFF", function()
    autoAttackOn = not autoAttackOn
    if autoAttackOn then startAutoAttack() end
end, C.Main)

makeSection(toolPage, "🔍 SCANNER")
makeBtn(toolPage, "Scan Remotes", function()
    local c = scanAllRemotes()
    notify("📡", c .. " remotes")
end, C.Cyan)
makeBtn(toolPage, "Print (F9)", function()
    print("═══ REMOTE LIST ═══")
    for i, r in ipairs(remotes) do print(i .. ". " .. r:GetFullName()) end
    print("═══════════════════")
end, C.Cyan)

makeSection(toolPage, "🛑 UTILITIES")
makeBtn(toolPage, "Kill Self", function()
    local hum = LP.Character and LP.Character:FindFirstChildOfClass("Humanoid")
    if hum then hum.Health = 0 end
end, C.Main)
makeBtn(toolPage, "Respawn", function() pcall(function() LP.Character:BreakJoints() end) end, C.Dim)
makeBtn(toolPage, "Rejoin", function()
    pcall(function() game:GetService("TeleportService"):Teleport(game.PlaceId, LP) end)
end, C.Pink)
makeBtn(toolPage, "Unload", function()
    pcall(function() sg:Destroy() end)
    if getgenv().ZabSrv51 then
        for _, c in pairs(getgenv().ZabSrv51) do pcall(function() c:Disconnect() end) end
    end
    clearAllParts()
    stopControlRoom()
    stopDecalSpam()
    removeSkybox()
end, C.Main)

-- ============ DRAG / HIDE / CLOSE ============
local dragging, dragStart, startPos
titleBar.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = main.Position
    end
end)
UIS.InputChanged:Connect(function(input)
    if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local d = input.Position - dragStart
        main.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + d.X, startPos.Y.Scale, startPos.Y.Offset + d.Y)
    end
end)
UIS.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)

local hidden = false
hideBtn.MouseButton1Click:Connect(function()
    hidden = not hidden
    if hidden then
        for _, p in pairs(tabPages) do p.Visible = false end
        tabBar.Visible = false
        main.Size = UDim2.new(0, 300, 0, 30)
    else
        tabBar.Visible = true
        switchTab(currentTab or "Main")
        main.Size = UDim2.new(0, 300, 0, 420)
    end
end)

UIS.InputBegan:Connect(function(input, gpe)
    if gpe then return end
    if input.KeyCode == Enum.KeyCode.RightControl then
        main.Visible = not main.Visible
    end
end)

closeBtn.MouseButton1Click:Connect(function() sg:Destroy() end)

-- Set tab awal
switchTab("Main")

-- ============ AUTO CANVAS ============
table.insert(getgenv().ZabSrv51, spawn(function()
    while sg.Parent do
        for _, page in pairs(tabPages) do
            pcall(function()
                local list = page:FindFirstChildOfClass("UIListLayout")
                if list then
                    page.CanvasSize = UDim2.new(0, 0, 0, list.AbsoluteContentSize.Y + 10)
                end
            end)
        end
        wait(0.5)
    end
end))

table.insert(getgenv().ZabSrv51, RS.Heartbeat:Connect(function()
    if getgenv().ZAB_Net.Active then
        for _, obj in ipairs(WS:GetDescendants()) do
            if obj:IsA("BasePart") and not obj.Anchored then Manipulate(obj) end
        end
    end
end))

table.insert(getgenv().ZabSrv51, LP.CharacterAdded:Connect(function()
    wait(1)
    if godmodeOn then startGodmode() end
    if noclipOn then startNoclip() end
    if antiVoidOn then startAntiVoid() end
    if autoJumpOn then startAutoJump() end
end))

notify("💀 ZAB v51", "Loaded! " .. totalRemotes .. " remotes")
print("═══ ZAB MEGA v51 ═══")
print("Credit: ZAB")
print("Password: ZABPRIVAT2026 / ZBNPRO999 / VIPZAB1212")
print("═══════════════════════")
