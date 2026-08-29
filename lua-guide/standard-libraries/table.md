# Table

### table.concat

Description: concatenates all strings in the table, starting from i, ending with j (default 1, #t respectively), separating with the `separator` value if defined, otherwise there is no separation.

Usage: table.concat(table \[, separator \[, i \[, j]]])

Example:

```lua
local t = {'a', 'b', 'c'}
print(table.concat(t)) -- abc
print(table.concat(t, ', ')) -- a, b, c
print(table.concat(t, ', ', 2)) -- b, c
print(table.concat(t, nil, 1, 2)) -- ab
```

### table.insert

Description: inserts a value to the end of the table, or at `pos`

Usage: table.insert(table, \[pos,] value)

Example:

```lua
local t = {'a', 'b', 'c'}
table.insert(t, 'd') -- {'a', 'b', 'c', 'd'}
table.insert(t, 3, 'f') -- {'a', 'b', 'f', 'c', 'd'}
```

### table.maxn

Description: returns the highest numerical index found in the table (different from true size)

Usage: table.maxn(table)

Example:

```lua
local t = {1, 2, 3, 4, 5, 100, 3, 77, 275}
print(table.maxn(t)) -- 9

t = {1, 2, 3, 4, 5, 100, 3, 77, 275, nil, nil, 177, ['a'] = 5}
print(table.maxn(t)) -- 12, 'a' is not a numerical index
```

### table.remove

Description: removes a value from the table at the end, or at `pos`

Usage: table.remove(table \[, pos])

Example:

```lua
local t = {1, 2, 3, 4, 5}
table.remove(t) -- {1, 2, 3, 4}
table.remove(t, 2) -- {1, 3, 4}
```

### table.sort

Description: sorts table with given `comp` (comparison) function, if not given, `<` is used by default, which results in least to greatest.

Usage: table.sort(table \[, comp])

Example:

```lua
local t = {5, 26, 7, 1, 400}
table.sort(t) -- {1, 5, 7, 26, 400}

local t = {5, 26, 7, 1, 400}
table.sort(t, function(a, b) return a > b end) -- {400, 26, 7, 5, 1}
```
