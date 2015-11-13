plr = game.Players.LocalPlayer
char = plr.Character
local larm = char["Left Arm"]
local rarm = char["Right Arm"]
local lleg = char["Left Leg"]
local rleg = char["Right Leg"]
local hed = char.Head
local torso = char.Torso
local root = char.HumanoidRootPart
----------------------------------------------------
larm.Size = larm.Size * 2
rarm.Size = rarm.Size * 2
lleg.Size = lleg.Size * 2
rleg.Size = rleg.Size * 2
torso.Size = torso.Size * 2
hed.Size = hed.Size * 2
root.Size = root.Size * 2
----------------------------------------------------
newWeld = function(wp0, wp1, wc0x, wc0y, wc0z)
local wld = Instance.new("Weld", wp1)
wld.Part0 = wp0
wld.Part1 = wp1
wld.C0 = CFrame.new(wc0x, wc0y, wc0z)
end
----------------------------------------------------
newWeld(torso, larm, 1.5, 0.5, 0)
larm.Weld.C1 = CFrame.new(4.3, 0.5, 0)
newWeld(torso, rarm, 1.5, 0.5, 0)
rarm.Weld.C1 = CFrame.new(-1.3, 0.5, 0)
newWeld(torso, hed, 0, 3, 0)
newWeld(torso, lleg, -0.5, -1, 0)
lleg.Weld.C1 = CFrame.new(0.5, 3, 0)--
newWeld(torso, rleg, 0.5, -1, 0)
rleg.Weld.C1 = CFrame.new(-0.5, 3, 0)
newWeld(root, torso, 0, -1, 0)
torso.Weld.C1 = CFrame.new(0, -1, 0)

if not game.Players.LocalPlayer.Character then repeat wait() until game.Players.LocalPlayer.Character end
if not game.Players.LocalPlayer.Character.Torso then repeat wait() until game.Players.LocalPlayer.Character.Torso end

wait()
--constants
local plr = game.Players.LocalPlayer
local mouse = game.Players.LocalPlayer:GetMouse()
local char = plr.Character
local torso = char["Torso"]
local rarm = char["Right Arm"]
local larm = char["Left Arm"]
local head = char["Head"]
--welds
local rweld = Instance.new("Weld",torso) --right arm
rweld.Part0 = torso
rweld.Part1 = rarm
local lweld = Instance.new("Weld",torso) --left arm
lweld.Part0 = torso
lweld.Part1 = larm
local hweld = Instance.new("Weld",torso) --head
hweld.Part0 = torso
hweld.Part1 = head
local tweld = Instance.new("Weld",torso) --torso
tweld.Part0 = char.HumanoidRootPart
tweld.Part1 = torso

rweld.C0 = CFrame.new(1.5,.5,0)
rweld.C1 = CFrame.new(0,.5,0)
lweld.C0 = CFrame.new(-1.5,.5,0)
lweld.C1 = CFrame.new(0,.5,0)
hweld.C0 = CFrame.new(0,0,0)
hweld.C1 = CFrame.new(0,-1.5,0)
if not game.Players.LocalPlayer.Character then repeat wait() until game.Players.LocalPlayer.Character end
if not game.Players.LocalPlayer.Character.Torso then repeat wait() until game.Players.LocalPlayer.Character.Torso end

wait()
--constants
local plr = game.Players.LocalPlayer
local mouse = game.Players.LocalPlayer:GetMouse()
local char = plr.Character
local torso = char["Torso"]
local rarm = char["Right Arm"]
local larm = char["Left Arm"]
local head = char["Head"]
--welds
local rweld = Instance.new("Weld",torso) --right arm
rweld.Part0 = torso
rweld.Part1 = rarm
local lweld = Instance.new("Weld",torso) --left arm
lweld.Part0 = torso
lweld.Part1 = larm
local hweld = Instance.new("Weld",torso) --head
hweld.Part0 = torso
hweld.Part1 = head
local tweld = Instance.new("Weld",torso) --torso
tweld.Part0 = char.HumanoidRootPart
tweld.Part1 = torso

rweld.C0 = CFrame.new(1.5,.5,0)
rweld.C1 = CFrame.new(0,.5,0)
lweld.C0 = CFrame.new(-1.5,.5,0)
lweld.C1 = CFrame.new(0,.5,0)
hweld.C0 = CFrame.new(0,0,0)
hweld.C1 = CFrame.new(0,-1.5,0)

function Lerp(c1,c2,al) --lerp makes it look nice and smooth
        local com1 = {c1.X,c1.Y,c1.Z,c1:toEulerAnglesXYZ()}
        local com2 = {c2.X,c2.Y,c2.Z,c2:toEulerAnglesXYZ()}
        for i,v in pairs(com1) do 
                com1[i] = v+(com2[i]-v)*al
        end
        return CFrame.new(com1[1],com1[2],com1[3]) * CFrame.Angles(select(4,unpack(com1)))
end

local anim = "N/A"

--running anim
local pose1 = {
        [rweld] = CFrame.new(3,0.5,0)*CFrame.Angles(math.rad(-45),math.rad(0),math.rad(10)),
        [lweld] = CFrame.new(-3,0.5,0)*CFrame.Angles(math.rad(-45),math.rad(0),math.rad(-10)),
        [hweld] = CFrame.new(0,1.5,0)*CFrame.Angles(math.rad(-5),math.rad(0),math.rad(0)),
        [tweld] = CFrame.new(0,0,0)*CFrame.Angles(math.rad(-7.5),math.rad(0),math.rad(0)),
} 

--idle anim
mainpose = "0.6"
local pose0 = {
        [rweld] = CFrame.new(3,mainpose,0)*CFrame.Angles(math.rad(0),math.rad(0),math.rad(5)),
        [lweld] = CFrame.new(-3,mainpose,0)*CFrame.Angles(math.rad(0),math.rad(0),math.rad(-5)),
        [hweld] = CFrame.new(0,1.5,0)*CFrame.Angles(math.rad(0),math.rad(0),math.rad(0)),
        [tweld] = CFrame.new(0,0,0)*CFrame.Angles(math.rad(0),math.rad(0),math.rad(0))
}

--jump anim
local pose01 = {
        [rweld] = CFrame.new(3,0.65,0)*CFrame.Angles(math.rad(0),math.rad(0),math.rad(30)),
        [lweld] = CFrame.new(-3,0.65,0)*CFrame.Angles(math.rad(0),math.rad(0),math.rad(-30)),
        [hweld] = CFrame.new(0,1.5,0.1)*CFrame.Angles(math.rad(-10),math.rad(0),math.rad(0)),
        [tweld] = CFrame.new(0,0,0)*CFrame.Angles(math.rad(0),math.rad(0),math.rad(0)),
} 


char.Humanoid.Running:connect(function(s)
        if s > 0 then
                anim = "anim1" --running anim
        else
                anim = "anim0" --idle anim
        end
end)

char.Humanoid.FreeFalling:connect(function()
        anim = "anim01" --falling anim
end)

game:GetService("RunService").RenderStepped:connect(function()
        if anim == "anim01" then
                rweld.C0 = Lerp(rweld.C0, pose01[rweld], 0.1)
                lweld.C0 = Lerp(lweld.C0, pose01[lweld], 0.1)
                hweld.C0 = Lerp(hweld.C0, pose01[hweld], 0.1)
                tweld.C0 = Lerp(tweld.C0, pose01[tweld], 0.1)
        elseif anim == "anim0" then
                rweld.C0 = Lerp(rweld.C0, pose0[rweld], 0.1)
                lweld.C0 = Lerp(lweld.C0, pose0[lweld], 0.1)
                hweld.C0 = Lerp(hweld.C0, pose0[hweld], 0.1)
                tweld.C0 = Lerp(tweld.C0, pose0[tweld], 0.1)
        elseif anim == "anim1" then
                rweld.C0 = Lerp(rweld.C0, pose1[rweld], 0.1)
                lweld.C0 = Lerp(lweld.C0, pose1[lweld], 0.1)
                hweld.C0 = Lerp(hweld.C0, pose1[hweld], 0.1)
                tweld.C0 = Lerp(tweld.C0, pose1[tweld], 0.1)
        end
end)
--------------------------------------------------------------
------------------------Hats----------------------------------
for i,v in pairs(char:children()) do if v.ClassName=="Hat" then
	v.Parent = nil
end
end

game:GetService('InsertService'):LoadAsset(22160652):children()[1].Parent = char--blind rouge]]
game:GetService('InsertService'):LoadAsset(20642008):children()[1].Parent = char--bandit
game:GetService('InsertService'):LoadAsset(102623484):children()[1].Parent = char--golden mostrosity
wait()
rog = char:FindFirstChild('Rogue')
rog.Handle.Mesh.Scale = Vector3.new(2,2,2)

band = char:FindFirstChild('Bandana')
band.Handle.Mesh.Scale = Vector3.new(2,2,2)
band.AttachmentPos = Vector3.new(0, 1.3, 0)

gm = char:FindFirstChild('GoldenSatyrHawk')
gm.Handle.Mesh.Scale = Vector3.new(2,2,2)
gm.AttachmentPos = Vector3.new(0, -1, -0.5)
---------------------------------------------------

plyr = plr
mouse = plyr:GetMouse()


NewRS = nil
boost = nil
gyro = nil
isfloating = false
charging = false
maxfuel = 10000000
fuel = maxfuel
charge_int = .5
maxTrq = Vector3.new(7000, .01, 7000)
origPow = Instance.new("BodyGyro").P
speed = 0
maxspd = 1000

function startfloat()

	if gyro then
		gyro:Destroy()
	end
	
	char = plyr.Character
	ra = char:FindFirstChild("Right Arm")
	la = char:FindFirstChild("Left Arm")
	torso = char.Torso
	char.Humanoid.PlatformStand = true
	

	
	boost = Instance.new("BodyVelocity", torso)
	boost.velocity = Vector3.new(0, 20, 0)
	boost.maxForce = Vector3.new(5500, 70000--[[6000]], 5500)
	
	gyro = Instance.new("BodyGyro", torso)
	gyro.cframe = torso.CFrame * CFrame.Angles(math.rad(-3), 0, 0)
	gyro.maxTorque = maxTrq
	
	isfloating = true
	--ns = torso.Neck
end

function floatforward()
	while gyro.Parent ~= nil and boost.Parent ~= nil do
		gyro.cframe = gyro.cframe 
	end
end

function float()
	speed = 0
	repeat
		if keylist['w'] then
		    gyro.maxTorque = maxTrq
		    gyro.P = origPow
			
			gyro.cframe = CFrame.new(torso.Position, mouse.Hit.p) * CFrame.Angles(math.rad(-90), 0, 0)
			
			if speed < maxspd then speed = speed + 1 end
			boost.velocity = CFrame.new(torso.Position, mouse.Hit.p).lookVector * speed

		else
		    if speed > 0 then speed = speed - 3 end
		    
            gyro.maxTorque = Vector3.new(maxTrq.x, 0, 0)
            gyro.P = origPow
            
			gyro.cframe = CFrame.new(torso.Position) * CFrame.Angles(math.rad(-3), 0, 0)
			boost.velocity = Vector3.new(0, 2, 0)
		end
		wait()
		fuel = fuel - .5
	until fuel <= -1 or not keylist["g"]
end

function stopfloat()
	
	--torso.Neck.C0 = CFrame.new(0, 1, 0, -1, -0, -0, 0, 0, 1, 0, 1, 0)
	
	char.Humanoid.PlatformStand = false
	
	if boost then
		boost:Destroy()
	end
	if gyro then
		gyro:Destroy()
	end
	
	isfloating = false
end


function Recharge()
	coroutine.resume(coroutine.create(function()
		charging = true
		char = plyr.Character
		lab:TweenSizeAndPosition(UDim2.new(1, 0, 1, 0), UDim2.new(0, 0, 0, 0), "Out", "Linear", .7, true)
		local con = char.Humanoid.Running:connect(function(spd)
			if spd > 0 then
				lab:TweenSizeAndPosition(UDim2.new(0, 0, 0, 0), UDim2.new(.5, 0, .5, 0), "Out", "Linear", .7, true)
			end
			wait()
			if spd <= 0 then
				lab:TweenSizeAndPosition(UDim2.new(1, 0, 1, 0), UDim2.new(0, 0, 0, 0), "Out", "Linear", .7, true)
			end
		end)
		repeat
			fuel = fuel + charge_int
			lab.Text = math.floor(100*(fuel/maxfuel)).."%"
			wait()
		until fuel >= maxfuel or isfloating
		lab:TweenSizeAndPosition(UDim2.new(0, 0, 0, 0), UDim2.new(.5, 0, .5, 0), "Out", "Linear", .7, true)
		con:disconnect()
		charging = false
	end))
end

function RunThru()
    --plyr.Character.Humanoid.Jump = true
	pcall(function() startfloat() end)
	
	float()
	
	stopfloat()

	if not charging then Recharge() end
end


keylist = {}
mouse.KeyDown:connect(function(key)
	keylist[key] = true
	
	if key == "g" then
		RunThru()
	elseif key == "w" then
	end
		
end)

mouse.KeyUp:connect(function(key)
	keylist[key] = nil
end)


debounce = false
plyr.Character.Head.Touched:connect(function(hit)
    if hit.Parent:FindFirstChild("Humanoid") and speed >= maxspd and not debounce then
        debounce = true
        guy = hit.Parent
        guy.Humanoid.PlatformStand = true
        local bf = Instance.new("BodyForce", guy.Torso)
        bf.force = CFrame.new(plyr.Character.Head.Position, hit.Parent.Torso.Position).lookVector * 500
        wait(.5)
        bf:Destroy()
        guy.Humanoid.PlatformStand = false
        wait(.5)
        debounce = false
    end
end)
