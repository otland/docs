# Errors

### List of errors

#### Attempt to call a nil value

Description: calling a function that doesn't exist

Example:

```lua
printtt("abc") -- printtt is not a function

test() -- calling before it's defined, same error

function test() end

test() -- works
```

#### Unexpected symbol near 'something'

Description: an invalid character is placed next to a value/keyword/variable/function call

```lua
function abc()) end -- unexpected symbol near ')'

local a = 5
a l= 15 -- unexpected symbol near 'l'

local a = 5] -- unexpected symbol near ']'
```

#### Attempt to index global 'variable' (a nil value)

Description: indexing via `[key]` or `.key` for a variable that doesn't exist

Example:

```lua
abc.x = 5 -- abc is nil, error

abc = {} -- abc defined here

abc.x = 5 -- works

xyz['x'] = 'abc' -- xyz is nil, error
```

#### Attempt to perform arithmetic on a nil value

Description: performing arithmetic (\*, /, -, +, %, ^) on a nil value

Example:

```lua
print(xyz + 5) -- error, xyz not defined
a = a + 5 -- error, a not defined
```

#### Attempt to perform arithmetic on field '?' (a nil value)

Description: performing arithmetic (\*, /, -, +, %, ^) on a nil value

Example:

```lua
local t = {}
t.x = t.x + 5
```

#### Attempt to compare nil with \<TYPE>

Description: using a comparison operator (<, >, \~=, ==, >=, <=) in which one side is a nil value

Example:

```lua
local x = 5
print(x < y) -- y is not defined
```

#### Malformed number near \<NUMBER>

Description: the number has an invalid character next to it

Example:

```lua
print(12345aaa) -- aaa makes it a malformed number
```

#### Unfinished capture | Malformed pattern

Description: the pattern is missing a closing `)`, or a closing `]`

Example:

```lua
print(string.match('ABC', '(')) -- unfinished capture
print(string.match('ABC', '[')) -- malformed pattern
```

### Interpreting errors

When you get an error, Lua provides a stack trace showing you where it originates from, where the error occurs, the function calls that led to the error, and the line number of where it occurred.

A general error will look like this:

```
file_location:LINE NUMBER: error message
stack traceback:
    file_location:LINE NUMBER: in <local/function> 'FUNC'
    file_location:LINE NUMBER: in main chunk
    [C]: in ?
```

Here's an example:

```
C:\Users\user\lua_file.lua:5: attempt to perform arithmetic on a nil value (field 'x')
stack traceback:
	C:\Users\user\lua_file.lua:5: in local 'c'
	C:\Users\user\lua_file.lua:7: in local 'b'
	C:\Users\user\lua_file.lua:9: in function 'a'
	C:\Users\user\lua_file.lua:12: in main chunk
	[C]: in ?
```

The code that resulted in this error is:

```lua
function a()
	local function b()
		local function c()
			local t = {}
			t.x = t.x + 5
		end
		c()
	end
	b()
end

a()
```

Here you can see the line number `5` after the file location, which tells us where the exact line with the code that resulted in the error. The stack traceback shows the functions that were called that led up to that.

First, function `a` is called at line 12, then function `b` is called at line 9 inside of `a`, then `c` is called at line 7 inside of function `b`, and finally at line 5, the error occurs inside of function `c`.

A note to add is that comments can offset the line number and make it appear as the error is in a line that doesn't exist or doesn't look like an error,
