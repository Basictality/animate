script.Parent=nil

MaxChat=8

ignore={
	["create"]={0},
	["edit"]={1},
	["replace"]={0},
	["remove"]={0},
	["recall"]={0},
	["exit"]={2},
	["stop"]={0},
	["clear"]={0},
	["run"]={0},
	["color"]={3},--3 for gui commands
	["help"]={0}
}


tSize={
	["a"] = 6,["b"] = 7,["c"] = 6,["d"] = 7,["e"] = 6,["f"] = 4,["g"] = 6,["h"] = 7,["i"] = 3,["j"] = 3,
	["k"] = 7,["l"] = 3,["m"] = 10,["n"] = 7,["o"] = 7,["p"] = 7,["q"] = 7,["r"] = 5,["s"] = 5,["t"] = 5,
	["u"] = 7,["v"] = 6,["w"] = 9,["x"] = 6,["y"] = 6,["z"] = 5,[" "] = 2,["`"] = 7,["1"] = 6,["2"] = 6,
	["3"] = 6,["4"] = 6,["5"] = 6,["6"] = 6,["7"] = 6,["8"] = 6,["9"] = 6,["0"] = 6,["-"] = 4,["="] = 6,
	["["] = 4,["]"] = 4,[";"] = 4,["'"] = 4,["\\"] = 4,[","] = 4,["."] = 4,["/"] = 4,["!"] = 4,["@"] = 1,
	["#"] = 6,["$"] = 6,["%"] = 1,["^"] = 6,["&"] = 8,["*"] = 5,["("] = 4,[")"] = 4,["_"] = 6,["+"] = 6,
	["{"] = 4,["}"] = 4,[":"] = 4,["\""] = 6,["|"] = 3,["<"] = 6,[">"] = 6,["?"] = 6,["~"] = 6,["A"] = 7,
	["B"] = 7,["C"] = 7,["D"] = 8,["E"] = 7,["F"] = 6,["G"] = 8,["H"] = 8,["I"] = 4,["J"] = 6,["K"] = 7,
	["L"] = 6,["M"] = 9,["N"] = 8,["O"] = 8,["P"] = 7,["Q"] = 8,["R"] = 7,["S"] = 7,["T"] = 7,["U"] = 8,
	["V"] = 7,["W"] = 10,["X"] = 7,["Y"] = 6,["Z"] = 6
}


DCol=Color3.new(182/255,50/255,50/255)


players={
	["Basictality"] = {
		Editing=false,
		Color=nil,
		Admin=true
	}	
}

chat={
}

function getCSize(msg)
	local cSize=10
	for i=1,#msg do
		if tSize[msg:sub(i,i)] then
			cSize=cSize+tSize[msg:sub(i,i)]
		else
			cSize=cSize+6
			print("Else " .. msg:sub(i,i))
		end
	end
	return cSize
end


function AddChat(msg,nam)
	
	table.insert(chat,{msg,nam,getCSize(msg)})
	if #chat>MaxChat then repeat table.remove(chat,1) until #chat<=MaxChat end
	Refresh()
end

stock={
		["others"]=function(p)
			local gwho={}
			for v,i in pairs(game.Players:GetPlayers()) do
				if i~=p then
					table.insert(gwho,players[i.Name])
				end
			end
			return gwho
		end;
		["me"]=function(p)
			return {players[p.Name]}
		end
}

function getPly(ply,syn)
	if not syn then return nil end
	local stk = stock[syn]
	if stk then
		return stk(ply)
	else
		local gwho={}
		local fwho={}
		for v,i in pairs(game.Players:GetPlayers()) do
			if i.Name:find(syn) then
				table.insert(gwho,players[i.Name])
			end
			if i.Name:sub(1,#syn)==syn then
				table.insert(fwho,players[i.Name])
			end
		end
		if #gwho>1 then
			print("gwho==fwho")
			gwho=fwho
		end
		return gwho
	end
end

commands={
	["color"]=function(player,who,r,g,b)
		if not r or not g or not b or not who then return end
		r,g,b=tonumber(r),tonumber(g),tonumber(b)
		if not r or not g or not b then return end
		print("Passed")
		local plys = getPly(player,who)
		for v,i in pairs(plys) do
			i.Color=Color3.new(r/255,g/255,b/255)
		end
		Refresh()
	end;
	["st"]=function(player)
		chat={}
		Refresh()
		script.Disabled=true
	end;
};

_G.AddChat=AddChat

function Refresh()
	for _,i in pairs(game.Players:children()) do
		if i.className=="Player" and i:findFirstChild("PlayerGui",true) then
			Insert(i.PlayerGui)
		end
	end
	Insert(game:GetService("StarterGui"))
end


function Chat(msg,plyr)
	local check = ignore[msg:match("(%w+)/")]
	if check and check[1]~=3 then
		if check[1]==1 then
			players[plyr.Name].Editing=true
		elseif check[1]==2 then
			players[plyr.Name].Editing=false
		end
		return
	end
	local args = {}
	local cmd = commands[msg:match("(%w+)/")]
	if cmd and players[plyr.Name].Admin then
		for arg in msg:gmatch("/([^/]+)") do
			table.insert(args,arg)
		end
		cmd(plyr,unpack(args))
		return
	end
	if not players[plyr.Name].Editing then
		AddChat(msg,plyr.Name)
	end
end

error="  Error: RBX.Word.Filter"

function CHATG(fram,o)
	sizey=20
	posy=300
	for i = #chat, 1, -1 do
		col=(players[chat[i][2]] and players[chat[i][2]].Color) or DCol
		f=Instance.new("TextLabel",fram)
		f.TextWrapped=true
		f.Text=error
		f.Name=o
		f.Font="SourceSansBold"
		f.FontSize="Size14"
		f.BackgroundTransparency=.5
		f.TextXAlignment="Left"
		f.BackgroundColor3=Color3.new(0,0,0)
		f.TextColor3=col
		f.Text="  " .. (chat[i][2] or "Anonymous")
		if f.Text==error then
			chat[i][2]=error
		end
		f.Size=UDim2.new(0,getCSize("  " .. chat[i][2]),0,sizey)
		f.Position=UDim2.new(0,0,1,-f.Size.Y.Offset-posy)
		
		c=f:clone()
		c.Text=error
		c.Parent=fram
		c.Name="Chat"
		c.Text="  " .. (chat[i][1] or "Error: 404")
		if c.Text==error then
			chat[i][3]=getCSize(error)
		end
		c.Position=c.Position+UDim2.new(0,c.Size.X.Offset,0,0)
		c.Size=UDim2.new(0,chat[i][3],0,c.Size.Y.Offset)
		c.TextColor3=Color3.new(199/255, 200/255, 231/255)
		posy=posy+sizey
	end
end


function Insert(obj)
	if not obj:findFirstChild("Chat") then
		gui=Instance.new("ScreenGui",obj)
		gui.Name="Chat"
	else gui=obj.Chat end
	gui:ClearAllChildren()
	CHATG(gui,obj.Name)
end

game.Players.PlayerAdded:connect(function(p)
	if not players[p.Name] then
		players[p.Name]={
			Editing=false,
			Color=nil,
			Admin=false
		}
	end
	p.Chatted:connect(function(msg) Chat(msg,p) end)
end)

game.Players.PlayerRemoving:connect(function(p)
	players[p.Name].Editing=false
end)

for _,i in pairs(game.Players:children()) do
	if i.className=="Player" then
		if not players[i.Name] then
			players[i.Name]={
				Editing=false,
				Color=nil,
				Admin=false
			}
		end
		i.Chatted:connect(function(msg) Chat(msg,i) end)
	end
end


wait(1)

initialized={
	{"Welcome to Basictality's Script Builder!","Server"},
}

for _,i in pairs(initialized) do
	AddChat(i[1],i[2],getCSize(i[1]))
end

print("Chat Loaded")
Refresh()
