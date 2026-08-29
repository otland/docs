# Scopes

Scopes are what define the range of functionality to a variable or function. This specifically applies in Lua to `local` variables & functions. When you define a variable or function with `local`, its scope is defined by the innermost block of code you define it in.

Example of various scopes:

```lua
local x = 15 -- scope is script-wide, x can be accessed anywhere inside of this script

function a()
    local first = true -- first can only be accessed throughout a()'s code block
    if first then
        local second = 123 -- can only be accessed within this if statement
        print(second) -- Output: 123
    end
    print(second) -- nil, cannot access that variable anymore
    print(first) -- Ouput: true | we can access this variable since we're still inside of the function's code block
end
```

Another example showing a function's scope:

```lua
local function outputTable(t)
    local function output(t)
        for k, v in pairs(t) do
            print(k, v)
        end
    end
    output(t) -- output function is only accessible inside of outputTable
end

outputTable({1, 2, 3}) -- works, outputTable's scope is script-wide
output({1, 2, 3}) -- will return an error, output is inaccessible since it's not inside the current scope, it is inside of outputTable. 
```
