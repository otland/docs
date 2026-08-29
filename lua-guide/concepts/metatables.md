# Metatables

Metatables are the underlying implementation of objects in Lua, they define custom behaviors such as addition between 2 objects, subtraction, accessing the value, etc.

Each of those are called metamethods, and they all begin with `__`.

All metamethods (Lua 5.1)

```lua
       __eq :     Equality      :  a == b
       __le :     Less than     :  a < b
       __ge :   Greater than    :  a > b
      __add :     Addition      :  a + b
      __sub :    Subtraction    :  a - b
      __mul :   Multiplication  :  a * b
      __div :     Division      :  a / b
      __pow :   Exponentation   :  a ^ b
      __unm :     Negation      :  -a
      __mod :      Modulus      :  a % b
   __concat :   Concatenation   :  a .. b
__metatable :     Metatable     :  getmetatable(a)
     __call :       Call        :  table()
    __index :     Indexing      :  table.x | table['x']
 __newindex :     New Index     :  table.x = 'abc'
     __mode :  Weak References  :  mt.__mode = 'k'
 __tostring : String Conversion :  tostring(a)
```

By default whenever you have a string, it has a metatable attached to it as you can see here:

```lua
local s = "abc"

print(getmetatable(s)) -- {__index = table: 0x56458af94c30}

for k, v in pairs(getmetatable(s).__index) do
	print(k, v)
end
```

When attempting to index the string, it instead returns the `string` library table. Which is why if you run this code, you'll see the `__index` of the metatable print this out:

```
dump	function: 0x557e9eddcba0
byte	function: 0x557e9eddcd70
reverse	function: 0x557e9eddba30
lower	function: 0x557e9eddbcd0
gsub	function: 0x557e9eddd810
upper	function: 0x557e9eddb980
sub	    function: 0x557e9eddcc50
match	function: 0x557e9eddd7f0
gmatch	function: 0x557e9eddc000
rep	    function: 0x557e9eddbae0
len	    function: 0x557e9eddbc70
char	function: 0x557e9eddc060
format	function: 0x557e9eddc1c0
find	function: 0x557e9eddd800
```

You can directly access these by indexing the string directly, instead of going through the string library:

```lua
local s = "abc"
print(s.len(s)) -- 3
print(s:len()) -- 3
```

The second print uses the `:` syntactic sugar, both are equivalent, but the second is preferred for shorter code. The left hand of the `:` will be inserted as the first argument to `string.len`, and will result in the equivalent code: `string.len(s)`.

You can create your own tables and define metatables for them to do as you'd like, like so:

```lua
local t = {1, 2, 3}

print(tostring(t)) -- table: 0x55b410c31620

setmetatable(t, {
    __tostring = function(self)
        return table.concat(self, ', ')
    end
})

print(tostring(t)) -- __tostring invoked, output is 1, 2, 3
```

Here we define a custom metamethod for the `tostring` function for the table, which instead calls table.concat to concatenate all table values in sequence with a separator of `,` inbetween each value.
