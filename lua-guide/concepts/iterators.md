# Iterators

Iterators provide a way to traverse data. Iterators will usually use a closure to keep track of what data it's on and uses that to determine what to give next.

Take the iterator `ipairs` for example, it traverses a table in sequence. Its implementation can be written like this:

```lua
function ipairs(t)
    local index = 0
    return function()
       index = index + 1
       if t[index] then -- check if the value exists
           return index, t[index] -- key, value
       end
       return nil 
    end
end

local t = {1, 2, 3}
for k, v in ipairs(t) do
    print(k, v)
end
```

```
Output:
1 1
2 2
3 3
```

Using closures, you can define your own way to iterate through a set of data. You could iterate half of it forward and half of it backwards, iterate the entire thing in reverse, iterate every 2 values, etc.

Here's what a reverse `ipairs` would look like:

```lua
function revipairs(t)
    local index = #t + 1 -- start at the last index in the table, +1 to make sure it hits the end value when index-1 happens
    return function()
        index = index - 1 -- travel backwards from the end
        if t[index] then -- again, checking if the value exists
            return index, t[index]
        end
        return nil
    end
end

local t = {1, 2, 3}
for k, v in revipairs(t) do
    print(k, v)
end
```

```
Output:
3 3
2 2
1 1
```
