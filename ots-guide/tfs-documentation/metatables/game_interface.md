# Game

* [Game.getSpectators()](game\_interface.md#game-getspectators)
* [Game.getPlayers()](game\_interface.md#game-getplayers)
* [Game.loadMap()](game\_interface.md#game-loadmap)
* [Game.getExperienceStage()](game\_interface.md#game-getexperiencestages)
* [Game.getMonstersCount()](game\_interface.md#game-getmonsterscount)
* [Game.getPlayersCount()](game\_interface.md#game-getplayerscount)
* [Game.getNpcCount()](game\_interface.md#game-getnpccount)
* [Game.getMonsterTypes()](game\_interface.md#game-getmonstertypes)
* [Game.getTowns()](game\_interface.md#game-gettowns)
* [Game.getHouses()](game\_interface.md#game-gethouses)
* [Game.getGameState()](game\_interface.md#game-getgamestate)
* [Game.setGameState()](game\_interface.md#game-setgamestate)
* [Game.getWorldType()](game\_interface.md#game-getworldtype)
* [Game.setWorldType()](game\_interface.md#game-setworldtype)
* [Game.getReturnMessage()](game\_interface.md#game-getreturnmessage)
* [Game.createItem()](game\_interface.md#game-createitem)
* [Game.createContainer()](game\_interface.md#game-createcontainer)
* [Game.createMonster()](game\_interface.md#game-getmonsterscount)
* [Game.createNpc()](game\_interface.md#game-createnpc)
* [Game.createTile()](game\_interface.md#game-createitem)
* [Game.createMonsterType()](game\_interface.md#game-createmonstertype)
* [Game.startRaid()](game\_interface.md#game-startraid)
* [Game.getClientVersion()](game\_interface.md#game-getclientversion)
* [Game.reload()](game\_interface.md#game-reload)

{% hint style="success" %}
Parameters in square brackets "\[parameter]" are optional

and their default value is specified after the name e.g "= false"
{% endhint %}

### Game.getSpectators()

position\[, multifloor = false\[, onlyPlayer = false\[, minRangeX = 0\[, maxRangeX = 0\[, minRangeY = 0\[, maxRangeY = 0]]]]]]

{% hint style="danger" %}
This method is pretty heavy (excessive usage might be affecting performance)
{% endhint %}

```lua
local position = Position(1000, 1000, 7)
local spectators = Game.getSpectators(position, false, true, 10, 10, 10, 10)
-- get all spectators from position in radius of 10 vertically and horizontally
for _, spectator in ipairs(spectators) do
    -- iterates over all spectators and prints their type
    print(type(spectator)) -- prints userdata
end
```

### Game.getPlayers()

```lua
local players = Game.getPlayers()
print(#players) -- prints players online
for _, player in ipairs(players) do
    -- iterate through players online and print their names
    print(player:getName()
end
```

### Game.loadMap()

path

```lua
Game.loadMap("/data/world/map.otbm")
```

### Game.getExperienceStage()

level

```lua
local experienceStage = Game.getExperienceStages(100)
print(experienceStage) -- prints current experience stage for level 100
```

### Game.getMonstersCount()

```lua
local monstersCount = Game.getMonstersCount()
print(monstersCount) -- prints number of alive monsters
```

### Game.getPlayersCount()

```lua
local playersCount = Game.getPlayersCount()
print(playersCount) -- prints number of players online
```

### Game.getNpcCount()

```lua
local npcCount = Game.getNpcCount()
print(npcCount) -- prints number of npcs
```

### Game.getMonsterTypes()

```lua
local monsterTypes = Game.getMonsterTypes()
for _, monsterType in ipairs(monsterTypes) do
    -- iterates through monster types and prints their names
    print(monsterType:getName())
end
```

### Game.getTowns()

```lua
local towns = Game.getTowns()
for _, townin ipairs(towns) do
    -- iterates through towns and prints their names
    print(town:getName()) TODO FIND THE METHOD
end
```

### Game.getHouses()

```lua
local houses = Game.getHouses()
for _, house in ipairs(houses) do
    -- iterates through houses and prints their owners guid
    print(house:getOwnerGuid())
end
```

### Game.getGameState()

```lua
local gameState = Game.getGameState()
if gameState == GAME_STATE_CLOSED then
    -- checks if server is closed, if it's then open it
    Game.setGameState(GAME_STATE_NORMAL)
end
```

### Game.setGameState()

state

```lua
Game.setGameState(GAME_STATE_NORMAL) -- sets game state to state normal
```

### Game.getWorldType()

```lua
local worldType = Game.getWorldType()
print(worldType) -- prints currently set world type ex. WORLD_TYPE_PVP
```

### Game.setWorldType()

worldType

```lua
Game.setWorldType(WORLD_TYPE_NO_PVP) -- sets current world type to non pvp
```

### Game.getReturnMessage()

returnValue

```lua
local player = Player(...)
if player then
    local returnMessage = Game.getReturnMessage(RETURNVALUE_NOTPOSSIBLE)
    print(returnMessage) -- prints Sorry not possible.
    player:sendCancelMessage(returnMessage)
end
```

### Game.createItem()

itemId\[, count\[, position]]

```lua
local item = Game.createItem(2160)
print(item) -- prints memory address
-- at this point item was created, but not added to anywhere, so it's stored in memory
-- either add it to any container
container:addItemEx(item)
-- or delete it to avoid memory leak
item:remove()

item = Game.createItem(2160, 1, Position(1001, 1000, 7)
print(item:getPosition().x) -- prints 1001
```

### Game.createContainer()

itemId, size\[, position]

```lua
local container = Game.createContainer(1987, 10)
print(container) -- prints memory address
-- at this point container was created, but not added to anywhere, so it's stored in memory
-- either add it to any container
container:addItemEx(container)
-- or delete it to avoid memory leak
container:remove()

container = Game.createContainer(2160, 10, Position(1001, 1000, 7)
print(container:getPosition().x) -- prints 1001
```

### Game.createMonster()

monsterName, position\[, extended = false\[, force = false]]

{% hint style="info" %}
**extended** means monster can be spawned in area near the specified position

**force** means monster will be always spawned in specified position, even if position is blocked
{% endhint %}

```lua
local monster = Game.createMonster("rat", Position(1000, 1000, 7), false, true)
if monster then
    print(monster:getId()) -- prints monster unique id
end
```

### Game.createNpc()

npcName, position\[, extended = false\[, force = false]]

```lua
local npc = Game.createNpc("Nekiro", Position(1000, 1000, 7), false, true)
if npc then
    print(npc:getId()) -- prints npc unique id
end
```

### Game.createTile()

x, y, z\[, isDynamic = false]

position\[, isDynamic = false]

{% hint style="info" %}
Dynamic tiles can store items and creatures, in most cases **walkable** one. (They take more memory too)
{% endhint %}

```lua
local tile = Game.createTile(1001, 1000, 7, false)
-- or Game.createTile(Position(1001, 1000, 7), false)
if tile then
    print(tile:getPosition().x) -- prints 1001
end
```

### Game.createMonsterType()

name

{% hint style="danger" %}
This method can **overwrite** already created monster types and **clear** their loot and spells
{% endhint %}

```lua
local newMonsterType = Game.createMonsterType("SpecialRat")
-- creates new (or overwrites if exists) monster type
if newMonsterType then
    print(newMonsterType:getName()) -- prints SpecialRat
end
```

### Game.startRaid()

raidName

{% hint style="warning" %}
This method might get soon deprecated in favor of raid system written in Lua
{% endhint %}

```lua
Game.startRaid("RatsThais") -- starts raid with name RatsThais
```

### Game.getClientVersion()

```lua
local clientVersion = Game.getClientVersion()
print(clientVersion) -- prints table: 0x93ff90

-- prints min and max allowed client version and version string
print(clientVersion.min, clientVersion.max, clientVersion.string)
```

### Game.reload()

reloadType

```lua
Game.reload(RELOAD_TYPE_GLOBAL) -- reloads all libs
Game.reload(RELOAD_TYPE_ACTIONS) -- reloads all actions
-- and so on...
```
