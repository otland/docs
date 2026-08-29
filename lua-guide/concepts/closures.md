# Closures

A closure is when you enclose a function inside of another, like so:

```lua
function a(var)
    local x = 5
    local function b()
       print(x, var) 
    end
    return b
 end
```

When you create a closure, all of the variables are accessible in its parent's scope. In this case, b has access to a's scope. This provides a way to access and manipulate variables inside a function after its parent returns. The variables that the closure can access are called upvalues. The variables `x` and `var` are both upvalues to function `b` in this case.

Take this example, a simple function to increment a value, which is inaccessible without the closure:

```lua
function counter()
    local i = 0
    return function()
        i = i + 1
        return i
    end
end
```

Here we define a function that returns an anonymous function (a function that has no name or identifier) which will increment the upvalue `i` and return the value back to us.

Each time we call `counter`, it generates a new counter for us, it can be called any amount of times and all the counters will have different values. Each time the returned function from counter is called (the function that increments), it will only change that counter, no others.

```lua
function counter()
    local i = 0
    return function()
        i = i + 1
        return i
    end
end

local counter_1 = counter() -- now counter_1 holds a unique function to increment the upvalue
local counter_2 = counter() -- counter_2 holds a new unique incrementer
counter_1() -- increment our first counter, i is now 1
counter_2() counter_2() counter_2() -- increment counter_2 3 times, i is 3, counter_1 is unaffected

print(counter_1(), counter_2()) -- Output: 2 4
```

For the print, the counters must be incremented again so we can get the value, since each time our incrementers run they return the variable after incrementing it.
