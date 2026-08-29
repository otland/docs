# Variables

Variables are a way to name a piece of data for future reference and usage. They can be reused over and over again without having to be recalculated or manually typed out again.

An analogy that could provide understanding of variables is a box. Say you have a box and put an object inside of it, then mark it so you know what's inside for future reference. Variables are that box, the value of the variable is the object inside of it, and the mark on the box is the variable name. When you access a variable, you take that object out to use it however you'd like.

There are two types of variables, a `local` variable and a global variable. Since explaining the difference involves scopes which requires knowledge of [Control Structures](control-structures.md), the difference will be covered later on in the [Scopes](scopes.md) section.

For now, we'll be using the `local` keyword to define any variables. The syntax for defining a local variable is: `local variable_name = value`. Since Lua is a dynamically-typed language, there's no need to define the type of value you're using, just assign a value & go.

Example of a simple variable called x:

```lua
local x = 5
```

You can also reference the value of another variable (or itself) inside the assignment:

```lua
local x = 1
local y = x + 2 -- value of y is 3
```

Variables really help out when you have a result of an expensive operation or calculation, since you can store the value without having to do that same operation or calculation again.

```lua
local var = some_function() -- Imagine this takes 1 second to execute some_function() and returns a value of 2
print(var) -- Output: 2

-- Later on:
var = var + 2 -- This is called reassignment, since var already has a value of 2, it turns into "var = 2 + 2"
print(var) -- Output: 4
```

Since `var` is assigned to the result of the expensive function, its value can be accessed as many times as we need without having to spend another second each time we need to use that specific value.

{% hint style="info" %}
Plenty more examples for variables using different types of values are in the next page.
{% endhint %}
