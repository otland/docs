# Loops

Loops are one of the most powerful concepts in any language. They provide a way to repeat a certain process for any number of times or based off of any condition. This lets programmers simplify and condense code that could otherwise result in thousands of lines of code.

### for loops

The simplest loop is a numerical loop, described in the previous section. Here is an example of how to use one:

```lua
for i = 1, 10 do
    print(i)
end
```

Here we're able to print numbers 1 through 10 by defining the start and stop as 1, and 10 respectively. The step (increments the loop variable) is defaulted to 1, which lets us move from 1 to 10 one step at a time (hence the name `step`).

Here's what it would look like with an explicitly defined step variable:

```lua
for i = 1, 10, 2 do
    print(i)
end
```

Here's the output:

```
1
3
5
7
9
```

Since the step variable is defined as 2, each iteration it increments our loop variable `i` by 2. Since it begins with 1, it hops to 3, 5, 7, and 9. The stopping point is 10, and since after the loop variable is incremented from 9 to 11, the loop is terminated since the loop variable is greater than or equal to its stop variable.

Now, generic for loops provide a way to iterate through a set of data. Here's an example:

```lua
local t = {1, 2, 3}
for key, value in ipairs(t) do
    t[key] = value * 5
end
```

This particular chunk of code will traverse through the table and multiply each value by 5, resulting in the table looking like `{5, 10, 15}` once the loop is finished. The iterator here is `ipairs` and we pass the table to it, telling `ipairs` to traverse that specific table for us. Each iteration, `ipairs` returns a key and a value (the same key and value used in the table).

`ipairs` will only traverse an ordered set of data, like in the above example. To traverse an unordered set of data, we use `pairs`.

```lua
local t = {
    a = 5,
    b = 10,
    c = 15
}

for key, value in pairs(t) do
    t[key] = value * 3
end
```

If at least 1 key in the table is out of order, the entire data set is considered out of order, and `ipairs` will not work. By using `pairs`, Lua will traverse it in any way possible, meaning it could get to `c` before `a` and `b`, and any other possible combination.

It may help to think of `ipairs` and `pairs` as your hands when looking through a book. If you have a book with 3 pages inside, with a number on each one (1, 2, 3) respectively, if your hands worked like `ipairs`, you would look through them in order. Otherwise, if your hands worked like `pairs`, you would flip through each one randomly, and never the same one twice.

### while loops

While loops depend on a condition to be truthy in order to continue executing, this can be used for whenever you have no idea how many times to iterate, just until you need to satisfy a specific condition.

These can be volatile, since if there's an error in your logic and the condition you provide can never end up false, the loop will execute forever and take up a large chunk of CPU until you kill the program manually.

Here is a way to use a while loop to mimic a numeric for loop:

```lua
local i = 1
while i <= 15 do
    print(i)
    i = i + 1
end
```

If `i` is never incremented, the condition would never be false and the loop would run forever. This code would print all numbers from 1 to 15.

### repeat loops

These and while loops are generally the same, and this is the type of loop you'll almost never see used or have a typical use of it. But, if you understand while loops you'll understand these as well.

Repeat loops check the condition to keep running after the body is executed, instead of before execution (like a while loop does). This can let you run the body at least once and it will determine if it should continue based off of a condition you provide.

An example of a numeric for in the form of a repeat loop:

```lua
local i = 1
repeat
    print(i)
    i = i + 1
until i >= 16
```

Again, this code prints all numbers from 1 to 15. Since the condition is checked after the body is executed to determine whether or not to run another iteration, it needs to check for 16 since after the body executes the result will be incremented by the time it reaches the condition. So if we only want it to print up until 15, the condition needs to check if it's 1 higher since we increment it before we know it already hit 15.

### Using the break keyword

By using `break`, you completely terminate the loop before it reaches its natural termination. This can be useful if you're looking for a specific value in a data set, like this:

```lua
local t = {1, 2, 3}
local lookingFor = 2
for key, value in ipairs(t) do
    if value == lookingFor then
        print("found the value we're looking for!")
        break
    end
end
```

In that example, once it reaches the 2nd iteration (which will have a value of 2, since we use `ipairs` to iterate in the exact sequence the table is defined), it will print that the value is found and will completely terminate the loop, preventing it from iterating any further.
