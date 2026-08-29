# Debugging

When you're not sure why your code doesn't work or some statements aren't executing, a good method of making sure where you're getting to is by debugging with print statements.

This method will allow you to see how far your function or code gets before the error or something you're expecting doesn't happen, and lets you pinpoint what you need to fix.

```lua
function swap(a)
	return not a
end

function doRandomStuff(a)
	a = swap(a)
	return swap(a)
end

function test(a)
	a = doRandomStuff(a)
	if a then
		print(123)
	end
end

test(true)
```

Here for example, we swap the boolean's value to the opposite, and if a is true we're supposed to print 123. But the problem is, swap happens twice instead of returning the 1st time it's swapped (which is the "example" error in this case. Here, we can add prints to see what's going on to see why we can't print 123:

```lua
function swap(a)
	return not a
end

function doRandomStuff(a)
	print('doRandomStuff - "a" value: '.. tostring(a))
	a = swap(a)
	print('doRandomStuff - "a" swapped value: '.. tostring(a))
	return swap(a)
end

function test(a)
	print('test - initial "a" value: '.. tostring(a))
	a = doRandomStuff(a)
	if a then
		print(123)
	end
end

test(false)
```

This current code will print:

```
test - initial "a" value: false
doRandomStuff - "a" value: false
doRandomStuff - "a" swapped value: true
```

We can see that we're obviously getting an expected value, after reassigning `a` to swap(a), which is the value we're supposed to use, but instead we swap it a 2nd time giving us back the original value (false->true->false). From here we know that the error is that we've swapped the boolean twice when it's supposed to be swapped once, so all we need to do is return `a` instead of return `swap(a)`.

```lua
function swap(a)
	return not a
end

function doRandomStuff(a)
	a = swap(a)
	return a
end

function test(a)
	a = doRandomStuff(a)
	if a then
		print(123)
	end
end

test(false)
```

Now the code works as intended, and prints 123.
