# Recursion

Recursion is a technique used to use an algorithm or function that calls itself repetitively until a certain condition is satisfied.

The go-to example for recursion is a factorial function:

```lua
function fact(n)
    if n == 0 then
        return 1
    end
    return n * fact(n - 1)
end
```

Here it will calculate the factorial by returning each value multiplied by the result of `fact(n - 1)`. It can be a bit confusing, since we know return breaks out and gives back a value to whatever called the function, but before a return can give back a value, it needs to be evaluated first. And until `n` reaches 0, it will keep trying to evaluate `n * fact(n - 1)` . Once `n` does reach 0, it returns the next multiplier (1) and then the first call to `fact` will be able to return the evaluated result. All of these is quite literally a chain of returns.

Here's a diagram of what's really happening:

```lua
fact(3)
--[[
fact(3)
|
-> return (3 * fact(2))
| [6] (3 * 2)  |
|        |     -> return (2 * fact(1))
|        <------- [2] (2 * 1) |
|                         |   -> return (1 * fact(0))
|                         |                  |
|                         |                  -> return 1
|                         <---------- [1]   (1 * 1)
-> fact(3) = 6, (3 * 2) end result                                  
]]
```

Here you can see the chain of returns, and how each `fact` call looks. Each time there's an attempt to return, it must evaluate what the value of `fact(n - 1)` is before giving back a value. Which is why the second it tries to return `3 * fact(2)`, it evaluates `fact(2)`, but `fact(2)` will have to evaluate `fact(1)`, and `fact(1)` will have to evaluate `fact(0)`. The second that chain breaks by returning 1, it goes back up each return and will "insert" the result of that `fact` call and multiply it. I tried to show this as best I could, the return statements evaluated in parentheses, the result in square brackets \[X] and a display to show the chain of where it's inserted/used as the multiplier in the above return.

Another example of recursion would be a Fibonacci sequence:

```lua
function fib(n)
    if n < 3 then
        return 1
    end
    return fib(n-1) + fib(n-2)
end
```

Here, it will calculate n-1 + n-2 until both `n`s reach a value which is less than 3. Each of these `fib` calls chain out like `fact` did, each call must be evaluated before it can be returned for usage.

```lua
fib(5)
--[[
fib(5) | Result: 5
  |              ^
  |              |
  |              ----------------------|
  --> return fib(4) + fib(3)  | (3+2) [5]
                | ^     ^  |
                | |     |  --->  return fib(2) + fib(1)    | (1+1) [2]
                | |     --------------------------------------------|
                | |
                | -------------------------------------|
                ---> return fib(3) + fib(2)   | (2+1) [3]
                             ^  |      ^ |                                  
                             |  |      | -> return 1   [1]
                             |  |      -----------------|
                             |  |
                             |  -> return fib(2) + fib(1)    | (1+1)  [2]
                             |              ^ |      ^ |               |
                             |              | |      | -> return 1 [1] |
                             |              | |      ---------------|  |
                             |              | -> return 1 [1]          |
                             |              ---------------|           |
                             ------------------------------------------|
  ]] 
```

Again, the evaluation is in parentheses, the result is in square brackets and moves back up the chain. Reading this diagram, you go bottom-right, then follow the square brackets back up the chain, up-left.
