# Optimizations

### String concatenation

Lua's garbage collector will run when it detects if too much memory is in use by the program. When using the string concat (..) operator, the result is a completely new string, and the old one is garbage if you're reassigning (which results in the old string having no reference) `x = x .. "\n"`, the garbage collector will eventually run and collect this string. When you're concatenating large strings together over and over again (like in a loop) that will add up quickly and force the garbage collector to run and will slow down code by a lot the larger those strings are.

```lua
local result = ''

for line in io.lines('large_file.txt') do
    result = result .. line -- old 'result' is now garbage
end
```

This code will take much longer to run because the more and more lines concatenated to result, the larger result is, and the larger result is, the more memory is used and forces the garbage collector to run.

A solution to speed this process up is by putting all strings into a table and running `table.concat` on it:

```lua
local strings = {}

for line in io.lines('large_file.txt') do
    table.insert(strings, line)
end

local result = table.concat(strings, '\n')
```

This will be much faster than manually concatenating all strings (table.concat uses a C implementation rather than Lua)

{% hint style="info" %}
Before getting into the rest of the optimizations, you really don't need to be using these unless you're **really** trying to get performance out of a hugely expensive program or function call.
{% endhint %}

### Squeezing performance from table indexing

When indexing a table to retrieve a value, it takes time. Although a small amount of time, it can result in a decent chunk of time if you're running a function which takes a long time to finish regardless of this optimization. Calling lib functions such as string.len, table.concat, etc. all take time since they're a part of libraries which are tables. This is a way to store those functions without having to retrieve them over and over again:

```lua
local stringLen = string.len
```

Now we the function retrieved and stored in stringLen rather than having to retrieve it over and over again from the string library. Calling stringLen in an expensive function will increase performance by a lot.

```lua
local stringLen = string.len
local tostring = tostring

function f()
	for i = 1, 10000 do
		stringLen(tostring(i))
	end
end

function f_2()
	for i = 1, 10000 do
		string.len(tostring(i))
	end
end
```

Between these two functions, `f` will perform faster than `f_2` because both functions used are saved in a local variable rather than getting retrieved from `_G`, which saves time over a long period of time.

### Adding values to tables

Lua provides a default function to insert a value into a table (table.insert), but, using this function takes significantly longer if you're just trying to insert a value into the next index that isn't used. If you're just looking to insert a new value into the next available index, this will perform much faster:

```lua
local t = {}
t[#t+1] = 'a'
t[#t+1] = 'b'
```

Here we just calculate the next index by using the current size + 1 (#t + 1) and insert a value into that new index.

If you're using a loop to insert new values, keeping track of the index manually will be faster than using the length operator each iteration:

```lua
local strings = {'a', 'b', 'c'}
local toInsert = {'d', 'e', 'f', 'g'}

local index = #strings -- current size
for _, str in ipairs(toInsert) do
    index = index + 1
    strings[index] = str
end
```

Since we keep track of the index manually and add 1 each iteration, the length operator doesn't need to be used every single time which would add up after a while.
