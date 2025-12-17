local TextChatService = game:GetService("TextChatService")
local UserInputService = game:GetService("UserInputService")
local player = game.Players.LocalPlayer

local comandos = { "/Mat55🇳🇬👆🏻", "/render🇳🇬🐊", "/furar pneus 💨👑", "/pegar 🇳🇬🐊" }
local iniciais = { ["/Mat55🇳🇬👆🏻"] = "M", ["/render🇳🇬🐊"] = "R", ["/furar pneus 💨👑"] = "F", ["/pegar 🇳🇬🐊"] = "P" }
local delays = { ["/Mat55🇳🇬👆🏻"] = 0.2, ["/render🇳🇬🐊"] = 0.2, ["/furar pneus 💨👑"] = 0.2, ["/pegar 🇳🇬🐊"] = 0.2 }
local reps = { ["/Mat55🇳🇬👆🏻"] = 1, ["/render🇳🇬🐊"] = 1, ["/furar pneus 💨👑"] = 1, ["/pegar 🇳🇬🐊"] = 1 }
local spamThreads, spamON = {}, {}
local mainGui = nil
local actionBtnsGui = nil

-- VERDE DO PAINEL (nem claro nem escuro)
local corUi = Color3.fromRGB(60, 190, 100)     
local painelLargura = 345                       -- Largura compacta e confortável
local painelAltura = 170 + #comandos*63         -- Altura compacta

local corTitulo = Color3.fromRGB(50, 165, 100)
local corLabelCinza = Color3.fromRGB(120,120,120)
local corBotao = Color3.fromRGB(230,230,230)
local corBotaoHover = Color3.fromRGB(210,210,210)
local corTextoBotao = Color3.fromRGB(60,60,60)

function dragify(Frame)
    Frame.Active = true
    Frame.Selectable = true
    local UIS = game:GetService("UserInputService")
    local dragging, dragInput, dragStart, startPos

    Frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = Frame.Position
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then dragging = false end
            end)
        end
    end)
    Frame.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)
    UIS.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            Frame.Position = UDim2.new(
                startPos.X.Scale,
                startPos.X.Offset + delta.X,
                startPos.Y.Scale,
                startPos.Y.Offset + delta.Y
            )
        end
    end)
end

local function spammarComando(comando)
    spamON[comando] = true
    local delay = tonumber(delays[comando]) or 0.2
    if delay < 0.1 then delay = 0.1 end
    local repeticoes = tonumber(reps[comando]) or 1

    local channel = (TextChatService.TextChannels and TextChatService.TextChannels:FindFirstChild("RBXGeneral"))
        or (TextChatService:FindFirstChild("TextChannels") and TextChatService:FindFirstChild("TextChannels"):FindFirstChild("RBXGeneral"))
        or TextChatService:FindFirstChild("RBXGeneral")
        or TextChatService:FindFirstChild("General")
        or TextChatService:FindFirstChild("All")

    spamThreads[comando] = task.spawn(function()
        for i = 1, repeticoes do
            if channel and spamON[comando] then
                channel:SendAsync(comando)
            end
            task.wait(delay)
        end
        spamON[comando] = false
    end)
end

local function pararSpam(comando)
    spamON[comando] = false
end

local function showActionButtons()
    if actionBtnsGui then actionBtnsGui:Destroy() end
    actionBtnsGui = Instance.new("ScreenGui")
    actionBtnsGui.Parent = player:WaitForChild("PlayerGui")
    actionBtnsGui.Name = "ActionBtns"

    for i,cmd in ipairs(comandos) do
        local letra = iniciais[cmd]
        local btn = Instance.new("TextButton", actionBtnsGui)
        btn.Size = UDim2.new(0,48,0,48)
        btn.Position = UDim2.new(0, 25 + (i-1)*70, 1, -90)
        btn.BackgroundColor3 = corBotao
        btn.Text = letra
        btn.Font = Enum.Font.Gotham
        btn.TextSize = 28
        btn.TextColor3 = corTitulo
        btn.Name = "Btn_"..cmd
        btn.Active = true
        btn.Selectable = true
        btn.AutoButtonColor = false
        local corner = Instance.new("UICorner", btn)
        corner.CornerRadius = UDim.new(1,0)
        local stroke = Instance.new("UIStroke", btn)
        stroke.Color = Color3.fromRGB(200, 200, 200)
        stroke.Thickness = 1.1
        btn.MouseEnter:Connect(function()
            btn.BackgroundColor3 = corBotaoHover
        end)
        btn.MouseLeave:Connect(function()
            btn.BackgroundColor3 = corBotao
        end)
        dragify(btn)
        btn.MouseButton1Click:Connect(function()
            btn.Text = "▶️"
            spammarComando(cmd)
            coroutine.wrap(function()
                while spamON[cmd] do wait(0.1) end
                btn.Text = letra
            end)()
        end)
    end
end

local function hideActionButtons()
    if actionBtnsGui then actionBtnsGui:Destroy() actionBtnsGui = nil end
end

local function createMainGui()
    local gui = Instance.new("ScreenGui")
    gui.Name = "GrotaUI"
    gui.Parent = player:WaitForChild("PlayerGui")
    mainGui = gui

    local frame = Instance.new("Frame", gui)
    frame.Size = UDim2.new(0, painelLargura, 0, painelAltura)
    frame.Position = UDim2.new(0.5, -painelLargura//2, 0.5, -painelAltura//2)
    frame.BackgroundColor3 = corUi
    frame.BackgroundTransparency = 0
    frame.Active = true
    frame.Selectable = true

    local uicorner = Instance.new("UICorner", frame)
    uicorner.CornerRadius = UDim.new(0.18, 0)
    dragify(frame)

    -- Título
    local titlebox = Instance.new("Frame", frame)
    titlebox.Size = UDim2.new(1, -34, 0, 44)
    titlebox.Position = UDim2.new(0, 17, 0, 13)
    titlebox.BackgroundColor3 = corTitulo
    titlebox.BackgroundTransparency = 0
    local tcorner = Instance.new("UICorner", titlebox)
    tcorner.CornerRadius = UDim.new(0.32,0)
    local titulo = Instance.new("TextLabel", titlebox)
    titulo.Text = [[<b><i>GROTA 🐊</i></b>]]
    titulo.RichText = true
    titulo.Size = UDim2.new(1,0,1,0)
    titulo.Font = Enum.Font.GothamBold
    titulo.TextSize = 27
    titulo.TextColor3 = Color3.fromRGB(240,255,245)
    titulo.BackgroundTransparency = 1
    titulo.TextYAlignment = Enum.TextYAlignment.Center
    titulo.TextXAlignment = Enum.TextXAlignment.Center

    for i,cmd in ipairs(comandos) do
        local yBase = 65 + (i-1)*63

        -- Nome comando
        local lbl = Instance.new("TextLabel", frame)
        lbl.Text = cmd
        lbl.Size = UDim2.new(0.8,0,0,16)
        lbl.Position = UDim2.new(0.09,0,0,yBase)
        lbl.BackgroundTransparency = 1
        lbl.Font = Enum.Font.Gotham
        lbl.TextSize = 15
        lbl.TextColor3 = corLabelCinza
        lbl.TextXAlignment = Enum.TextXAlignment.Left

        -- Delay box
        local delayBox = Instance.new("TextBox", frame)
        delayBox.Size = UDim2.new(0.29,0,0,19)
        delayBox.Position = UDim2.new(0.11,0,0,yBase+17)
        delayBox.Text = tostring(delays[cmd])
        delayBox.PlaceholderText = "⏱️ Delay"
        delayBox.Font = Enum.Font.Gotham
        delayBox.TextSize = 12
        delayBox.BackgroundColor3 = corBotao
        delayBox.TextColor3 = corTextoBotao
        delayBox.BorderSizePixel = 0
        local inputCorner1 = Instance.new("UICorner", delayBox)
        inputCorner1.CornerRadius = UDim.new(0.32,0)
        delayBox.FocusLost:Connect(function()
            delays[cmd] = tonumber(delayBox.Text) or 0.2
            if delays[cmd] < 0.1 then delays[cmd] = 0.1 end
            delayBox.Text = tostring(delays[cmd])
        end)

        -- Reps box
        local repsBox = Instance.new("TextBox", frame)
        repsBox.Size = UDim2.new(0.29,0,0,19)
        repsBox.Position = UDim2.new(0.46,0,0,yBase+17)
        repsBox.Text = tostring(reps[cmd])
        repsBox.PlaceholderText = "🔁 Repetições"
        repsBox.Font = Enum.Font.Gotham
        repsBox.TextSize = 12
        repsBox.BackgroundColor3 = corBotao
        repsBox.TextColor3 = corTextoBotao
        repsBox.BorderSizePixel = 0
        local inputCorner2 = Instance.new("UICorner", repsBox)
        inputCorner2.CornerRadius = UDim.new(0.32,0)
        repsBox.FocusLost:Connect(function()
            reps[cmd] = math.max(1, math.floor(tonumber(repsBox.Text) or 1))
            repsBox.Text = tostring(reps[cmd])
        end)

        -- INICIAR
        local startBtn = Instance.new("TextButton", frame)
        startBtn.Text = "🚀 Iniciar"
        startBtn.Size = UDim2.new(0.36,0,0,20)
        startBtn.Position = UDim2.new(0.09,0,0,yBase+36)
        startBtn.BackgroundColor3 = corBotao
        startBtn.TextColor3 = corTextoBotao
        startBtn.Font = Enum.Font.Gotham
        startBtn.TextSize = 13
        local startUICorner = Instance.new("UICorner", startBtn)
        startUICorner.CornerRadius = UDim.new(0.28,0)
        local startStroke = Instance.new("UIStroke", startBtn)
        startStroke.Color = Color3.fromRGB(200,200,200)
        startStroke.Thickness = 1.0
        startStroke.Transparency = 0
        startBtn.MouseEnter:Connect(function()
            startBtn.BackgroundColor3 = corBotaoHover
        end)
        startBtn.MouseLeave:Connect(function()
            startBtn.BackgroundColor3 = corBotao
        end)
        startBtn.MouseButton1Click:Connect(function()
            pararSpam(cmd)
            spammarComando(cmd)
        end)

        -- PARAR
        local stopBtn = Instance.new("TextButton", frame)
        stopBtn.Text = "🛑 Parar"
        stopBtn.Size = UDim2.new(0.36,0,0,20)
        stopBtn.Position = UDim2.new(0.52,0,0,yBase+36)
        stopBtn.BackgroundColor3 = corBotao
        stopBtn.TextColor3 = corTextoBotao
        stopBtn.Font = Enum.Font.Gotham
        stopBtn.TextSize = 13
        local stopUICorner = Instance.new("UICorner", stopBtn)
        stopUICorner.CornerRadius = UDim.new(0.28,0)
        local stopStroke = Instance.new("UIStroke", stopBtn)
        stopStroke.Color = Color3.fromRGB(200,200,200)
        stopStroke.Thickness = 1.0
        stopStroke.Transparency = 0
        stopBtn.MouseEnter:Connect(function()
            stopBtn.BackgroundColor3 = corBotaoHover
        end)
        stopBtn.MouseLeave:Connect(function()
            stopBtn.BackgroundColor3 = corBotao
        end)
        stopBtn.MouseButton1Click:Connect(function() pararSpam(cmd) end)
    end

    -- Botões extras num rodapé compacto
    local botaoAtivar = Instance.new("TextButton", frame)
    botaoAtivar.Text = "Ativar Botões"
    botaoAtivar.Size = UDim2.new(0.36,0,0,20)
    botaoAtivar.Position = UDim2.new(0.11,0,1,-35)
    botaoAtivar.BackgroundColor3 = corBotao
    botaoAtivar.TextColor3 = corTextoBotao
    botaoAtivar.Font = Enum.Font.Gotham
    botaoAtivar.TextSize = 12
    local cornerBa = Instance.new("UICorner", botaoAtivar)
    cornerBa.CornerRadius = UDim.new(0.3,0)
    local ativarStroke = Instance.new("UIStroke", botaoAtivar)
    ativarStroke.Color = Color3.fromRGB(200,200,200)
    ativarStroke.Thickness = 1.0
    ativarStroke.Transparency = 0
    botaoAtivar.MouseEnter:Connect(function()
        botaoAtivar.BackgroundColor3 = corBotaoHover
    end)
    botaoAtivar.MouseLeave:Connect(function()
        botaoAtivar.BackgroundColor3 = corBotao
    end)
    botaoAtivar.MouseButton1Click:Connect(showActionButtons)

    local botaoDesativar = Instance.new("TextButton", frame)
    botaoDesativar.Text = "Desativar Botões"
    botaoDesativar.Size = UDim2.new(0.36,0,0,20)
    botaoDesativar.Position = UDim2.new(0.52,0,1,-35)
    botaoDesativar.BackgroundColor3 = corBotao
    botaoDesativar.TextColor3 = corTextoBotao
    botaoDesativar.Font = Enum.Font.Gotham
    botaoDesativar.TextSize = 12
    local cornerBd = Instance.new("UICorner", botaoDesativar)
    cornerBd.CornerRadius = UDim.new(0.3,0)
    local desativarStroke = Instance.new("UIStroke", botaoDesativar)
    desativarStroke.Color = Color3.fromRGB(200,200,200)
    desativarStroke.Thickness = 1.0
    desativarStroke.Transparency = 0
    botaoDesativar.MouseEnter:Connect(function()
        botaoDesativar.BackgroundColor3 = corBotaoHover
    end)
    botaoDesativar.MouseLeave:Connect(function()
        botaoDesativar.BackgroundColor3 = corBotao
    end)
    botaoDesativar.MouseButton1Click:Connect(hideActionButtons)
end

local function createMenuToggleBtn()
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "MenuToggleBtn"
    screenGui.Parent = player:WaitForChild("PlayerGui")

    local btn = Instance.new("TextButton", screenGui)
    btn.Size = UDim2.new(0, 44, 0, 44)
    btn.AnchorPoint = Vector2.new(0.5, 0.5)
    btn.Position = UDim2.new(0.065, 0, 0.12, 0)
    btn.BackgroundColor3 = corTitulo
    btn.BackgroundTransparency = 0
    btn.Name = "ToggleMenuBtn"
    btn.Text = "🐊"
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 28
    btn.TextColor3 = Color3.fromRGB(245, 247, 250)
    local uicorner = Instance.new("UICorner", btn)
    uicorner.CornerRadius = UDim.new(1,0)
    local btnStroke = Instance.new("UIStroke", btn)
    btnStroke.Color = Color3.fromRGB(0,0,0)
    btnStroke.Thickness = 1.2
    btnStroke.Transparency = 0
    dragify(btn)
    btn.MouseButton1Click:Connect(function()
        if mainGui then
            mainGui.Enabled = not mainGui.Enabled
        else
            createMainGui()
            mainGui.Enabled = true
        end
    end)
end

createMainGui()
createMenuToggleBtn()
mainGui.Enabled = false
