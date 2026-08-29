# Memoization

Memoization is a programming technique to basically "cache" expensive procedures or operations in order to avoid evaluating their results again.

Take this function for example, to generate a character list starting from lowercase chars up to a certain character code:

```lua
local mem = {}

function generateCharlist(n)
	if mem[n] then
		return mem[n]
	end
	local str = ''
	for i = 97, 97+n do -- start from lowercase
		str = str .. string.char(i) -- convert number to character
	end
	mem[n] = str
	return str
end

local firstList = generateCharlist(25) -- performs the generation
local secondList = generateCharlist(25) -- uses the pre-generated value

print(firstList, secondList) -- abcdefghijklmnopqrstuvwxyz	abcdefghijklmnopqrstuvwxyz
```

Here once `generateCharlist` is called the first time, that string is generated and inserted into the `mem` table, the next time it runs with the exact same param as the first call, it will use the pre-generated value rather than having to spend the time generating it again.

Do not use that code as a good "optimized" example of that process (specifically lines 7-10), since I intended for it to perform poorly. More info about why this is awful to do can be found in the [Optimizations](../auxiliary/optimizations.md) page.
