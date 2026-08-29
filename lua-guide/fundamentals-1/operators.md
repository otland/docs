# Operators

Operators are a symbol(s) to perform a specific action. Operands are the values the operator uses in the action.

### Relational Operators

When using these operators, both operands must be the of the same type.

Comparing by reference means both operands must point to the exact same memory address, the value of its contents don't matter. Example:

```lua
local a = {1, 2, 3}
local b = {1, 2, 3}
local c = a -- c now also holds the same reference to the table that a does
print(a == b) -- Output: false, both have separate memory addresses
print(a == c) -- Output: true, both variables hold the same reference to the exact same table
```

{% tabs %}
{% tab title="<" %}
Operator: Less Than (`a < b`)

If the value of `a` is less than `b`, the result is `true`, otherwise, `false`.

Operands Types:

* number (compares by value)
* string (compares by alphabetical order)
{% endtab %}

{% tab title=">" %}
Operator: Greater Than (`a > b`)

If the value of `a` is greater than `b`, the result is `true`, otherwise, `false`.

Operands Types:

* number (compares by value)
* string (compares by alphabetical order)
{% endtab %}

{% tab title="<=" %}
Operator: Less Than or Equal To (`a <= b`)

If the value of `a` is less than or equal to `b`, the result is `true`, otherwise, `false`.

Operands Types:

* number (compares by value)
* string (compares by alphabetical order)
{% endtab %}

{% tab title=">=" %}
Operator: Greater Than or Equal To (`a >= b`)

If the value of `a` is greater than or equal to `b`, the result is `true`, otherwise, `false`.

Operands Types:

* number (compares by value)
* string (compares by alphabetical order)
{% endtab %}

{% tab title="==" %}
Operator: Equal (`a == b`)

If `a` is exactly equal to `b`, the result is `true`, otherwise, `false`.

Operands Types:

* number (compares by value)
* string (compares by value)
* boolean (compares by value)
* function (compares by reference)
* table (compares by reference)
* userdata (compares by reference)
* thread (compares by reference)
{% endtab %}

{% tab title="~=" %}
Operator: Not Equal (`a ~= b`)

If `a` is anything but `b`, the result is `true`, otherwise, `false`.

Operands Types:

* number (compares by value)
* string (compares by value)
* boolean (compares by value)
* function (compares by reference)
* table (compares by reference)
* userdata (compares by reference)
* thread (compares by reference)
{% endtab %}
{% endtabs %}

### Logical Operators

Note: When something is defined as being "truthy", it means that the value is considered to be `true` by Lua, which is any value that isn't `false` or `nil`.

{% tabs %}
{% tab title="and" %}
Syntax: `a and b` where a & b are both evaluated as expressions.

If `a` is truthy, `b` is the result of the operation, otherwise it is the result of `a`.

```lua
local x = true and 5 -- x is 5
local y = x and 10 -- y is 10, x is evaluated to true because 5 isn't a value of false or nil
local z = false and 100 -- false, a is not truthy thus the second value is not the result
```
{% endtab %}

{% tab title="or" %}
Syntax: `a or b` where a & b are both evaluated as expressions.

If `a` is truthy, result is `a`, otherwise `b`.

```lua
local x = true or 5 -- x is true, a is truthy so b is never evaluated
local y = false or 10 -- y is 10, a is not truthy so b is evaluated and the result
local z = (10 > 5) or (x + y) -- true, a is evaluated and 10 > 5 results in true, b is never evaluated
```
{% endtab %}

{% tab title="not" %}
Syntax: `not a`

Inverts the truthiness of `a`, any expression or value that results in true, the value is flipped to false, and vice versa.

```lua
local x = not true -- x is false
local y = not x -- y is true
```
{% endtab %}
{% endtabs %}

Here are some more examples pairing these operators together:

```lua
local x = 1
local y = 2
--    (    A operand to 'or'    )    (  B operand to 'or'  )
--    (1 > 2  and <expression>  ) or (<fallback expression>)    
print((x > y) and 'X is greater!' or 'Y is greater!') -- Output: Y is greater!
```

Since 1 (x) is not a greater number than 2 (y), the result of the `and` operator is `nil` because of the `a` operand resulting in `false`, the `or` operator comes in because the result of the `and` operation is the `a` operand to `or`, so the result looks like `nil or 'Y is greater!'`. In plain English, all that's happening here is: "If my x variable is bigger than our y variable, give me back a string that says X is greater, otherwise, give me a string that says Y is greater."

### Mathematical Operators

{% tabs %}
{% tab title="Addition (+)" %}
Syntax: `a + b`

```lua
local x = 5 + 10 -- 15
local y = 1.2 + 6.3 -- 7.5
```
{% endtab %}

{% tab title="Subtraction (-)" %}
Syntax: `a - b`

```lua
local x = 5 - 2 -- 3
local y = 2.5 - 1.2 -- 1.3
```
{% endtab %}

{% tab title="Multiplication (*)" %}
Syntax: `a * b`

```lua
local x = 5 * 3 -- 15
local y = 1.5 * 1.5 -- 2.25
```
{% endtab %}

{% tab title="Division (/)" %}
Syntax: `a / b`

```lua
local x = 10 / 2 -- 5
local y = 9 / 2.5 -- 3.6
```
{% endtab %}

{% tab title="Exponentation (^)" %}
Syntax: `a ^ b`

```lua
local x = 5 ^ 2 -- 25
local y = 2 ^ 2.5 -- 5.65685424949
```
{% endtab %}

{% tab title="Negation (-)" %}
Syntax: `-a`

```lua
local x = -5 -- -5
local y = 10 -- 10
y = -y -- y is now -10
y = -x -- y is now 5
```
{% endtab %}
{% endtabs %}

### Concatenation

Concatenation is an operation that joins two strings together. The result is a copy of both strings joined together, since Lua cannot manipulate the contents of a string itself.

Syntax: `a .. b`

Examples:

```lua
local a = "Hello "
local b = ", world!"
print(a .. b) -- Output: Hello, world!
```

{% hint style="info" %}
You can chain these operators however many times you like in any order.
{% endhint %}

### Length

The length operator (#) is primarily used on tables, but can be effective for strings as well. For strings, it returns the number of bytes (usually each byte is a single character). For tables, it returns the length of the table as long as it has no holes and is ordered:

```lua
local t = {1, 2, 3}
print(#t) -- 3
```

Depending on the version of Lua you're using, if the array or table has nil values inbetween the other values, the result of the length operator will be different. Any keys that aren't numerical are not counted towards the length.

If you have keys that aren't numbers, or have nil values/holes in your table, a table size function can be implemented by simply using the `pairs` iterator:

```lua
function table.size(t)
    local size = 0
    for k, v in pairs(t) do
        size = size + 1
    end
    return size
end

local t = {1, 2, 3}
local t2 = {a = 5, [2] = 4, 84}
print(table.size(t), table.size(t2)) -- Output: 3 3
```
