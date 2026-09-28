# Script-master-fishing-no-key-
Script master fishing no key
local code = [==[
--// DATBEO SCRIPT - FULL FINAL (11 NHẠC + TELE RESPAWN)
local Players    = game:GetService("Players")
local CoreGui    = game:GetService("CoreGui")
local Tween      = game:GetService("TweenService")
local VIM        = game:GetService("VirtualInputManager")
local Sound      = game:GetService("SoundService")
local P          = Players.LocalPlayer

if CoreGui:FindFirstChild("DatBeoGui") then CoreGui.DatBeoGui:Destroy() end

local S = Instance.new("ScreenGui")
S.Name = "DatBeoGui"
S.ResetOnSpawn = false
S.Parent = CoreGui

local C = {
    bg = Color3.fromRGB(15,15,20), bg2 = Color3.fromRGB(25,25,35),
    gold = Color3.fromRGB(255,200,60), cyan = Color3.fromRGB(0,220,255),
    grn = Color3.fromRGB(0,255,130), red = Color3.fromRGB(255,60,80),
    purple = Color3.fromRGB(180, 100, 255),
    dim = Color3.fromRGB(130,130,145),
}

local function corner(p,r) local c=Instance.new("UICorner",p); c.CornerRadius=UDim.new(0,r or 8) end
local function stroke(p,c,t) local s=Instance.new("UIStroke",p); s.Color=c or C.gold; s.Thickness=t or 1.5; s.Transparency=0.3; return s end
local function grad(p,c1,c2,r) local g=Instance.new("UIGradient",p); g.Color=ColorSequence.new(c1,c2); g.Rotation=r or 90 end

local function drag(f)
    local d,ds,sp
    f.InputBegan:Connect(function(i)
        if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then
            d=true; ds=i.Position; sp=f.Position
            i.Changed:Connect(function() if i.UserInputState==Enum.UserInputState.End then d=false end end)
        end
    end)
    f.InputChanged:Connect(function(i)
        if d and (i.UserInputType==Enum.UserInputType.MouseMovement or i.UserInputType==Enum.UserInputType.Touch) then
            local x=i.Position-ds
            f.Position=UDim2.new(sp.X.Scale,sp.X.Offset+x.X,sp.Y.Scale,sp.Y.Offset+x.Y)
        end
    end)
end

local function btn(parent,size,pos,text)
    local b=Instance.new("TextButton",parent)
    b.Size=size; b.Position=pos
    b.BackgroundColor3=Color3.fromRGB(30,30,40)
    b.BackgroundTransparency = 0.15
    b.TextColor3=Color3.fromRGB(220,220,230)
    b.TextSize=11; b.Font=Enum.Font.GothamBold; b.Text=text
    b.BorderSizePixel=0; b.AutoButtonColor=false
    b.ZIndex = 10
    corner(b,6)
    b.MouseEnter:Connect(function() Tween:Create(b,TweenInfo.new(0.15),{BackgroundColor3=Color3.fromRGB(50,50,65)}):Play() end)
    b.MouseLeave:Connect(function() Tween:Create(b,TweenInfo.new(0.15),{BackgroundColor3=Color3.fromRGB(30,30,40)}):Play() end)
    return b
end

local Islands = {
    [1] = {name = "🏝️ Đảo 1", pos = Vector3.new(-41.90, 11.09, 303740)},
    [2] = {name = "🌴 Đảo 2", pos = Vector3.new(-1166.36, 10.68, -66.31)},
    [3] = {name = "🏜️ Đảo 3", pos = Vector3.new(-51.02, 10.13, -954.41)},
    [4] = {name = "❄️ Đảo 4", pos = Vector3.new(1095.07, 9.38, -284.33)},
    [5] = {name = "🌋 Đảo 5", pos = Vector3.new(1807.50, 9.17, 1073.44)},
}
_G.SelectedIsland = 1

local Main = Instance.new("Frame", S)
Main.Size = UDim2.new(0, 440, 0, 310)
Main.Position = UDim2.new(0.5, -220, 0.5, -155)
Main.BackgroundColor3 = C.bg
Main.BackgroundTransparency = 0.3
Main.BorderSizePixel = 0
Main.Visible = false
corner(Main, 12)
local MS = stroke(Main, C.gold, 1.5, 0.3)
drag(Main)

local MemeBg = Instance.new("ImageLabel", Main)
MemeBg.Size = UDim2.new(1, 0, 1, 0)
MemeBg.Position = UDim2.new(0, 0, 0, 0)
MemeBg.BackgroundTransparency = 1
MemeBg.Image = "rbxassetid://5009915812"
MemeBg.ScaleType = Enum.ScaleType.Crop
MemeBg.ZIndex = 0
MemeBg.ImageTransparency = 0.6
corner(MemeBg, 12)

local Head = Instance.new("Frame", Main)
Head.Size = UDim2.new(1, 0, 0, 32)
Head.BackgroundColor3 = C.bg2
Head.BackgroundTransparency = 0.2
Head.BorderSizePixel = 0
Head.ZIndex = 5
corner(Head, 12)
grad(Head, Color3.fromRGB(45,38,25), Color3.fromRGB(25,25,35))

local Title = Instance.new("TextLabel", Head)
Title.Size = UDim2.new(1, 0, 1, 0)
Title.BackgroundTransparency = 1
Title.TextColor3 = C.gold
Title.TextSize = 13
Title.Font = Enum.Font.GothamBold
Title.Text = "⚡ DATBEO SCRIPT ⚡"
Title.ZIndex = 6

local BtnInfo = Instance.new("TextButton", Main)
BtnInfo.Size = UDim2.new(0, 20, 0, 20)
BtnInfo.Position = UDim2.new(1, -50, 0, 6)
BtnInfo.BackgroundColor3 = Color3.fromRGB(30, 40, 50)
BtnInfo.TextColor3 = C.cyan
BtnInfo.TextSize = 12
BtnInfo.Font = Enum.Font.GothamBold
BtnInfo.Text = "ℹ"
BtnInfo.BorderSizePixel = 0
BtnInfo.ZIndex = 10
corner(BtnInfo, 4)

local Close = Instance.new("TextButton", Main)
Close.Size = UDim2.new(0, 20, 0, 20)
Close.Position = UDim2.new(1, -26, 0, 6)
Close.BackgroundColor3 = Color3.fromRGB(50,30,30)
Close.TextColor3 = C.red
Close.TextSize = 12
Close.Font = Enum.Font.GothamBold
Close.Text = "✕"
Close.BorderSizePixel = 0
Close.ZIndex = 10
corner(Close, 4)

local Sidebar = Instance.new("Frame", Main)
Sidebar.Size = UDim2.new(0, 80, 1, -45)
Sidebar.Position = UDim2.new(0, 8, 0, 38)
Sidebar.BackgroundTransparency = 1
Sidebar.ZIndex = 5

local function sidebarBtn(pos, text, color)
    local b = Instance.new("TextButton", Sidebar)
    b.Size = UDim2.new(1, 0, 0, 34)
    b.Position = UDim2.new(0, 0, 0, pos)
    b.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
    b.BackgroundTransparency = 0.15
    b.TextColor3 = color
    b.TextSize = 10
    b.Font = Enum.Font.GothamBold
    b.Text = text
    b.BorderSizePixel = 0
    b.ZIndex = 10
    corner(b, 6)
    return b
end

local BtnTabFarm = sidebarBtn(0, "🌾 FARM", C.grn)
local BtnTabSell = sidebarBtn(38, "💰 SELL", C.dim)
local BtnTabTele = sidebarBtn(76, "🌊 TELE", C.dim)
local BtnTabESP  = sidebarBtn(114, "👁️ ESP", C.dim)
local BtnTabFix  = sidebarBtn(152, "🔧 FIX", C.dim)

local ContentX = 96
local ContentW = 336

local FarmFrame = Instance.new("Frame", Main)
FarmFrame.Size = UDim2.new(0, ContentW, 1, -50)
FarmFrame.Position = UDim2.new(0, ContentX, 0, 44)
FarmFrame.BackgroundTransparency = 1
FarmFrame.Visible = true
FarmFrame.ZIndex = 5

local BtnAuto = btn(FarmFrame, UDim2.new(1, 0, 0, 32), UDim2.new(0, 0, 0, 0), "🎣 AUTO CÂU: OFF")
BtnAuto.TextColor3 = C.grn
BtnAuto.TextSize = 12

local BtnSkill = btn(FarmFrame, UDim2.new(0.49, -2, 0, 28), UDim2.new(0, 0, 0, 38), "⚔️ AUTO SKILL: OFF")
BtnSkill.TextColor3 = C.grn

local BtnMini = btn(FarmFrame, UDim2.new(0.49, -2, 0, 28), UDim2.new(0.51, 2, 0, 38), "🎮 AUTO MINI: OFF")
BtnMini.TextColor3 = C.grn

local BtnLock = btn(FarmFrame, UDim2.new(0.49, -2, 0, 28), UDim2.new(0, 0, 0, 72), "🔒 KHÓA: OFF")
BtnLock.TextColor3 = C.grn

local BtnUnlock = btn(FarmFrame, UDim2.new(0.49, -2, 0, 28), UDim2.new(0.51, 2, 0, 72), "🔓 MỞ KHÓA")
BtnUnlock.TextColor3 = C.gold

local MusicRow = Instance.new("Frame", FarmFrame)
MusicRow.Size = UDim2.new(1, 0, 0, 30)
MusicRow.Position = UDim2.new(0, 0, 0, 106)
MusicRow.BackgroundTransparency = 1
MusicRow.ZIndex = 10

local BtnPrev = btn(MusicRow, UDim2.new(0, 26, 1, 0), UDim2.new(0, 0, 0, 0), "◀")
BtnPrev.TextColor3 = C.cyan

local SongName = Instance.new("TextLabel", MusicRow)
SongName.Size = UDim2.new(1, -58, 1, 0)
SongName.Position = UDim2.new(0, 28, 0, 0)
SongName.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
SongName.BackgroundTransparency = 0.2
SongName.TextColor3 = C.gold
SongName.TextSize = 10
SongName.Font = Enum.Font.GothamBold
SongName.Text = "♪ Loading..."
SongName.TextTruncate = Enum.TextTruncate.AtEnd
SongName.ZIndex = 10
corner(SongName, 6)

local BtnNext = btn(MusicRow, UDim2.new(0, 26, 1, 0), UDim2.new(1, -26, 0, 0), "▶")
BtnNext.TextColor3 = C.cyan

local BtnMusic = btn(FarmFrame, UDim2.new(1, 0, 0, 28), UDim2.new(0, 0, 0, 140), "🎵 NHẠC: ON")
BtnMusic.TextColor3 = C.cyan

local SellFrame = Instance.new("Frame", Main)
SellFrame.Size = UDim2.new(0, ContentW, 1, -50)
SellFrame.Position = UDim2.new(0, ContentX, 0, 44)
SellFrame.BackgroundTransparency = 1
SellFrame.Visible = false
SellFrame.ZIndex = 5

local BtnSell = btn(SellFrame, UDim2.new(0.49, -2, 0, 32), UDim2.new(0, 0, 0, 0), "💰 SELL ALL")
BtnSell.TextColor3 = C.gold
BtnSell.TextSize = 12

local BtnSellMax = btn(SellFrame, UDim2.new(0.49, -2, 0, 32), UDim2.new(0.51, 2, 0, 0), "🔥 SELL MAX")
BtnSellMax.TextColor3 = C.red
BtnSellMax.TextSize = 12

local BtnMilestone = btn(SellFrame, UDim2.new(1, 0, 0, 30), UDim2.new(0, 0, 0, 38), "🎯 MỐC BÁN: 50 CÁ")
BtnMilestone.TextColor3 = C.cyan

local BtnAutoSell = btn(SellFrame, UDim2.new(1, 0, 0, 30), UDim2.new(0, 0, 0, 74), "💰 AUTO SELL: OFF")
BtnAutoSell.TextColor3 = C.gold

local CountBg = Instance.new("Frame", SellFrame)
CountBg.Size = UDim2.new(1, 0, 0, 30)
CountBg.Position = UDim2.new(0, 0, 0, 110)
CountBg.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
CountBg.BackgroundTransparency = 0.2
CountBg.BorderSizePixel = 0
CountBg.ZIndex = 10
corner(CountBg, 6)

local CountLabel = Instance.new("TextLabel", CountBg)
CountLabel.Size = UDim2.new(0, 180, 1, 0)
CountLabel.Position = UDim2.new(0, 10, 0, 0)
CountLabel.BackgroundTransparency = 1
CountLabel.TextColor3 = C.dim
CountLabel.TextSize = 11
CountLabel.Font = Enum.Font.Gotham
CountLabel.Text = "Số cá cần bán:"
CountLabel.TextXAlignment = Enum.TextXAlignment.Left
CountLabel.ZIndex = 11

local CountBox = Instance.new("TextBox", CountBg)
CountBox.Size = UDim2.new(0, 120, 0, 22)
CountBox.Position = UDim2.new(1, -130, 0, 4)
CountBox.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
CountBox.TextColor3 = C.cyan
CountBox.TextSize = 12
CountBox.Font = Enum.Font.GothamBold
CountBox.Text = "50"
CountBox.ClearTextOnFocus = false
CountBox.BorderSizePixel = 0
CountBox.ZIndex = 11
corner(CountBox, 4)

local TeleFrame = Instance.new("Frame", Main)
TeleFrame.Size = UDim2.new(0, ContentW, 1, -50)
TeleFrame.Position = UDim2.new(0, ContentX, 0, 44)
TeleFrame.BackgroundTransparency = 1
TeleFrame.Visible = false
TeleFrame.ZIndex = 5

local ESPFrame = Instance.new("Frame", Main)
ESPFrame.Size = UDim2.new(0, ContentW, 1, -50)
ESPFrame.Position = UDim2.new(0, ContentX, 0, 44)
ESPFrame.BackgroundTransparency = 1
ESPFrame.Visible = false
ESPFrame.ZIndex = 5

local BtnESPPlayer = btn(ESPFrame, UDim2.new(1, 0, 0, 32), UDim2.new(0, 0, 0, 0), "👤 ESP PLAYERS: OFF")
BtnESPPlayer.TextColor3 = C.cyan

local BtnESPFish = btn(ESPFrame, UDim2.new(1, 0, 0, 32), UDim2.new(0, 0, 0, 38), "🐟 ESP FISH: OFF")
BtnESPFish.TextColor3 = C.gold

local BtnESPZeno = btn(ESPFrame, UDim2.new(1, 0, 0, 32), UDim2.new(0, 0, 0, 76), "⚡ ESP ZENO: OFF")
BtnESPZeno.TextColor3 = C.purple

local FixFrame = Instance.new("Frame", Main)
FixFrame.Size = UDim2.new(0, ContentW, 1, -50)
FixFrame.Position = UDim2.new(0, ContentX, 0, 44)
FixFrame.BackgroundTransparency = 1
FixFrame.Visible = false
FixFrame.ZIndex = 5

local FixInfo = Instance.new("TextLabel", FixFrame)
FixInfo.Size = UDim2.new(1, 0, 0, 40)
FixInfo.Position = UDim2.new(0, 0, 0, 0)
FixInfo.BackgroundTransparency = 1
FixInfo.TextColor3 = C.dim
FixInfo.TextSize = 10
FixInfo.Font = Enum.Font.Gotham
FixInfo.Text = "Tắt hiệu ứng menu + giảm tần suất vòng lặp\ngiúp giảm lag khi chơi lâu."
FixInfo.TextWrapped = true
FixInfo.ZIndex = 10

local BtnFixLag = btn(FixFrame, UDim2.new(1, 0, 0, 38), UDim2.new(0, 0, 0, 50), "🔧 FIX LAG: OFF")
BtnFixLag.TextColor3 = C.cyan
BtnFixLag.TextSize = 12

local FixStatus = Instance.new("TextLabel", FixFrame)
FixStatus.Size = UDim2.new(1, 0, 0, 20)
FixStatus.Position = UDim2.new(0, 0, 0, 95)
FixStatus.BackgroundTransparency = 1
FixStatus.TextColor3 = C.dim
FixStatus.TextSize = 10
FixStatus.Font = Enum.Font.Gotham
FixStatus.Text = "● Chưa bật"
FixStatus.ZIndex = 10

local Status = Instance.new("TextLabel", Main)
Status.Size = UDim2.new(1, -20, 0, 16)
Status.Position = UDim2.new(0, 10, 1, -18)
Status.BackgroundTransparency = 1
Status.TextColor3 = Color3.fromRGB(200, 200, 200)
Status.TextSize = 10
Status.Font = Enum.Font.Gotham
Status.Text = "● Sẵn sàng"
Status.TextXAlignment = Enum.TextXAlignment.Left
Status.ZIndex = 10

local InfoFrame = Instance.new("Frame", S)
InfoFrame.Size = UDim2.new(0, 380, 0, 240)
InfoFrame.Position = UDim2.new(0.5, -190, 0.5, -120)
InfoFrame.BackgroundColor3 = C.bg
InfoFrame.BorderSizePixel = 0
InfoFrame.Visible = false
corner(InfoFrame, 12)
stroke(InfoFrame, C.cyan, 2)
grad(InfoFrame, C.bg2, C.bg)
drag(InfoFrame)

local InfoHead = Instance.new("Frame", InfoFrame)
InfoHead.Size = UDim2.new(1, 0, 0, 32)
InfoHead.BackgroundColor3 = C.bg2
InfoHead.BorderSizePixel = 0
corner(InfoHead, 12)
grad(InfoHead, Color3.fromRGB(25, 40, 50), Color3.fromRGB(25, 25, 35))

local InfoTitle = Instance.new("TextLabel", InfoHead)
InfoTitle.Size = UDim2.new(1, 0, 1, 0)
InfoTitle.BackgroundTransparency = 1
InfoTitle.TextColor3 = C.cyan
InfoTitle.TextSize = 13
InfoTitle.Font = Enum.Font.GothamBold
InfoTitle.Text = "ℹ️ THÔNG TIN LIÊN HỆ"

local InfoClose = Instance.new("TextButton", InfoFrame)
InfoClose.Size = UDim2.new(0, 20, 0, 20)
InfoClose.Position = UDim2.new(1, -26, 0, 6)
InfoClose.BackgroundColor3 = Color3.fromRGB(50, 30, 30)
InfoClose.TextColor3 = C.red
InfoClose.TextSize = 12
InfoClose.Font = Enum.Font.GothamBold
InfoClose.Text = "✕"
InfoClose.BorderSizePixel = 0
corner(InfoClose, 4)

local InfoText = Instance.new("TextLabel", InfoFrame)
InfoText.Size = UDim2.new(1, -30, 1, -50)
InfoText.Position = UDim2.new(0, 15, 0, 40)
InfoText.BackgroundTransparency = 1
InfoText.TextColor3 = Color3.fromRGB(220, 220, 230)
InfoText.TextSize = 11
InfoText.Font = Enum.Font.Gotham
InfoText.TextXAlignment = Enum.TextXAlignment.Left
InfoText.TextYAlignment = Enum.TextYAlignment.Top
InfoText.TextWrapped = true
InfoText.Text = "Cảm ơn bạn đã sử dụng script!\n\n" ..
    "📧 Nếu có lỗi hãy gửi đến Gmail:\n" ..
    "nguyenthetrongdat13072012@gmail.com\n\n" ..
    "💬 Hoặc nhắn tin riêng bằng Zalo:\n" ..
    "0964 296 801\n\n" ..
    "⚠️ Không gọi điện nhá!\n" ..
    "Đứa mô gọi điện là GAY 🤣"

local Reopen = Instance.new("TextButton", S)
Reopen.Size = UDim2.new(0, 46, 0, 46)
Reopen.Position = UDim2.new(0, 20, 0.5, -23)
Reopen.BackgroundColor3 = C.bg2
Reopen.TextColor3 = C.gold
Reopen.TextSize = 20
Reopen.Font = Enum.Font.GothamBold
Reopen.Text = "⚡"
Reopen.BorderSizePixel = 0
Reopen.Visible = false
corner(Reopen, 23)
stroke(Reopen, C.gold, 2)
grad(Reopen, Color3.fromRGB(45,38,25), C.bg2)
drag(Reopen)

_G.AutoFish = false; _G.AutoSkill = false; _G.AutoMini = false
_G.LockPos = false; _G.AnchorPos = nil
_G.ForceUnlock = false; _G.AutoSell = false
_G.FixLag = false
_G.SellTarget = 50
_G.ESPPlayer = false
_G.ESPFish = false
_G.ESPZeno = false

local Playlist = {
    {name = "Trả Cho Anh", id = "110396752508363"},
    {name = "Trả Cho Anh Ver #2", id = "71214605813266"},
    {name = "Anh Độ", id = "99152674992699"},
    {name = "Ai Đưa Em Về", id = "110919391228823"},
    {name = "Nhạc Vietsub #1", id = "99072612944031"},
    {name = "Pháo", id = "77063870786604"},
    {name = "Vũ Trụ Có Anh", id = "99555946575863"},
    {name = "Rainy", id = "79277371759525"},
    {name = "Biển Hoa", id = "1007728815581027"},
    {name = "Sơn Thủy Trùng Mây", id = "80510130014912"},
    {name = "Heavenly Jumpstyle", id = "139945126932727"},
}
local CurrentSong = 1

local BGM = Instance.new("Sound")
BGM.Name = "DatBeoBGM"
BGM.Looped = false
BGM.Volume = 0.5
BGM.Parent = Sound

local function LoadSong(index)
    if index > #Playlist then index = 1 end
    if index < 1 then index = #Playlist end
    CurrentSong = index
    BGM.SoundId = "rbxassetid://" .. Playlist[index].id
    BGM:Play()
    print("[NHẠC] Đang phát:", Playlist[index].name)
    if SongName then SongName.Text = "♪ " .. Playlist[index].name end
end

local function NextSong() LoadSong(CurrentSong + 1) end
local function PrevSong() LoadSong(CurrentSong - 1) end

BGM.Ended:Connect(NextSong)
LoadSong(1)

local function K(key, delay)
    delay = delay or 0
    pcall(function() keypress(key) keyrelease(key) end)
    pcall(function()
        VIM:SendKeyEvent(true, key, false, game)
        VIM:SendKeyEvent(false, key, false, game)
    end)
    if delay > 0 then task.wait(delay) end
end

local function Click(hold)
    hold = hold or 0.05
    pcall(function() mouse1press() task.wait(hold) mouse1release() end)
    pcall(function()
        local vp = workspace.CurrentCamera.ViewportSize
        VIM:SendMouseButtonEvent(vp.X/2, vp.Y/2, 0, true, game, 0)
        task.wait(hold)
        VIM:SendMouseButtonEvent(vp.X/2, vp.Y/2, 0, false, game, 0)
    end)
end

local FishHUD = Instance.new("Frame", S)
FishHUD.Size = UDim2.new(0, 180, 0, 50)
FishHUD.Position = UDim2.new(0, 15, 0, 100)
FishHUD.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
FishHUD.BackgroundTransparency = 0.3
FishHUD.BorderSizePixel = 0
FishHUD.ZIndex = 100
FishHUD.Active = false
corner(FishHUD, 10)
local FHStroke = stroke(FishHUD, C.cyan, 2)
grad(FishHUD, Color3.fromRGB(25, 25, 35), Color3.fromRGB(15, 15, 20))
drag(FishHUD)

local FishIcon = Instance.new("TextLabel", FishHUD)
FishIcon.Size = UDim2.new(0, 40, 1, 0)
FishIcon.Position = UDim2.new(0, 5, 0, 0)
FishIcon.BackgroundTransparency = 1
FishIcon.TextColor3 = C.cyan
FishIcon.TextSize = 28
FishIcon.Font = Enum.Font.GothamBold
FishIcon.Text = "🐟"
FishIcon.ZIndex = 101

local FishText = Instance.new("TextLabel", FishHUD)
FishText.Size = UDim2.new(1, -50, 1, 0)
FishText.Position = UDim2.new(0, 45, 0, -5)
FishText.BackgroundTransparency = 1
FishText.TextColor3 = C.grn
FishText.TextSize = 16
FishText.Font = Enum.Font.GothamBold
FishText.Text = "0 / 50"
FishText.TextXAlignment = Enum.TextXAlignment.Left
FishText.ZIndex = 101

local FishSub = Instance.new("TextLabel", FishHUD)
FishSub.Size = UDim2.new(1, -50, 0, 12)
FishSub.Position = UDim2.new(0, 45, 1, -16)
FishSub.BackgroundTransparency = 1
FishSub.TextColor3 = C.dim
FishSub.TextSize = 9
FishSub.Font = Enum.Font.Gotham
FishSub.Text = "KHO CÁ"
FishSub.TextXAlignment = Enum.TextXAlignment.Left
FishSub.ZIndex = 101

function showToast(text, color)
    local toast = Instance.new("TextLabel", S)
    toast.Size = UDim2.new(0, 220, 0, 36)
    toast.Position = UDim2.new(0.5, -110, 0.15, 0)
    toast.BackgroundColor3 = Color3.fromRGB(20, 20, 25)
    toast.BackgroundTransparency = 0.2
    toast.TextColor3 = color or C.grn
    toast.TextSize = 13
    toast.Font = Enum.Font.GothamBold
    toast.Text = text
    toast.BorderSizePixel = 0
    toast.ZIndex = 200
    corner(toast, 8)
    stroke(toast, color or C.grn, 2)
    grad(toast, Color3.fromRGB(30, 30, 40), Color3.fromRGB(15, 15, 20))
    toast.TextTransparency = 1
    toast.BackgroundTransparency = 1
    Tween:Create(toast, TweenInfo.new(0.2), {TextTransparency = 0, BackgroundTransparency = 0.2}):Play()
    Tween:Create(toast, TweenInfo.new(1.5), {Position = UDim2.new(0.5, -110, 0.1, 0)}):Play()
    task.wait(1.8)
    Tween:Create(toast, TweenInfo.new(0.4), {TextTransparency = 1, BackgroundTransparency = 1}):Play()
    task.wait(0.4)
    toast:Destroy()
end

local function getFish()
    local count = 0
    local function check(container)
        if container then
            for _, item in ipairs(container:GetChildren()) do
                if item:IsA("Tool") then
                    local name = string.lower(item.Name)
                    if not (name:find("rod") or name:find("cần") or name:find("bait") 
                        or name:find("mồi") or name:find("potion") or name:find("thuốc") 
                        or name:find("license") or name:find("gps") or name:find("radar") 
                        or name:find("pass")) then
                        count = count + 1
                    end
                end
            end
        end
    end
    check(P.Backpack)
    check(P.Character)
    return count
end

local function updateFishHUD()
    local current = getFish()
    local target = _G.SellTarget or 50
    FishText.Text = current .. " / " .. target
    if current >= target then
        FishText.TextColor3 = C.gold
        FHStroke.Color = C.gold
    elseif current >= target * 0.7 then
        FishText.TextColor3 = C.cyan
        FHStroke.Color = C.cyan
    else
        FishText.TextColor3 = C.grn
        FHStroke.Color = C.cyan
    end
end

task.spawn(function()
    while true do
        task.wait(0.5)
        pcall(updateFishHUD)
    end
end)

local function clickBtn(keys)
    local inset = game:GetService("GuiService"):GetGuiInset()
    for _, obj in pairs(P.PlayerGui:GetDescendants()) do
        if (obj:IsA("TextButton") or obj:IsA("TextLabel")) and obj.Visible then
            local txt = string.lower(obj.Text or "")
            for _, kw in ipairs(keys) do
                if txt:find(kw) then
                    local pos, sz = obj.AbsolutePosition, obj.AbsoluteSize
                    local cx, cy = pos.X + sz.X/2 + inset.X, pos.Y + sz.Y/2 + inset.Y
                    VIM:SendMouseButtonEvent(cx, cy, 0, true, game, 1)
                    task.wait(0.05)
                    VIM:SendMouseButtonEvent(cx, cy, 0, false, game, 1)
                    return true
                end
            end
        end
    end
    return false
end

local function TeleByRespawn(targetPos, islandName)
    local char = P.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not hrp or not hum then return end
    
    Status.Text = "● 📡 Ping 999..."
    Status.TextColor3 = C.gold
    task.spawn(function() showToast("📡 Ping 999 + Loading...", C.gold) end)
    
    pcall(function()
        if setfflag then 
            setfflag("TaskSchedulerMaxStepsPerSec", "0")
            setfflag("TaskSchedulerTargetFps", "1")
        end
    end)
    pcall(function()
        settings():GetService("NetworkSettings"):SetIncomingReplicationLag(999)
    end)
    pcall(function()
        sethiddenproperty(game:GetService("NetworkSettings"), "IncomingReplicationLag", 999)
    end)
    
    task.wait(1)
    
    _G.TeleTargetPos = targetPos
    _G.TeleTargetName = islandName
    _G.TeleLockEnd = tick() + 20
    _G.TeleLockActive = true
    
    Status.Text = "● 💀 Kill để respawn..."
    print("[TELE] Kill character...")
    
    pcall(function() hum.Health = 0 end)
    pcall(function() hum:TakeDamage(hum.MaxHealth * 10) end)
    pcall(function() if hum.Parent then hum.Parent:BreakJoints() end end)
    
    task.wait(0.5)
end

P.CharacterAdded:Connect(function(newChar)
    if not _G.TeleLockActive then return end
    
    print("[TELE] Respawn → tele đến", _G.TeleTargetName)
    Status.Text = "● 🌀 Respawn, đang tele..."
    Status.TextColor3 = C.cyan
    
    local newHrp = newChar:WaitForChild("HumanoidRootPart", 5)
    local newHum = newChar:WaitForChild("Humanoid", 5)
    if not newHrp or not newHum then return end
    
    task.wait(0.3)
    
    local lockEnd = _G.TeleLockEnd or (tick() + 20)
    local targetPos = _G.TeleTargetPos
    local spamCount = 0
    
    while tick() < lockEnd and _G.TeleLockActive do
        pcall(function()
            newHrp.CFrame = CFrame.new(targetPos + Vector3.new(0, 5, 0))
            newHrp.Velocity = Vector3.new(0, 0, 0)
            newHrp.RotVelocity = Vector3.new(0, 0, 0)
            newHrp.Anchored = true
            newHum.WalkSpeed = 0
            newHum.JumpPower = 0
            newHum.UseJumpPower = true
            newHum.PlatformStand = true
            newHum:Move(Vector3.new(0, 0, 0))
        end)
        
        spamCount = spamCount + 1
        if spamCount % 20 == 0 then
            local remain = math.floor(lockEnd - tick())
            Status.Text = "● 🔒 Khóa cứng... còn " .. remain .. "s"
        end
        
        task.wait(0.05)
    end
    
    pcall(function()
        newHrp.Anchored = false
        newHum.WalkSpeed = 16
        newHum.JumpPower = 50
        newHum.PlatformStand = false
    end)
    
    pcall(function()
        if setfflag then 
            setfflag("TaskSchedulerMaxStepsPerSec", "60")
            setfflag("TaskSchedulerTargetFps", "240")
        end
    end)
    pcall(function()
        settings():GetService("NetworkSettings"):SetIncomingReplicationLag(0)
    end)
    pcall(function()
        sethiddenproperty(game:GetService("NetworkSettings"), "IncomingReplicationLag", 0)
    end)
    
    _G.TeleLockActive = false
    _G.TeleTargetPos = nil
    _G.TeleTargetName = nil
    
    Status.Text = "● ✅ Đã đến!"
    Status.TextColor3 = C.grn
    task.spawn(function() showToast("✅ Đã đến đảo!", C.grn) end)
    print("[TELE] Hoàn tất sau", spamCount, "lần spam")
end)

local IslandButtons = {}
for i = 1, 5 do
    local b = btn(TeleFrame, UDim2.new(1, 0, 0, 32), UDim2.new(0, 0, 0, (i-1)*36), Islands[i].name)
    b.TextColor3 = Color3.fromRGB(220, 220, 230)
    b.TextSize = 11
    IslandButtons[i] = b
    
    b.MouseButton1Click:Connect(function()
        _G.SelectedIsland = i
        for j, b2 in pairs(IslandButtons) do
            if j == i then
                b2.BackgroundColor3 = Color3.fromRGB(50, 45, 30)
                b2.TextColor3 = C.gold
            else
                b2.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
                b2.TextColor3 = Color3.fromRGB(220, 220, 230)
            end
        end
        task.spawn(function()
            TeleByRespawn(Islands[i].pos, Islands[i].name)
        end)
    end)
end
IslandButtons[1].BackgroundColor3 = Color3.fromRGB(50, 45, 30)
IslandButtons[1].TextColor3 = C.gold

local function SellAll()
    local char = P.Character
    if not char then return false, "Không có char" end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not hrp or not hum then return false, "Không có HRP/Humanoid" end
    
    local oldCFrame = hrp.CFrame
    local oldWalkSpeed = hum.WalkSpeed
    
    local npc, shortest = nil, math.huge
    for _, g in pairs(workspace:GetDescendants()) do
        if g:IsA("Model") or g:IsA("BasePart") then
            local n = string.lower(g.Name)
            if n:find("fish") then
                local p = g:IsA("BasePart") and g 
                    or g:FindFirstChild("HumanoidRootPart") 
                    or g:FindFirstChildWhichIsA("BasePart")
                if p then
                    local d = (p.Position - hrp.Position).Magnitude
                    if d < shortest then shortest = d; npc = p end
                end
            end
        end
    end
    if not npc then return false, "Không tìm thấy NPC fish" end
    
    local npcPos = npc.Position
    local standPos = npcPos + (hrp.Position - npcPos).Unit * 4
    standPos = Vector3.new(standPos.X, npcPos.Y, standPos.Z)
    
    Status.Text = "● Bay đến NPC (2x)..."
    Status.TextColor3 = C.cyan
    
    local flySpeed = 32
    local flyStart = tick()
    while tick() - flyStart < 15 do
        if not hrp or not hrp.Parent then break end
        local currentPos = hrp.Position
        local dist = (standPos - currentPos).Magnitude
        if dist < 3 then break end
        local dir = (standPos - currentPos).Unit
        local newPos = currentPos + dir * (flySpeed * 0.05)
        pcall(function()
            hrp.CFrame = CFrame.new(newPos, newPos + hrp.CFrame.LookVector)
            hrp.Velocity = Vector3.new(0, 0, 0)
        end)
        task.wait(0.05)
    end
    
    hum.WalkSpeed = 0
    hum.JumpPower = 0
    hrp.Anchored = true
    hrp.CFrame = CFrame.new(standPos, Vector3.new(npcPos.X, standPos.Y, npcPos.Z))
    task.wait(0.5)
    
    local prompt = nil
    local promptDist = math.huge
    for _, p in pairs(workspace:GetDescendants()) do
        if p:IsA("ProximityPrompt") and p.Enabled then
            local part = p.Parent
            if part and part:IsA("BasePart") then
                local d = (part.Position - hrp.Position).Magnitude
                if d < 15 and d < promptDist then
                    prompt = p
                    promptDist = d
                end
            end
        end
    end
    
    local fCount = getFish()
    local loopCount = 0
    local sellStart = tick()
    
    repeat
        if tick() - sellStart >= 25 then break end
        loopCount = loopCount + 1
        
        hrp.Anchored = true
        hum.WalkSpeed = 0
        hum.JumpPower = 0
        
        if prompt then pcall(function() fireproximityprompt(prompt) end) end
        
        Status.Text = "● Chờ 2s trước khi bấm E..."
        task.wait(2)
        
        K(Enum.KeyCode.E, 0.1)
        task.wait(0.5)
        
        clickBtn({"bán tất cả", "sell all", "bán", "sell", "confirm", "đồng ý", "all", "tất cả"})
        task.wait(1.5)
        
        fCount = getFish()
    until fCount == 0 or loopCount >= 10
    
    local cStart = tick()
    while tick() - cStart < 3 do
        clickBtn({"tạm biệt", "bye", "thoát", "close", "leave", "exit"})
        task.wait(0.5)
    end
    
    hrp.CFrame = oldCFrame
    hum.WalkSpeed = oldWalkSpeed
    hum.JumpPower = 50
    hrp.Anchored = false
    task.wait(0.3)
    
    updateFishHUD()
    return true, "Đã bán " .. loopCount .. " lần"
end

local function SaveAnchor()
    local c = P.Character
    if c and c:FindFirstChild("HumanoidRootPart") then
        _G.AnchorPos = c.HumanoidRootPart.Position
        _G.LockPos = true
    end
end

task.spawn(function()
    while true do
        task.wait(0.2)
        if not _G.ForceUnlock and _G.LockPos and _G.AnchorPos then
            local c = P.Character
            if c and c:FindFirstChild("HumanoidRootPart") then
                if (c.HumanoidRootPart.Position - _G.AnchorPos).Magnitude > 3 then
                    c.HumanoidRootPart.CFrame = CFrame.new(_G.AnchorPos)
                end
            end
        end
    end
end)

task.spawn(function()
    while true do
        task.wait(0.05)
        if _G.AutoSkill or _G.AutoFish then
            K(Enum.KeyCode.Z, 0.01)
            K(Enum.KeyCode.X, 0.01)
            K(Enum.KeyCode.C, 0.01)
            K(Enum.KeyCode.V, 0.01)
        end
    end
end)

task.spawn(function()
    while true do
        task.wait(0.05)
        if _G.AutoMini or _G.AutoFish then
            K(Enum.KeyCode.W, 0.02)
            K(Enum.KeyCode.A, 0.05)
            K(Enum.KeyCode.D, 0.07)
        end
    end
end)

local function CheckFish()
    local pg = P:FindFirstChild("PlayerGui")
    if pg then
        for _, g in pairs(pg:GetDescendants()) do
            if (g:IsA("TextLabel") or g:IsA("TextButton")) then
                if string.find(string.lower(tostring(g.Text or "")), "fish caught") then return true end
            end
        end
    end
    return false
end

task.spawn(function()
    while true do
        task.wait(0.1)
        if _G.AutoFish then
            Status.Text = "● Thả cần..."
            Click(0.5)
            task.wait(3.5)
            
            Status.Text = "● Chờ cá..."
            local startT = tick()
            local caught = false
            
            while _G.AutoFish and (tick() - startT < 20) do
                if CheckFish() then caught = true break end
                task.wait(0.3)
            end
            
            if caught then
                local currentFish = getFish()
                local target = _G.SellTarget
                updateFishHUD()
                Status.Text = "● Đã câu! Kho: " .. currentFish .. "/" .. target
                Status.TextColor3 = C.grn
                
                task.spawn(function()
                    showToast("🐟 Kho +1  (" .. currentFish .. "/" .. target .. ")", C.cyan)
                end)
                task.wait(1)
                
                if _G.AutoSell and currentFish >= target then
                    Status.Text = "● Đủ " .. target .. " cá! Bán..."
                    Status.TextColor3 = C.gold
                    task.spawn(function() showToast("💰 Đủ " .. target .. " cá!", C.gold) end)
                    
                    local wasLocked = _G.LockPos
                    _G.LockPos = false; _G.AnchorPos = nil; _G.ForceUnlock = true
                    task.wait(0.5)
                    
                    local ok, msg = SellAll()
                    task.wait(1.5)
                    
                    _G.ForceUnlock = false
                    if wasLocked then SaveAnchor() end
                    updateFishHUD()
                    
                    Status.Text = ok and ("● ✅ " .. msg) or ("● ❌ Bán lỗi!")
                    Status.TextColor3 = ok and C.grn or C.red
                end
                task.wait(0.5)
            else
                Status.Text = "● ⏰ Hết thời gian"
                task.wait(0.5)
            end
        else
            task.wait(0.2)
        end
    end
end)

local function createESP(target, color, name)
    if not target then return end
    local h = Instance.new("Highlight")
    h.Name = "DatBeoESP_" .. name
    h.Adornee = target
    h.FillColor = color
    h.FillTransparency = 0.5
    h.OutlineColor = color
    h.OutlineTransparency = 0
    h.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
    h.Parent = target
end

local function clearESP(name)
    for _, v in pairs(workspace:GetDescendants()) do
        if v:IsA("Highlight") and v.Name == "DatBeoESP_" .. name then v:Destroy() end
    end
end

local function createPlayerESP(character, playerName)
    if not character or not character.Parent then return end
    local head = character:FindFirstChild("Head")
    if not head then return end
    if head:FindFirstChild("DatBeoNameESP") then head.DatBeoNameESP:Destroy() end
    
    local billboard = Instance.new("BillboardGui")
    billboard.Name = "DatBeoNameESP"
    billboard.Size = UDim2.new(0, 200, 0, 40)
    billboard.StudsOffset = Vector3.new(0, 3, 0)
    billboard.AlwaysOnTop = true
    billboard.Parent = head
    
    local frame = Instance.new("Frame", billboard)
    frame.Size = UDim2.new(1, 0, 1, 0)
    frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    frame.BackgroundTransparency = 0.4
    frame.BorderSizePixel = 0
    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 6)
    
    local nameLabel = Instance.new("TextLabel", frame)
    nameLabel.Size = UDim2.new(1, 0, 1, 0)
    nameLabel.BackgroundTransparency = 1
    nameLabel.TextColor3 = C.cyan
    nameLabel.TextSize = 14
    nameLabel.Font = Enum.Font.GothamBold
    nameLabel.Text = playerName
    nameLabel.TextStrokeTransparency = 0
end

local function updateESPPlayers()
    if not _G.ESPPlayer then return end
    for _, plr in pairs(Players:GetPlayers()) do
        if plr ~= P and plr.Character then
            if not plr.Character:FindFirstChild("DatBeoESP_Player") then
                createESP(plr.Character, C.cyan, "Player")
            end
            createPlayerESP(plr.Character, plr.Name)
        end
    end
end

local function updateESPFish()
    if not _G.ESPFish then return end
    for _, g in pairs(workspace:GetDescendants()) do
        if g:IsA("Model") and string.lower(g.Name):find("fish merchant") then
            if not g:FindFirstChild("DatBeoESP_Fish") then
                createESP(g, C.gold, "Fish")
            end
        end
    end
end

local function updateESPZeno()
    if not _G.ESPZeno then return end
    for _, g in pairs(workspace:GetDescendants()) do
        if (g:IsA("Model") or g:IsA("BasePart")) and string.lower(g.Name):find("zeno") then
            if not g:FindFirstChild("DatBeoESP_Zeno") then
                createESP(g, C.purple, "Zeno")
            end
        end
    end
end

task.spawn(function()
    while true do
        task.wait(1)
        if _G.ESPPlayer then updateESPPlayers() end
        if _G.ESPFish then updateESPFish() end
        if _G.ESPZeno then updateESPZeno() end
    end
end)

local function SwitchTab(tab)
    FarmFrame.Visible = (tab == "farm")
    SellFrame.Visible = (tab == "sell")
    TeleFrame.Visible = (tab == "tele")
    ESPFrame.Visible = (tab == "esp")
    FixFrame.Visible = (tab == "fix")
    
    BtnTabFarm.BackgroundColor3 = Color3.fromRGB(30, 30, 40); BtnTabFarm.TextColor3 = C.dim
    BtnTabSell.BackgroundColor3 = Color3.fromRGB(30, 30, 40); BtnTabSell.TextColor3 = C.dim
    BtnTabTele.BackgroundColor3 = Color3.fromRGB(30, 30, 40); BtnTabTele.TextColor3 = C.dim
    BtnTabESP.BackgroundColor3 = Color3.fromRGB(30, 30, 40); BtnTabESP.TextColor3 = C.dim
    BtnTabFix.BackgroundColor3 = Color3.fromRGB(30, 30, 40); BtnTabFix.TextColor3 = C.dim
    
    if tab == "farm" then
        BtnTabFarm.BackgroundColor3 = Color3.fromRGB(35, 55, 45); BtnTabFarm.TextColor3 = C.grn
    elseif tab == "sell" then
        BtnTabSell.BackgroundColor3 = Color3.fromRGB(50, 45, 30); BtnTabSell.TextColor3 = C.gold
    elseif tab == "tele" then
        BtnTabTele.BackgroundColor3 = Color3.fromRGB(30, 40, 55); BtnTabTele.TextColor3 = C.cyan
    elseif tab == "esp" then
        BtnTabESP.BackgroundColor3 = Color3.fromRGB(40, 30, 55); BtnTabESP.TextColor3 = C.purple
    elseif tab == "fix" then
        BtnTabFix.BackgroundColor3 = Color3.fromRGB(30, 45, 55); BtnTabFix.TextColor3 = C.cyan
    end
end

BtnTabFarm.MouseButton1Click:Connect(function() SwitchTab("farm") end)
BtnTabSell.MouseButton1Click:Connect(function() SwitchTab("sell") end)
BtnTabTele.MouseButton1Click:Connect(function() SwitchTab("tele") end)
BtnTabESP.MouseButton1Click:Connect(function() SwitchTab("esp") end)
BtnTabFix.MouseButton1Click:Connect(function() SwitchTab("fix") end)

BtnAuto.MouseButton1Click:Connect(function()
    _G.AutoFish = not _G.AutoFish
    if _G.AutoFish then
        BtnAuto.Text = "🎣 AUTO CÂU: ON"; BtnAuto.TextColor3 = C.red
        _G.AutoSkill = true; _G.AutoMini = true
        BtnSkill.Text = "⚔️ AUTO SKILL: ON"; BtnSkill.TextColor3 = C.red
        BtnMini.Text = "🎮 AUTO MINI: ON"; BtnMini.TextColor3 = C.red
        if not _G.ForceUnlock then
            SaveAnchor()
            BtnLock.Text = "🔒 KHÓA: ON"; BtnLock.TextColor3 = C.red
        end
        Status.Text = "● Đang chạy..."
    else
        BtnAuto.Text = "🎣 AUTO CÂU: OFF"; BtnAuto.TextColor3 = C.grn
        _G.AutoSkill = false; _G.AutoMini = false
        BtnSkill.Text = "⚔️ AUTO SKILL: OFF"; BtnSkill.TextColor3 = C.grn
        BtnMini.Text = "🎮 AUTO MINI: OFF"; BtnMini.TextColor3 = C.grn
        Status.Text = "● Đã tắt"
    end
end)

BtnSkill.MouseButton1Click:Connect(function()
    _G.AutoSkill = not _G.AutoSkill
    BtnSkill.Text = _G.AutoSkill and "⚔️ AUTO SKILL: ON" or "⚔️ AUTO SKILL: OFF"
    BtnSkill.TextColor3 = _G.AutoSkill and C.red or C.grn
end)

BtnMini.MouseButton1Click:Connect(function()
    _G.AutoMini = not _G.AutoMini
    BtnMini.Text = _G.AutoMini and "🎮 AUTO MINI: ON" or "🎮 AUTO MINI: OFF"
    BtnMini.TextColor3 = _G.AutoMini and C.red or C.grn
end)

BtnLock.MouseButton1Click:Connect(function()
    if _G.LockPos then
        _G.LockPos = false; _G.AnchorPos = nil
        BtnLock.Text = "🔒 KHÓA: OFF"; BtnLock.TextColor3 = C.grn
    else
        SaveAnchor()
        BtnLock.Text = "🔒 KHÓA: ON"; BtnLock.TextColor3 = C.red
    end
end)

BtnUnlock.MouseButton1Click:Connect(function()
    _G.LockPos = false; _G.AnchorPos = nil; _G.ForceUnlock = true
    BtnLock.Text = "🔒 KHÓA: OFF"; BtnLock.TextColor3 = C.grn
    Status.Text = "● Đã mở khóa!"
    task.wait(0.5); _G.ForceUnlock = false
end)

BtnMusic.MouseButton1Click:Connect(function()
    if BGM.Playing then
        BGM:Pause()
        BtnMusic.Text = "🎵 NHẠC: OFF"
        BtnMusic.TextColor3 = C.red
    else
        BGM:Play()
        BtnMusic.Text = "🎵 NHẠC: ON"
        BtnMusic.TextColor3 = C.cyan
    end
end)

BtnNext.MouseButton1Click:Connect(function() NextSong() end)
BtnPrev.MouseButton1Click:Connect(function() PrevSong() end)

BtnSell.MouseButton1Click:Connect(function()
    Status.Text = "● Đang bán..."; Status.TextColor3 = C.gold
    task.spawn(function()
        local wasLocked = _G.LockPos
        _G.LockPos = false; _G.AnchorPos = nil; _G.ForceUnlock = true
        task.wait(0.5)
        local ok, msg = SellAll()
        task.wait(0.5)
        _G.ForceUnlock = false
        if wasLocked then SaveAnchor() end
        updateFishHUD()
        Status.Text = ok and ("● ✅ " .. msg) or ("● ❌ " .. msg)
        Status.TextColor3 = ok and C.grn or C.red
    end)
end)

BtnSellMax.MouseButton1Click:Connect(function()
    Status.Text = "● Đang bán MAX..."; Status.TextColor3 = C.red
    task.spawn(function()
        local wasLocked = _G.LockPos
        _G.LockPos = false; _G.AnchorPos = nil; _G.ForceUnlock = true
        task.wait(0.5)
        local ok, msg = SellAll()
        task.wait(0.5)
        _G.ForceUnlock = false
        if wasLocked then SaveAnchor() end
        updateFishHUD()
        Status.Text = ok and ("● 🔥 " .. msg) or ("● ❌ " .. msg)
        Status.TextColor3 = ok and C.grn or C.red
    end)
end)

local milestoneIdx = 4
local milestones = {10, 20, 30, 50}

BtnMilestone.MouseButton1Click:Connect(function()
    milestoneIdx = milestoneIdx + 1
    if milestoneIdx > #milestones then milestoneIdx = 1 end
    _G.SellTarget = milestones[milestoneIdx]
    BtnMilestone.Text = "🎯 MỐC BÁN: " .. _G.SellTarget .. " CÁ"
    CountBox.Text = tostring(_G.SellTarget)
    updateFishHUD()
end)

BtnAutoSell.MouseButton1Click:Connect(function()
    _G.AutoSell = not _G.AutoSell
    BtnAutoSell.Text = _G.AutoSell and "💰 AUTO SELL: ON" or "💰 AUTO SELL: OFF"
    BtnAutoSell.TextColor3 = _G.AutoSell and C.red or C.gold
end)

CountBox.FocusLost:Connect(function()
    local n = tonumber(CountBox.Text)
    if n then
        n = math.clamp(math.floor(n), 1, 50)
        CountBox.Text = tostring(n)
        _G.SellTarget = n
        updateFishHUD()
    else
        CountBox.Text = "50"
        _G.SellTarget = 50
    end
end)

BtnESPPlayer.MouseButton1Click:Connect(function()
    _G.ESPPlayer = not _G.ESPPlayer
    if _G.ESPPlayer then
        BtnESPPlayer.Text = "👤 ESP PLAYERS: ON"; BtnESPPlayer.TextColor3 = C.red
        updateESPPlayers()
    else
        BtnESPPlayer.Text = "👤 ESP PLAYERS: OFF"; BtnESPPlayer.TextColor3 = C.cyan
        clearESP("Player")
        for _, plr in pairs(Players:GetPlayers()) do
            if plr.Character and plr.Character:FindFirstChild("Head") then
                local b = plr.Character.Head:FindFirstChild("DatBeoNameESP")
                if b then b:Destroy() end
            end
        end
    end
end)

BtnESPFish.MouseButton1Click:Connect(function()
    _G.ESPFish = not _G.ESPFish
    if _G.ESPFish then
        BtnESPFish.Text = "🐟 ESP FISH: ON"; BtnESPFish.TextColor3 = C.red
        updateESPFish()
    else
        BtnESPFish.Text = "🐟 ESP FISH: OFF"; BtnESPFish.TextColor3 = C.gold
        clearESP("Fish")
    end
end)

BtnESPZeno.MouseButton1Click:Connect(function()
    _G.ESPZeno = not _G.ESPZeno
    if _G.ESPZeno then
        BtnESPZeno.Text = "⚡ ESP ZENO: ON"; BtnESPZeno.TextColor3 = C.red
        updateESPZeno()
    else
        BtnESPZeno.Text = "⚡ ESP ZENO: OFF"; BtnESPZeno.TextColor3 = C.purple
        clearESP("Zeno")
    end
end)

BtnFixLag.MouseButton1Click:Connect(function()
    _G.FixLag = not _G.FixLag
    if _G.FixLag then
        BtnFixLag.Text = "🔧 FIX LAG: ON"; BtnFixLag.TextColor3 = C.red
        FixStatus.Text = "● Đã bật"; FixStatus.TextColor3 = C.grn
        for _, v in pairs(Main:GetDescendants()) do
            local g = v:FindFirstChild("UIGradient"); if g then g:Destroy() end
            local st = v:FindFirstChild("UIStroke"); if st then st:Destroy() end
            local c = v:FindFirstChild("UICorner"); if c then c:Destroy() end
        end
        Main.BackgroundTransparency = 0
    else
        BtnFixLag.Text = "🔧 FIX LAG: OFF"; BtnFixLag.TextColor3 = C.cyan
        FixStatus.Text = "● Đã tắt"; FixStatus.TextColor3 = C.dim
        corner(Main, 12); stroke(Main, C.gold, 1.5, 0.3); grad(Main, C.bg2, C.bg)
        for _, v in pairs(Main:GetDescendants()) do
            if v:IsA("TextButton") then corner(v, 6) end
        end
    end
end)

BtnInfo.MouseButton1Click:Connect(function() InfoFrame.Visible = true end)
InfoClose.MouseButton1Click:Connect(function() InfoFrame.Visible = false end)

Close.MouseButton1Click:Connect(function()
    Main.Visible = false; Reopen.Visible = true
end)
Reopen.MouseButton1Click:Connect(function()
    Main.Visible = true; Reopen.Visible = false
end)

for _, obj in pairs(Main:GetDescendants()) do
    if obj:IsA("Frame") or obj:IsA("ScrollingFrame") then obj.Active = false end
end
for _, obj in pairs(InfoFrame:GetDescendants()) do
    if obj:IsA("Frame") or obj:IsA("ScrollingFrame") then obj.Active = false end
end
Main.Active = false
InfoFrame.Active = false

Main.Visible = true
SwitchTab("farm")
updateFishHUD()

task.spawn(function()
    task.wait(1)
    pcall(function()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "⚡ DATBEO100KG",
            Text = "Script được viết bởi datbeo100kgkakakaka!",
            Duration = 5
        })
    end)
    showToast("⚡ DatBeo Script đã load!", C.gold)
end)
]==]
math.randomseed(os.time()*tick()*999999)
local e,k={},{}
for i=1,#code do local b=string.byte(code,i); local key=math.random(1,255); k[i]=key; e[i]=bit32.bxor(b,key) end
local p={} for i=1,#code do p[i]=i end
for i=#p,2,-1 do local j=math.random(1,i); p[i],p[j]=p[j],p[i] end
local es,ks={},{}
for i=1,#p do es[i]=e[p[i]]; ks[i]=k[p[i]] end
local out="local e={"..table.concat(es,",").."};local k={"..table.concat(ks,",").."};local p={"..table.concat(p,",").."};local t={};for i=1,#e do t[p[i]]=string.char(bit32.bxor(e[i],k[i])) end;local f=loadstring(table.concat(t));if f then f() end"
print(out)
