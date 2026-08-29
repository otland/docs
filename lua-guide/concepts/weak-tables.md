# Weak Tables

Lua's way of memory management is running something called a garbage collector. Every garbage collection cycle, all objects that have no references is freed back up to use to the program. Weak tables are a way to let the garbage collector know that it can go ahead and free up the memory if there are no references to that object anymore.

The weakness of a table is set by the `__mode` metamethod, if the string of `__mode` contains k, the keys are weak. If it contains v, the values are weak. If it contains both (kv), both the keys and values are considered weak.

Example:

```lua
local t = {}

setmetatable(t, {__mode = 'k'})

do
    -- closure
    local key = {} -- key is the reference to this table (object)
    t[key] = 123
end

collectgarbage() -- force a garbage collection cycle
-- variable 'key' is out of scope since it was created in a closure
-- after garbage collection, the object held by key is removed from 't'

for k, v in pairs(t) do
    print(k, v)
end

-- prints nothing

do
    key = {}
    t[key] = 123
end

collectgarbage()
-- key is still valid since it's a global variable

for k, v in pairs(t) do
    print(k, v)
end

-- prints table: 0x56144f2e36e0 123
```
