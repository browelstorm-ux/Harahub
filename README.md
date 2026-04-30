-- LocalScript dentro de StarterPlayerScripts

local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "CustomUI"

-- Botão principal (abrir/fechar)
local toggleButton = Instance.new("TextButton", gui)
toggleButton.Size = UDim2.new(0, 120, 0, 40)
toggleButton.Position = UDim2.new(0, 20, 0.5, -20)
toggleButton.Text = "Abrir UI"

-- Frame principal
local mainFrame = Instance.new("Frame", gui)
mainFrame.Size = UDim2.new(0, 500, 0, 300)
mainFrame.Position = UDim2.new(0.5, -250, 0.5, -150)
mainFrame.Visible = false
mainFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)

-- Botão minimizar
local minimize = Instance.new("TextButton", mainFrame)
minimize.Size = UDim2.new(0, 30, 0, 30)
minimize.Position = UDim2.new(1, -35, 0, 5)
minimize.Text = "-"

-- Lado direito (menu)
local menuFrame = Instance.new("Frame", mainFrame)
menuFrame.Size = UDim2.new(0, 150, 1, 0)
menuFrame.Position = UDim2.new(1, -150, 0, 0)
menuFrame.BackgroundColor3 = Color3.fromRGB(40,40,40)

-- Lado esquerdo (conteúdo)
local contentFrame = Instance.new("Frame", mainFrame)
contentFrame.Size = UDim2.new(1, -150, 1, 0)
contentFrame.BackgroundColor3 = Color3.fromRGB(50,50,50)

-- Função de criar botão de menu
local function createMenuButton(name, order)
	local btn = Instance.new("TextButton", menuFrame)
	btn.Size = UDim2.new(1, -10, 0, 30)
	btn.Position = UDim2.new(0, 5, 0, (order-1)*35 + 5)
	btn.Text = name
	
	btn.MouseButton1Click:Connect(function()
		contentFrame:ClearAllChildren()
		
		local label = Instance.new("TextLabel", contentFrame)
		label.Size = UDim2.new(1, 0, 0, 40)
		label.Text = "Opções de "..name
		
		-- exemplo de toggle
		local toggle = Instance.new("TextButton", contentFrame)
		toggle.Size = UDim2.new(0, 150, 0, 40)
		toggle.Position = UDim2.new(0, 10, 0, 50)
		toggle.Text = "OFF"
		toggle.BackgroundColor3 = Color3.fromRGB(120,0,0)
		
		local ativo = false
		
		toggle.MouseButton1Click:Connect(function()
			ativo = not ativo
			if ativo then
				toggle.Text = "ON"
				toggle.BackgroundColor3 = Color3.fromRGB(0,120,0)
			else
				toggle.Text = "OFF"
				toggle.BackgroundColor3 = Color3.fromRGB(120,0,0)
			end
		end)
	end)
end

-- Criando categorias (exemplo genérico)
local categorias = {"Visual", "Movimento", "Jogador", "Extras"}
for i, nome in ipairs(categorias) do
	createMenuButton(nome, i)
end

-- Abrir/fechar UI
toggleButton.MouseButton1Click:Connect(function()
	mainFrame.Visible = not mainFrame.Visible
end)

-- Minimizar
minimize.MouseButton1Click:Connect(function()
	mainFrame.Visible = false
end)
