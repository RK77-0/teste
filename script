
-- Sistema de Load Única - Previne recarregar múltiplas vezes
if _G.UnifiedScriptLoaded then
    warn("⚠️ Script já foi carregado! Use: _G.UnifiedScriptLoaded = false para recarregar")
    return
end

_G.UnifiedScriptLoaded = true
print("✅ Script carregado com sucesso!")

--[[
    🎮 MENU UNIFICADO V1.0
    Camera + Visual FX
    Abre automaticamente ao injetar
]]

repeat task.wait() until game:IsLoaded()

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Lighting = game:GetService("Lighting")
local Workspace = game:GetService("Workspace")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local camera = Workspace.CurrentCamera

-- ========================
-- CONFIGURAÇÕES GLOBAIS
-- ========================
local Config = {
    -- Camera
    CameraEnabled = false,
    FOV = 85,
    CameraOffset = Vector3.new(1.2, 0.3, 0),
    
    -- Visual FX
    VisualEnabled = false
}

-- ========================
-- GUI PRINCIPAL
-- ========================
local gui = Instance.new("ScreenGui")
gui.Name = "UnifiedMenu"
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.IgnoreGuiInset = true

if gethui then
    gui.Parent = gethui()
elseif syn and syn.protect_gui then
    syn.protect_gui(gui)
    gui.Parent = game.CoreGui
else
    gui.Parent = game.CoreGui
end

-- Frame Principal
local main = Instance.new("Frame")
main.Parent = gui
main.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
main.BorderSizePixel = 0
main.Position = UDim2.new(0.5, -200, 0.5, -200)
main.Size = UDim2.new(0, 400, 0, 400)
main.Active = true
main.Visible = true
main.ClipsDescendants = true

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 12)
mainCorner.Parent = main

-- Sombra
local mainShadow = Instance.new("ImageLabel")
mainShadow.Parent = main
mainShadow.BackgroundTransparency = 1
mainShadow.Position = UDim2.new(0, -15, 0, -15)
mainShadow.Size = UDim2.new(1, 30, 1, 30)
mainShadow.ZIndex = 0
mainShadow.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
mainShadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
mainShadow.ImageTransparency = 0.5

-- Header
local header = Instance.new("Frame")
header.Parent = main
header.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
header.BorderSizePixel = 0
header.Size = UDim2.new(1, 0, 0, 60)

local headerCorner = Instance.new("UICorner")
headerCorner.CornerRadius = UDim.new(0, 12)
headerCorner.Parent = header

local headerAccent = Instance.new("Frame")
headerAccent.Parent = header
headerAccent.BackgroundColor3 = Color3.fromRGB(88, 166, 255)
headerAccent.BorderSizePixel = 0
headerAccent.Size = UDim2.new(1, 0, 0, 3)
headerAccent.Position = UDim2.new(0, 0, 1, -3)

local accentGradient = Instance.new("UIGradient")
accentGradient.Parent = headerAccent
accentGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(88, 166, 255)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(120, 190, 255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(88, 166, 255))
}

-- Drag System
local dragging, dragStart, startPos = false, nil, nil

header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = main.Position
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        main.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

-- Título
local icon = Instance.new("TextLabel")
icon.Parent = header
icon.BackgroundTransparency = 1
icon.Position = UDim2.new(0, 15, 0, 0)
icon.Size = UDim2.new(0, 40, 1, 0)
icon.Font = Enum.Font.GothamBold
icon.Text = "🎮"
icon.TextColor3 = Color3.fromRGB(88, 166, 255)
icon.TextSize = 24

local title = Instance.new("TextLabel")
title.Parent = header
title.BackgroundTransparency = 1
title.Position = UDim2.new(0, 55, 0, 5)
title.Size = UDim2.new(1, -110, 0, 25)
title.Font = Enum.Font.GothamBold
title.Text = "MENU UNIFICADO"
title.TextColor3 = Color3.fromRGB(240, 240, 240)
title.TextSize = 18
title.TextXAlignment = Enum.TextXAlignment.Left

local subtitle = Instance.new("TextLabel")
subtitle.Parent = header
subtitle.BackgroundTransparency = 1
subtitle.Position = UDim2.new(0, 55, 0, 30)
subtitle.Size = UDim2.new(1, -110, 0, 20)
subtitle.Font = Enum.Font.Gotham
subtitle.Text = "Camera • Visual FX"
subtitle.TextColor3 = Color3.fromRGB(120, 120, 120)
subtitle.TextSize = 12
subtitle.TextXAlignment = Enum.TextXAlignment.Left

-- Botão Fechar
local closeBtn = Instance.new("TextButton")
closeBtn.Parent = header
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
closeBtn.BorderSizePixel = 0
closeBtn.Position = UDim2.new(1, -45, 0.5, -18)
closeBtn.Size = UDim2.new(0, 36, 0, 36)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.Text = "×"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.TextSize = 24
closeBtn.AutoButtonColor = false

local closeBtnCorner = Instance.new("UICorner")
closeBtnCorner.CornerRadius = UDim.new(0, 8)
closeBtnCorner.Parent = closeBtn

closeBtn.MouseButton1Click:Connect(function()
    main.Visible = false
end)

closeBtn.MouseEnter:Connect(function()
    TweenService:Create(closeBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(255, 100, 100)}):Play()
end)

closeBtn.MouseLeave:Connect(function()
    TweenService:Create(closeBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(255, 70, 70)}):Play()
end)

-- Container de Tabs
local tabsContainer = Instance.new("Frame")
tabsContainer.Parent = main
tabsContainer.BackgroundTransparency = 1
tabsContainer.Position = UDim2.new(0, 15, 0, 70)
tabsContainer.Size = UDim2.new(1, -30, 0, 40)

local tabsLayout = Instance.new("UIListLayout")
tabsLayout.Parent = tabsContainer
tabsLayout.FillDirection = Enum.FillDirection.Horizontal
tabsLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
tabsLayout.Padding = UDim.new(0, 10)

-- Sistema de Tabs
local currentTab = "Camera"
local pages = {}

local function createTab(name, icon)
    local tab = Instance.new("TextButton")
    tab.Parent = tabsContainer
    tab.BackgroundColor3 = name == currentTab and Color3.fromRGB(88, 166, 255) or Color3.fromRGB(28, 28, 28)
    tab.BorderSizePixel = 0
    tab.Size = UDim2.new(0, 180, 1, 0)
    tab.Font = Enum.Font.GothamBold
    tab.Text = icon .. " " .. name
    tab.TextColor3 = name == currentTab and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(150, 150, 150)
    tab.TextSize = 14
    tab.AutoButtonColor = false
    
    local tabCorner = Instance.new("UICorner")
    tabCorner.CornerRadius = UDim.new(0, 8)
    tabCorner.Parent = tab
    
    return tab
end

local cameraTab = createTab("Camera", "📷")
local visualTab = createTab("Visual FX", "🌇")

-- Criar Páginas
local function createPage()
    local page = Instance.new("ScrollingFrame")
    page.Parent = main
    page.BackgroundTransparency = 1
    page.Position = UDim2.new(0, 15, 0, 120)
    page.Size = UDim2.new(1, -30, 1, -130)
    page.ScrollBarThickness = 4
    page.BorderSizePixel = 0
    page.ScrollBarImageColor3 = Color3.fromRGB(88, 166, 255)
    page.CanvasSize = UDim2.new(0, 0, 0, 0)
    page.AutomaticCanvasSize = Enum.AutomaticSize.Y
    page.Visible = false
    
    local layout = Instance.new("UIListLayout")
    layout.Parent = page
    layout.Padding = UDim.new(0, 10)
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    
    return page
end

pages.Camera = createPage()
pages.Visual = createPage()
pages.Camera.Visible = true

-- Switch Tab Function
local function switchTab(name, tab)
    currentTab = name
    
    for _, t in pairs({cameraTab, visualTab}) do
        t.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
        t.TextColor3 = Color3.fromRGB(150, 150, 150)
    end
    
    tab.BackgroundColor3 = Color3.fromRGB(88, 166, 255)
    tab.TextColor3 = Color3.fromRGB(255, 255, 255)
    
    for _, page in pairs(pages) do
        page.Visible = false
    end
    pages[name].Visible = true
end

cameraTab.MouseButton1Click:Connect(function() switchTab("Camera", cameraTab) end)
visualTab.MouseButton1Click:Connect(function() switchTab("Visual", visualTab) end)

-- ========================
-- FUNÇÕES DE UI
-- ========================
local function createToggle(parent, name, key, callback)
    local frame = Instance.new("Frame")
    frame.Parent = parent
    frame.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
    frame.BorderSizePixel = 0
    frame.Size = UDim2.new(1, 0, 0, 45)
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = frame
    
    local label = Instance.new("TextLabel")
    label.Parent = frame
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 15, 0, 0)
    label.Size = UDim2.new(1, -70, 1, 0)
    label.Font = Enum.Font.Gotham
    label.Text = name
    label.TextColor3 = Color3.fromRGB(220, 220, 220)
    label.TextSize = 14
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    local toggle = Instance.new("Frame")
    toggle.Parent = frame
    toggle.BackgroundColor3 = Config[key] and Color3.fromRGB(88, 166, 255) or Color3.fromRGB(45, 45, 45)
    toggle.BorderSizePixel = 0
    toggle.Position = UDim2.new(1, -52, 0.5, -11)
    toggle.Size = UDim2.new(0, 45, 0, 22)
    
    local toggleCorner = Instance.new("UICorner")
    toggleCorner.CornerRadius = UDim.new(1, 0)
    toggleCorner.Parent = toggle
    
    local circle = Instance.new("Frame")
    circle.Parent = toggle
    circle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    circle.BorderSizePixel = 0
    circle.Position = Config[key] and UDim2.new(1, -20, 0.5, -9) or UDim2.new(0, 2, 0.5, -9)
    circle.Size = UDim2.new(0, 18, 0, 18)
    
    local circleCorner = Instance.new("UICorner")
    circleCorner.CornerRadius = UDim.new(1, 0)
    circleCorner.Parent = circle
    
    local btn = Instance.new("TextButton")
    btn.Parent = frame
    btn.BackgroundTransparency = 1
    btn.Size = UDim2.new(1, 0, 1, 0)
    btn.Text = ""
    
    btn.MouseButton1Click:Connect(function()
        Config[key] = not Config[key]
        TweenService:Create(toggle, TweenInfo.new(0.2), {
            BackgroundColor3 = Config[key] and Color3.fromRGB(88, 166, 255) or Color3.fromRGB(45, 45, 45)
        }):Play()
        TweenService:Create(circle, TweenInfo.new(0.2), {
            Position = Config[key] and UDim2.new(1, -20, 0.5, -9) or UDim2.new(0, 2, 0.5, -9)
        }):Play()
        if callback then callback(Config[key]) end
    end)
    
    return frame
end

local function createSlider(parent, name, key, min, max, callback)
    local frame = Instance.new("Frame")
    frame.Parent = parent
    frame.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
    frame.BorderSizePixel = 0
    frame.Size = UDim2.new(1, 0, 0, 60)
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = frame
    
    local label = Instance.new("TextLabel")
    label.Parent = frame
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 15, 0, 8)
    label.Size = UDim2.new(1, -30, 0, 20)
    label.Font = Enum.Font.Gotham
    label.Text = name
    label.TextColor3 = Color3.fromRGB(220, 220, 220)
    label.TextSize = 14
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    local value = Instance.new("TextLabel")
    value.Parent = frame
    value.BackgroundTransparency = 1
    value.Position = UDim2.new(1, -60, 0, 8)
    value.Size = UDim2.new(0, 50, 0, 20)
    value.Font = Enum.Font.GothamBold
    value.Text = tostring(Config[key])
    value.TextColor3 = Color3.fromRGB(88, 166, 255)
    value.TextSize = 14
    value.TextXAlignment = Enum.TextXAlignment.Right
    
    local sliderBg = Instance.new("Frame")
    sliderBg.Parent = frame
    sliderBg.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    sliderBg.BorderSizePixel = 0
    sliderBg.Position = UDim2.new(0, 15, 1, -22)
    sliderBg.Size = UDim2.new(1, -30, 0, 6)
    
    local sliderBgCorner = Instance.new("UICorner")
    sliderBgCorner.CornerRadius = UDim.new(1, 0)
    sliderBgCorner.Parent = sliderBg
    
    local sliderFill = Instance.new("Frame")
    sliderFill.Parent = sliderBg
    sliderFill.BackgroundColor3 = Color3.fromRGB(88, 166, 255)
    sliderFill.BorderSizePixel = 0
    sliderFill.Size = UDim2.new((Config[key] - min) / (max - min), 0, 1, 0)
    
    local sliderFillCorner = Instance.new("UICorner")
    sliderFillCorner.CornerRadius = UDim.new(1, 0)
    sliderFillCorner.Parent = sliderFill
    
    local draggingSlider = false
    
    sliderBg.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            draggingSlider = true
        end
    end)
    
    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            draggingSlider = false
        end
    end)
    
    UserInputService.InputChanged:Connect(function(input)
        if draggingSlider and input.UserInputType == Enum.UserInputType.MouseMovement then
            local mousePos = UserInputService:GetMouseLocation()
            local relativePos = mousePos.X - sliderBg.AbsolutePosition.X
            local percentage = math.clamp(relativePos / sliderBg.AbsoluteSize.X, 0, 1)
            local newValue = math.floor(min + (max - min) * percentage)
            
            Config[key] = newValue
            value.Text = tostring(newValue)
            sliderFill.Size = UDim2.new(percentage, 0, 1, 0)
            
            if callback then callback(newValue) end
        end
    end)
    
    return frame
end

local function createButton(parent, name, callback)
    local btn = Instance.new("TextButton")
    btn.Parent = parent
    btn.BackgroundColor3 = Color3.fromRGB(88, 166, 255)
    btn.BorderSizePixel = 0
    btn.Size = UDim2.new(1, 0, 0, 45)
    btn.Font = Enum.Font.GothamBold
    btn.Text = name
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 14
    btn.AutoButtonColor = false
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = btn
    
    btn.MouseButton1Click:Connect(callback)
    
    btn.MouseEnter:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(100, 180, 255)}):Play()
    end)
    
    btn.MouseLeave:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(88, 166, 255)}):Play()
    end)
    
    return btn
end

-- ========================
-- PÁGINA CAMERA
-- ========================
createToggle(pages.Camera, "🎥 Ativar Camera Customizada", "CameraEnabled", function(value)
    if value then
        camera.FieldOfView = Config.FOV
    else
        camera.FieldOfView = 70
    end
end)

createSlider(pages.Camera, "🔍 Campo de Visão (FOV)", "FOV", 60, 120, function(value)
    if Config.CameraEnabled then
        camera.FieldOfView = value
    end
end)

-- ========================
-- PÁGINA VISUAL
-- ========================
createToggle(pages.Visual, "🌇 Ativar Efeitos Visuais", "VisualEnabled", function(value)
    if value then
        -- Limpar efeitos antigos
        for _, v in pairs(Lighting:GetChildren()) do
            if v:IsA("BloomEffect") or v:IsA("ColorCorrectionEffect") or v:IsA("SunRaysEffect") or v:IsA("BlurEffect") then
                v:Destroy()
            end
        end
        
        -- Aplicar configurações
        Lighting.Brightness = 2
        Lighting.ClockTime = 16.5
        Lighting.FogEnd = 2500
        Lighting.FogStart = 0
        Lighting.FogColor = Color3.fromRGB(255, 210, 160)
        Lighting.OutdoorAmbient = Color3.fromRGB(180, 120, 90)
        Lighting.Ambient = Color3.fromRGB(120, 80, 60)
        Lighting.ColorShift_Top = Color3.fromRGB(255, 180, 120)
        Lighting.ColorShift_Bottom = Color3.fromRGB(90, 60, 40)
        Lighting.ExposureCompensation = 0.2
        
        -- Criar efeitos
        local bloom = Instance.new("BloomEffect")
        bloom.Intensity = 0.04
        bloom.Size = 40
        bloom.Threshold = 0.2
        bloom.Parent = Lighting
        
        local color = Instance.new("ColorCorrectionEffect")
        color.Saturation = -0.03
        color.Contrast = 0.06
        color.TintColor = Color3.fromRGB(255, 230, 200)
        color.Parent = Lighting
        
        local sun = Instance.new("SunRaysEffect")
        sun.Intensity = 0.12
        sun.Spread = 0.2
        sun.Parent = Lighting
        
        local blur = Instance.new("BlurEffect")
        blur.Size = 0.5
        blur.Parent = Lighting
    else
        for _, v in pairs(Lighting:GetChildren()) do
            if v:IsA("BloomEffect") or v:IsA("ColorCorrectionEffect") or v:IsA("SunRaysEffect") or v:IsA("BlurEffect") then
                v:Destroy()
            end
        end
        
        Lighting.FogEnd = 10000
        Lighting.Ambient = Color3.fromRGB(128, 128, 128)
        Lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
        Lighting.ColorShift_Top = Color3.new(0,0,0)
        Lighting.ColorShift_Bottom = Color3.new(0,0,0)
        Lighting.Brightness = 1
    end
end)

createButton(pages.Visual, "🔄 Resetar para Padrão", function()
    Config.VisualEnabled = false
    for _, v in pairs(Lighting:GetChildren()) do
        if v:IsA("BloomEffect") or v:IsA("ColorCorrectionEffect") or v:IsA("SunRaysEffect") or v:IsA("BlurEffect") then
            v:Destroy()
        end
    end
    Lighting.FogEnd = 10000
    Lighting.Ambient = Color3.fromRGB(128, 128, 128)
    Lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
    Lighting.Brightness = 1
end)

-- ========================
-- SISTEMA DE CAMERA
-- ========================
RunService.RenderStepped:Connect(function()
    if not Config.CameraEnabled then return end
    
    local character = player.Character
    if not character then return end
    
    local head = character:FindFirstChild("Head")
    if not head then return end
    
    local camCFrame = camera.CFrame
    local offsetWorld = head.CFrame:VectorToWorldSpace(Config.CameraOffset)
    camera.CFrame = camCFrame + offsetWorld
end)

-- Notificação de carregamento
local function notify(text)
    game.StarterGui:SetCore("SendNotification", {
        Title = "Menu Unificado";
        Text = text;
        Duration = 3;
    })
end

notify("Menu carregado com sucesso!")
print("🎮 Menu Unificado carregado!")
print("📌 Menu aberto automaticamente")

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer
local mouse = player:GetMouse()

-- Definir as localizações
local locations = {
	{name = "Vila Principal", pos = Vector3.new(556, 9.71, 690)},
	{name = "Vila Pequena", pos = Vector3.new(-453, 54.51, 299)},
	{name = "Corporação Demon Slayer", pos = Vector3.new(-788, 9.72, -773)},
	{name = "Vila da Neve", pos = Vector3.new(1220, 9.31, -1612)},
	{name = "Zona de Perigo", pos = Vector3.new(11, 9.35, -1010)}
}

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TeleportMenu"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

-- Frame principal
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 250, 0, 40)
mainFrame.Position = UDim2.new(0.5, -125, 0, 10)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = screenGui

-- Botão para abrir/fechar menu
local toggleButton = Instance.new("TextButton")
toggleButton.Name = "ToggleButton"
toggleButton.Size = UDim2.new(1, 0, 1, 0)
toggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.TextSize = 18
toggleButton.Font = Enum.Font.GothamBold
toggleButton.Text = "Menu de Teleporte"
toggleButton.Parent = mainFrame

-- Frame do menu (lista de localizações)
local menuFrame = Instance.new("Frame")
menuFrame.Name = "MenuFrame"
menuFrame.Size = UDim2.new(0, 250, 0, 0)
menuFrame.Position = UDim2.new(0, 0, 1, 0)
menuFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
menuFrame.BorderSizePixel = 0
menuFrame.ClipsDescendants = true
menuFrame.Parent = mainFrame

-- ScrollingFrame para melhor UI
local scrollFrame = Instance.new("ScrollingFrame")
scrollFrame.Name = "ScrollFrame"
scrollFrame.Size = UDim2.new(1, 0, 1, 0)
scrollFrame.BackgroundTransparency = 1
scrollFrame.BorderSizePixel = 0
scrollFrame.ScrollBarThickness = 8
scrollFrame.Parent = menuFrame

-- Criar botões para cada localização
for i, location in ipairs(locations) do
	local button = Instance.new("TextButton")
	button.Name = location.name
	button.Size = UDim2.new(1, 0, 0, 40)
	button.Position = UDim2.new(0, 0, 0, (i - 1) * 40)
	button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
	button.TextColor3 = Color3.fromRGB(255, 255, 255)
	button.TextSize = 14
	button.Font = Enum.Font.Gotham
	button.Text = location.name
	button.Parent = scrollFrame
	
	-- Efeito de hover
	button.MouseEnter:Connect(function()
		button.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
	end)
	
	button.MouseLeave:Connect(function()
		button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
	end)
	
	-- Teleportar ao clicar
	button.MouseButton1Click:Connect(function()
		if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
			player.Character.HumanoidRootPart.CFrame = CFrame.new(location.pos)
		end
	end)
end

-- Atualizar tamanho do ScrollFrame
scrollFrame.CanvasSize = UDim2.new(0, 0, 0, #locations * 40)

-- Lógica de abrir/fechar menu
local menuOpen = false
local tweenService = game:GetService("TweenService")

local function toggleMenu()
	menuOpen = not menuOpen
	local targetSize = menuOpen and UDim2.new(0, 250, 0, math.min(#locations * 40, 200)) or UDim2.new(0, 250, 0, 0)
	local tweenInfo = TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut)
	local tween = tweenService:Create(menuFrame, tweenInfo, {Size = targetSize})
	tween:Play()
end

toggleButton.MouseButton1Click:Connect(toggleMenu)

-- Fechar menu ao clicar fora
mouse.Button1Down:Connect(function()
	if menuOpen then
		local mousePos = mouse.X
		local buttonPos = mainFrame.AbsolutePosition.X
		local buttonSize = mainFrame.AbsoluteSize.X
		
		if mousePos < buttonPos or mousePos > buttonPos + buttonSize then
			toggleMenu()
		end
	end
end)

local RunService = game:GetService("RunService")

local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local rootPart = character:WaitForChild("HumanoidRootPart")

-- Configurações
local JUMP_POWER = 50
local DOUBLE_JUMP_POWER = 60
local GROUND_CHECK_DISTANCE = 5
local DOUBLE_JUMP_COOLDOWN = 1

-- Estados
local isGrounded = false
local lastJumpTime = 0
local canDoubleJump = false
local hasUsedDoubleJump = false

-- Limpar scripts antigos
for _, child in pairs(rootPart:GetChildren()) do
    if child:IsA("BodyVelocity") or child:IsA("BodyGyro") or child:IsA("BodyPosition") then
        child:Destroy()
    end
end

-- Função para verificar se está no chão
local function checkGround()
    local rayOrigin = rootPart.Position + Vector3.new(0, 2, 0)
    local rayDirection = Vector3.new(0, -1, 0)
    local raycastParams = RaycastParams.new()
    raycastParams.FilterType = Enum.RaycastFilterType.Blacklist
    raycastParams.FilterDescendantsInstances = {character}
    
    local rayResult = workspace:Raycast(rayOrigin, rayDirection * GROUND_CHECK_DISTANCE, raycastParams)
    return rayResult ~= nil
end

-- Loop de detecção de solo
RunService.Heartbeat:Connect(function()
    local wasGrounded = isGrounded
    isGrounded = checkGround()
    
    if isGrounded and not wasGrounded then
        canDoubleJump = false
        hasUsedDoubleJump = false
    elseif not isGrounded and wasGrounded then
        canDoubleJump = true
    end
end)

-- DOUBLE JUMP COM PARTÍCULAS E ANIMAÇÃO
local function criarEfeitoDoubleJump()
    -- Destruir efeitos antigos
    for _, v in pairs(workspace:GetChildren()) do
        if v.Name == "DoubleJumpFX" then
            v:Destroy()
        end
    end
    
    -- CARREGAR ANIMAÇÃO
    local humanoid = character:FindFirstChild("Humanoid")
    if humanoid then
        local animator = humanoid:FindFirstChild("Animator")
        if not animator then
            animator = Instance.new("Animator")
            animator.Parent = humanoid
        end
        
        local animation = Instance.new("Animation")
        animation.AnimationId = "rbxassetid://18737420848"
        
        pcall(function()
            local animTrack = animator:LoadAnimation(animation)
            animTrack:Play()
        end)
    end
    
    local folder = Instance.new("Folder")
    folder.Name = "DoubleJumpFX"
    folder.Parent = workspace
    
    -- PARTÍCULAS BRANCAS EM VOLTA DO JOGADOR (25)
    for i = 1, 25 do
        local angle = (i / 25) * math.pi * 2
        local elevation = math.sin(angle * 3) * 1.5
        
        local particle = Instance.new("Part")
        particle.Shape = Enum.PartType.Ball
        particle.Size = Vector3.new(0.4, 0.4, 0.4)
        particle.Color = Color3.fromRGB(0, 0, 0)
        particle.Material = Enum.Material.Neon
        particle.CanCollide = false
        particle.CFrame = rootPart.CFrame + Vector3.new(math.cos(angle) * 4, elevation, math.sin(angle) * 4)
        particle.TopSurface = Enum.SurfaceType.Smooth
        particle.BottomSurface = Enum.SurfaceType.Smooth
        particle.Parent = folder
        
        local tweenPart = tweenService:Create(
            particle,
            TweenInfo.new(1, Enum.EasingStyle.Sine, Enum.EasingDirection.Out),
            {Size = Vector3.new(0.02, 0.02, 0.02), Transparency = 1}
        )
        tweenPart:Play()
        
        local startTime = tick()
        local conn
        conn = RunService.Heartbeat:Connect(function()
            local elapsed = tick() - startTime
            if elapsed < 1 then
                local radius = 4 + (elapsed * 3)
                local offset = Vector3.new(
                    math.cos(angle) * radius,
                    elevation + (elapsed * 2),
                    math.sin(angle) * radius
                )
                particle.CFrame = rootPart.CFrame + offset
            else
                conn:Disconnect()
            end
        end)
    end
    
    -- Sons finos e suaves
    local sounds = {
        {id = "rbxassetid://113971697134227", pitch = 1.1, volume = 1},
        {id = "rbxassetid://113971697134227", pitch = 1.3, volume = 5}
    }
    
    for _, soundData in pairs(sounds) do
        local sound = Instance.new("Sound")
        sound.SoundId = soundData.id
        sound.Volume = soundData.volume
        sound.Pitch = soundData.pitch
        sound.Parent = rootPart
        sound:Play()
        game:GetService("Debris"):AddItem(sound, 1.5)
    end
    
    game:GetService("Debris"):AddItem(folder, 1.2)
end

-- Input do double jump
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    
    if input.KeyCode == Enum.KeyCode.Space then
        if canDoubleJump and not hasUsedDoubleJump and (tick() - lastJumpTime) >= DOUBLE_JUMP_COOLDOWN then
            hasUsedDoubleJump = true
            lastJumpTime = tick()
            
            local vel = rootPart.AssemblyLinearVelocity
            rootPart.AssemblyLinearVelocity = Vector3.new(vel.X, 0, vel.Z)
            
            local bodyVelocity = Instance.new("BodyVelocity")
            bodyVelocity.Velocity = Vector3.new(0, DOUBLE_JUMP_POWER, 0)
            bodyVelocity.MaxForce = Vector3.new(0, math.huge, 0)
            bodyVelocity.Parent = rootPart
            
            game:GetService("Debris"):AddItem(bodyVelocity, 0.1)
            
            criarEfeitoDoubleJump()
        end
    end
end)

-- Recriar ao morrer
player.CharacterAdded:Connect(function(newCharacter)
    character = newCharacter
    humanoid = character:WaitForChild("Humanoid")
    rootPart = character:WaitForChild("HumanoidRootPart")
    isGrounded = false
    lastJumpTime = 0
    canDoubleJump = false
    hasUsedDoubleJump = false
    
    for _, child in pairs(rootPart:GetChildren()) do
        if child:IsA("BodyVelocity") or child:IsA("BodyGyro") or child:IsA("BodyPosition") then
            child:Destroy()
        end
    end
end)

-- ESP Premium Otimizado v3.1
local ESP = {
    Enabled = false,
    Players = false,
    NPCs = false,
    Box = false,
    Filled = false,
    Name = false,
    Distance = false,
    Health = false,
    HealthBar = false,
    HealthText = false,
    Tracers = false,
    TeamCheck = false,
    UseTeamColor = false,
    PlayerDistance = 1000,
    NPCDistance = 500,
    BoxColor = Color3.fromRGB(255, 50, 50),
    NPCColor = Color3.fromRGB(255, 200, 0),
    VisibleColor = Color3.fromRGB(0, 255, 0),
    NotVisibleColor = Color3.fromRGB(255, 0, 0),
    UseVisibilityCheck = false,
    TracerColor = Color3.fromRGB(255, 255, 255),
    BoxThickness = 2,
    TextSize = 13
}

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Workspace = game:GetService("Workspace")
local TweenService = game:GetService("TweenService")
local Camera = Workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer
local drawings = {}
local npcCache = {}
local connections = {}

-- Otimização: Cache de componentes
local componentCache = setmetatable({}, {__mode = "k"})

-- GUI Principal
local gui = Instance.new("ScreenGui")
gui.Name = "ESPPremium"
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.IgnoreGuiInset = true

if gethui then
    gui.Parent = gethui()
elseif syn and syn.protect_gui then
    syn.protect_gui(gui)
    gui.Parent = game.CoreGui
else
    gui.Parent = game.CoreGui
end

-- Frame Principal (reduzido e mais elegante)
local main = Instance.new("Frame")
main.Parent = gui
main.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
main.BorderSizePixel = 0
main.Position = UDim2.new(0.015, 0, 0.3, 0)
main.Size = UDim2.new(0, 300, 0, 420)
main.Active = true
main.ClipsDescendants = true

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 12)
mainCorner.Parent = main

local mainShadow = Instance.new("ImageLabel")
mainShadow.Parent = main
mainShadow.BackgroundTransparency = 1
mainShadow.Position = UDim2.new(0, -15, 0, -15)
mainShadow.Size = UDim2.new(1, 30, 1, 30)
mainShadow.ZIndex = 0
mainShadow.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
mainShadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
mainShadow.ImageTransparency = 0.5

-- Header Minimalista
local header = Instance.new("Frame")
header.Parent = main
header.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
header.BorderSizePixel = 0
header.Size = UDim2.new(1, 0, 0, 50)

local headerGradient = Instance.new("UIGradient")
headerGradient.Parent = header
headerGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(24, 24, 24)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(18, 18, 18))
}
headerGradient.Rotation = 90

local headerCorner = Instance.new("UICorner")
headerCorner.CornerRadius = UDim.new(0, 12)
headerCorner.Parent = header

local headerAccent = Instance.new("Frame")
headerAccent.Parent = header
headerAccent.BackgroundColor3 = Color3.fromRGB(88, 166, 255)
headerAccent.BorderSizePixel = 0
headerAccent.Size = UDim2.new(1, 0, 0, 2)
headerAccent.Position = UDim2.new(0, 0, 1, -2)

local accentGradient = Instance.new("UIGradient")
accentGradient.Parent = headerAccent
accentGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(88, 166, 255)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(120, 190, 255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(88, 166, 255))
}

-- Sistema de arrastar otimizado
local dragging, dragStart, startPos = false, nil, nil

header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = main.Position
    end
end)

local dragConnection = UserInputService.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        main.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

-- Título com ícone
local icon = Instance.new("TextLabel")
icon.Parent = header
icon.BackgroundTransparency = 1
icon.Position = UDim2.new(0, 15, 0, 0)
icon.Size = UDim2.new(0, 30, 1, 0)
icon.Font = Enum.Font.GothamBold
icon.Text = "⚡"
icon.TextColor3 = Color3.fromRGB(88, 166, 255)
icon.TextSize = 20

local title = Instance.new("TextLabel")
title.Parent = header
title.BackgroundTransparency = 1
title.Position = UDim2.new(0, 45, 0, 0)
title.Size = UDim2.new(1, -90, 1, 0)
title.Font = Enum.Font.GothamBold
title.Text = "ESP PREMIUM"
title.TextColor3 = Color3.fromRGB(240, 240, 240)
title.TextSize = 16
title.TextXAlignment = Enum.TextXAlignment.Left

local version = Instance.new("TextLabel")
version.Parent = header
version.BackgroundTransparency = 1
version.Position = UDim2.new(0, 45, 0, 20)
version.Size = UDim2.new(1, -90, 0, 15)
version.Font = Enum.Font.Gotham
version.Text = "v3.1"
version.TextColor3 = Color3.fromRGB(120, 120, 120)
version.TextSize = 11
version.TextXAlignment = Enum.TextXAlignment.Left

-- Botão X melhorado
local closeBtn = Instance.new("TextButton")
closeBtn.Parent = header
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
closeBtn.BorderSizePixel = 0
closeBtn.Position = UDim2.new(1, -38, 0.5, -15)
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.Text = "x"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.TextSize = 18
closeBtn.AutoButtonColor = false

local closeBtnCorner = Instance.new("UICorner")
closeBtnCorner.CornerRadius = UDim.new(0, 8)
closeBtnCorner.Parent = closeBtn

local function disableAndClose()
    ESP.Enabled = false
    for char, e in pairs(drawings) do
        pcall(function()
            for _, d in pairs(e) do
                if d and d.Remove then
                    d.Visible = false
                    d:Remove()
                end
            end
        end)
    end
    drawings = {}
    npcCache = {}
    for _, conn in pairs(connections) do
        if conn then conn:Disconnect() end
    end
    if dragConnection then dragConnection:Disconnect() end
    connections = {}
    gui:Destroy()
end

closeBtn.MouseButton1Click:Connect(disableAndClose)

closeBtn.MouseEnter:Connect(function()
    TweenService:Create(closeBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(255, 100, 100)}):Play()
end)

closeBtn.MouseLeave:Connect(function()
    TweenService:Create(closeBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(255, 70, 70)}):Play()
end)

-- Container de Tabs
local tabsContainer = Instance.new("Frame")
tabsContainer.Parent = main
tabsContainer.BackgroundTransparency = 1
tabsContainer.Position = UDim2.new(0, 10, 0, 58)
tabsContainer.Size = UDim2.new(1, -20, 0, 36)

local tabsLayout = Instance.new("UIListLayout")
tabsLayout.Parent = tabsContainer
tabsLayout.FillDirection = Enum.FillDirection.Horizontal
tabsLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
tabsLayout.Padding = UDim.new(0, 8)

-- Função para criar tabs
local currentTab = "ESP"
local function createTab(name)
    local tab = Instance.new("TextButton")
    tab.Parent = tabsContainer
    tab.BackgroundColor3 = name == currentTab and Color3.fromRGB(88, 166, 255) or Color3.fromRGB(28, 28, 28)
    tab.BorderSizePixel = 0
    tab.Size = UDim2.new(0, 135, 1, 0)
    tab.Font = Enum.Font.GothamBold
    tab.Text = name
    tab.TextColor3 = name == currentTab and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(150, 150, 150)
    tab.TextSize = 13
    tab.AutoButtonColor = false
    
    local tabCorner = Instance.new("UICorner")
    tabCorner.CornerRadius = UDim.new(0, 8)
    tabCorner.Parent = tab
    
    return tab
end

local espTab = createTab("ESP")
local configTab = createTab("CONFIG")

-- Páginas otimizadas
local function createPage()
    local page = Instance.new("ScrollingFrame")
    page.Parent = main
    page.BackgroundTransparency = 1
    page.Position = UDim2.new(0, 10, 0, 102)
    page.Size = UDim2.new(1, -20, 1, -112)
    page.ScrollBarThickness = 4
    page.BorderSizePixel = 0
    page.ScrollBarImageColor3 = Color3.fromRGB(88, 166, 255)
    page.CanvasSize = UDim2.new(0, 0, 0, 0)
    page.AutomaticCanvasSize = Enum.AutomaticSize.Y
    
    local layout = Instance.new("UIListLayout")
    layout.Parent = page
    layout.Padding = UDim.new(0, 8)
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    
    return page, layout
end

local espPage, espLayout = createPage()
local configPage, configLayout = createPage()
configPage.Visible = false

-- Sistema de Tabs
local function switchTab(name, tab, page)
    currentTab = name
    espTab.BackgroundColor3 = name == "ESP" and Color3.fromRGB(88, 166, 255) or Color3.fromRGB(28, 28, 28)
    espTab.TextColor3 = name == "ESP" and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(150, 150, 150)
    configTab.BackgroundColor3 = name == "CONFIG" and Color3.fromRGB(88, 166, 255) or Color3.fromRGB(28, 28, 28)
    configTab.TextColor3 = name == "CONFIG" and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(150, 150, 150)
    espPage.Visible = name == "ESP"
    configPage.Visible = name == "CONFIG"
end

espTab.MouseButton1Click:Connect(function() switchTab("ESP", espTab, espPage) end)
configTab.MouseButton1Click:Connect(function() switchTab("CONFIG", configTab, configPage) end)

-- Funções otimizadas de criação de elementos
local function createSection(parent, name)
    local section = Instance.new("Frame")
    section.Parent = parent
    section.BackgroundTransparency = 1
    section.Size = UDim2.new(1, 0, 0, 28)
    
    local label = Instance.new("TextLabel")
    label.Parent = section
    label.BackgroundTransparency = 1
    label.Size = UDim2.new(1, 0, 1, 0)
    label.Font = Enum.Font.GothamBold
    label.Text = name
    label.TextColor3 = Color3.fromRGB(88, 166, 255)
    label.TextSize = 13
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    local line = Instance.new("Frame")
    line.Parent = section
    line.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    line.BorderSizePixel = 0
    line.Position = UDim2.new(0, 0, 1, -1)
    line.Size = UDim2.new(1, 0, 0, 1)
    
    return section
end

local function createToggle(parent, name, key, callback)
    local frame = Instance.new("Frame")
    frame.Parent = parent
    frame.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
    frame.BorderSizePixel = 0
    frame.Size = UDim2.new(1, 0, 0, 40)
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = frame
    
    local label = Instance.new("TextLabel")
    label.Parent = frame
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 12, 0, 0)
    label.Size = UDim2.new(1, -60, 1, 0)
    label.Font = Enum.Font.Gotham
    label.Text = name
    label.TextColor3 = Color3.fromRGB(220, 220, 220)
    label.TextSize = 13
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    local toggle = Instance.new("Frame")
    toggle.Parent = frame
    toggle.BackgroundColor3 = ESP[key] and Color3.fromRGB(88, 166, 255) or Color3.fromRGB(45, 45, 45)
    toggle.BorderSizePixel = 0
    toggle.Position = UDim2.new(1, -48, 0.5, -10)
    toggle.Size = UDim2.new(0, 42, 0, 20)
    
    local toggleCorner = Instance.new("UICorner")
    toggleCorner.CornerRadius = UDim.new(1, 0)
    toggleCorner.Parent = toggle
    
    local circle = Instance.new("Frame")
    circle.Parent = toggle
    circle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    circle.BorderSizePixel = 0
    circle.Position = ESP[key] and UDim2.new(1, -18, 0.5, -8) or UDim2.new(0, 2, 0.5, -8)
    circle.Size = UDim2.new(0, 16, 0, 16)
    
    local circleCorner = Instance.new("UICorner")
    circleCorner.CornerRadius = UDim.new(1, 0)
    circleCorner.Parent = circle
    
    local btn = Instance.new("TextButton")
    btn.Parent = frame
    btn.BackgroundTransparency = 1
    btn.Size = UDim2.new(1, 0, 1, 0)
    btn.Text = ""
    
    btn.MouseButton1Click:Connect(function()
        ESP[key] = not ESP[key]
        TweenService:Create(toggle, TweenInfo.new(0.2), {
            BackgroundColor3 = ESP[key] and Color3.fromRGB(88, 166, 255) or Color3.fromRGB(45, 45, 45)
        }):Play()
        TweenService:Create(circle, TweenInfo.new(0.2), {
            Position = ESP[key] and UDim2.new(1, -18, 0.5, -8) or UDim2.new(0, 2, 0.5, -8)
        }):Play()
        if callback then callback(ESP[key]) end
    end)
end

local function createSlider(parent, name, key, min, max, suffix)
    local frame = Instance.new("Frame")
    frame.Parent = parent
    frame.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
    frame.BorderSizePixel = 0
    frame.Size = UDim2.new(1, 0, 0, 55)
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = frame
    
    local label = Instance.new("TextLabel")
    label.Parent = frame
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 12, 0, 8)
    label.Size = UDim2.new(1, -24, 0, 16)
    label.Font = Enum.Font.Gotham
    label.Text = name .. ": " .. ESP[key] .. suffix
    label.TextColor3 = Color3.fromRGB(220, 220, 220)
    label.TextSize = 13
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    local sliderBg = Instance.new("Frame")
    sliderBg.Parent = frame
    sliderBg.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    sliderBg.BorderSizePixel = 0
    sliderBg.Position = UDim2.new(0, 12, 0, 32)
    sliderBg.Size = UDim2.new(1, -24, 0, 6)
    
    local sliderCorner = Instance.new("UICorner")
    sliderCorner.CornerRadius = UDim.new(1, 0)
    sliderCorner.Parent = sliderBg
    
    local sliderFill = Instance.new("Frame")
    sliderFill.Parent = sliderBg
    sliderFill.BackgroundColor3 = Color3.fromRGB(88, 166, 255)
    sliderFill.BorderSizePixel = 0
    sliderFill.Size = UDim2.new((ESP[key] - min) / (max - min), 0, 1, 0)
    
    local fillCorner = Instance.new("UICorner")
    fillCorner.CornerRadius = UDim.new(1, 0)
    fillCorner.Parent = sliderFill
    
    local sliderDragging = false
    
    sliderBg.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            sliderDragging = true
        end
    end)
    
    table.insert(connections, UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            sliderDragging = false
        end
    end))
    
    table.insert(connections, UserInputService.InputChanged:Connect(function(input)
        if sliderDragging and input.UserInputType == Enum.UserInputType.MouseMovement then
            local pos = math.clamp((input.Position.X - sliderBg.AbsolutePosition.X) / sliderBg.AbsoluteSize.X, 0, 1)
            local value = math.floor(min + (max - min) * pos)
            ESP[key] = value
            sliderFill.Size = UDim2.new(pos, 0, 1, 0)
            label.Text = name .. ": " .. value .. suffix
        end
    end))
end

local function createColorPicker(parent, name, key)
    local frame = Instance.new("Frame")
    frame.Parent = parent
    frame.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
    frame.BorderSizePixel = 0
    frame.Size = UDim2.new(1, 0, 0, 40)
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = frame
    
    local label = Instance.new("TextLabel")
    label.Parent = frame
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 12, 0, 0)
    label.Size = UDim2.new(1, -60, 1, 0)
    label.Font = Enum.Font.Gotham
    label.Text = name
    label.TextColor3 = Color3.fromRGB(220, 220, 220)
    label.TextSize = 13
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    local colorBox = Instance.new("Frame")
    colorBox.Parent = frame
    colorBox.BackgroundColor3 = ESP[key]
    colorBox.BorderSizePixel = 0
    colorBox.Position = UDim2.new(1, -36, 0.5, -12)
    colorBox.Size = UDim2.new(0, 28, 0, 24)
    
    local colorCorner = Instance.new("UICorner")
    colorCorner.CornerRadius = UDim.new(0, 6)
    colorCorner.Parent = colorBox
    
    local colorStroke = Instance.new("UIStroke")
    colorStroke.Color = Color3.fromRGB(60, 60, 60)
    colorStroke.Thickness = 1
    colorStroke.Parent = colorBox
    
    local btn = Instance.new("TextButton")
    btn.Parent = colorBox
    btn.BackgroundTransparency = 1
    btn.Size = UDim2.new(1, 0, 1, 0)
    btn.Text = ""
    
    btn.MouseButton1Click:Connect(function()
        local colors = {
            Color3.fromRGB(255, 50, 50),
            Color3.fromRGB(255, 150, 0),
            Color3.fromRGB(255, 255, 0),
            Color3.fromRGB(0, 255, 0),
            Color3.fromRGB(88, 166, 255),
            Color3.fromRGB(150, 0, 255),
            Color3.fromRGB(255, 0, 255),
            Color3.fromRGB(255, 255, 255),
        }
        
        local currentIndex = 1
        for i, color in ipairs(colors) do
            if ESP[key] == color then
                currentIndex = i
                break
            end
        end
        
        currentIndex = currentIndex % #colors + 1
        ESP[key] = colors[currentIndex]
        TweenService:Create(colorBox, TweenInfo.new(0.2), {BackgroundColor3 = ESP[key]}):Play()
    end)
end

-- Criar Interface ESP
createSection(espPage, "GERAL")
createToggle(espPage, "ESP Ativado", "Enabled")
createToggle(espPage, "Mostrar Jogadores", "Players")
createToggle(espPage, "Mostrar NPCs", "NPCs")
createToggle(espPage, "Verificar Time", "TeamCheck")

createSection(espPage, "VISUAL")
createToggle(espPage, "Caixa", "Box")
createToggle(espPage, "Caixa Preenchida", "Filled")
createToggle(espPage, "Nome", "Name")
createToggle(espPage, "Distância", "Distance")
createToggle(espPage, "HP (Texto)", "HealthText")
createToggle(espPage, "Barra de HP", "HealthBar")
createToggle(espPage, "Linhas (Tracers)", "Tracers")

createSection(espPage, "DISTÂNCIA")
createSlider(espPage, "Jogadores", "PlayerDistance", 100, 3000, "m")
createSlider(espPage, "NPCs", "NPCDistance", 100, 2000, "m")

-- Criar Interface CONFIG
createSection(configPage, "VISIBILIDADE")
createToggle(configPage, "Checar Visibilidade", "UseVisibilityCheck")
createColorPicker(configPage, "Cor Visível", "VisibleColor")
createColorPicker(configPage, "Cor Não Visível", "NotVisibleColor")

createSection(configPage, "CORES")
createToggle(configPage, "Usar Cor do Time", "UseTeamColor")
createColorPicker(configPage, "Cor Jogadores", "BoxColor")
createColorPicker(configPage, "Cor NPCs", "NPCColor")
createColorPicker(configPage, "Cor Linhas", "TracerColor")

createSection(configPage, "CONFIGURAÇÕES")
createSlider(configPage, "Espessura da Linha", "BoxThickness", 1, 5, "px")
createSlider(configPage, "Tamanho do Texto", "TextSize", 10, 20, "px")

-- Tecla Toggle
table.insert(connections, UserInputService.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Insert then
        main.Visible = not main.Visible
    end
end))

-- Sistema ESP (igual ao anterior)
local function newESP(char, isNPC)
    if drawings[char] then return end
    
    local e = {
        box = Drawing.new("Square"),
        boxFill = Drawing.new("Square"),
        name = Drawing.new("Text"),
        dist = Drawing.new("Text"),
        hp = Drawing.new("Text"),
        hpBar = Drawing.new("Square"),
        hpOut = Drawing.new("Square"),
        tracer = Drawing.new("Line"),
        npc = isNPC,
        char = char
    }
    
    e.box.Thickness = ESP.BoxThickness
    e.box.Filled = false
    e.box.Transparency = 1
    e.box.ZIndex = 2
    e.box.Visible = false
    
    e.boxFill.Filled = true
    e.boxFill.Transparency = 0.15
    e.boxFill.ZIndex = 1
    e.boxFill.Visible = false
    
    e.name.Size = ESP.TextSize
    e.name.Center = true
    e.name.Outline = true
    e.name.ZIndex = 2
    e.name.Visible = false
    
    e.dist.Size = ESP.TextSize - 1
    e.dist.Center = true
    e.dist.Outline = true
    e.dist.ZIndex = 2
    e.dist.Visible = false
    
    e.hp.Size = ESP.TextSize - 1
    e.hp.Center = true
    e.hp.Outline = true
    e.hp.ZIndex = 2
    e.hp.Visible = false
    
    e.hpOut.Filled = false
    e.hpOut.Thickness = 1
    e.hpOut.Color = Color3.new(0, 0, 0)
    e.hpOut.Transparency = 1
    e.hpOut.ZIndex = 1
    e.hpOut.Visible = false
    
    e.hpBar.Filled = true
    e.hpBar.Transparency = 1
    e.hpBar.ZIndex = 2
    e.hpBar.Visible = false
    
    e.tracer.Thickness = 1
    e.tracer.Transparency = 0.7
    e.tracer.ZIndex = 1
    e.tracer.Visible = false
    
    drawings[char] = e
end

local function removeESP(char)
    if drawings[char] then
        pcall(function()
            for _, d in pairs(drawings[char]) do
                if d and d.Remove then
                    d.Visible = false
                    d:Remove()
                end
            end
        end)
        drawings[char] = nil
    end
end

local function isNPC(m)
    return m:IsA("Model") and m:FindFirstChild("Humanoid") and m:FindFirstChild("HumanoidRootPart") and not Players:GetPlayerFromCharacter(m)
end

local function isVisible(from, to, character)
    local params = RaycastParams.new()
    params.FilterDescendantsInstances = {LocalPlayer.Character, character, Camera}
    params.FilterType = Enum.RaycastFilterType.Blacklist
    params.IgnoreWater = true
    
    local direction = (to - from)
    local distance = direction.Magnitude
    local result = Workspace:Raycast(from, direction.Unit * distance, params)
    
    if not result then return true end
    if result.Instance then
        return result.Instance:IsDescendantOf(character)
    end
    return false
end

-- Jogadores
for _, p in pairs(Players:GetPlayers()) do
    if p ~= LocalPlayer then
        table.insert(connections, p.CharacterAdded:Connect(function(c)
            task.wait(0.3)
            if c and c.Parent then newESP(c, false) end
        end))
        if p.Character then newESP(p.Character, false) end
    end
end

table.insert(connections, Players.PlayerAdded:Connect(function(p)
    table.insert(connections, p.CharacterAdded:Connect(function(c)
        task.wait(0.3)
        if c and c.Parent then newESP(c, false) end
    end))
end))

table.insert(connections, Players.PlayerRemoving:Connect(function(p)
    if p.Character then removeESP(p.Character) end
end))

-- NPCs com cache otimizado
local function addNPC(m)
    if not isNPC(m) or npcCache[m] then return end
    npcCache[m] = true
    newESP(m, true)
    
    local conn = m.AncestryChanged:Connect(function(_, parent)
        if not parent then
            removeESP(m)
            npcCache[m] = nil
        end
    end)
    table.insert(connections, conn)
end

for _, v in pairs(Workspace:GetDescendants()) do
    if v:IsA("Model") then addNPC(v) end
end

table.insert(connections, Workspace.DescendantAdded:Connect(function(d)
    if d:IsA("Model") then
        task.wait(0.2)
        addNPC(d)
    elseif d:IsA("Humanoid") or d.Name == "HumanoidRootPart" then
        task.wait(0.2)
        if d.Parent and d.Parent:IsA("Model") then addNPC(d.Parent) end
    end
end))

-- Update Loop Otimizado
local lastUpdate = tick()
local updateInterval = 1/60 -- 60 FPS

table.insert(connections, RunService.RenderStepped:Connect(function()
    local now = tick()
    if now - lastUpdate < updateInterval then return end
    lastUpdate = now
    
    if not ESP.Enabled or not LocalPlayer.Character or not LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        for _, e in pairs(drawings) do
            e.box.Visible = false
            e.boxFill.Visible = false
            e.name.Visible = false
            e.dist.Visible = false
            e.hp.Visible = false
            e.hpBar.Visible = false
            e.hpOut.Visible = false
            e.tracer.Visible = false
        end
        return
    end
    
    local lRoot = LocalPlayer.Character.HumanoidRootPart
    local viewportSize = Camera.ViewportSize
    
    for char, e in pairs(drawings) do
        if not char or not char.Parent or not char:FindFirstChild("HumanoidRootPart") or not char:FindFirstChild("Humanoid") then
            e.box.Visible = false
            e.boxFill.Visible = false
            e.name.Visible = false
            e.dist.Visible = false
            e.hp.Visible = false
            e.hpBar.Visible = false
            e.hpOut.Visible = false
            e.tracer.Visible = false
            continue
        end
        
        local root = char.HumanoidRootPart
        local hum = char.Humanoid
        local head = char:FindFirstChild("Head")
        
        if hum.Health <= 0 or not head then
            e.box.Visible = false
            e.boxFill.Visible = false
            e.name.Visible = false
            e.dist.Visible = false
            e.hp.Visible = false
            e.hpBar.Visible = false
            e.hpOut.Visible = false
            e.tracer.Visible = false
            continue
        end
        
        local dist = (lRoot.Position - root.Position).Magnitude
        local maxDist = e.npc and ESP.NPCDistance or ESP.PlayerDistance
        
        if dist > maxDist then
            e.box.Visible = false
            e.boxFill.Visible = false
            e.name.Visible = false
            e.dist.Visible = false
            e.hp.Visible = false
            e.hpBar.Visible = false
            e.hpOut.Visible = false
            e.tracer.Visible = false
            continue
        end
        
        if (e.npc and not ESP.NPCs) or (not e.npc and not ESP.Players) then
            e.box.Visible = false
            e.boxFill.Visible = false
            e.name.Visible = false
            e.dist.Visible = false
            e.hp.Visible = false
            e.hpBar.Visible = false
            e.hpOut.Visible = false
            e.tracer.Visible = false
            continue
        end
        
        if not e.npc and ESP.TeamCheck then
            local p = Players:GetPlayerFromCharacter(char)
            if p and p.Team == LocalPlayer.Team then
                e.box.Visible = false
                e.boxFill.Visible = false
                e.name.Visible = false
                e.dist.Visible = false
                e.hp.Visible = false
                e.hpBar.Visible = false
                e.hpOut.Visible = false
                e.tracer.Visible = false
                continue
            end
        end
        
        local vec, onScreen = Camera:WorldToViewportPoint(root.Position)
        
        if onScreen then
            local headPos = Camera:WorldToViewportPoint(head.Position + Vector3.new(0, 0.5, 0))
            local legPos = Camera:WorldToViewportPoint(root.Position - Vector3.new(0, 3, 0))
            local h = math.abs(headPos.Y - legPos.Y)
            local w = h / 2
            
            local col = e.npc and ESP.NPCColor or ESP.BoxColor
            
            if ESP.UseVisibilityCheck then
                local targetPos = head.Position
                local visible = isVisible(Camera.CFrame.Position, targetPos, char)
                col = visible and ESP.VisibleColor or ESP.NotVisibleColor
            elseif not e.npc and ESP.UseTeamColor then
                local p = Players:GetPlayerFromCharacter(char)
                if p and p.TeamColor then 
                    col = p.TeamColor.Color 
                end
            end
            
            e.box.Thickness = ESP.BoxThickness
            e.name.Size = ESP.TextSize
            e.dist.Size = ESP.TextSize - 1
            e.hp.Size = ESP.TextSize - 1
            
            if ESP.Box then
                e.box.Size = Vector2.new(w, h)
                e.box.Position = Vector2.new(vec.X - w/2, vec.Y - h/2)
                e.box.Color = col
                e.box.Visible = true
                
                if ESP.Filled then
                    e.boxFill.Size = Vector2.new(w, h)
                    e.boxFill.Position = Vector2.new(vec.X - w/2, vec.Y - h/2)
                    e.boxFill.Color = col
                    e.boxFill.Visible = true
                else
                    e.boxFill.Visible = false
                end
            else
                e.box.Visible = false
                e.boxFill.Visible = false
            end
            
            if ESP.Name then
                e.name.Text = char.Name
                e.name.Position = Vector2.new(vec.X, headPos.Y - 18)
                e.name.Color = col
                e.name.Visible = true
            else
                e.name.Visible = false
            end
            
            if ESP.Distance then
                e.dist.Text = math.floor(dist) .. "m"
                e.dist.Position = Vector2.new(vec.X, legPos.Y + 5)
                e.dist.Color = Color3.new(1, 1, 1)
                e.dist.Visible = true
            else
                e.dist.Visible = false
            end
            
            if ESP.HealthText then
                local pct = math.floor((hum.Health / hum.MaxHealth) * 100)
                e.hp.Text = pct .. "%"
                e.hp.Position = Vector2.new(vec.X, legPos.Y + 18)
                e.hp.Color = Color3.fromRGB(255 - pct * 2.55, pct * 2.55, 0)
                e.hp.Visible = true
            else
                e.hp.Visible = false
            end
            
            if ESP.HealthBar then
                local pct = hum.Health / hum.MaxHealth
                local barX = vec.X - w/2 - 6
                local barY = vec.Y - h/2
                
                e.hpOut.Size = Vector2.new(3, h)
                e.hpOut.Position = Vector2.new(barX, barY)
                e.hpOut.Visible = true
                
                local hpH = h * pct
                e.hpBar.Size = Vector2.new(2, hpH)
                e.hpBar.Position = Vector2.new(barX + 0.5, barY + (h - hpH))
                e.hpBar.Color = Color3.fromRGB(255 - pct * 255, pct * 255, 0)
                e.hpBar.Visible = true
            else
                e.hpBar.Visible = false
                e.hpOut.Visible = false
            end
            
            if ESP.Tracers then
                e.tracer.From = Vector2.new(viewportSize.X / 2, viewportSize.Y)
                e.tracer.To = Vector2.new(vec.X, vec.Y)
                e.tracer.Color = ESP.TracerColor
                e.tracer.Visible = true
            else
                e.tracer.Visible = false
            end
        else
            e.box.Visible = false
            e.boxFill.Visible = false
            e.name.Visible = false
            e.dist.Visible = false
            e.hp.Visible = false
            e.hpBar.Visible = false
            e.hpOut.Visible = false
            e.tracer.Visible = false
        end
    end
end))
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Configurações
local Config = {
    DefaultSpeed = 16,
    MinSpeed = 0,
    MaxSpeed = 500,
    ToggleKey = Enum.KeyCode.P
}

local currentSpeed = Config.DefaultSpeed
local guiVisible = true

-- Criação da GUI
local function createGui()
    local gui = Instance.new("ScreenGui")
    gui.Name = "SpeedControlGUI"
    gui.ResetOnSpawn = false
    gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    
    local frame = Instance.new("Frame")
    frame.Name = "MainFrame"
    frame.Size = UDim2.new(0, 220, 0, 150)
    frame.Position = UDim2.new(0.5, -110, 0.5, -75)
    frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    frame.BorderSizePixel = 0
    frame.Active = true
    frame.Draggable = true
    frame.Parent = gui
    
    -- Arredondamento de cantos
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = frame
    
    -- Sombra
    local shadow = Instance.new("ImageLabel")
    shadow.Name = "Shadow"
    shadow.Size = UDim2.new(1, 30, 1, 30)
    shadow.Position = UDim2.new(0, -15, 0, -15)
    shadow.BackgroundTransparency = 1
    shadow.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
    shadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
    shadow.ImageTransparency = 0.5
    shadow.ZIndex = 0
    shadow.Parent = frame
    
    -- Header
    local header = Instance.new("Frame")
    header.Name = "Header"
    header.Size = UDim2.new(1, 0, 0, 35)
    header.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    header.BorderSizePixel = 0
    header.Parent = frame
    
    local headerCorner = Instance.new("UICorner")
    headerCorner.CornerRadius = UDim.new(0, 8)
    headerCorner.Parent = header
    
    -- Corrige cantos inferiores do header
    local headerFix = Instance.new("Frame")
    headerFix.Size = UDim2.new(1, 0, 0, 8)
    headerFix.Position = UDim2.new(0, 0, 1, -8)
    headerFix.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    headerFix.BorderSizePixel = 0
    headerFix.Parent = header
    
    local label = Instance.new("TextLabel")
    label.Name = "Title"
    label.Size = UDim2.new(1, -10, 1, 0)
    label.Position = UDim2.new(0, 10, 0, 0)
    label.Text = "⚡ Speed Control"
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextSize = 16
    label.Font = Enum.Font.GothamBold
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.BackgroundTransparency = 1
    label.Parent = header
    
    -- TextBox para velocidade
    local textBox = Instance.new("TextBox")
    textBox.Name = "SpeedInput"
    textBox.Size = UDim2.new(0, 200, 0, 40)
    textBox.Position = UDim2.new(0, 10, 0, 45)
    textBox.Text = tostring(Config.DefaultSpeed)
    textBox.PlaceholderText = "Digite a velocidade"
    textBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
    textBox.TextSize = 14
    textBox.Font = Enum.Font.Gotham
    textBox.ClearTextOnFocus = false
    textBox.Parent = frame
    
    local textBoxCorner = Instance.new("UICorner")
    textBoxCorner.CornerRadius = UDim.new(0, 6)
    textBoxCorner.Parent = textBox
    
    -- Botão reset
    local button = Instance.new("TextButton")
    button.Name = "ResetButton"
    button.Size = UDim2.new(0, 200, 0, 35)
    button.Position = UDim2.new(0, 10, 0, 95)
    button.Text = "🔄 Resetar Velocidade"
    button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextSize = 14
    button.Font = Enum.Font.GothamBold
    button.AutoButtonColor = false
    button.Parent = frame
    
    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0, 6)
    buttonCorner.Parent = button
    
    gui.Parent = playerGui
    
    return gui, textBox, button
end

-- Funções auxiliares
local function setSpeed(newSpeed)
    if newSpeed < Config.MinSpeed then newSpeed = Config.MinSpeed end
    if newSpeed > Config.MaxSpeed then newSpeed = Config.MaxSpeed end
    
    currentSpeed = newSpeed
    
    local character = player.Character
    if character then
        local humanoid = character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = currentSpeed
        end
    end
end

local function animateButton(button, color)
    local tween = TweenService:Create(
        button,
        TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
        {BackgroundColor3 = color}
    )
    tween:Play()
end

-- Inicialização
local gui, textBox, button = createGui()

-- Eventos da TextBox
textBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local newSpeed = tonumber(textBox.Text)
        if newSpeed then
            setSpeed(newSpeed)
        else
            textBox.Text = tostring(currentSpeed)
        end
    end
end)

-- Eventos do Botão
button.MouseEnter:Connect(function()
    animateButton(button, Color3.fromRGB(80, 80, 80))
end)

button.MouseLeave:Connect(function()
    animateButton(button, Color3.fromRGB(60, 60, 60))
end)

button.MouseButton1Click:Connect(function()
    animateButton(button, Color3.fromRGB(100, 100, 100))
    task.wait(0.1)
    animateButton(button, Color3.fromRGB(80, 80, 80))
    
    setSpeed(Config.DefaultSpeed)
    textBox.Text = tostring(Config.DefaultSpeed)
end)

-- Mantém a velocidade constante
RunService.Stepped:Connect(function()
    local character = player.Character
    if character then
        local humanoid = character:FindFirstChild("Humanoid")
        if humanoid and humanoid.WalkSpeed ~= currentSpeed then
            humanoid.WalkSpeed = currentSpeed
        end
    end
end)

-- Toggle da GUI
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if input.KeyCode == Config.ToggleKey and not gameProcessed then
        guiVisible = not guiVisible
        gui.Enabled = guiVisible
    end
end)

-- Aplica velocidade ao spawnar
player.CharacterAdded:Connect(function(character)
    local humanoid = character:WaitForChild("Humanoid")
    humanoid.WalkSpeed = currentSpeed
end)

-- Configuração inicial
setSpeed(Config.DefaultSpeed)

loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()


loadstring(game:HttpGet("https://raw.githubusercontent.com/L4BIBKAZI/L4BIB-HUB/refs/heads/main/Weak%20Legacy%202"))()
