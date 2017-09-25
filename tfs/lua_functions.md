### Game
#### Available methods:
[createItem(itemId, count[, position])](#Game.createItem{itemId, count[, position]})  
[createContainer(itemId, size[, position])](#Game.createContainer{itemId, size[, position]})  
[createMonster(monsterName, position[, extended = false[, force = false]])](#Game.createMonster{monsterName, position[, extended = false[, force = false]]})  
[createNpc(npcName, position[, extended = false[, force = false]])](#Game.createNpc{npcName, position[, extended = false[, force = false]]})  
[createTile(x, y, z[, isDynamic = false])](#Game.createTile{x, y, z[, isDynamic = false]})  
[createTile(position[, isDynamic = false])](#Game.createTile{position[, isDynamic = false]})  
[getExperienceStage(level)](#Game.getExperienceStage{level})  
[getGameState()](#Game.getGameState{})  
[getHouses()](#Game.getHouses{})  
[getMonsterCount()](#Game.getMonsterCount{})  
[getNpcCount()](#Game.getNpcCount{})  
[getPlayerCount()](#Game.getPlayerCount{})  
[getPlayers()](#Game.getPlayers{})  
[getReturnMessage(value)](#Game.getReturnMessage{value})  
[getSpectators(position[, multifloor = false[, onlyPlayer = false[, minRangeX = 0[, maxRangeX = 0[, minRangeY = 0[, maxRangeY = 0]]]]]])](#Game.getSpectators{position[, multifloor = false[, onlyPlayer = false[, minRangeX = 0[, maxRangeX = 0[, minRangeY = 0[, maxRangeY = 0]]]]]]})  
[getTowns()](#Game.getTowns{})  
[getWorldType()](#Game.getWorldType{})  
[loadMap(path)](#Game.loadMap{path})  
[setGameState(state)](#Game.setGameState{state})  
[setWorldType(type)](#Game.setWorldType{type})  
[startRaid(raidName)](#Game.startRaid{raidName})  


***

<a name="Game.createItem{itemId, count[, position]}"/>
###### Game.createItem(itemId, count[, position])
> **Description:** Creates an item.  
> **Parameters:** <ul><li>_itemId_ - _Id of the item to be created_</li><li>_count_ - _How many are we creating?_</li><li>_position_ - _Where do we place it? (optional)_</li></ul>
> **Returns:** The item created. (userdata)  
> **Example:** 
```Lua
-- Create an item somewhere on the map.
local item = Game.createItem(2400, 1, Position(100, 100, 7))
--
-- Create a temporary item that is given to a player (if it isn't moved from creation it will be deleted)
local player = Player(...)
player:addItemEx(Game.createItem(2400, 1))
```
> **Added in version:** 1.0

***

<a name="Game.createContainer{itemId, size[, position]}"/>
###### Game.createContainer(itemId, size[, position])
> **Description:** Creates a container with given size.  
> **Parameters:** <ul><li>_itemId_ - _Id of the item to be created_</li><li>_size_ - _Size of the container_</li><li>_position_ - _Where do we place it? (optional)_</li></ul>
> **Returns:** The container created. (userdata)  
> **Example:** 
```Lua
-- Create an amulet of loss as a container with size 5 at position: x 100, y 100, z 7.
local item = Game.createContainer(ITEM_AMULETOFLOSS, 5, Position(100, 100, 7))
--
-- Create a temporary container that is given to a player (if it isn't moved from creation it will be deleted)
local player = Player(...)
player:addItemEx(Game.createContainer(ITEM_AMULETOFLOSS, 5))
```
> **Added in version:** 1.1

***

<a name="Game.createMonster{monsterName, position[, extended = false[, force = false]]}"/>
###### Game.createMonster(monsterName, position[, extended = false[, force = false]])
> **Description:** Creates a monster.  
> **Parameters:** <ul><li>_monsterName_ - _Name of the monster to be created_</li><li>_position_ - _Where do we place it?_</li><li>_extended_ - _Extend the range? (optional, default: false)_</li><li>_force_ - _Will it be created even if it cannot stand at the position? (optional, default: false)_</li></ul>
> **Returns:** The monster created. (userdata)  
> **Example:** 
```Lua
-- This should always create this monster.
local monster = Game.createMonster("demon", Position(100, 100, 7), false, true)
if not monster then
	-- Something went wrong?
end
```
> **Added in version:** 1.0

***

<a name="Game.createNpc{npcName, position[, extended = false[, force = false]]}"/>
###### Game.createNpc(npcName, position[, extended = false[, force = false]])
> **Description:** Creates a npc.  
> **Parameters:** <ul><li>_npcName_ - _Name of the npc to be created_</li><li>_position_ - _Where do we place it?_</li><li>_extended_ - _Extend the range? (optional, default: false)_</li><li>_force_ - _Will it be created even if it cannot stand at the position? (optional, default: false)_</li></ul>
> **Returns:** The npc created. (userdata)  
> **Example:** 
```Lua
-- This may possibly not create the npc.
local npc = Game.createMonster("some npc", Position(100, 100, 7), false, false)
if not npc then
	-- Something is probably blocking that position and around it aswell
end
```
> **Added in version:** 1.0

***

<a name="Game.createTile{x, y, z[, isDynamic = false]}"/>
###### Game.createTile(x, y, z[, isDynamic = false])
> **Description:** Creates a tile if it can.  
> **Parameters:** <ul><li>_x_ - _X coordinate_</li><li>_y_ - _Y coordinate_</li><li>_z_ - _Z coordinate_</li><li>_isDynamic_ - _Is this tile dynamic? (optional, default: false)_</li></ul>
> **Returns:** The tile created or the previous existing one. (userdata)  
> **Example:** 
```Lua
local tile = Game.createTile(100, 100, 7)
local ground = tile:getGround()
if ground then
	print(ground:getName())
end
```
> **Added in version:** 1.0

***

<a name="Game.createTile{position[, isDynamic = false]}"/>
###### Game.createTile(position[, isDynamic = false])
> **Description:** Creates a tile if it can.  
> **Parameters:** <ul><li>_position_ - _Location of the tile._</li><li>_isDynamic_ - _Is this tile dynamic? (optional, default: false)_</li></ul>
> **Returns:** The tile created or the previous existing one. (userdata)  
> **Example:** 
```Lua
local tile = Game.createTile(Position(100, 100, 7))
local ground = tile:getGround()
if ground then
	print(ground:getName())
end
```
> **Added in version:** 1.0

***

<a name="Game.getExperienceStage{level}"/>
###### Game.getExperienceStage(level)
> **Description:** Find the experience rate related to a certain level.  
> **Parameters:** <ul><li>_level_ - _Level to get the stage with._</li></ul>
> **Returns:** The experience rate related to the specified level.  
> **Example:** 
```Lua
-- Print the experience rate for level 8 to the console
print(Game.getExperienceStage(8))
```
> **Added in version:** 1.0

***

<a name="Game.getGameState{}"/>
###### Game.getGameState()
> **Description:** Gets the current gamestate.  
> **Parameters:** None  
> **Returns:** Current gamestate on the server.  
> **Example:** 
```Lua
print(Game.getGameState())
```
> **Added in version:** 1.0

***

<a name="Game.getHouses{}"/>
###### Game.getHouses()
> **Description:** Get all houses.  
> **Parameters:** None  
> **Returns:** A table containing all houses (userdata).  
> **Example:** 
```Lua
-- This prints the names of all houses that exist on the server
local houses = Game.getHouses()
for i = 1, #houses do
	print(houses[i]:getName())
end
```
> **Added in version:** 1.0

***

<a name="Game.getMonsterCount{}"/>
###### Game.getMonsterCount()
> **Description:** Find the total amount of monsters on the server.  
> **Parameters:** None  
> **Returns:** Total amount of monsters on the server.  
> **Example:** 
```Lua
print(Game.getMonsterCount())
```
> **Added in version:** 1.0

***

<a name="Game.getNpcCount{}"/>
###### Game.getNpcCount()
> **Description:** Find the total amount of npcs on the server.  
> **Parameters:** None  
> **Returns:** Total amount of npcs on the server.  
> **Example:** 
```Lua
print(Game.getNpcCount())
```
> **Added in version:** 1.0

***

<a name="Game.getPlayerCount{}"/>
###### Game.getPlayerCount()
> **Description:** Find the total amount of players on the server.  
> **Parameters:** None  
> **Returns:** Total amount of players on the server.  
> **Example:** 
```Lua
print(Game.getPlayerCount())
```
> **Added in version:** 1.0

***

<a name="Game.getPlayers{}"/>
###### Game.getPlayers()
> **Description:** Get all connected players.  
> **Parameters:** None  
> **Returns:** A table containing all connected players (userdata).  
> **Example:** 
```Lua
-- This prints the names of all players connected to the server
local players = Game.getPlayers()
for i = 1, #players do
	print(players[i]:getName())
end
```
> **Added in version:** 1.0

***

<a name="Game.getReturnMessage{value}"/>
###### Game.getReturnMessage(value)
> **Description:** Gets a message associated with the value.  
> **Parameters:** <ul><li>_value_ - _Internal return value_</li></ul>
> **Returns:** true  
> **Example:** 
```Lua
-- This makes no sense but its an example.
local player = Player(...)
player:say(Game.getReturnMessage(RETURNVALUE_YOUARENOTTHEOWNER), TALKTYPE_SAY)
```
> **Added in version:** 1.0

***

<a name="Game.getSpectators{position[, multifloor = false[, onlyPlayer = false[, minRangeX = 0[, maxRangeX = 0[, minRangeY = 0[, maxRangeY = 0]]]]]]}"/>
###### Game.getSpectators(position[, multifloor = false[, onlyPlayer = false[, minRangeX = 0[, maxRangeX = 0[, minRangeY = 0[, maxRangeY = 0]]]]]])
> **Description:** Get all creatures in the area.  
> **Parameters:** <ul><li>_position_ - _Center position_</li><li>_multifloor_ - _Search multiple floors? (optional, default: false)_</li><li>_onlyPlayer_ - _Find only players? (optional, default: false)_</li><li>_minRangeX_ - _Minimum range on the x axis (optional, default: 0)_</li><li>_maxRangeX_ - _Maximum range on the x axis (optional, default: 0)_</li><li>_minRangeY_ - _Minimum range on the y axis (optional, default: 0)_</li><li>_maxRangeY_ - _Maximum range on the y axis (optional, default: 0)_</li></ul>
> **Returns:** A table containing creatures found (userdata).  
> **Example:** 
```Lua
-- This finds all players in a 5x5 area around (100, 100, 7)
local spectators = Game.getSpectators(Position(100, 100, 7), false, true, 0, 2, 0, 2)
for i = 1, #spectators do
	local spectator = spectators[i]
	spectator:say(spectator:getName(), TALKTYPE_SAY)
end
```
> **Added in version:** 1.0

***

<a name="Game.getTowns{}"/>
###### Game.getTowns()
> **Description:** Get all towns.  
> **Parameters:** None  
> **Returns:** A table containing all towns (userdata).  
> **Example:** 
```Lua
-- This prints the names of all towns that exist on the server
local towns = Game.getTowns()
for i = 1, #towns do
	print(towns[i]:getName())
end
```
> **Added in version:** 1.0

***

<a name="Game.getWorldType{}"/>
###### Game.getWorldType()
> **Description:** Gets the current world type.  
> **Parameters:** None  
> **Returns:** Current gamestate on the server.  
> **Example:** 
```Lua
print(Game.getWorldType())
```
> **Added in version:** 1.0

***

<a name="Game.loadMap{path}"/>
###### Game.loadMap(path)
> **Description:** This loads a new map chunk.  
> **Parameters:** <ul><li>_path_ - _File path to the map._</li></ul>
> **Returns:** Nothing  
> **Example:** 
```Lua
Game.loadMap("data/map/some_other_map.otbm")
```
> **Added in version:** 1.0

***

<a name="Game.setGameState{state}"/>
###### Game.setGameState(state)
> **Description:** Sets the current gamestate.  
> **Parameters:** <ul><li>_state_ - _The new gamestate_</li></ul>
> **Returns:** true  
> **Example:** 
```Lua
-- Shutdown the server
Game.setGameState(GAME_STATE_SHUTDOWN)
```
> **Added in version:** 1.0

***

<a name="Game.setWorldType{type}"/>
###### Game.setWorldType(type)
> **Description:** Sets the current world type.  
> **Parameters:** <ul><li>_type_ - _The new world type_</li></ul>
> **Returns:** true  
> **Example:** 
```Lua
-- Change to hardcore pvp
Game.setWorldType(WORLD_TYPE_PVP_ENFORCED)
```
> **Added in version:** 1.0

***

<a name="Game.startRaid{raidName}"/>
###### Game.startRaid(raidName)
> **Description:** Starts a raid if one with said name exist.  
> **Parameters:** <ul><li>_raidName_ - _Name of the raid._</li></ul>
> **Returns:** true if the raid started, nil otherwise.  
> **Example:** 
```Lua
if Game.startRaid("test") then
	-- Raid was started.
end
```
> **Added in version:** 1.0

###Global
####Available methods:
[addEvent(callback, delay, ...)](#addEvent{callback, delay, ...})  
[stopEvent(eventid)](#stopEvent{eventid})  


***

<a name="addEvent{callback, delay, ...}"/>
###### addEvent(callback, delay, ...)
> **Description:** This function is used to run other functions at a later time.  
> **Parameters:** <ul><li>_callback_ - _The function that should run at a later time._</li><li>_delay_ - _Time before the callback runs in milliseconds._</li><li>_..._ - _This can expand into any amount of variables, they are sent to the callback when it runs. (optional)_</li></ul>
> **Returns:** The id associated with this event.  
> **Example:** 
```Lua
-- Creates an event that prints "Hello World!" to the console.
addEvent(print, 1000, "Hello World!")
```
> **Added in version:** 1.0

***

<a name="stopEvent{eventid}"/>
###### stopEvent(eventid)
> **Description:** This function is used to stop functions that should run later.  
> **Parameters:** <ul><li>_eventid_ - _The event id to stop._</li></ul>
> **Returns:** true if an event was stopped, false otherwise.  
> **Example:** 
```Lua
-- Creates an event that should print "Hello World!" but it's stopped before that can happen.
local event = addEvent(print, 1000, "Hello World!")
stopEvent(event)
```
> **Added in version:** 1.0

###os
####Available methods:
[mtime()](#os.mtime{})  


***

<a name="os.mtime{}"/>
###### os.mtime()
> **Description:** Returns the Unix time (epoch) in milliseconds  
> **Parameters:** None  
> **Returns:** The Unix time (epoch) in milliseconds  
> **Example:** 
```Lua
print(os.mtime() .. " milliseconds have passed since the Unix epoch")
```
> **Added in version:** 1.0

###table
####Available methods:
[create(arrayLength, keyLength)](#table.create{arrayLength, keyLength})  


***

<a name="table.create{arrayLength, keyLength}"/>
###### table.create(arrayLength, keyLength)
> **Description:** Creates a new table with specified length.  
> **Parameters:** <ul><li>_arrayLength_ - _Ordered indexes (1, 2, ...arrayLength)_</li><li>_keyLength_ - _Unordered indexes (anything that does not follow the above)_</li></ul>
> **Returns:** The created table.  
> **Example:** 
```Lua
local t = table.create(5, 0)
for i = 1, #t do
	t[i] = i + 1
end
```
> **Added in version:** 1.0
