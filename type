--[[
Tested in:
Luau (Roblox)
Lua 5.2
Lua 5.3
Lua 5.4


newproxy was added in Lua 5.1, and removed in Lua 5.2
We have a Simple Lua Version of it in hand here, which I had to recreate using the knowledge we had of newproxy from Lua 5.1 and Luau.
--]]

local proxy = {}
newproxy = newproxy or function(bool)
    if bool then
		setmetatable(proxy, {
			__index = {}
		})
	end
    return proxy
end

function type(a)
	local s, e = pcall(function()
		return a.Archivable and (string.match(tostring(a), "^(.-):") == nil)
	end)

	local _nil = ((a == nil) and "nil")													 -- Checks if 'a' is nil, returns "nil" if it's nil.
	local Instance = ((s and e ~= nil) and "Instance")									 -- Checks if a.Archivable and the check for if it's a: function, table or thread returned nil. It then checks if 'e' is not nil, 'e' is error or the message it returned, 'e' should return true, since it checks for Archivable and if it's a: function, table or thread. (Archivable is a boolean, if I used ClassName it would return "string" for an Instance.)
	local userdata = ((a == newproxy(true)) and "userdata")								 -- Checks if 'a' is similar to a new proxy.
	local coffee = (string.match(tostring(a), "^(.-):"))								 -- Checks if it's a: function, table or thread.
	local boolean = (((a == true) and "boolean" or (a == false) and "boolean"))			 -- Checks if a is directly true or false (I know that this is a bad check)
	local number = (((tonumber(a) ~= nil and tostring(a) ~= nil) and "number"))			 -- Checks if tonumber is possible on 'a' and tostring is possible too.
	local string = ((((not tostring(a) == _nil) and (not tonumber(a)))) and "string")	 -- Checks if not tostring 'a' is similar to nil, if it's not then it checks if tonumber is not possible on 'a'.
	local unknown = "Unknown"															 -- Returns "Unknown" if it's nil.

	return Instance or userdata or coffee or boolean or number or string or unknown
end

function Function() end 
local Table = {}
local Thread = coroutine and coroutine.create and coroutine.create(function() end)
local Userdata = newproxy and newproxy(true)
local Boolean = true
local Number = 1
local String = "Hello World!"
local NewInstance = Instance and Instance.new and Instance.new("Part")

print(type(Function)) -- Output: function

print(type(Table)) -- Output: table

print(type(Thread)) -- Output: thread

print(type(Userdata)) -- Output: userdata

print(type(Boolean)) -- Output: boolean

print(type(Number)) -- Output: number

print(type(String)) -- Output: string

print(type(NewInstance)) -- Output: Instance

