# Object-Oriented Programming

Object-Oriented Programming (shortened to OOP) is a programming paradigm to wrap up a set of variables and functions (called methods) inside of a single object. A common example of this is a "Player" in a game, each player has the same set of variable names but different values, such as health, name, etc. A `class` is the definition of the variables and methods which are used by objects created using that class.

Since Lua has no true OOP implementation such as classes, we can get quite close to OOP and still be able to create unique objects and play around with them. The way we wrap all variables and functions inside a "class" is by holding all of that data in a table. Here's an example of creating a Player class:

```lua
Player = {}

setmetatable(Player, {
	__call = function(self, name, health)
		local playerData = {
			name = name,
			health = health
		}
		return setmetatable(playerData, {__index = Player})
	end
})

function Player.getName(self)
	return self.name
end

function Player.getHealth(self)
	return self.health
end

function Player.print(self)
	print('Player "'.. self:getName() ..'": (Health: '.. self:getHealth() ..')')
end

local playerOne = Player('John', 100)
local playerTwo = Player('Jack', 150)
playerOne:print()
playerTwo:print()
```

The output of the above example results in:

```
Player "John": (Health: 100)
Player "Jack": (Health: 150)
```

Here we use the `__call`metamethod to create a definition on what happens when you call the table like it's a function. Player is defined at the top as a table, `{}`, but with the `__call` metamethod, doing `Player(name, health)`is valid. Once the `__call`metamethod is invoked, we simply take the arguments passed to it and insert it into a table. After which, we just simply return the table after using `setmetatable` to define our object's `__index`, which is used whenever we try to access the player object's table. The `__index` will hold everything inside of the Player table, but out object only holds name and health. Using `__index`, if what we're trying to access doesn't exist in the player object such as doing `playerOne.xyz`, it uses the table defined in `__index` to look in as well, if `xyz` is a key inside of Player, then that is returned.

We can see that here, there are 3 methods defined inside the Player table, which are getName, getHealth, and print. When calling `playerOne:print()`, it searches the player object which only holds `{name = 'John', health = 100}`, since `print` is not a key in our player object, it will search the `Player` table for it, and since we did define a `print` method, that will be used.

Again, `playerOne:print()` is the equivalent to `Player.print(playerOne)`, just shorter and using the `:` syntax sugar.
