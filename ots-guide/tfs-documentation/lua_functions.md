# Lua functions

## Game

### Available methods:

* [broadcastMessage\(message, messageType\)](lua_functions.md#Game-broadcastMessage)
* [convertIpToString\(ip\)](lua_functions.md#Game-convertIpToString)
* [createItem\(itemId, count\[, position\]\)](lua_functions.md#Game-createItem)
* [createContainer\(itemId, size\[, position\]\)](lua_functions.md#Game-createContainer)
* [createMonster\(monsterName, position\[, extended = false\[, force = false\]\]\)](lua_functions.md#Game-createMonster)
* [createNpc\(npcName, position\[, extended = false\[, force = false\]\]\)](lua_functions.md#Game-createNpc)
* [createTile\(x, y, z\[, isDynamic = false\]\)](lua_functions.md#Game-createTile)
* [createTile\(position\[, isDynamic = false\]\)](lua_functions.md#Game-createTile)
* [getExperienceStage\(level\)](lua_functions.md#Game-getExperienceStage)
* [getGameState\(\)](lua_functions.md#Game-getGameState)
* [getHouses\(\)](lua_functions.md#Game-getHouses)
* [getMonsterCount\(\)](lua_functions.md#Game-getMonsterCount)
* [getNpcCount\(\)](lua_functions.md#Game-getNpcCount)
* [getPlayerCount\(\)](lua_functions.md#Game-getPlayerCount)
* [getPlayers\(\)](lua_functions.md#Game-getPlayers)
* [getReturnMessage\(value\)](lua_functions.md#Game-getReturnMessage)
* [getReverseDirection\(direction\)](lua_functions.md#Game-getReverseDirection)
* [getSkillType\(weaponType\)](lua_functions.md#Game-getSkillType)
* [getSpectators\(position\[, multifloor = false\[, onlyPlayer = false\[, minRangeX = 0\[, maxRangeX = 0\[, minRangeY = 0\[, maxRangeY = 0\]\]\]\]\]\]\)](lua_functions.md#Game-getSpectators)
* [getStorageValue\(key\)](lua_functions.md#Game-getStorageValue)
* [getTowns\(\)](lua_functions.md#Game-getTowns)
* [getWorldType\(\)](lua_functions.md#Game-getWorldType)
* [loadMap\(path\)](lua_functions.md#Game-loadMap)
* [setGameState\(state\)](lua_functions.md#Game-setGameState)
* [setStorageValue\(key, value\)](lua_functions.md#Game-setStorageValue)
* [setWorldType\(type\)](lua_functions.md#Game-setWorldType)
* [startRaid\(raidName\)](lua_functions.md#Game-startRaid)

#### Game.broadcastMessage\(message, messageType\)

> **Description:** Send message to all players **Parameters:** **Returns:** Nothing **Example:**
>
> ```lua
> local message = 'Hello'
> local messageType = MESSAGE_STATUS_DEFAULT
> Game.broadcastMessage(message, messageType)
> ```
>
> **Added in version:** 1.0

#### Game.convertIpToString\(ip\)

> **Description:** Convert numeric representation of IPv4 to string with dot separated octets **Parameters:** **Returns:** String **Example:**
>
> ```lua
> function Player:onLook(thing, position, distance)
>   if thing:isCreature() then
>     if thing:isPlayer() then
>       local playerIp = thing:getIp()
>       local ip = Game.convertIpToString(playerIp)
>       local description = string.format("IP: [%s].", ip)
>     end
>   end
>   self:sendTextMessage(MESSAGE_INFO_DESCR, description)
>   return true
> end
> ```
>
> **Added in version:** 1.0

#### Game.createItem\(itemId, count\[, position\]\)

> **Description:** Creates an item.  
> **Parameters:** **Returns:** The item created. \(userdata\)  
> **Example:**
>
> ```lua
> -- Create an item somewhere on the map.
> local item = Game.createItem(2400, 1, Position(100, 100, 7))
> --
> -- Create a temporary item that is given to a player (if it isn't moved from creation it will be deleted)
> local player = Player(...)
> player:addItemEx(Game.createItem(2400, 1))
> ```
>
> **Added in version:** 1.0

#### Game.createContainer\(itemId, size\[, position\]\)

> **Description:** Creates a container with given size.  
> **Parameters:** **Returns:** The container created. \(userdata\)  
> **Example:**
>
> ```lua
> -- Create an amulet of loss as a container with size 5 at position: x 100, y 100, z 7.
> local item = Game.createContainer(ITEM_AMULETOFLOSS, 5, Position(100, 100, 7))
> --
> -- Create a temporary container that is given to a player (if it isn't moved from creation it will be deleted)
> local player = Player(...)
> player:addItemEx(Game.createContainer(ITEM_AMULETOFLOSS, 5))
> ```
>
> **Added in version:** 1.1

#### Game.createMonster\(monsterName, position\[, extended = false\[, force = false\]\]\)

> **Description:** Creates a monster.  
> **Parameters:** **Returns:** The monster created. \(userdata\)  
> **Example:**
>
> ```lua
> -- This should always create this monster.
> local monster = Game.createMonster("demon", Position(100, 100, 7), false, true)
> if not monster then
>     -- Something went wrong?
> end
> ```
>
> **Added in version:** 1.0

#### Game.createNpc\(npcName, position\[, extended = false\[, force = false\]\]\)

> **Description:** Creates a npc.  
> **Parameters:** **Returns:** The npc created. \(userdata\)  
> **Example:**
>
> ```lua
> -- This may possibly not create the npc.
> local npc = Game.createMonster("some npc", Position(100, 100, 7), false, false)
> if not npc then
>     -- Something is probably blocking that position and around it aswell
> end
> ```
>
> **Added in version:** 1.0

#### Game.createTile\(x, y, z\[, isDynamic = false\]\)

> **Description:** Creates a tile if it can.  
> **Parameters:** **Returns:** The tile created or the previous existing one. \(userdata\)  
> **Example:**
>
> ```lua
> local tile = Game.createTile(100, 100, 7)
> local ground = tile:getGround()
> if ground then
>     print(ground:getName())
> end
> ```
>
> **Added in version:** 1.0

#### Game.createTile\(position\[, isDynamic = false\]\)

> **Description:** Creates a tile if it can.  
> **Parameters:** **Returns:** The tile created or the previous existing one. \(userdata\)  
> **Example:**
>
> ```lua
> local tile = Game.createTile(Position(100, 100, 7))
> local ground = tile:getGround()
> if ground then
>     print(ground:getName())
> end
> ```
>
> **Added in version:** 1.0

#### Game.getExperienceStage\(level\)

> **Description:** Find the experience rate related to a certain level.  
> **Parameters:** **Returns:** The experience rate related to the specified level.  
> **Example:**
>
> ```lua
> -- Print the experience rate for level 8 to the console
> print(Game.getExperienceStage(8))
> ```
>
> **Added in version:** 1.0

#### Game.getGameState\(\)

> **Description:** Gets the current gamestate.  
> **Parameters:** None  
> **Returns:** Current gamestate on the server.  
> **Example:**
>
> ```lua
> print(Game.getGameState())
> ```
>
> **Added in version:** 1.0

#### Game.getHouses\(\)

> **Description:** Get all houses.  
> **Parameters:** None  
> **Returns:** A table containing all houses \(userdata\).  
> **Example:**
>
> ```lua
> -- This prints the names of all houses that exist on the server
> local houses = Game.getHouses()
> for i = 1, #houses do
>     print(houses[i]:getName())
> end
> ```
>
> **Added in version:** 1.0

#### Game.getMonsterCount\(\)

> **Description:** Find the total amount of monsters on the server.  
> **Parameters:** None  
> **Returns:** Total amount of monsters on the server.  
> **Example:**
>
> ```lua
> print(Game.getMonsterCount())
> ```
>
> **Added in version:** 1.0

#### Game.getNpcCount\(\)

> **Description:** Find the total amount of npcs on the server.  
> **Parameters:** None  
> **Returns:** Total amount of npcs on the server.  
> **Example:**
>
> ```lua
> print(Game.getNpcCount())
> ```
>
> **Added in version:** 1.0

#### Game.getPlayerCount\(\)

> **Description:** Find the total amount of players on the server.  
> **Parameters:** None  
> **Returns:** Total amount of players on the server.  
> **Example:**
>
> ```lua
> print(Game.getPlayerCount())
> ```
>
> **Added in version:** 1.0

#### Game.getPlayers\(\)

> **Description:** Get all connected players.  
> **Parameters:** None  
> **Returns:** A table containing all connected players \(userdata\).  
> **Example:**
>
> ```lua
> -- This prints the names of all players connected to the server
> local players = Game.getPlayers()
> for i = 1, #players do
>     print(players[i]:getName())
> end
> ```
>
> **Added in version:** 1.0

#### Game.getReturnMessage\(value\)

> **Description:** Gets a message associated with the value.  
> **Parameters:** **Returns:** true  
> **Example:**
>
> ```lua
> -- This makes no sense but its an example.
> local player = Player(...)
> player:say(Game.getReturnMessage(RETURNVALUE_YOUARENOTTHEOWNER), TALKTYPE_SAY)
> ```
>
> **Added in version:** 1.0

#### Game.getReverseDirection\(direction\)

> **Description:** Gets reversed direction. **Parameters:** **Returns:** Direction \(integer\) **Example:**
>
> ```lua
> local direction = DIRECTION_NORTH
> local reversedDirection = Game.getReverseDirection(direction)
> print('Numerical value of SOUTH direction is equel '.. tostring(reversedDirection))
> ```
>
> **Added in version:** 1.0

#### Game.getSkillType\(weaponType\)

> **Description:** Gets skill type associatet with weapon type. **Parameters:** **Returns:** Skill type \(integer\) **Example:**
>
> ```lua
> local itemtype = ItemType(...)
> local weaponType = itemtype:getWeaponType()
> local skillType = Game.getSkillType(weaponType)
> ```
>
> **Added in version:** 1.0

#### Game.getSpectators\(position\[, multifloor = false\[, onlyPlayer = false\[, minRangeX = 0\[, maxRangeX = 0\[, minRangeY = 0\[, maxRangeY = 0\]\]\]\]\]\]\)

> **Description:** Get all creatures in the area.  
> **Parameters:** **Returns:** A table containing creatures found \(userdata\).  
> **Example:**
>
> ```lua
> -- This finds all players in a 5x5 area around (100, 100, 7)
> local spectators = Game.getSpectators(Position(100, 100, 7), false, true, 0, 2, 0, 2)
> for i = 1, #spectators do
>     local spectator = spectators[i]
>     spectator:say(spectator:getName(), TALKTYPE_SAY)
> end
> ```
>
> **Added in version:** 1.0

#### Game.getStorageValue\(key\)

> **Description:** Get value from globalStorageTable **Parameters:** **Returns:** Value from table on empty index nil value **Example:**
>
> ```lua
> local storage = Game.getStorageValue(1)
> print(tostring(storage))
> ```
>
> **Added in version:** 1.0

#### Game.getTowns\(\)

> **Description:** Get all towns.  
> **Parameters:** None  
> **Returns:** A table containing all towns \(userdata\).  
> **Example:**
>
> ```lua
> -- This prints the names of all towns that exist on the server
> local towns = Game.getTowns()
> for i = 1, #towns do
>     print(towns[i]:getName())
> end
> ```
>
> **Added in version:** 1.0

#### Game.getWorldType\(\)

> **Description:** Gets the current world type.  
> **Parameters:** None  
> **Returns:** Current gamestate on the server.  
> **Example:**
>
> ```lua
> print(Game.getWorldType())
> ```
>
> **Added in version:** 1.0

#### Game.loadMap\(path\)

> **Description:** This loads a new map chunk.  
> **Parameters:** **Returns:** Nothing  
> **Example:**
>
> ```lua
> Game.loadMap("data/map/some_other_map.otbm")
> ```
>
> **Added in version:** 1.0

#### Game.setGameState\(state\)

> **Description:** Sets the current gamestate.  
> **Parameters:** **Returns:** true  
> **Example:**
>
> ```lua
> -- Shutdown the server
> Game.setGameState(GAME_STATE_SHUTDOWN)
> ```
>
> **Added in version:** 1.0

#### Game.setStorageValue\(key, value\)

> **Description:** Insert value into globalStorageTable on specific key **Parameters:** **Returns:** Nothing **Example:**
>
> ```lua
> Game.setStorageValue(1, 1000)
> ```
>
> **Added in version:** 1.0

#### Game.setWorldType\(type\)

> **Description:** Sets the current world type.  
> **Parameters:** **Returns:** true  
> **Example:**
>
> ```lua
> -- Change to hardcore pvp
> Game.setWorldType(WORLD_TYPE_PVP_ENFORCED)
> ```
>
> **Added in version:** 1.0

#### Game.startRaid\(raidName\)

> **Description:** Starts a raid if one with said name exist.  
> **Parameters:** **Returns:** true if the raid started, nil otherwise.  
> **Example:**
>
> ```lua
> if Game.startRaid("test") then
>     -- Raid was started.
> end
> ```
>
> **Added in version:** 1.0

## Global

### Available methods:

[addEvent\(callback, delay, ...\)](lua_functions.md#addEvent) [stopEvent\(eventid\)](lua_functions.md#stopEvent)

#### addEvent\(callback, delay, ...\)

> **Description:** This function is used to run other functions at a later time.  
> **Parameters:** **Returns:** The id associated with this event.  
> **Example:**
>
> ```lua
> -- Creates an event that prints "Hello World!" to the console.
> addEvent(print, 1000, "Hello World!")
> ```
>
> **Added in version:** 1.0

#### stopEvent\(eventid\)

> **Description:** This function is used to stop functions that should run later.  
> **Parameters:** **Returns:** true if an event was stopped, false otherwise.  
> **Example:**
>
> ```lua
> -- Creates an event that should print "Hello World!" but it's stopped before that can happen.
> local event = addEvent(print, 1000, "Hello World!")
> stopEvent(event)
> ```
>
> **Added in version:** 1.0

## os

### Available methods:

[mtime\(\)](lua_functions.md#os-mtime)

#### os.mtime\(\)

> **Description:** Returns the Unix time \(epoch\) in milliseconds  
> **Parameters:** None  
> **Returns:** The Unix time \(epoch\) in milliseconds  
> **Example:**
>
> ```lua
> print(os.mtime() .. " milliseconds have passed since the Unix epoch")
> ```
>
> **Added in version:** 1.0

## table

### Available methods:

[create\(arrayLength, keyLength\)](lua_functions.md#table-create)

#### table.create\(arrayLength, keyLength\)

> **Description:** Creates a new table with specified length.  
> **Parameters:** **Returns:** The created table.  
> **Example:**
>
> ```lua
> local t = table.create(5, 0)
> for i = 1, #t do
>     t[i] = i + 1
> end
> ```
>
> **Added in version:** 1.0

