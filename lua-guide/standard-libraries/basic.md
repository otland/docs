# Basic

### \_G

Description: Global variable that holds the global environment (all global functions/variables)

Example:

```lua
print(_G.tostring(true)) -- tostring is global, which makes it accessible via _G as well
```

### setfenv

Description: sets the environment for a function to use, rather than \_G.

Usage: setfenv(f)

Example:

```lua
function x()
    zzz.x = 5
    print() -- will not work here, the environment is not _G.
end

setfenv(x, {zzz = {x = 10}})
```

### getfenv

Description: returns the environment in use by given function or stack level, default 1.

Usage: getfenv(\[f])

Example:

```lua
function x()
    zzz.x = 5
    print() -- will not work here, the environment is not _G.
end

setfenv(x, {zzz = {x = 10}})
print(getfenv(x)) -- environment is {zzz = {x = 10}}
```

### setmetatable

Description: sets the metatable for given table

Usage: setmetatable(table, metatable)

Example:

```lua
local t = {}
setmetatable(t, {__call = print})
```

### getmetatable

Description: gets the metatable of specified table, returning the `__metatable` metamethod's value if applicable

Usage: getmetatable(table)

Example:

```lua
local t = {}
setmetatable(t, {__call = print})
print(getmetatable(t)) -- {__call = print}
setmetatable(t, {__metatable = {x = 5}})
print(getmetatable(t)) -- {x = 5}
```

### rawset

Description: sets a value in the table at specified index without invoking any metamethods

Usage: rawset(table, index, value)

Example:

```lua
local t = {}
setmetatable(t, {__newindex = function(self, k, v)
    print('Value set at index '.. tostring(k) ..' to value '.. tostring(v))
end})

t.x = 5 -- Value set at index x to value 5
rawset(t, 'xx', 50) -- prints nothing, __newindex is not be invoked
```

### rawget

Description: returns a value from a table at given index without invoking any metamethods

Usage: rawget(table, index)

Example:

```lua
local t = {}
setmetatable(t, {__index = function(self, k, v)
    print('Accessing value at index '.. tostring(k))
end})

print(t.x) -- Accessing value at index x
print(rawget(t, 'x')) -- nothing, __index is not invoked
```

### rawequal

Description: compares two values using == without invoking any metamethod

Usage: rawequal(v1, v2)

Example:

```lua
local mt = {__eq = function(a, b)
    print('Checking equality ( '.. tostring(a) ..' vs '.. tostring(b) ..' )')
    return rawequal(a, b)
end}

local t = {}
setmetatable(t, mt)

local t2 = {}
setmetatable(t2, mt)

print(t == t2) -- Checking equality ( table: 00f28b00 vs table: 00f28a10 )
print(rawequal(t, t2)) -- nothing, __eq is not invoked
```

### pairs

Description: iterator to traverse over a table in any order possible

Usage: pairs(t)

Example:

```lua
local t = {1, 2, 3}
for k, v in pairs(t) do
    print(k, v)
end
```

### ipairs

Description: iterator to traverse over a table in sequence

Usage: ipairs(t)

Example:

```lua
local t = {1, 2, 3}
for k, v in ipairs(t) do
    print(k, v)
end
```

### loadstring

Description: loads a Lua chunk

Usage: loadstring(string \[, chunkName])

Example:

```lua
local f = loadstring([[return function() print(123) end]])
f() -- 123
```

### loadfile

Description: loads a Lua chunk from specified file, or from standard input if filename is not specified

Usage: loadfile(\[filename])

Example:

```lua
-- x.lua
return function() print(123) end

-- other file.lua
local f = loadfile("x.lua")
f() -- 123
```

### next

Description: returns the next key, value pair in `table` starting from specified index, otherwise `index`, is nil

Usage: next(table \[, index])

Example:

```lua
local t = {1, 2, 3}
print(next(t, 2)) -- 3, 3
print(next(t)) -- 1, 1
```

### pcall

Description: calls a function in a protected state, returning any errors if they happen, otherwise returns true if successful plus the returned values from `f`

Usage: pcall(f, ...)

Example:

```lua
function x(n)
    return x + n
end

local success, ret = pcall(x, 5)
print(success, ret) -- false    C:\Users\user\lua_file.lua:2: attempt to perform arithmetic on a function value (global 'x')
```

### xpcall

Description: calls a function in a protected state, using `err` as the error handler and returning true if no errors happen, otherwise returns false plus the result from `err`

Usage: xpcall(f, err)

Example:

```lua
function x(n)
    return x + n
end

local function x_error_handler(error)
	print(error)
	return 123
end

local success, ret = xpcall(x, x_error_handler)
print(success, ret)
```

Output:

```
C:\Users\user\lua_file.lua:2: attempt to perform arithmetic on a function value (global 'x')
false 123
```

### unpack

Description: unpacks a table in sequence, starting from i and ending with j (1, #table respectively by default), returning all values from it

Usage: unpack(table \[, i \[, j]])

Example:

```lua
local t = {1, 2, 3, 4, 5}
print(unpack(t)) -- 1, 2, 3, 4, 5
print(unpack(t, 2, 4)) -- 2, 3, 4
```

### type

Description: returns the data type of given value

Usage: type(value)

Example:

```lua
print(type(123)) -- number
print(type({})) -- table
print(type(nil)) -- nil
print(type('')) -- string
print(type(true)) -- boolean
```

### tonumber

Description: converts value to a number if possible

Usage: tonumber(val \[,base])

Example:

```lua
local x = '5'
print(tonumber(x)) -- 5
print(type(tonumber(x))) -- number
print(type(x)) -- string
```

### tostring

Description: converts value to a string

Usage: tostring(val)

Example:

```lua
print(tostring({})) -- table: 00ee88a8
print(tostring(5)) -- 5

print('This is a boolean: '.. tostring(true)) -- This is a boolean: true
```
