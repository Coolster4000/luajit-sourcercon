# RCON implementation in Lua by github.com/xiaooloong

This library was written by github.com/xiaooloong to query/rcon source servers in nginx/openresty. I've made a small change to instead rely on luasocket and luajit. These changes are so small, the only reason I even forked this was to easily clone on another machine. I didn't implement any changes for the sourcequery aspect of this library because I don't use it since I don't have dependencies. If you need it, you should be able to figure it out. Ignore the lualib folder, that's a holdover from the openresty library and I don't know enough about git to remove it. Just place the `sourcequery` folder with your script.

Usage:

foo.lua
```lua
local rcon = require 'sourcequery.rcon'
local r = rcon:new()
--[[
    rcon:connect(
        password,   -- rcon_password
        ip,         -- ip address
        port,       -- tcp port, default value is 27015
        timeout     -- timeout, default value is 1000(ms)
    )
]]--
local ok, err = r:connect('qT8VzUwm8', '127.0.0.1', 27016)
--[[
    local ok, err = r:connect('pass', '127.0.0.1')
    local ok, err = r:connect('pass', '127.0.0.1', 27016, 3000)
]]--
if not ok then
    return print(err)
end

ok, err = r:exec('status')
r:close()
print(ok, err)
```
to run: `luajit foo.lua`
