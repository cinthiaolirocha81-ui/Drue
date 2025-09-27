-- 🐸 Frog Hub v14 - Painel baixo com botão Float v2
local keyNeeded = "hubfrg45637"
local linkKey = "https://rkns.link/flbbj"

local player = game.Players.LocalPlayer

-- GUI principal
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 320, 0, 200) -- painel baixo
Frame.Position = UDim2.new(0.3, 0, 0.3, 0)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
Frame.Active = true
Frame.Draggable = true
Frame.ClipsDescendants = true

-- Título
local Titulo = Instance.new("TextLabel", Frame)
Titulo.Size = UDim2.new(1, -20, 0, 50)
Titulo.Position = UDim2.new(0, 10, 0, 10)
Titulo.BackgroundTransparency = 1
Titulo.Text = "🐸 Frog Hub v14"
Titulo.TextColor3 = Color3.fromRGB(0, 255, 150)
Titulo.Font = Enum.Font.GothamBlack
Titulo.TextSize = 30
Titulo.TextScaled = true

-- Caixa de Key
local CaixaKey = Instance.new("TextBox", Frame)
CaixaKey.Size = UDim2.new(1, -20, 0, 40)
CaixaKey.Position = UDim2.new(0, 10, 0, 70)
CaixaKey.PlaceholderText = "Digite a Key..."
CaixaKey.TextScaled = true
CaixaKey.TextColor3 = Color3.fromRGB(255,255,255)
CaixaKey.BackgroundColor3 = Color3.fromRGB(40,40,50)
CaixaKey.BorderSizePixel = 0

-- Botão Copiar Link
local CopiarLink = Instance.new("TextButton", Frame)
CopiarLink.Size = UDim2.new(1, -20, 0, 30)
CopiarLink.Position = UDim2.new(0, 10, 0, 120)
CopiarLink.Text = "📋 Copiar Link"
CopiarLink.TextScaled = true
CopiarLink.BackgroundColor3 = Color3.fromRGB(0,255,150)
CopiarLink.TextColor3 = Color3.fromRGB(20,20,20)
CopiarLink.BorderSizePixel = 0
CopiarLink.MouseButton1Click:Connect(function()
    setclipboard(linkKey)
end)

-- Frame para funções
local FuncoesContainer = Instance.new("Frame", Frame)
FuncoesContainer.Size = UDim2.new(1, -20, 0, 50)
FuncoesContainer.Position = UDim2.new(0, 10, 0, 160)
FuncoesContainer.BackgroundTransparency = 1
FuncoesContainer.Visible = false

local floatV2Bloco
local lastClick = 0

-- Função Float v2
local function criarFloatV2()
    local now = tick()
    if now - lastClick < 0.3 then
        if floatV2Bloco then
            floatV2Bloco:Destroy()
            floatV2Bloco = nil
        end
        return
    end
    lastClick = now

    if not floatV2Bloco then
        floatV2Bloco = Instance.new("Part", workspace)
        floatV2Bloco.Size = Vector3.new(6,1,6)
        floatV2Bloco.Anchored = true
        floatV2Bloco.CanCollide = true
        floatV2Bloco.Transparency = 1
        floatV2Bloco.Position = player.Character.HumanoidRootPart.Position - Vector3.new(0,3,0)

        task.spawn(function()
            while floatV2Bloco and task.wait(0.05) do -- aumenta a velocidade
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    floatV2Bloco.Position = player.Character.HumanoidRootPart.Position - Vector3.new(0,3,0)
                end
            end
        end)
    end
end

-- Checar Key
CaixaKey.FocusLost:Connect(function()
    if CaixaKey.Text == keyNeeded then
        FuncoesContainer.Visible = true

        -- Criar botão Float v2
        local BtnFloat = Instance.new("TextButton", FuncoesContainer)
        BtnFloat.Size = UDim2.new(1,0,0,35)
        BtnFloat.Position = UDim2.new(0,0,0,0)
        BtnFloat.Text = "💠 Float v2"
        BtnFloat.TextScaled = true
        BtnFloat.BackgroundColor3 = Color3.fromRGB(0,255,150)
        BtnFloat.TextColor3 = Color3.fromRGB(20,20,20)
        BtnFloat.BorderSizePixel = 0
        BtnFloat.MouseButton1Click:Connect(criarFloatV2)
    else
        CaixaKey.Text = "❌ Key Errada"
    end
end)
