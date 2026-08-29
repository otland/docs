# Types

### Quick Description

* nil: A type to denote a value that is nothing, nonexistent, null.
* string: A sequence of characters (letters, symbols, numbers).
* number: Any kind of number.
* boolean: Two types of values, true or false.
* function: A chunk of redistributable code to be executed at a later time.
* table: The only data structure in the language, holds _key, value_ pairs.
* userdata: A chunk of memory which holds C data (Lua's parent language).
* thread: A reference to a coroutine.

## More Information & Examples

Since userdata and threads are advanced and are rarely used, they will not be covered here.

### nil

```lua
local x = nil -- define x, but holds no value as denoted by nil
```

```lua
local x = 5 -- start out with a number value
x = nil -- reassign x to hold no value
```

### string

```lua
local message = "Hello, world!" -- double quote definition
print(message) -- will output to console: Hello, world! without quotes
```

```lua
local message = 'Hello, world!' -- single quote definition
print(message) -- will output to console: Hello, world! without quotes
```

#### Escape Sequences

Escape sequences are a way to translate its sequence into a different character that may be difficult or impossible to respresent in a string. In Lua, the escape sequence is denoted by a backslash followed by a special character.

* **\\"**: double quote
* **\\'**: single quote
* **\\\\**: backslash
* : new line

{% hint style="info" %}
These are the main escape sequences you'll ever need to use, if you wish to see the full list, check out the Auxiliary chapter of this book.
{% endhint %}

This is a string utilizing the double quote escape sequence to insert a literal double quote into the string. The reason for this is that if you do this without using an escape sequence, you will break out of the string because a string starts with the first quote and ends with the second. More about this can be read in the [Operators](operators.md) page.

```lua
print("I love the language called \"Lua\"!") -- Output: I love the language called "Lua"!
```

The same can be done with single quotes:

```lua
print('I love the language called \'Lua\'!') -- Output: I love the language called 'Lua'!
```

Inserting literal backslashes into a string:

```lua
print("Directory: \\home\\user\\desktop") -- Output: Directory: \home\user\desktop
```

And finally, newline:

```lua
print("This string\nis split up!")
--[[ Output:
This string
is split up!
]]
```

Here is a string that cannot have any escape sequences in it, everything is interpreted as raw characters.

```lua
local message = [[Escape\n sequences\\ do \"nothing\' here!]]
print(message) -- Output: Escape\n sequences\\ do \"nothing\' here!
```

### number

The main thing that might not be obvious is the use of `e` , which means the following number is an exponent.

```lua
print(5) -- Output: 5
print(5.0) -- Output: 5.0
print(5.25225) -- Output: 5.25225
print(0.5e1) -- Output: 5.0
```

### boolean

Booleans are simple, there are only 2 possible values: `true` and `false`. Their main use is to indicate whether or not an operation or function call is successful, and used to indicate truthiness in a condition expression, which is covered in the [Operators](operators.md) page.

### table

Tables are (in my opinion) the most fun & complex data type Lua has to offer. They hold key, value pairs of data which can let you hold any kind of data you want in any order or way you'd like. The easiest way to learn how it works, is by thinking of tables as a ton of storage lockers. With a storage locker, you need a key to access what's inside of it, the same concept applies to tables. The keys for tables can be any type of value (except `nil`), and the value can be any type of value. All values must be separated by a comma.

Keys are denoted by either `[key]` or `key`. If square brackets are used, the key can be of any type, but writing the key plainly is a shortcut for a key with a `string` type. Here's a simple example of an array of numbers:

```lua
local array = {1, 2, 3}
```

You can see here that no keys are explicitly defined. If you don't explicitly define keys, they are automatically ordered starting from 1. Here's the exact same array but written with keys to show what it looks like:

```lua
local array = {
    [1] = 1,
    [2] = 2,
    [3] = 3
}
```

Both are equivalent, however, the first one is much shorter and easier to look at if you understand how it works internally.

Here is an example of what a player might look like for a game:

```lua
local player = {
    name = "John",
    health = 100,
    level = 5
}
```

Each key in this example is a `string` type, since no brackets are used. The exact same can be written with square brackets like so:

```lua
local player = {
    ["name"] = "John",
    ["health"] = 100,
    ["level"] = 5
}
```

Tables can also be nested (a table inside of a table), here's an example:

```lua
local player = {
    name = "John",
    health = 100,
    level = 5,
    friends = {"Jake", "Freddie"}
}
```

Again, since there's no explicit definition of the keys, they are automatically ordered starting from 1. To access tables, you can use either the `table[key]` syntax, or `table.key`. The difference between both is the same concept as before: with square brackets the key can be of any type, with the period the key must be a `string`. Here's an example:

```lua
local player = {
    name = "John",
    health = 100,
    level = 5,
    friends = {"Jake", "Freddie"}
}

print(player.name) -- Output: John
print(player["name"]) -- Output: John
```

### function

Functions are extremely powerful, they allow you to reuse code at any time of your choosing instead of having to copy/paste a set of code over and over again, which results in cleaner and more organized code.

Take this function for example, this defines a new function called `average` which calculates the average of the parameters passed (a & b), and uses the `return` keyword to give back a value which we use to show its output to the console.

You will see the word "call" many times throughout this book, calling means to invoke or execute a function. To call a function, use parentheses + any parameters you'd like to pass after writing the name of the function, like so: `function_name(param1, param2, etc)`

```lua
function average(a, b)
    return (a + b) / 2
end

print(average(5, 7)) -- Output: 6
```

When passing an argument to a function, it is first evaluated before the value is inserted as the parameter. In the example above, `print` is called and the **result** of `average(5, 7)` is inserted as the first parameter. However, if you don't call the function, it would give an output like this:

```lua
function average(a, b)
    return (a + b) / 2
end

print(average) -- Output: function: 0x56555778d880
```

The reason it outputs the function itself, is because it isn't called. We're simply passing the function itself to the first parameter of print instead of calling it to get a result from it.

Functions can also be a part of tables, and can be explicitly defined inside of said table within the function name using the `.` syntax used for tables normally:

```lua
local a = {}

function a.something()
    print('something!')
end

a.something() -- Ouput: something!
```

This will be prudent in the future since Lua's standard libraries include functions inside of tables, such as `table.insert`, which is part of the `table` library.

Now to introduce variadic functions. These work the same as normal functions, except they have a special parameter (which is `...`) that holds any number of values passed to it. The best example of this is the `print` function, it holds any number of parameters and outputs all of them in sequence to the console. The print function is basically written as this:

```lua
function print(...)
    local arguments = {...}
    for i = 1, #arguments do
        io.write(arguments[i] .. "\n")
    end
end
```

Don't worry if you have no clue what's going on, since this uses things we haven't gone over yet (but if you'd like to understand now, head to the [Loops](loops.md) page and come back). The gist is that `...` holds the rest of the arguments passed to the function, and it is dumped into a table so we can access them, then the rest is just outputting each argument in sequence along with a new line.

The variadic parameter doesn't have to be the only one in the parameter list, it can be used to hold any values after a specific set of arguments you'd like to take in first, like so:

```lua
function example(a, b, ...)
    -- no definition here, just an example
end

example(1, 2, 3, 4, 5, 6, "asdf", nil, "bb")
```

Parameters a & b hold 1 & 2 respectively, while the rest of the arguments are held in `...`, which can't be accessed out-of-the-box like a & b can.
