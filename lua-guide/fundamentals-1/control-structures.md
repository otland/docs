# Control Structures

Control Structures define which way a program flows. Lua provides a simple set of generic control structures seen in most languages today:

* if, then, else, elseif
* while
* repeat
* for
* break
* return

Each of these control structures determines the way your code flows in your program. Each one besides `return`, `break`, and `repeat` are terminated by the `end` keyword.

### if, then, else, elseif

An if statement tests the condition given and determines whether or not to move forward, if the condition is truthy it executes the code given in the first `if` block. Otherwise, if there is an `elseif` statement, that condition is also tested and has the exact same behavior as an `if` statement. If none of those conditions evaluate to true, the `else` block is executed. Each `if` statement should be accompanied by an `end` to terminate the control structure, you should not place them for any `else` or `elseif`s you may place. Each statement may only contain one `if`, any number of `elseif`s, one `else`, and finally one `end`.

A general if statement:

```lua
if condition then
    print('1st condition was true')
end
```

If our condition was truthy (any value that isn't `false` or `nil`), the print will be executed. Otherwise, nothing will happen.

An example using all keywords:

```lua
local x = 50
local y = 10
if (x - y) < 10 then
    print('1st condition was true')
elseif (x - y) < 20 then
    print('2nd condition was true')
else
    print('none of the conditions were true')
end
```

In this example, all conditions evaluate to false because `x - y` is 40, which is not less than 10 nor 20, resulting in the last print being executed, since the `else` keyword is a fallback in the case that no other conditions are truthy.

### while

A while loop will continuously execute its body as long as the condition provided is truthy. The condition is evaluated each time before executing the body again.

Structure of a while loop:

```lua
while condition do
    -- body
end
```

More information & examples are covered in the [Loops](loops.md) page.

### repeat

A repeat loop will also continuously execute its body as long as the condition provided is truthy. The difference here is that the condition is evaluated after the body runs, not before. So any repeat loop will always execute at least once.

Structure of a repeat loop:

```lua
repeat
    -- body
until condition
```

More information & examples are covered in the [Loops](loops.md) page.

### for

There are two different kinds of for loops, a numeric for, or a generic for. These also execute their bodies until the loop is terminated.

A numeric for is ran for a specific amount of times, the loop variable starts at the number provided for `start`, and stops at the number provided for `stop`. The loop variable gets incremented by the `step`each iteration, the default being 1.

```lua
for var = start,stop,step do
    -- body
end
```

A generic for loop traverses all values returned by an iterator (a function which provides a way to traverse a container, or a specific set of values)

```lua
for <loop vars> in iterator(<args>) do
    -- body
end
```

More information & examples are covered in the [Loops](loops.md) page.

### break

A break will instantly halt execution and break any loop, and will not be able to return back to the loop.

More information & examples are covered in the [Loops](loops.md) page.

### return

A return gives back any number of values from a function, it works like a break in the sense that it halts execution of the function and can't continue onward at any point.

```lua
function abc()
    return 1, 2, 3
end

local a, b, c = abc() -- a = 1, b = 2, c = 3
```

In this single return, 3 values are returned and can be unpacked into variables, or a table if you have no idea how many values will be returned, like this:

```lua
function abc(arg)
    if arg then
        return 1, 2, 3
    end
    return 1, 2, 3, 4, 5
end

local args = {abc(true)} -- {1, 2, 3}
args = {abc(false)} -- {1, 2, 3, 4, 5}
```

Here, the default return value is `1, 2, 3, 4, 5`, if the condition to the `if` statement is false, the default is used. However, if `arg` evaluates to true in the `if` statement, `1, 2, 3` will be returned and not `1, 2, 3, 4, 5`, since return breaks out of the function, the rest of the code will not be executed.

Since Lua automatically assigns indexes like previously discussed, unpacking it like this creates an array the same way you do it manually, which lets you use a different way to get all returned values of a function if you don't specifically know how many or what values it's returning.

If you still use variables to unpack the return values into, they are unpacked in order, so even if you have 3 variables and 5 return values, it will use the first 3 return values to assign those variables in sequence:

```lua
function abc(arg)
    if arg then
        return 1, 2, 3
    end
    return 1, 2, 3, 4, 5
end

local x, y, z = abc(false) -- returns 1, 2, 3, 4, 5 | x,y,z are 1,2,3 respectively
```
